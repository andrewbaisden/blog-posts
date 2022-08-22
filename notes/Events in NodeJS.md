# Events in NodeJS

## What are events in Node.js?

Microservice-based computer systems are modern computer systems that frequently use events to initiate and facilitate communication between separated services. These events are basically a way to manage the state across an application. We are going to use a social media network like Twitter as an example so that it becomes pretty straightforward to understand.

So in the case of Twitter let's say that we have just posted a new tweet to our timeline. That is the equivalent of a state change because our application has either been updated or changed to display some new information. And this event can carry state information such as the time the tweet was posted, the date, the message and other valuable information. The events can even be identifiers so in the Twitter example, you could get a notification that your tweet has a comment, retweet or likes.

Event producers, event routers, and event consumers are the main parts of this type of structure. These events are sent by a producer and end up in the router, which then filters and dispatches them to consumers. Because of the decoupling between the producer and consumer services, each may be updated, modified, and deployed separately.

In this tutorial, we will learn how to use events in a Node.js application and how to use the built-in HTTP API in Node.js.

## How do events work in Node.js?

Let's walk through a Node.js example so that you can see how events would work within the back-end framework. Firstly we would begin with an event listener, emitting an event like a function initiating a request. That request could ping a server with a 200 status response, which means the request was successful.

In another example, we could have a timer that expires before it triggers another predefined event. It is also possible that we could have a file which has been successfully read using the **fs.readFile()** method in Node.js. All of these examples will trigger emit events. To access these events, we would create an event listener that picks up the emitted event. The event listeners are then attached to a callback function which runs some code that we have written. In a simple example, it could be using **console.log** to output some information into the console.

## Using events in a Node.js app

It's time for us to create a simple example so that we can see what events look like in a JavaScript codebase. We will continue with the Twitter example.

**cd** into a directory on your computer and then run the code below so that you can set up a project.

```shell
mkdir my-app-events
cd my-app-events
npm init -y
touch app.js
```

Now open the project in your code editor and add this run script below to your **package.json** file.

```json
"start": "node app.js"
```

Lastly copy the code below into your **app.js** file.

```javascript
const eventEmitter = require('events');

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

twitterEmitter.on('postTweet', (id, tweet, comments, retweets, likes, date) => {
  console.log({
    id: id,

    tweet: tweet,

    comments: comments,

    retweets: retweets,

    likes: likes,

    date: date,
  });
});

// Running the callback function which emits the event

twitterEmitter.emit('postTweet', 1, 'Hello World!', 0, 0, 0, '08-01-2022');
```

Now all you need to do is run the command **npm run start** from the command line inside of your root folder where the **app.js** file is and you should be able to see an object outputted in your command line window.

The object is for a simple tweet that holds data for an id, tweet, comments, retweets, likes and the date.

```javascript
{
  id: 1,
  tweet: 'Hello World!',
  comments: 0,
  retweets: 0,
  likes: 0,
  date: '08-01-2022'
}
```

Basically, all we did was create an emitter class, and initialise it. Then we created an event listener and a callback function which we called.

## The HTTP API vs Express

### HTTP API Example

Now that we have learned the basics of events, I will walk you through one final example. We will create another basic server this time using the HTTP API built into Node.js and Express. The difference between the two is that the HTTP API is built into Node.js and is used for sending and receiving data. Whereas Express is more of a framework that gives you everything you need to set up a backend architecture.

You should be inside the root project folder for **my-app-events**. Create a file named **index.js** manually or through the command line with the command **touch index.js**. Next copy and paste this code into the **index.js** file.

```javascript
const http = require('http');

// Creates a http server

const server = http.createServer();

// Emits a request event with a callback function

server.on('request', (req, res) => {
  console.log('Server request received');

  res.end('Hello from the Twitter server');
});

// Selects a port for the server

const port = process.env.PORT || 3000;

// Creates an event listener

server.listen(port, () =>
  console.log(`Server listening on port ${port}, http://localhost:${port}`)
);
```

Finally, create another run script in your **package.json** file.

```json
"start:http": "node index.js"
```

Run the script and go to [http://localhost:3000](http://localhost:3000) in your web browser and you should see the message **Hello from the Twitter server**. You should also see the message **Server request received** in your console.

### Express Example

As a comparison, this is how the same functionality would work in an Express application. To get this example to work you would first need to install the package **express**.

```shell
npm i express
```

And create another file like this example **index2.js** file below.

```javascript
const express = require('express');

const app = express();

app.get('/', (req, res) => {
  console.log('Server request received');

  res.send('Hello from the Twitter server');
});

// Selects a port for the server

const port = process.env.PORT || 3001;

// Creates an event listener

app.listen(port, () =>
  console.log(`Server listening on port ${port}, http://localhost:${port}`)
);
```

Then create a new run script for the **package.json** file.

```shell
"start:express": "node index2.js"
```

## Final Thoughts
In this tutorial, we went over various aspects of events within a Node application. If you have any further questions, connect with us here at [Sprkl](https://sprkl.dev/).
