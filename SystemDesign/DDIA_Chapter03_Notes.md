## Introduction
* Databases fundamentally does two things: **Store** data and **retrieve** the stored data.
* Chapter 3 discusses how data model and queries are interpreted by databases.
* Understanding under-the-hood details can help us pick the right solution and tune the performance.
* We’ll first look at two types of storage engines: **log-structured** and **page-oriented** storage engines.

## Data Structures Thank Power Your Database
* Many databases internally uses a log, which is an **append-only** data file.
* To retrieve data efficiently, we need an **index**, which is an additional structure derived from primary data and only affects performance of queries.
* Well-chosen indexes speed up queries but **slow down writes**. Therefore, databases don’t index everything by default and requires developers to use knowledge of query pattens to choose index manually.

### Hash Indexes
* Hash Indexes are for key-value data** and are similar to a dictionary, which is usually implemented as a hash map (hash table).
* If the database writes only append new entries to a file, the hash table can simply store key to byte offset in the data file. The hash table (with keys) has to fit into **memory** for quick look up performance, but the values don’t have to fit into memory.
* To avoid the disk run out of space, a good solution is to break logs into **segments** and perform **compaction** (remove duplicate keys). Further, file segments can be merged while performing compaction. We can use a background thread to perform merging and compaction and switch our read request to the newly created segment when they are read. Afterwards, old segments can be deleted.
* There are a few details for a real implementation of the idea above
  * Use bytes instead of CSV
  * Deletes are adding a special log entry to the data file (tombstone) and the data will be removed during merging and compaction.
  * Index will need to be snapshotted for fast crash recovery (compared to re-indexing).
  * Checksums are required for detecting partially written records.
  * Writes have to strictly be in sequential order. Many implementation choose to have one writer thread.
* Why append-only logs are good
  * Sequential writes are much faster than random writes, especially on magnetic spinning-disk hard drives and to some extent SSDs.
  * Concurrency and crash recovery are much simpler if segment files are append-only or immutable.
  * Merging old segments avoids data fragmentation.
* What are the limitations of hash table indexes?
  * Hash table must fit into memory. If there are too many keys, it will not fit.
  * Range queries are not efficient.

### SStables and LSM-Trees
* The Sorted String Table (SSTable) requires each segment file to be sorted by key. It has the following advantages.
  * Merging segments is simple and efficient.
  * We no longer require offset of every single key for efficient lookup. One key for every few kilobytes of segment file is usually sufficient.
  * Since reading requires a linear scan in between indexed keys, we can group those records and compress them to save storage or I/O bandwidth.

#### Constructing and Maintaining SStables
* While maintaining a sorted structure on disk is possible (B-Trees), red-black trees or AVL trees can be used to keep logs sorted in memory. The flow is as follows:
  * When a write comes in, insert the entry to the in-memory data structure (sometimes called memtable).
  * When memtable gets bigger than some threshold (a few megabytes), create a new memtable to handle new writes, and write the old memtable to disk.
  * For reads, first try to find the key in memtable, and in the latest segment, and in the second last segment…
  * Occasionally, run a merging and compaction process to combine segment files.
* The issue with this scheme is that in-memory data will be lost if the database crashes. We can keep a separate unsorted log for recovery and this log can be discarded whenever a memtable is dumped to disk.
* This indexing structure is named Log-Structure Merge-Tree (LSM-Tree).

#### Making an LSM-tree out of SSTables
* The algorithm here is used by LevelDB and RocksDB, which are key-value storage libraries to be used in other applications. Similar storage systems are also used in Cassandra and HBase.
* Systems that uses the principle of merging and compacting sorted files are often called LSM systems.

#### Performance Optimizations
* A look-up can take a long time if the entry does not exist in any of the memtable. Bloom filters can be used to solve this issue.
* There are two major strategies to determine the order and timing of merging and compaction: size-tiered (HBase, Cassandra) and level compaction (LevelDB, RockDB, Cassandra).
  * Size-tiered: newer and smaller SSTables are merged into larger ones.
  * Level: The key range is split up into several SSTables and older data is moved to separate “levels,” which allows compaction to proceed more incrementally and use less disk space.
