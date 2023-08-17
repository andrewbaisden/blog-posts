## Introduction

Making websites is not what it used to be. Over the past ten years, it has changed from being a very straightforward area controlled by HTML, CSS, and JavaScript to a vast ecosystem of tools and frameworks, each with its own distinct features and capabilities. You need to have a solid understanding of several cutting-edge technologies if you want to become an expert in modern web development. The complexity of today's development environment necessitates an agile mind and a strong commitment to lifelong learning, from data fetching to authentication, rendering to backend, and containerisation.

This article is for people who are ready to step up their game and genuinely understand the practices of a modern JavaScript developer. Next.js, Auth.js, Databases, GraphQL, Docker, and Preevy will all be covered in this guide. We'll look at the server-side rendering and static site creation with Next.js. Auth.js will assist us in unravelling the secrets of robust and secure user authentication. We'll reimagine how we interact with APIs and handle data via the perspective of GraphQL. Docker will show us the tremendous containerisation options, and Preevy will provide us with the ability to provision a preview environment for our application. Finally, we will do a production deployment on [Vercel](https://vercel.com/), and [Netlify](https://www.netlify.com/) so that we can experience what it's like to have an application up and running on different platforms.

Are you ready to push the boundaries, test your knowledge, and possibly even redefine your perception of what current web development involves? Then strap in for a detailed review of understanding contemporary web programming. We will start by going over an introduction of each technology and then we will build an app to reinforce what we have learned.

> **The main aim of this article will be to create a simple application and then demonstrate the relationship between the tools. With this knowledge, you will be able to see how straightforward it is to deploy your Next.js applications online regardless of how basic or complex the codebase is.**

In the upcoming sections, we will go through these topics related to building modern Next.js applications:

- Using Next.js for web app development
- Adding authentication with Auth.js
- Databases for persisting state and storing data
- GraphQL the modern alternative to REST APIs
- Having a Docker development environment
- Setting up Preevy to provision preview environments
- Building and deploying our application

## Using Next.js for web app development

Next.js is a framework for building server-side rendered React apps, making it suitable for generating quick and dynamic web applications. It's significant for web app development because it helps with things like page routing, server-side rendering, and quick loading times, which are critical for generating a great user experience. Additionally, it is simple to use and has a growing community of developers who are always striving to improve it. It has already replaced Create React App as the number one React build tool.

Building a web application is just one stage of the development process we also have to think about making our applications secure using authentication. Let's now learn about Auth.js, a new modern way to add an authentication layer to our applications.

## Adding authentication with Auth.js

Auth.js is created by Vercel and is an open-source community project. It was originally called NextAuth.js until they rebranded and it is designed to be an authentication layer for the web. Auth.js helps developers to configure an authentication flow for their online projects. It is compatible with an extensive list of authentication providers along with additional choices. With Auth.js we can integrate many different providers into our applications, giving us the power to use them to log in and out. Some of the most well-known provider options include Google, GitHub, Facebook, Instagram and many more.

It currently supports frameworks like Next.js, Svelte.js and Solid.js with many more on the way. Let's now dive into databases and see why they are a good storage option for our data.

## Databases for persisting state and storing data

When it comes to storing information, many people choose databases. Databases have become a crucial aspect of most applications, whether you want to store user data or keep track of the state. They assist you in organising your data and ensuring that it is secure and accessible when needed. Databases can be used for a variety of purposes, ranging from analytics to powering websites and apps. As a result, they have become an indispensable tool for developers and businesses.

Several databases are available, each with unique features that can either be or might not prove suitable for our needs. The most common is RDBMS (relational database management systems), which stores data in tables with various columns that can be connected together. NoSQL databases, on the other hand, provide more scalability and flexibility and additional possibilities for customising how your data is stored.

Whatever choice you use, databases are an essential resource for preserving state and storing data. Their ability to simplify and automate activities makes them worthwhile to consider when developing apps or services. And their dependability assures that your data will be protected and accessible for a long time.

Now that we have an introduction to databases, let's move on to learning about GraphQL and why it's the perfect modern alternative to REST APIs.

## GraphQL the modern alternative to REST APIs

GraphQL is increasingly replacing conventional REST APIs as the preferred protocol. Instead of dealing with a vast and often burdensome payload of data, this powerful tool allows developers to request only what they need from an API. GraphQL also allows developers to query several resources at the same time via nesting, which can result in quicker and more efficient development. It also offers good documentation support, making it simple to understand and use, which makes GraphQL an appealing alternative for modern development.

Utilising GraphQL ensures that your technical stack is robust and up to date with current trends. With GraphQL, it is possible for it to be used on both the client and server sides. This means that you can choose to create a backend which will fetch the data from the API or you could have it running on the frontend so that you can skip creating a backend altogether. In this tutorial, we will use it on the front so there will be no need to create an Express.js backend server.

Another essential part of modern developer technical stacks is Docker. Let's keep reading and see how Docker can help us with our projects.

## Having a Docker development environment

Docker development involves more than just setting up a single development environment. It is about ensuring that your whole development process can be efficiently replicated, reused, and automated. With the proper configuration, you'll be able to swiftly and consistently build various settings, eventually saving time and money in the long run.

Docker allows developers to bundle their apps into "containers" that contain all of the essential code and dependencies for running them in production. You no longer need to wonder whether it works locally and will also work when it goes live. These containers are lightweight and easy to move across servers, allowing you to test new features without affecting old ones. Everything is carefully wrapped up together.

The last section we will cover before we start building our app will be Preevy. Let's learn how this new tool can help us to provision our preview environments.

## Setting up Preevy to provision preview environments

Preevy is created by LiveCycle and is used to assist development teams in improving their code-review operations by offering a simple and affordable approach to building temporary environments for each branch. These are also referred to as **Preview Environments**. Before merging changes on a branch, we can use preview environments to test, check, and see changes.

With Preevy, the difficulty of installing preview environments is decreased considerably, allowing all developers with a basic understanding of Docker to use it. We can create a development version via a URL which is typically appended to each pull/merge request. With this setup, we will have a version which is only for development and not production to play around with.

We will need to create an account with Amazon AWS so that we can use AWS Lightsail for the deployment. When using the aws-lightsail driver, Preevy can deploy virtual machines on AWS Lightsail. AWS Lightsail is Amazon's low-cost option for cloud-based virtual machines. AWS lightsail deployment time for a VM is typically under 2 minutes, and its monthly cost can be as cheap as $3.50, making them perfect for large-scale preview settings.

We now have a much greater understanding of what makes up a modern JavaScript full-stack application. It's time for us to start building our app so let's get to it!

## Building and deploying our application

The app that we are going to build is an e-commerce website like Amazon. It will be a basic example with a few page routes, two of which will require GitHub or Google authenticated sign-in before you can see the data on the pages.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1687372351/next-auth-store-app_ik1wq4.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1687372351/next-auth-store-app_ik1wq4.jpg)

