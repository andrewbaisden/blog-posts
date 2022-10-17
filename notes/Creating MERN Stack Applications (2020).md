Before you begin make sure that you have [Node](https://nodejs.org/en/) and [Create React App](https://create-react-app.dev/) installed. And if you are planning on using a local mongodb database then make sure that you have that setup too.

## Reference Material

[Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
[Connect to MongoDB](https://docs.mongodb.com/guides/server/drivers/)
[MongoDB CRUD Operations](https://docs.mongodb.com/manual/crud/)
[MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
[Mongoose](https://mongoosejs.com/)
[Express.js](https://expressjs.com/)
[EJS](https://ejs.co/)
[React](https://reactjs.org/)
[React Router](https://reactrouter.com/web/guides/quick-start)
[Redux](https://redux.js.org/)
[Netlify](https://www.netlify.com/)
[Vercel](https://vercel.com/)

## Tools Required

You can use whatever code editor and terminal application you want. But for interacting with HTTP APIs on the backend. The Postman App is my preference.

Code Editor: Visual Studio Code
Terminal: Hyper
API Testing App: Postman

## Checklist

These are the steps we will be following

1. Initialise the project using a GIT Workflow (optional setup a kanban board for the project)
2. Set up a MongoDB Database (local or online)
3. Create the backend Node/Express server that connects to the database with CRUD requests
4. Create the frontend using either EJS or React/Redux

- Ejs templating (HTML and CSS Grid/Flexbox)
- React/Redux (Styled components using CSS Grid/Flexbox)

5. Online Deployment to production server (Netlify, Vercel, Heroku etc…)

## Project Setup

I will be creating an app to track the Anime that I watch. However feel free to use whatever theme you want.

### GIT Workflow

Go to GitHub and create a new repo then create a folder on your local machine and `cd` into it using your terminal app. Then initialise the repo like below.

Throughout this project you should be committing your work to GitHub and following a GIT Workflow.

```bash
echo "# anime-tracker" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/yourname/anime-tracker.git
git push -u origin master
```

### Set up a MongoDB Database

For production you need to use an online database as a local database is for development purposes only. Either way you can use whichever one you want in this guide.

**Online**
https://www.mongodb.com/cloud/atlas
https://mlab.com/

You should have a connection string like below replacing the username and password with your credentials

```bash
mongodb+srv://<username>:<password>@cluster0-tyqyw.mongodb.net/<dbname>?retryWrites=true&w=majority
```

**Local**

Make sure that you have mongoDB and mongoDB compass installed locally

Use the commands below in your terminal to create a local database of your choosing

```bash
mongo
show dbs;
use animes;
db.createCollection("series");
```

To connect to the database you will use the connection string below

```bash
mongodb://127.0.0.1:27017/animes
```

### Setup the folder structure and install dependencies

Open the project folder in your code editor, create a backend folder and then install the dependencies

```bash
touch .gitignore
mkdir backend
cd backend
npm init -y
npm i express nodemon ejs cors concurrently mongoose dotenv
```

Setup the folder structure inside the backend folder

```bash
mkdir controllers
mkdir models
mkdir public
mkdir routes
mkdir src
mkdir src/pages
touch app.js
touch .gitignore
```

Add `node_modules` `.env` and `.DS_Store` to the `.gitignore` file in the root and backend folders

### Create the Node/Express server that connects to the database

Create a `.env` file in the root directory of your project. Add environment-specific variables on new lines in the form of `NAME=VALUE`. For example:

```bash
DB_HOST="mongodb://127.0.0.1:27017/animes"
DB_USER="databaseuser"
DB_PASS="databasepassword"
```

Open the ` app.js` file and add the code below

Local MongoDB databases do not require a username and password only the host

```javascript
const express = require('express');
const mongoose = require('mongoose');
const path = require('path');
const cors = require('cors');
require('dotenv').config();

const app = express();

app.use(cors());

app.set('view engine', 'ejs');
app.set('views', './src/pages');

app.use(express.urlencoded({ extended: false }));

app.use('/static', express.static(path.join(`${__dirname}/public`)));

app.get('/', (req, res) => res.send('Home Route'));

const port = process.env.PORT || 8080;

mongoose
	.connect(process.env.DB_HOST, {
		useCreateIndex: true,
		useUnifiedTopology: true,
		useNewUrlParser: true,
		useFindAndModify: false,
	})
	.then(() => {
		app.listen(port, () => console.log(`Server and Database running on ${port}, http://localhost:${port}`));
	})
	.catch((err) => {
		console.log(err);
	});
```

Open the `package.json` file and add the following run scripts for start, dev and servers

```json
{
	"name": "backend",
	"version": "1.0.0",
	"description": "",
	"main": "index.js",
	"scripts": {
		"start": "node app.js",
		"dev": "nodemon app.js",
		"servers": "concurrently \"npm run dev\" \"cd ../frontend && npm run start\""
	},
	"keywords": [],
	"author": "Andrew Baisden",
	"license": "MIT",
	"dependencies": {
		"concurrently": "^5.2.0",
		"cors": "^2.8.5",
		"dotenv": "^8.2.0",
		"ejs": "^3.1.3",
		"express": "^4.17.1",
		"mongoose": "^5.9.24",
		"nodemon": "^2.0.4"
	}
}
```

Use the command `npm run dev` in your terminal window and the app should be up and running as well as connected to your mongodb database.

**_Tree Structure (Hidden files are not shown)_**

├── README.md
└── backend
├── app.js
├── controllers
├── models
├── node_modules
├── package-lock.json
├── package.json
├── public
├── routes
└── src
└── pages

8 directories, 4 files

### Create a controller and routes files

First create an `index.ejs` file in `src/pages` and add the html below

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Home</title>
	</head>
	<body>
		<h1>Home Page</h1>
	</body>
</html>
```

Then create an `edit-anime.ejs` file in `src/pages` and add the html below

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Add Anime</title>
	</head>
	<body>
		<h1>Add Anime</h1>

		<form method="POST" action="/add-anime">
			<div>
				<label>Name</label>
				<input type="text" name="name" required />
			</div>
			<div>
				<label>Image</label>
				<input type="text" name="image" required />
			</div>
			<div>
				<label>Description</label>
				<input type="text" name="description" required />
			</div>
			<div>
				<button type="submit">Add Anime</button>
			</div>
		</form>
	</body>
</html>
```

Finally create an `anime.ejs` file in `src/pages` and add the html below

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Anime</title>
	</head>
	<body>
		<h1>Anime</h1>
	</body>
</html>
```

Next create an `admin.js` file and put it in the `controllers` folder

```javascript
exports.getIndex = (req, res) => {
	res.status(200).render('index');
};
```

Then create an `admin.js` file and put it in the `routes` folder

```javascript
const express = require('express');
const adminController = require('../controllers/admin');

const router = express.Router();

router.get('/', adminController.getIndex);

module.exports = router;
```

Import the admin route file into your main `app.js` file in the root folder and replace the home route with the new admin route

```javascript
const adminRoute = require('./routes/admin');

// Replace the code for the old route with the new route code

// Old Code
app.get('/', (req, res) => res.send('Home Route'));

// New Code
app.use('/', adminRoute);
```

### Create a mongoose Schema

Create an `Anime.js` file in the models folder and then copy and paste the code below into that file

```javascript
const mongoose = require('mongoose');

const AnimeSchema = mongoose.Schema({
	name: {
		type: String,
		required: true,
	},
	image: {
		type: String,
		required: true,
	},
	description: {
		type: String,
		required: true,
	},
});

module.exports = mongoose.model('series', AnimeSchema);
```

### Creating the CRUD requests

Next we will create the CRUD requests for interacting with the database. This is also the perfect opportunity to use the Postman App for dong HTTP requests for all of the routes. This will allow you to POST data and see GET routes without having to use your browser. It is beyond the scope of this guide however its very easy to use if you look at the documentation.

#### Adding data to the database (Create)

We are creating routes for for the page with the add form and a post route to add that form data to the database

Update the `admin.js` file in the `controllers` folder with the code below

```javascript
const Anime = require('../models/Anime');

exports.getIndex = (req, res) => {
	res.status(200).render('index');
};

exports.getAddAnime = (req, res) => {
	res.status(200).render('edit-anime');
};

exports.postAnime = (req, res) => {
	const { name, image, description } = req.body;

	const anime = new Anime({ name: name, image: image, description: description });
	anime.save();
	console.log('Anime Added to the database');
	res.status(201).redirect('/');
};
```

Update the `admin.js` file in the `routes` folder with the code below

```javascript
const express = require('express');
const adminController = require('../controllers/admin');

const router = express.Router();

router.get('/', adminController.getIndex);

router.get('/add-anime', adminController.getAddAnime);

router.post('/add-anime', adminController.postAnime);

module.exports = router;
```

Now if you go to [http://localhost:8080/add-anime](http://localhost:8080/add-anime) and submit some form data it should be added to your database. If you are using a local mongodb database use the MongoDB Compass app to check your database you will need to refresh it to see the new entries. If you have an online database just go to your cluster to see the collections.

Alternatively use the Postman App to send a post request to the route http://localhost:8080/add-anime like in the example below

![Postman](https://res.cloudinary.com/d74fh3kw/image/upload/v1594913050/create_route_e8gwq3.png 'Postman Create Route')

#### Reading data from the database (Read)

Now we are retrieving data from the database and rendering it inside of our pages by using async function calls. We will be using the `.ejs` templating language for creating the pages so refer to the documentation if you want to understand the code. It is basically like vanilla javascript but with `.ejs` templating syntax tags so it should be easy to understand.

Update the `admin.js` file in the `controllers` folder with the code below

```javascript
const Anime = require('../models/Anime');

exports.getIndex = async (req, res) => {
	const anime = await Anime.find((data) => data);

	try {
		console.log(anime);
		res.status(200).render('index', { anime: anime });
	} catch (error) {
		console.log(error);
	}
};

exports.getAnime = async (req, res) => {
	const animeId = req.params.animeId;

	const anime = await Anime.findById(animeId, (anime) => anime);

	try {
		console.log(anime);
		res.status(200).render('anime', { anime: anime });
	} catch (error) {
		console.log(error);
	}
};

exports.getAddAnime = (req, res) => {
	res.status(200).render('edit-anime');
};

exports.postAnime = (req, res) => {
	const { name, image, description } = req.body;

	const anime = new Anime({ name: name, image: image, description: description });
	anime.save();
	console.log('Anime Added to the database');
	res.status(201).redirect('/');
};
```

Update the `admin.js` file in the `routes` folder with the code below

```javascript
const express = require('express');
const adminController = require('../controllers/admin');

const router = express.Router();

router.get('/', adminController.getIndex);

router.get('/add-anime', adminController.getAddAnime);

router.post('/add-anime', adminController.postAnime);

router.get('/:animeId', adminController.getAnime);

module.exports = router;
```

Update the `index.ejs` file in the `src/pages` folder with the code below

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Home</title>
	</head>
	<body>
		<h1>Home Page</h1>

		<main>
			<% anime.forEach(data => { %>
				<ul>
					<li><h1><a href="/<%= data.id %>"><%= data.name %></a></h1></li>
					<li><img src="<%= data.image %>" alt="<%= data.name %>" /></h1></li>
					<li><p><%= data.description %></p></li>
				</ul>
			<% }) %>
		</main>

	</body>
</html>
```

Update the `anime.ejs` file in the `src/pages` folder with the code below

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Anime</title>
	</head>
	<body>
		<h1>Anime</h1>

		<main>
			<h1><%= anime.name %></h1>
			<img src="<%= anime.image %>" alt="<%= anime.name %>" />
			<p><%= anime.description %></p>
		</main>
	</body>
</html>
```

Now you should see your database data rendered on the homepage and if you click on one of the links it should take you to its corresponding page based on its ID. This data is also logged to the console.

#### Deleting data from the database (Delete)

Now we are creating a delete route to delete items from the database

Update the `admin.js` file in the `controllers` folder with the code below

```javascript
const Anime = require('../models/Anime');

exports.getIndex = async (req, res) => {
	const anime = await Anime.find((data) => data);

	try {
		console.log(anime);
		res.status(200).render('index', { anime: anime });
	} catch (error) {
		console.log(error);
	}
};

exports.getAnime = async (req, res) => {
	const animeId = req.params.animeId;

	const anime = await Anime.findById(animeId, (anime) => anime);

	try {
		console.log(anime);
		res.status(200).render('anime', { anime: anime });
	} catch (error) {
		console.log(error);
	}
};

exports.getAddAnime = (req, res) => {
	res.status(200).render('edit-anime');
};

exports.postAnime = (req, res) => {
	const { name, image, description } = req.body;

	const anime = new Anime({ name: name, image: image, description: description });
	anime.save();
	console.log('Anime Added to the database');
	res.status(201).redirect('/');
};

exports.postDelete = async (req, res) => {
	const animeId = req.body.animeId;

	const anime = await Anime.findByIdAndRemove(animeId, (data) => data);

	try {
		console.log(anime);
		console.log('Item Deleted');
		res.redirect('/');
	} catch (error) {
		console.log(error);
	}
};
```

Update the `admin.js` file in the `routes` folder with the code below

```javascript
const express = require('express');
const adminController = require('../controllers/admin');

const router = express.Router();

router.get('/', adminController.getIndex);

router.get('/add-anime', adminController.getAddAnime);

router.post('/add-anime', adminController.postAnime);

router.get('/:animeId', adminController.getAnime);

router.post('/delete', adminController.postDelete);

module.exports = router;
```

Update the `anime.ejs` file in the `src/pages` folder with the code below

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Anime</title>
	</head>
	<body>
		<h1>Anime</h1>

		<main>
			<h1><%= anime.name %></h1>
			<img src="<%= anime.image %>" alt="<%= anime.name %>" />
			<p><%= anime.description %></p>

			<div>
				<form method="POST" action="/delete">
					<div>
						<input type="hidden" value="<%= anime.id %>" name="animeId" />
						<button>Delete</button>
					</div>
				</form>
			</div>
		</main>
	</body>
</html>
```

Now if you go to an item page and then click on the delete button you should be able to delete it

#### Updating data from the database (Update)

Now we are creating routes for updating each item in the database. Update the files with the code below.

Update the `admin.js` file in the `controllers` folder with the code below

```javascript
const Anime = require('../models/Anime');

exports.getIndex = async (req, res) => {
	const anime = await Anime.find((data) => data);

	try {
		console.log(anime);
		res.status(200).render('index', { anime: anime });
	} catch (error) {
		console.log(error);
	}
};

exports.getAnime = async (req, res) => {
	const animeId = req.params.animeId;

	const anime = await Anime.findById(animeId, (anime) => anime);

	try {
		console.log(anime);
		res.status(200).render('anime', { anime: anime });
	} catch (error) {
		console.log(error);
	}
};

exports.getAddAnime = (req, res) => {
	res.status(200).render('edit-anime', { editing: false });
};

exports.getEditAnime = async (req, res) => {
	const animeId = req.params.animeId;

	const editMode = req.query.edit;

	if (!editMode) {
		return res.redirect('/');
	}

	const anime = await Anime.findById(animeId);

	try {
		if (!animeId) {
			return res.redirect('/');
		}
		console.log(anime);
		res.status(200).render('edit-anime', { anime: anime, editing: editMode });
	} catch (error) {
		console.log(error);
	}
};

exports.postAnime = (req, res) => {
	const { name, image, description } = req.body;

	const anime = new Anime({ name: name, image: image, description: description });
	anime.save();
	console.log('Anime Added to the database');
	res.status(201).redirect('/');
};

exports.postEditAnime = (req, res) => {
	const animeId = req.body.animeId;
	const { name, image, description } = req.body;

	Anime.findById(animeId)
		.then((anime) => {
			anime.name = name;
			anime.image = image;
			anime.description = description;

			return anime.save();
		})
		.then(() => {
			console.log('Item Updated');
			res.status(201).redirect('/');
		})
		.catch((err) => {
			console.log(err);
		});
};

exports.postDelete = async (req, res) => {
	const animeId = req.body.animeId;

	const anime = await Anime.findByIdAndRemove(animeId, (data) => data);

	try {
		console.log(anime);
		console.log('Item Deleted');
		res.redirect('/');
	} catch (error) {
		console.log(error);
	}
};
```

Update the `admin.js` file in the `routes` folder with the code below

```javascript
const express = require('express');
const adminController = require('../controllers/admin');

const router = express.Router();

router.get('/', adminController.getIndex);

router.get('/add-anime', adminController.getAddAnime);

router.get('/edit-anime/:animeId', adminController.getEditAnime);

router.post('/add-anime', adminController.postAnime);

router.post('/edit-anime', adminController.postEditAnime);

router.get('/:animeId', adminController.getAnime);

router.post('/delete', adminController.postDelete);

module.exports = router;
```

Update the `anime.ejs` file in the `src/pages` folder with the code below

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Anime</title>
	</head>
	<body>
		<h1>Anime</h1>

		<main>
			<h1><%= anime.name %></h1>
			<img src="<%= anime.image %>" alt="<%= anime.name %>" />
			<p><%= anime.description %></p>

			<div>
				<form method="POST" action="/delete">
					<div>
						<input type="hidden" value="<%= anime.id %>" name="animeId" />
						<button>Delete</button>
					</div>
				</form>
			</div>
			<div>
				<a href="/edit-anime/<%= anime.id %>?edit=true">Edit</a>
			</div>
		</main>
	</body>
</html>
```

Update the `edit-anime.ejs` file in the `src/pages` folder with the code below

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title><% if(editing){ %>Edit Anime<% } else { %>Add Anime<% } %></title>
	</head>
	<body>
		<h1><% if(editing){ %>Edit Anime<% } else { %>Add Anime<% } %></h1>

		<form method="POST" action="/<% if(editing){ %>edit-anime<% } else { %>add-anime<% } %>">
			<div>
				<label>Name</label>
				<input type="text" name="name" value="<% if(editing){ %><%= anime.name %><% } %>" required />
			</div>
			<div>
				<label>Image</label>
				<input type="text" name="image" value="<% if(editing){ %><%= anime.image %><% } %>" required />
			</div>
			<div>
				<label>Description</label>
				<input type="text" name="description" value="<% if(editing){ %><%= anime.description %><% } %>" required />
			</div>
			<% if(editing){ %>
			<div>
				<input type="hidden" name="animeId" value="<%= anime.id %>" />
			</div>
			<% } %>
			<div>
				<button type="submit"><% if(editing){ %>Edit Anime<% } else { %>Add Anime<% } %></button>
			</div>
		</form>
	</body>
</html>
```

Now when you go to an item page you will see an edit button. When you click the button it will take you to the form which has now been updated with that items data from the database. When you update the item it will redirect you to the home page where you will see the new changes.

#### React Frontend

Congratulations you just created a full stack application that connects to a mongoDB database and has full CRUD requests! However its not a MERN app yet because it does not have a React front end. The next phase is easy all you have to do is return the backend data as `json` and use fetch or axios requests to get the data. And as for the form you just need to make sure that you send the POST requests to your backend server. We installed CORS right at the start so there will be no crosss origin errors when you try to connect your front end to the backend. And we also setup a run script to run the backend and frontend servers together which will make it better.

Create a frontend folder in your root folder and then setup a react app inside of it

```bash
mkdir frontend
cd frontend
npx create-react-app .
```

Return to the root folder for the backend and then run the command `npm run servers` to start both the backend and frontend servers together. You should see your React App running in the browser.

Now go to the backend folder and go into `controllers/admin.js` and update the code with the one below.

All we are doing is returning the data that gets sent to the index route as `.json` so that we can use fetch/axios to map over it in the frontend. We are also going to update the POST route for adding new anime so that it redirects to the React frontend app index page.

```javascript
const Anime = require('../models/Anime');

exports.getIndex = async (req, res) => {
	const anime = await Anime.find((data) => data);

	try {
		console.log(anime);
		// Data rendered as an object and passed down into index.ejs
		// res.status(200).render('index', { anime: anime });

		// Data returned as json so a fetch/axios requst can get it
		res.json(anime);
	} catch (error) {
		console.log(error);
	}
};

exports.getAnime = async (req, res) => {
	const animeId = req.params.animeId;

	const anime = await Anime.findById(animeId, (anime) => anime);

	try {
		console.log(anime);
		res.status(200).render('anime', { anime: anime });
	} catch (error) {
		console.log(error);
	}
};

exports.getAddAnime = (req, res) => {
	res.status(200).render('edit-anime', { editing: false });
};

exports.getEditAnime = async (req, res) => {
	const animeId = req.params.animeId;

	const editMode = req.query.edit;

	if (!editMode) {
		return res.redirect('/');
	}

	const anime = await Anime.findById(animeId);

	try {
		if (!animeId) {
			return res.redirect('/');
		}
		console.log(anime);
		res.status(200).render('edit-anime', { anime: anime, editing: editMode });
	} catch (error) {
		console.log(error);
	}
};

exports.postAnime = (req, res) => {
	const { name, image, description } = req.body;

	const anime = new Anime({ name: name, image: image, description: description });
	anime.save();
	console.log('Anime Added to the database');

	// Updated the home route to the React App index page
	res.status(201).redirect('http://localhost:3000/');
};

exports.postEditAnime = (req, res) => {
	const animeId = req.body.animeId;
	const { name, image, description } = req.body;

	Anime.findById(animeId)
		.then((anime) => {
			anime.name = name;
			anime.image = image;
			anime.description = description;

			return anime.save();
		})
		.then(() => {
			console.log('Item Updated');
			res.status(201).redirect('/');
		})
		.catch((err) => {
			console.log(err);
		});
};

exports.postDelete = async (req, res) => {
	const animeId = req.body.animeId;

	const anime = await Anime.findByIdAndRemove(animeId, (data) => data);

	try {
		console.log(anime);
		console.log('Item Deleted');
		res.redirect('/');
	} catch (error) {
		console.log(error);
	}
};
```

Now go to the frontend folder and go into `src/app.js` and replace the code with the one below

```javascript
import React, { Fragment, useEffect, useState } from 'react';

const App = () => {
	useEffect(() => {
		const getAPI = async () => {
			const response = await fetch('http://localhost:8080/');
			const data = await response.json();

			try {
				console.log(data);
				setLoading(false);
				setAnime(data);
			} catch (error) {
				console.log(error);
			}
		};
		getAPI();
	}, []);

	const [anime, setAnime] = useState([]);
	const [loading, setLoading] = useState(true);

	return (
		<Fragment>
			<h1>Anime Home</h1>

			<div>
				{loading ? (
					<div>Loading</div>
				) : (
					<div>
						{anime.map((data) => (
							<div key={data._id}>
								<ul>
									<li>
										<h1>
											<a href="/{data.id}">{data._id}</a>
										</h1>
									</li>
									<li>
										<img src={data.image} alt={data.name} />
									</li>
									<li>
										<p>{data.description}</p>
									</li>
								</ul>
							</div>
						))}
					</div>
				)}
			</div>
			<div>
				<h1>Add New Anime</h1>
				<form method="POST" action="http://localhost:8080/add-anime">
					<div>
						<label>Name</label>
						<input type="text" name="name" required />
					</div>
					<div>
						<label>Image</label>
						<input type="text" name="image" required />
					</div>
					<div>
						<label>Description</label>
						<input type="text" name="description" required />
					</div>

					<div>
						<button type="submit">Add Anime</button>
					</div>
				</form>
			</div>
		</Fragment>
	);
};

export default App;
```

You should now see your data rendered out in the frontend when you got to [http://localhost:3000/](http://localhost:3000/)

I also created a form at the bottom which will let you add new entries to the database. Obviously in a complete project you should be using components to build your app I just created a quick example to show you what it looks like.

Well done you just created a MERN app those are the basics! To complete the app you should add routing on the frontend using [React Router](https://reactrouter.com/web/guides/quick-start) so that you can create more dynamic pages. My preference is to use [Styled Components](https://styled-components.com/) but you can use whatever CSS library you want. You can even add Redux or another state library. Just make sure that you return the data from the GET routes in the backend using `.json` so that you can use fetch/axios in the frontend to manage the data.

Alternatively you can just work with the `.ejs` frontend and give that styling and navigation too using CSS its up to you. When your app is complete just deploy it to one of the many available platforms out there like [Netlify](https://www.netlify.com/) and [Vercel](https://vercel.com/)

You can see my final version on my GitHub at [Anime Tracker](https://github.com/andrewbaisden/anime-tracker) feel free to clone and download the repo. This build has a `.ejs` frontend and CSS. I also made a few minor adjustments to the codebase.

![Anime Tracker Home](https://res.cloudinary.com/d74fh3kw/image/upload/v1596194619/anime-home_glu2zg.jpg 'Anime Tracker Home')

![Anime Tracker Add Anime](https://res.cloudinary.com/d74fh3kw/image/upload/v1596194617/anime-add_axp12q.jpg 'Anime Tracker Add Anime')

![Anime Tracker Anime](https://res.cloudinary.com/d74fh3kw/image/upload/v1596194617/anime-anime_isznm3.jpg 'Anime Tracker Anime')

![Anime Tracker Edit Anime](https://res.cloudinary.com/d74fh3kw/image/upload/v1596194617/anime-edit_boosq2.jpg 'Anime Tracker Edit Anime')
