![micromark](https://raw.githubusercontent.com/editdev/micromark/43c5c09/docs/banner.png)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

# micromark — Spring Boot REST Backend with MySQL

## Swagger OpenApi Docu

 when run locally:

 http://localhost:8080/swagger-ui.html#/main

 http://localhost:8080/swagger-ui.html#/pipeline-api

 or on stage server installation:

 https://your-app.up.railway.app/swagger-ui.html

## Init your local app with Railway

 install Railway CLI first, as described step-by-step in the Railway "Getting started" manuals!

 Having a Railway account do:

`railway login`

 `railway init` creates the app with a new project name (see the rename section).

## DB
 set up MySQL db on Railway following the steps in this tutorial:

 https://docs.railway.app/databases/mysql

 You will need the DB TABLE SCHEMA - check `./_Project/schema.sql`

 To configure DB, use Railway GUI or connect via CLI:

 `railway connect mysql` (opens mysql prompt on Railway instance)

 Optional Rename service:

 `railway service rename {old_name} {new_name}`

## Rename the app instance

  Change to better project name:

 `railway project rename newname`

## MySQL GUI on Railway

 To get the GUI with the MySQL instance:

 https://railway.app/project/{your-project-id}/service/{service-id}

## CLI TO CREATE TABLES
 `railway login`

 `railway connect mysql` (opens mysql prompt, needed to create the db tables)

## Logging
 `railway login`

 `railway logs --tail 500` (stream last 500 lines)

## DEPLOY & START APP
 edit .env only uses to run MySQL locally (needs local MySQL installation):

 .env needs these three content items (1.-3.)

 1. connection-string:

 `SPRING_DATASOURCE_URL=jdbc:mysql://localhost:3306/springboot_relay_core_db`

 local credentials:

 2. `SPRING_DATASOURCE_USERNAME=...{local mysql username e.g. root}`

 3. `SPRING_DATASOURCE_PASSWORD=...{local mysql password}`

## Build app (need built .jar package)

`railway login`

`railway init`

`./gradlew clean build`

## Deploy app to github.com and to Railway

 `git add .`

 `git commit -m "first commit"`

 `git push`

 `railway up`

# Start app locally (needs MySQL linked in .env file)

`railway run ./gradlew bootRun`

 open local app:

`railway open`

 or

`start chrome https://localhost:8080`


## Actions on REST Server (test with e.g. postman rest client)

 `{server_uri}` local = `http://localhost:8080`

 Show all Pipelines

 Get Request on:

 `{server_uri}/api/pipelines`

 POST a pipeline `{server_uri}/api/pipelines`

 JSON Payload:

 `{"tenant_id": "2222","label": "etl-pipeline","enabled": false}`

 Post a stage: `{server_uri}/api/pipeline/<pipeline_id>/stages`

 JSON Payload:

`{"id": 2,"tenant_id": "2222","pipeline_id": "2222","active": false,"name": "Transform","run_date":"2020-01-01","order":"1"}`

# Original README from Railway java getting started (copyright by Railway) following

# micromark-starter

A barebones Spring Boot app, which can easily be deployed to Railway.

This application supports the [Deploying Spring Boot on Railway](https://docs.railway.app/languages/java) article - check it out.

[![Deploy on Railway](https://railway.app/button.svg)](https://railway.app/new)

## Running Locally

Make sure you have Java and Gradle installed. Also, install the [Railway CLI](https://docs.railway.app/develop/cli).

```sh
$ git clone https://github.com/editdev/micromark.git
$ cd micromark
$ ./gradlew build
$ railway run ./gradlew bootRun
```

Your app should now be running on [localhost:8080](http://localhost:8080/).

If you're going to use a database, ensure you have a local `.env` file that reads something like this:

```
SPRING_DATASOURCE_URL=jdbc:mysql://localhost:3306/springboot_relay_core_db
```

## Deploying to Railway

```sh
$ railway init
$ railway up
$ railway open
```

## Documentation

For more information about using Java on Railway, see these articles:

- [Java on Railway](https://docs.railway.app/languages/java)
