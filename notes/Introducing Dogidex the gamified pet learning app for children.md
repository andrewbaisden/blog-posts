I have known about HarperDB for quite some time in fact I have already written two articles on it. [Creating React/Flask apps that connect to PostgreSQL and HarperDB](https://andrewbaisden.hashnode.dev/creating-reactflask-apps-that-connect-to-postgresql-and-harperdb) and [Creating React/Node apps that connect to PostgreSQL and HarperDB](https://andrewbaisden.hashnode.dev/creating-reactnode-apps-that-connect-to-postgresql-and-harperdb) which were highly popular on the DEV platform before I started cross posting. Anyway when I heard about this Hashnode and HarperDB Hackathon I just had to find a way to get involved.

This application is called Dogidex and the idea behind it is that it could potentially be used as a learning tool for children which would make learning new things fun and engaging. Due to the time constraints of working on other projects and having lots of interviews at the time the application is barebones and not as fully featured as I would have liked. Nonetheless the application is at least more on brand with HarperDB and makes up for the "Goldeneye" drama 😂

## Dogidex Technical Stack

**Back-End**: Node.js, HarperDB
**Front-End**: React

I decided to go with the tried and trusted React/Node combination as it is my preference and I have the most experience with it.

## The Design

I designed the application using Figma which has become my favourite vector design tool. In terms of design inspiration it was quite heavily inspired by Pokemon. I created the dog creative on the homepage using Figma and I used Photoshop to create the dog images which needed transparent backgrounds.

## Back-End Architecture

The back-end is fairly simple it is just a basic Express.js application that connects to the HarperDB instance. The first thing that I did was create the data for the REST API. For this I created a `.csv` file for the data. Fortunately VS Code has a great extension with linting for `.csv` so it was quite easy to build the data for the database. Once it was completed I created a new table in my HarperDB instance and then imported the `.csv` data into the table.

### Creating a HarperDB Database

First you need to create a HarperDB account and then create a database. I called my database **dogs**. Creating and setting up a HarperDB Database is very easy. Just follow this video [HarperDB Cloud Launch Tour](https://www.youtube.com/watch?v=fAKZxK-XamM&t=0s) and you can also take a look at the documentation for HarperDB with Node here [https://docs.harperdb.io/](https://docs.harperdb.io/).

**Login Credentials**

You will need an authorisation code to connect to HarperDB. First use your API tool to send a GET request to your HarperDB URL with your username and password. You need to use Basic Auth. Then use the generate code button and select Node.js and HTTP you will find your authorisation code in the headers code. The images below show you how it's done.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1601839963/harper-db-login_y1a2ym.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1601839963/harper-db-login_y1a2ym.jpg 'HarperDB Insomnia Login')

![https://res.cloudinary.com/d74fh3kw/image/upload/v1601839963/auth-code_ht1oel.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1601839963/auth-code_ht1oel.jpg 'HarperDB Auth')

**Connecting to HarperDB**

Once you are set up make sure that you update your `.env` file with your HarperDB credentials like below.

```bash
HARPERDB_URL="https://yourdatabase.harperdbcloud.com/"
HARPERDB_USERNAME="admin"
HARPERDB_PASSWORD="yourpassword"
HARPERDB_AUTH="yourauthcode"
```

Next I updated my `index.js` file with the code below. I imported the connection code for HarperDB, the database credentials for it and I also created GET routes. Axios is used for fetching the data from the HarperDB API.

```javascript
const express = require('express');
const cors = require('cors');
require('dotenv').config();
const axios = require('axios');

const app = express();

app.use(express.urlencoded({ extended: false }));
app.use(express.json());

// CORS implemented so that we don't get errors when trying to access the server from a different server location
app.use(cors());

// HarperDB Database routes

// GET: Fetch all dogs from the database
app.get('/online/harperdb', (req, res) => {
	const data = { operation: 'sql', sql: 'SELECT * FROM dev.dogs' };

	const config = {
		method: 'post',
		url: process.env.HARPERDB_URL,
		headers: {
			Authorization: `Basic ${process.env.HARPERDB_AUTH}`,
			'Content-Type': 'application/json',
		},
		data: data,
	};

	axios(config)
		.then((response) => {
			const data = response.data;
			console.log(data);
			res.json(data);
		})
		.catch((error) => {
			console.log(error);
		});
});

// GET: Fetch dog by dogId from the database
app.get('/online/harperdb/:dogId', (req, res) => {
	const dogId = req.params.dogId;
	console.log(dogId);

	const data = { operation: 'sql', sql: `SELECT * FROM dev.dogs WHERE id = "${dogId}"` };

	const config = {
		method: 'post',
		url: process.env.HARPERDB_URL,
		headers: {
			Authorization: `Basic ${process.env.HARPERDB_AUTH}`,
			'Content-Type': 'application/json',
		},
		data: data,
	};

	axios(config)
		.then((response) => {
			const data = response.data;
			console.log(data);
			res.json(data);
		})
		.catch((error) => {
			console.log(error);
		});
});

const port = process.env.PORT || 8000;

app.listen(port, () => console.log(`Server running on ${port}, http://localhost:${port}`));
```

## Front-End Architecture

As you can see the application is quite straightforward. There is a selection of dogs and you can view their profiles. Of course I had envisioned a feature rich application with so much functionality but the basis is there for future development.

The live version is here [https://dogidex.netlify.app/](https://dogidex.netlify.app/)

![https://res.cloudinary.com/d74fh3kw/image/upload/v1625096428/dogidex/dogidex_uiwbgw.webp](https://res.cloudinary.com/d74fh3kw/image/upload/v1625096428/dogidex/dogidex_uiwbgw.webp)

## Improvements that could be made with more time

For starters more features would be great 🤣 An application like this has the potential to work cross platform and could easily be turned into a full blown learning tool for children.

- Cross platform so that this app would be available on the web, desktop and mobile
- Full CRUD so that a user can add and remove the dogs
- More interactivity I had plans to incorporate lots of gamification features so the ability to basically manage all of the dogs like they are virtual pets or Pokemon. Being able to feed them, learn about different dog types and I even had a cool idea for **evolution** just like Pokemon but with puppies growing older.
- Encouraging learning so that children would understand what its like to care for a pet at a young age and how much time and care is required to keep them healthy and fit
- The gamification features make it fun but some of the underlying concepts would have reached kids how to have good time management and to be productive while also helping them to learn a topic that they might find boring otherwise

Those are just some improvements obviously there are infinite ideas that could be incorporated into this app if I had worked on it for a month and not just a few days because of time commitments 😅

## Final Thoughts

I really hope that you enjoyed reading this article and learned something from it. As a content creator and technical writer I am passionate about sharing my knowledge and helping other people reach their goals. Let's connect across social media you can find all of my social media profiles and blogs on [linktree](https://linktr.ee/andrewbaisden).

Peace ✌️
