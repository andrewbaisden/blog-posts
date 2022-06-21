# How to use ESLint and Prettier for code analysis and formatting

ESLint and Prettier are pretty much the two most popular tools when it comes to doing code analysis and formatting in a developers codebase. They are extremely good at what they do which is why they tend to be an essential part of a projects setup.

The difference between the two is that ESLint is usually responsible for finding and reporting on different patterns inside of ECMAScript/JavaScript code. ESLint is designed to work with JavaScript files only and it is very successful when it comes to ensuring that a codebase is consistent and without notable bugs.

Prettier on the other hand is an opinionated code formatter. Unlike ESLint it supports a variety of languages like JavaScript, HTML, CSS, GraphQL, Markdown and many others. Both tools are fairly well supported in the developer community and extensions are available for both of them in most code editors or IDE's like Visual Studio Code for example.

**Visual Studio Code Marketplace**
[ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
[Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

**Website**
[https://prettier.io/](https://prettier.io/)
[https://eslint.org/](https://eslint.org/)

## Why you should use a linter and code formatter

Linting is a way to fix problems in your code while still in development mode before your application is ready for production. A lot of these fixes can be done automatically and you can customise the whole process to suit your teams needs. When using Prettier you can have the code in your files formatted automatically which saves you tons of time and energy.

It's also one less thing you need to worry about in a code review because it is guaranteed to be the same for everyone. It enforces the same style and code quality across the whole team so there are no conflicts like when you have your own personal local setup.

This is a common process that teams follow when working on projects. It is typical for there to be a file for ESLint and Prettier alongside an ignore file much like a `.gitignore` file that every developer should be familiar with when using a service like GitHub for version control. The format for your main file can be either JavaScript, YAML or JSON. I'm using JSON in these examples.

See the example files below which would all be inside of one project:

`.eslintignore`
`.eslintrc.json`
`.prettierignore`
`.prettierrc.json`

## Creating a ESLint and Prettier workflow setup

ESLint and Prettier files can conflict with each other because there are occasions when they end up checking the same rules which can lead to duplication. Fortunately it is possible to get them both to work together.

### Visual Studio Code Settings

Firstly you need to install the ESLint and Prettier extensions.

Then go to Code -> Preferences -> Settings

You can use the search box to search for the ESLint and Prettier extensions you installed. It should be fine to leave the default ESLint settings but you can change them if you want to. Prettier might require some global setting changes but customise it how you want.

These are the most notable ones I have.

- Prettier: Semi ✅
- Prettier: Single Quote ✅
- Prettier: Trailing Comma **es5**

While on the Settings page search for **format**.

Make sure that these settings are correct you might need to scroll down to find the default formatter:

- Editor: Format On Save ✅
- Editor: Default Formatter **Prettier - Code formatter**

### Plain JavaScript/NodeJS Setup

Open the command line and then go to a directory like your desktop. Run the commands below to setup your project.

```shell
mkdir backend
cd backend
npm init -y
npm install eslint eslint-config-prettier eslint-plugin-prettier --save-dev
```

Now run the code below in the same folder and go through the setup.

```shell
npm init @eslint/config
```

These are the settings I chose:

✔ How would you like to use ESLint? - **To check syntax, find problems, and enforce code style**
✔ What type of modules does your project use? - **CommonJS (require/exports)**
✔ Which framework does your project use? - **None of these**
✔ Does your project use TypeScript? - **No**
✔ Where does your code run? - **Node**
✔ How would you like to define a style for your project? - **Use a popular style guide**
✔ Which style guide do you want to follow? - **[Airbnb](https://github.com/airbnb/javascript)**
✔ What format do you want your config file to be in? - **JSON**

Checking peerDependencies of eslint-config-airbnb-base@latest

The config that you've selected requires the following dependencies:

eslint-config-airbnb-base@latest eslint@^7.32.0 || ^8.2.0 eslint-plugin-import@^2.25.2

✔ Would you like to install them now? - **Yes**
✔ Which package manager do you want to use? - **npm**

Now run the commands in the code block below to create files for Prettier.

```shell
npm install --save-dev --save-exact prettier
echo {}> .prettierrc.json
```

Open your `.eslintrc.json` file and add these configuration settings. Prettier needs to be last in the array otherwise it won't work properly.

```json
"extends": ["airbnb-base", "plugin:prettier/recommended"],

"plugins": ["prettier"],
```

Next open the `.prettierrc.json` file and copy and paste these settings. You can learn about these settings in the [Prettier Options](https://prettier.io/docs/en/options.html) documentation. This is just my setup you can create your own to suit your preferences.

```json
{
  "printWidth": 100,

  "semi": true,

  "singleQuote": true,

  "tabWidth": 4,

  "useTabs": false,

  "trailingComma": "none",

  "endOfLine": "auto"
}
```

Lastly run the code below to create some ignore files for ESLint and Prettier. They work just like a `.gitignore` file so whatever entries you have in there will be ignored so they wont get linted or formatted.

```shell
touch .prettierignore .eslintignore
```

Just copy and past the same code into the `.prettierignore` and `.eslintignore` files.

```shell
node_modules
package.lock.json
build
```

### Using ESLint and Prettier

Let's do a quick test. Create an `index.js` file either in your editor or using the command below in the terminal.

```shell
touch index.js
```

Add this JavaScript code to the file.

```javascript
const x = 100;

console.log(x);

const test = (a, b) => {
  return a + b;
};
```

In your code editor you should see some errors and warnings in the problems tab at the bottom. And if you make your code less readable by adding spacing or tabs all over the place and then save the file. Prettier should clean up and fix everything.

There should be a squiggly line under the console.log and test function name. If you hover your mouse cursor over them you can see the ESLint rule assigned to them. Go to the `.eslintrc.json` file and add these rules at the bottom.

```json
"rules": {

"no-console": "off",

"no-unused-vars": "off"

}
```

Now if you go back to the `index.js` file the warnings should be gone! You can find all of the rules in the [ESLint rules](https://eslint.org/docs/rules/) documentation. It's also possible to change the rules/options in the `.prettierrc.json` file by going to the [Prettier Options](https://prettier.io/docs/en/options.html) page.

#### Restarting the ESLint Server

Sometimes the linting does not work after making changes. To fix this in Visual Studio Code run the command **Shift+CMD+P** to Show the Command Palette and then search for **ESLint: Restart ESLint Server**. This should get the linting working properly in all files.

Remember that you might need to restart the ESLint server every single time you add/remove rules or make changes. Otherwise the rules might not work and it could cause ESLint and Prettier to have conflicts.

### ReactJS Setup

The same setup works with other JavaScript frameworks like React. You just need to choose the appropriate settings. See the example below.

Remember to select **JavaScript modules (import/export)** because thats what React uses and the code will run in the browser.

```shell
npx create-react-app my-app
cd my-app
npm install eslint eslint-config-prettier eslint-plugin-prettier --save-dev
npm init @eslint/config
```

Now run the commands in the code block below to create files for Prettier.

```shell
npm install --save-dev --save-exact prettier
echo {}> .prettierrc.json
```

Open your `.eslintrc.json` file and add these configuration settings. Prettier needs to be last in the array otherwise it won't work properly.

```json
"extends": [

"plugin:react/recommended",

"airbnb",

"plugin:prettier/recommended"

],

"plugins": ["react", "prettier"],
```

Next open the `.prettierrc.json` file and copy and paste these settings. You can learn about these settings in the [Prettier Options](https://prettier.io/docs/en/options.html) documentation. This is just my setup you can create your own to suit your preferences.

```json
{
  "printWidth": 100,

  "semi": true,

  "singleQuote": true,

  "tabWidth": 4,

  "useTabs": false,

  "trailingComma": "none",

  "endOfLine": "auto"
}
```

Lastly run the code below to create some ignore files for ESLint and Prettier. They work just like a `.gitignore` file so whatever entries you have in there will be ignored so they wont get linted or formatted.

```shell
touch .prettierignore .eslintignore
```

Just copy and past the same code into the `.prettierignore` and `.eslintignore` files.

```shell
node_modules
package.lock.json
build
```

Now if you open the `App.js` file you should see warnings and errors in the problems tab below. If you wan't to disable a rule follow the steps earlier and find the rules in the [ESLint rules](https://eslint.org/docs/rules/) documentation.
