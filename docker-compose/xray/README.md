# Xray Docker Compose Examples

This directory provides some examples that show different ways to run Xray with Docker Compose.
To learn more about Docker and how to set it up, please refer to the [Docker](https://docs.docker.com) and [Docker Compose](https://docs.docker.com/compose/overview/) documentation.  

Xray is available as different Docker images for:

* [xray-server](https://bintray.com/jfrog/reg2/jfrog%3Axray-server) : Generating violations, hosting API / UI endpoints, running scheduled jobs
* [xray-indexer](https://bintray.com/jfrog/reg2/jfrog%3Axray-indexer) : Responsible for the indexing process
* [xray-analysis](https://bintray.com/jfrog/reg2/jfrog%3Axray-analysis) : Responsible for enriching component metadata
* [xray-persist](https://bintray.com/jfrog/reg2/jfrog%3Axray-persist) : Matching the given components graph, completing component naming, storing the data in the relevant databases
* [xray-rabbitmq](https://bintray.com/jfrog/reg2/jfrog%3Axray-rabbitmq) : Microservice Communication and Messaging
* [xray-postgres](https://bintray.com/jfrog/reg2/jfrog%3Axray-postgres) : Components Graph Database
* [xray-mongo](https://bintray.com/jfrog/reg2/jfrog%3Axray-mongo) : Components Metadata and Configuration

These images are available for download from [JFrog Bintray](https://bintray.com/jfrog).

## Docker-Compose Usage

To run any of the examples, you should execute:

```bash
$ docker-compose -f <compose-file> <options>
```

---
### Persistent Storage

For persistent storage, all volumes are mounted from the host.

All examples default to the host's **/data** directory via `.env` file

> **IMPORTANT:** You should create the directories on the host before running `docker-compose`.

- Xray data: **/data/xray**
- RabbitMQ data: **/data/rabbitmq**
- PostgreSQL data: **/data/postgres**
- MongoDB data: **/data/mongodb**

---
# Docker Compose Examples

Below is a list of included examples. You are welcome to contribute.

---
## Xray

#### Run Xray with RabbitMQ, PostgreSQL and MongoDB

Preparing all the needed files and directories on the host.

```bash
$ sudo ./prepareHostEnv.sh
```

If it's the first installation, you have to create users first using [`createMongoUsers.js`](createMongoUsers.js) script :

```bash
$ sudo docker-compose -f xray.xml up -d mongo
$ sudo cat createMongoUsers.js | docker exec -i xray-mongodb mongo
```

Then you are ready to go :

```bash
$ sudo docker-compose -f xray.yml up -d
```

This example starts the following containers and exposes Xray on port 8000 (http)

## Run Xray with Traefik

_TODO_