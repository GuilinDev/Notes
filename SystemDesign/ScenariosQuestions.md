<details>
<summary><h4>1. If we are dealing with a read-heavy system, it’s good to consider?</h4></summary>

### Cache

</details>

<details>
<summary><h4>2. If we need low latency in system, it’s good to consider using?</h4></summary>

### Cache & CDN.

</details>

<details>
<summary><h4>3. If we are dealing with a write-heavy system, it’s good to consider using?</h4></summary>

### Message Queue for Async processing.

</details>

<details>
<summary><h4>4. If we need a system to be ACID complaint, we should go for?</h4></summary>

### RDBMS or SQL Database.

</details>

<details>
<summary><h4>5. If data is unstructured & doesn’t require ACID properties, we should go for?</h4></summary>

### NO-SQL Database.

</details>

<details>
<summary><h4>6. If the system has complex data in the form of videos, images, files etc, we should go for?</h4></summary>

### Blob / Object storage (S3, GCS, Azure Blob Storage).

</details>

<details>
<summary><h4>7. If the system requires complex pre-computation like a news feed, we should consider using?</h4></summary>

### Message Queue & Cache.

</details>

<details>
<summary><h4>8. If the system requires searching data in high volume, we should consider using?</h4></summary>

### [search index](https://use-the-index-luke.com/), tries or search engine like Elasticsearch.

</details>

<details>
<summary><h4>9. If the system requires to Scale SQL Database, we should consider using?</h4></summary>

### Database Sharding.

</details>

<details>
<summary><h4>10. If the system requires High Availability, Performance, and Throughput, we should consider using?</h4></summary>

### Load Balancer.

</details>

<details>
<summary><h4>11. If the system requires faster data delivery globally, reliability, high availability, and performance, we should consider?</h4></summary>

### CDN.

</details>

<details>
<summary><h4>12. If the system has data with nodes, edges, and relationships like friend lists, and road connections, we should consider using?</h4></summary>

### Graph Database.

</details>

<details>
<summary><h4>13. If the system needs scaling of various components like servers, databases, etc, we should consider using?</h4></summary>

### Horizontal Scaling.

</details>
<details>
<summary><h4>14. If the system requires high performing database queries, we should consider using?</h4></summary>

### [Database Indexes](https://use-the-index-luke.com/).

</details>

<details>
<summary><h4>15. If the system requires bulk job processing, we should consider using?</h4></summary>

### Batch Processing & Message Queues.

</details>

<details>
<summary><h4>16. If the system requires reducing server load and preventing DOS attacks, we should consider using?</h4></summary>

### Rate Limiter.

</details>

</details>

<details>
<summary><h4>17. If the system has microservices, we should consider using?</h4></summary>

### API Gateway (Authentication, SSL Termination, Routing etc) & Service Discovery.

</details>

</details>

<details>
<summary><h4>18. If the system has a single point of failure, what we should implement in that component?</h4></summary>

### Redundancy.

</details>

</details>

<details>
<summary><h4>19. If the system needs to be fault-tolerant, and durable, we should implement?</h4></summary>

### Data Replication (creating multiple copies of data on different servers).

</details>

</details>

<details>
<summary><h4>20. If the system needs user-to-user communication (bi-directional) in a fast way, we should consider using?</h4></summary>

### Websockets.

</details>

</details>

<details>
<summary><h4>21. If the system needs the ability to detect failures in a distributed system, we should consider implementing?</h4></summary>

### Heartbeat.

</details>

</details>

<details>
<summary><h4>22. If the system needs to ensure data integrity, we should consider implementing?</h4></summary>

### [Checksum Algorithm](https://docs.google.com/presentation/d/1Cpx-P8_sJ9MhPgx44B22UibcX2bgpT5Tg7kqjxifOfc/edit?usp=sharing).

</details>

</details>

<details>
<summary><h4>23. If the system needs to transfer data between various servers in a decentralized way, we should go for?</h4></summary>

### [Gossip Protocol](https://docs.google.com/presentation/d/1Cpx-P8_sJ9MhPgx44B22UibcX2bgpT5Tg7kqjxifOfc/edit?usp=sharing).

</details>

</details>

<details>
<summary><h4>24. If the system needs to scale servers with add/removal of nodes efficiently, no hotspots, we should implement?</h4></summary>

### Consistent Hashing.

</details>

</details>

<details>
<summary><h4>25. If the system needs anything to deal with a location like maps, nearby resources, we should consider using?</h4></summary>

### [Quadtree, Geohash etc.](https://docs.google.com/presentation/d/1Cpx-P8_sJ9MhPgx44B22UibcX2bgpT5Tg7kqjxifOfc/edit?usp=sharing)

</details>