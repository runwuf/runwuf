# PgBouncer
* PgBouncer connection pooling modes: transaction (default), session and statement

# pghoard
* Aiven for PostgreSQL® databases are automatically backed up, with full backups made daily, and write-ahead logs (WAL) copied at 5 minute intervals, or for every new file generated.

# check replication lag on standby
`select NOW() - pg_last_xact_replay_timestamp()`
