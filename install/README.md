# Install on RaspberryPi
to install postgres on raspberry pi run

`install.pi.postgres.sh`

## Check status
Check status of your server with

`sudo service postgresql status`

## Set password
set new initial password for user postgres with

`sudo -iu postgres psql -c "\password postgres"`

change config to login on command line open the file 
`sudo vim /etc/postgresql/13/main/pg_hba.conf`
and change the line
`local   all             postgres                                peer`
to
`local   all             postgres                                md5`

restart the service with `sudo service postgresql restart`

now login with
`psql -U postgres`

## get version
`SELECT version();`

```
PostgreSQL 13.5 (Raspbian 13.5-0+deb11u1) on arm-unknown-linux-gnueabihf, compiled by gcc (Raspbian 10.2.1-6+rpi1) 10.2.1 20210110, 32-bit
```

## activate remote connection

in `/etc/postgresql/13/main/postgresql.conf` set listen addresses to eg:

`listen_addresses = '192.168.0.2, 192.168.0.3'`

and in `/etc/postgresql/13/main/pg_hba.conf` set IPv4 local connections to somthing like

`host    all             all             0.0.0.0/0               md5`


