Overview

This task involved fixing a failing replica in a Master/Replica setup using Docker Compose with PostgreSQL.

The master container was running correctly, but the replica was stuck in a restart loop.

Root Cause

In physical replication, some configuration parameters on the replica must be equal to or higher than the master.

The replica had lower values for the following parameters:

max_connections

max_locks_per_transaction

max_wal_senders

max_worker_processes

PostgreSQL refused to start the replica due to this mismatch.

Solution
1. Check master values
```
docker exec postgres-db-master psql -U helsingor helsingor -c "show max_connections;"
docker exec postgres-db-master psql -U helsingor helsingor -c "show max_locks_per_transaction;"
docker exec postgres-db-master psql -U helsingor helsingor -c "show max_wal_senders;"
docker exec postgres-db-master psql -U helsingor helsingor -c "show max_worker_processes;"
```

Master values:

max_connections = 100
max_locks_per_transaction = 64
max_wal_senders = 10
max_worker_processes = 8
2. Update replica config

Edit:
```
/home/admin/postgres/replica/postgres.conf
```

Set:
```
max_connections = 100
max_locks_per_transaction = 64
max_wal_senders = 10
max_worker_processes = 8
```
3. Recreate replica container
```docker compose up -d --force-recreate postgres-db-replica
```
Verification
```docker exec postgres-db-master psql -U helsingor helsingor -c "select * from pg_stat_replication;"```

If a row appears, replication is working.
