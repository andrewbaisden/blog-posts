These days it is quite normal for apps to be developed that run on various platforms. This allows users to access the same application using different devices. In this tutorial you will learn how to create cross platform apps that work on the web, and on mobile. The web version will be created using React and Redux whereas the mobile versions will be created using React Native and Redux. We will be using the Expo framework to create the React Native and Redux apps.

The App that we will be creating is called Deck of Cards. It is just a simple app that lets you randomly place cards on a card table that automatically get removed after a set amount of time.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1618509335/Deck_of_Cards_up0fvv.png](https://res.cloudinary.com/d74fh3kw/image/upload/v1618509335/Deck_of_Cards_up0fvv.png 'Deck of Cards App')

## Setup

Before we begin make sure that you have your development environment setup with [Node](https://nodejs.org/en/) installed with the correct packages. If you are working on a Mac then you will be able to use the Apple Simulator as well as Android Simulators. If you are working on Windows or Linux then you can only use Android Simulators for testing. However you should be able to connect your own physical device to either operating system so that you can test the apps on your phone.

### Tools Required

- An IDE or Code Editor like Visual Studio Code
- A Terminal/Bash Application like Hyper, iTerm 2, Apple Terminal etc...
- The [Redux DevTools](https://github.com/reduxjs/redux-devtools) installed in your browser

### Packages Required

- [Create React App](https://reactjs.org/docs/create-a-new-react-app.html)
- [Expo Framework](https://expo.io/)
- [Redux](https://redux.js.org/)
- [yarn](https://yarnpkg.com/) (optional you can use either npm or yarn)

## Contents

- [Creating the web version using React and Redux](#Creating the web version using React and Redux)
- [Creating the mobile versions using React Native and Redux](#Creating the mobile versions using React Native and Redux)

## Creating the web version using React and Redux

### Project Setup

Create a folder on your desktop called **deck of cards** and then open the project in your code editor. Now use your terminal to **cd** into the project directory and then setup a boilerplate React Application using the code below.

```bash
npx create-react-app my-app-web
```

Once the app has been setup **cd** into it using your terminal application and then run the application.

```bash
cd my-app-web
npm run start
```

You should see the app running in your browser. It's time to install some packages and clean up the boilerplate for the React App. First you need to install the packages below using your terminal app so make sure that you are in the root directory with the `package.json` file in it.

```bash
npm i redux react-redux redux-thunk redux-devtools-extension uuid
```

Now delete all of the files inside of the **src** folder. The app is going to break but don't worry we are just getting rid of the bloatware so we can start from scratch. Your project should have a tree structure like below.

```bash
└── my-app-web
    ├── README.md
    ├── node_modules
    ├── package-lock.json
    ├── package.json
    ├── public
    │   ├── favicon.ico
    │   ├── index.html
    │   ├── logo192.png
    │   ├── logo512.png
    │   ├── manifest.json
    │   └── robots.txt
    ├── src
    └── yarn.lock
```

Now make sure that you are in the **src** folder. Create an `index.js` file and enter the code below.

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

Next you need to create an `App.js` file in the same folder and enter the code below.

```jsx
import React, { Fragment } from 'react';

const App = () => {
	return (
		<Fragment>
			<h1>React App</h1>
		</Fragment>
	);
};

export default App;
```

You might need to reload the webpage or restart the server. Afterwards you should see the page working with the heading text.

### Setting up the Redux Store

With the React App setup and working we can now start working on the Redux Store. We will need a `store.js` file as well as folders for **actions** and **reducers**. If you open your web browser and got to the Redux DevTools it should say something like "_No store found. Make sure to follow the instructions._"

Create a `store.js` file in the **src** folder and then enter the code below to setup the Redux Store.

```jsx
import { createStore, applyMiddleware } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';
import thunk from 'redux-thunk';
import rootReducer from './reducers';

const initialState = {};

const middleware = [thunk];

const store = createStore(rootReducer, initialState, composeWithDevTools(applyMiddleware(...middleware)));

export default store;
```

Now update the `index.js` file with the code below.

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import store from './store';
import { Provider } from 'react-redux';

ReactDOM.render(
	<Provider store={store}>
		<App />
	</Provider>,
	document.getElementById('root')
);
```

Next create an empty folder called **actions** and an empty folder called **reducers** and put them in the **src** folder. Go inside the **reducers** folder and create a file called `index.js`. Add the code below to that file.

```jsx
import { combineReducers } from 'redux';

export default combineReducers({});
```

Once you have done that return to the app in the browser and reload the page. If you go to the Redux DevTools you should see it working now.

### Creating the Cards Reducer

The next step will be to create files for the actions as well as a reducer file for the reducer. The actions folder will also contain a file for the constants which will be centralised so you will only need to change them in one place. Go into the **actions** folder and create a file called `types.js` and a file called `card.js` . Put the code below into the `types.js` file.

```jsx
export const SET_CARD = 'SET_CARD';
export const REMOVE_CARD = 'REMOVE_CARD';
```

Now go into the **reducers** folder and create a file called `card.js` . Add the code below into that file. This will set up the state as well as the function which will be used for the reducer.

```jsx
import { SET_CARD, REMOVE_CARD } from '../actions/types';

const initialState = [
	{
		text: 'Deck of Cards',
	},
];

export default function (state = initialState, action) {
	const { type, payload } = action;

	switch (type) {
		case SET_CARD:
			return [...state, payload];
		case REMOVE_CARD:
			return state.filter((card) => card.id !== payload);
		default:
			return state;
	}
}
```

Now update the `index.js` file in the **reducers** folder with an import for the `card.js` file.

```jsx
import { combineReducers } from 'redux';
import card from './card';

export default combineReducers({
	card,
});
```

Next go into the **actions** folder and add the code below to the `card.js` file. This will set up the dispatch function that will send the data. This will dispatch the card information as an action that will pass the state.

```jsx
import uuid from 'uuid';
import { SET_CARD, REMOVE_CARD } from './types';

export const setCard = (msg, cardType) => (dispatch) => {
	const id = uuid.v4();
	dispatch({
		type: SET_CARD,
		payload: { msg, cardType, id },
	});

	// Change the value in the set time out to increase or decrease the time. The default is 10000 which equals 10 seconds
	// Alternativly you can comment out the code below so that the cards just stay on the screen and don't get removed
	setTimeout(() => dispatch({ type: REMOVE_CARD, payload: id }), 10000);
};
```

### Connecting the App to the Redux Store

Finally we will connect the actions and reducers to the main `App.js` file. Firstly create an `App.css` file and put it in the root of the **src** folder. Add the below styles to the `App.css` file.

```css
@import url('https://fonts.googleapis.com/css2?family=Karantina:wght@300;400;700&display=swap');
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}

html {
	font-size: 62.5%;
}

body {
	font-size: 1.6rem;
	font-family: 'Karantina', cursive;
	background: #4f8a82;
}

main {
	margin: 0 auto;
	max-width: 100%;
	width: 120rem;
}

.container {
	margin: 2rem 2rem 2rem 2rem;
}

.heading-text {
	color: #ffffff;
	margin: 2rem 0 2rem 0;
	font-size: 4rem;
	text-transform: uppercase;
	text-align: center;
}

.card-board-container {
	margin: 2rem auto;
	padding: 2rem 0 2rem 4.5rem;
	display: flex;
	flex-flow: row wrap;
	max-width: 100%;
	width: 120rem;
	border: 1rem solid #943807;
	height: 60rem;
}

.btn-place-card {
	cursor: pointer;
	padding: 2rem;
	border: 0.2rem solid #ffdd07;
	background: #284743;
	color: #ffdd07;
	font-weight: 700;
	text-transform: uppercase;
	transition: background 0.5s;
}

.btn-place-card:hover {
	background: #48726c;
	border: 0.2rem solid #ffea63;
}

.btn-place-card:focus {
	outline: 0;
}

.card {
	margin-bottom: 2rem;
}

/* Use the CSS below as a reference for adding a full deck of cards which is 52 cards in total */
/* Example full deck of cards */
/* https://upload.wikimedia.org/wikipedia/commons/thumb/8/81/English_pattern_playing_cards_deck.svg/1200px-English_pattern_playing_cards_deck.svg.png */

.card-spade-1,
.card-spade-2,
.card-spade-3,
.card-heart-1,
.card-heart-2,
.card-heart-3,
.card-diamond-1,
.card-diamond-2,
.card-diamond-3,
.card-club-1,
.card-club-2,
.card-club-3 {
	width: 7rem;
	height: 9.5rem;
	background: #ffffff;
	box-shadow: 0px 0px 17px 0px rgba(199, 199, 199, 1);
}

.card-spade-1::before {
	content: '🂡';
	color: black;
	position: relative;
	font-size: 12rem;
	top: -2.54rem;
	left: -0.9rem;
}

.card-spade-2::before {
	content: '🂢';
	color: black;
	position: relative;
	font-size: 12rem;
	top: -2.54rem;
	left: -0.9rem;
}

.card-spade-3::before {
	content: '🂣';
	color: black;
	position: relative;
	font-size: 12rem;
	top: -2.54rem;
	left: -0.9rem;
}

.card-heart-1::before {
	content: '🂱';
	color: #ff5555;
	position: relative;
	font-size: 12rem;
	top: -2.54rem;
	left: -0.9rem;
}

.card-heart-2::before {
	content: '🂲';
	color: #ff5555;
	position: relative;
	font-size: 12rem;
	top: -2.54rem;
	left: -0.9rem;
}

.card-heart-3::before {
	content: '🂳';
	color: #ff5555;
	position: relative;
	font-size: 12rem;
	top: -2.54rem;
	left: -0.9rem;
}

.card-diamond-1::before {
	content: '🃁';
	color: #ff5555;
	position: relative;
	font-size: 12rem;
	top: -2.54rem;
	left: -0.9rem;
}

.card-diamond-2::before {
	content: '🃂';
	color: #ff5555;
	position: relative;
	font-size: 12rem;
	top: -2.54rem;
	left: -0.9rem;
}

.card-diamond-3::before {
	content: '🃃';
	color: #ff5555;
	position: relative;
	font-size: 12rem;
	top: -2.54rem;
	left: -0.9rem;
}

.card-club-1::before {
	content: '🃑';
	color: #000000;
	position: relative;
	font-size: 12rem;
	top: -2.54rem;
	left: -0.9rem;
}

.card-club-2::before {
	content: '🃒';
	color: #000000;
	position: relative;
	font-size: 12rem;
	top: -2.54rem;
	left: -0.9rem;
}

.card-club-3::before {
	content: '🃓';
	color: #000000;
	position: relative;
	font-size: 12rem;
	top: -2.54rem;
	left: -0.9rem;
}
```

Now open the `App.js` file inside of the **src** folder and replace the code inside with the one below.

```jsx
import { connect } from 'react-redux';
import { setCard } from './actions/card';
import PropTypes from 'prop-types';
import { useState, Fragment } from 'react';
import './App.css';

function App({ setCard, cards }) {
	const [cardRandomNum, setCardRandomNum] = useState(1);
	const [card] = useState(['spade', 'heart', 'diamond', 'club']);
	const [cardTypeOutput, setCardTypeOutput] = useState('spade');

	const btnHandleClick = () => {
		// Change the code below to Math.floor(Math.random() * 13 + 1) if you want to get cards from 1 - 13 which is the full deck. 52 cards in total.
		setCardRandomNum(Math.floor(Math.random() * 3 + 1));
		console.log(cardRandomNum);

		const cardType = [Math.floor(Math.random() * card.length)];

		setCardTypeOutput(card[cardType]);
		console.log(cardTypeOutput);

		setCard(cardRandomNum, cardTypeOutput);
		console.log(cards);
	};
	return (
		<Fragment>
			<main>
				<section className="container">
					<div>
						<h1 className="heading-text">{cards[0].text}</h1>
					</div>
					<div>
						<button className="btn-place-card" onClick={btnHandleClick}>
							Place Cards
						</button>
					</div>

					<div className="card-board-container">
						{(cards !== null) & (cards.length > 0) &&
							cards.map((card) => <div key={card.id} className={`card card-${card.cardType}-${card.msg}`}></div>)}
					</div>
				</section>
			</main>
		</Fragment>
	);
}

App.propTypes = {
	setCard: PropTypes.func.isRequired,
	cards: PropTypes.array.isRequired,
};

const mapStateToProps = (state) => ({
	cards: state.card,
});

export default connect(mapStateToProps, { setCard })(App);
```

You might need to reload the page or restart the server but when you do you should see the Deck of Cards App working. All you have to do is repeatedly click on the place cards button and it should randomly generate cards inside of the table box. Each set of cards goes up to 3 however you can expand it to all 52 cards in a deck by changing a few lines of code. The cards are automatically removed after 10 seconds using the **REMOVE_CARD** dispatch action in the `actions/card./js` file. If you want to you can change the timing or remove it completely so that the cards stay on the screen.

Alternatively if you want to add more cards you will need to follow the comments inside of the `App.js` file and the `App.css` file to do it. To add more card icons you just need to add or replace them with new unicode characters. You can find some [here](https://www.webnots.com/alt-code-shortcuts-for-playing-cards-suit/) .

## Creating the mobile versions using React Native and Redux

### Project Setup

Create a folder on your desktop called **deck of cards** or use the one that you already created before and then open the project in your code editor. Now use your terminal to **cd** into the project directory and then setup a boilerplate React Native Application using the code below. Make sure that you choose the **blank** option. We will be using **yarn** for the tutorial but you can use **npm** if you want to.

```bash
expo init my-app-mobile
```

Once the app has been setup **cd** into it using your terminal application and then run the application.

```bash
cd my-app-mobile
yarn start
```

You should see a web browser window open with the Expo Developer Tools. Run the app using one of the simulators or use a device by scanning the barcode with your phone. It's time to install some packages and clean up the boilerplate for the React Native App. First you need to install the packages below using your terminal app so make sure that you are in the root directory with the `package.json` file in it.

```bash
yarn add redux react-redux redux-thunk redux-devtools-extension uuid
```

Your project should have a tree structure like below.

```bash
├── App.js
├── app.json
├── assets
│   ├── adaptive-icon.png
│   ├── favicon.png
│   ├── icon.png
│   └── splash.png
├── babel.config.js
├── node_modules
├── package.json
└── yarn.lock
```

### Setting up the Redux Store

With the React Native App setup and working we can now start working on the Redux Store. We will need a `store.js` file as well as folders for **actions**, **reducers **and **components**. If you run the app in a web browser and got to the Redux DevTools it should say something like "_No store found. Make sure to follow the instructions._"

Create a **src** folder and then create a `store.js` file inside of it and then enter the code below to setup the Redux Store.

```jsx
import { createStore, applyMiddleware } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';
import thunk from 'redux-thunk';
import rootReducer from './reducers';

const initialState = {};

const middleware = [thunk];

const store = createStore(rootReducer, initialState, composeWithDevTools(applyMiddleware(...middleware)));

export default store;
```

Now update the `App.js` file with the code below.

```jsx
import React from 'react';
import store from './src/store';
import { Provider } from 'react-redux';
import DeckOfCards from './src/components/DeckOfCards';

const App = () => {
	return (
		<Provider store={store}>
			<DeckOfCards />
		</Provider>
	);
};

export default App;
```

In the next step create a folder called **components** and put it inside of the **src** folder. Now create a file called `DeckOfCards.js` inside of it. Add the code below to that file.

```jsx
import React from 'react';
import { View, Text, StyleSheet, TouchableOpacity, FlatList } from 'react-native';
import { setCard } from '../actions/card';
import { connect } from 'react-redux';
import PropTypes from 'prop-types';
import { useState } from 'react';

const App = ({ setCard, cards }) => {
	const [cardRandomNum, setCardRandomNum] = useState(1);
	const [card] = useState(['spade', 'heart', 'diamond', 'club']);
	const [cardTypeOutput, setCardTypeOutput] = useState('spade');

	const btnHandleClick = () => {
		// Change the code below to Math.floor(Math.random() * 13 + 1) if you want to get cards from 1 - 13 which is the full deck. 52 cards in total.
		setCardRandomNum(Math.floor(Math.random() * 3 + 1));
		console.log(cardRandomNum);

		const cardType = [Math.floor(Math.random() * card.length)];

		setCardTypeOutput(card[cardType]);
		console.log(cardTypeOutput);

		setCard(cardRandomNum, cardTypeOutput);
		console.log(cards);
	};

	return (
		<View style={styles.appContainer}>
			<View style={styles.appHeading}>
				<View>
					<Text style={styles.heading}>Deck of Cards</Text>
				</View>
				<View style={{ marginTop: 50 }}>
					<TouchableOpacity onPress={btnHandleClick}>
						<Text style={styles.cardBtn}>Place Cards</Text>
					</TouchableOpacity>
				</View>
			</View>
			<View style={styles.appMain}>
				<View>
					<FlatList
						numColumns={11}
						keyExtractor={(card) => card.id}
						data={cards}
						renderItem={({ item }) => {
							let cardTypeGraphic = '';
							let cardColorType = '';

							const spade = {
								one: {
									graphic: '🂡',
								},
								two: {
									graphic: '🂢',
								},
								three: {
									graphic: '🂣',
								},
							};

							const heart = {
								one: {
									graphic: '🂱',
								},
								two: {
									graphic: '🂲',
								},
								three: {
									graphic: '🂳',
								},
							};

							const diamond = {
								one: {
									graphic: '🃁',
								},
								two: {
									graphic: '🃂',
								},
								three: {
									graphic: '🃃',
								},
							};

							const club = {
								one: {
									graphic: '🃑',
								},
								two: {
									graphic: '🃒',
								},
								three: {
									graphic: '🃓',
								},
							};

							if (item.cardType === 'spade' && item.msg === 1) {
								cardTypeGraphic = spade.one.graphic;
								cardColorType = 'black';
							} else if (item.cardType === 'spade' && item.msg === 2) {
								cardTypeGraphic = spade.two.graphic;
								cardColorType = 'black';
							} else if (item.cardType === 'spade' && item.msg === 3) {
								cardTypeGraphic = spade.three.graphic;
								cardColorType = 'black';
							} else if (item.cardType === 'heart' && item.msg === 1) {
								cardTypeGraphic = heart.one.graphic;
								cardColorType = 'red';
							} else if (item.cardType === 'heart' && item.msg === 2) {
								cardTypeGraphic = heart.two.graphic;
								cardColorType = 'red';
							} else if (item.cardType === 'heart' && item.msg === 3) {
								cardTypeGraphic = heart.three.graphic;
								cardColorType = 'red';
							} else if (item.cardType === 'diamond' && item.msg === 1) {
								cardTypeGraphic = diamond.one.graphic;
								cardColorType = 'red';
							} else if (item.cardType === 'diamond' && item.msg === 2) {
								cardTypeGraphic = diamond.two.graphic;
								cardColorType = 'red';
							} else if (item.cardType === 'diamond' && item.msg === 3) {
								cardTypeGraphic = diamond.three.graphic;
								cardColorType = 'red';
							} else if (item.cardType === 'club' && item.msg === 1) {
								cardTypeGraphic = club.one.graphic;
								cardColorType = 'black';
							} else if (item.cardType === 'club' && item.msg === 2) {
								cardTypeGraphic = club.two.graphic;
								cardColorType = 'black';
							} else if (item.cardType === 'club' && item.msg === 3) {
								cardTypeGraphic = club.three.graphic;
								cardColorType = 'black';
							}

							return (
								<View>
									{cards.length <= 0 ? (
										<View>
											<Text></Text>
										</View>
									) : (
										<View style={styles.cardContainer}>
											<View style={styles.card}>
												<View>
													<Text
														style={{
															marginLeft: -3,
															// You might need to change the marginTop value if the cards are not aligned on your device
															marginTop: 0,
															padding: 0,
															fontSize: 60,
															color: `${cardColorType}`,
														}}
													>
														{cardTypeGraphic}
													</Text>
												</View>
											</View>
										</View>
									)}
								</View>
							);
						}}
					/>
				</View>
			</View>
		</View>
	);
};

const styles = StyleSheet.create({
	appContainer: {
		backgroundColor: '#4f8a82',
		height: '100%',
		width: '100%',
	},
	appHeading: {
		marginTop: 50,
	},
	heading: {
		textTransform: 'uppercase',
		color: '#ffffff',
		fontWeight: 'bold',
		textAlign: 'center',
		fontSize: 20,
	},
	cardBtn: {
		backgroundColor: '#284743',
		textAlign: 'center',
		color: '#ffdd07',
		textTransform: 'uppercase',
		padding: 20,
		fontWeight: 'bold',
		borderWidth: 2,
		borderColor: '#ffdd07',
	},
	appMain: {
		marginTop: 50,
		marginBottom: 50,
		height: '100%',
		borderColor: '#943807',
		borderLeftWidth: 10,
		borderRightWidth: 10,
		borderTopWidth: 10,
		borderBottomWidth: 10,
		padding: 10,
	},
	flatlist: {
		flexDirection: 'column',
	},
	cardContainer: {
		display: 'flex',
		flexDirection: 'row',
		flexWrap: 'wrap',
		alignSelf: 'baseline',
	},
	card: {
		backgroundColor: '#ffffff',
		shadowColor: 'rgba(199, 199, 199, 1)',
		height: 46,
		width: 35,
	},
});

App.propTypes = {
	setCard: PropTypes.func.isRequired,
	cards: PropTypes.array.isRequired,
};

const mapStateToProps = (state) => ({
	cards: state.card,
});

export default connect(mapStateToProps, { setCard })(App);
```

### Creating the Cards Reducer

Next create an empty folder called **actions** and an empty folder called **reducers** and put them in the **src** folder. Go inside the **reducers** folder and create a file called `index.js`. Add the code below to that file.

```jsx
import { combineReducers } from 'redux';
import card from './card';

export default combineReducers({
	card,
});
```

After you have done that create a `card.js` file and put it in the same **reducers** folder. Add the code below to that file.

```jsx
import { SET_CARD, REMOVE_CARD } from '../actions/types';

const initialState = [];

export default function (state = initialState, action) {
	const { type, payload } = action;

	switch (type) {
		case SET_CARD:
			return [...state, payload];
		case REMOVE_CARD:
			return state.filter((card) => card.id !== payload);
		default:
			return state;
	}
}
```

Finally go to the **actions** folder and then create a `card.js` file and a `types.js` file.

Add the code below into the `types.js` file

```jsx
export const SET_CARD = 'SET_CARD';
export const REMOVE_CARD = 'REMOVE_CARD';
```

Now enter the code below into the `card.js` file

```jsx
import uuid from 'uuid';
import { SET_CARD, REMOVE_CARD } from './types';

export const setCard = (msg, cardType) => (dispatch) => {
	// uuid might not work be working properly with this version of Expo so a random number is used in this example instead
	// const id = uuid.v4();
	const id = String(Math.floor(Math.random() * 9000));
	dispatch({
		type: SET_CARD,
		payload: { msg, cardType, id },
	});

	// Change the value in the set time out to increase or decrease the time. The default is 10000 which equals 10 seconds
	// Alternativly you can comment out the code below so that the cards just stay on the screen and don't get removed
	setTimeout(() => dispatch({ type: REMOVE_CARD, payload: id }), 10000);
};
```

If you did everything correctly you should see the app working on mobile! You will probably need to reload the browser or restart your simulator or phone to see it working. You might need to play around with the styles inside of the `DeckOfCards.js` file if it is not rendering correctly as every device and setup is different.

## Final Thoughts

I really hope that you enjoyed reading this article and learned something from it. As a content creator and technical writer I am passionate about sharing my knowledge and helping other people reach their goals. Let's connect across social media you can find all of my social media profiles and blogs on [linktree](https://linktr.ee/andrewbaisden).

Peace ✌️
