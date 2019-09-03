#Containerized-Fullstack

## Current issues:
Network connection http://172.24.0.4:3000/ times out with no erros.  Unsure why it won't connect.

## Gordon explains how to make this broken POS run:
0. In local testing, change testDB.js from `mongodb://mongodb:27017` to `mongodb://localhost:27017`.  Original author failed to use correct form, documented at https://mongoosejs.com/docs/connections.html.
1. In ./docker-compose.yml
   1a. Insert `build: ./client`
   1b. Insert `build: ./api`
   1c. Original author forgot to push his Dockerfiles.  I included them.  Great attention to detail, genius.
2. Reminder: how to sigkill Mongo PID:
   `sudo lsof -iTCP -sTCP:LISTEN -n -P`
   `sudo kill ${PID}`
   `mongod`
3. Docker-compose commands must be prefixed sudo.  See  https://github.com/docker/compose/issues/4039
   2a. `sudo docker-compose build`
   2b. `sudo docker-compose up`  
4. After modification of images or source, first declare `sudo docker system prune`
5. Note all modifications to Dockerfile and .yml that the original author failed to implement.  Specifically, inclusion of bash script wrappers to resolve this issue: Despite being dependency, mongo image does not start listening until API and client images attempt to connect to mongo, fail, and crash.
6. Verify no extra formatting at the top of the bash scripts.

## Original (terrible) documentation, author, and readme:
Original documentation and author: https://medium.com/free-code-camp/create-a-fullstack-react-express-mongodb-app-using-docker-c3e3e21c4074

## About the apps
There are two apps. (1) The Client which serves the FrontEnd (using React), and (2) the API (in Node/Express).

## How to run the API
1. In your terminal, navigate to the `api` directory.
2. Run `npm install` to install all dependencies.
3. Run `npm start` to start the app.

## How to run the Client
1. In another terminal, navigate to the `client` directory.
2. Run `npm install` to install all dependencies.
3. Run `npm start` to start the app

## Check if they are connected
1. With the two apps running, open your browser in http://localhost:3000/.
2. If you see a webpage saying `Welcome to React`, it means the FrontEnd is working.
3. If the same webpage has the phrase `API is working properly`, it means the API is working.
4. Enjoy!