## What are events in NodeJs?

Microservice-based computer systems are modern computer systems that frequently use events to initiate and facilitate communication between separate services. These events are basically a way to manage the state across an application. We are going to use a social media network like Twitter as an example so that it becomes pretty straightforward to understand.

So in the case of Twitter let's say that we have just posted a new tweet to our timeline. That is the equivalent of a state change because our application has either been updated or changed to display some new information. And this event can carry state information such as the time the tweet was posted, the date, the message and other valuable information. The events can even be identifiers so in the Twitter example, you could get a notification that your tweet has a comment, retweet or likes.

Event producers, event routers, and event consumers are the main parts of this type of structure. These events are sent by a producer and end up in the router, which then filters and dispatches them to consumers. Because of the decoupling between the producer and consumer services, each may be updated, modified, and deployed separately.

In this tutorial, we will learn how to use events in a NodeJS application and how to create a simple microservice using NodeJS.

## How do events work in NodeJS?

Let's walk through a NodeJS example so that you can see how events would work within the back-end framework. Firstly we would begin with an event listener, emitting an event like a function initiating a request. That request could ping a server with a 200 status response, which means the request was successful.

In another example, we could have a timer that expires before it triggers another predefined event. It is also possible that we could have a file which has been successfully read using the **fs.readFile()** method in NodeJS. All of these examples will trigger emit events. To access these events, we would create an event listener that picks up the emitted event. The event listeners are then attached to a callback function that runs some code we have written. In a simple example, it could be using **console.log** to output some information into the console.

## Using HTTP for messaging

There are two types of HTTP messages there is one for doing requests and another one for doing responses which is the data that is returned after you have sent your request. These responses return information such as if your request was a success. In this case, you would get a 200 status code which essentially means that everything is ok.

On the flip side, you might get a 500 status code which means that the server encountered an unexpected condition that prevented it from fulfilling the request. Similarly, you could get a 404 status code which means that the page could not be found. You can learn more about HTTP status codes here [HTTP response status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status). Significantly more information is returned such as the content type, headers, the server type as well as additional information. The important thing is that you have information and data which you will be able to understand and use in your applications.

Another way for services to communicate with each other is by using a message broker. Let's learn how message brokers can be used for communication between different services.

### Message Brokers

In order to create a standard integration mechanism to enable cloud-native, microservices-based, serverless, and hybrid cloud architectures, we can use message brokers as an inter-application communication solution.

Message brokers are pieces of software that facilitate information exchange and communication between different apps, services and computer systems. By converting messages across communication protocols, the message broker can be enabled to work with interdependent services to directly "talk" to one another. This occurs regardless of their differing programming languages or platform implementations.

RabbitMQ is a very popular message broker tool. It uses Advanced Message Queuing Protocol (AMQP). AMQP is made up of Producers, A Broker and Consumers. One of its biggest advantages is the fact that it increases scalability as well as has loose coupling.

### Monolithic vs Microservice

Monolithic applications are huge applications where all of the services and the entire codebase is part of one single unit. So for example in the case of an e-commerce website like Amazon all of the shopping, products, payments and user information would be in one codebase if they were using monolithic architecture. It's all built, coded and scaled together which unfortunately means you are dependent on one programming language. If a piece of code was changed for say the user section then the entire monolithic application would have to be rebuilt which is bad for scalability it also introduces problems where coding bugs could take down the entire application among other things. There is just too much complexity.

Microservices on the other hand are decoupled into smaller applications that are pieces of the main application. They can be built in any programming language because they are all different applications with their own codebase. So in other words you will have different services for each feature of an application. Using Amazon as an example again would mean that the products, payments and user information would all have their own service. Each service is loosely coupled and they can run independently of each other.

So if the payments service was to go down it would only be that area of the application and not the entire Amazon website. These services are capable of communicating with each other using various methods like API calls. They all can have endpoints such as `/payment/18f7qweh27f` or `/user/383r7f3j29` or `/cart/item/39rt8g4393k` and they would use HTTP Response and HTTP Requests to talk to each other. All communication is synchronous so they wait before the data arrives.

Microservices can be made up of various tools and technologies. Some of the most popular ones are listed below.

