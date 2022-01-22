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

now login with
`psql -U postgres`
