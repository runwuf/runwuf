# Redis
* repl-backlog-size (redis_repl_backlog_size_percent) is memory used to keep track of recent changes. This buffer is used by slaves to catch up fast after a reconnect instead of transferring the whole database. Replication buffer keeps the new updates to the master, till the RDB snapshot of master is transferred to the slave and is loaded into its memory. After this the data in the replication buffer is transferred to the slave.
* client-output-buffer-limit - max size we allow a replication buffer to grow.