> **We will be using hard code data in place of a database layer just to make things easier in this project. If this was a production-level application then we would set up a real database layer. There is no CRUD functionality this app has page routing and the logic for logging in and out of authenticated routes. It is easy enough to create your own more advanced applications once you understand these fundamentals.**

In addition, we are also going to be using the most up-to-date and latest [App Router](https://nextjs.org/docs/app) feature in Next.js which replaces the older [Pages Router](https://nextjs.org/docs/pages/building-your-application) setup. So we get a feel for using the latest syntax and codebase Next.js has available to us. Vercel will get priority in the code because they are the creators of Auth.js although we will cover Netlify deployments later.

Firstly ensure that you are aware of the prerequisites and that you have your developer environment set up.

### Prerequisites

- [Node.js](https://nodejs.org/en)
- [Next.js](https://nextjs.org/)
- [Auth.js](https://authjs.dev/)
- [Apollo GraphQL](https://www.apollographql.com/)
- [Docker](https://www.docker.com/)
- [Amazon Web Services (AWS)](https://aws.amazon.com/?nc2=h_lg) for AWS Lightsail deployments with Preevy
- [AWS CLI ](https://aws.amazon.com/cli/)
- [Preevy](https://preevy.dev/)
- [GitHub](https://github.com/) and [Google](https://www.google.com/) account for setting up authentication
- [Vercel](https://vercel.com/)
- [Netlify](https://www.netlify.com/)

With the prerequisites out of the way let us now start building our app in the upcoming section.

### Building the app

Firstly navigate to a directory on your computer like on the desktop so that we have a location to use for creating our project. Now run these commands to set up our project using Next.js.

```shell
mkdir store-project
cd store-project
npx create-next-app my-app
```

These are the settings I used:

✔ Would you like to use TypeScript with this project? … **No** / Yes
✔ Would you like to use ESLint with this project? … **No** / Yes
✔ Would you like to use Tailwind CSS with this project? … **No** / Yes
✔ Would you like to use `src/` directory with this project? … No / **Yes**
✔ Use App Router (recommended)? … No / **Yes**
✔ Would you like to customize the default import alias? … **No** / Yes

Now we are going to create the files and folders that we will be using for this project run the following commands:

```shell
touch .dockerignore .env .gitignore docker-compose.yml
cd my-app
touch .env.local Dockerfile
cd src/app
mkdir account account/account account/rewards
mkdir api api/auth api/auth/"[...nextauth]"
mkdir components delivery graphql queries utils
touch account/account/page.js account/account/page.module.css
touch account/rewards/page.js account/rewards/page.module.css
touch api/auth/"[...nextauth]"/route.js
touch components/MainMenu.js components/mainmenu.module.css components/Provider.js
touch delivery/page.js delivery/page.module.css
touch graphql/route.js
touch queries/clientQueries.js
touch utils/cors.js utils/withApollo.js
touch not-found.js page.module.css
cd ../../
```

We should now be in the root folder for `my-app` so now we will install some packages for the project so run these commands here.

```shell
npm i @apollo/client @apollo/server @as-integrations/next graphql graphql-tag next-auth
```

With our basic setup done for our project, we can now focus on adding the code to our files which we will do now. This step can be tedious but we will be almost done afterwards this is the longest step. We will save the `.env` and `.env.local` files until last because they require some extra steps to be done first.

Open the `store-project` folder in your code editor and add this code to the `.dockerignore` file and the `.gitignore` file in the root folder:

```shell
# See https://help.github.com/articles/ignoring-files/ for more about ignoring files.



# dependencies

/node_modules

/.pnp

.pnp.js



# testing

/coverage



# next.js

/.next/

/out/



# production

/build



# misc

.DS_Store

*.pem



# debug

npm-debug.log*

yarn-debug.log*

yarn-error.log*



# local env files

.env*.local



# vercel

.vercel



# typescript

*.tsbuildinfo

next-env.d.ts
```

Next, add this code to the `docker-compose.yml` file:

```yaml
version: '3'

services:
  my-app:
    container_name: my-app
    build:
      context: ./my-app
      dockerfile: Dockerfile
    environment:
      NEXTAUTH_URL: ${NEXTAUTH_URL}
      NEXTAUTH_SECRET: ${NEXTAUTH_SECRET}
      GITHUB_ID: ${GITHUB_ID}
      GITHUB_SECRET: ${GITHUB_SECRET}
      GOOGLE_ID: ${GOOGLE_ID}
      GOOGLE_SECRET: ${GOOGLE_SECRET}
    volumes:
      - ./my-app/src:/app/src
      - ./my-app/public:/app/public
    restart: always
    ports:
      - 3000:3000
```

Put this code in the `Dockerfile` :

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

Now we will replace the code inside of `next.config.js` with this so the app router feature is configured:

```javascript
/** @type {import('next').NextConfig} */

const nextConfig = {
  output: 'standalone',
};

module.exports = {
  nextConfig,

  experimental: {
    appDir: true,
  },
};

module.exports = nextConfig;
```

Moving on let's do the files inside of the `src/app` directory now. Add this to `account/account/page.js`:

```javascript
'use client';

import { useSession, signIn, signOut } from 'next-auth/react';

import { useQuery } from '@apollo/client';

import { GET_ACCOUNT } from '../../queries/clientQueries';

import withApollo from '../../utils/withApollo';

import MainMenu from '../../components/MainMenu';

import styles from './page.module.css';

const Account = () => {
  const { loading, error, data } = useQuery(GET_ACCOUNT);

  const { data: session, status } = useSession();

  const userEmail = session?.user?.email;

  if (loading)
    return (
      <>
        <MainMenu />

        <div className="container">
          <h1>Loading...</h1>
        </div>
      </>
    );

  if (error)
    return (
      <>
        <MainMenu />

        <div className="container">
          <h1>Oh no there is an error :(</h1>
        </div>
      </>
    );

  if (status === 'loading') {
    return <div>Please wait...</div>;
  }

  if (status === 'authenticated') {
    return (
      <>
        <MainMenu />

        <div className="container">
          <div className={styles.signinflow}>
            <p>Signed in as {userEmail}</p>

            <button onClick={() => signOut()} className={styles.signinflowbtn}>
              Sign out
            </button>
          </div>

          {!loading && !error && (
            <div>
              {data.account.map((account) => (
                <div key={account.id}>
                  <h1>{account.name}</h1>

                  <p>User ID: {account.id}</p>

                  <p>Country: {account.country}</p>

                  <p>Giftcard ID: {account.giftCardId}</p>

                  <p>Address: {account.address}</p>
                </div>
              ))}
            </div>
          )}
        </div>
      </>
    );
  }

  return (
    <>
      <MainMenu />

      <div className="container">
        <div className={styles.signinflow}>
          <button onClick={() => signIn('')} className={styles.signinflowbtn}>
            Sign in
          </button>

          <p>
            You are not currently signed in. Sign in here to view your profile.
          </p>
        </div>
      </div>
    </>
  );
};

export default withApollo(Account);
```

Put this in `account/account/page.module.css`:

```css
.signinflow {
  background-color: #131921;

  padding: 0.5rem;

  color: #ffffff;
}

.signinflowbtn {
  border: none;

  padding: 0.5rem;

  background: #febd69;

  font-weight: bold;

  cursor: pointer;

  margin: 1rem;
}
```

For the rewards page add this to `account/rewards/page.js`:

```javascript
'use client';

import { useSession, signIn, signOut } from 'next-auth/react';

import { useQuery } from '@apollo/client';

import { GET_REWARDS } from '../../queries/clientQueries';

import withApollo from '../../utils/withApollo';

import MainMenu from '../../components/MainMenu';

import styles from './page.module.css';

const Rewards = () => {
  const { loading, error, data } = useQuery(GET_REWARDS);

  const { data: session, status } = useSession();

  const userEmail = session?.user?.email;

  if (loading)
    return (
      <>
        <MainMenu />

        <div className="container">
          <h1>Loading...</h1>
        </div>
      </>
    );

  if (error)
    return (
      <>
        <MainMenu />

        <div className="container">
          <h1>Oh no there is an error :(</h1>
        </div>
      </>
    );

  if (status === 'loading') {
    return <div>Please wait...</div>;
  }

  if (status === 'authenticated') {
    return (
      <>
        <MainMenu />

        <div className="container">
          <div className={styles.signinflow}>
            <p>Signed in as {userEmail}</p>

            <button onClick={() => signOut()} className={styles.signinflowbtn}>
              Sign out
            </button>
          </div>

          {!loading && !error && (
            <div className={styles.vouchercontainer}>
              {data.rewards.map((vouchers) => (
                <div key={vouchers.id} className={styles.voucher}>
                  <div>
                    <div>
                      <p>Type: {vouchers.savingType}</p>

                      <p className={styles.voucherdescription}>
                        {vouchers.description}
                      </p>
                    </div>
                  </div>

                  <div>
                    <div>
                      {vouchers.info.map((data) => (
                        <div>
                          <p>Expiration Date: {data.valid}</p>

                          <p>
                            Code:{' '}
                            <span className={styles.vouchercode}>
                              {data.code}
                            </span>
                          </p>
                        </div>
                      ))}
                    </div>
                  </div>
                </div>
              ))}
            </div>
          )}
        </div>
      </>
    );
  }

  return (
    <>
      <MainMenu />

      <div className="container">
        <div className={styles.signinflow}>
          <button onClick={() => signIn('')} className={styles.signinflowbtn}>
            Sign in
          </button>

          <p>
            You are not currently signed in. Sign in here to view your rewards.
          </p>
        </div>
      </div>
    </>
  );
};

export default withApollo(Rewards);
```

This goes in `account/rewards/page.module.css`:

```css
.signinflow {
  background-color: #131921;

  padding: 0.5rem;

  color: #ffffff;
}

.signinflowbtn {
  border: none;

  padding: 0.5rem;

  background: #febd69;

  font-weight: bold;

  cursor: pointer;

  margin: 1rem;
}

.vouchercontainer {
  display: flex;

  flex-flow: row nowrap;

  justify-content: center;

  margin-top: 2rem;
}

.voucher {
  background: #ffffff;

  border: 1px solid black;

  padding: 1rem;

  width: 100%;
}

.voucherdescription {
  color: rgb(59, 191, 26);

  font-weight: bold;
}

.vouchercode {
  color: rgb(191, 26, 26);

  font-weight: bold;
}

@media screen and (max-width: 1500px) {
  .vouchercontainer {
    flex-flow: row wrap;
  }
}
```

We will add this code to `api/auth/[...nextauth]/route.js`:

```javascript
import NextAuth from 'next-auth';

import GithubProvider from 'next-auth/providers/github';

import GoogleProvider from 'next-auth/providers/google';

export const handler = NextAuth({
  providers: [
    GithubProvider({
      clientId: process.env.GITHUB_ID,

      clientSecret: process.env.GITHUB_SECRET,
    }),

    GoogleProvider({
      clientId: process.env.GOOGLE_ID,

      clientSecret: process.env.GOOGLE_SECRET,
    }),
  ],
});

export { handler as GET, handler as POST };
```

The components folder is next. Put this code in `components/MainMenu.js`:

```javascript
import Link from 'next/link';

import styles from './mainmenu.module.css';

export default function MainMenu() {
  return (
    <nav className={styles.mainmenu}>
      <Link href="/" className={styles.link}>
        e-store
      </Link>

      <Link href="/delivery" className={styles.link}>
        Delivery
      </Link>

      <Link href="/account/rewards" className={styles.link}>
        Rewards
      </Link>

      <Link href="/account/account" className={styles.link}>
        Account
      </Link>
    </nav>
  );
}
```

Remaining in the same folder this is for `components/mainmenu.module.css`:

```css
.mainmenu {
  background-color: #232f3e;

  padding: 0.5rem;

  display: flex;

  flex-flow: row nowrap;

  justify-content: space-around;
}

.link {
  color: #ffffff;

  text-decoration: none;
}
```

And this is going into `components/Provider.js`:

```javascript
'use client';

import { SessionProvider } from 'next-auth/react';

const Provider = ({ children }) => {
  return <SessionProvider>{children}</SessionProvider>;
};

export default Provider;
```

The file inside of `delivery/page.js` gets this code:

```javascript
'use client';

import MainMenu from '../components/MainMenu';

import styles from './page.module.css';

export default function Nutrition() {
  return (
    <>
      <MainMenu />

      <div className="container">
        <h1>Frequently Asked Questions</h1>

        <div className={styles.faqcontent}>
          <h2>
            Is free shipping on purchases over $25 available on all products?
          </h2>

          <p>
            Things sold and delivered by e-store are eligible, as are things
            sold by marketplace sellers when e-store is the dispatcher. You can
            combine qualifying goods worth less than $25 to produce an order
            worth more than $25 and qualify for free delivery.
          </p>
        </div>

        <div className={styles.faqcontent}>
          <h2>
            How can I order and pick up from an e-store Hub Locker or Gateway?
          </h2>

          <p>
            When you're all set to place your order, choose e-store Hub as your
            delivery address. We will send you an acknowledgement message with a
            barcode once your delivery arrives. Simply go to your chosen Locker
            or Gateway to pick up your package. Have your pickup message of
            confirmation with the barcode available when you arrive. You will
            scan the barcode yourself at the Locker; at the Gateway, the store
            clerk will check it before handing you your product. There is no
            need to provide identification while picking up.
          </p>
        </div>
      </div>
    </>
  );
}
```

And the CSS for `delivery/page.module.css`:

```css
.faqcontent {
  margin-bottom: 1rem;
}
```

Let's do our GraphQL route file with our data. Put this in `graphql/route.js`:

```javascript
import { ApolloServer } from '@apollo/server';

import { startServerAndCreateNextHandler } from '@as-integrations/next';

import { gql } from 'graphql-tag';

import allowCors from '../utils/cors';

const account = [
  {
    id: 'r89fdjk23r89yew234fg89h23',

    name: 'Mark Thomas',

    country: 'United States',

    giftCardId: '89dfviuhbbwerdfv897hwedfqdfqwf',

    address: `456 Maple Avenue, Austin, TX 78701`,
  },
];

const rewards = [
  {
    id: '1',

    savingType: 'Voucher',

    description: 'Save $2 at checkout',

    info: [
      {
        valid: '2023',

        code: '89wdfeqwh89fewh98fh',
      },
    ],
  },

  {
    id: '2',

    savingType: 'Voucher',

    description: 'Save 20% at checkout',

    info: [
      {
        valid: '2023',

        code: 'erfgerwgergewgewg345',
      },
    ],
  },

  {
    id: '3',

    savingType: 'Voucher',

    description: 'Save 25% at checkout',

    info: [
      {
        valid: '2023',

        code: '34fg67werf45y45ytg0a',
      },
    ],
  },

  {
    id: '4',

    savingType: 'Voucher',

    description: 'Save 5% at checkout',

    info: [
      {
        valid: '2023',

        code: 'er234dfrgdfsgerwerwge',
      },
    ],
  },

  {
    id: '5',

    savingType: 'Voucher',

    description: 'Save 50% at checkout',

    info: [
      {
        valid: '2023',

        code: 'gerwff4576jhey6233343',
      },
    ],
  },
];

// Define the GraphQL schema and resolvers

const typeDefs = gql`
  type Rewards {
    id: String

    savingType: String

    description: String

    info: [Rewards]
  }

  type Rewards {
    valid: String

    code: String
  }

  type Account {
    id: String

    name: String

    country: String

    giftCardId: String

    address: String
  }

  type Query {
    rewards: [Rewards]

    account: [Account]
  }
`;

const resolvers = {
  Query: {
    rewards: () => rewards,

    account: () => account,
  },
};

// Create the Apollo Server

const server = new ApolloServer({
  typeDefs,

  resolvers,
});

const handler = startServerAndCreateNextHandler(server, {
  context: async (req, res) => ({ req, res }),
});

export async function GET(request) {
  return handler(request);
}

export async function POST(request) {
  return handler(request);
}

export default allowCors(handler);
```

Following that file we have this code with our GraphQL queries which goes in `queries/clientQueries.js`:

```javascript
import { gql } from '@apollo/client';

const GET_ACCOUNT = gql`
  query {
    account {
      id
      name
      country
      giftCardId
      address
    }
  }
`;

const GET_REWARDS = gql`
  query {
    rewards {
      id
      savingType
      description
      info {
        valid
        code
      }
    }
  }
`;

export { GET_ACCOUNT, GET_REWARDS };
```

Almost done just a few files remain. Now onto the utility files. Add this code to `utils/cors.js`:

```javascript
const allowCors = (fn) => async (req, res) => {
  res.setHeader('Access-Control-Allow-Credentials', true);

  res.setHeader('Access-Control-Allow-Origin', '*');

  res.setHeader('Access-Control-Allow-Origin', req.headers.origin);

  res.setHeader(
    'Access-Control-Allow-Methods',

    'GET,OPTIONS,PATCH,DELETE,POST,PUT'
  );

  res.setHeader(
    'Access-Control-Allow-Headers',

    'X-CSRF-Token, X-Requested-With, Accept, Accept-Version, Content-Length, Content-MD5, Content-Type, Date, X-Api-Version'
  );

  if (req.method === 'OPTIONS') {
    res.status(200).end();

    return;
  }

  await fn(req, res);
};

export default allowCors;
```

Now this code will go inside of `utils/withApollo.js`:

```javascript
import { ApolloClient, InMemoryCache, ApolloProvider } from '@apollo/client';

import { useMemo } from 'react';

import { SessionProvider } from 'next-auth/react';

export function initializeApollo(initialState = null) {
  const _apolloClient = new ApolloClient({
    // Local GraphQL Endpoint

    uri: 'http://localhost:3000/graphql',

    // Add your Preevy GraphQL Endpoint

    // uri: 'https://yourapp.livecycle.run/graphql',

    // Add your Vercel GraphQL Endpoint

    // uri: 'https://yourapp.vercel.app/graphql',

    // Add your Netlify GraphQL Endpoint

    // uri: 'https://yourapp.netlify.app/graphql',

    cache: new InMemoryCache().restore(initialState || {}),
  });

  return _apolloClient;
}

export function useApollo(initialState) {
  const store = useMemo(() => initializeApollo(initialState), [initialState]);

  return store;
}

export default function withApollo(PageComponent) {
  const WithApollo = ({ apolloClient, apolloState, session, ...pageProps }) => {
    const client = useApollo(apolloState);

    return (
      <SessionProvider session={session}>
        <ApolloProvider client={client}>
          <PageComponent {...pageProps} />
        </ApolloProvider>
      </SessionProvider>
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

Let's finish the last few files now. Replace all the CSS in `globals.css` with this one:

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

body {
  background: #e3e6e6;

  font-family: 'Istok Web', sans-serif;
}

.container {
  margin: 0 auto;

  width: 100%;

  max-width: 120rem;

  padding: 2rem;
}
```

Replace the code in `layout.js` with this code:

```javascript
import './globals.css';

import { Istok_Web } from 'next/font/google';

const istok = Istok_Web({ subsets: ['latin'], weight: '400' });

export const metadata = {
  title: 'e-store App',

  description: 'Generated by create next app',
};

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body className={istok.className}>{children}</body>
    </html>
  );
}
```

This goes into `not-found.js`:

```javascript
'use client';

import MainMenu from './components/MainMenu';

export default function NotFound() {
  return (
    <>
      <MainMenu />

      <div className="container">
        <h1>404 Page Not Found</h1>
      </div>
    </>
  );
}
```

We will put this code in our homepage file which is the `page.js` file in the `app` folder so replace it with this code you see here:

```javascript
'use client';

import styles from './page.module.css';

import MainMenu from './components/MainMenu';

export default function Home() {
  return (
    <>
      <MainMenu />

      <div className="container">
        <main className={styles.maincontent}>
          <div className={styles.contentbox}>
            <h1>Sony WH-1000XM5 Noise Cancelling Wireless Headphones</h1>

            <p>
              For total convenience, these Bluetooth headphones can be paired
              with two devices at the same time.
            </p>
          </div>

          <div className={styles.contentbox}>
            <h1>PlayStation 5 Console</h1>

            <p>
              The PS5 console unleashes new gaming possibilities that you never
              anticipated
            </p>
          </div>

          <div className={styles.contentbox}>
            <h1>Xbox Series X</h1>

            <p>
              Introducing Xbox Series X, the fastest, most powerful Xbox ever.
            </p>
          </div>

          <div className={styles.contentbox}>
            <h1>SanDisk Extreme Pro 2TB Portable NVMe SSD</h1>

            <p>
              A forged aluminum chassis acts as a heat sink to deliver higher
              sustained speeds in a portable drive that’s tough enough to take
              on any adventure.
            </p>
          </div>

          <div className={styles.contentbox}>
            <h1>Apple 2023 MacBook Pro laptop M2 Pro</h1>

            <p>Take on demanding projects with the M2 Pro or M2 Max chip.</p>
          </div>

          <div className={styles.contentbox}>
            <h1>Samsung 43 Inch BU8000 UHD Crystal 4K Smart TV</h1>

            <p>
              Immerse Yourself In Exceptional Colour All In 4K - Dynamic Crystal
              Colour delivers a new level of UHD, allowing you to experience a
              billion shades of colour for a lifelike, vivid picture.
            </p>
          </div>
        </main>
      </div>
    </>
  );
}
```

And lastly, this goes into the `page.module.css` file in the `app` folder:

```css
.contentbox {
  background-color: #ffffff;

  padding: 1rem;

  width: 100%;

  max-width: 60rem;

  margin: 0 1rem 1rem 1rem;
}

.maincontent {
  display: flex;

  flex-flow: row nowrap;

  justify-content: center;

  padding: 1rem;
}

@media screen and (max-width: 1500px) {
  .maincontent {
    flex-flow: row wrap;
  }
}
```

Thats it! The main files are completed! It's time to deal with those ENV files now this is where we will set our environment variables so that we can get the authentication working on restricted routes. The account and rewards page will have an authentication layer on them.

#### Authentication setup

Our application uses Auth.js for authentication. It's possible to have many different sign-in providers for your application. This app is set up to use GitHub and Google logins. You need an ID and secret key from GitHub and Google which we will then put in our ENV files. Read the documentation and find your ID and secrets. In my opinion, it is much easier to do it with GitHub and you only need one of them to work so that you can see the authentication working in the app.

[GitHub Auth setup](https://authjs.dev/getting-started/oauth-tutorial)
[Google Auth setup](https://developers.google.com/identity/protocols/oauth2)

Make sure that you pay attention to the Authorization callback URL. It will look different depending on where your app is running and you will need to update or change it on GitHub and Google otherwise the authenticated pages won't get access. See the examples below for GitHub:

Localhost URL:

```shell
http://localhost:3000/api/auth/callback/github
```

Preevy URL:

```shell
https://yourapp.livecycle.run/api/auth/callback/github
```

Vercel URL:

```shell
https://yourapp.vercel.app/api/auth/callback/github
```

When you have your ID and secrets add them to both ENV files so `.env` and `.env.local`. We need two because one is for local development and the other is for production. Just copy the same code into both. See the example below and modify it with your ID and secrets.

Just two more things to mention, we need a secret for our `NEXTAUTH_SECRET` variable it can be anything you want. Just randomly generate a string of characters like you would for a secure password. The `NEXTAUTH_URL` is required for Preevy deployments without it the authentication will go to localhost when it's deployed online which is incorrect and will stop the page loading.

In some cases, we can get the authentication to work without having the `NEXTAUTH_URL` variable in the ENV file altogether. But it will only work on localhost, Docker and Vercel so it's safer to just keep it in there. We have set `NEXTAUTH_URL` to `http://localhost:3000/` because that is where we will run our app first.

```shell
NEXTAUTH_SECRET="yoursecret"

NEXTAUTH_URL="http://localhost:3000/"

GITHUB_ID="yourid"

GITHUB_SECRET="yoursecret"

GOOGLE_ID="yourid"

GOOGLE_SECRET="yoursecret"
```

The `NEXTAUTH_URL` variable will need to be changed depending on where our app is hosted and running.

See the examples here:

Localhost URL:

```shell
NEXTAUTH_URL="http://localhost:3000/"
```

Preevy URL:

```shell
NEXTAUTH_URL="https://yourapp.livecycle.run/"
```

Vercel URL:

```shell
NEXTAUTH_URL="https://yourapp.vercel.app/"
```

Everything should be complete now so let's run our app.

#### Running our app locally

To run our app locally go inside the `my-app` folder and run this command:

```shell
npm run dev
```

The GraphQL Apollo Server endpoint is here [http://localhost:3000/graphql](http://localhost:3000/graphql) so we can test our GraphQL queries in development. We can also change this endpoint inside of the file in the directory `utils/withApollo.js`. This becomes important when our app is online on Preevy and Vercel.

To run our app inside of Docker first make sure Docker is running on your computer. Stop the other local development server from running first because you can't have two applications using port 3000. Then run this command inside of the `store-project` root folder with the `docker-compose.yml` file:

```shell
docker-compose up
```

Now let's see how to get it to work as a preview environment on Preevy.

#### Creating a preview build on Preevy

You can follow the Preevy set-up in the [official documentation](https://preevy.dev/) and take a look at the [Preevy GitHub](https://github.com/livecycle/preevy) for more setup instructions. In this tutorial, we are using AWS Lightsail as our cloud host. The main Preevy commands are:

```shell
preevy init

## Add a flag and an id like 123
preevy up --id 123
```

Make sure that you add an `id` flag and a number afterwards otherwise, it could throw an error. Update the Authorization callback URL on GitHub and Google so it matches the Preevy URL that was generated and don't forget to change the `NEXTAUTH_URL` variable in the ENV file to the generated Preevy URL like this example:

```shell
NEXTAUTH_URL="https://yourapp.livecycle.run/"
```

Also can change the GraphQL endpoint inside of the file in the directory `utils/withApollo.js` to the URL endpoint for Preevy.

Run the command `preevy up --id 123 ` to push the latest changes again.

We have done so much already it's now time to finish it off with deployment so let's work on that in the final section.

#### Deploying our app on Vercel

The Vercel setup is pretty straightforward. Firstly create a repository on GitHub. I named mine **store-project** and then run the GIT commands inside of the `my-app` folder to push it to GitHub.

See this GIT code example here:

```shell
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/replacewithyourname/store-project.git
git push -u origin main
```

Then sign into Vercel and Add a new project.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1687374709/vercel-add-new-project_ekykhm.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1687374709/vercel-add-new-project_ekykhm.jpg)

Next import the repository you just created.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1687374911/vercel-import-project_qjze5r.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1687374911/vercel-import-project_qjze5r.jpg)

On the next screen configure your project and there is an option for environment variables so add all the environment variables in the ENV file to Vercel and then hit the deploy button.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1687376186/vercel-env_hvseta.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1687376186/vercel-env_hvseta.jpg)

Our app should be live on Vercel! However, the authenticated routes won't work yet we have to make some updates to the code like before.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1687376380/vercel-congrats_gyoj90.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1687376380/vercel-congrats_gyoj90.jpg)

Update the Authorization callback URL on GitHub and Google so it matches the Vercel URL that was generated this is the first step to get the authenticated pages working.

See the example here:

**Homepage URL**

```shell
https://store-project-qwerty.vercel.app/
```

**Authorization callback URL**

```shell
https://store-project-qwerty.vercel.app/api/auth/callback/github
```

Next, update the `NEXTAUTH_URL` variable on Vercel to the URL that Vercel generated for your app. You will find it under Settings > Environment Variables see the image for reference.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1687377198/vercel-env-update_fauzx6.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1687377198/vercel-env-update_fauzx6.jpg)

And finally like before don't forget to also change the GraphQL endpoint inside of the file in the directory `utils/withApollo.js` to the URL endpoint for Vercel.

```javascript
export function initializeApollo(initialState = null) {
  const _apolloClient = new ApolloClient({
    // Local GraphQL Endpoint

    // uri: 'http://localhost:3000/graphql',

    // Add your Preevy GraphQL Endpoint

    // uri: 'https://yourapp.livecycle.run/graphql',

    // Add your Vercel GraphQL Endpoint

    uri: 'https://yourapp.vercel.app/graphql',

    // Add your Netlify GraphQL Endpoint

    // uri: 'https://yourapp.netlify.app/graphql',

    cache: new InMemoryCache().restore(initialState || {}),
  });

  return _apolloClient;
}
```

Now push the latest changes back to GitHub so that Vercel can rebuild your codebase with the new Vercel URL. Assuming you did everything correctly you should now see working authenticated routes for your app deployed on Vercel!

![https://res.cloudinary.com/d74fh3kw/image/upload/v1687377802/vercel-auth-route_uisj0x.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1687377802/vercel-auth-route_uisj0x.jpg)

So with Vercel deployment complete let's do Netlify now.

#### Deploying our app on Netlify

Sign into Netlify and then import an existing project.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1687378959/netlify-project_w8xodt.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1687378959/netlify-project_w8xodt.jpg)

Next, connect to your GitHub and import the project you created.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1687381475/netlify-import-project-git_v6mi56.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1687381475/netlify-import-project-git_v6mi56.jpg)

![https://res.cloudinary.com/d74fh3kw/image/upload/v1687381524/netlify-pick-git_fgcqag.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1687381524/netlify-pick-git_fgcqag.jpg)

Once again add in those ENV variables and hit deploy.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1687382128/netlify-env_mid7ls.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1687382128/netlify-env_mid7ls.jpg)

And just like before our app should be live on Netlify! We have the same problem as before though, the authenticated routes won't work yet we have to make some updates to the code like the previous section.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1687382469/netlify-online_vqbx1h.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1687382469/netlify-online_vqbx1h.jpg)

Firstly like in the Vercel example update the Authorization callback URL on GitHub and Google so it matches the Netlify URL that was generated for your app. Next, update the `NEXTAUTH_URL` variable on Netlify to the URL that Netlify generated for your app. You will find it under Site settings > Environment Variables see the image for reference.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1687382904/netlify-auth_irtvcf.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1687382904/netlify-auth_irtvcf.jpg)

And just like we did before don't forget to also change the GraphQL endpoint inside of the file in the directory `utils/withApollo.js` to the URL endpoint for Netlify.

```javascript
export function initializeApollo(initialState = null) {
  const _apolloClient = new ApolloClient({
    // Local GraphQL Endpoint

    // uri: 'http://localhost:3000/graphql',

    // Add your Preevy GraphQL Endpoint

    // uri: 'https://yourapp.livecycle.run/graphql',

    // Add your Vercel GraphQL Endpoint

    // uri: 'https://yourapp.vercel.app/graphql',

    // Add your Netlify GraphQL Endpoint

    uri: 'https://yourapp.netlify.app/graphql',

    cache: new InMemoryCache().restore(initialState || {}),
  });

  return _apolloClient;
}
```

Finally, push the latest changes back to GitHub so that Netlify can rebuild your codebase with the new Netlify URL.

Assuming you did everything correctly you should now see working authenticated routes for your app deployed on Netlify!

> If the authenticated route goes to [http://localhost:3000/api/auth/callback/github](http://localhost:3000/api/auth/callback/github) or [http://localhost:3000/api/auth/callback/google](http://localhost:3000/api/auth/callback/google) then in the Deploys section on Netlify press the Trigger deploy button and select **Clear cache and deploy site** and that should fix the error.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1687385557/netlify-trigger-deploy_wgpyjc.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1687385557/netlify-trigger-deploy_wgpyjc.jpg)

We are done! Our application is complete and we have a version deployed online on Vercel and Netlify good job! It might not be obvious but it's worth noting that the authentication part of our app will only work on Vercel or Netlify not both at the same time. We would have to duplicate the codebase and create a unique app for them on GitHub and Google to get them to work at the same time.

## Conclusion

To summarise, current web development is an ever-changing profession that necessitates a grasp and command of a variety of tools and technologies. The ones we've looked at in this article Next.js, Auth.js, databases, GraphQL, Docker, and Preevy aren't exhaustive, but they're nonetheless important in modern web development settings. Vercel and Netlify are some of the many serverless deployment platforms that make it easy for us to deploy our production applications online so that the world can access them.

With its hybrid static and server rendering, Next.js provides a solid platform for developing scalable, high-performance apps. Auth.js simplifies the difficult work of user authentication, allowing developers to quickly add secure login features. Our database study revealed the need for organised data storage and retrieval, and GraphQL shone as an alternative to REST for developing flexible and efficient APIs. Docker, an essential technology for building isolated environments, is at the heart of today's software development and deployment cycle. Finally, Preevy, an emerging player in the pre-provisioning preview environment for static sites, can accelerate development build testing considerably.

Each of these technologies has distinct advantages and applications. The true value of these tools, however, is in their combination, when utilised successfully together, these tools can allow developers to design extremely efficient, performant, secure, and scalable online applications. Mastering these technologies is no easy task it takes time, effort, and a lot of practice. However, the payoff is well worth the effort. By becoming proficient in these tools, you are not only providing yourself with the abilities required to flourish in the present web development scene, but you are also preparing yourself for the future as these technologies advance and influence the world of web development.

So, keep researching, keep learning, and bear in mind that mastery in web development is a path of ongoing learning and adaptability.
