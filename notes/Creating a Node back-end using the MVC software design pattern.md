In this tutorial you will learn how to create a Node back-end using the Model–view–controller (MVC) software design pattern. This design pattern gives you the ability to make user interfaces that are separated into three different elements. The business logic is separated so that the data, user interface and user input are not mixed together. This allows for a much cleaner architecture as the different layers are decoupled allowing for changes to be done more rapidly and easily.

One important caveat to mention here however is that these days the **View** part of this software design pattern is no longer as relevant as it used to be years ago. This is because we now have front-end frameworks like React, Vue, Angular and Svelte which are used for building the front-end of applications. Nonetheless these concepts are still useful to know because **Models** and **Controllers** are still used today when back-end developers build REST and GraphQL API's that return some sort of data. Data like JavaScript Object Notation (JSON) which is used in an API and is retrieved using the fetch or Axios API.

## Prerequisites

Make sure that you have the tools and packages below installed

- [Node and npm](https://nodejs.org/en/)
- [Express](https://expressjs.com/)
- [Nodemon](https://nodemon.io/)
- [EJS](https://ejs.co/)

## The Design Pattern

### Model

The Model is the main component of this design pattern. It is responsible for handling all of the data inside of the structure. This is where all of the data, business logic and principles will be defined.

### View

Essentially the view is the user interface. This is the part of the application that a user is going to visually see. So basically the front-end which was designed. Before front-end frameworks like React, Vue, Angular and Svelte existed, back-end developers used templating languages like EJS, PUG and Handlebars.

### Controller

The controller can be considered as the brains of the application. It takes in any inputs that the user requests and then turns them into commands which the model and view can interpret.

## Setting up the project

Create a folder named **my-app **on your desktop or in a directory and then **cd** into it. Also open the folder in your code editor. Make sure that you are in the **my-app** folder and then run the commands below in your terminal app.

```bash
mkdir backend
cd backend
npm init -y
npm i express nodemon ejs
mkdir controllers models public routes src
mkdir src/pages
touch index.js
```

This will create the basic setup for our project. Now let's create a simple express server. Copy and paste the code below into the `index.js` file.

```JavaScript
const express = require('express');

const app = express();

app.get('/', (req, res) => res.send('Home Route'));

const port = process.env.PORT || 5000;

app.listen(port, () => console.log(`Server running on port ${port}, http://localhost:${port}`));
```

Now add these run scripts to the `package.json` file.

```json
	"scripts": {
		"start": "node index.js",
		"dev": "nodemon index.js"
	},
```

In your terminal app run either one of the run codes below to see the app running in your web browser. The first run code uses Node which means that the server needs to be restarted if you want to see changes. The second run code uses Nodemon which does hot reloading which means that you only need to reload the web browser to see new changes.

```bash
npm run start
```

```bash
npm run dev
```

## Creating the MVC Controllers

It's time to create some controllers. Create two files called `admin.js` and put one inside of the **controllers** folder and the other one inside of the **routes** folder. Next create an `AnimeData.json` file and put it inside of the **models** folder. Now create an `index.ejs` file and put it inside of the **src/pages** folder. Add the code below to the `index.ejs` file.

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta http-equiv="X-UA-Compatible" content="IE=edge" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Home Route</title>
	</head>
	<body>
		<h1>Home Route</h1>
	</body>
</html>
```

Put the code below into the `AnimeData.json` file.

```json
[
	{
		"id": "1",
		"type": "Anime",
		"name": "Boku no Hero Academia"
	},
	{
		"id": "2",
		"type": "Anime",
		"name": "Jujutsu Kaisen"
	},
	{
		"id": "3",
		"type": "Anime",
		"name": "Shingeki no Kyojin"
	}
]
```

Add the code below to the `admin.js` file inside of the **controllers** folder.

```javascript
const AnimeData = require('../models/AnimeData.json');

exports.getIndex = (req, res) => {
	res.render('index');
};

exports.getAnime = (req, res) => {
	res.json(AnimeData);
};
```

Next add the code below to the `admin.js` file inside of the **routes** folder.

```javascript
const express = require('express');
const adminController = require('../controllers/admin');

const router = express.Router();

router.get('/', adminController.getIndex);

router.get('/anime', adminController.getAnime);

module.exports = router;
```

Finally update the `index.js` file in the root folder with the code below.

```JavaScript
const express = require('express');
const path = require('path');
const adminRoute = require('./routes/admin');

const app = express();

// EJS template engine setup
app.set('view engine', 'ejs');
app.set('views', './src/pages');

// Setting up the directory on the server for CSS, JavaScript and media files
app.use('/static', express.static(path.join(__dirname + '/public')));

// Configuring the server to work with form submissions and json files
app.use(express.urlencoded({ extended: false }));
app.use(express.json());

// Connecting all of the routes
app.use('/', adminRoute);

const port = process.env.PORT || 5000;

app.listen(port, () => console.log(`Server running on port ${port}, http://localhost:${port}`));
```

You will need to reload the page or restart the server. Now if you go to the home route [http://localhost:5000](http://localhost:5000) it should load the `index.ejs` file. If you go to [http://localhost:5000/anime](http://localhost:5000/anime) you should see the data in the json file returned in the browser.

## Connecting the CSS and JavaScript files to the front-end

The last step is to connect a CSS stylesheet and JavaScript file to the `index.ejs` file. Create two folders inside of the **public** folder. One called **css** and the other one called **js**. Now create a `styles.css` file and put it inside of the **css** folder with the code below.

```css
body {
	background: #bada55;
}
```

Next create a `scripts.js` file and put it inside of the **js** folder with the code below.

```JavaScript
console.log('Hello World');
```

Lastly update the `index.ejs` file with the code below which now has the links for the CSS and JavaScript files.

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta http-equiv="X-UA-Compatible" content="IE=edge" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Home Route</title>
		<link rel="stylesheet" href="http://localhost:5000/static/css/styles.css" />
	</head>
	<body>
		<h1>Home Route</h1>

		<script src="http://localhost:5000/static/js/scripts.js"></script>
	</body>
</html>
```

Reload your browser or restart the server. If you go to the home route you should see a green background and if you go to the browser console you should see the code **Hello World**. And those are the basics for creating a Node back-end server using the MVC software design pattern. If you were planning on connecting the back-end to a framework like React, you would not need the **src** folder. Instead you would use the **models** folder for returning the data as json. The **models** folder is also the place where you would create the programming logic used for connecting the back-end to a database like mongodb, postgresql and HarperDB.

## Final Thoughts

I really hope that you enjoyed reading this article and learned something from it. As a content creator and technical writer I am passionate about sharing my knowledge and helping other people reach their goals. Let's connect across social media you can find all of my social media profiles and blogs on [linktree](https://linktr.ee/andrewbaisden).

Peace ✌️
