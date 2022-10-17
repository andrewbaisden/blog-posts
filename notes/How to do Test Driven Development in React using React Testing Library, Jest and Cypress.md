## What is Test Driven Development?

Test Driven Development or TDD for short is essentially a process that developers and teams go through when they are testing their code. Coding, design and testing are combined together and test cases are created to ensure that the code has been robustly tested and any bugs or errors have been resolved in the development phase prior to it reaching production level.

This is considered to be good practice and a methodology that all developers should be following when they are working on a codebase. Through this process the code improves over time leading to a much more stable application. In this article we will look at Unit Tests, Integration Tests and End-To-End Tests.

### What are Unit Tests?

Basically a Unit Test is a method of testing small samples of code within an application. This can include functions that run code blocks or API's which return data. The goal is to find out if the code is working properly and if it is catching any errors when they occur. Like for example incorrect data getting returned in a form.

### What are Integration Tests?

Integration Tests are pretty much just multiple Unit Tests grouped together. So whereas a single Unit Test would test one piece of functionality an Integration Test is more like a test suite. So in a sense you are now testing multiple code blocks at the same time like for example an entire carousel component. If it was a Unit Test then you would only be testing to see if an image was loading whereas in an Integration Test you are now testing to see if the title is loading, image is loading, and the correct data is showing up etc... Integration tests are great for testing user flows.

### What are End-To-End Tests?

End-End Tests are a way to test an applications frontend workflow. It is a method to test the whole application so that you know it's going to behave the way you expect it to. The difference between End-To-End testing and the other two is that End-To-End testing tests the software and the system whereas the other two are more for systematic testing.

### How to do testing?

Jest and React Testing Library are extremely popular when it comes to doing Unit and Integration tests in the command line. Cypress is a popular tool for doing End-To-End testing in the browser. Jest can even be used on the backend so you can cover all your bases and use the same library for backend and frontend testing work.

**Unit Test/Integration Test libraries**

