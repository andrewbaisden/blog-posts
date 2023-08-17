## Introduction

Building successful and efficient web apps needs two things: a strong technological foundation, and a solid approach to managing the work itself.

Many development resources focus on one or the other. There are many good technical resources documenting how to build with various technologies and frameworks. There are also many good sources of insight for how to go about managing the development workflow across multiple stakeholders. 

But in this article, I will attempt to combine both into one and illustrate how I leveraged some great technologies to not only build a full-stack application, but also to manage the process and the pre-release workflow.

## Technologies I used

We'll be looking at how I worked with four main technologies: Node.js, GraphQL, Next.js, and [Preevy](https://github.com/livecycle/preevy). Each of these tools has been impactful for the broader web development community, and this is why I thought this was an interesting project and tech stack example to share with the community.

Node.js, for example, provides developers with scalable and efficient backend development tools. Then there's GraphQL, a cutting-edge data query language that's changing the way we handle and modify data. Next.js is a sophisticated React framework that aids in the creation of highly performant and SEO-friendly front-end interfaces. Finally, Preevy is a tool for quickly and easily provisioning pre-release preview environments on your cloud (Amazon, Google or Microsoft). Preevy's shareable preview environments are a useful way for developers to share their latest code changes, get feedback and collaborate with other stakeholders before any code is merged to staging or production, enabling developers to enjoy a faster pre-release review workflow.

Our summary of building a full-stack application will cover the following topics:

