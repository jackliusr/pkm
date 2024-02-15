- [How to Survive an Apache Kafka Outage](https://www.confluent.io/blog/how-to-survive-a-kafka-outage/)
- observers: Observers in Confluent Server are effectively asynchronous replicas. They replicate partitions from the leader just like the followers do, but they can never participate in the ISR or become a partition leader (unless the operator runs unclean leader election on an observer). What makes them asynchronous is the fact that they are never considered when incrementing the high watermark because they never join the ISR. This provides the following
	- benefits:
		- Relaxed physical distance and network requirements between DCs.
		- Improved data durability without sacrificing throughput.
		- Replication works across high-latency network connections with weak or unpredictable bandwidth. Since observers are effectively asynchronous replicas, this prevents them from falling in and out of sync with the ISR, also known as “ISR thrashing.”
		- A complement to [Follower Fetching](https://cwiki.apache.org/confluence/display/KAFKA/KIP-392%3A+Allow+consumers+to+fetch+from+closest+replica): The ability for a consumer to read from a replica instead of a leader. Having an observer in the same region as the consumers will allow consumers to read more cost effectively from the locally placed observer instead of trying to consume over the expensive high-latency network connection.
		- Disaster recovery benefits, such as automatic client failover.
	- ![](https://cdn.confluent.io/wp-content/uploads/observers-in-confluent-server-e1612991392335.png){:height 365, :width 594}
	- observerPromotionPolicy: under-min-isr, under-replicated, leader-is-observer
- issues: handling re-balancing, topic-partition offsets, etc