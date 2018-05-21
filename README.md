# Purpose #

Honeyguide is a project meant to assist the HCV Target team with data analysis using QUAIL to pull
data and redash as the front end.

# Getting started #

Make sure you have docker, docker-compose and an internet connection.

Copy the `fake.env` file and rename it to `.env`. See the following subsection for more information

Fill in the correct info. If you decide to change the redash password then make sure to change it
in the connection string as well.

Run `docker-compose up --build`

Run `./provision_redash_database.sh`

Go to `localhost:8080` and log into redash!

## ENV variables and what they do ##
NOTE: spaces are underscores in the file

|variable | explanation |
|---------|-------------|
|PG ADMIN DEFAULT PASS| default password for the pgadmin user|
|PG ADMIN DEFAULT USER|default username for the pgadmin user|
|PIP CAPPY CLONE URL|https url for the ctsit/cappy library|
|PIP QUAIL CLONE URL|https url for the ctsit/QUAIL library |
|PIP HAWKEYE CLONE URL|https url for the ctsit/hawkeye library|
|POSTGRES PASSWORD| the password for the postgres user on the postgres database
|QUAIL HOUR|the hour the quail cron job will run. changed at the image level
|QUAIL MINUTE|the minute the quail cron job will run. also image level|
|QUAIL REDCAP URL|the redcap url from which to pull data
|QUAIL TOKEN|the token to use for the redcap project. cannot be a super user token|
|REDASH COOKIE SECRET|some long random string|
|REDASH DATABASE URL|how redash connects to the database. this will need to match the REDASH PASSWORD variable|
|REDASH PASSWORD|the password for the redash database|


# Adding a datasource #

When using redash and adding a datasource you have two options. One is to use the postgres instance and
information, the other is to add the sqlite databases that are made by quail itself.

## Postgres databases ##

The only thing to note here is that the hostname of the postgres instance is the same as the key of the
service in the `docker-compose.yaml` file.

## Sqlite database ##

You can add the sqlite databases themselves as a redash datasource because they are mounted in the redash
container at `/quail_data`

# If a service is killed #

You need to increase the memory limit. There are different ways to do this based on how you are using
docker so you will have to look this up on your own.

# Running a pull without cron #

There is a script that can be run from the docker host once the containers are running that will
allow one to pull whenever they want.

# Reporting #

Hawkeye is installed on the system so once you set up the mail server you can respond to quail file creation