* LSM-tree: Write throughput is high. Can efficiently index data much larger than memory.

### B-Trees
* While log-structured indexes are gaining acceptance, B-tree is the most widely used indexing structure.
* B-trees is the standard index implementation for almost all relational databases and most non-relational databases.
* B-trees also keep key-value entires sorted by key, which allows quick value lookups and range queries.
* Log-structure indexes breaks databases down into variable length segments (several mbs or more), while B-tree breaks databases down into a fixed-size blocks or pages (4KB traditionally, but depends on underlying hardware).
* Each page can be identified by an address or location, which can be stored in another page on disk.
* A root page contains the full range of keys (or reference to pages containing the full range) and is where query start.
* A leaf page contains only individual keys, which contains the value inline or reference to where the values can be found.
* The branching factor is the number of references to a child page in one page of a B-tree.
* When changing values in B-trees, the page containing the value is looked up, modified, and written back to disk.
* When adding new values, first, the page whose range contains the key is looked up. If there is extra space in the page, the key-value entry is simply added, else, the page is split into two halves and the parent page is updated to account for the new file structure.
* The algorithm above ensures a B-tree with n nodes is always balanced and has a depth of _O(log n)_.

#### Making B-Trees Reliable
* When changing values or splitting pages, the B-tree overwrites data on disk. This is a risky operation. If anything crashes during an overwrite, the index could be corrupted.
* To make B-tree more resilient to such failures, a common solution is to include an write-ahead-log (WAL, or redo log), which every B-tree modification is first written to. In case of failure, this log can be used to restore the B-tree back to a consistent state.
* Care should also be taken when multiple threads may access the B-tree at the same time. An inconsistent state could be read during an update. Latches (lightweight locks) can be placed to protect the tree’s integrity.

#### B-Tree Optimization 
* Just to mention a few optimizations:
  * Copy-on-write and atomic to remove the need to maintain a WAL for crashes
  * Key compression by storing essential information for acting as boundaries.
  * Arrange page on disk such that pages appear in sequential order on disk.
  * Additional pointers (such as left, right siblings) to allow efficient scanning of keys in order without jumping back to parents.
  * Fractal trees to reduce disk seeks.

### Comparing B-Trees and LSM-Trees
* Typically, B-Trees are faster for reads and LSM-Trees are faster for writes. The actual performance for a specific system would require benchmarking.

#### Advantages of LSM-Trees
* Both B-Tree and LSM-tree indexes would require writing a piece of data to disk multiple times on write. This effect is known as write amplification. In write heavy applications, write amplification would directly impact performance.
* LSM-trees are typically able to sustain higher write throughput due to two main reasons: a lower write amplification and a sequential write (especially on magnetic hard drives).
* LSM-trees can be compressed better and have lower fragmentation due to rewriting of SSTables.
* Even on SSDs, LSM-trees are still advantages as it represents data more compactly and allows more read and write requests within the same bandwidth.

#### Downsides of LSM-Trees
* The compaction process of LSM-trees can sometimes interfere with reads and writes, as reads and writes can be blocked by the compaction process on disk resources. Although the impact on average response time is usually small, this could greatly increase high-percentage response time.
* If write throughput is high and compaction is not configured correctly, it is not impossible that compaction can’t keep up with incoming writes. Unmerged segments will then grow until disk space is all used. This effect has to be actively monitored.
* Since each key only appears once in a B-tree, B-trees are more attractive in databases when transaction isolation is implemented using locks on range of keys.

### Other Indexing Structures
* Secondary indexes can be created from a key-value index. The main difference between primary and secondary indexes is that secondary indexes are not unique. This can be solved two ways:
  * Make the value in the index a list of matching row identifiers.
  * Make each key unique by adding a row identifier to the secondary key.
* Both B-trees and log-structured indexes can be used as secondary indexes.

