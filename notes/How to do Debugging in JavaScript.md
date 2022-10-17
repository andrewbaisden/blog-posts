Debugging is an essential part of a project process that every developer has to go through. Regardless of the programming language, debugging code is one of the key methods for ensuring that your code is working as expected. It is damn near impossible for a human to write perfect code no matter how hard we try we are highly likely to encounter bugs at some point which will need to be resolved.

A developer's ability to solve problems is a highly sought-after trait that can be the difference between an average developer and an experienced Senior developer who shows leadership and authority qualities.

## What is debugging?

Basically debugging is the steps that you go through in order to find and fix errors that occur inside of your scripts and codebase. The tools and environments that support debugging are available in all recent web browsers today and these can be found inside modern code editors and Integrated development environments (IDEs).

## The different ways we can do debugging in JavaScript

### Online debugging solutions

There are countless ways to do debugging in JavaScript and each one has its advantages and disadvantages. The important thing is to use a method that works for your use case because the main goal here is to figure out what is causing the bugs in your codebase and how to fix them. Your aim should be to find working solutions and document the process so that you will remember how you solved it and this knowledge can then be used to help other developers troubleshoot similar bugs.

Websites like [Stackoverflow](https://stackoverflow.com/) are a godsend for all developers because they make our lives so much easier. You can usually debug an issue in a fraction of the time that it would usually take if you were doing it on your own. Another online tool that is extremely good for debugging is [Sentry](https://sentry.io/welcome/).

Sentry offers free and paid plans so anybody can give it a try. It is a platform that can deal with crashes, and broken API calls in your application among many other things. You can even monitor the data in your application in real-time and there are beautiful dashboards that really assist with the visual effect.

Another great way for debugging problems can be done using a CI/CD workflow combined with [GitHub Actions](https://github.com/features/actions). For example, you could create a GitHub action to test that your JSON file has the correct formatting. If it does not then it will fail the check preventing the code from being deployed to production which could break your application. This is a good safeguard that can keep your codebase free from easy-to-fix errors.

### Local debugging solutions

Usually when debugging the first step that a developer would choose is to use their code editor, IDE or their web browser for getting to the problem of a code issue. If you are using a JavaScript framework like React for example then it is pretty standard for those bugs to be shown on an error page on your localhost server and also inside of a command line when you are running the server.

When using Test Driven Development with a framework like React Testing Library, Jest and Cypress. This workflow can boost code quality and gives you better test coverage for your entire codebase. A test runner can show you which tests are failing and which are passing so you can easily narrow down and figure out where there are bugs in your codebase.

#### Using console.log for debugging

By far the easiest way to do debugging in JavaScript is by using `console.log` and `console.error` statements.

Let's do a quick example. Firstly use your command line to `cd` to a directory and run the command below to scaffold a project.

```shell
mkdir my-app
cd my-app
touch index.html scripts.js
```

Create an `index.html` file and add the code below to the file.

```html
<!DOCTYPE html>

<html lang="en">
  <head>
    <meta charset="UTF-8" />

    <meta http-equiv="X-UA-Compatible" content="IE=edge" />

    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <title>Pokemon API</title>
  </head>

  <body>
    <script src="scripts.js"></script>
  </body>
</html>
```

Now create a `scripts.js` file and add the code in the snippet below to that file.

```javascript
const getPokemon = async () => {
  // This URL will throw an error try putting in a number between 1 and 8 eg... "generation/1/"

  const API = 'https://pokeapi.co/api/v2/generation/0/';

  const response = await fetch(API);

  const data = await response.json();

  try {
    console.log(data);
  } catch (error) {
    console.error(error);
  }
};

getPokemon();
```

Lastly, open the project in a web browser by clicking on the `index.html` file. You should see a blank page which is fine because there is no HTML on the page. You just need to open the developer tools and go to the console. The easiest way to do this is just to use your mouse and right-click on the page and select **inspect**. Then click on the **console** tab.

In the example above we can see an API call to one of the Pokémon APIs. An error is logged to the console because the API has an invalid URL. The comment inside of the code snippet provides a solution to get it working.

#### Using the JavaScript Chrome Debugger

Another way to debug is by using the Chrome Debugger inside of any Chromium web browser. So this should work in Google Chrome, Brave and Microsoft Edge. The `debugger` keyword basically stops code from executing and is present in most JavaScript engines.

Update your `scripts.js` file with the function below. Just add it below the Pokémon function.

```javascript
function hello(user) {
  let name = `Hello, ${user}!`;

  debugger; // The debugger stops the code on this line

  say(name);
}

hello('User1');
```

Now reload your web browser and go to the **Sources** tab like in the screenshot below.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1658769621/call-stack_oqwzp6.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1658769621/call-stack_oqwzp6.jpg)

As you can see the `debugger` statement has stopped the code executing on that line. You can add as many `debugger` statements as you want to stop the code from executing on any line you want in your codebase.

And if you use Visual Studio Code as your code editor then it is also possible to use the built-in Chrome Debugging combined with setting breakpoints for even more control when looking for bugs.

#### Using the browser developer tools network tab

The network tab inside of a web browser is also a really good way to debug your codebase. You are able to see all of the assets for your application regardless of the file type which is good. From this view, you can see the size of the asset and how long it took to load. The **Status** column is incredibly important too.

The number inside of the **Status** column is called an [HTTP response status code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status). A status code of 200 means that everything is ok and the assets loaded fine. If you see an error code of 404 it means that the file could not be found. Those are two examples there are many more.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1658770159/network-tab_ci8uxd.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1658770159/network-tab_ci8uxd.jpg)

This becomes even more useful when you are using a Rest Client tool for Testing APIs. Three popular tools for testing REST APIs are [Postman](https://www.postman.com/), [Thunder Client](https://www.thunderclient.com/), and [Insomnia](https://insomnia.rest/).

## ESLint and Prettier for JavaScript debugging

Arguably the two most popular npm packages for doing JavaScript debugging are [ESLint](https://eslint.org/) and [Prettier](https://prettier.io/). When combined these two are extremely powerful at analysing your codebase to quickly find problems as well as enforcing good code standards and formatting all of your code so that it is the same for every developer in your team.

This is a standard that all teams should be working towards having implemented in their workflows. These npm packages can be used in your JavaScript frameworks like React and your back-end frameworks and libraries like Node and Nest.js.

Take a look at an example `.prettierrc.json` and `.eslintrc.json` file. The rules inside of them determine what type of checking will be available for your codebase. You can find the full set of rules on their respective websites.

An example `.prettierrc.json` file.

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

An example `.eslintrc.json` file.

```json
"rules": {

"no-console": "off",

"no-unused-vars": "off"

}
```

## Final Thoughts

Today we learned about the different ways that we can do debugging inside of our JavaScript applications. The list of methods is quite extensive and we have so many options for finding bugs and solving problems inside of our codebases. Let's not forget that [Sentry](https://sentry.io/welcome/) is one of the best solutions for performing debugging too!
