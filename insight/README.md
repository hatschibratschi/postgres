# General insight into the databases

## psql meta commands

`\c` connect to (other) database
`\l[+]` list databases

### Definitions

`\d[+] [pattern]` show all columns, their types, the tablespace (if not the default) and any special attributes such as NOT NULL or defaults of object.


### Stuff

`\h` help for sql commands
`\?` help for psql commands

### Links
* https://www.postgresql.org/docs/current/app-psql.html

## View running queries

`SELECT datname as database_name,usename as user_name,pid,query,query_start,
backend_start FROM pg_stat_activity ORDER BY pid;`

## pg_dump

### export create statement of table

`pg_dump your.db -t your.table --schema-only`

`pg_dump -U your_user your_database -t your_table --schema-only`

