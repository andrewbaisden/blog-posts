NodeJS 18 introduced some new cool features and one of the most useful ones is the built in Fetch API. What this means is that we longer need to use 3rd party npm packages like `node-fetch` because the functionality is now native and baked into Node. That's one less dependency that we need to install so our `node_modules` folders should be a little lighter.

Before you can use the latest NodeJS features like the Fetch API you first need to check that you are running the latest version of Node on your computer. Run the command `node -v` in your console to see which version you have running. If its less than 18 then you need to upgrade before you can use these new features.

## Using the Fetch API

If you are already familiar with using the Fetch API in the browser when developing JavaScript applications, then this syntax should be easy to understand. We finally have a native solution for fetching data on the backend using JavaScript.

```javascript
const getAPI = async () => {
	const res = await fetch('https://pokeapi.co/api/v2/pokemon/');

	if (res.ok) {
		const data = await res.json();

		console.log(data);
	}
};

getAPI();
```

Let's create a practical example so you can see one potential use case. Navigate to a directory and then copy and paste the code below into your command line to scaffold a project.

```shell
mkdir node-backend-fetch
cd node-backend-fetch
npm init -y
npm i express nodemon
touch app.js
mkdir controllers routes
touch controllers/pokemon.js
touch routes/pokemon.js
```

Open the project in your code editor and then copy the code below into their corresponding files.

`controllers/pokemon.js`

```javascript
exports.getPokemon = async (req, res) => {
	const api = await fetch('https://pokeapi.co/api/v2/pokemon/');

	if (api.ok) {
		const data = await api.json();

		console.log(data);

		try {
			res.json(data);
		} catch (error) {
			console.log(error);
		}
	}
};

exports.getPokemonMoves = async (req, res) => {
	const api = await fetch('https://pokeapi.co/api/v2/move/');

	if (api.ok) {
		const data = await api.json();

		console.log(data);

		try {
			res.json(data);
		} catch (error) {
			console.log(error);
		}
	}
};
```

`routes/pokemon.js`

```javascript
const express = require('express');

const pokemonController = require('../controllers/pokemon');

const router = express.Router();

router.get('/pokemon', pokemonController.getPokemon);

router.get('/pokemon-moves', pokemonController.getPokemonMoves);

module.exports = router;
```

`app.js`

```javascript
const express = require('express');

const pokemonRoute = require('./routes/pokemon');

const app = express();

app.use('/', pokemonRoute);

const port = process.env.PORT || 3000;

app.listen(port, () => console.log(`Server running on ${port}, http://localhost:${port}`));
```

`package.json`

Add these run scripts.

```json
"scripts": {

"start": "node app.js",

"dev": "nodemon app.js"

},
```

Double check to make sure that you are using Node 18 and then run the command `npm run dev` to start the backend server.

If you go to this route [http://localhost:3000/pokemon](http://localhost:3000/pokemon) you should have a list of Pokemon returned in json. The data is also logged to the console.

And if you go to this route [http://localhost:3000/pokemon-moves](http://localhost:3000/pokemon-moves) you should have a list of Pokemon moves which is also returned as json. Like in the other example the data is logged to the console too.

## Final Thoughts

This was a brief introduction to using the NodeJS 18 Fetch API. To learn more check out the [official announcement](https://nodejs.org/en/blog/announcements/v18-release-announce/).
