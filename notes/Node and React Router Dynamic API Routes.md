# Node and React Router Dynamic API Routes

We will be creating a book library website similar to Audible that has a backend Node API. This API will hold the book data which will be dynamically available allowing you to select all of the books and also the books by book ID. You will learn how to create routes on the backend and also on the frontend in React using React Router.

## Step 1: Setup the backend project

Create a folder for your project and then `cd` into it. Copy and paste this code into your terminal and then hit enter to setup your project

```bash
touch .gitignore
mkdir backend
cd backend
touch .gitignore
npm init -y
npm i express nodemon cors concurrently uuid
mkdir controllers data models public routes
touch app.js
touch controllers/admin.js
touch routes/admin.js
touch models/Books.js
touch data/books.json
```

`cd` to the root folder and then open the project in your code editor. Add the code below to both `.gitignore` files

```bash
.DS_STORE
node_modules
```

Copy and paste the code below into the corresponding files

`app.js`

```JavaScript
const express = require('express');
const cors = require('cors');
const adminRoute = require('./routes/admin');

const app = express();
app.use(cors());

app.use(express.urlencoded({ extended: false }));

app.use('/', adminRoute);

const port = process.env.PORT || 8080;

app.listen(port, () => console.log(`Server running on port ${port}, http://localhost:${port}`));
```

`controllers/admin.js`

```javascript
exports.getIndex = (req, res) => {
	res.send('Book Library Home Route');
};
```

`routes/admin.js`

```javascript
const express = require('express');
const router = express.Router();
const adminController = require('../controllers/admin');

router.get('/', adminController.getIndex);

module.exports = router;
```

Add these run scripts to your `package.json` file

```json
"scripts": {
		"start": "node app.js",
		"dev": "nodemon app.js",
		"servers": "concurrently \"npm run start\" \"cd ../frontend && npm run start\""
	},
```

Now run the command `npm run dev` from your backend folder and the server should be up and running.

## Step 2: Create the REST API

In this guide we will be using a local file server however it is fairly simple to connect it to a database as well. If you want to learn how to connect a mongoDB database you can read my article [Creating MERN Stack Applications (2020)](https://dev.to/andrewbaisden/creating-mern-stack-applications-2020-4a44)

Replace and update the code in the existing files with the ones below

`controllers/admin.js`

```JavaScript
const Books = require('../models/Books');

exports.getIndex = (req, res) => {
	res.send('Book Library Home Route');
};

exports.getBooks = (req, res) => {
	Books.fetchAll((books) => {
		console.log(books);
		res.json(books);
	});
};

exports.getBook = (req, res) => {
	const bookId = req.params.bookId;

	Books.findById(bookId, (book) => {
		console.log(book);
		res.json(book);
	});
};