#### Storing Values within the Index
* In a key-value pair, the key is used to locate the entry and the value can be either the actual data or a reference to the storage location (known as a heap file). Using heap files is common for building multiple secondary indexes to reduce duplication.
* When updating values without changing keys, if the new value is no larger than old data, the value can be directly overwritten, and if the new value is larger, either all indexes needs to be updated or a forwarding pointer can be left in the old record.
* Sometimes, the extra hop to the heap file is too expensive for reads, and the indexed row is stored directly in the index. This is called a clustered index.
* A compromise between a non-clustered index and a clustered index is a covering index or index with included columns, where only some columns are stored within the index.

#### Multi-Column Indexes
* Multi-column indexes are created for querying rows using multiple columns of a table.
* The concatenate index is the most common multi-column index. This is done by simply concatenating fields together into one key. However the index is useless when a query is based on only one column.
* To index a two-dimensional location database (with latitude and longitude), we can use a space-filling curve and use a regular B-tree index. Specialized spatial index such as R-trees are also used.

#### Full-Text Search and Fuzzy indexes
* Full-text search indexes are used to search for words in a document. The most common way is to use a trie, which is a tree where each node represents a letter and each path from the root to a leaf represents a word.
* Fuzzy indexes are used to search for words that are similar to a given word. This is done by using a hash function to map words to a fixed-length integer. The hash function is chosen such that words that are similar to each other will have similar hash values. The hash value is then used as the key in a B-tree index.
* Some applications require searching for a similar key. This can be done by fuzzy indexes.
* For example, Lucene allows searching for words within edit distance 1. In Lucene, the in-memory index is a finite state automaton over the characters in the keys (similar to a trie). This automaton can then be transformed into a Levenshtein automaton, which supports efficient search for words within a given distance.

#### Keeping Everything in Memory
* In-memory indexes are used when the data is too large to fit in memory. The main advantage is that reads and writes are much faster. The main disadvantage is that the data is lost when the system crashes.
* To make the index more resilient to crashes, the index can be periodically flushed to disk. This is known as a checkpoint.
* Some in-memory key-value stores, such as Memcached, are intended for caching only, where data is lost when the machine restarts. Some other in-memory databases aim for durability, which can be achieved with special hardware and saving change logs and snapshots to disk.
* Counterintuitively, in-memory databases are faster mainly because they avoid serialization and deserialization between in-memory structures and binaries, not because of the disk read and write time.
* In-memory databases could also provide data models that are hard to implement with disk-based indexes, such as priority queues, stacks.
* The anti-caching approach, where the least-recently-used data is dumped to disk when there is not enough memory and loaded back when queried, enables in-memory databases to support larger-than-memory databases. Yet the index would still have to fit into memory.

## Transaction Processing or Analytics?
* Transaction processing systems are used to process transactions, such as online banking, where the data is updated frequently and the queries are simple.
* Analytics systems are used to process large amounts of data, such as web logs, where the data is updated infrequently and the queries are complex.
* The term transaction (an entry) was coined in the early days of databases, where commercial transactions were the main entries in databases. Although the data in databases are now different, the access pattern: looking up a few entries by key, inserting or updating data based on user input, remains the same and is referred to as online transaction processing (OLTP).
* Databases nowadays are also used for data analytics. The access pattern: scanning through the whole database and performing aggregation, is a very different from OLTP. This pattern is referred to as the online analytic processing (OLAP).

|  | OLTP | OLAp |
|----------|----------|----------|
| Main read pattern | Small number of records, fetched by key | Aggregated over large number of records |
| Main write pattern | Random-access, low-latency writes from user input | Bulk import or event stream |
| Primarily used by | Customer, through web-application | Analysts, for making business decisions |
| Data | 	Latest state of the world | History of events |
| Size | GB to TB | TB to PB |
| Bottleneck | Disk seek time | Disk bandwidth |

* Starting 1980s, people stopped using OLTP systems for OLAP applications. The data for analytics is hosted in a separate database - a data warehouse.

### Data Warehousing
* OLTP is expected to be highly available with low latency, so it is not ideal to run analytics on OLTP databases.
* A data warehouse contains a read-only copy of the data in OLTP systems through periodic dumps or stream of updates.
* The process of getting data from OLTP systems to data warehouses is called Extract-Transform-Load (ETL).
* Data warehouses, separate from OLTP systems, can be optimized for analytics access patterns.
* The indexing algorithms mentioned above are for OLTP systems, not analytics.

