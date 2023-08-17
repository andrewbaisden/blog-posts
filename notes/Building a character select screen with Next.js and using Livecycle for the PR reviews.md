## Introduction

In this post, we will look at how to create a character choose screen with Next.js, a popular React-based framework for creating server-side rendered apps. We go over the fundamentals of Next.js and then walk through the process of creating a character choose screen with interactive features utilising Tailwind CSS and JavaScript.

Moreover, we go through the advantages of utilising Livecycle, a code review tool that automates and simplifies the pull request (PR) review process, as well as how to set it up for a Next.js project. We describe how Livecycle can increase the efficiency and quality of code reviews, and we lead you through the stages of creating, requesting reviews, approving, and merging a pull request with Livecycle.

Ultimately, this post gives a detailed method on creating a character choice screen with Next.js and leveraging Livecycle for PR reviews in order to improve the development process and user experience.

## Building a character select screen with Next.js

### The importance of building a character select screen

The creation of a character select screen is essential in applications that need user involvement, such as games or simulations. The character pick screen is the user's initial point of interaction with the programme, giving a visual and interactive interface for the user to select and customise their character.

Having a well-designed and functional character select screen can enhance the user experience, as it allows the user to personalise their experience and feel more invested in the application. A good character select screen can also make the application more accessible, as it provides clear instructions and options for the user.

A character select screen that is well-designed and effective may improve the user experience by allowing the user to personalise their experience and feel more involved in the programme. A decent character pick screen may also make the programme more accessible by providing the user with clear instructions and alternatives.

Overall, developing a character pick screen is essential for producing a user-friendly and engaging application, and it may give useful insights for the application development process.

From a programming standpoint, we get to construct a beautiful user experience, and in this lesson, we will utilise Tailwind CSS to do so. Additionally, we will learn about state and how to pass an object of data around in order to display the character's profile and other associated information.

### How does Next.js benefit React developers?

Next.js is an open-source React-based framework that provides several advantages to developers. It supports server-side rendering for quicker loading times and better SEO, simplifies routing, supports automated code splitting, has built-in CSS and Sass support, provides API routes, and allows static site development.

These characteristics simplify the creation and management of complicated applications, enhance application speed, and lessen the requirement for server-side rendering, making it a popular option among React developers.

It is also the number one React build tool so its perfect for creating React applications.

### Setting up the character select screen project in Next.js

#### Creating the project

Navigate to a directory on your computer like the desktop and then run the commands below to scaffold a Next.js project. Go through and select the options you prefer I just left everything as default. We will also install uuid for generating random ids this will become useful when we start to work with our data later.

```shell
npx create-next-app@latest character-select-screen
cd character-select-screen
npm i uuid
```

#### Installing Tailwind CSS

Now you will need to install `tailwindcss` and its peer dependencies via npm, and then run the init command to generate a `tailwind.config.js` and `postcss.config.js` file. Run the commands below in your terminal.

```shell
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

Next open the project in your code editor we have to update some files to complete the setup for Tailwind CSS. Open the `tailwind.config.js` file and replace all of the code with this one.

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    './app/**/*.{js,ts,jsx,tsx}',
    './pages/**/*.{js,ts,jsx,tsx}',
    './components/**/*.{js,ts,jsx,tsx}',

    // Or if using `src` directory:
    './src/**/*.{js,ts,jsx,tsx}',
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

Lastly replace all of the code inside of the `globals.css` file with this code which has a CSS reset and the Tailwind directives for the CSS.

```css
@tailwind base;

@tailwind components;

@tailwind utilities;

*,
*::before,
*::after {
  margin: 0;

  padding: 0;

  box-sizing: border-box;
}

:root {
  --main-font-size: 16px;
}

html {
  font-size: var(--main-font-size);
}
```

Finally run your build process with `npm run dev` and your Next.js project should be fully working with Tailwind CSS. With the basic setup complete we can now move onto the design phase.

#### Creating a character select screen

Lets now design the UI with CSS, create the components for the screen and add interactivity with JavaScript. All you have to do is copy and paste the code into the correct files.

Update the `globals.css` file with this CSS here.

```css
@import url('https://fonts.googleapis.com/css2?family=Kanit:wght@400;700&family=Roboto&display=swap');

@tailwind base;

@tailwind components;

@tailwind utilities;

*,
*::before,
*::after {
  margin: 0;

  padding: 0;

  box-sizing: border-box;
}

:root {
  --main-font-size: 16px;
}

html {
  font-size: var(--main-font-size);
}

