# nodejs-ssr-boilerplate (Work In Progress)

# Project Status
- [x] Render JSX at / 
- [x] Docker Image for server
- [x] Custom Server Logic
     - [x] Retry port on server startup
     - [x] Watch for sigint signals etc. to handle graceful shutdowns
     - [x] Inversion of control with TSyringe dependency injection
     - [x] ENV variables supplied through webpack
- [x] Docker Compose for local development with hot reload (With DB image & volume boilerplate commented out)
- [x] Docker Compose boilerplate for production (With DB image & volume boilerplate commented out)
- [x] Jest bootstrapped as a second webpack entrypoint 
- [x] Hydrate markup on the client
- [x] Sass
- [] React Router on the client
- [] Websockets for non / endpoints
- [] Graphql
- [] Prisma


# Running Locally

To run this app, first the client code has to be watched for changes and bundled on each change.

`cd client && npm i && npm start`

The bundle appears inside the server/www folder which the express server serves static files from

To run the server:

`cd server && npm i && npm run build:dev`

# Running Through Containers

instructions for containerized runtime coming soon...
