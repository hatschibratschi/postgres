# General insight into the databases

## psql

`\c` connect to (other) database

## View running queries

`SELECT datname as database_name,usename as user_name,pid,query,query_start,
backend_start FROM pg_stat_activity ORDER BY pid;`

## pg_dump

### export create statement of table

`pg_dump your.db -t your.table --schema-only`

`pg_dump -U your_user your_database -t your_table --schema-only`