body {
  font-family: 'Kanit', sans-serif;

  background-color: rgb(30 41 59);
}

.header {
  background-color: white;

  padding: 2rem;
}

.header p {
  font-size: 1.5rem;
}

h1 {
  font-size: 2rem;
}

h2 {
  font-size: 2.5rem;
}

.character-profile:hover {
  border: 0.2rem solid rgb(252 211 77);

  cursor: pointer;
}
```

And lastly replace all of the code in the `index.js` file with all of the logic here and this will complete the design.

```javascript
import { useState, useEffect } from 'react';

import { v4 as uuidv4 } from 'uuid';

export default function Home() {
  useEffect(() => {
    console.log(data);
  }, []);

  const [data, setData] = useState([
    {
      id: uuidv4(),

      name: 'Xandorath',

      img: 'https://res.cloudinary.com/d74fh3kw/image/upload/v1677434472/game-character-assault-01_yzbzk1.jpg',

      type: 'Assault',

      ability: 'Offensive combatant',

      bio: 'Assault class combat abilities are unmatched on the battlefield. They have a keen eye for spotting enemy positions and are skilled in using a variety of weapons, including rifles, shotguns, and pistols. Their favourite weapon is a fully automatic assault rifle that they can use to suppress enemy fire and gain an advantage in a firefight. They are also adept at using grenades and other explosive devices to clear out enemy positions.',
    },

    {
      id: uuidv4(),

      name: 'Valtorien',

      img: 'https://res.cloudinary.com/d74fh3kw/image/upload/v1677434473/game-character-assault-02_ynlshz.jpg',

      type: 'Assault',

      ability: 'Destructive challenger',

      bio: 'Assault class combat abilities are unmatched on the battlefield. They have a keen eye for spotting enemy positions and are skilled in using a variety of weapons, including rifles, shotguns, and pistols. Their favourite weapon is a fully automatic assault rifle that they can use to suppress enemy fire and gain an advantage in a firefight. They are also adept at using grenades and other explosive devices to clear out enemy positions.',
    },

    {
      id: uuidv4(),

      name: 'Zephyrion',

      img: 'https://res.cloudinary.com/d74fh3kw/image/upload/v1677434472/game-character-medic-01_rlv9hz.jpg',

      type: 'Medic',

      ability: 'Support powerhouse',

      bio: 'Medics skills and abilities make them an invaluable asset to any team. They are an expert in first aid and can quickly assess and stabilise wounded soldiers on the battlefield. They are also skilled in using medical equipment, including defibrillators, IVs, and other life-saving devices. Their quick thinking and calm demeanour under pressure have saved countless lives on the battlefield.',
    },

    {
      id: uuidv4(),

      name: 'Eryndor',

      img: 'https://res.cloudinary.com/d74fh3kw/image/upload/v1677434473/game-character-medic-02_l8t2ar.jpg',

      type: 'Medic',

      ability: 'Rapid healer',

      bio: 'Medics skills and abilities make them an invaluable asset to any team. They are an expert in first aid and can quickly assess and stabilise wounded soldiers on the battlefield. They are also skilled in using medical equipment, including defibrillators, IVs, and other life-saving devices. Their quick thinking and calm demeanour under pressure have saved countless lives on the battlefield.',
    },

    {
      id: uuidv4(),

      name: 'Lythirius',

      img: 'https://res.cloudinary.com/d74fh3kw/image/upload/v1677434473/game-character-scout-01_faaogs.jpg',

      type: 'Scout',

      ability: 'Frontline spy',

      bio: 'Scouts skills and abilities make them a valuable asset on the battlefield. They are an expert in reconnaissance and can quickly assess enemy positions and movements. They are also skilled in using a variety of weapons, including long-range rifles and pistols, to eliminate enemy targets from a distance.',
    },

    {
      id: uuidv4(),

      name: 'Aerineth',

      img: 'https://res.cloudinary.com/d74fh3kw/image/upload/v1677434474/game-character-scout-02_o6pvwt.jpg',

      type: 'Scout',

      ability: 'Recon agent',

      bio: 'Scouts skills and abilities make them a valuable asset on the battlefield. They are an expert in reconnaissance and can quickly assess enemy positions and movements. They are also skilled in using a variety of weapons, including long-range rifles and pistols, to eliminate enemy targets from a distance.',
    },

    {
      id: uuidv4(),

      name: 'Kaeloria',

      img: 'https://res.cloudinary.com/d74fh3kw/image/upload/v1677434473/game-character-tech-01_idvkjv.jpg',

      type: 'Tech',

      ability: 'Strategic intellect',

      bio: 'Tech skills and abilities make them an important part of any team. They are an expert in the use of technology and can quickly assess a situation and come up with a plan to deploy the right devices to gain an advantage. They are skilled in using a variety of gadgets, including drones, hacking tools, and remote-controlled vehicles, to gather intelligence, disrupt enemy communications, and take out enemy targets.',
    },

    {
      id: uuidv4(),

      name: 'Dravenath',

      img: 'https://res.cloudinary.com/d74fh3kw/image/upload/v1677434474/game-character-tech-02_qidcju.jpg',

      type: 'Tech',

      ability: 'Skilled Hacker',

      bio: 'Tech skills and abilities make them an important part of any team. They are an expert in the use of technology and can quickly assess a situation and come up with a plan to deploy the right devices to gain an advantage. They are skilled in using a variety of gadgets, including drones, hacking tools, and remote-controlled vehicles, to gather intelligence, disrupt enemy communications, and take out enemy targets.',
    },

    {
      id: uuidv4(),

      name: 'Sylphiria',

      img: 'https://res.cloudinary.com/d74fh3kw/image/upload/v1677434473/game-character-magic-01_pq2dav.jpg',

      type: 'Magic',

      ability: 'Cardinal hero',

      bio: 'The Magic class has skills and abilities which make them an invaluable asset on the battlefield. They are skilled in a variety of magic types, including elemental magic, divination, and enchantment. They can use their magic to manipulate the environment, summon magical creatures, and even read the thoughts of their enemies.',
    },

    {
      id: uuidv4(),

      name: 'Torvaxus',

      img: 'https://res.cloudinary.com/d74fh3kw/image/upload/v1677434473/game-character-magic-02_sfcq3e.jpg',

      type: 'Magic',

      ability: 'Dynamic Conjurer',

      bio: 'The Magic class has skills and abilities which make them an invaluable asset on the battlefield. They are skilled in a variety of magic types, including elemental magic, divination, and enchantment. They can use their magic to manipulate the environment, summon magical creatures, and even read the thoughts of their enemies.',
    },
  ]);

  const [selectedCharacter, setSelectedCharacter] = useState(data[0]);

  const getCharacter = (character) => {
    console.log('Character Data', character);

    setSelectedCharacter(character);
  };

  const calcCharTypeColor = (type) => {
    if (type === 'Assault') {
      return 'bg-rose-500';
    } else if (type === 'Medic') {
      return 'bg-cyan-500';
    } else if (type === 'Scout') {
      return 'bg-lime-500';
    } else if (type === 'Tech') {
      return 'bg-indigo-500';
    } else if (type === 'Magic') {
      return 'bg-fuchsia-500';
    }
  };

  return (
    <>
      <div className="container mx-auto">
        <div className="header">
          <div>
            {(selectedCharacter === data.length) === 0 ? (
              <div>
                <p>Loading...</p>
              </div>
            ) : (
              <div key={selectedCharacter.id}>
                <h1>{selectedCharacter.name}</h1>

                <h2>{selectedCharacter.ability}</h2>

                <p>{selectedCharacter.type}</p>

                <p>{selectedCharacter.bio}</p>
              </div>
            )}
          </div>
        </div>

        <main>
          <section className="grid grid-cols-6">
            {data.map((character) => (
              <div
                key={character.id}
                className="character-profile border-solid border-2 border-black"
                onClick={() => getCharacter(character)}
              >
                <img src={character.img} />

                <div className={calcCharTypeColor(character.type)}>
                  <p className="text-white text-center font-bold uppercase">
                    {character.type}
                  </p>
                </div>
              </div>
            ))}
          </section>
        </main>
      </div>
    </>
  );
}
```

![https://res.cloudinary.com/d74fh3kw/image/upload/v1677434974/character-select-ui_qlqh0v.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1677434974/character-select-ui_qlqh0v.jpg)

## Using Livecycle for PR reviews

The code review procedure for developers working on projects hosted on GitHub, GitLab, and Bitbucket can be automated by the application Livecycle. It connects with various platforms and analyses live code changes, giving comments and advice to the developer to increase the quality of the code. Using Livecycle has several advantages, including automating code reviews, which saves developers time and effort by allowing them to more quickly evaluate each other's work. Developers may concentrate on other activities since Livecycle can analyse code changes in a matter of seconds and offer feedback.

By pointing up problems that a human code review may have overlooked, Livecycle may help increase the quality of the code. It can spot possible security holes, performance problems, and other typical code mistakes. This can aid in bug prevention and raise the codebase's general quality. The ability to standardise code across a team is another advantage of adopting Livecycle. In order to make sure that all code is consistent and simple to understand, Livecycle may enforce coding standards and best practises.

Ultimately, by automating the code review process, spotting problems that a human review may have missed, and enforcing coding standards, Livecycle may save time spent and enhance the quality of the code. Teams may work more productively and generate higher-quality code as a result, improving the final output.

### Setting up Livecycle for a Next.js project

Firstly go to [Livecycle](https://livecycle.io/) and create an account. The next step will be to put your project on GitHub. Now with that done if you go to the Livecycle website you can now connect the GitHub repo you just created.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1677347087/livecycle-playground_fmgunq.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1677347087/livecycle-playground_fmgunq.jpg)
The last two steps require you to setup a preview environment and then choose a template depending on the build tool you used. In our case that is going to be Next.js SSG because
its a static website.

**This is the setting up environment screen**
![https://res.cloudinary.com/d74fh3kw/image/upload/v1677436132/livecycle-choose-environment_ufozjz.png](https://res.cloudinary.com/d74fh3kw/image/upload/v1677436132/livecycle-choose-environment_ufozjz.png)
**This is the choosing a template screen**

![https://res.cloudinary.com/d74fh3kw/image/upload/v1677436132/livecycle-setup-environment_bqrncb.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1677436132/livecycle-setup-environment_bqrncb.jpg)

### A quick Livecycle demo

Livecycle can be incorporated and used for different team members. Like for example copywriters can use it for changing text, designers can use it for showing developers a design element that should be changed, testers can use it for showing issues, and developers are able to add new features. These are just a few use cases.

#### Copywriter collaboration example

Lets say that a copywriter wants to make an edit to the application. They can choose to record a video, edit the HTML elements or take a screenshot. Recording a video allows you to show something of relevance, editing HTML elements lets you change the copy on the fly and taking a screenshot obviously takes a picture of the screen.

In this example the copywriter edited the HTML and changed the copy you can see what that looks like in the pictures here.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1677438339/livecycle-copywriter-edit-01_ok1riz.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1677438339/livecycle-copywriter-edit-01_ok1riz.jpg)

![https://res.cloudinary.com/d74fh3kw/image/upload/v1677438339/livecycle-copywriter-edit-02_ln7epe.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1677438339/livecycle-copywriter-edit-02_ln7epe.jpg)

To learn more check out the introduction YouTube video tour [A Guided Tour of Livecycle in 2 minutes and 20 seconds (no captions)](https://www.youtube.com/watch?v=5UsGndLyXXg)

## So... where do I go from here and how can I learn more?

By using these resources below, you can enhance your knowledge and skills in building applications with Next.js and using Livecycle for PR reviews.

1. Next.js Documentation - The official Next.js documentation offers a thorough how-to for developing apps using the framework. Everything is covered, from using the framework for the first time to more complicated subjects like data fetching and server-side rendering.
2. Livecycle Documentation - Use of the tool for code reviews is covered in great length in the official Livecycle documentation. From creating a project to approving and integrating pull requests, it covers it all.
3. React Documentation - Building apps using Next.js requires a solid grasp of React because it is built on top of that framework. The React library is fully described in the official React documentation.
4. Next.js Examples - On their website, Next.js offers a number of examples, one of which is a character choice screen. Building your own Next.js apps might be inspired and aided by these examples.
5. Livecycle Integrations - Livecycle has integrations with several other applications, such as GitHub, Bitbucket, and Slack. You may further streamline your development process by investigating these integrations.

## Conclusion

To recap, this article provided a detailed guide on how to build a character select screen using Next.js and how to use Livecycle for PR reviews. We explained the benefits of using Next.js for server-side rendered applications and walked through the steps to create a character select screen with interactive elements.

Additionally, we explored how Livecycle can automate and streamline the code review process for a Next.js project. We discussed the benefits of using Livecycle and demonstrated how to create, request reviews, approve, and merge a pull request using this tool.

By following the steps outlined in this article, developers can improve the development process and ensure high-quality code for their Next.js projects. Building a user-friendly character select screen and automating the code review process can lead to a better overall user experience, ultimately resulting in a successful project.

Thanks for reading!

If you got value from this article, then you're probably the kind of human who would appreciate the value Livecycle can bring to front end teams and their development workflows. I'd be thrilled if you [tried our SDK](https://www.sdk.livecycle.io/?utm_source=devto&utm_medium=post&utm_campaign=telegram) on one of your own projects and gave it a spin with your team. 🙏
