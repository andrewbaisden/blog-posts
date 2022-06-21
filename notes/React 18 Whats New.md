# React 18 Whats New

The latest version of React (version 18) has been officially available since March 2022. It brought along many new features and behind the scenes changes which have made the framework even more powerful. React continues to be the first and preferred framework of choice for JavaScript developers and is always highly sought after in companies.

Many new features were introduced in React 18 and today we will cover some of the more popular ones because those features are likely to get used the most by developers in their projects. I will cover the following:

- React Suspense
- The New Root API
- The New useId hook
- The New useTransition hook

## React Suspense

When using a REST API there are two ways to retrieve data. You can do them synchronously or asynchronously. Synchronous API calls are known as blocking calls because they are unable to return anything until the request has completed or there was some error returning the data. This type of API call locks up the application and prevents the user from doing anything until the action is done.

On the other hand an Asynchronous API call does the complete opposite to this. It is non blocking and the response is returned immediately while the request continues to process in the background. Your application remains responsive and does not lock up waiting for something to happen so you can continue to use it while the data is retrieved in the background. This gives the user a much better experience on the frontend.

Essentially React Suspense is asynchronous because it forces your components to wait for something to happen before they can render the data inside of the API or data structure. The components must wait for an asynchronous API call to complete fetching some data before it is rendered on a screen. Behind the scenes the data is loading and it is possible to show a fallback preloader to the user so that they are aware that something is happening on the frontend.

### React Suspense Example

This is the the new syntax which uses React Suspense combined with the React.lazy() API.
`App.js`

```javascript
// The new syntax for React 18 using React.lazy() to delay loading the component so that Suspense works properly.

import { Suspense, lazy } from 'react';

const Pokemon = lazy(() => {
	return import('./Pokemon');
});

const App = () => {
	return (
		<Suspense fallback={<h1>Loading pokemon...</h1>}>
			<Pokemon />
		</Suspense>
	);
};

export default App;
```

`Pokemon.js`

```javascript
// The new syntax for React 18

import React, { useEffect, useState } from 'react';

const Pokemon = () => {
	useEffect(() => {
		const getPokemons = () => {
			const API = 'http://pokeapi.co/api/v2/pokemon?limit=500';

			fetch(API)
				.then((response) => {
					console.log(response);

					return response.json();
				})

				.then((data) => {
					console.log(data.results);

					setData(data.results);
				})

				.catch((err) => {
					console.log(err);
				});
		};

		getPokemons();
	}, []);

	const [data, setData] = useState([]);

	return (
		<>
			{/* You don't need a ternary operator with a variable for loading anymore */}

			{data.map((pokemon) => (
				<div key={pokemon.name}>
					<h2>{pokemon.name}</h2>
				</div>
			))}
		</>
	);
};

export default Pokemon;
```

### Ternary Operator Example

This is the old syntax which uses the JavaScript Ternary Operator combined with a variable state that checks if the data is loading or has loaded. It displays a preloader when the data has yet to be loaded and the data when it is complete.

`App.js`

```javascript
// The old syntax

import Pokemon from './Pokemon';

const App = () => {
	return (
		<>
			<Pokemon />
		</>
	);
};

export default App;
```

`Pokemon.js`

```javascript
// The old syntax

import React, { useEffect, useState } from 'react';

const Pokemon = () => {
	useEffect(() => {
		const getPokemons = () => {
			const API = 'http://pokeapi.co/api/v2/pokemon?limit=500';

			fetch(API)
				.then((response) => {
					console.log(response);

					return response.json();
				})

				.then((data) => {
					console.log(data.results);

					setLoading(false);

					setData(data.results);
				})

				.catch((err) => {
					console.log(err);
				});
		};

		getPokemons();
	}, []);

	const [data, setData] = useState([]);

	const [loading, setLoading] = useState(true);

	return (
		<>
			{/* The old syntax using ternary operators with a variable for loading */}

			{loading ? (
				<h1>Loading pokemon...</h1>
			) : (
				<div>
					{data.map((pokemon) => (
						<div key={pokemon.name}>
							<h2>{pokemon.name}</h2>
						</div>
					))}
				</div>
			)}
		</>
	);
};

export default Pokemon;
```

