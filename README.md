Aging-notebook
===============

This repo contains docker stacks with notebooks relevant to aging research

Folder layout
-------------

bin - shell scripts to run stuff:
    * _download-geo.sh_ downloads and extracts sqlite database with GEO metadata
    * _migrate.sh_ migrates downloaded sqlite to postgres (usually used after download-geo.sh)
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

If everything looks fine it will look like:
![Screenshot](images/zeppelin.jpg?raw=true "Zeppelin screenshot")

Notebook with GEO
=================

Contains both notebooks but also run postgres database where you can migrate GEO metadata
To start this notebook:
```bash
bin/start-with-geo.sh
```


Setting up GEO database
-----------------------
Download the sqlite database with:
```bash
bin/download-geo.sh
```
Make sure that notebook with geo is started, if not start with:
```bash
bin/start-with-geo.sh
```

Install pgloader to your system ( see https://pgloader.io/ ), for Ubuntu/Mint it will be:
```bash
sudo apt install pgloader
```

Run the migration script:
```bash
bin/migrate.sh
```

You can check that the data was transferred inside of the adminer by opening http://localhost:5050 and connecting to the database (default login is *postgres*, default password is *changeme*)