# React SSR Made Easy! (Work In Progress)

# Project Status
- [x] Sends JSX as string from the server on the root route when the page is requested by the browser... Hydrates that markup on the client after fetching the resulting HTML.
- [x] Hot Reload for Bundled CSS on the server
- [x] Sass
- [x] Jest (bootstrapped as a second webpack entrypoint on the server) 
- [x] Docker Image
- [x] Custom Server Logic
     - [ ] Retry port on server startup if busy
     - [x] Watch for sigint signals etc. to handle graceful shutdowns
     - [x] Inversion of control with TSyringe dependency injection
     - [x] ENV variables supplied through webpack
- [x] Bash script for setting up postgresql locally
- [x] Bash script for extra control over container orchestration through Docker Compose 
- [x] Docker Compose for local development with hot reload
- [ ] Docker Compose boilerplate for production
- [ ] Universal State Management
- [ ] Universal Routing through Express
- [ ] Prisma Schema with a CMS Domain for managing pages & content
- [ ] Auth Server
- [ ] Graphql for async requests to the server
- [x] Prisma ORM
- [ ] Code generation for graphql from a prisma schema to avoid writing boilerplate
- [ ] Repositories & Express endpoints to match the CMS Domain DB data


# Running Locally
`npm i` (installs the concurrently library to run npm install concurrently across the frontend/backend projects and the isomorphic local library)

* Preferred way of running things is using containers, however if for any reason you need to run this locally, please install postgres on your linux first using the bash script below. This also prints out the required connection string for the DB.

`cd nodejs-ssr-boilerplate/src/script` (go to the root to use the bootstrap project)


`. ./.setupPostgres.sh` (Ensures postgres is installed, sets up a role and db so the psql command will work without problems on the linux user)

`npm run prisma` (This runs npx prisma migrate dev --name init && npx prisma db seed && npx prisma generate)
* migrate dev creates the initial  migration to match the DB with the schema
* db seed generates some dummy data in that DB
* generate creates the prisma client and types associated with the schema to query the DB

This project is a full-stack app and the express server on the backend requires client bundles to be generated ahead of time so they could be used as static assets. A bootstrap project is used to simplify usage!

`cd nodejs-ssr-boilerplate` (go to the root to use the bootstrap project)


`npm run start:local` (Transpile & Run the server through the browser-refresh library on the server, Transpile & watch the frontend code for changes )


# Running Through Containers

* If running for the first time, update the server-dev service environment variables inside docker-compose-dev.yaml... `MIGRATE_ON_STARTUP` to true and `RUNTIME_ENV` to "container". The DB data is mounted on the container as a volume, we would like to create tables & generate seed data when running for the first time!

* Ensure that the docker-compose version is above v2.0 with docker-compose -v

`cd nodejs-ssr-boilerplate` (Go into the bootstrap project)

`npm start` (Run the /server/script/.runContainers.sh script which adds additional logic around docker-compose) 

Things to note about using the containers:

* To use this workflow, it is needed to install any packages which we might need within the container as we won't have thenpm binary locally.


`docker exec -it sinda-ssr-server /bin/sh` (This goes into the container where we have access to npm)

To install a dependency on one of the projects, all variations have been listed for convenience:

client: 

`(cd client; npm install example-package)` 

server: 

`(cd server; npm install example-package)` 

isomorphic lib: 

`(cd isomorphic; npm install example-package)`

bootstrap project: 

`npm install example-package` 