exports.postAddBook = (req, res) => {
	const { name, author, narrated, img, bookLength, releaseDate, language } = req.body;

	const book = new Books(null, name, author, narrated, img, bookLength, releaseDate, language);
	book.save();
	res.json({ msg: 'Book Added' });
};
```

`data/books.json`

```json
[
	{
		"id": "647f8d9a-97b5-461c-9cfe-b04d8b9e1028",
		"name": "Algorithms to Live By The Computer Science of Human Decisions",
		"author": "Brian Christian, Tom Griffiths",
		"narrated": "Brian Christian",
		"img": "https://m.media-amazon.com/images/I/519lKuoLN-L._SL500_.jpg",
		"bookLength": "11 hrs and 50 mins",
		"releaseDate": "19-04-16",
		"language": "English"
	},
	{
		"id": "acf5dcd6-0b8f-4838-9951-3dd1e0f88aee",
		"name": "Psycho-Cybernetics Updated and Expanded",
		"author": "Maxwell Maltz",
		"narrated": "Matt Furey",
		"img": "https://m.media-amazon.com/images/I/51XVTl7HZTL._SL500_.jpg",
		"bookLength": "12 hrs and 16 mins",
		"releaseDate": "11-04-17",
		"language": "English"
	},
	{
		"id": "edc89cce-c823-4690-afc3-d6aa7c8a3be9",
		"name": "A Survival Guide for Life",
		"author": "Bear Grylls",
		"narrated": "Tom Patrick Stephens",
		"img": "https://m.media-amazon.com/images/I/51pNAYZrptL._SL500_.jpg",
		"bookLength": "3 hrs and 32 mins",
		"releaseDate": "26-09-13",
		"language": "English"
	},
	{
		"id": "f19b22bb-c4b4-42a4-be32-4bffa6a89fac",
		"name": "Never Split the Difference Negotiating as if Your Life Depended on It",
		"author": "Chris Voss, Tahl Raz",
		"narrated": "Michael Kramer",
		"img": "https://m.media-amazon.com/images/I/51TSWCruAHL._SL500_.jpg",
		"bookLength": "8 hrs and 7 mins",
		"releaseDate": "20-06-19",
		"language": "English"
	},
	{
		"id": "94cb2436-2bdf-4872-bfd8-9acb860f5a0d",
		"name": "A Life in Parts",
		"author": "Bryan Cranston",
		"narrated": "Bryan Cranston",
		"img": "https://m.media-amazon.com/images/I/51nBvxV-3+L._SL500_.jpg",
		"bookLength": "8 hrs and 51 mins",
		"releaseDate": "20-10-16",
		"language": "English"
	},
	{
		"id": "e18926e7-494e-4604-82c5-daeb4ea1dde9",
		"name": "Elon Musk",
		"author": "Ashlee Vance",
		"narrated": "Fred Sanders",
		"img": "https://m.media-amazon.com/images/I/51e-uVPtr5L._SL500_.jpg",
		"bookLength": "13 hrs and 23 mins",
		"releaseDate": "28-04-16",
		"language": "English"
	},
	{
		"id": "f69fa7bb-93f6-497f-8e99-108467af8124",
		"name": "Steve Jobs The Exclusive Biography",
		"author": "Walter Isaacson",
		"narrated": "Dylan Baker, Walter Isaacson (introduction)",
		"img": "https://m.media-amazon.com/images/I/51b8AJgZETL._SL500_.jpg",
		"bookLength": "25 hrs and 3 mins",
		"releaseDate": "24-10-11",
		"language": "English"
	},
	{
		"id": "f4008cdd-1c76-4071-8dab-830b6fd3c379",
		"name": "Gut",
		"author": "Giulia Enders",
		"narrated": "Katy Sobey",
		"img": "https://m.media-amazon.com/images/I/5110ffzUFkL._SL500_.jpg",
		"bookLength": "7 hrs and 26 mins",
		"releaseDate": "24-06-15",
		"language": "English"
	},
	{
		"id": "5a1caf9b-f7ce-4ada-9046-309c66b2dc36",
		"name": "The 4-Hour Work Week",
		"author": "Timothy Ferriss",
		"narrated": " Ray Porter",
		"img": "https://m.media-amazon.com/images/I/518+s5Nu4XL._SL500_.jpg",
		"bookLength": "13 hrs and 1 min",
		"releaseDate": "10-11-11",
		"language": "English"
	},
	{
		"id": "86084cd9-5191-4c7f-99b8-acbb930070f1",
		"name": "Cosmos",
		"author": "Carl Sagan",
		"narrated": "LeVar Burton, Seth MacFarlane, Neil deGrasse Tyson, Ann Druyan",
		"img": "https://m.media-amazon.com/images/I/51e91glnHUL._SL500_.jpg",
		"bookLength": "14 hrs and 31 mins",
		"releaseDate": "30-05-17",
		"language": "English"
	}
]
```

`models/Books.js`

```javascript
const fs = require('fs');
const { v4: uuidv4 } = require('uuid');
const path = require('path');
const p = path.join(`${__dirname}/../data/books.json`);

const getBooksFromFile = (cb) => {
	fs.readFile(p, (err, fileContent) => {
		if (err) {
			cb([]);
		} else {
			cb(JSON.parse(fileContent));
		}
	});
};

module.exports = class Books {
	constructor(id, name, author, narrated, img, bookLength, releaseDate, language) {
		this.id = id;
		this.name = name;
		this.author = author;
		this.narrated = narrated;
		this.img = img;
		this.bookLength = bookLength;
		this.releaseDate = releaseDate;
		this.language = language;
	}
	save() {
		getBooksFromFile((books) => {
			this.id = String(uuidv4());

			books.push(this);

			fs.writeFile(p, JSON.stringify(books), (err) => {
				console.log(err);
			});
		});
	}
	static fetchAll(cb) {
		getBooksFromFile(cb);
	}
	static findById(id, cb) {
		getBooksFromFile((books) => {
			const bookId = books.find((b) => b.id === id);
			cb(bookId);
		});
	}
};
```

`routes/admin.js`

```javascript
const express = require('express');
const router = express.Router();
const adminController = require('../controllers/admin');

