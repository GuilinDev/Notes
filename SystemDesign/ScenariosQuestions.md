<details>
<summary><h3>1. If we are dealing with a read-heavy system, it’s good to consider?</h3></summary>

### A: Cache

</details>

<details>
<summary><h3>2. If we need low latency in system, it’s good to consider using?</h3></summary>

### A: Cache & CDN.

</details>

<details>
<summary><h3>3. If we are dealing with a write-heavy system, it’s good to consider using?</h3></summary>

### A: Message Queue for Async processing.

</details>

<details>
<summary><h3>4. If we need a system to be ACID complaint, we should go for?</h3></summary>

### A: RDBMS or SQL Database.

</details>

<details>
<summary><h3>5. If data is unstructured & doesn’t require ACID properties, we should go for?</h3></summary>

### A: NO- SQL Database.

</details>

<details>
<summary><h3>6. If the system has complex data in the form of videos, images, files etc, we should go for?</h3></summary>

### A: Blob / Object storage (S3, GCS, Azure Blob Storage).

</details>

<details>
<summary><h3>7. If the system requires complex pre-computation like a news feed, we should consider using?</h3></summary>

### A: Message Queue & Cache.

</details>

<details>
<summary><h3>8. If the system requires searching data in high volume, we should consider using?</h3></summary>

### A: [search index](https://use-the-index-luke.com/), tries or search engine like Elasticsearch.

</details>

<details>
<summary><h3>9. If the system requires to Scale SQL Database, we should consider using?</h3></summary>

### A: Database Sharding.

</details>

<details>
<summary><h3>10. If the system requires High Availability, Performance, and Throughput, we should consider using?</h3></summary>

### A: Load Balancer.

</details>

<details>
<summary><h3>11. If the system requires faster data delivery globally, reliability, high availability, and performance, we should consider?</h3></summary>

### A: CDN.

</details>

<details>
<summary><h3>12. If the system has data with nodes, edges, and relationships like friend lists, and road connections, we should consider using?</h3></summary>

### A: Graph Database.

</details>

<details>
<summary><h3>13. If the system needs scaling of various components like servers, databases, etc, we should consider using?</h3></summary>

### A: Horizontal Scaling.

</details>
<details>
<summary><h3>14. If the system requires high performing database queries, we should consider using?</h3></summary>

### A: [Database Indexes](https://use-the-index-luke.com/).

</details>

<details>
<summary><h3>15. If the system requires bulk job processing, we should consider using?</h3></summary>

### A: Batch Processing & Message Queues.

</details>

<details>
<summary><h3>16. If the system requires reducing server load and preventing DOS attacks, we should consider using?</h3></summary>

### A: Rate Limiter.

</details>

</details>

<details>
<summary><h3>17. If the system has microservices, we should consider using?</h3></summary>

### A: API Gateway (Authentication, SSL Termination, Routing etc) & Service Discovery.

</details>

</details>

<details>
<summary><h3>18. If the system has a single point of failure, what we should implement in that component?</h3></summary>

### A: Redundancy.

</details>

</details>

<details>
<summary><h3>19. If the system needs to be fault-tolerant, and durable, we should implement?</h3></summary>

### A: Data Replication (creating multiple copies of data on different servers).

</details>

</details>

<details>
<summary><h3>20. If the system needs user-to-user communication (bi-directional) in a fast way, we should consider using?</h3></summary>

### A: Websockets.

</details>

</details>

<details>
<summary><h3>21. If the system needs the ability to detect failures in a distributed system, we should consider implementing?</h3></summary>

### A: Heartbeat.

</details>

</details>

<details>
<summary><h3>22. If the system needs to ensure data integrity, we should consider implementing?</h3></summary>

### A: [Checksum Algorithm](https://docs.google.com/presentation/d/1Cpx-P8_sJ9MhPgx44B22UibcX2bgpT5Tg7kqjxifOfc/edit?usp=sharing).

</details>

</details>

<details>
<summary><h3>23. If the system needs to transfer data between various servers in a decentralized way, we should go for?</h3></summary>

### A: [Gossip Protocol](https://docs.google.com/presentation/d/1Cpx-P8_sJ9MhPgx44B22UibcX2bgpT5Tg7kqjxifOfc/edit?usp=sharing).

</details>

</details>

<details>
<summary><h3>24. If the system needs to scale servers with add/removal of nodes efficiently, no hotspots, we should implement?</h3></summary>

### A: Consistent Hashing.

</details>

</details>

<details>
<summary><h3>25. If the system needs anything to deal with a location like maps, nearby resources, we should consider using?</h3></summary>

### A: [Quadtree, Geohash etc.](https://docs.google.com/presentation/d/1Cpx-P8_sJ9MhPgx44B22UibcX2bgpT5Tg7kqjxifOfc/edit?usp=sharing)

</details>