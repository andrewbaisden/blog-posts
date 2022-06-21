# Building a user authenticated dashboard in React Native

In this tutorial you will learn how to create a React Native application that has a user authenticated dashboard. Users will be able to sign up by creating an account and then sign into their user dashboard. They will be able to view some information associated with their account and the app will give the user the ability to sign up, sign in and sign out of their account.

## Prerequisites

Before you begin make sure that you have the following tools and packages installed and setup.

[Node and npm](https://nodejs.org/en/)
[Expo CLI](https://docs.expo.io/)
[MongoDB Atlas](https://www.mongodb.com/try/download/community)
[MongoDB Compass](https://www.mongodb.com/try/download/compass)
[Postman](https://www.postman.com/) or [Insomnia](https://insomnia.rest/) (We will be using Postman API in this tutorial but you can use Insomnia or something different)
[Visual Studio Code](https://code.visualstudio.com/) (Or an IDE of your choice)
[Hyper](https://hyper.is/) (Or a BASH application of your choice like iTerm2 etc...)
[Yarn](https://yarnpkg.com/) (We will using Yarn with React Native you can use npm if you want but you will have to make some slight changes)

## Building the back-end

### Creating a MongoDB Database

For production you need to use an online database because a local database is for development purposes only. Either way you can use whichever one you want in this guide.

#### Online

Make sure that you have an account online with [MongoDB Atlas](https://www.mongodb.com/try/download/community). You will need to create a new cluster and then select a location that is near you in the free tier. You will probably need to create a user under **Security** and then under **Network Access** you will need to whitelist your IP address so that you can connect to the database.

Next click on the **Connect** button followed by the **Connect your application** button. See the images below for an example of the process.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1626276793/mongodb-atlas-01_spkoaz.png](https://res.cloudinary.com/d74fh3kw/image/upload/v1626276793/mongodb-atlas-01_spkoaz.png 'MongoDB Atlas choose connection')

![https://res.cloudinary.com/d74fh3kw/image/upload/v1626276793/mongodb-atlas-02_ql4awq.png](https://res.cloudinary.com/d74fh3kw/image/upload/v1626276793/mongodb-atlas-02_ql4awq.png 'MongoDB Atlas Node.js connection')

You should have a connection string like below. Replace the username, password and database name with your credentials.

```bash
mongodb+srv://<username>:<password>@cluster0.tyqyw.mongodb.net/myFirstDatabase?retryWrites=true&w=majority
```

The next step is to create a database and a collection see the screenshots below. Click on the **Add My Own Data** button then create a database and collection called **dashboard**.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1626278491/database-create-01_ldkigr.png](https://res.cloudinary.com/d74fh3kw/image/upload/v1626278491/database-create-01_ldkigr.png 'Add your own data')

![https://res.cloudinary.com/d74fh3kw/image/upload/v1626278491/database-create-02_bgydbb.png](https://res.cloudinary.com/d74fh3kw/image/upload/v1626278491/database-create-02_bgydbb.png 'Create a database and a collection')

#### Local

Make sure that you have MongoDB and MongoDB compass installed locally and use the commands below in your BASH application to create a local database of your choosing.

```bash
mongo
show dbs;
use dashboard;
db.createCollection("users");
```

Now open the MongoDB Compass app and you should be able to see the database that you created. You can use either the MongoDB Compass app or the terminal to manage and view the database. To connect to the database you will use the connection string below.

```bash
mongodb://127.0.0.1:27017/dashboard
```

### Connecting the back-end to the MongoDB Database

The next thing that we need to do is create the back-end and connect it to a MongoDB database so that we have the functionality to create user accounts.

Create a folder on your desktop or in a directory of your choice called **dashboard-app**. `cd` into the folder and run the commands below in your BASH application to setup your project.

```bash
mkdir backend
touch .gitignore
cd backend
npm init -y
mkdir controllers middlewares models routes
touch index.js .gitignore .env
touch controllers/user.js
touch middlewares/requireAuth.js
touch models/User.js
touch routes/user.js
```

Now it is time to install some packages you should be in the **backend** folder so run the commands below.

```bash
npm i axios bcrypt cors dotenv ejs express jsonwebtoken mongoose nodemon concurrently
```

Next open the project in your code editor and add the code below to their corresponding files.

**index.js**

```javascript
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
require('dotenv').config();
const userRoute = require('./routes/user');

const app = express();

app.use(cors());

app.use(express.urlencoded({ extended: false }));
app.use(express.json());

app.use('/', userRoute);

const port = process.env.PORT || 8080;

mongoose
	.connect(process.env.DB_HOST, {
		useCreateIndex: true,
		useFindAndModify: false,
		useNewUrlParser: true,
		useUnifiedTopology: true,
	})
	.then(() => {
		app.listen(port, () => console.log(`Server and database running on ${port}, http://localhost:${port}`));
	})
	.catch((err) => {
		console.log(err);
	});
```

**.env**

Put your environment variables in here, the secret can be anything you want it to be just make sure that it is secure. I used a random string of alphanumeric characters.

```bash
DB_HOST="mongodb://127.0.0.1:27017/dashboard"
DB_HOST_ONLINE="mongodb+srv://username:password@cluster0.tyqyw.mongodb.net/dashboard?retryWrites=true&w=majority"
SECRET="mG7m2ZtprtU9aY3r"
```

If you choose to use **DB_HOST_ONLINE** make sure that you update it in the `index.js` file in connect.

```javascript
mongoose.connect(process.env.DB_HOST, {
	useCreateIndex: true,
	useFindAndModify: false,
	useNewUrlParser: true,
	useUnifiedTopology: true,
});
```

**.gitignore**
Add this code to the `.gitignore` files in the root and **backend** folders.

```bash
node_modules
.env
.DS_STORE
```

**controllers/user.js**

```javascript
const jwt = require('jsonwebtoken');
const User = require('../models/User');
require('dotenv').config();

exports.getAddUser = (req, res) => {
	res.render('add-user');
};

exports.postAddUser = async (req, res) => {
	const { email, password } = req.body;

	try {
		const user = new User({ email, password });
		await user.save();
		const token = jwt.sign({ userId: user._id }, `${process.env.SECRET}`);
		res.send({ token: token });
		console.log('User Added with token:', token);
	} catch (error) {
		console.log(error.message);
		return res.status(422).send(error.message);
	}
};

exports.getUser = (req, res) => {
	res.send(`Your email: ${req.user.email}`);
};

exports.postSignIn = async (req, res) => {
	const { email, password } = req.body;
	if (!email || !password) {
		return res.status(422).send({ error: 'Must provide email and password' });
	}
	const user = await User.findOne({ email });
	if (!user) {
		return res.status(404).send({ error: 'Email not found' });
	}

	try {
		await user.comparePassword(password);
		const token = jwt.sign({ userId: user._id }, `${process.env.SECRET}`);
		res.send({ token });
	} catch (err) {
		return res.status(422).send({ error: 'Invalid password or email' });
	}
};
```

**middlewares/requireAuth.js**

```javascript
const jwt = require('jsonwebtoken');
const mongoose = require('mongoose');
const User = mongoose.model('User');
require('dotenv').config();

module.exports = (req, res, next) => {
	const { authorization } = req.headers;

	if (!authorization) {
		return res.status(401).send({ error: 'You must be logged in.' });
	}

	const token = authorization.replace('Bearer ', '');
	jwt.verify(token, `${process.env.SECRET}`, async (err, payload) => {
		if (err) {
			return res.status(401).send({ error: 'You must be logged in.' });
		}
		const { userId } = payload;

		const user = await User.findById(userId);
		req.user = user;
		next();
	});
};
```

**models/User.js**

```javascript
const mongoose = require('mongoose');
const bcrypt = require('bcrypt');

const UserSchema = mongoose.Schema({
	email: {
		type: String,
		unique: true,
		requried: true,
	},
	password: {
		type: String,
		required: true,
	},
});

UserSchema.pre('save', function (next) {
	const user = this;
	if (!user.isModified('password')) {
		return next();
	}
	bcrypt.genSalt(10, (err, salt) => {
		if (err) {
			return next(err);
		}
		bcrypt.hash(user.password, salt, (err, hash) => {
			if (err) {
				return next(err);
			}
			user.password = hash;
			next();
		});
	});
});

UserSchema.methods.comparePassword = function (candidatePassword) {
	const user = this;

	return new Promise((resolve, reject) => {
		bcrypt.compare(candidatePassword, user.password, (err, isMatch) => {
			if (err) {
				return reject(err);
			}
			if (!isMatch) {
				return reject(false);
			}
			resolve(true);
		});
	});
};

module.exports = mongoose.model('User', UserSchema);
```

**routes/user.js**

```javascript
const express = require('express');
const userController = require('../controllers/user');
const requireAuth = require('../middlewares/requireAuth');

const router = express.Router();

// requireAuth is used to give authentication to different routes which means that they cant be accessed without a JWT Token

router.post('/signup', userController.postAddUser);

router.post('/signin', userController.postSignIn);

module.exports = router;
```

**package.json**

Add these run scripts to the `package.json` file.

```bash
	"scripts": {
		"test": "echo \"Error: no test specified\" && exit 1",
		"start": "node index.js",
		"dev": "nodemon index.js",
		"servers": "concurrently \"npm run start\" \" cd ../frontend && yarn start \""
	},
```

Now if you run the command `npm run dev` from the **backend** folder you should have a working backend that connects to your MongoDB database.

What we did was create a database that can store users emails and passwords. The passwords are hashed and encrypted so that they are not stored in plain text which would make it easy for malicious users to steal. We will be using JWT tokens to verify that users are who they claim to be and that they have an account which will let them sign up and sign into their accounts. There is a route in the backend for signing up and signing in users which returns a JWT token if the details are correct.

### Using the Postman API app to test the routes

Next open Postman or whatever API testing tool that you prefer to use.

**Signup Route**

Create a user and do a POST request take a look at the image below to see an example of it working. As you can see a token is returned once a user has successfully signed up for an account.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1626275292/dashboard-app-signup_no74vv.png](https://res.cloudinary.com/d74fh3kw/image/upload/v1626275292/dashboard-app-signup_no74vv.png 'Signup Route')

The user can be seen in the MongoDB database via the MongoDB Compass app.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1626275292/dashboard-app-mongodb-user_guyikd.png](https://res.cloudinary.com/d74fh3kw/image/upload/v1626275292/dashboard-app-mongodb-user_guyikd.png 'MongoDB Compass')

**Signin Route**

Now try to sign in using the user that you just created. You will need the email, password and also the JWT token see below for examples of how it should look.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1626275292/dashboard-app-signin-01_vm3mtf.png](https://res.cloudinary.com/d74fh3kw/image/upload/v1626275292/dashboard-app-signin-01_vm3mtf.png 'Sign in with email and password')

![https://res.cloudinary.com/d74fh3kw/image/upload/v1626275827/dashboard-app-signin-02_iohjkj.png](https://res.cloudinary.com/d74fh3kw/image/upload/v1626275827/dashboard-app-signin-02_iohjkj.png 'Sign in using the JWT Token')

## Building the front-end

### Doing the initial setup

Now its time to create the React Native front-end. We will be using the Expo CLI tool. Make sure that you are in the root folder for the project and then run the command below. Choose a blank template and continue the setup.

```bash
npx expo-cli init frontend
```

`cd` into the **frontend** folder and then install the dependencies below using your BASH application.

```bash
yarn add react-navigation react-navigation-stack @react-native-community/masked-view react-navigation-tabs axios react-native-elements @react-native-async-storage/async-storage
```

```bash
expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view
```

Next `cd` into the **backend** folder and run the command below to start the back-end and front-end together.

```bash
npm run servers
```

You should see links and a QR code for opening the Expo CLI developer tools. Open it in a browser window and then choose either a device or simulator to get it running.

### Creating the front-end

Use your BASH application to `cd` into the **frontend** folder. Run the command below to setup the project.

```bash
mkdir src
cd src
touch navigationRef.js
mkdir api components context screens
touch api/users.js
touch components/AuthForm.js components/NavLink.js
touch context/AuthContext.js context/createDataContext.js
touch screens/AccountScreen.js screens/DashboardScreen.js screens/ProfileScreen.js screens/ResolveAuthScreen.js screens/SigninScreen.js screens/SignupScreen.js
```

When you have completed that step the next thing that you need to do is add the correct code to each corresponding file. Add the code below to each file in the directory.

**api/users.js**

```jsx
import axios from 'axios';

export default axios.create({
	baseURL: 'http://localhost:8080/',
});
```

**components/AuthForm.js**

```jsx
import React, { useState } from 'react';
import { StyleSheet } from 'react-native';
import { Text, Button, Input } from 'react-native-elements';

const AuthForm = ({ headerText, errorMessage, onSubmit, submitButtonText }) => {
	const [email, setEmail] = useState('');
	const [password, setPassword] = useState('');

	return (
		<>
			<Text h3 style={styles.gridSpace}>
				{headerText}
			</Text>

			<Input label="Email" value={email} onChangeText={setEmail} autoCapitalize="none" autoCorrect={false} />

			<Input
				secureTextEntry
				label="Password"
				value={password}
				onChangeText={setPassword}
				autoCapitalize="none"
				autoCorrect={false}
			/>
			{errorMessage ? <Text style={styles.errorMessage}>{errorMessage}</Text> : null}

			<Button
				style={styles.gridSpace}
				buttonStyle={styles.btn}
				title={submitButtonText}
				onPress={() => onSubmit({ email, password })}
			/>
		</>
	);
};

const styles = StyleSheet.create({
	errorMessage: {
		fontSize: 16,
		color: 'red',
		marginLeft: 15,
		marginTop: 15,
	},
	btn: {
		backgroundColor: '#6203BF',
	},
	gridSpace: {
		margin: 15,
		textAlign: 'center',
		fontWeight: 'bold',
	},
});

export default AuthForm;
```

**components/NavLink.js**

```jsx
import React from 'react';
import { Text, TouchableOpacity, StyleSheet } from 'react-native';
import { withNavigation } from 'react-navigation';

const NavLink = ({ navigation, text, routeName }) => {
	return (
		<TouchableOpacity style={styles.gridSpace} onPress={() => navigation.navigate(routeName)}>
			<Text style={styles.link}>{text}</Text>
		</TouchableOpacity>
	);
};

const styles = StyleSheet.create({
	link: {
		color: '#1639ff',
	},
	gridSpace: {
		margin: 15,
	},
});

export default withNavigation(NavLink);
```

**context/AuthContext.js**

```jsx
import AsyncStorage from '@react-native-async-storage/async-storage';
import createDataContext from './createDataContext';
import usersAPI from '../api/users';
import { navigate } from '../navigationRef';

const authReducer = (state, action) => {
	switch (action.type) {
		case 'add_error':
			return { ...state, errorMessage: action.payload };
		case 'signin':
			return { errorMessage: '', token: action.payload };
		case 'clear_error_message':
			return { ...state, errorMessage: '' };
		case 'signout':
			return { token: null, errorMessage: '' };
		default:
			return state;
	}
};

const tryLocalSignin = (dispatch) => async () => {
	const token = await AsyncStorage.getItem('token');
	if (token) {
		dispatch({ type: 'signin', payload: token });
		navigate('Dashboard');
	} else {
		navigate('Signup');
	}
};

const clearErrorMessage = (dispatch) => () => {
	dispatch({ type: 'clear_error_message' });
};

const signup =
	(dispatch) =>
	async ({ email, password }) => {
		try {
			const response = await usersAPI.post('/signup', { email, password });
			await AsyncStorage.setItem('token', response.data.token);
			dispatch({ type: 'signin', payload: response.data.token });
			navigate('Dashboard');
		} catch (err) {
			dispatch({
				type: 'add_error',
				payload: 'There was an error with the sign up please try again',
			});
		}
	};

const signin =
	(dispatch) =>
	async ({ email, password }) => {
		try {
			const response = await usersAPI.post('/signin', { email, password });
			await AsyncStorage.setItem('token', response.data.token);
			dispatch({ type: 'signin', payload: response.data.token });

			navigate('Dashboard');
		} catch (err) {
			dispatch({
				type: 'add_error',
				payload: 'There was an error with the sign in please try again',
			});
		}
	};

const signout = (dispatch) => async () => {
	await AsyncStorage.removeItem('token');
	dispatch({ type: 'signout' });
	navigate('loginFlow');
};

export const { Provider, Context } = createDataContext(
	authReducer,
	{ signin, signout, signup, clearErrorMessage, tryLocalSignin },
	{ token: null, errorMessage: '' }
);
```

**context/createDataContext.js**

```jsx
import React, { useReducer } from 'react';

export default (reducer, actions, defaultValue) => {
	const Context = React.createContext();

	const Provider = ({ children }) => {
		const [state, dispatch] = useReducer(reducer, defaultValue);

		const boundActions = {};
		for (let key in actions) {
			boundActions[key] = actions[key](dispatch);
		}

		return <Context.Provider value={{ state, ...boundActions }}>{children}</Context.Provider>;
	};

	return { Context, Provider };
};
```

**screens/AccountScreen.js**

```jsx
import React, { useContext } from 'react';
import { StyleSheet, Text } from 'react-native';
import { Button } from 'react-native-elements';
import { SafeAreaView } from 'react-navigation';
import { Context as AuthContext } from '../context/AuthContext';

const AccountScreen = () => {
	const { signout } = useContext(AuthContext);

	return (
		<SafeAreaView forceInset={{ top: 'always' }}>
			<Text style={styles.container}>Account</Text>

			<Button buttonStyle={styles.btn} title="Sign Out" onPress={signout} />
		</SafeAreaView>
	);
};

const styles = StyleSheet.create({
	btn: {
		backgroundColor: '#6203BF',
		margin: 15,
	},
	container: {
		margin: 30,
		fontSize: 48,
		textAlign: 'center',
	},
});

export default AccountScreen;
```

**screens/DashboardScreen.js**

```jsx
import React, { useContext } from 'react';
import { StyleSheet, View, Text } from 'react-native';

const DashboardScreen = () => {
	return (
		<>
			<View>
				<Text style={styles.container}>Dashboard</Text>
				<View style={styles.contentContainer}>
					<Text style={styles.welcome}>Welcome 🎉</Text>
				</View>
			</View>
		</>
	);
};

const styles = StyleSheet.create({
	container: {
		margin: 50,
		fontSize: 48,
		textAlign: 'center',
	},
	contentContainer: {
		justifyContent: 'center',
		alignItems: 'center',
	},
	welcome: {
		margin: 50,
	},
});

export default DashboardScreen;
```

**screens/ProfileScreen.js**

```jsx
import React from 'react';
import { StyleSheet, View, Text } from 'react-native';

const ProfileScreen = () => {
	return (
		<>
			<View>
				<Text style={styles.container}>Profile</Text>
				<View style={styles.contentContainer}>
					<View style={styles.profilePicture}></View>
				</View>
			</View>
		</>
	);
};

const styles = StyleSheet.create({
	container: {
		margin: 50,
		fontSize: 48,
		textAlign: 'center',
	},
	contentContainer: {
		justifyContent: 'center',
		alignItems: 'center',
	},
	profilePicture: {
		width: 200,
		height: 200,
		borderRadius: 100,
		backgroundColor: 'grey',
	},
});

export default ProfileScreen;
```

**screens/ResolveAuthScreen.js**

```jsx
import { useEffect, useContext } from 'react';
import { Context as AuthContext } from '../context/AuthContext';

const ResolveAuthScreen = () => {
	const { tryLocalSignin } = useContext(AuthContext);

	useEffect(() => {
		tryLocalSignin();
	}, []);

	return null;
};

export default ResolveAuthScreen;
```

**screens/SigninScreen.js**

```jsx
import React, { useContext } from 'react';
import { View, StyleSheet } from 'react-native';
import { NavigationEvents } from 'react-navigation';
import AuthForm from '../components/AuthForm';
import NavLink from '../components/NavLink';
import { Context } from '../context/AuthContext';

const SigninScreen = () => {
	const { state, signin, clearErrorMessage } = useContext(Context);
	return (
		<View style={styles.container}>
			<NavigationEvents onWillFocus={clearErrorMessage} />
			<AuthForm headerText="Sign In" errorMessage={state.errorMessage} onSubmit={signin} submitButtonText="Sign In" />
			<NavLink text="If you don't have an account then sign up" routeName="Signup" />
		</View>
	);
};

SigninScreen.navigationOptions = () => {
	return {
		headerShown: false,
	};
};

const styles = StyleSheet.create({
	container: {
		flex: 1,
		justifyContent: 'center',
		marginBottom: 250,
	},
});

export default SigninScreen;
```

**screens/SignupScreen.js**

```jsx
import React, { useContext } from 'react';
import { View, StyleSheet } from 'react-native';
import { NavigationEvents } from 'react-navigation';
import { Context as AuthContext } from '../context/AuthContext';
import AuthForm from '../components/AuthForm';
import NavLink from '../components/NavLink';

const SignupScreen = () => {
	const { state, signup, clearErrorMessage } = useContext(AuthContext);

	return (
		<View style={styles.container}>
			<NavigationEvents onWillFocus={clearErrorMessage} />
			<AuthForm headerText="Sign Up" errorMessage={state.errorMessage} submitButtonText="Sign Up" onSubmit={signup} />
			<NavLink routeName="Signin" text="If you already have an account then sign in!" />
		</View>
	);
};

SignupScreen.navigationOptions = () => {
	return {
		header: () => false,
	};
};

const styles = StyleSheet.create({
	container: {
		flex: 1,
		justifyContent: 'center',
		marginBottom: 250,
	},
});

export default SignupScreen;
```

**navigationRef.js**

```jsx
import { NavigationActions } from 'react-navigation';

let navigator;

export const setNavigator = (nav) => {
	navigator = nav;
};

export const navigate = (routeName, params) => {
	navigator.dispatch(
		NavigationActions.navigate({
			routeName,
			params,
		})
	);
};
```

**App.js**

Replace all of the code in the `App.js` file with the code below.

```jsx
import React from 'react';
import { createAppContainer, createSwitchNavigator } from 'react-navigation';
import { createStackNavigator } from 'react-navigation-stack';
import { createBottomTabNavigator } from 'react-navigation-tabs';
import AccountScreen from './src/screens/AccountScreen';
import SigninScreen from './src/screens/SigninScreen';
import SignupScreen from './src/screens/SignupScreen';
import ProfileScreen from './src/screens/ProfileScreen';
import DashboardScreen from './src/screens/DashboardScreen';
import { Provider as AuthProvider } from './src/context/AuthContext';
import { setNavigator } from './src/navigationRef';
import ResolveAuthScreen from './src/screens/ResolveAuthScreen';

const switchNavigator = createSwitchNavigator({
	ResolveAuth: ResolveAuthScreen,
	loginFlow: createStackNavigator({
		Signup: SignupScreen,
		Signin: SigninScreen,
	}),
	mainFlow: createBottomTabNavigator({
		Dashboard: DashboardScreen,
		Profile: ProfileScreen,
		Account: AccountScreen,
	}),
});

const App = createAppContainer(switchNavigator);

export default () => {
	return (
		<AuthProvider>
			<App
				ref={(navigator) => {
					setNavigator(navigator);
				}}
			/>
		</AuthProvider>
	);
};
```

Ok that was a lot of code! It is highly likely that you are going to have to restart everything to see it working. So go back into the backend folder and run the command again to run both servers. If you are using a simulator then you will have to close it and then run a new one to see the new changes.

```bash
npm run servers
```

Assuming everything went well you should have a working back-end and front-end which will allow you to sign up, sign in and sign out.
