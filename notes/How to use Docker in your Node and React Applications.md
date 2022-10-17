Docker gives developers the ability to package all of their applications inside of containers. These containers can run on any machine that has Docker installed and the application will be identical. This is a great way to run a clone of a codebase on multiple systems and you can be sure that they are all going to be the same.

CI/CD workflows and DevOps testing environments are significantly better when using Docker which is essentially a set of software tools that can be shared. Kubernetes is another tool which is used for operating multiple Docker containers but in a much larger scale.

In this tutorial we will learn how to create and run a NodeJS Express backend and a React frontend inside of a Docker container.

## Running a NodeJS Express backend inside Docker

Before you begin make sure that you have Docker installed and running on your computer.

Now use the command line to navigate to a directory like your desktop then run the commands below.

```shell
mkdir my-app-docker
cd my-app-docker
touch docker-compose.yml
mkdir api
cd api
npm init -y
npm i express
touch app.js Dockerfile .dockerignore
cd ..
```

We setup a backend called api and created some Docker files. Now open the project in your code editor and add the code below to their corresponding files.

Put this in the `docker-compose.yml` file. Be careful with the yaml formatting otherwise you will get Docker errors when you try to run it.

```yaml
version: '3.8'
services:
  api:
    build: ./api
    container_name: api_backend
    ports:
      - '4000:4000'
    volumes:
      - ./api:/app
      - ./app/node_modules
```

Add this is the `app.js` file.

```javascript
const express = require('express');

const app = express();

const port = process.env.PORT || 4000;

app.get('/', (req, res) => {
  res.send('Home Route');
});

app.listen(port, () =>
  console.log(`Server running on port ${port}, http://localhost:${port}`)
);
```

Now add this line to the `.dockerignore` file.

```shell
node_modules
```

Next add this code to the `Dockerfile` file.

```shell
FROM node:16-alpine

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 4000

CMD ["node", "app.js"]
```

Lastly add this run script to the `package.json` file.

```json
"scripts": {

"start": "node app.js"

},
```

**(Optional) Using Nodemon to have the server auto restart when changes occur**

If you want to have the server restart every single time you make a change to the files in the backend then you can configure it to use Nodemon.

All you have to do is update the `Dockerfile` and `package.json` file inside of the **api** folder.

Update the code in the `Dockerfile` using the code below. We are now installing Nodemon at the start and using **dev** as the run command.

```shell
FROM node:16-alpine

RUN npm install -g nodemon

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 4000

CMD ["npm", "run", "dev"]
```

Now update the `package.json` file with this run script for Nodemon.

```json
"scripts": {

"start": "node app.js",

"dev": "nodemon -L app.js"

},
```

We just created a basic NodeJS Express app that runs on port 4000. That port is also mapped to 4000 in docker which lets us run it in a Docker container.

### Starting the servers

To run the server outside of a Docker container using Node like normal just run the code below in your command line. You need to be sure that you are inside of the api folder. If you go to [http://localhost:4000](http://localhost:4000) you should see the home route in your browser window.

```shell
npm run start
```

Getting the NodeJS Express app to run inside of Docker requires a different command. First you need to be in the root folder where the `docker-compose.yml` file is. Now run the command below and it should run inside of a Docker container.

Don't forget to stop the node server running first because you can only have one server running on port 4000.

```shell
docker-compose up
```

If you go to [http://localhost:4000](http://localhost:4000) you should see the home route in your browser window.

You can stop the server with the command below or you can go to the Docker app and stop the container from running.

```shell
docker-compose down
```

## Running a React frontend inside Docker

Now lets create a React frontend! Use your command line to get inside of the root folder for my-app-docker. Run the commands below to setup the project.

```shell
npx create-react-app client
cd client
touch .dockerignore Dockerfile
```

Now add the code below into their corresponding files.

Add this line into the `.dockerignore` file.

```shell
node_modules
```

Put this code into the `Dockerfile` file.

```shell
FROM node:17-alpine

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

Finally update the `docker-compose.yml` in the root folder with the code below. We have added a client section at the bottom with settings for getting React running inside of a Docker container. Be careful with the yaml formatting otherwise you will get Docker errors when you try to run it.

```yaml
version: '3.8'
services:
  api:
    build: ./api
    container_name: api_backend
    ports:
      - '4000:4000'
    volumes:
      - ./api:/app
      - ./app/node_modules
  client:
    build: ./client
    container_name: client_frontend
    ports:
      - '3000:3000'
    volumes:
      - ./client:/app
      - ./app/node_modules
    stdin_open: true
    tty: true
```

### Starting the servers

To run the server outside of a Docker container using Node like normal just run the code below in your command line. Make sure that you are inside of the client folder. If you go to [http://localhost:3000](http://localhost:3000) you should see the home route in your browser window.

```shell
npm run start
```

Getting the React app to run inside of Docker requires a different command. First you need to be in the root folder where the `docker-compose.yml` file is. Now run the command below and it should run inside of a Docker container.

Don't forget to stop the React app server running first because you can only have one server running on port 3000.

```shell
docker-compose up
```

If you go to [http://localhost:3000](http://localhost:3000) you should see the home route in your browser window.

You can stop the server with the command below or you can go to the Docker app and stop the container from running.

```shell
docker-compose down
```

With this setup you can have a NodeJS backend and React frontend running at the same time inside of Docker! If you encounter any errors then you might need to open your Docker desktop application and remove any images that are related to this project. Then you can try running the `docker-compose up` command again and hopefully this time everything should be working as expected.
