# How to use HarperDB custom functions to build your entire backend

## What is HarperDB

When HarperDB first started they were a distributed database platform. Essentially this meant that anyone could spin up a cloud instance for creating a database for storing your data online. These databases supported both SQL and NoSQL capabilities which made them very versatile because they had a solution which could cater to everyone.

Version 3.0 of HarperDB worked like any traditional database. In a typical full stack application a developer would have their API code hosted on a server somewhere. And that server would do an API call to the HarperDB cloud platform basically allowing the developer to connect to their database instance and retrieve the data they wanted.

## HarperDB Custom Functions

Towards the end of 2021 HarperDB released version 3.1 which introduced a new feature for the platform. HarperDB grew from a distributed database to a distributed application development platform. Basically this means that you can now host your database and server API on the same platform with full CRUD functionality! It is a single solution that takes care of all of your backend requirements.

HarperDB now offers [custom functions](https://harperdb.io/docs/custom-functions/) which are quite similar to AWS Lambda functions. The basic methodology is that you write your business logic in code and then decide when you are going to use it. What this means is that the service should be significantly faster when compared to traditional methods because the data does not need to move over different networks and servers. It is all in one place making it significantly easier to maintain.

The Custom Functions use Node.js and Fastify which means that they are pretty much just Node.js projects. This bonus essentially gives you access to the whole npm ecosystem boosting your development workflow.

## How to use HarperDB Custom Functions

In this tutorial I will give you a quick introduction to using Custom Functions on HarperDB. We will create an application that is called **Ancient Civilizations Timeline**. It will just be a simple website that retrieves some data from a HarperDB database using the new Custom Functions feature.

This will be the tech stack:

Frontend: HTML, CSS, TypeScript, React
Backend: Node.js, HarperDB

### Prerequisites

Firstly you need to create a [HarperDB](https://harperdb.io) account if you don't have one already.

#### Step 1 - Create an account

Sign up for a free account

![https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646586964/harperdb-sign-up-screen_j4g0mf.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646586964/harperdb-sign-up-screen_j4g0mf.jpg)

#### Step 2 - Create a new organisation

Create a new organisation

![https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646587087/harperdb-create-organization_bag4yz.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646587087/harperdb-create-organization_bag4yz.jpg)

Add a new organisation

![https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646587087/harperdb-add-new-organization_z55frg.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646587087/harperdb-add-new-organization_z55frg.jpg)

#### Step 3 - Create a New HarperDB Cloud Instance

Create a New HarperDB Cloud Instance

![https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646587677/harperdb-create-new-cloud-instance_k19yui.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646587677/harperdb-create-new-cloud-instance_k19yui.jpg)

Click the button on the left for **Create AWS or Verizon Wavelength Instance**

![https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646587679/harperdb-select-instance-type_svstlr.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646587679/harperdb-select-instance-type_svstlr.jpg)

Choose the option for HarperDB Cloud on AWS and then click the button for Instance Info.

![https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646587678/harperdb-choose-cloud-provider_nsldac.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646587678/harperdb-choose-cloud-provider_nsldac.jpg)

Create an instance name and user credentials then click the Instance Details button.

![https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646587678/harperdb-instance-info_z4lkn6.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646587678/harperdb-instance-info_z4lkn6.jpg)

Select the options for FREE RAM and Storage Size. Select whichever region you prefer and then click the button to confirm the instance details. Please be aware that you are limited to 1 free cloud instance across organisation's you own.

![https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646587679/harperdb-instance-specs_vzsgjq.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646587679/harperdb-instance-specs_vzsgjq.jpg)

Agree to the terms and then click the add instance button.

![https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646590776/harperdb-add-instance_xaazmv.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646590776/harperdb-add-instance_xaazmv.jpg)

#### Step 4 - View your HarperDB Cloud Instance

Now you should have an organisation

![https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646588792/harperdb-organization-redacted_ccpg4w.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646588792/harperdb-organization-redacted_ccpg4w.jpg)

When you click on your organisation you should see your cloud instance

![https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646589044/harperdb-instance-redacted_ptfook.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646589044/harperdb-instance-redacted_ptfook.jpg)

Click on that and you will see the database screen

![https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646591118/harperdb-db-screen_eagtct.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646591118/harperdb-db-screen_eagtct.jpg)

## Creating the backend database and API on HarperDB

### Database Setup

Now create a schema called **timeline** and give the table and hash attribute a name of **history**.

![https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646681881/harperdb-schema-table_aopfkj.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646681881/harperdb-schema-table_aopfkj.jpg)

Go to this [repo](https://github.com/andrewbaisden/harperdb-civilizations/blob/main/frontend/src/data/civilisation.sql) and copy the SQL query. Now go to the query link on HarperDB and copy and paste the SQL query into it. Finally click on the execute button to run the query. This will add the data to the database. The query is very big because I created some custom SVG images using Figma which I then converted into Base64 to store in the database.

![https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646682043/harperdb-sql-query-highlight_x3afyg.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646682043/harperdb-sql-query-highlight_x3afyg.jpg)

Return to the database table screen by clicking on the browse button and you should see a table filled with data. If you put your mouse cursor over the image icons you can see what the images look like.

![https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646682131/harperdb-table-data-highlight_inp3mi.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646682131/harperdb-table-data-highlight_inp3mi.jpg)

### API Setup

You should now have a database that has a table full of data. The next step will be to create a custom function so that we can fetch the data using a REST GET request. Click on the functions link and then click on the enable custom functions button.

![https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646682355/harperdb-enable-custom-functions_slqqjs.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646682355/harperdb-enable-custom-functions_slqqjs.jpg)

You should be on the functions screen now. Give your project a name of **api** and then replace all of the code in the editor with the code below. You should see a link for custom functions server url in the bottom left corner. Copy the link into your browser and add the endpoint **api** at the end. The endpoint should return your database data as JSON.

```javascript
'use strict';

const customValidation = require('../helpers/example');

// eslint-disable-next-line no-unused-vars,require-await
module.exports = async (server, { hdbCore, logger }) => {
  // GET, WITH NO preValidation AND USING hdbCore.requestWithoutAuthentication
  // BYPASSES ALL CHECKS: DO NOT USE RAW USER-SUBMITTED VALUES IN SQL STATEMENTS
  server.route({
    url: '/',
    method: 'GET',
    handler: (request) => {
      request.body = {
        operation: 'sql',
        sql: 'SELECT * FROM timeline.history ORDER BY id',
      };
      return hdbCore.requestWithoutAuthentication(request);
    },
  });
};
```

This is the structure for my endpoint:

[https://functions-cloud-1-abaisden.harperdbcloud.com/api](https://functions-cloud-1-abaisden.harperdbcloud.com/api)

## Creating the frontend React Application

We will be using create-react-app and TypeScript for the frontend. Create a project folder for the React frontend and then use your terminal to run the commands below inside of that folder.

```bash
npx create-react-app my-app --template typescript
cd my-app
npm start
```

You should see the default React boilerplate in your web browser. Open the project you just created in your code editor. Replace the code in `app.css` and `app.tsx` with the code below, and delete all the code in `index.css` and leave blank.

Don't forget to add your own API URL inside of `App.tsx` replacing the one that I have put there. This is the line that you need to look for inside of `App.tsx`

```typescript
// Replace this API URL with your Custom Functions Server URL
const API = 'https://functions-cloud-1-test.harperdbcloud.com/api';
```

### App.css

```css
@import url('https://fonts.googleapis.com/css2?family=League+Spartan:wght@400;500;700&display=swap');

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
  font-size: 1.6rem;
  font-family: 'League Spartan', sans-serif;
  color: black;
  background-color: white;
}

header {
  text-align: center;
}

header h1 {
  text-align: center;
  margin-top: 1rem;
  text-transform: uppercase;
  font-size: 4rem;
}

.container {
  padding: 2rem;
}

.civilisation-container {
  display: flex;
  flex-flow: column nowrap;
  align-items: center;
}

.civilisation {
  display: flex;
  flex-flow: column nowrap;
  text-align: center;
  align-items: center;
  border: 0.2rem solid black;
  border-radius: 1rem;
  padding: 1rem;
}

.civilisation h1 {
  text-transform: uppercase;
  margin-top: 2rem;
}

.civilisation img {
  width: 100%;
  max-width: 20rem;
  margin: 2rem 0 2rem 0;
}

.civilisation ul li {
  list-style: none;
}

.civilisation p {
  margin: 2rem 0 2rem 0;
  font-size: 1.8rem;
  line-height: 2rem;
}

.timeline-line {
  background: black;
  height: 4rem;
  width: 1rem;
}
```

### App.tsx

```typescript
import { useState, useEffect } from 'react';
import './App.css';

const App = () => {
  interface timeline {
    current_location: string;
    description: string;
    highlights: string;
    history: string;
    id: number;
    image: string;
    original_location: string;
    period: string;
    timeline: string;
    __createdtime__: number;
    __updatedtime__: number;
  }

  useEffect(() => {
    const getApi = () => {
      // Replace this API URL with your Custom Functions Server URL
      const API = 'https://functions-cloud-1-test.harperdbcloud.com/api';

      fetch(API)
        .then((response) => {
          return response.json();
        })
        .then((data) => {
          console.log(data);
          setLoading(false);
          setData(data);
        })
        .catch((err) => {
          console.log(err);
        });
    };

    getApi();
  }, []);
  const [loading, setLoading] = useState<boolean>(false);
  const [data, setData] = useState<timeline[]>([]);
  return (
    <>
      <header>
        <h1>Human Civilization</h1>
        <p>
          An Ancient Civilizations Timeline for 8 of the most influential
          cultures in human history
        </p>
      </header>

      <div className="container">
        {loading ? (
          <div>
            <h1>Loading...</h1>
          </div>
        ) : (
          <div>
            {data.map((civilisation) => (
              <div className="civilisation-container">
                <div className="civilisation" key={civilisation.id}>
                  <h1>{civilisation.timeline}</h1>
                  <img src={civilisation.image} alt={civilisation.timeline} />
                  <ul>
                    <li>
                      <strong>Period: </strong>
                      {civilisation.period}
                    </li>
                    <li>
                      <strong>Original Location:</strong>{' '}
                      {civilisation.original_location}
                    </li>
                    <li>
                      <strong>Current Location:</strong>{' '}
                      {civilisation.current_location}
                    </li>
                    <li>
                      <strong>Highlights: </strong>
                      {civilisation.highlights}
                    </li>
                  </ul>
                  <p>{civilisation.description}</p>
                </div>
                <div className="timeline-line"></div>
              </div>
            ))}
          </div>
        )}
      </div>
    </>
  );
};

export default App;
```

Assuming you did everything correctly you should be able to see the application working in your web browser. Congratulations you just learned how to use HarperDB custom functions and how to connect them to a React frontend. We covered doing a GET request in this tutorial of course it is possible to do full CRUD requests too if you read the documentation.

![https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646691854/harperdb-civilisations_ibbqtu.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/c_scale,w_800/v1646691854/harperdb-civilisations_ibbqtu.jpg)