#### The Divergence between OLTP Databases and Data Warehouses
* Although most data warehouses use a relational data model, the internals of the systems is very different as they are optimized for different access patterns.
* Although some products combines OLTP with data warehousing (Microsoft SQL, SAP HANA), they are increasingly becoming two separate systems.

### Stars and Snowflakes: Schemas for Analytics
* Many data warehousing systems uses a star-schema, whose center is a fact table, where each row represents an event. The fact table uses foreign keys to refer to other tables (called dimension tables) for entities (with extra information) that was involved in the event.
* The snowflake schema further breaks dimensions down into sub-dimensions. Snowflake schemas are more normalized than star schemas, but star schemas are easier for analysts to work with.
* A typical data warehouse, tables could be very wide (up to several hundred columns), and dimension tables could also be very wide.

## Column-riented Storage
* A typical data warehouse query only access several rows.
* The data in a row-oriented database is stored in rows, where each row is a tuple of values. The data in a column-oriented database is stored in columns, where each column is a tuple of values.
* In most OLTP and document databases, storage is laid out in a row-oriented fashion, meaning all data from one row are stored next to each other. This is inefficient for queries which only accesses a few columns of all rows. The whole row will have to be read and filtered down to the columns of interest.
* In column-oriented storage, data of all rows from each column are stored together. It relies on each file containing the rows in the same order.

### Column Compression
* Column-oriented storage often lends itself to good compression.
* Bitmap encoding of distinct values in a column can lead to good compression. Further, if the bitmap is sparse, we can use run-length encoding for more compression.
* Bitmap indexes are good for “equal” and “contain” queries.

#### Memory Bandwidth and Vectorized Processing
* Disk is not the only bottleneck. Bandwidth between memory and CPU, branch misprediction and [bubbles](https://en.wikipedia.org/wiki/Pipeline_stall) in CPU instruction processing pipeline, and using SIMD instructions all could be points of optimization.
* Column-oriented storage also uses CPU cycles efficiently, since the query engine can fit a chunk of compressed column data could fit into L1 cache and iterate it through a tight loop (without function calls).
* Also, operators can be designed to operate on such chunks of data directly. This is called [vectorized processing](https://en.wikipedia.org/wiki/Vector_processor).

### Sort Order in Column Storage
* Although storing column in insertion order is easy, we can choose to sort them based on what queries are common.
* The administrator can specify a column for the database to be sorted in as well as a second column to break ties.
* The sorted columns would be much easier to compress if there are not a lot of distinct values in the column.

#### Several Different Sort Orders
* Since data warehouse usually store multiple copies of the same data, it could use a different sort order for each replication, so that we can use different datasets for different queries.
* An analogy of multiple sorted orders to row-based databases is multiple secondary indexes. The difference is that row-based databases stores the data in one place and use pointers in secondary indexes, while column stores don’t use any pointers.

### Writing to Column0-Oriented Storage
* Sorted columns optimizes for read-only queries, yet writes are more difficult.
* In-place updates would require rewriting the whole column on every write. Instead, we can use a LSM-tree like structure where a in-memory store buffers the new writes. When enough new writes are accumulated, they are then merged with the column files and written to new files in bulk.
* Queries, in this case, would require reading data from both disk and the in-memory store. This will be hidden within the engine and invisible to the user.

### Aggregation: Data Cubes and Materialized Views
* Data cubes are precomputed aggregations of the data. They are used to speed up queries.
* Since many queries involves aggregation functions, a data warehouse can cache materialized aggregates to avoid recomputing expensive queries.
* One way of creating such a cache is a materialized view, which is defined like a standard view, but with results stored on disk, while virtual views are expanded and processed at query time.
* Updating materialized view, when data changes, is expensive, and therefore materialized views are not used in OLTP systems often.
* A common special case of materialized view is a data cube or OLAP cube, where data is pre-summarized over each dimension. This enables fast queries with precomputed queries, yet a data cube may not have the flexibility as raw data.