## The New Root API

React 18 has new syntax for the root index.js file which gives you access to new features and improvements. The previous syntax will give you a red warning message in the console because ReactDOM.render is no longer supported in React 18. Use the new syntax to clear the warning message.

You are now required to use createRoot instead and until you switch to the new API, your app will behave as if it’s running React 17. The new root API has a cleaner and clearer syntax and the new concurrent renderer becomes enabled so you can now access concurrent features which the previous API could not.

### New Syntax

```javascript
import ReactDOM from 'react-dom/client';

import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));

root.render(<App />);
```

### Old Syntax

```javascript
import React from 'react';

import ReactDOM from 'react-dom';

import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

## The New useId hook

React 18 gives you a useful way for generating id's when creating DOM elements with the new useId hook. If you have multiple id's you can even append a suffix like "twitter" to make it unique.

Bonus Tip: You can make the label clickable by adding the **htmlFor** tag for example.

`App.js`

```javascript
import { useId } from 'react';

const App = () => {
	const id = useId();

	return (
		<>
			<div>
				<label htmlFor={`${id}-twitter`}>Do you have a Twitter?</label>

				<input id={`${id}-twitter`} type="checkbox" name="twitter" />
			</div>

			<div>
				<label>Do you have a Instagram?</label>

				<input id={`${id}-instagram`} type="checkbox" name="instagram" />
			</div>

			<div>
				<label>Do you have a YouTube?</label>

				<input id={id} type="checkbox" name="youtube" />
			</div>
		</>
	);
};

export default App;
```

## The New useTransition hook

In React 18 you can use the new useTransition hook to load data before rendering it to the screen. When you use the return value **isPending** you can create a preloader for each loading transition.

You can see it in action in this custom carousel slider.

`App.js`

```javascript
import { useState, useEffect, useTransition } from 'react';

const App = () => {
	useEffect(() => {
		mountain().then((data) => {
			console.log(data);

			setLoading(false);

			setData(data);
		});
	}, []);

	let [data, setData] = useState([]);

	let [loading, setLoading] = useState(true);

	let [count, setCount] = useState(0);

	let [index, setIndex] = useState(0);

	let [isPending, startTransition] = useTransition();

	const showNext = () => {
		startTransition(() => {
			setCount(count + 1);
		});

		setIndex(count + 1);

		console.log('Count', count + 1);
	};

	const showPrevious = () => {
		startTransition(() => {
			setCount(count - 1);
		});

		setIndex(count - 1);

		console.log('Count', count - 1);
	};

	const mountain = (loaded) => {
		return new Promise((resolve, reject) => {
			setTimeout(() => {
				if (loaded) {
					reject(new Error('Failed to load data'));
				} else {
					resolve([
						{
							id: 0,

							name: 'Mountain 1',

							img: 'https://images.unsplash.com/photo-1570641963303-92ce4845ed4c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1587&q=80',
						},

						{
							id: 1,

							name: 'Mountain 2',

							img: 'https://images.unsplash.com/photo-1434394354979-a235cd36269d?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2051&q=80',
						},

						{
							id: 2,

							name: 'Mountain 3',

							img: 'https://images.unsplash.com/photo-1472791108553-c9405341e398?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2137&q=80',
						},
					]);
				}
			}, 2000);
		});
	};

	return (
		<>
			{loading ? (
				<h1>Loading...</h1>
			) : (
				<div>
					{isPending ? (
						<div>
							<h1>Loading the next image</h1>
						</div>
					) : (
						<div>
							<h1>{data[index].name}</h1>

							<img src={data[index].img} alt="Mountain" style={{ width: '100%', height: '300px', maxWidth: '500px' }} />
						</div>
					)}
				</div>
			)}

			<button onClick={showPrevious} disabled={count === 0 ? true : false}>
				Previous
			</button>

			<button onClick={showNext} disabled={count === 2 ? true : false}>
				Next
			</button>
		</>
	);
};

export default App;
```

## Final Thoughts

This was a brief introduction into the new features inside of React 18. Take a look at the official blog to see all of the new documentation [React v18.0](https://reactjs.org/blog/2022/03/29/react-v18.html).