- Building the Node.js Express backend server
- Building the Next.js frontend server
- Running the project in Docker
- Provisioning a shareable preview environment using [Preevy](https://github.com/livecycle/preevy)

## Building a "food menu" app in public

I've written this summary in the style of a "learning in public" diary. Hopefully this will make the content both interesting and accessible to a wide audience.

The app that we will be building will be for a food menu. Essentially there will be a Node.js backend with a GraphQL server that has an endpoint for our data which will be hard coded. And the Next.js frontend will connect to the Node.js backend to retrieve the data using GraphQL queries.

## Prerequisites

- [Node.js](https://nodejs.org/en)
- [Next.js](https://nextjs.org/)
- [Docker](https://www.docker.com/)
- [Preevy](https://github.com/livecycle/preevy)
- [Amazon Web Services (AWS) and AWS CLI](https://aws.amazon.com/)

Make sure you have the prerequisites now let's get started!

## Building the Node.js Express backend server

We are going to start by creating our project locally on our computer. Navigate to a directory and run the commands below to setup our project and backend structure:

```shell
mkdir menu-project
cd menu-project
mkdir server
touch docker-compose.yml
cd server
npm init -y
npm i express express-graphql graphql cors
npm i -D dotenv nodemon
mkdir data schema
touch .env Dockerfile index.js
touch data/menu.js schema/schema.js
```

Next, open the project in a code editor and then add the upcoming code to the correct files.

Put this code in `data/menu.js`:

```javascript
const bases = [
  {
    id: '1',

    menuItem: 'Base',

    name: 'Egg Noodles',
  },

  {
    id: '2',

    menuItem: 'Base',

    name: 'Whole-wheat Noodles',
  },

  {
    id: '3',

    menuItem: 'Base',

    name: 'Rice Noodles',
  },

  {
    id: '4',

    menuItem: 'Base',

    name: 'Udon Noodles',
  },

  {
    id: '5',

    menuItem: 'Base',

    name: 'Jasmine Rice',
  },

  {
    id: '6',

    menuItem: 'Base',

    name: 'Whole-grain Rice',
  },
];

const vegetables = [
  {
    id: '1',

    menuItem: 'Vegetables',

    name: 'Pak Choi',
  },

  {
    id: '2',

    menuItem: 'Vegetables',

    name: 'Shiitake Mushrooms',
  },

  {
    id: '3',

    menuItem: 'Vegetables',

    name: 'Champignon Mushrooms',
  },

  {
    id: '4',

    menuItem: 'Vegetables',

    name: 'Mixed Peppers',
  },

  {
    id: '5',

    menuItem: 'Vegetables',

    name: 'Broccoli',
  },

  {
    id: '6',

    menuItem: 'Vegetables',

    name: 'Spinach',
  },

  {
    id: '7',

    menuItem: 'Vegetables',

    name: 'Baby Corn',
  },

  {
    id: '8',

    menuItem: 'Vegetables',

    name: 'Red Onion',
  },

  {
    id: '9',

    menuItem: 'Vegetables',

    name: 'Bamboo Shoots',
  },
];

const meats = [
  {
    id: '1',

    menuItem: 'Meat',

    name: 'Chicken',
  },

  {
    id: '2',

    menuItem: 'Meat',

    name: 'Chicken Katsu',
  },

  {
    id: '3',

    menuItem: 'Meat',

    name: 'Beef',
  },

  {
    id: '4',

    menuItem: 'Meat',

    name: 'Pulled Beef',
  },

  {
    id: '5',

    menuItem: 'Meat',

    name: 'Bacon',
  },

  {
    id: '6',

    menuItem: 'Meat',

    name: 'Pork',
  },

  {
    id: '7',

    menuItem: 'Meat',

    name: 'Duck',
  },

  {
    id: '8',

    menuItem: 'Meat',

    name: 'Prawns',
  },

  {
    id: '9',

    menuItem: 'Meat',

    name: 'Tofu',
  },
];

const sauces = [
  {
    id: '1',

    menuItem: 'Sauce',

    name: 'Sweet Teriyaki',
  },

  {
    id: '2',

    menuItem: 'Sauce',

    name: 'Sweet and Sour',
  },

  {
    id: '3',

    menuItem: 'Sauce',

    name: 'Garlic and black pepper',
  },

  {
    id: '4',

    menuItem: 'Sauce',

    name: 'Oyster Sauce',
  },

  {
    id: '5',

    menuItem: 'Sauce',

    name: 'Hot soybean sauce',
  },

  {
    id: '6',

    menuItem: 'Sauce',

    name: 'Yellow curry & coconut',
  },

  {
    id: '7',

    menuItem: 'Sauce',

    name: 'Peanut',
  },

  {
    id: '8',

    menuItem: 'Sauce',

    name: 'Asian spiced red sauce',
  },
];

module.exports = { bases, vegetables, meats, sauces };
```

This code will go into `schema/schema.js`:

```javascript
const { bases, vegetables, meats, sauces } = require('../data/menu');

const {
  GraphQLObjectType,

  GraphQLID,

  GraphQLString,

  GraphQLList,

  GraphQLSchema,
} = require('graphql');

const BaseType = new GraphQLObjectType({
  name: 'Base',

  fields: () => ({
    id: { type: GraphQLID },

    menuItem: { type: GraphQLString },

    name: { type: GraphQLString },
  }),
});

const VegetableType = new GraphQLObjectType({
  name: 'Vegetable',

  fields: () => ({
    id: { type: GraphQLID },

    menuItem: { type: GraphQLString },

    name: { type: GraphQLString },
  }),
});

const MeatType = new GraphQLObjectType({
  name: 'Meat',

  fields: () => ({
    id: { type: GraphQLID },

    menuItem: { type: GraphQLString },

    name: { type: GraphQLString },
  }),
});

const SauceType = new GraphQLObjectType({
  name: 'Sauce',

  fields: () => ({
    id: { type: GraphQLID },

    menuItem: { type: GraphQLString },

    name: { type: GraphQLString },
  }),
});

const RootQuery = new GraphQLObjectType({
  name: 'RootQueryType',

  fields: {
    bases: {
      type: new GraphQLList(BaseType),

      resolve(parent, args) {
        return bases;
      },
    },

    base: {
      type: BaseType,

      args: { id: { type: GraphQLID } },

      resolve(parent, args) {
        return bases.find((base) => base.id === args.id);
      },
    },

    vegetables: {
      type: new GraphQLList(VegetableType),

      resolve(parent, args) {
        return vegetables;
      },
    },

    vegetable: {
      type: VegetableType,

      args: { id: { type: GraphQLID } },

      resolve(parent, args) {
        return vegetables.find((vegetable) => vegetable.id === args.id);
      },
    },

    meats: {
      type: new GraphQLList(MeatType),

      resolve(parent, args) {
        return meats;
      },
    },

    meat: {
      type: MeatType,

      args: { id: { type: GraphQLID } },

      resolve(parent, args) {
        return meats.find((meat) => meat.id === args.id);
      },
    },

    sauces: {
      type: new GraphQLList(SauceType),

      resolve(parent, args) {
        return sauces;
      },
    },

    sauce: {
      type: SauceType,

      args: { id: { type: GraphQLID } },

      resolve(parent, args) {
        return sauces.find((sauce) => sauce.id === args.id);
      },
    },
  },
});

module.exports = new GraphQLSchema({
  query: RootQuery,
});
```

And here we have our `.env` file:

```shell
NODE_ENV = "development"

PORT = 8080
```

Let's put this code in the `Dockerfile`:

```shell
FROM node:18

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 8080

CMD ["node", "index.js"]
```

And our `index.js` file gets this server code:

```javascript
const express = require('express');

const cors = require('cors');

require('dotenv').config();

const { graphqlHTTP } = require('express-graphql');

const schema = require('./schema/schema');

const app = express();

app.use(cors());

app.use(
  '/graphql',

  graphqlHTTP({
    schema,

    graphiql: process.env.NODE_ENV === 'development',
  })
);

const port = process.env.PORT || 8080;

app.listen(port, () =>
  console.log(`Server running on port ${port}, http://localhost:${port}`)
);
```

And lastly the `docker-compose.yml` file:

```yaml
version: '3'
services:
  server:
    container_name: server
    build:
      context: ./server
      dockerfile: Dockerfile
    volumes:
      - ./server:/app
    ports:
      - '8080:8080'
    environment:
      - NODE_ENV=development

  client:
    container_name: client
    build:
      context: ./client
      dockerfile: Dockerfile
    volumes:
      - ./client/src:/app/src
      - ./client/public:/app/public
    restart: always
    ports:
      - 3000:3000
```

We just have to add these run scripts to the `package.json` file and we are good to go:]

```json
"scripts": {

"start": "node index.js",

"dev": "nodemon index.js"

},
```

Now with the backend part of our project setup just go into the root folder for the server and run the command below to start the backend server:

```shell
npm run start
```

Just go to [http://localhost:8080/graphql](http://localhost:8080/graphql) to see your GraphQL API.

Next up is the front end let's get to it.

## Building the Next.js frontend server

Change your directory so that it is in the root of the `menu-project` folder and run the commands below to set up our project to use Next.js.

```shell
npx create-next-app client
```

Complete the setup I used this configuration here:

✔ Would you like to use TypeScript with this project? … **No** / Yes
✔ Would you like to use ESLint with this project? … **No** / Yes
✔ Would you like to use Tailwind CSS with this project? … **No** / Yes
✔ Would you like to use `src/` directory with this project? … No / **Yes**
✔ Use App Router (recommended)? … No / **Yes**
✔ Would you like to customize the default import alias? … **No** / Yes

`cd` into the `client` folder and run this command to install the packages we will need:

```shell
npm i @apollo/client graphql
```

We need to create project files now so let's run this code to get them done:

```shell
touch Dockerfile
cd src/app
mkdir components queries utils
touch components/Bases.js components/Meats.js components/Sauces.js components/Vegetables.js
touch queries/clientQueries.js
touch utils/withApollo.js
```

All that's left is to add the code to our files and we are done. So starting with `components/Bases.js`:

```javascript
'use client';

import { useQuery } from '@apollo/client';

import { GET_BASE } from '../queries/clientQueries';

import withApollo from '../utils/withApollo';

const Bases = () => {
  const { loading, error, data } = useQuery(GET_BASE);

  if (loading) return <p>Loading bases...</p>;

  if (error) return <p>The food failed to load there is a problem</p>;

  return (
    <div>
      {!loading && !error && (
        <div className="base-box">
          <div>
            <div className="cost-container">
              <h1>01</h1>

              <p>$5.95 only one</p>
            </div>

            <h2>
              Chose <br />
              your base
            </h2>

            {data.bases.map((bases) => (
              <div key={bases.id}>
                <table>
                  <tr>
                    <td>
                      {bases.id} {bases.name}
                    </td>
                  </tr>
                </table>
              </div>
            ))}
          </div>
        </div>
      )}
    </div>
  );
};

export default withApollo(Bases);
```

Next up is `components/Meats.js`:

```javascript
'use client';

import { useQuery } from '@apollo/client';

import { GET_MEAT } from '../queries/clientQueries';

import withApollo from '../utils/withApollo';

const Meats = () => {
  const { loading, error, data } = useQuery(GET_MEAT);

  if (loading) return <p>Loading meats...</p>;

  if (error) return <p>The food failed to load there is a problem</p>;

  return (
    <div>
      {!loading && !error && (
        <div className="meat-box">
          <div>
            <div className="cost-container">
              <h1>03</h1>

              <p>$1.25 each 2 Max</p>
            </div>

            <h2>
              Choose <br /> your Meats
            </h2>

            {data.meats.map((meats) => (
              <div key={meats.id}>
                <table>
                  <tr>
                    <td>
                      {meats.id} {meats.name}
                    </td>
                  </tr>
                </table>
              </div>
            ))}
          </div>
        </div>
      )}
    </div>
  );
};

export default withApollo(Meats);
```

Following that add this code to `components/Sauces.js`:

```javascript
'use client';

import { useQuery } from '@apollo/client';

import { GET_SAUCE } from '../queries/clientQueries';

import withApollo from '../utils/withApollo';

const Sauces = () => {
  const { loading, error, data } = useQuery(GET_SAUCE);

  if (loading) return <p>Loading sauces...</p>;

  if (error) return <p>The food failed to load there is a problem</p>;

  return (
    <div>
      {!loading && !error && (
        <div className="sauces-box">
          <div>
            <div className="cost-container">
              <h1>04</h1>

              <p>FREE</p>
            </div>

            <h2>
              Choose <br />
              your Sauces
            </h2>

            {data.sauces.map((sauces) => (
              <div key={sauces.id}>
                <table>
                  <tr>
                    <td>
                      {sauces.id} {sauces.name}
                    </td>
                  </tr>
                </table>
              </div>
            ))}
          </div>
        </div>
      )}
    </div>
  );
};

export default withApollo(Sauces);
```

This code will be going into `components/Vegetables.js`:

```javascript
'use client';

import { useQuery } from '@apollo/client';

import { GET_VEGETABLE } from '../queries/clientQueries';

import withApollo from '../utils/withApollo';

const Vegetables = () => {
  const { loading, error, data } = useQuery(GET_VEGETABLE);

  if (loading) return <p>Loading vegetables...</p>;

  if (error) return <p>The food failed to load there is a problem</p>;

  return (
    <div>
      {!loading && !error && (
        <div className="vegetable-box">
          <div>
            <div className="cost-container">
              <h1>02</h1>

              <p>$1.25 each 4 Max</p>
            </div>

            <h2>
              Choose <br />
              your Vegetables
            </h2>

            {data.vegetables.map((vegetables) => (
              <div key={vegetables.id}>
                <table>
                  <tr>
                    <td>
                      {vegetables.id} {vegetables.name}
                    </td>
                  </tr>
                </table>
              </div>
            ))}
          </div>
        </div>
      )}
    </div>
  );
};

export default withApollo(Vegetables);
```

Now over to the `queries/clientQueries.js`:

```javascript
import { gql } from '@apollo/client';

const GET_BASE = gql`
  query getBase {
    bases {
      id

      name

      menuItem
    }
  }
`;

const GET_VEGETABLE = gql`
  query getVegetable {
    vegetables {
      id

      name

      menuItem
    }
  }
`;

const GET_MEAT = gql`
  query getMeat {
    meats {
      id

      name

      menuItem
    }
  }
`;

const GET_SAUCE = gql`
  query getSauce {
    sauces {
      id

      name

      menuItem
    }
  }
`;

export { GET_BASE, GET_VEGETABLE, GET_MEAT, GET_SAUCE };
```

Almost done this code is for `utils/withApollo.js`:

```javascript
import { ApolloClient, InMemoryCache, ApolloProvider } from '@apollo/client';

import { useMemo } from 'react';

export function initializeApollo(initialState = null) {
  const _apolloClient = new ApolloClient({
    // Local GraphQL Endpoint

    uri: 'http://localhost:8080/graphql',

    // Add your Preevy GraphQL Endpoint

    // uri: 'https://your-backend-server-livecycle.run/graphql',

    cache: new InMemoryCache().restore(initialState || {}),
  });

  return _apolloClient;
}

export function useApollo(initialState) {
  const store = useMemo(() => initializeApollo(initialState), [initialState]);

  return store;
}

export default function withApollo(PageComponent) {
  const WithApollo = ({ apolloClient, apolloState, ...pageProps }) => {
    const client = useApollo(apolloState);

    return (
      <ApolloProvider client={client}>
        <PageComponent {...pageProps} />
      </ApolloProvider>
    );
  };

  // On the server

  if (typeof window === 'undefined') {
    WithApollo.getInitialProps = async (ctx) => {
      const apolloClient = initializeApollo();

      let pageProps = {};

      if (PageComponent.getInitialProps) {
        pageProps = await PageComponent.getInitialProps(ctx);
      }

      if (ctx.res && ctx.res.finished) {
        // When redirecting, the response is finished.

        // No point in continuing to render

        return pageProps;
      }

      const apolloState = apolloClient.cache.extract();

      return {
        ...pageProps,

        apolloState,
      };
    };
  }

  return WithApollo;
}
```

Next up our CSS in `globals.css` so replace all the code with this one:

```css
*,
*::before,
*::after {
  margin: 0;

  padding: 0;

  box-sizing: border-box;
}

html {
  font-size: 16px;
}

header h1 {
  text-align: center;

  color: #ffffff;

  font-size: 4rem;

  text-transform: uppercase;
}

h1 {
  color: #1c1917;
}

h2 {
  color: #1c1917;

  font-size: 1.4rem;

  text-transform: uppercase;

  border-top: 0.3rem solid black;

  border-bottom: 0.3rem solid black;

  margin-bottom: 1rem;

  padding: 1rem 0 1rem 0;
}

body {
  background: #374151;
}

.container {
  width: 100%;

  max-width: 90rem;

  margin: 2rem auto;

  display: flex;

  flex-flow: row wrap;

  justify-content: space-around;

  background: #f9fafb;

  padding: 2rem;
}

.base-box,
.vegetable-box,
.meat-box,
.sauces-box {
  background: #f43f5e;

  width: 20rem;

  height: auto;

  padding: 1rem;

  color: #ffffff;

  font-weight: bold;

  margin-bottom: 2rem;
}

.cost-container {
  display: flex;

  flex-flow: row nowrap;

  justify-content: space-between;

  align-items: center;

  margin-bottom: 1rem;
}

.cost-container p {
  background: #eff6ff;

  padding: 0.2rem;

  color: #f43f5e;

  font-size: 1rem;
}

@media screen and (max-width: 800px) {
  .container {
    flex-flow: column;

    align-items: center;
  }
}
```

Just one more to go after this, so next is the `page.js` file and like before replace all the code with what we have here:

```javascript
'use client';

import Bases from './components/Bases';

import Vegetables from './components/Vegetables';

import Meats from './components/Meats';

import Sauces from './components/Sauces';

export default function Home() {
  return (
    <>
      <header>
        <h1>Menu</h1>
      </header>

      <div className="container">
        <Bases />

        <Vegetables />

        <Meats />

        <Sauces />
      </div>
    </>
  );
}
```

Finally, let's complete our project by putting this code in the `Dockerfile` in the client folder:

```shell
FROM node:18-alpine

WORKDIR /app

# Install dependencies based on the preferred package manager

COPY package.json yarn.lock* package-lock.json* pnpm-lock.yaml* ./

RUN \

if [ -f yarn.lock ]; then yarn --frozen-lockfile; \

elif [ -f package-lock.json ]; then npm ci; \

elif [ -f pnpm-lock.yaml ]; then yarn global add pnpm && pnpm i; \

# Allow install without lockfile, so example works even without Node.js installed locally

else echo "Warning: Lockfile not found. It is recommended to commit lockfiles to version control." && yarn install; \

fi

COPY src ./src

COPY public ./public

COPY next.config.js .

# Next.js collects completely anonymous telemetry data about general usage. Learn more here: https://nextjs.org/telemetry

# Uncomment the following line to disable telemetry at run time

# ENV NEXT_TELEMETRY_DISABLED 1

# Note: Don't expose ports here, Compose will handle that for us

# Start Next.js in development mode based on the preferred package manager

CMD \

if [ -f yarn.lock ]; then yarn dev; \

elif [ -f package-lock.json ]; then npm run dev; \

elif [ -f pnpm-lock.yaml ]; then pnpm dev; \

else yarn dev; \

fi
```

Now with the frontend and backend side of our project setup just go into the root folder for the `client` and run the command below to start the frontend server:

```shell
npm run dev
```

Double-check that your backend server is still running and you should see the menu which is receiving data from the backend server.

The next section will show us how to run the app inside of a Docker container so on we go.

## Running the project in Docker

Getting your application to run in Docker is super easy. First, make sure that Docker is running on your computer and that the other servers are not running because they will use the same ports. Then just ensure that you are inside the root folder for `menu-project` and then run the command `docker-compose up`. This will run the backend and frontend servers at the same time. Now just got to the same URLs as before for the server and client to see everything working.

The server is running on [http://localhost:8080](http://localhost:8080)
The client is running on [http://localhost:3000](http://localhost:3000)

Lastly, its time to deploy a preview environment using Preevy. By doing this we can share our work very easily with other people working on the project. They'll be able to see the latest version of the app with a single click, without needing to see how it looks or behaves in our development environment. This has already saved me hours of back and forth and I'm very happy to have found this tool and included it in my workflow.

## Creating a provision preview environment on Preevy

First, read the documentation on [Preevy](https://preevy.dev/) and install it and then get ready to run the commands here to create a provisioning environment. Inside the root folder for `menu-project` run the following commands:

```shell
preevy init
preevy up --id 321
```

You must pass an `--id` flag with a string of numbers. I used 321 as an example which should work. The setup might take some time to complete because it has to create the backend and the front end on AWS. When it's complete you should get two URL's one for the server and one for the client see the example here:

```shell
server  8080 https://your-url-server.livecycle.run/
client  3000 https://your-url-client.livecycle.run/
```

Clicking on the links should take you to both servers running online. You will notice that the page is showing errors and not loading our data on the client link. That's because it's still set to `http://localhost:8080/graphql` in your code. Update the `uri` in the file `client/src/app/utils/withApollo.js` to your Preevy server GraphQL endpoint and then run the command `preevy up --id 321` again to push the latest changes. 

Now the page should be showing data from our GraphQL API.

## Conclusion

Ultimately, the combination of tools like Node.js, GraphQL, Next.js is transforming the online development environment by bringing improved performance, flexibility, and data privacy compliance to the forefront. When these technologies are combined, they constitute a strong toolbox that enables developers to create scalable, efficient, and privacy-conscious apps.

And tools like Preevy facilitate an only better developer experience by enabling developers lightning fast ways to securely deploy and share their work with others, so they can collect clear feedback and release higher-quality products.

Hopefully, you've found that this article presents a realistic strategy for exploiting the synergy of these technologies.

However, because technology is always evolving, it is obligatory for every developer to constantly research and experiment with these tools. With this knowledge, you'll be well-equipped to take your web development talents to the next level, keeping on the cutting edge of technical innovation and creating apps that truly make a difference.