- [Jest](https://jestjs.io/)
- [React Testing Library](https://testing-library.com/)

**End-To-End Test libraries**

- [Cypress](https://www.cypress.io/)

## Project Setup

Let's setup our project. Navigate to a directory on your computer open up the command line and run the commands below.

```shell
npx create-react-app tdd-react-cypress-app
cd tdd-react-cypress-app
npm install cypress @testing-library/cypress --save-dev
mkdir src/components
mkdir src/components/{Form,Header,Profile,ProfileDetails,Sidebar}
touch src/components/Form/{Form.js,Form.test.js,Form.css}
touch src/components/Header/{Header.js,Header.test.js,Header.css}
touch src/components/Profile/{Profile.js,Profile.test.js,Profile.css}
touch src/components/ProfileDetails/{ProfileDetails.js,ProfileDetails.test.js,ProfileDetails.css}
touch src/components/Sidebar/{Sidebar.js,Sidebar.test.js,Sidebar.css}
```

Now run this command to start Cypress you should see a Cypress window open on your computer.

```shell
# To start Cypress
npx cypress open
```

There are lots of example integration tests if you want you can run them to see what they do. When you are ready open the project in your code editor, go inside of your project and find the Cypress integration folder at `my-app/cypress/integration` and delete the folders inside of it so we have a clean slate.

Then create a file called `user.spec.js` and put it inside of the **integration** folder with the code below. This will be out first End-To-End test but its not going to work yet because our application has no code!

```javascript
describe('user form flow', () => {
	beforeEach(() => {
		cy.viewport(1600, 900);
		cy.visit('http://localhost:3000/');
	});

	it('user can save form', () => {
		// save form data

		cy.get('input[name="firstName"]').type('Eren');

		cy.get('input[name="lastName"]').type('Yeager');

		cy.get('input[name="email"]').type('erenyeager@gmail.com');

		cy.get('input[name="career"]').type('Attack Titan');

		cy.get('textarea[name="bio"]').type('Hello there my name is Eren Yeager!');

		cy.get('input[name="save"]').click();
	});
});
```

It's finally time to add the code to the files we created earlier. Copy and paste the code below into their corresponding files. It's quite a tedious process because they are separated into components but it will be worth it in the end.

Alternatively you can just clone/download the repo and skip to the end of this article which is the __Unit Tests and Integration Tests__ section.

[https://github.com/andrewbaisden/tdd-react-cypress-app](https://github.com/andrewbaisden/tdd-react-cypress-app)

### App Component Files

`App.css`

```css
@import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@400;500;700&display=swap');

*,
*::before,
*::after {
	padding: 0;

	margin: 0;

	box-sizing: 0;
}

html {
	font-size: 16px;
}

body {
	font-family: 'Quicksand', sans-serif;

	font-size: 1.6rem;

	color: #2d2d2d;

	background: #b3b3b3
		url('https://images.unsplash.com/photo-1506905925346-21bda4d32df4?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2670&q=80');
}

.container {
	margin: 2rem auto;

	display: flex;

	flex-flow: row nowrap;

	width: 100%;

	height: 50rem;

	max-width: 100rem;
}

main {
	width: 100%;

	max-width: 60rem;
}
```

`App.js`

```javascript
import Sidebar from './components/Sidebar/Sidebar';

import Header from './components/Header/Header';

import Profile from './components/Profile/Profile';

import './App.css';

const App = () => {
	return (
		<>
			<div data-testid="container" className="container">
				<Sidebar />

				<main>
					<Header />

					<Profile />
				</main>
			</div>
		</>
	);
};

export default App;
```

`App.test.js`

```javascript
import { render, screen } from '@testing-library/react';

import App from './App';

describe('<App />', () => {
	it('has a container div', () => {
		render(<App />);

		const el = screen.getByTestId('container');

		expect(el.className).toBe('container');
	});
});
```

### Form Component Files

`Form.css`

```css
.profile-details-form-container {
	margin-top: 2rem;

	display: flex;

	flex-flow: column nowrap;
}

.profile-details-form-container input {
	width: 100%;

	height: 2rem;

	padding: 0.5rem;

	font-size: 1.3rem;
}

.profile-details-form-container label {
	width: 100%;
}

.profile-details-form-container textarea {
	width: 100%;

	height: 5rem;

	resize: none;

	padding: 0.5rem;

	font-size: 1.3rem;
}

input[type='submit'] {
	border: none;

	background: #7e7dd6;

	color: #ffffff;

	font-weight: 600;

	width: 8rem;

	border-radius: 0.2rem;

	cursor: pointer;

	font-size: 1rem;
}

.form-output {
	margin-top: 1rem;

	width: 40rem;

	font-weight: 600;

	font-size: 0.8rem;
}
```

`Form.js`

```javacript
import { useState } from 'react';

import './Form.css';



const Form = () => {

const [firstName, setFirstName] = useState('');

const [lastName, setLastName] = useState('');

const [email, setEmail] = useState('');

const [career, setCareer] = useState('');

const [bio, setBio] = useState('');

const [data, setData] = useState('');



const formSubmit = (e) => {

e.preventDefault();



const user = {

firstName: firstName,

lastName: lastName,

email: email,

career: career,

bio: bio,

};



const formData = JSON.stringify(user);



console.log(formData);

setData(formData);

clearForm();

};



const clearForm = () => {

setFirstName('');

setLastName('');

setEmail('');

setCareer('');

setBio('');

};



return (

<>

<div>

<form onSubmit={formSubmit} className="profile-details-form-container">

<div>

<label data-testid="firstname">First Name</label>

<input

type="text"

name="firstName"

value={firstName}

onChange={(e) => setFirstName(e.target.value)}

placeholder="First Name"

/>

</div>

<div>

<label data-testid="lastname">Last Name</label>

<input

type="text"

name="lastName"

value={lastName}

onChange={(e) => setLastName(e.target.value)}

placeholder="Last Name"

/>

</div>

<div>

<label data-testid="email">Email</label>

<input

type="text"

name="email"

value={email}

onChange={(e) => setEmail(e.target.value)}

placeholder="Email"

/>

</div>

<div>

<label data-testid="career">Career</label>

<input

type="text"

name="career"

value={career}

onChange={(e) => setCareer(e.target.value)}

placeholder="Career"

/>

</div>

<div>

<label data-testid="bio">Bio</label>

<textarea name="bio" value={bio} onChange={(e) => setBio(e.target.value)} placeholder="Bio"></textarea>

</div>

<div>

<input name="save" type="submit" value="Save" />

</div>

</form>

<div className="form-output">

<p>Output</p>

<div>{data}</div>

</div>

</div>

</>

);

};



export default Form;
```

`Form.test.js`

```javacript
import { render, screen } from '@testing-library/react';

import Form from './Form';



describe('<Form />', () => {

it('has a first name label', () => {

render(<Form />);

const el = screen.getByTestId('firstname');

expect(el.innerHTML).toBe('First Name');

});

it('has a last name label', () => {

render(<Form />);

const el = screen.getByTestId('lastname');

expect(el.innerHTML).toBe('Last Name');

});

it('has a email label', () => {

render(<Form />);

const el = screen.getByTestId('email');

expect(el.innerHTML).toBe('Email');

});

it('has a career label', () => {

render(<Form />);

const el = screen.getByTestId('career');

expect(el.innerHTML).toBe('Career');

});

it('has a bio label', () => {

render(<Form />);

const el = screen.getByTestId('bio');

expect(el.innerHTML).toBe('Bio');

});

});
```

`Header.css`

```css
header {
	background: #ffffff;

	display: flex;

	flex-flow: row nowrap;

	justify-content: space-between;

	padding: 1rem;

	border-bottom: 0.1rem solid rgb(234, 234, 234);
}

.page-title,
.page-info {
	display: flex;

	flex-flow: row nowrap;

	justify-content: center;

	align-items: center;
}

.page-title h1 {
	font-size: 2rem;
}

.page-info {
	display: flex;

	flex-flow: row nowrap;

	justify-content: space-around;

	max-width: 15rem;

	width: 100%;
}

.page-info button {
	border: none;

	background: #7e7dd6;

	color: #ffffff;

	padding: 1rem;

	border-radius: 0.5rem;

	font-weight: 600;

	cursor: pointer;
}

.secure,
.notifications {
	display: flex;

	flex-flow: row nowrap;

	justify-content: center;

	align-items: center;

	border: 0.2rem solid rgb(233, 233, 233);

	padding: 0.5rem;

	height: 2rem;

	border-radius: 0.5rem;
}
```

`Header.js`

```javascript
import './Header.css';

const Header = () => {
	return (
		<>
			<header>
				<div className="page-title">
					<h1 data-testid="info">Information</h1>

					<div>📝</div>
				</div>

				<div className="page-info">
					<div className="secure">🛡</div>

					<div role="alert" className="notifications">
						🔔
					</div>

					<button data-testid="confirm-btn">Confirm</button>
				</div>
			</header>
		</>
	);
};

export default Header;
```

`Header.test.js`

```javascript
import { screen, render } from '@testing-library/react';

import Header from './Header';

describe('<Header />', () => {
	it('has a title h1', () => {
		render(<Header />);

		const el = screen.getByTestId('info');

		expect(el.innerHTML).toBe('Information');
	});

	it('has a notification div', () => {
		render(<Header />);

		const el = screen.getByRole('alert');
	});

	it('has a confirm button', () => {
		render(<Header />);

		const el = screen.getByTestId('confirm-btn');

		expect(el.innerHTML).toBe('Confirm');
	});
});
```

`Profile.css`

```css
.profile-container {
	display: flex;

	flex-flow: row nowrap;

	justify-content: space-between;

	padding: 1rem;

	background: #ffffff;
}

.profile-container section {
	margin: 1rem;
}

.profile-container h1 {
	font-size: 1.5rem;
}

.profile-container p {
	font-size: 1.3rem;
}
```

`Profile.js`

```javascript
import Form from '../Form/Form';

import ProfileDetails from '../ProfileDetails/ProfileDetails';

import './Profile.css';

const Profile = () => {
	return (
		<>
			<div className="profile-container">
				<section>
					<article>
						<h1 data-testid="user-profile">User Profile</h1>

						<p>Fill in your user details in the form below.</p>
					</article>

					<Form />
				</section>

				<section>
					<ProfileDetails />
				</section>
			</div>
		</>
	);
};

export default Profile;
```

`Profile.test.js`

```javascript
import { screen, render } from '@testing-library/react';

import Profile from './Profile';

describe('<Profile />', () => {
	it('has a heading', () => {
		render(<Profile />);

		const el = screen.getByText(/User Profile/i);

		expect(el).toBeTruthy();
	});
});
```

`ProfileDetails.css`

```css
.profile-details-container {
	width: 20rem;
}

.profile-details-container p {
	font-size: 1rem;

	font-weight: 600;

	margin-top: 1rem;
}

.profile-details-container form label {
	font-size: 1rem;

	margin-left: 1rem;
}

.profile-details-image {
	display: flex;

	flex-flow: column nowrap;

	align-items: flex-start;
}

.profile-details-image h1 {
	font-size: 1.2rem;

	margin-bottom: 1rem;
}

.profile-details-image div {
	background: #7e7dd6;

	border-radius: 100%;

	height: 5rem;

	width: 5rem;

	display: flex;

	flex-flow: row nowrap;

	justify-content: center;

	align-items: center;
}
```

`ProfileDetails.js`

```javascript
import './ProfileDetails.css';

const ProfileDetails = () => {
	return (
		<>
			<div className="profile-details-container">
				<div className="profile-details-image">
					<h1>Profile Photo</h1>

					<div>😎</div>
				</div>

				<p>Select your gender</p>

				<form>
					<div>
						<input type="radio" id="male" name="male" value="Male" />

						<label htmlFor="male">Male</label>

						<br />
					</div>

					<div>
						<input type="radio" id="male" name="male" value="Male" />

						<label htmlFor="female">Female</label>

						<br />
					</div>

					<div>
						<input type="radio" id="male" name="male" value="Male" />

						<label htmlFor="nonBinary">Non-binary</label>

						<br />
					</div>
				</form>
			</div>
		</>
	);
};

export default ProfileDetails;
```

`ProfileDetails.test.js`

```javascript
import { screen, render } from '@testing-library/react';

import ProfileDetails from './ProfileDetails';

describe('<ProfileDetails />', () => {
	it('has a gender select heading', () => {
		render(<ProfileDetails />);

		const el = screen.getByText(/Select your gender/i);

		expect(el).toBeTruthy();
	});
});
```

`Sidebar.css`

```css
aside {
	background-color: rgba(255, 255, 255, 0.15);

	backdrop-filter: blur(10px);

	padding: 2rem;

	width: 100%;

	max-width: 16rem;

	border-top-left-radius: 8px;

	border-bottom-left-radius: 8px;

	height: 43.4rem;
}

.profile-sidebar-container {
	display: flex;

	flex-flow: row nowrap;

	justify-content: space-between;
}

.profile-image {
	background: #7e7dd6;

	border-radius: 100%;

	padding: 1rem;

	height: 2rem;
}

.profile-user p {
	font-size: 1rem;
}

.profile-user h1 {
	font-size: 1.6rem;
}

.settings {
	display: flex;

	flex-flow: row nowrap;

	justify-content: center;

	align-items: center;

	background: #ffffff;

	padding: 0.5rem;

	height: 2rem;

	width: 2rem;

	border-radius: 0.5rem;

	border: none;

	cursor: pointer;
}

aside {
	display: flex;

	flex-flow: column nowrap;

	justify-content: space-between;
}

aside nav,
.support-log-out {
	display: flex;

	flex-flow: column nowrap;
}

aside nav a,
.support-log-out a {
	color: rgb(43, 43, 43);

	text-decoration: none;

	font-weight: 600;

	padding: 0.4rem;

	border-radius: 0.2rem;
}

aside nav a:hover,
.support-log-out a:hover {
	background-color: #ffffff;
}
```

`Sidebar.js`

```javascript
import './Sidebar.css';

const Sidebar = () => {
	return (
		<>
			<aside>
				<div className="profile-sidebar-container">
					<div className="profile-image">😎</div>

					<div className="profile-user">
						<p>Welcome back,</p>

						<h1>Eren Yeager</h1>
					</div>

					<button className="settings">⚙️</button>
				</div>

				<nav>
					<a href="/" data-testid="search">
						🔍 Search
					</a>

					<a href="/" data-testid="dashboard">
						🏠 Dashboard
					</a>

					<a href="/" data-testid="assets">
						💷 Assets
					</a>

					<a href="/" data-testid="business">
						💼 Business
					</a>

					<a href="/" data-testid="data">
						📈 Data
					</a>

					<a href="/" data-testid="backups">
						🛠 Backups
					</a>
				</nav>

				<div className="support-log-out">
					<a href="/" data-testid="support">
						💬 Support
					</a>

					<a href="/" data-testid="log-out">
						⇥ Log Out
					</a>
				</div>
			</aside>
		</>
	);
};

export default Sidebar;
```

`Sidebar.test.js`

```javascript
import { screen, render } from '@testing-library/react';

import Sidebar from './Sidebar';

describe('<Sidebar />', () => {
	it('has a search link', () => {
		render(<Sidebar />);

		const el = screen.getByTestId('search');
	});

	it('has a dashboard link', () => {
		render(<Sidebar />);

		const el = screen.getByTestId('dashboard');
	});

	it('has a assets link', () => {
		render(<Sidebar />);

		const el = screen.getByTestId('assets');
	});

	it('has a business link', () => {
		render(<Sidebar />);

		const el = screen.getByTestId('business');
	});

	it('has a data link', () => {
		render(<Sidebar />);

		const el = screen.getByTestId('data');
	});

	it('has a backups link', () => {
		render(<Sidebar />);

		const el = screen.getByTestId('backups');
	});

	it('has a support link', () => {
		render(<Sidebar />);

		const el = screen.getByTestId('support');
	});

	it('has a log-out link', () => {
		render(<Sidebar />);

		const el = screen.getByTestId('log-out');
	});
});
```

Next run the commands below in your command line application but in different tabs/windows. So now you should have React, Jest and Cypress running at the same time. You might need to press __a__ or __enter__ to run all Jest tests.

```shell
# To start React
npm run start
```

```shell
# To start Jest
npm run test
```

```shell
# To start Cypress
npx cypress open
```

## Unit Tests and Integration Tests

You can find all of the example Unit and Integration Tests inside of the component folders. All of the tests should be passing you can play around with the files to see the tests fail and pass.

## End-To-End Tests

The End-To-End tests are inside of `my-app/cypress/integration/user.spec.js`. To run the tests go to the Cypress application window and click on the button to run the test. If you click on that dropdown menu that has Electron as an option you will be able to select different web browsers.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1651347203/cypress_w7gdrn.png](https://res.cloudinary.com/d74fh3kw/image/upload/v1651347203/cypress_w7gdrn.png)

The `user.spec.js` integration test automatically fills out the form and then the save button is clicked. A string version of the object that was created is output at the bottom of the page.

So lets do a quick recap you now know how to create:

- Unit Tests
- Integration Tests
- End-To-End Tests

This was just a quick introduction take a look at the official documentation for [Jest](https://jestjs.io/), [React Testing Library](https://testing-library.com/) and [Cypress](https://www.cypress.io/) to learn more.
