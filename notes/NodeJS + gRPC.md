# NodeJS + gRPC

## What is gRPC

Today the main topic that we will be learning about is gRPC. We will also learn about Microservices, the advantages of gRPC, and the difference between gRPC libraries. At the end of this article I will run through a basic tutorial for getting gRPC working with Node.js. So let's get started!

gRPC is a very modern, open source framework that was released in August 2016. It is a high-performance Remote Procedure Call framework (hence the name RPC) that is capable of running in any type of environment. What sets gRPC apart from similar frameworks is its ability to offer much higher performance when clients and server applications are trying to communicate with each other. So we have established that is gives us many performance gains but we also need to take into account that gRPC is much harder to implement and many of us developers have never used it before so this is something we will need to take into account.

We are all familiar with the traditional ways for clients and servers to connect with each other most notably using REST API which we know as RESTful API. But there is also GraphQL which is an open-source data query language for APIs. I will talk you through the difference between the two types. Now in the case of REST API it typically works on the client whereas with GraphQL all of that logic is set up on the backend. Each system has its own pros and cons which gives us different options to choose from. I am going to show you the differences between these frameworks in the upcoming sections. You are going to learn that they are compromised of various technical stacks which are combined together to create what is known as a microservice.

## Microservices

Now let me give you an introduction to what microservices are. They are basically an architectural structure which is a collection of various services that form an overall style. This type of architecture gives a developer or team the ability to rapidly build complex applications. In doing so we could be able to scale up a technology stack whenever we needed to like in the case of developing a new feature request for an app we are working on.

In one example we could have a backend microservice that uses Python, Node.js and Go. Each language serves a purpose and they need to connect together. If we were to try using gRPC in a browser it would not work without installing the right setup and configurations. However, the perfect use case is when it comes to using it in a backend microservice environment like in our example with Python, Node.js and Go.

## gRPC Advantages

It's time for us to learn some advantages of gRPC which I will demonstrate to you. One of the advantages of using gRPC is its flexibility. When we use separate libraries it is quite common that we are going to be doing a lot of the setup for the different connection layers. Every language has a different HTTP client library so maintaining and updating them all across the board for every single microservice that we use can create a lot of overhead and frustration.

Now with gRPC, it natively supports all of the HTTP clients setups so we don't have to manually do it across all of our services. Another huge advantage is the fact that gRPC can do code generation using protocol buffers. They are effectively like a blueprint for doing communications between different parties.

We already know that REST APIs are a traditional method for sending data and unlike gRPC they do not use blueprints so to speak so the messages are sent as key-value pairs which are not checked until they reach our recipient.

Take a look at the below example for a traditional `.json` file.

```json
{
  "id": "77etf783fwerf23f",
  "name": "Luke Skywalker",
  "profession": "Jedi Knight",
  "email": "lukeskywalker@gmail.com"
}
```

