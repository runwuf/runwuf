To make use of log compaction, all messages sent to the topic must have an explicit key.
Compacted topic: only latest version of the key’s value is kept. In the example above, only the current address for a specific user is kept.
Apache Kafka client trying to produce or consume messages might face warning "leader not found messages" as the partitions are moved between brokers.
Kafka Connect -  try increasing tasks.max to match the number of partitions.
Topic ordering is guaranteed only per partition. If you require relative ordering of records, you need to put that subset of data into the same partition.
Bigger batches increase throughput but also increase the latency for individual messages. Conversely, using smaller batches decreases message processing latency, but the overhead per message increases and the overall throughput decreases. [batch.size] [linger.ms]