# Kafka
* To make use of log compaction, all messages sent to the topic must have an explicit key.
* Compacted topic - only latest version of the key’s value is kept.
* Apache Kafka client trying to produce or consume messages might face warning "leader not found messages" as the partitions are moved between brokers.
* Topic ordering is guaranteed only per partition. If you require relative ordering of records, you need to put that subset of data into the same partition.
* Kafka Producer is thread-safe, but Consumer is NOT thread-safe

# Producer
* Bigger batches increase throughput but also increase the latency for individual messages. Conversely, using smaller batches decreases message processing latency, but the overhead per message increases and the overall throughput decreases. [batch.size] [linger.ms]
* acks ( how many ack before message is produced. acks=-1 means ALL)
* max.inflight.requests.per.connection (>1 can affect ordering unless enable.idemoptence is true)
* enable.idempotence (Ensuring exactly once )
* 

# Consumer
* partition.assignment.strategy - Range, RoundRobin, Sticky, Cooperative Sticky.
* group.instance.id - unique string to provide a consumer with static group membership.
* GroupCoordinator manages of consumer & offset. Broker where partition leader is located is the GroupCoordinator.
* ConsumerCoordinator is created first which is responsible for communicating with Group Coordinator
* __consumer_offsets is the topic used internally by Kafka to store group consumption.
* consumer poll(…) - check heartbear thread, subscribe to topic, if ConsumerCoordinator is unknown, send FindCoordinator request, Determine if you need to re-join a group. If subscription’s (or assigned) partition changes, you need to rejoin, send joinGroup request followed by syncGroup request, and finally ensureActiveGroup(..).
* Consumer Reblance - new consumer, consumer offline/no heartbeat, consumer unsubscribe from ConsumerGroup, topic partition # increased.
* subscribe() & assign() both cannot be called by same consumer and will lead to IllegalStateException
* To delay rebalance use group.initial.rebalance.delay.ms configuration
* max.poll.interval.ms → By increasing you give more time to consumer to handle batch of records returned from the poll. But increasing may delay consumer group rebalance since that happens inside call to poll()
* max.poll.records → To limit total number of records returned from single call to poll()

# Kafka Connect
* Kafka Connect -  try increasing tasks.max to match the number of partitions.