When we compare it to gRPC on the other hand we can see that it defines services in a `.proto` file like in the code snippet I have created below. These services are basically like a schema for the data that is going to be sent much like defining a schema for the data in a GraphQL file. Similarly using a tool like [Swagger](https://swagger.io/) for our RESTful API design needs.

```proto
message Profile {
	required int32 id = 1;
	required string name = 2;
	optional string email = 3;
}
```

So in this example, we are defining which procedures can be called from other microservices. That would be our Python, Node.js and Go backends in this case. When we want to have the source code generated and output for the languages that we are working on we would use a compiler on the `.proto` file and then it would output the correct source code for the languages which we specified.

Let me give you another one of the big areas where gRPC excels over REST and GraphQL. By now we know that it is in speed and performance and the fact that it uses HTTP 2.0 is another reason because it is using the latest specification which is more modern when compared to HTTP 1.0. It has significantly more performance improvements due to the fact that protocol buffers become serialised and the data is sent using binary.

This will do wonders for us as it leads to much better security because gRPC supports SSL/TLS, ALTS and Token-based authentication with Google. We can read about all of these concepts in the [Authentication](https://grpc.io/docs/guides/auth/) section in their official documentation. Streaming gives us another advantage because gRPC can do client, server and bidirectional streaming which is available in HTTP 2.0 only.

When we use JSON data it tends to be uncompressed because we are dealing with key-value pairs whereas with a binary file the data is much smaller. The flexibility combined with speed gains makes gRPC a good choice for us when we are trying to build an architecture that needs a high level of performance.

## The difference between grpc and grpc-js

What we need to realise is that the original Node.js gRPC library was the first to be released although it is no longer recommended because it has been deprecated in favour of the newer grpc-js library. The more modern grpc-js library has been available since April 2020 and it is a pure TypeScript reimplementation of the previous library.

According to the creators, it supports the following features which should cover the majority of use cases:

- Clients
- Automatic reconnection
- Servers
- Streaming
- Metadata
- Partial compression support: clients can decompress response messages
- Pick first and round-robin load balancing policies
- Client Interceptors
- Connection Keepalives
- HTTP Connect support (proxies)

While the newer library is almost a like-for-like replacement there are some differences which are better explained to us in the [Migrating from grpc](https://www.npmjs.com/package/@grpc/grpc-js) section on their npm package page.

## How gRPC is used in a Node.js environment

We should familiarise ourselves with Nest.js which is an extremely popular Node.js backend framework that uses TypeScript. The documentation on their website is actually quite good and they even have a microservices section dedicated to using [Nest gRPC](https://docs.nestjs.com/microservices/grpc) which we can learn from.

They also use the `.proto` file standard to dynamically link the clients and servers together so that we can put together remote procedure calls, that will automatically serialise and deserialise the structured data.

### Setting up a gRPC project in Node.js

Let's create a simple example so we can see what a gRPC project would look like in Node.js. I have included the GitHub repo with the codebase here [https://github.com/andrewbaisden/nodejs-grpc](https://github.com/andrewbaisden/nodejs-grpc).

First, let's navigate to a directory in our computer using the command line and then let's copy and paste the code below to scaffold a project.

```shell
mkdir nodejs-grpc
cd nodejs-grpc
npm init -y
npm i @grpc/grpc-js @grpc/proto-loader minimist nodemon
touch welcome_client.js welcome_server.js welcome.proto
```

Now we need to open the project in a code editor or IDE and copy and paste the code below. We are going to put the code below in the files that we just created.

First let's put this code in our `wlecome_client.js` file.

```javascript
const PROTO_PATH = __dirname + '/welcome.proto';

const parseArgs = require('minimist');

const grpc = require('@grpc/grpc-js');

const protoLoader = require('@grpc/proto-loader');

const packageDefinition = protoLoader.loadSync(PROTO_PATH, {
  keepCase: true,

  longs: String,

  enums: String,

  defaults: true,

  oneofs: true,
});

const welcome_proto = grpc.loadPackageDefinition(packageDefinition).welcome;

function main() {
  const argv = parseArgs(process.argv.slice(2), {
    string: 'target',
  });

  let target;

  if (argv.target) {
    target = argv.target;
  } else {
    target = 'localhost:50051';
  }

  const client = new welcome_proto.Welcome(
    target,

    grpc.credentials.createInsecure()
  );

  let user;

  if (argv._.length > 0) {
    user = argv._[0];
  } else {
    user = 'Luke Skywalker';
  }

  client.SayWelcome({ name: user }, function (err, response) {
    console.log('Message:', response.message);
  });
}

main();
```

Next, we will add this code into our `welcome_server.js` file.

```javascript
const PROTO_PATH = __dirname + '/welcome.proto';

const grpc = require('@grpc/grpc-js');

const protoLoader = require('@grpc/proto-loader');

const packageDefinition = protoLoader.loadSync(PROTO_PATH, {
  keepCase: true,

  longs: String,

  enums: String,

  defaults: true,

  oneofs: true,
});

const welcome_proto = grpc.loadPackageDefinition(packageDefinition).welcome;

/**

* Implements the SayWelcome RPC method.

*/

function SayWelcome(call, callback) {
  callback(null, { message: 'Welcome ' + call.request.name });
}

/**

* Starts an RPC server that receives requests for the Welcome service at the

* sample server port

*/

function main() {
  const server = new grpc.Server();

  server.addService(welcome_proto.Welcome.service, { SayWelcome: SayWelcome });

  server.bindAsync(
    '0.0.0.0:50051',

    grpc.ServerCredentials.createInsecure(),

    () => {
      server.start();
    }
  );
}

main();
```

Now we will copy this code into our `welcome.proto` file.

```proto
syntax = "proto3";

package welcome;

// The welcome service definition.
service Welcome {
  // Sends a welcome
  rpc SayWelcome (WelcomeRequest) returns (WelcomeReply) {}
}

// The request message containing the user's name.
message WelcomeRequest {
  string name = 1;
}

// The response message containing the welcome
message WelcomeReply {
  string message = 1;
}
```

Lastly, we are going to add these run scripts to our `package.json` file.

```json
"scripts": {

"start:server": "nodemon welcome_server.js",

"start:client": "node welcome_client.js"

},
```

Now let's go to the command line and run the commands below in different tabs/windows. We should make sure that we start the server before the client. When doing so we should see the message `Message: Welcome Luke Skywalker` outputted in the command line window for the client.

```shell
npm run start:server
```

```shell
npm run start:client
```

## Final Thoughts

If you are interested in learning more then take a look at the main documentation for gRPC. The framework officially supports many languages, platforms and OS versions. These include JavaScript, TypeScript, C#, Node.js, Go, Kotlin, PHP and many more which you can find in the [documentation](https://grpc.io/docs/).

It is quite clear after reading this article that gRPC is awesome!

We covered a lot in this tutorial. We started by introducing gRPC and its various concepts. There is a lot more you can do with gRPC, read it in the docs [gRPC](https://grpc.io/) to find out more, or if you have any questions, connect with us here at [sprkl](https://sprkl.dev/).