router.get('/', adminController.getIndex);

router.get('/books', adminController.getBooks);

router.get('/books/:bookId', adminController.getBook);

router.post('/add-book', adminController.postAddBook);

module.exports = router;
```

**There are three CRUD routes**

[http://localhost:8080/books/](http://localhost:8080/books/) is for sending a GET request that will return all of the books as json

[http://localhost:8080/books/647f8d9a-97b5-461c-9cfe-b04d8b9e1028](http://localhost:8080/books/647f8d9a-97b5-461c-9cfe-b04d8b9e1028) is for sending a GET request that will get a book by its bookId (just replace the ID with one for any of the books in the file to return its data as json)

[http://localhost:8080/add-book](http://localhost:8080/add-book) is for sending a POST request that will add a new book to the file. This app does not have a form so you will need to use an API tool like Insomnia or Postman to add new books. Or you could just do it manually by updating the file in `data/books.json`

![https://res.cloudinary.com/d74fh3kw/image/upload/v1597243024/insomnia_g3c15b.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1597243024/insomnia_g3c15b.jpg 'Insomnia API App')

![https://res.cloudinary.com/d74fh3kw/image/upload/v1597243024/postman_u8poty.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1597243024/postman_u8poty.jpg 'Postman API APP')

And thats it for the backend you now have Dynamic API Routes working for the Book data.

## Step 3: Setup the frontend project

`cd` into the root folder for your project and then copy and paste this code into your terminal and then hit enter to setup your React frontend project

```bash
mkdir frontend
cd frontend
npx create-react-app .
npm i react-router-dom
```

Once the setup is complete `cd` back into the backend folder and run the command `npm run servers` so that both the backend and frontend servers run at the same time.

Go to the frontend folder and inside of `src` create folders for `components` and `pages`. Delete all of the css inside of `App.css` Now we are going to get React Router up and running so first create a file called `Home.js` and put it inside the `pages` folder.

Update and add the code below into their corresponding files

`pages/Home.js`

```jsx
import React, { Fragment } from 'react';

const Home = () => {
	return (
		<Fragment>
			<h1>Book Library Home Page</h1>
		</Fragment>
	);
};

export default Home;
```

`app.js`

```jsx
import React from 'react';
import { BrowserRouter as Router, Switch, Route } from 'react-router-dom';
import Home from './pages/Home';
import './App.css';

const App = () => {
	return (
		<Router>
			<Switch>
				<Route exact path="/" component={Home} />
			</Switch>
		</Router>
	);
};

export default App;
```

`index.js`

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

Now when you go to [http://localhost:3000/](http://localhost:3000/) you should see the home page for the Book Library

## Step 4: Create the app

Ok lets finish building this app!

Create a component called `Nav.js` and put it in the `components` folder. Now create two files `Book.js` and `Books.js` and put them in the `pages` folder.

Finally copy and replace the code in the files with the code below

`components/Nav.js`

```jsx
import React, { Fragment } from 'react';
import { Link } from 'react-router-dom';

const Nav = () => {
	// Function for refreshing the page when the :bookId is put into the browser searchbar. Without it the Book component wont load unless you do a manual page reload.
	const refresh = () => {
		setTimeout(() => {
			window.location.reload();
		}, 100);
	};
	return (
		<Fragment>
			<nav>
				<Link onClick={refresh} to="/" href="/" className="logo">
					SoundBite
				</Link>
				<Link onClick={refresh} to="/books" href="/books">
					Library
				</Link>
			</nav>
		</Fragment>
	);
};

export default Nav;
```

`pages/Book.js`

```jsx
import React, { Fragment, useEffect, useState } from 'react';
import Nav from '../components/Nav';

