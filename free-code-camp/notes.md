# Free code camp data engineer short tutorial

https://transparent-trout-f2f.notion.site/FreeCodeCamp-Data-Engineering-Course-Resources-e9d2b97aed5b4d4a922257d953c4e759

## Docker workshop

https://docs.docker.com/guides/workshop/

### download docker desktop and docker compose

### create dockerfile

### Build the app

### when need to update codes, have to remove and rebuild image

### data will be gone when stop and restart

### to persist data, create a volume (database) and then mount it to the container

### multi-container app

might need to build an image for MySQL, and another image for front-end app
will need to create a network to connect these two containers

### creating network

### create a MYSql container and then attach to the netwrok

### confirm database is created

### create another container (front-end app) and attach to the network, need to make sure to pass the info to use the MYSql database

### can use docker compose to simplify the process, need to create compose.yaml

### then run with docker compose

### shut down with docker compose

## SQL

### pull the latest postgres image and run it in a container

### create a new database inside postgres

### run postgres

### create a table

### now can run query against table

## Building data pipeline (ELT) using python, docker and postgres

### create files

elt_script.py
Dockerfile # a Dockerfile for elt_script.py so it can be depended on the other two containers, meaning it won't be built until both the sourse and destination container are ready
docker-compose.yaml
init.sql # initialize the volume

### elt_script.py

- check depended tasks
- config for source and destination
- command for dumping the data from the source database to data_dump.sql
- store environment in dictionary
- run dump command
- command for loading the data from data_dump.sql
- store environment in dictionary
- run load command

### run with docker compose (build image and start containers)

```bash
docker compose up
```

### connect to destination database and confirm

## dbt - custom models to transform data after loading

### create environment for the python project and create an alias for the activation command

### installing dbt-core and dbt-postgres (adapter)

```
pip install  dbt-postgres
```

### initialize a project and give a name

```bash
dbt init
```

### edit the dbt/profiles.yml file dbt created and fill out the info, nano is cli editor

```bash
nano ~/.dbt/profiles.yml
```

modify the threads, host, port, user, password, dbname, schema etc. and save file
so it has the info to connect to destination database
change view to table in tests/dbt_project.yml

### create table references (table.sql)

these are the table we need for transformation

### create schemas for the reference tables (schema.yml)

### create sources.yml that specifying the raw data from the destination database

### now we can create custom models to transform data

basically, we can use sql to transform and jinja to reference
for example, we can join the tables from the raw data and create new features/columns

### add dbt service on the docker compose file, depending on the elt script, then run docker compose

### shut down docker without any data persisting

```bash
docker compose down -v
```

### comfirm the new table in destination database

### dbt macros

- macros are something we can reuse to create custom models to reduce repetitive codes
- using jinja, we can reference pieces of code from other macro files very easily
- we can also control the variables in the macro files using "set"

```jinja
{% set film_title = 'Inception' %}
```

## CRON Job

### create start.sh file and add to docker file

## airflow

## airbyte
