- [Data Modeling Patterns in Redis](https://redis.com/blog/nosql-data-modeling/)
  collapsed:: true
	- The **Embedded** Pattern
	      One-to-one relationships
	- **Partial Embed** Pattern
	      One-to-many relationships
	      Many-to-many relationships
	          Pattern 1: Many-to-many relationships with bounded sides
	          Pattern 2: Many-to-many relationships with unbounded sides
	- The **Aggregate** Pattern
	- The **Polymorphic** Pattern
	- The **Bucket** Pattern
	- The **Revision** Pattern
	- The **Tree and Graph** Pattern
	- The **Schema Version** Pattern
- RESP2  vs RESP3
	- RESP3 can carry out-of-band / “push” messages on a single connection, where-as RESP2 requires a separate connection for these messages
	- RESP3 can (when appropriate) convey additional semantic meaning about returned payloads inside the same result structure
	- Some commands (see this topic) return different result structures in RESP3 mode; for example a flat interleaved array might become a jagged array
- data structure:
	- hashset:
- database: Redis by default have 16 databases that can be selected by using SELECT command.  since Redis Cluster only supports database zero.
- default ttl: -1, keep forever
- Syntax to flush Redis cache to clear redis cache
  ```bash
  redis-cli FLUSHDB
  redis-cli -n DB_NUMBER FLUSHDB
  redis-cli -n DB_NUMBER FLUSHDB ASYNC
  redis-cli FLUSHALL
  redis-cli FLUSHALL ASYNC
  ```
- redisinsight is free to use: 
  ```bash
  docker run -d --name redisinsight -v redisinsight:/db -p 8001:5540 redislabs/redisinsight:latest
  ```
- redis stack: In addition to all of the features of Redis OSS, Redis Stack supports:
  - Probabilistic data structures
  - Queryable JSON documents
  - Querying across hashes and JSON documents
  - Time series data support (ingestion & querying), including full-text search
- redis-commander: Redis web management tool written in node.js
  ```yaml
  version: '3'
  services:
    redis:
      container_name: redis
      hostname: redis
      image: redis
      ports:
          - "6379:6379"
      links: 
      - redis-commander

    redis-commander:
      container_name: redis-commander
      hostname: redis-commander
      image: rediscommander/redis-commander:latest
      build: .
      restart: always
      environment:
          - REDIS_HOSTS=redis
      ports:
          - "8081:8081"
  ```
- [C# Redis – Implementing Cache Tagging](https://stackify.com/implementing-cache-tagging-redis/)
  - issues:
    - tag-set growth: Redis only allows the expiration of entire entries – expiration cannot be set to a single value within any of Redis’ collection data types.
    - evit
- Redis Smart Cache: java ![Redis Smart Cache](https://raw.githubusercontent.com/redis-field-engineering/redis-smart-cache/master/src/media/redis-smart-cache-flow.png)
  