const Book = ({ match }) => {
	useEffect(() => {
		const getAPI = () => {
			const API = 'http://localhost:8080/books';

			fetch(API)
				.then((response) => {
					return response.json();
				})
				.then((data) => {
					console.log(data);
					setLoading(true);
					const book = data.find((p) => p.id === match.params.bookId);
					setData(book);
					console.log(book);
				});
		};
		getAPI();
	}, [match.params.bookId]);

	const [loading, setLoading] = useState(false);
	const [data, setData] = useState([]);

	return (
		<Fragment>
			<main>
				<Nav />
				<h1>My Book</h1>
				<div>
					{loading === false ? (
						<div>
							<h1>Loading...</h1>
						</div>
					) : (
						<div>
							<div key={data.id} className="library-book">
								<div className="library-book-img">
									<img src={data.img} alt={data.name} />
								</div>
								<div className="library-book-content">
									<h1>{data.name}</h1>
									<p>Author: {data.author}</p>
									<p>Narrated by: {data.narrated}</p>
									<p>Length: {data.bookLength}</p>
									<p>Release Date: {data.releaseDate}</p>
									<p>Language: {data.language}</p>
								</div>
								<div className="library-book-listen">
									<p>{data.bookLength}</p>
									<button className="btn-listen">Listen now</button>
									<button className="btn-download">Download</button>
								</div>
							</div>
						</div>
					)}
				</div>
			</main>
		</Fragment>
	);
};

export default Book;
```

`pages/Books.js`

```jsx
import React, { Fragment, useState, useEffect } from 'react';
import { BrowserRouter as Router, Link } from 'react-router-dom';
import Nav from '../components/Nav';

const Books = () => {
	useEffect(() => {
		getAPI();
	}, []);

	const [loading, setLoading] = useState(false);
	const [data, setData] = useState([]);

	const getAPI = () => {
		const API = 'http://localhost:8080/books';

		fetch(API)
			.then((response) => {
				return response.json();
			})
			.then((data) => {
				console.log(data);
				setLoading(true);
				setData(data);
			});
	};

	// Function for refreshing the page when the :bookId is put into the browser searchbar. Without it the Book component wont load unless you do a manual page reload.
	const refresh = () => {
		setTimeout(() => {
			window.location.reload();
		}, 100);
	};

	return (
		<Router>
			<Fragment>
				<main>
					<Nav />
					<div className="library-heading">
						<h1>Library</h1>
						<h2>Titles</h2>
					</div>
					<div className="library-container">
						{loading === false ? (
							<div>
								<h1>Loading...</h1>
							</div>
						) : (
							<div className="library-book-container">
								{data.map((book) => (
									<div key={book.id} className="library-book">
										<div className="library-book-img">
											<Link onClick={refresh} to={`/books/${book.id}`}>
												<img src={book.img} alt={book.name} />
											</Link>
										</div>
										<div className="library-book-content">
											<Link onClick={refresh} to={`/books/${book.id}`}>
												<h1>{book.name}</h1>
											</Link>
											<p>Author: {book.author}</p>
											<p>Narrated by: {book.narrated}</p>
										</div>
										<div className="library-book-listen">
											<p>{book.bookLength}</p>
											<button className="btn-listen">Listen now</button>
											<button className="btn-download">Download</button>
										</div>
									</div>
								))}
							</div>
						)}
					</div>
				</main>
			</Fragment>
		</Router>
	);
};

export default Books;
```

`pages/Home.js`

```jsx
import React, { Fragment } from 'react';
import Nav from '../components/Nav';

const Home = () => {
	return (
		<Fragment>
			<main>
				<Nav />
			</main>
			<div className="hero">
				<h1>SoundBite Original</h1>
				<h2>The</h2>
				<p>Timeman</p>
				<button>Shop now</button>
			</div>
			<div className="banners">
				<section>
					<div>
						<h1>2 for 1</h1>
					</div>
					<div>
						<p>Choose from over 500 listens in top categories</p>
						<button>Shop Now</button>
					</div>
				</section>
				<section>
					<div>
						<h1>Black Sunday</h1>
					</div>
					<div>
						<p>A journey to a new world leads to a revelation</p>
						<button>Shop Now</button>
					</div>
				</section>
				<section>
					<div>
						<h1>Comedy House</h1>
					</div>
					<div>
						<p>Let the fun come to you in these specials</p>
						<button>Shop Now</button>
					</div>
				</section>
				<section>
					<div>
						<h1>The Power</h1>
					</div>
					<div>
						<p>SoundBites best of the best by month</p>
						<button>Shop Now</button>
					</div>
				</section>
			</div>
		</Fragment>
	);
};

export default Home;
```

`App.css`

```css
@import url('https://fonts.googleapis.com/css2?family=Encode+Sans+Condensed:wght@400;500;600;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Philosopher:ital,wght@1,700&display=swap');

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
	font-family: 'Encode Sans Condensed', sans-serif;
	color: #333333;
}

main {
	max-width: 120rem;
	width: 100%;
	margin: 0 auto;
	padding: 2rem;
}

