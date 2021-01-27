# Creating React/Node apps that connect to PostgreSQL and HarperDB

I'm sure that most of you are already more than familiar with the MERN stack. Having a React front end with a Node/Express back end that connects to a MongoDB database. Well, I will show you just how easy it is to connect to a Node back end which uses a PostgreSQL database to persist the data. And as a bonus I will even show you how to connect to [https://harperdb.io/](https://harperdb.io/) which is a SQL/NoSQL data management platform. It is fully indexed, doesn't duplicate data, and runs on any device from the edge to the cloud.

I will assume that you already have an understanding of JavaScript, Node and SQL as this guide is meant to be a quick introduction.

You will be creating an app that looks like the image below.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1601743727/meta-movies-blog_rh9omg.png](https://res.cloudinary.com/d74fh3kw/image/upload/v1601743727/meta-movies-blog_rh9omg.png "Meta Movies")

__Prerequisites__

- Insomnia or Postman API App installed
- NPM/Node Installed on your computer
- PostgreSQL installed and setup

## Create a PostgreSQL Database

For this guide I will be using Valentina Studio as a GUI to manage the local PostgreSQL database which you can find here [https://www.valentina-db.com/en/valentina-studio-overview](https://www.valentina-db.com/en/valentina-studio-overview) However feel free to use whatever tool you like you can even use the command line to interact with your database if you prefer.

Firstly create a database called `metacritic` and then use the SQL below the images to create a table called movies.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1601740643/create-database_ss4dhj.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1601740643/create-database_ss4dhj.jpg "Create SQL Database")

![https://res.cloudinary.com/d74fh3kw/image/upload/v1601740641/sql-query-editor_zekzhp.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1601740641/sql-query-editor_zekzhp.jpg "Open SQL Editor")

![https://res.cloudinary.com/d74fh3kw/image/upload/v1601740643/create-table_zohikv.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1601740643/create-table_zohikv.jpg "Create SQL Table")

```sql
CREATE TABLE movies (
    movie_id SERIAL PRIMARY KEY,
    movie_name VARCHAR(200) NOT NULL,
    img_url TEXT NOT NULL,
    release_year INT NOT NULL,
    summary TEXT NOT NULL,
    director VARCHAR(200) NOT NULL,
    genre VARCHAR(100) NOT NULL,
    rating VARCHAR(100) NOT NULL,
    movie_runtime INT NOT NULL,
    meta_score INT NOT NULL
)
```

Then use the SQL below the image to add some data to the table movies.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1601740647/insert-data_d0f7mz.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1601740647/insert-data_d0f7mz.jpg "Insert data into table movies")

```sql
INSERT INTO movies (movie_name, img_url, release_year, summary, director, genre, rating, movie_runtime, meta_score)
VALUES ('Casino Royale', 'https://static.metacritic.com/images/products/movies/9/08b5f3a45845fa3b6d1cb5f4978b5081-250h.jpg', 2006, 'After earning his license to kill James Bonds first 007 mission takes him to Madagascar where he is to spy on a terrorist. Not everything goes as planned and Bond decides to investigate independently of MI6.', 'Martin Campbell', 'Action', 'PG-13', 144, 80),('Tenet', 'https://static.metacritic.com/images/products/movies/7/a60818c40f69031bf30ca846444011e4-250h.jpg', 2020, 'Armed with only one word - Tenet - and fighting for the survival of the entire world the Protagonist (John David Washington) journeys through a twilight world of international espionage on a mission that will unfold in something beyond real time. Not time travel. Inversion.', 'Christopher Nolan', 'Action', 'PG-13', 150, 69),('Mulan', 'https://static.metacritic.com/images/products/movies/0/a496c3f832582876dc9b0d66197cab78-250h.jpg', 2020, 'When the Emperor of China issues a decree that one man per family must serve in the Imperial Army to defend the country from Northern invaders Hua Mulan the eldest daughter of an honored warrior steps in to take the place of her ailing father. Masquerading as a man Hua Jun she is tested every step of the way and must harness her inner-strength and embrace her true potential. It is an epic journey that will transform her into an honored warrior and earn her the respect of a grateful nation…and a proud father.', 'Niki Caro', 'Action', 'PG-13', 115, 67),('The Old Guard','https://static.metacritic.com/images/products/movies/7/b1db3c24db156b33c9fcfbbc199fcfcb-250h.jpg', 2020, 'Led by a warrior named Andy (Charlize Theron) a covert group of tight-knit mercenaries with a mysterious inability to die have fought to protect the mortal world for centuries. But when the team is recruited to take on an emergency mission and their extraordinary abilities are suddenly exposed it’s up to Andy and Nile (Kiki Layne) the newest soldier to join their ranks to help the group eliminate the threat of those who seek to replicate and monetize their power by any means necessary.', 'Gina Prince-Bythewood', 'Action', 'R', 125, 70),('Greyhound', 'https://static.metacritic.com/images/products/movies/4/499215874bac5acda666be3659bacf7e-250h.jpg', 2020, 'In the early days of WWII an international convoy of 37 Allied ships led by captain Ernest Krause (Tom Hanks) in his first command of a U.S. destroyer crosses the treacherous North Atlantic while hotly pursued by wolf packs of Nazi U-boats.', 'Aaron Schneider', 'Action', 'PG-13', 91, 64),('The New Mutants', 'https://static.metacritic.com/images/products/movies/4/8fcef9e9a93457f7a0fdf2a51cf30a0d-250h.jpg', 2020, 'In an isolated hospital young mutants are being held for psychiatric monitoring. When strange occurrences begin to take place both their new mutant abilities and their friendships will be tested as they battle to try and make it out alive.', 'Josh Boone', 'Action', 'PG-13', 94, 43),('I Used to Go Here', 'https://static.metacritic.com/images/products/movies/5/9456ab11b0bd3b457f32c6c58157bf95-250h.jpg', 2020, 'Following the lackluster launch of her debut novel 35-year-old writer Kate Conklin (Gillian Jacobs) receives an invitation from her former professor and old crush (Jemaine Clement) to speak at her alma mater. With her book tour canceled and her ego deflated Kate decides to take the trip wondering if returning to her old college as a published author might give her the morale boost she sorely needs. Instead she falls into a comical regression – from misadventures with eccentric twenty-year-olds to feelings of jealousy toward her former professor’s new favorite student. Striking the balance between bittersweet and hilarious Kate takes a journey through her past to redefine her future.', 'Kris Rey', 'Comedy', 'PG-13', 80, 68),('Hooking Up', 'https://static.metacritic.com/images/products/movies/0/fffb93ea39fcce7d65563163daa57c4c-250h.jpg', 2020, 'She (Brittany Snow) is an adventurous writer pumping out scandalous content for a lifestyle magazine. He (Sam Richardson) is a hopeless romantic who’s just been dumped by his high school sweetheart and given a medical diagnosis that’s left him shook. After a chance meeting the mismatched duo hit the road on a cross country trip to provide them both some much needed healing.', 'Nico Raineau', 'Drama', 'R', 104, 44),('Infamous', 'https://static.metacritic.com/images/products/movies/4/6da52f15b0fec577a53de1255cff6518-250h.jpg', 2020, 'Living in a small Florida town and working at a diner was never Arielles (Bella Thorne) dream life. Shes always wanted more. Fame. Popularity. Admiration. When she falls for a recently paroled young criminal named Dean she drags him back into a life of danger learning that posting their criminal exploits on social media is an easy way to viral fame. Obsessed with their rising number of followers they embark on a dangerous adventure together that leads to robbery cop chases and even murder. Heading to Hollywood the City of Stars they will realize what it takes to become famous and have to decide if this dangerous lifestyle is really worth it.', 'Joshua Caldwell', 'Drama', 'PG-13', 100, 40),('The LEGO Movie', 'https://static.metacritic.com/images/products/movies/7/55a09ad4264baf7d3e32b23a693d2307-250h.jpg', 2014, 'An ordinary LEGO minifigure, mistakenly thought to be the extraordinary MasterBuilder, is recruited to join a quest to stop an evil LEGO tyrant from gluing the universe together.', 'Christopher Miller and Phil Lord', 'Action', 'PG', 100, 83)
```

Run the SQL below to see all of the data in the table movies.

```sql
SELECT * FROM movies
```

![https://res.cloudinary.com/d74fh3kw/image/upload/v1601740641/select-all-movies_vqxgrh.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1601740641/select-all-movies_vqxgrh.jpg "Select all from movies table SQL Query")

## Create a Node/Express back end Server

First navigate to a location like your desktop or a folder and then use the code below to set up your project by using your terminal application.

```bash
mkdir meta-movies-app
cd meta-movies-app
mkdir backend
cd backend
npm init -y
npm i express cors dotenv axios knex pg
touch index.js
touch .gitignore
touch .env
```

Open the project in your code editor and then create a Node server in the `index.js` file

```javascript
const express = require('express');
const cors = require('cors');

const app = express();

app.use(cors());

app.get('/', (req, res) => res.send('Home Route'));

const port = process.env.PORT || 5000;

app.listen(port, () => console.log(`Server running on port ${port}, http://localhost:${port}`));
```

Add this run script to your `package.json` file. 

```json
	"scripts": {
		"start": "node index.js"
	},
```

Add this code to your `.gitignore` file in the root folder.

```bash
.env
node_modules
```

Run the application from the back end folder and go to your browser window to see the homepage.

```bash
npm run start
```

## Connect to the PostgreSQL database

Add your database name, username and password like in the example below to your `.env` file. I believe that the username is always __postgres__ when working with postgres databases locally.

```bash
DATABASE_HOST="127.0.0.1"
DATABASE="metacritic"
DATABASE_USERNAME="postgres"
DATABASE_PASSWORD="yourdatabasepassword"
```

Now update the `index.js` file in the root folder with the code below.

```javascript
const express = require('express');
const cors = require('cors');
const knex = require('knex');
require('dotenv').config();

const db = knex({
	client: 'pg',
	connection: {
		host: process.env.DATABASE_HOST,
		user: process.env.DATABASE_USERNAME,
		password: process.env.DATABASE_PASSWORD,
		database: process.env.DATABASE,
	},
});

const app = express();

app.use(express.urlencoded({ extended: false }));
app.use(express.json());

// CORS implemented so that we don't get errors when trying to access the server from a different server location
app.use(cors());

// GET: Fetch all movies from the database
app.get('/', (req, res) => {
	db.select('*')
		.from('movies')
		.then((data) => {
			console.log(data);
			res.json(data);
		})
		.catch((err) => {
			console.log(err);
		});
});

const port = process.env.PORT || 5000;

app.listen(port, () => console.log(`Server running on port ${port}, http://localhost:${port}`));
```

Restart your server and go to your browser window and reload the page. You should see the data in your database for the table movies returned as json and the data is also logged to your terminal window.

You can look at the documentation for the Knex.js package to learn more about the code [http://knexjs.org/](http://knexjs.org/)

## Implementing some CRUD functionality

Replace the code in your `index.js` file with the code below. It is now possible to create, read update and delete data from the database. Restart your Node server to see the changes.

```javascript
const express = require('express');
const cors = require('cors');
const knex = require('knex');
require('dotenv').config();

const db = knex({
	client: 'pg',
	connection: {
		host: process.env.DATABASE_HOST,
		user: process.env.DATABASE_USERNAME,
		password: process.env.DATABASE_PASSWORD,
		database: process.env.DATABASE,
	},
});

const app = express();

app.use(express.urlencoded({ extended: false }));
app.use(express.json());

// CORS implemented so that we don't get errors when trying to access the server from a different server location
app.use(cors());

// GET: Fetch all movies from the database
app.get('/', (req, res) => {
	db.select('*')
		.from('movies')
		.then((data) => {
			console.log(data);
			res.json(data);
		})
		.catch((err) => {
			console.log(err);
		});
});

// GET: Fetch movie by movieId from the database
app.get('/:movieId', (req, res) => {
	const movieId = req.params.movieId;
	db.select('*')
		.from('movies')
		.where('movie_id', '=', movieId)
		.then((data) => {
			console.log(data);
			res.json(data);
		})
		.catch((err) => {
			console.log(err);
		});
});

// POST: Create movies and add them to the database
app.post('/add-movie', (req, res) => {
	const { movieName, imgUrl, releaseYear, summary, director, genre, rating, movieRuntime, metaScore } = req.body;
	db('movies')
		.insert({
			movie_name: movieName,
			img_url: imgUrl,
			release_year: releaseYear,
			summary: summary,
			director: director,
			genre: genre,
			rating: rating,
			movie_runtime: movieRuntime,
			meta_score: metaScore,
		})
		.then(() => {
			console.log('Movie Added');
			return res.json({ msg: 'Movie Added' });
		})
		.catch((err) => {
			console.log(err);
		});
});

// DELETE: Delete movie by movieId from the database
app.delete('/delete-movie', (req, res) => {
	const movieId = req.body;
	const movieIdToDelete = Number(movieId.movieId);
	console.log(movieIdToDelete);
	db('movies')
		.where('movie_id', '=', movieIdToDelete)
		.del()
		.then(() => {
			console.log('Movie Deleted');
			return res.json({ msg: 'Movie Deleted' });
		})
		.catch((err) => {
			console.log(err);
		});
});

// PUT: Update movie by movieId from the database
app.put('/update-movie', (req, res) => {
	db('movies')
		.where('movie_id', '=', 1)
		.update({ movie_name: 'Goldeneye' })
		.then(() => {
			console.log('Movie Updated');
			return res.json({ msg: 'Movie Updated' });
		})
		.catch((err) => {
			console.log(err);
		});
});

const port = process.env.PORT || 5000;

app.listen(port, () => console.log(`Server running on port ${port}, http://localhost:${port}`));
```

### Using an API tool to test the different endpoints

In this guide I will be using the Insomnia API app to perform different CRUD requests. Use the screenshots as an example to see it work on your computer.

__GET: Fetch all movies from the database__

Just go to [http://127.0.0.1:5000/](http://127.0.0.1:5000/) and hit send to see all of the database data returned as json

![https://res.cloudinary.com/d74fh3kw/image/upload/v1601560293/fetch_all_egp8v5.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1601560293/fetch_all_egp8v5.jpg "Fetch all movies")

__GET: Fetch movie by movieId from the database__

Just go to [http://127.0.0.1:5000/1](http://127.0.0.1:5000/1) and hit send to see the movie that is matched with that ID returned as json. It will work with any ID number as long as it is in the database.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1601560293/fetch_by_movieId_afkn0e.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1601560293/fetch_by_movieId_afkn0e.jpg "Fetch movie by movieId")

__POST: Create movies and add them to the database__

Send a POST request to [http://127.0.0.1:5000/add-movie](http://127.0.0.1:5000/add-movie) with key value pair data as displayed in the example screenshot. Then go to the Fetch all movies route to see the new entry. Alternatively you can just use your database GUI or the CLI to see the new database entry.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1601560293/post_qzeccc.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1601560293/post_qzeccc.jpg "Add to the database")

__DELETE: Delete movie by movieId from the database__

Send a DELETE request to the route [http://127.0.0.1:5000/delete-movie](http://127.0.0.1:5000/delete-movie) using the name movieId. And as the value use any ID that is in the database to delete that entry.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1601560293/delete_k3zcif.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1601560293/delete_k3zcif.jpg "Delete from the database")

__PUT: Update movie by movieId from the database__

Use your API tool and send a PUT request to [http://127.0.0.1:5000/update-movie](http://127.0.0.1:5000/update-movie) to update an entry in the database. Go to the bottom of the `index.js` file to see the code for the UPDATE route. You can change the SQL query to update any of the fields in the table and then all you have to do is select the movie_id to update its entry. You can see the Javascript code and SQL query below.

Python

```javascript
// PUT: Update movie by movieId from the database
app.put('/update-movie', (req, res) => {
	db('movies')
		.where('movie_id', '=', 1)
		.update({ movie_name: 'Goldeneye' })
		.then(() => {
			console.log('Movie Updated');
			return res.json({ msg: 'Movie Updated' });
		})
		.catch((err) => {
			console.log(err);
		});
});
```

SQL

```sql
UPDATE movies SET movie_name = 'Goldeneye'
WHERE movie_id = 1
```

Well done you just created a Node app that connects to a PostgreSQL database. The next section will be about HarperDB.

## Create a HarperDB Database

First you need to create a HarperDB account and then create a database. I called my database "movies". Creating and setting up a HarperDB Database is very easy. Just follow this video [HarperDB Cloud Launch Tour](https://www.youtube.com/watch?v=fAKZxK-XamM&t=0s) and you can also take a look at the documentation for HarperDB with Node here [https://docs.harperdb.io/](https://docs.harperdb.io/).

__Login Credentials__

You will need an authorisation code to connect to HarperDB. First use your API tool to send a GET request to your HarperDB URL with your username and password. You need to use Basic Auth. Then use the generate code button and select Node.js and HTTP you will find your authorisation code in the headers code. The images below show you how it's done.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1601839963/harper-db-login_y1a2ym.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1601839963/harper-db-login_y1a2ym.jpg "HarperDB Insomnia Login")

![https://res.cloudinary.com/d74fh3kw/image/upload/v1601839963/auth-code_ht1oel.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1601839963/auth-code_ht1oel.jpg "HarperDB Auth")

__Connecting to HarperDB__

Once you are set up make sure that you update your `.env` file with your HarperDB credentials like below.

```bash
DATABASE_HOST="127.0.0.1"
DATABASE="metacritic"
DATABASE_USERNAME="postgres"
DATABASE_PASSWORD="yourdatabasepassword"
HARPERDB_URL="https://yourdatabase.harperdbcloud.com/"
HARPERDB_USERNAME="admin"
HARPERDB_PASSWORD="yourpassword"
HARPERDB_AUTH="yourauthcode"
```

Now update your `index.js` file with the code below. We imported HarperDB, the database credentials for it and also created routes which you can find at the bottom with full CRUD requests. Axios is used for fetching data from the HarperDB API.

```javascript
const express = require('express');
const cors = require('cors');
const knex = require('knex');
require('dotenv').config();
const axios = require('axios');

const db = knex({
	client: 'pg',
	connection: {
		host: process.env.DATABASE_HOST,
		user: process.env.DATABASE_USERNAME,
		password: process.env.DATABASE_PASSWORD,
		database: process.env.DATABASE,
	},
});

const app = express();

app.use(express.urlencoded({ extended: false }));
app.use(express.json());

// CORS implemented so that we don't get errors when trying to access the server from a different server location
app.use(cors());

// GET: Fetch all movies from the database
app.get('/', (req, res) => {
	db.select('*')
		.from('movies')
		.then((data) => {
			console.log(data);
			res.json(data);
		})
		.catch((err) => {
			console.log(err);
		});
});

// GET: Fetch movie by movieId from the database
app.get('/:movieId', (req, res) => {
	const movieId = req.params.movieId;
	db.select('*')
		.from('movies')
		.where('movie_id', '=', movieId)
		.then((data) => {
			console.log(data);
			res.json(data);
		})
		.catch((err) => {
			console.log(err);
		});
});

// POST: Create movies and add them to the database
app.post('/add-movie', (req, res) => {
	const { movieName, imgUrl, releaseYear, summary, director, genre, rating, movieRuntime, metaScore } = req.body;
	db('movies')
		.insert({
			movie_name: movieName,
			img_url: imgUrl,
			release_year: releaseYear,
			summary: summary,
			director: director,
			genre: genre,
			rating: rating,
			movie_runtime: movieRuntime,
			meta_score: metaScore,
		})
		.then(() => {
			console.log('Movie Added');
			return res.json({ msg: 'Movie Added' });
		})
		.catch((err) => {
			console.log(err);
		});
});

// DELETE: Delete movie by movieId from the database
app.delete('/delete-movie', (req, res) => {
	const movieId = req.body;
	const movieIdToDelete = Number(movieId.movieId);
	console.log(movieIdToDelete);
	db('movies')
		.where('movie_id', '=', movieIdToDelete)
		.del()
		.then(() => {
			console.log('Movie Deleted');
			return res.json({ msg: 'Movie Deleted' });
		})
		.catch((err) => {
			console.log(err);
		});
});

// PUT: Update movie by movieId from the database
app.put('/update-movie', (req, res) => {
	db('movies')
		.where('movie_id', '=', 1)
		.update({ movie_name: 'Goldeneye' })
		.then(() => {
			console.log('Movie Updated');
			return res.json({ msg: 'Movie Updated' });
		})
		.catch((err) => {
			console.log(err);
		});
});

// HarperDB Database routes

// GET: Fetch all movies from the database
app.get('/online/harperdb', (req, res) => {
	const data = { operation: 'sql', sql: 'SELECT * FROM dev.movies' };

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

// GET: Fetch movie by movieId from the database
app.get('/online/harperdb/:movieId', (req, res) => {
	const movieId = req.params.movieId;
	console.log(movieId);

	const data = { operation: 'sql', sql: `SELECT * FROM dev.movies WHERE id = ${movieId}` };

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

// POST: Create movies and add them to the database
app.post('/online/harperdb/add-movie', (req, res) => {
	const { movieName, imgUrl, releaseYear, summary, director, genre, rating, movieRuntime, metaScore } = req.body;
	console.log(req.body);

	const data = {
		operation: 'insert',
		schema: 'dev',
		table: 'movies',
		records: [
			{
				movie_name: movieName,
				img_url: imgUrl,
				release_year: releaseYear,
				summary: summary,
				director: director,
				genre: genre,
				rating: rating,
				movie_runtime: movieRuntime,
				meta_score: metaScore,
			},
		],
	};

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

// DELETE: Delete movie by movieId from the database
app.delete('/online/harperdb/delete-movie', (req, res) => {
	const movieId = req.body.movieId;
	console.log(movieId);

	const data = { operation: 'sql', sql: `DELETE FROM dev.movies WHERE id = ${movieId}` };

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
			res.send({ msg: 'Movie Deleted' });
			console.log('Movie Deleted');
		})
		.catch((error) => {
			console.log(error);
		});
});

// PUT: Update movie by movieId from the database
app.put('/online/harperdb/update-movie', (req, res) => {
	const movieId = req.body.movieId;
	console.log(movieId);

	const data = { operation: 'sql', sql: `UPDATE dev.movies SET movie_name = 'Goldeneye' WHERE id = ${movieId}` };

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
			res.send({ msg: 'Movie Updated' });
			console.log('Movie Updated');
		})
		.catch((error) => {
			console.log(error);
		});
});

const port = process.env.PORT || 5000;

app.listen(port, () => console.log(`Server running on port ${port}, http://localhost:${port}`));
```

Use your API tool or check out the routes in the browser to see the data returned as json from the HarperDB Database instance. For the update route just use your API tool with a key value pair like below.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1601901677/update-harperdb_mvedoy.png](https://res.cloudinary.com/d74fh3kw/image/upload/v1601901677/update-harperdb_mvedoy.png "Update HarperDB")

HarperDB stores ID's as strings so please be aware that you won't be able to fetch, update and delete a movie by movieId if its ID is a number unless you make some adjustments to your code. We have been storing our ID's as numbers however it's easy to switch between the two just make the `movieId` a string instead of a number.

You will need to restart your node server to see the changes.

## Building the front end

It's time to create a front end that will get data back from the API. `cd` into the root folder for the meta-movies-app and then run the command below to set up a project in React.

```bash
npx create-react-app frontend
cd frontend
```

Now start the react app server using either `npm start` or `yarn start`

Navigate inside of your react project and then delete all of the css inside of the `index.css` file. Next replace the code inside of the `App.css` and `App.js` files with the code below.

__App.css__

```css
@import url('https://fonts.googleapis.com/css2?family=Arsenal:wght@400;700&display=swap');
* {
	padding: 0;
	margin: 0;
	box-sizing: border-box;
}

html {
	font-size: 62.5%;
}

body {
	font-size: 1.6rem;
	font-family: 'Arsenal', sans-serif;
	/* letter-spacing: 0.2rem; */
	background: rgb(242, 242, 242);
	color: #0e0e0e;
}

header {
	background: #0e0e0e;
	padding: 1rem;
}

header h1 {
	margin: 0 auto;
	text-align: center;
	text-transform: uppercase;
	color: #ffffff;
}

section {
	display: flex;
	flex-flow: row wrap;
	justify-content: space-evenly;
	margin: 4rem;
}

.form-container {
	margin: 2rem auto;
	width: 50rem;
	max-width: 100%;
	padding: 0 2rem 0 2rem;
}

form {
	display: flex;
	flex-flow: column;
}

form input {
	height: 3rem;
	padding: 1.5rem;
}

form textarea {
	padding: 1.5rem;
}

form button {
	padding: 1rem;
	border: none;
	background: #fcee0b;
	font-weight: bold;
	cursor: pointer;
	transition: background 0.3s;
	text-transform: uppercase;
}

form button:hover {
	background: rgb(243, 212, 35);
}

form div {
	display: flex;
	flex-flow: column;
	margin-bottom: 1.3rem;
}

.movie-container {
	background: #fcee0b;
	padding: 4rem;
	margin-top: 2rem;
	border-radius: 2rem 7rem;
	width: 50rem;
	max-width: 100%;
}

.movie-container h1 {
	font-size: 3rem;
}

.movie-container p {
	margin: 1rem 0 1rem 0;
	font-size: 2rem;
}

.movie-container img {
	width: 10rem;
	height: 15rem;
}

.high {
	background: #66cc32;
	width: 4rem;
	color: #ffffff;
	text-align: center;
	font-weight: 700;
	display: inline-block;
	padding: 0.5rem;
	border-radius: 1rem;
}

.medium {
	background: #ffcc32;
	width: 4rem;
	color: #ffffff;
	text-align: center;
	font-weight: 700;
	display: inline-block;
	padding: 0.5rem;
	border-radius: 1rem;
}

.low {
	background: #ff0100;
	width: 4rem;
	color: #ffffff;
	text-align: center;
	font-weight: 700;
	display: inline-block;
	padding: 0.5rem;
	border-radius: 1rem;
}

@media screen and (max-width: 1094px) {
	section {
		justify-content: center;
		/* margin: 0 auto; */
	}
}

```

__App.js__

```jsx
import React, { Fragment, useState, useEffect } from 'react';
import './App.css';

const App = () => {
	useEffect(() => {
		const getAPI = () => {
			// Change this endpoint to whatever local or online address you have
			// Local PostgreSQL Database
			const API = 'http://127.0.0.1:5000/';

			fetch(API)
				.then((response) => {
					console.log(response);
					return response.json();
				})
				.then((data) => {
					console.log(data);
					setLoading(false);
					setApiData(data);
				});
		};
		getAPI();
	}, []);
	const [apiData, setApiData] = useState([]);
	const [loading, setLoading] = useState(true);
	return (
		<Fragment>
			<header>
				<h1>Meta Movie Reviews</h1>
			</header>
			<div className="form-container">
				<h2>Add Movie</h2>
				<form method="POST" action="http://127.0.0.1:5000/add-movie">
					<div>
						<label>Movie Name</label>
						<input type="text" name="movieName" required />
					</div>
					<div>
						<label>Box Image</label>
						<input type="text" name="imgUrl" required />
					</div>
					<div>
						<label>Realease Year</label>
						<input type="text" name="releaseYear" required />
					</div>
					<div>
						<label>Summary</label>
						<textarea rows="5" cols="50" name="summary"></textarea>
					</div>
					<div>
						<label>Director</label>
						<input type="text" name="director" required />
					</div>
					<div>
						<label>Genre</label>
						<input type="text" name="genre" required />
					</div>
					<div>
						<label>Rating</label>
						<input type="text" name="rating" required />
					</div>
					<div>
						<label>Runtime</label>
						<input type="text" name="movieRuntime" required />
					</div>
					<div>
						<label>Meta Score</label>
						<input type="text" name="metaScore" required />
					</div>
					<div>
						<button type="submit">Add Movie</button>
					</div>
				</form>
			</div>
			<main>
				{loading === true ? (
					<div>
						<h1>Loading...</h1>
					</div>
				) : (
					<section>
						{apiData.map((movie) => {
							let metaColor = 'low';

							if (movie.meta_score >= 70) {
								metaColor = 'high';
							} else if (movie.meta_score <= 69 && movie.meta_score >= 49) {
								metaColor = 'medium';
							} else {
								metaColor = 'low';
							}

							return (
								<div className="movie-container" key={String(movie.movie_id)}>
									<h1>{movie.movie_name}</h1>
									<p>
										<strong>Director:</strong> {movie.director}
									</p>
									<p>
										<strong>Genre:</strong> {movie.genre}
									</p>
									<img src={movie.img_url} alt={movie.movie_name} />

									<p>
										<strong>Meta Score:</strong> <span className={metaColor}>{movie.meta_score}</span>
									</p>
									<p>
										<strong>Runtime:</strong> {movie.movie_runtime}
									</p>
									<p>
										<strong>Rating:</strong> {movie.rating}
									</p>
									<p>
										<strong>Release Year:</strong> {movie.release_year}
									</p>
									<p>{movie.summary}</p>
								</div>
							);
						})}
					</section>
				)}
			</main>
		</Fragment>
	);
};

export default App;
```

Restart your Node server if you need to and make sure that it is also running. You should see the app working inside of your browser. It also has a form that allows you to add new database entries which automatically get displayed on the page. Meta Scores are even colour coded depending on their number which is done using an if statement which you can see in the code. 

The app is connected to your local PostgreSQL database however it is easy enough to change the endpoint for the API to HarperDB. All of the other routes are in the back end so you can play around with them and connect them to the front end which i'm sure you are already capable of doing.

When you add a new movie it does not redirect back to the react homepage. If you want to add this functionality then update your post route function in the backend `index.js` file in the PostgreSQL section with the code below. Restart your back end server to see the changes.

```javascript
// POST: Create movies and add them to the database
app.post('/add-movie', (req, res) => {
	const { movieName, imgUrl, releaseYear, summary, director, genre, rating, movieRuntime, metaScore } = req.body;
	db('movies')
		.insert({
			movie_name: movieName,
			img_url: imgUrl,
			release_year: releaseYear,
			summary: summary,
			director: director,
			genre: genre,
			rating: rating,
			movie_runtime: movieRuntime,
			meta_score: metaScore,
		})
		.then(() => {
			console.log('Movie Added');
			// return res.json({ msg: 'Movie Added' });
			return res.redirect('http://localhost:3000');
		})
		.catch((err) => {
			console.log(err);
		});
});
```
