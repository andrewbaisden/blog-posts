# How to deploy a Python/Flask App to Vercel

This is just a quick simple example of course more complex applications will work as well.

## Prerequisites

**Step 1**

Create an account with [Vercel](https://vercel.com) if you don't already have one.

Vercel is a cloud platform for static sites and Serverless Functions that fits perfectly with your workflow. It enables developers to host Jamstack websites and web services that deploy instantly, scale automatically, and requires no supervision, all with no configuration.

**Step 2**

Use npm to install Vercel globally on your computer [https://www.npmjs.com/package/vercel](https://www.npmjs.com/package/vercel)

```bash
npm i -g vercel
```

**Step 3**

Make sure that you have the latest version of Python3 installed and the Flask framework with pip3

[https://pypi.org/project/Flask/](https://pypi.org/project/Flask/)

```bash
pip install Flask
```

## Setup the project

Create a project

If you are having problems getting the virtual environment to work then read this documentation [https://docs.python.org/3/library/venv.html](https://docs.python.org/3/library/venv.html)

```bash
mkdir vercel-python-app
cd vercel-python-app
python3 -m venv venv
. venv/bin/activate
cd venv
touch index.py
```

Open the project in your code editor and then create a Python/Flask server in the `index.py` file

```python
from flask import Flask


app = Flask(__name__)


@app.route('/')
def home():
    return 'Home Page Route'


@app.route('/about')
def about():
    return 'About Page Route'


@app.route('/portfolio')
def portfolio():
    return 'Portfolio Page Route'


@app.route('/contact')
def contact():
    return 'Contact Page Route'


@app.route('/api')
def api():
    with open('data.json', mode='r') as my_file:
        text = my_file.read()
        return text
```

Setup the development environment by running these commands in your terminal. 

```bash
export FLASK_APP=index.py   
export FLASK_ENV=development
```

If you are using Windows then see here for the environment variable syntax [https://flask.palletsprojects.com/en/1.1.x/quickstart/#a-minimal-application](https://flask.palletsprojects.com/en/1.1.x/quickstart/#a-minimal-application)

Now create a `data.json` file and put it in the root folder for `venv` and add the `.json` below into it

```json
[
	{
		"id": 1,
		"first_name": "Rene",
		"last_name": "Clemmett",
		"email": "rclemmett0@linkedin.com",
		"gender": "Male",
		"ip_address": "42.86.99.75"
	},
	{
		"id": 2,
		"first_name": "Rustie",
		"last_name": "Chrishop",
		"email": "rchrishop1@bloomberg.com",
		"gender": "Male",
		"ip_address": "197.128.10.252"
	},
	{
		"id": 3,
		"first_name": "Joe",
		"last_name": "Cocklie",
		"email": "jcocklie2@ustream.tv",
		"gender": "Male",
		"ip_address": "124.81.44.28"
	},
	{
		"id": 4,
		"first_name": "Diane",
		"last_name": "Catt",
		"email": "dcatt3@sogou.com",
		"gender": "Female",
		"ip_address": "169.47.61.184"
	},
	{
		"id": 5,
		"first_name": "Quinton",
		"last_name": "Shellsheere",
		"email": "qshellsheere4@icq.com",
		"gender": "Male",
		"ip_address": "2.57.97.184"
	},
	{
		"id": 6,
		"first_name": "Lena",
		"last_name": "Paull",
		"email": "lpaull5@tmall.com",
		"gender": "Female",
		"ip_address": "121.4.165.63"
	},
	{
		"id": 7,
		"first_name": "Corena",
		"last_name": "Lamswood",
		"email": "clamswood6@hud.gov",
		"gender": "Female",
		"ip_address": "78.65.53.3"
	},
	{
		"id": 8,
		"first_name": "Justinian",
		"last_name": "Nequest",
		"email": "jnequest7@virginia.edu",
		"gender": "Male",
		"ip_address": "62.24.98.224"
	},
	{
		"id": 9,
		"first_name": "Vladimir",
		"last_name": "Boeter",
		"email": "vboeter8@addthis.com",
		"gender": "Male",
		"ip_address": "87.119.34.255"
	},
	{
		"id": 10,
		"first_name": "Jillene",
		"last_name": "Eades",
		"email": "jeades9@amazon.de",
		"gender": "Female",
		"ip_address": "159.173.99.31"
	}
]
```

Run the command below to see your Python/Flask app working locally in the browser

```bash
flask run
```

## Deploying to Vercel

Make sure that you are in the root folder for your project so inside of the `venv` folder and then run the command `vercel` in your terminal. 

Use the project setup settings below as a guide to setup your own project with Vercel.

```bash
? Set up and deploy “~/Desktop/username/vercel-python-app/venv”? [Y/n] y
? Which scope do you want to deploy to? username
? Link to existing project? [y/N] n
? What’s your project’s name? venv
? In which directory is your code located? ./
> Upload [====================] 98% 0.0sNo framework detected. Default Project Settings:
- Build Command: `npm run vercel-build` or `npm run build`
- Output Directory: `public` if it exists, or `.`
- Development Command: None
? Want to override the settings? [y/N] n
```

Once that is complete it is going to give you some links. The app is NOT going to work yet it is only going to give you a browser file download of your `index.py` file. You need to create a `vercel.json` file and put it in the root folder so that Vercel knows that it is a Python application. And it is very important that your `index.py` file remains in the root folder along with your other server side code for the project otherwise your app won't work.

Create a `vercel.json` file and put it in the root of your project folder and then add the code below

```json
{
	"version": 2,
	"builds": [
		{
			"src": "./index.py",
			"use": "@vercel/python"
		}
	],
	"routes": [
		{
			"src": "/(.*)",
			"dest": "/"
		}
	]
}
```

Next manually create a `requirements.txt` file and put it in the root folder with the code below

```plaintext
flask==1.0.2
```

When creating a more complex application that has multiple packages installed it is best to use the command below for automatically creating a `requirements.txt` file. This is the equivalent to a `package.json` file which you should be familiar with if you have worked with Node. You will need to have your dependancies install on the server for it to work. However for this simple example it is not required as the only package that we are using is flask.

```bash
pip3 freeze > requirements.txt
```

Now run the command `vercel --prod`  to deploy your app. Open the Production link and your app should be working online with full working routes.