nav {
	display: flex;
	justify-content: start;
	margin-bottom: 4rem;
	align-items: flex-end;
}

nav a {
	margin-right: 2rem;
	text-decoration: none;
	color: #333333;
	font-weight: 500;
}

.logo {
	color: #333333;
	font-size: 3rem;
}

.logo::after {
	content: '';
	display: inline-block;
	width: 2rem;
	height: 2rem;
	background: #f2a517;
	border-radius: 100%;
	position: relative;
	top: -1rem;
}

.logo::before {
	content: 'a terraform company';
	display: block;
	width: 10rem;
	height: 2rem;
	position: relative;
	top: 5.5rem;
	left: 2rem;
	font-size: 1.2rem;
}

.hero {
	width: 100%;
	background: #333333;
	height: 40rem;
	text-align: center;
	color: #ffffff;
	padding: 5rem;
	display: grid;
	justify-content: center;
	align-items: center;
}

.hero h2,
.hero p {
	text-transform: uppercase;
	font-family: 'Philosopher', sans-serif;
}

.hero p {
	font-size: 9rem;
}

.hero button,
.banners button {
	background: #f1a517;
	border: none;
	border-radius: 0.5rem;
	padding: 1rem;
	cursor: pointer;
	margin: 1rem 0 1rem 0;
}

.banners {
	display: grid;
	grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
	padding: 2rem;
	grid-gap: 2rem;
}

.banners section {
	display: grid;
	grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
	background: #cccccc;
	padding: 4rem;
	grid-gap: 2rem;
}

.library-heading {
	border-bottom: 0.1rem solid rgb(236, 236, 236);
}

.library-heading h1 {
	font-size: 5rem;
}

.library-heading h2 {
	font-weight: 700;
	margin: 2rem 0 2rem 0;
}

.library-book {
	display: flex;
	flex-flow: row wrap;
	margin: 2rem 0 2rem 0;
	border-bottom: 0.1rem solid rgb(236, 236, 236);
}

.library-book img {
	width: 15rem;
	margin-right: 2rem;
	margin-bottom: 2rem;
}

.library-book-content {
	max-width: 80rem;
	width: 100%;
}

.library-book-content a {
	text-decoration: none;
}

.library-book-content h1 {
	font-size: 2rem;
	color: #333333;
	font-weight: 600;
}

.library-book-content p {
	margin: 1rem 0 1rem 0;
}

.library-book-listen {
	display: flex;
	flex-flow: column wrap;
	justify-content: space-evenly;
	margin: 2rem 0 2rem 0;
}

.btn-listen {
	background: #f1a517;
	border: none;
	border-radius: 0.5rem;
	padding: 1rem;
	cursor: pointer;
	margin: 1rem 0 1rem 0;
}

.btn-download {
	background: #e6e6e6;
	border: none;
	border-radius: 0.5rem;
	padding: 1rem;
	cursor: pointer;
	margin: 1rem 0 1rem 0;
}

@media screen and (max-width: 960px) {
	.banners {
		grid-template-columns: 1fr;
	}

	.library-book {
		justify-content: center;
		align-items: center;
	}
	.library-book-content {
		display: flex;
		flex-flow: column wrap;
		justify-content: center;
		align-items: center;
	}
}
```

`App.js`

```jsx
import React from 'react';
import { BrowserRouter as Router, Switch, Route } from 'react-router-dom';
import Home from './pages/Home';
import './App.css';
import Books from './pages/Books';
import Book from './pages/Book';

const App = () => {
	return (
		<Router>
			<Switch>
				<Route exact path="/" component={Home} />
				<Route exact path="/books" component={Books} />
				<Route exact path="/books/:bookId" component={Book} />
			</Switch>
		</Router>
	);
};

export default App;
```

Your App should look like the images below! Congrats you just learned the basics of creating backend and frontend dynamic API routes.

**Books Home Page**

![Books Home Page](https://res.cloudinary.com/d74fh3kw/image/upload/v1597259350/books_home_sb9d3s.png 'Books Home Page')

**Books Library Page**

![Books Library Pag](https://res.cloudinary.com/d74fh3kw/image/upload/v1597259040/books_hmundj.png 'Books Library Pag')

**My Book Page**

![My Book Page](https://res.cloudinary.com/d74fh3kw/image/upload/v1597259040/book_n1vnld.png 'My Book Page')
