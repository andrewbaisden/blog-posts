_If you enjoy this topic, you will probably like my articles, tweets, and stuff. If you're wondering, check out my [social media profiles](https://limey.io/andrewbaisden) and don't forget to subscribe and follow since I'm offering programming and motivating tools and information to help you achieve your dreams._

## What is code test coverage?

The percentage of code that is executed during the execution of a set of tests is referred to as test coverage. It serves as a gauge for how much of the codebase is tested and might point out parts of the code that may not have received enough testing. We will talk about several methods for enhancing test coverage in a JavaScript React project in this post.

1.  Make sure all new code is tested. Making ensuring that any new code is accompanied by at least one test is one of the best strategies to increase test coverage. This guarantees that the tests are using the new code and helps identify any errors as soon as they arise.
2.  Use tools for code coverage You may find out whether portions of your codebase are not being tested using a variety of methods. These tools may be used as a component of your test suite and offer a report displaying the proportion of code that is tested. Jest and Istanbul are two common JavaScript tools.
3.  For edge cases, create tests. Testing is crucial, not just for the happy route but also for several edge situations that might not be obvious at first. Corner instances that could have gone unnoticed otherwise might be found thanks to this.
4.  Utilize test frameworks Writing and organising tests is made simpler by the functions and assertions offered by testing frameworks like Mocha, Jasmine, and Jest. Code coverage tools are frequently included in these frameworks, which makes it simpler to track test coverage as you add additional tests.
5.  Creating unit tests Unit tests are brief, standalone tests that evaluate a single piece of code, such as a function. Writing a set of unit tests can make it easier to find problems when they occur and ensure that all components of the code are tested.

So basically, increasing test coverage is a crucial step in maintaining the integrity of the codebase in a JavaScript React project. You can assist guarantee that your code is extensively tested and that any errors are discovered early on by using the procedures described above.

## How does code coverage work in a React project?

Here is an illustration of how a code coverage tool may be used for a project created with React.

Install a code coverage programme first, such [nyc](https://www.npmjs.com/package/nyc). To accomplish this, issue the following command:

```shell
npm install --save-dev nyc
```

The `nyc` command may then be used to run your tests and provide a code coverage report. For instance, you may alter your `package.json` file to add the following script if you are using Jest as your test runner:

```json
"scripts": {
  "test": "nyc jest"
}
```

Now, nyc will execute your tests and produce a code coverage report when you run `npm test`. By launching the file `coverage/index.html` in your browser, you may view the report.

You may define a coverage threshold in your `package.json` file to make sure that your test coverage is within acceptable bounds. See the example below.

```json
"nyc": {
  "check-coverage": true,
  "lines": 80,
  "statements": 80,
  "branches": 80,
  "functions": 80
}
```

If the coverage for any of the supplied metrics is lower than 80%, the tests will fail.

By adding tests to every new code and testing for edge situations, you may increase test coverage in addition to employing a code coverage tool. Additionally, to make writing and organising your tests simpler, you may utilise a testing framework like Mocha or Jasmine.

Here is a depiction of a React component along with some Jest tests for it.

```javascript
export default function MyComponent() {
  return (
    <>
      <div>
        <h1>My Component</h1>
        {props.children}
      </div>
    </>
  );
}
```

Now check out this sample of a test with excellent code coverage for the component `MyComponent`.

```javascript
import { shallow } from 'enzyme';
import MyComponent from './MyComponent';

describe('MyComponent', () => {
  it('renders the correct content', () => {
    const wrapper = shallow(
      <MyComponent>
        <p>Hello World</p>
      </MyComponent>
    );
    expect(wrapper.find('h1').text()).toEqual('My Component');
    expect(wrapper.find('p').text()).toEqual('Hello World');
  });
});
```

This test thoroughly covers the function by exercising both the drawing of the 'h1' element and the rendering of the `props.children` element.

And as you can see in this illustration of a test for the identical component with inadequate code coverage which is not as refined.

```javascript
import { shallow } from 'enzyme';
import MyComponent from './MyComponent';

describe('MyComponent', () => {
  it('renders the correct content', () => {
    const wrapper = shallow(
      <MyComponent>
        <p>Hello World</p>
      </MyComponent>
    );
    expect(wrapper.find('h1').text()).toEqual('My Component');
  });
});
```

This test does not test the rendering of the `props.children` element; it only tests the rendering of the "h1" element. It provides inadequate coverage for the function as a result.

You may include an extra test that simulates the rendering of the `props.children` element to increase the code coverage of this test.

_If you like this article, chances are that you would like my posts, tweets and content as well. If you are curious, have a look at my [social media profiles](https://limey.io/andrewbaisden) and don't forget to subscribe and follow because I am sharing programming and motivation resources and knowledge to support you in achieving your goals 💫_
