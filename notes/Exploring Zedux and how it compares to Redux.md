## Introduction

The React ecosystem has so many state libraries it can be so hard to choose one for your project. All of these choices give us so many options which is always going to be a good thing because we will never run out of alternatives. I'm guessing that you have not heard about Zedux or maybe you have and your new to it. You're probably thinking omg another React state library what makes this one so special and why should we learn it over the plethora of options at our disposal? That's a perfectly valid question and it's one that I was curious about myself because this library was new to me as well so I will be approaching this as a first-time learner too.

Before we get started let's quickly take a look at some of the other React state options that are already available to us. Some of the state management tools that we can choose from are:

- [Redux](https://redux.js.org/)
- [Hookstate](https://hookstate.js.org/)
- [Recoil](https://recoiljs.org/)
- [Jotai](https://jotai.org/)
- [Rematch](https://rematchjs.org/)
- [Zustand](https://docs.pmnd.rs/zustand/getting-started/introduction)
- [MobX](https://mobx.js.org/README.html)
- [React Query](https://tanstack.com/query/latest/)
- [Valtio](https://valtio.pmnd.rs/)
- [Akita](https://opensource.salesforce.com/akita/)
- [Easy Peasy](https://easy-peasy.dev/)

There are many more state library tools out there these are just a few of the most popular ones. Other than using an external React state library we can also use the built-in React [Context API with Reducer](https://react.dev/learn/scaling-up-with-reducer-and-context). Another solution would be to use [GraphQL](https://graphql.org/) for managing our data and state instead. So as you can see we have a lot of different ways to manage our state and data if we wanted to. Today we are just going to focus on Zedux and Redux however so with our introduction out of the way it's time to get started.
## What is Zedux

[Zedux](https://omnistac.github.io/zedux/) is a fairly new state engine for React which features a composable store model wrapped in a DI-driven atomic architecture. The creators of Zedux said that they spent 5 years evaluating other React state libraries and taking their best features and combining them all together to create their own powerhouse state management library. They did all this while also working on their own unique features to truly make Zedux a feature-rich library.

What sets Zedux apart is the way it distinguishes itself by separating the state layer (stores) from the architectural layer (atoms). Apparently, this enables a strong Dependency Injection approach that is theoretically comparable to yet simpler and more dynamic than Angulars. In the next section, we will compare Zedux with Redux and see just how simple and straightforward the codebase and syntax are and why it's perfect for beginners to get started.

## The differences between Zedux and Redux

### A beginner-friendly setup

Getting up and running with Zedux inside of a React project could not be easier just take a look at this code example and be amazed at how easy on the eye it is! Unlike more complex state libraries that have lots of boilerplate code like Redux, the code you see here is so lightweight and only a few lines of code long. This is all the code you need after the package has been installed it's ridiculously easy which is one of the greatest advantages of this library over other state management tools.

```javascript
import { atom, useAtomState } from '@zedux/react';

const narutoAtom = atom('naruto', 'Naruto');

const nameAtom = atom('name', '');

export default function Greeting() {
  const [naruto, setNaruto] = useAtomState(narutoAtom);

  const [name, setName] = useAtomState(nameAtom);

  return (
    <>
      <input value={name} onChange={(event) => setName(event.target.value)} />

      <div>
        <p>{naruto}</p>

        <button onClick={() => setNaruto(name)}>Change Name</button>
      </div>
    </>
  );
}
```

Much like other state management libraries out there Zedux also uses Stores for managing global states in our applications. Stores in Zedux applications use what's known as a composable store model. They are said to be lightweight, powerful and fast. A big selling point of the Zedux state library is the fact that there is a Zero Config option. The configuration is optional which means that it is not necessary to have reducer hierarchies which have action creators for each store.

```javascript
import { createStore } from '@zedux/react';

const easySauceStore = createStore();
```

As you can see here it requires very little code to set up a basic Zedux store.

### Comparing Zedux with Redux

Redux and Zedux have fairly broad differences between them such as their APIs, and unique capabilities yet have similar aims and general methodologies. We are now going to take a much closer look to see how they differ on different subjects. 
#### Build Architecture

In terms of building architecture, they both go in different directions. Redux follows the Elm architecture which is Model, View, and Update. They are the three separate parts of an Elm application, according to the Elm application architectural pattern. The interaction of these independent elements results in an organised and productive application cycle.

In comparison, Zedux has a different approach as it focuses more on representing the state as a limited state machine. State machines with distinct states and transitions are easier to define given the design. Another difference is the way they both handle reducers. Reducers are purely functional elements in Redux that take the current state and an action and return a new state. In Zedux they are not called Reducers instead they are referred to as "actors". These are action-handling functions, but they also have the ability to send out new actions, which might have unintended consequences.

Another area to compare is when we use Actions in our state frameworks. The approach that Redux uses is to have pure functions which utilise a state and an action as inputs and outputs a new state. Zedux on the other hand allows for synchronous or asynchronous actions as well as "staged" activities, which allow for many actions to be delivered in succession with a predetermined delay.
#### Middleware

Lastly, let's touch on the subject of middleware and how it works in both of them. Although Zedux middleware can intercept actions, it can also alter actors and construct its own mini-state machines. This is in contrast to Redux which enables features like log tracking, crash analysis reports, and action processing for asynchronous code. With this method, we can be allowed to create logic that intercepts actions before they reach the reducer.

We learned a great deal and bolster our knowledge let's move on and build something now taking what we have just learned into account. The theory is over we are moving on to some practical now.

## Building an app with Zedux and comparing it to a Redux app

Alright, we learned about some of the differences between Zedux and Redux I think it's time that we put some of that new knowledge to good use and actually see what Zedux looks like in a real codebase. The app that we will be building today is going to be a settlement-type app let me give you a quick run-through on what it is exactly.

Basically, the application describes 4 of the main settlement types which are ranked by population size and include:

- Hamlet
- Village
- Town
- City

There are buttons for incrementing and decrementing by 1 and we can also use the input to add people to our hypothetical plot of land which will increase or decrease in size and there is a description that tells us what type of settlement it is based on how big the population is. And just for fun, we can add numbers of people if they are odd or even in size. That's essentially the app it's a nice demo to test out how the state works in a Zedux and Redux application.

You can see what the application looks like in this image here.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1691439481/redux-zedux-settlement-app_cfyr0u.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1691439481/redux-zedux-settlement-app_cfyr0u.jpg)

So we are pretty much going to end up with two applications which are identical. One was built using Zedux and the other one was built using Redux.

> **Spoiler alert the Zedux application has less boilerplate and as a result a much smaller codebase.**

Anyway, enough talking let's just get to it shall we because there is quite a bit of code and setup to go through. First, we will start with the Zedux app version. The React framework which will use is [Next.js](https://nextjs.org/).

The codebase for both applications can be found online here [https://github.com/andrewbaisden/settlement-types](https://github.com/andrewbaisden/settlement-types)

### Zedux settlement app

First, navigate to a folder on your computer and then set up your Next.js project by running the command here:

Just use all the default setup configuration settings.

```shell
npx create-next-app my-app-zedux
```

Now `cd` into your project folder and install the Zedux package:

```shell
cd my-app-zedux
npm i @zedux/react
```

Let's now create the folders and files for our project. Run these commands below to do that now while in the root folder for `my-app-zedux`:

```shell
mkdir src/app/components src/app/components/Counter
mkdir src/app/styles
touch src/app/components/Counter/Counter.js src/app/components/Counter/counter.module.css
touch src/app/styles/globals.css
touch src/app/store.js
```

Alright good our project has the right files and folders now let's add the code and we are ready to run it.

Starting with the `next.config.js` file let's add this code. The images for the app are hosted on Cloudinary so we need to add the domain to this file so it gets access:

```javascript
/** @type {import('next').NextConfig} */

module.exports = {
  images: {
    domains: ['res.cloudinary.com'],
  },
};
```

Now for the `Counter.js` file in the components folder:

```javascript
'use client';

import { useState } from 'react';

import { useAtomState } from '@zedux/react';

import Image from 'next/image';

import { countAtom, settlementAtom } from '../../store';

import styles from './counter.module.css';

export default function Counter() {
  const [
    count,

    { decrement, increment, incrementByAmount, incrementOdd, incrementEven },
  ] = useAtomState(countAtom);

  const [settlement] = useAtomState(settlementAtom);

  const [incrementAmount, setIncrementAmount] = useState(2);

  const [imgSize] = useState(200);

  const Settlements = () => {
    if (count > 0 && count <= 100) {
      return (
        <>
          <h1>{settlement[0].type}</h1>

          <h2>Size: {settlement[0].size}</h2>

          <p>{settlement[0].description}</p>

          <Image
            alt={settlement[0].type}
            src={settlement[0].img}
            height={imgSize}
            width={imgSize}
          />
        </>
      );
    } else if (count > 100 && count <= 3000) {
      return (
        <>
          <h1>{settlement[1].type}</h1>

          <h2>Size: {settlement[1].size}</h2>

          <p>{settlement[1].description}</p>

          <Image
            alt={settlement[1].type}
            src={settlement[1].img}
            height={imgSize}
            width={imgSize}
          />
        </>
      );
    } else if (count > 3001 && count <= 5000) {
      return (
        <>
          <h1>{settlement[2].type}</h1>

          <h2>Size: {settlement[2].size}</h2>

          <p>{settlement[2].description}</p>

          <Image
            alt={settlement[2].type}
            src={settlement[2].img}
            height={imgSize}
            width={imgSize}
          />
        </>
      );
    } else if (count > 5001) {
      return (
        <>
          <h1>{settlement[3].type}</h1>

          <h2>Size: {settlement[3].size}</h2>

          <p>{settlement[3].description}</p>

          <Image
            alt={settlement[3].type}
            src={settlement[3].img}
            height={imgSize}
            width={imgSize}
          />
        </>
      );
    }
  };

  return (
    <div className={styles.container}>
      <div className={styles.settlements}>
        <Settlements />
      </div>

      <div className={styles.counter}>
        <button
          className={styles.button}
          aria-label="Decrement value"
          onClick={decrement}
        >
          -
        </button>

        <span className={styles.value}>{count}</span>

        <button
          className={styles.button}
          aria-label="Increment value"
          onClick={increment}
        >
          +
        </button>
      </div>

      <div className={styles.buttonmenu}>
        <input
          className={styles.textbox}
          aria-label="Set increment amount"
          value={incrementAmount}
          onChange={(e) => setIncrementAmount(Number(e.target.value ?? 0))}
        />

        <button
          className={styles.button}
          onClick={() => incrementByAmount(incrementAmount)}
        >
          Add People
        </button>

        <button
          className={styles.button}
          onClick={() => incrementOdd(incrementAmount)}
        >
          Add If Odd
        </button>

        <button
          className={styles.button}
          onClick={() => incrementEven(incrementAmount)}
        >
          Add If Even
        </button>
      </div>

      <div className={styles.legend}>
        <p>Settlement Sizes by people (example)</p>

        <p>Add X numbers of people to see the differences in the settlement.</p>

        <ul>
          <li>Hamlet: 1 - 100</li>

          <li>Village: 101 - 3000</li>

          <li>Town: 3001 - 5000</li>

          <li>City: 50001 - Infinity</li>
        </ul>
      </div>
    </div>
  );
}
```

The next file has our CSS for the `Counter.js` file and this goes into the `counter.module.css` file:

```css
.container {
  margin: 0 auto;

  max-width: 96rem;
}

.counter {
  display: flex;

  justify-content: center;
}

.settlements {
  display: flex;

  flex-flow: column nowrap;

  align-items: center;

  margin: 2rem auto;

  padding: 1rem;

  border: 0.1rem solid black;
}

.buttonmenu {
  display: flex;

  flex-flow: row nowrap;

  justify-content: center;

  margin-top: 2rem;
}

.value {
  font-size: 5rem;

  padding-left: 1.6rem;

  padding-right: 1.6rem;

  margin-top: 0.5rem;

  font-family: 'Courier New', Courier, monospace;
}

.button {
  appearance: none;

  background: none;

  font-size: 2rem;

  padding-left: 1.2rem;

  padding-right: 1.2rem;

  outline: none;

  border: 2px solid transparent;

  color: rgb(96 165 250);

  padding-bottom: 0.4rem;

  cursor: pointer;

  background-color: rgba(76, 106, 182, 0.1);

  transition: all 0.15s;
}

.textbox {
  font-size: 2rem;

  padding: 0.2rem;

  width: 10rem;

  text-align: center;

  margin-right: 0.4rem;
}

.button:hover,
.button:focus {
  background-color: rgb(59 130 246);

  color: #ffffff;
}

.button:active {
  background-color: rgba(76, 85, 182, 0.2);
}

.legend {
  padding: 0.5rem;
}
```

Moving on let's do the `globals.css` file in the `styles` folder:

```css
html,
body {
  min-height: 100vh;

  padding: 0;

  margin: 0;

  font-family: system-ui, sans-serif;
}

a {
  color: inherit;

  text-decoration: none;
}

* {
  box-sizing: border-box;
}
```

After that is the `layout.js` file in the `app` folder so replace all the code with this:

```javascript
import './styles/globals.css';

export default function RootLayout(props) {
  return (
    <html lang="en">
      <body>
        <main>{props.children}</main>
      </body>
    </html>
  );
}

export const metadata = {
  title: 'Settlements',
};
```

Next up is the `page.js` file once again replace all the code:

```javascript
'use client';

import Counter from './components/Counter/Counter';

export default function IndexPage() {
  return (
    <>
      <Counter />
    </>
  );
}
```

And lastly, the `store.js` file has our store and state:

```javascript
import { api, atom, injectStore } from '@zedux/react';

export const countAtom = atom('count', () => {
  const store = injectStore(0);

  return api(store).setExports({
    decrement: () => store.setState((state) => state - 1),

    increment: () => store.setState((state) => state + 1),

    incrementByAmount: (action) => store.setState((state) => (state += action)),

    incrementOdd: (action) => {
      if (store.getState() % 2 === 1) {
        return store.setState((state) => state + action);
      }
    },

    incrementEven: (action) => {
      if (store.getState() % 2 === 0) {
        return store.setState((state) => state + action);
      }
    },
  });
});

export const settlementAtom = atom('settlement', () => {
  const store = injectStore([
    {
      type: 'Hamlet',

      size: '1 - 100',

      description:
        'A hamlet is a smaller-scale community than a town or village. The term "smaller settlement" is frequently only a colloquial term for a smaller settlement, or even a subdivision or satellite organisation to a bigger community.',

      img: 'https://res.cloudinary.com/d74fh3kw/image/upload/v1691415034/hamlet_n50lem.jpg',
    },

    {
      type: 'Village',

      size: '101 - 3000',

      description:
        'Although the term is sometimes used to cover both hamlets and smaller towns, a village is a grouped human settlement or community, bigger than a hamlet but less than a town, with a population generally ranging from a few hundred to a few thousand.',

      img: 'https://res.cloudinary.com/d74fh3kw/image/upload/v1691415578/village_n7hoyb.jpg',
    },

    {
      type: 'Town',

      size: '3001 - 5000',

      description:
        'An urban area, or town, is a place where people reside. It alludes to the entirety of the human community, including all of its social, material, organisational, spiritual, and cultural components. Towns are often smaller than cities and bigger than villages, however the criteria used to differentiate between them vary greatly throughout the world.',

      img: 'https://res.cloudinary.com/d74fh3kw/image/upload/v1691416139/town_lhwwza.jpg',
    },

    {
      type: 'City',

      size: '5001 - Infinity',

      description:
        'A large-scale urban area is referred to as a city. It can be described as a location that is permanently populated, has clearly defined administrative boundaries, and whose inhabitants focus mostly on non-agricultural jobs. For housing, transportation, sanitation, utilities, land use, the manufacturing of commodities, and communication, cities often have vast systems.',

      img: 'https://res.cloudinary.com/d74fh3kw/image/upload/v1691416356/city_aw2lvq.jpg',
    },
  ]);

  return store;
});
```

Ok, now our codebase should be complete just make sure that you are in the root for the folder `my-app-zedux` and run the command `npm run dev` to start the application.

### Redux settlement app

As I mentioned earlier the Redux app is identical however the codebase is much bigger due to the huge boilerplate and set-up for the codebase. So instead of going through all of the setup I have put both codebases online here [https://github.com/andrewbaisden/settlement-types](https://github.com/andrewbaisden/settlement-types).
## Conclusion

Congratulations we just made it to the end of this tutorial! We learned about the differences between Zedux and Redux and we even built an app using Zedux. As you can see they are many common similarities between the two however Zedux is much more beginner friendly. I think the fact that Zedux has a zero-configuration option makes it an incredibly good alternative to Redux and other state libraries because it does not take much to get up and running.

In comparison Redux as good as it is still requires quite a lengthy setup with a lot of boilerplate and in my opinion, the learning curve is a bit higher as a result. Nonetheless, both state libraries have great documentation so whichever one you use it is guaranteed that your project is in safe hands.