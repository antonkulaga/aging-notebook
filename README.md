Aging-notebook
===============

This repo contains docker stacks with notebooks relevant to aging research

Folder layout
-------------

bin - shell scripts to run stuff:
    * _download-geo.sh_ downloads sqlite database with GEO metadata
    * _migrate.sh_ migrates downloaded sqlite to postgres
    * _start.sh_ starts aging notebook stack
    * _start-with-geo.sh_ starts extended aging notebook stack that also contains postgres container
                 
conf - configuration for containers
databases - database data, note it is .gitignfored
notebooks - zeppelin notebooks data (not gitignored)

Notebook
--------

Docker stack that runs Spark and Zeppelin. 
Before running it make sure that you have docker swarm working.
If docker swarm is not running you can initialize it with:
```bash
docker swarm init
```
It can also be useful to use admin panels like https://github.com/swarmpit/swarmpit to manage Docker Swarm

To start the docker stack for notebook run:
```bash
bin/start.sh
```
Then open:
```
http://localhost:9002
```

Notebook with GEO
-----------------

Contains both notebooks but also run postgres database where you can migrate GEO metadata