- [RabbitMQ](https://www.rabbitmq.com/)
- [Kafka](https://kafka.apache.org/)
- [Docker](https://www.docker.com/)
- [Kubernetes](https://kubernetes.io/)
- [Socket.io](https://socket.io/)
- [WebSockets](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API)

## Building microservices using events

It's time for us to create a simple example so that we can see what events look like in a JavaScript codebase. We will continue with the Twitter example from earlier and we will be building some microservices. There will be 3 NodeJS servers and they will be able to communicate with each other using REST APIs and various endpoints.

Setting up this project could take a while so I have made it simple for you. Firstly use the command line to go to a directory like your desktop. Then run the commands below to scaffold your project. You can see what all the commands are doing if you read them.

```shell
mkdir twitter-app
cd twitter-app
mkdir messages-service profile-service tweet-service
cd messages-service
npm init -y
npm i express nodemon
touch index.js
mkdir data
cd data
touch messages.json
cd ../..
cd profile-service
npm init -y
npm i express nodemon axios
touch index.js
cd ..
cd tweet-service
npm init -y
npm i express nodemon
touch index.js
cd ..
```

Open the **twitter-app** project in your code editor. Add the code below to their corresponding services and files.

### message-service

Add the code below to `messages-service/data/messages.json`

```json
[
  {
    "id": 1,

    "username": "stolomio0",

    "message": "Vestibulum quam sapien, varius ut, blandit non, interdum in, ante. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Duis faucibus accumsan odio. Curabitur convallis."
  },

  {
    "id": 2,

    "username": "lwoofenden1",

    "message": "In hac habitasse platea dictumst. Morbi vestibulum, velit id pretium iaculis, diam erat fermentum justo, nec condimentum neque sapien placerat ante. Nulla justo.\n\nAliquam quis turpis eget elit sodales scelerisque. Mauris sit amet eros. Suspendisse accumsan tortor quis turpis.\n\nSed ante. Vivamus tortor. Duis mattis egestas metus."
  },

  {
    "id": 3,

    "username": "yjentgens2",

    "message": "Cras non velit nec nisi vulputate nonummy. Maecenas tincidunt lacus at velit. Vivamus vel nulla eget eros elementum pellentesque."
  },

  {
    "id": 4,

    "username": "kapthorpe3",

    "message": "Phasellus in felis. Donec semper sapien a libero. Nam dui."
  },

  {
    "id": 5,

    "username": "lmcginney4",

    "message": "Donec diam neque, vestibulum eget, vulputate ut, ultrices vel, augue. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Donec pharetra, magna vestibulum aliquet ultrices, erat tortor sollicitudin mi, sit amet lobortis sapien sapien non mi. Integer ac neque."
  },

  {
    "id": 6,

    "username": "ktidcombe5",

    "message": "Integer tincidunt ante vel ipsum. Praesent blandit lacinia erat. Vestibulum sed magna at nunc commodo placerat.\n\nPraesent blandit. Nam nulla. Integer pede justo, lacinia eget, tincidunt eget, tempus vel, pede."
  },

  {
    "id": 7,

    "username": "vwarcop6",

    "message": "In quis justo. Maecenas rhoncus aliquam lacus. Morbi quis tortor id nulla ultrices aliquet.\n\nMaecenas leo odio, condimentum id, luctus nec, molestie sed, justo. Pellentesque viverra pede ac diam. Cras pellentesque volutpat dui.\n\nMaecenas tristique, est et tempus semper, est quam pharetra magna, ac consequat metus sapien ut nunc. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Mauris viverra diam vitae quam. Suspendisse potenti."
  },

  {
    "id": 8,

    "username": "jforryan7",

    "message": "Integer tincidunt ante vel ipsum. Praesent blandit lacinia erat. Vestibulum sed magna at nunc commodo placerat.\n\nPraesent blandit. Nam nulla. Integer pede justo, lacinia eget, tincidunt eget, tempus vel, pede."
  },

  {
    "id": 9,

    "username": "houthwaite8",

    "message": "Proin eu mi. Nulla ac enim. In tempor, turpis nec euismod scelerisque, quam turpis adipiscing lorem, vitae mattis nibh ligula nec sem."
  },

  {
    "id": 10,

    "username": "nselland9",

    "message": "Phasellus in felis. Donec semper sapien a libero. Nam dui."
  }
]
```

Next, add the code below to `messages-service/index.js`

```javascript
const express = require('express');

const app = express();

app.get('/', (req, res) => {
  const data = require('./data/messages.json');

  res.json(data);
});

const port = process.env.port || 8001;

app.listen(port, () =>
  console.log(
    `Message service running on port ${port}, http://localhost:${port}`
  )
);
```

Finally, add the run scripts to `messages-service/package.json`

```json
"scripts": {

"start": "node index.js",

"dev": "nodemon index.js"

},
```

### profile-service

Add the code below to `profile-service/index.js`

```javascript
const express = require('express');

const axios = require('axios');

const app = express();

// Retrieve the tweet service

app.get('/tweet', async (req, res) => {
  const response = await axios.get('http://localhost:8000/');

  try {
    console.log(response.data);

    res.send(response.data);
  } catch (error) {
    console.log(error);

    res.send(500);
  }
});

// Retrieve the message service

app.get('/message', async (req, res) => {
  const response = await axios.get('http://localhost:8001/');

  try {
    console.log(response.data);

    res.send(response.data);
  } catch (error) {
    console.log(error);

    res.send(500);
  }
});

const port = process.env.PORT || 8002;

app.listen(port, () =>
  console.log(`Profile service running on ${port}, http://localhost:${port}`)
);
```

And once again, add the run scripts to `profile-service/package.json`

```json
"scripts": {

"start": "node index.js",

"dev": "nodemon index.js"

},
```

### tweet-service

Add the code below to `tweet-service/index.js`

```javascript
const express = require('express');

const app = express();

const port = process.env.PORT || 8000;

const eventEmitter = require('events');

app.get('/', (req, res) => {
  // Creating an event emitter class

  class Twitter extends eventEmitter {
    constructor() {
      super();
    }
  }

  // Initiating the event emitter

  let twitterEmitter = new Twitter();

  // Creating the event listener and callback function

  // postTweet is the name of the event

  twitterEmitter.on(
    'postTweet',

    (id, tweet, comments, retweets, likes, date) => {
      const data = {
        id: id,

        tweet: tweet,

        comments: comments,

        retweets: retweets,

        likes: likes,

        date: date,
      };

      console.log(data);

      res.json(data);
    }
  );

  // Running the callback function which emits the event

  twitterEmitter.emit('postTweet', 1, 'Hello World!', 0, 0, 0, '08-01-2022');
});

app.listen(port, () =>
  console.log(`Tweet service running on ${port}, http://localhost:${port}`)
);
```

And for the last time again, add the run scripts to `tweet-service/package.json`

```json
"scripts": {

"start": "node index.js",

"dev": "nodemon index.js"

},
```

To get all of the servers running just `cd` into each root folder with the `package.json` file and use the command below to start them all up. Do this in separate command line windows/tabs.

```shell
npm run dev
```

Now we should have 3 microservices all running independently of each other on different ports. They each have their own server so if one goes down the other ones won't be affected because they are individuals. So basically we have created a server for `message-service`, `profile-service` and `tweet-service`. The `message-service` acts as a database and has a `messages.json` file that stores data for Twitter messages. This is a basic simulation and in a real-world project, it could be a database that persists this type of data. The endpoint for retrieving the JSON messages is [http://localhost:8001/](http://localhost:8001/) .

We also have a `tweet-service` which basically, has an emitter class which is initialised. Then we created an event listener and a callback function which we call inside of the endpoint. This is returned as a JSON at [http://localhost:8000/](http://localhost:8000/).

Lastly, we have the `profile-service` which essentially uses the npm package `axios` to send a GET request to the `message-service` and the `tweet-service` endpoints. The tweets are returned at [http://localhost:8002/tweet](http://localhost:8002/tweet) and the messages are returned at [http://localhost:8002/message](http://localhost:8002/message). In a real-world example, this data could be used to build components on a web page using HTML, CSS and JavaScript.

## Final thoughts

In this tutorial, we went over various aspects of events within a Node application. We also learned how to create a basic microservice using the social media network Twitter as an example. You also learned about a few ways in which you can integrate HTTP communication into your applications. If you have any further questions, connect with us here at [Sprkl](https://sprkl.dev/).
