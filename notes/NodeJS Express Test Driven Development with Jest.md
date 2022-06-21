# NodeJS Express Test Driven Development with Jest

Test Driven Development is quite straightforward to do when you understand the fundamentals behind the methodology. It is fairly common for companies to expect their developers to be using Test Driven Development whenever they are working on a project. It has become mandatory so if you have not learned it yet then it's really good to practice it in your own personal projects so that you become accustomed to this type of workflow.

There are many libraries and frameworks in JavaScript which are used for backend testing. Two of the most popular ones are [Jest](https://jestjs.io/) and [Mocha](https://mochajs.org/). There are even alternatives like [Jasmine](https://jasmine.github.io/), [Ava](https://github.com/avajs/ava), [Tape](https://github.com/substack/tape) and [QUnit](https://qunitjs.com/) among others. Node.js now has its own built in test runner which is stable since v18.0. However it is still in experimental mode so it is likely to change over time.

In this article, we’ll discuss how to use the new NodeJS test runner for doing some basic testing as well as using Jest for testing different endpoints.

For the NodeJS section there will be a few functions which all perform different calculations.

1. Calculating age
2. Creating a box
3. Seeing a persons power level
4. Checking employees work schedules

The last section of this article will be about the Jest test runner. We will create a NodeJS Express backend which has some CRUD (create, read, update, delete) functionality. There will be 3 working endpoints.

1. A GET endpoint for retrieving an array of objects
2. A GET endpoint for retrieving an item from an array of objects by ID
3. A POST endpoint for adding an item to an array of objects

## Doing testing on the backend

### Using the NodeJS test runner to test backend code

If you wanted to use the built in Node.js test runner you just need to import the following library below and then follow the Node.js documentation [Node.js v18.0.0 documentation](https://nodejs.org/api/test.html#test-runner)for running the tests. Of course you need to make sure that you are using Node version 18 and you can check the version in the command line with this command `node -v `.

This is how you would use the Node test module using ESM Modules or CommonJs syntax.

```javascript
// JavaScript ESM Modules syntax
import test from 'node:test';

// JavaScript CommonJS syntax
const test = require('node:test');
```

Firstly lets see what it's like to do testing using the built in NodeJS test runner.

#### Project Setup

Open your BASH application and then `cd` to any directory you prefer like the desktop. Run the commands below to scaffold your project.

```shell
mkdir node-backend-testing
cd node-backend-testing
npm init -y
touch index.js index.test.js
```

Next open the newly created project in your code editor and add the code below to the files they relate to.

`index.js`

```javascript
const calcAge = (dob) => {
  const digits = {
    year: 'numeric',
  };

  const year = new Date().toLocaleDateString('en-US', digits);

  console.log(year);

  return year - dob;
};

const createBox = (x, y) => {
  return x * y;
};

const canDrive = () => {
  const age = 18;

  if (age >= 18) {
    return 'Full Driving Licence';
  } else {
    return 'Provisional License';
  }
};

const powerLevel = () => {
  const power = 9001;

  if (power > 9000) {
    return true;
  } else {
    return false;
  }
};

const workSchedule = (employeeOne, employeeTwo) => {
  return employeeOne + employeeTwo;
};

module.exports = {
  calcAge,

  createBox,

  canDrive,

  powerLevel,

  workSchedule,
};
```

`index.test.js`

```javascript
const test = require('node:test');

const assert = require('assert/strict');

const {
  calcAge,
  createBox,
  canDrive,
  powerLevel,
  workSchedule,
} = require('./index');

// Calculates how old someone is and depending on the year this test could pass or fail

test('calculates age', () => {
  return assert.equal(calcAge(2000), 22);
});

// Creates a box with an equal height and width

test('creates a box', async (t) => {
  await t.test('creates a small box', () => {
    assert.equal(createBox(10, 10), 100);
  });

  await t.test('creates a large box', () => {
    assert.equal(createBox(50, 50), 2500);
  });
});

// Checks to see whether or not the person has a full driving licence

test('checks license', () => {
  return assert.match(`${canDrive()}`, /Full Driving Licence/);
});

// Confirms that the person has a power level that is over 9000!

test('confirms power level', () => {
  return assert.ok(powerLevel());
});

// Checks to see if the employees have the same amount of shift work days in a week

test('employees have an equal number of work days', () => {
  const employeeOne = ['Monday', 'Tuesday', 'Wednesday,', 'Thursday'];

  const employeeTwo = ['Friday', 'Saturday', 'Sunday,', 'Monday'];

  return assert.equal(workSchedule(employeeOne.length, employeeTwo.length), 8);
});
```

`package.json`

Add this run script.

```json
"scripts": {

"test": "node index.test.js"

},
```

The test script runs the Node test runner which will run the tests in `index.test.js`.

#### Running Node Tests

You only need to run one command from inside of the root folder. Again just another reminder that you need to be using Node version 18 or higher for this to work. Run the command below and you should see 5 tests passing in the console.

```shell
npm run test
```

You can play around with the code inside of the `index.js` and `index.test.js` files to see the tests pass and fail. If you look at the test errors in the console you will know whats failing and the reason why it's failing.

Let me give you some examples below.

##### Calculate Age test

To calculate a user’s age, use the current year minus their year of birth. See the example below in the `index.test.js` file:

```javascript
test('calculates age', () => {
  return assert.equal(calcAge(2000), 21);
});
```

To see the test fail just enter an incorrect age like **21**. The function is expecting a return value of **22** in this example so the number **21** makes the test fail.

##### Create a box test

The test is expecting the answers **100** and **2500**. The equation is 10 x 10 and 50 x 50. Just enter in values that don't add up to the correct number in the output to see the test fail like in the example below.

```javascript
test('creates a box', async (t) => {
  await t.test('creates a small box', () => {
    assert.equal(createBox(10, 30), 100);
  });

  await t.test('creates a large box', () => {
    assert.equal(createBox(50, 20), 2500);
  });
});
```

##### Check licence test

This test checks to see if the person has a full driving licence. Change the age in the `index.js` file canDrive function so that it is less than 18 and the test will fail.

```javascript
const canDrive = () => {
  const age = 17;

  if (age >= 18) {
    return 'Full Driving Licence';
  } else {
    return 'Provisional License';
  }
};
```

##### Confirm power level test

This test checks to see if the person has a power level that is over 9000 (Dragonball Z reference) 😁 Change the power level inside of the `index.js` file powerLevel function to be less than 9000 to see the test fail.

```javascript
const powerLevel = () => {
  const power = 5000;

  if (power > 9000) {
    return true;
  } else {
    return false;
  }
};
```

##### Checks to see if the employees have the same number of work days test

This tests checks that employees are working an equal amount of days. They are currently both working 4 days each which gives a total of 8 days combined. To see the test fail just enter or remove some days from the arrays so they are no longer the same length.

```javascript
test('employees have an equal number of work days', () => {
  const employeeOne = ['Monday', 'Tuesday', 'Wednesday,', 'Thursday'];

  const employeeTwo = ['Friday', 'Saturday'];

  return assert.equal(workSchedule(employeeOne.length, employeeTwo.length), 8);
});
```

### Using Jest to test backend code

Now let's do some backend testing using the Jest testing library.

#### Project Setup

Open your BASH application and then `cd` to any directory you prefer like the desktop. Run the commands below to scaffold your project.

```shell
mkdir jest-backend-testing
cd jest-backend-testing
npm init -y
npm i express http-errors jest nodemon supertest
mkdir routes
touch routes/products.js
touch app.js app.test.js server.js
```

Now open the project in your code editor and add the code below into their corresponding files.

`routes/product.js`

```javascript
const express = require('express');

const router = express.Router();

const createError = require('http-errors');

// Products Array

const products = [{ id: '1', name: 'Playstation 5', inStock: false }];

// GET / => array of items

router.get('/', (req, res) => {
  res.json(products);
});

// GET / => items by ID

router.get('/:id', (req, res, next) => {
  const product = products.find(
    (product) => product.id === String(req.params.id)
  );

  // GET /id => 404 if item not found

  if (!product) {
    return next(createError(404, 'Not Found'));
  }

  res.json(product);
});

router.post('/', (req, res, next) => {
  const { body } = req;

  if (typeof body.name !== 'string') {
    return next(createError(400, 'Validation Error'));
  }

  const newProduct = {
    id: '1',

    name: body.name,

    inStock: false,
  };

  products.push(newProduct);

  res.status(201).json(newProduct);
});

module.exports = router;
```

`app.js`

```javascript
const express = require('express');

const productsRoute = require('./routes/products');

const app = express();

app.use(express.urlencoded({ extended: false }));

app.use(express.json());

app.use('/', productsRoute);

module.exports = app;
```

`app.test.js`

```javascript
const request = require('supertest');

const app = require('./app');

describe('GET /', () => {
  it('GET / => array of items', () => {
    return request(app)
      .get('/')

      .expect('Content-Type', /json/)

      .expect(200)

      .then((response) => {
        expect(response.body).toEqual(
          expect.arrayContaining([
            expect.objectContaining({
              id: expect.any(String),

              name: expect.any(String),

              inStock: expect.any(Boolean),
            }),
          ])
        );
      });
  });

  it('GET / => items by ID', () => {
    return request(app)
      .get('/1')

      .expect('Content-Type', /json/)

      .expect(200)

      .then((response) => {
        expect(response.body).toEqual(
          expect.objectContaining({
            id: expect.any(String),

            name: expect.any(String),

            inStock: expect.any(Boolean),
          })
        );
      });
  });

  it('GET /id => 404 if item not found', () => {
    return request(app).get('/10000000000').expect(404);
  });

  it('POST / => create NEW item', () => {
    return (
      request(app)
        .post('/')

        // Item send code

        .send({
          name: 'Xbox Series X',
        })

        .expect('Content-Type', /json/)

        .expect(201)

        .then((response) => {
          expect(response.body).toEqual(
            expect.objectContaining({
              name: 'Xbox Series X',

              inStock: false,
            })
          );
        })
    );
  });

  it('POST / => item name correct data type check', () => {
    return request(app).post('/').send({ name: 123456789 }).expect(400);
  });
});
```

`server.js`

```javascript
const app = require('./app');

const port = process.env.PORT || 3000;

app.listen(port, () =>
  console.log(`Server running on port ${port}, http://localhost:${port}`)
);
```

`package.json`

Lastly add these run scripts to your `package.json` file.

```json
"scripts": {

"start": "node server.js",

"dev": "nodemon server.js",

"test": "jest --watchAll"

},
```

**start**
The start script runs the server file using node.

**dev**
The dev script runs the server file using nodemon which enables autoreloading.

**jest**
The test script runs the test runner Jest which automatically watches for file changes.

#### Running Jest Tests

It's time to start the application and the test runner. Run the commands below in different tabs/windows so that you have one script running the development server and the other one running the Jest test runner.

The server is running on [http://localhost:3000/](http://localhost:3000/).

```shell
npm run dev
```

```shell
npm run test
```

You should now have the **dev** server running as well the Jest test runner which should have 5 tests which are all passing. Let's go through all of the tests one by one so you can see them fail and pass.

The tests have the same name as the headings so they should be fairly easy to find in the files.

##### GET / => array of items

[http://localhost:3000/](http://localhost:3000/).

This test checks to see if an array of objects is returned. To see it fail open the `products.js` file and replace the route at the top with the code below.

```javascript
router.get('/', (req, res) => {
  res.send('products');
});
```

You should get the error `expected Content-Type" matching /json/, got "text/html; charset=utf-8` and the test should fail.

Now try changing it to the code below.

```javascript
router.get('/', (req, res) => {
  res.json('products');
});
```

You should get this error `Expected: ArrayContaining [ObjectContaining {"id": Any<String>, "inStock": Any<Boolean>, "name": Any<String>}]`.

##### GET / => items by ID

[http://localhost:3000/1](http://localhost:3000/1).

This test checks to see if an item is returned with the correct ID. To see it fail change the products array at the top of the file in `products.js` to have an id that is a number instead of a string like in the example here.

```javascript
const products = [{ id: 1, name: 'Playstation 5', inStock: false }];
```

You should get the error `expected "Content-Type" matching /json/, got "text/html; charset=utf-8"`.

##### GET /id => 404 if item not found

[http://localhost:3000/incorrectpage](http://localhost:3000/incorrectpage)

This test checks to see if an item can't be found. To see it fail change the 404 error code to something else in the `products.js` file like in the example below.

```javascript
if (!product) {
  return next(createError(400, 'Not Found'));
}
```

You should get the error `expected 404 "Not Found", got 400 "Bad Request"`.

##### POST / => create NEW item

This test checks that the object has the correct datatypes and data. To see it fail open the `app.test.js` file and replace the send code with the code below.

```javascript
.send({

name: 'Nintendo Switch',

})
```

You should see the error below.

```shell
 - Expected  - 2
    + Received  + 3

    - ObjectContaining {
    + Object {
    +   "id": "1",
        "inStock": false,
    -   "name": "Xbox Series X",
    +   "name": "Nintendo Switch",
```

##### POST / => item name correct data type check

This test checks to see if the name variable is the correct data type. It should only fail if a string is detected. To see the test fail open the `app.test.js` file scroll to the bottom and change the number to a string like in this example.

```javascript
return request(app).post('/').send({ name: '123456789' }).expect(400);
```

You should get this error `expected 400 "Bad Request", got 201 "Created"`.

### Jest 28: New features

Jest 28 was released in April 2022 and it brought along a lot of new features which you can read about here [Jest 28](https://jestjs.io/blog/2022/04/25/jest-28). One of the most requested features is called [Sharding](https://jestjs.io/docs/cli#--shard). Essentially sharding should in theory let you split your test suite into different shards, so that they can run a fraction of your suite tests. For example to run a third of your tests you could use the commands below.

```shell
jest --shard=1/3
jest --shard=2/3
jest --shard=3/3
```

And that was an introduction to doing testing on the backend using Node and Jest. Those are just the basics of testing there is so much more to learn so check out the official documentation for [Jest](https://jestjs.io/) .
