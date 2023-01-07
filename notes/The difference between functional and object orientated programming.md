_If you enjoy this topic, you will probably like my articles, tweets, and stuff. If you're wondering, check out my [social media profiles](https://limey.io/andrewbaisden) and don't forget to subscribe and follow since I'm offering programming and motivating tools and information to help you achieve your dreams._

## An introduction to programming languages

There are many different types and styles of programming languages, and each has its own benefits and shortcomings. Functional programming and object-oriented programming are two of the most widely used programming paradigms. Today, we'll go over the main distinctions between the two paradigms of programming and how each may be utilised to create effective software solutions.

## What is Functional Programming

A programming paradigm known as "functional programming" focuses on the creation of larger, more complicated functions by combining smaller functions. Functional programming is founded on the premise that a programme is made up of functions that may be coupled and evaluated to achieve a result, avoiding the need of state and mutable data. Declarative code, or code that specifies what the programme should do rather than how it should accomplish it, is another key component of functional programming.

## What is Object-Oriented Programming

The goal of object-oriented programming (OOP), a programming paradigm, is to build programmes by constructing objects that communicate with one another. The foundation of OOP is the concept that an object should include both data and the methods available for manipulating that data. Reusing existing code, which is the habit of writing code that can be used in other settings, is another thing that OOP promotes.

## How the two compare in a JavaScript example

Here is an example of a simple "Game" class in JavaScript that demonstrates some of the key differences between functional and object-oriented programming:

### Object-Oriented Programming example:

```javascript
class Game {
  // A class serves as an object creation template. It explains the characteristics and actions that objects belonging to the class will possess.
  constructor(name, release) {
    // When an object is generated from a class, a particular method called the function Object() { [native code] } is invoked. It is utilised to configure the object's initial state.
    this.name = name;
    this.release = release;
  }

  show() {
    // This function belongs to the Game class. It may be invoked on any object that is a class instance.
    console.log(`${this.name}, was released in the year ${this.release}.`);
  }
}

const mw2 = new Game('Call of Duty: Modern Warfare II', 2022);
// The "new" keyword produces a new Game class object. To build the object, the function Object() { [native code] } method is used with the inputs "Call of Duty: Modern Warfare II" and 2022.

mw2.show();
// The Output is "Call of Duty: Modern Warfare II, was released in the year 2022."
```

### Functional Programming example:

```javascript
function createGame(name, release) {
  // This function produces an object with the specified properties as a result. It doesn't have methods like a class or utilise the term "this."
  return {
    name: name,
    release: release,
  };
}

const mw2 = createGame('Call of Duty: Modern Warfare II', 2022);
// The object is created by invoking the createGame function with the parameters "Call of Duty: Modern Warfare II" and 2022.

console.log(`${mw2.name}, was released in the year ${mw2.release}.`);
// The Output is Call of Duty: Modern Warfare II, was released in the year 2022."
```

You define a class in object-oriented programming (OOP) that acts as a template for constructing objects. The class can have methods (class-specific procedures) and attributes (variables that belong to the class). Objects are formed from the class by using the "new" keyword, and they inherit the class's methods and attributes.

You define functions in functional programming that accept inputs and return outputs. These functions can be used to generate and handle objects, but the objects themselves do not have methods or attributes like objects in OOP. Instead, you directly access the object's attributes.

## Final thoughts

Two of the most well-liked programming paradigms, functional programming and object-oriented programming, each have their own benefits and limitations. Functional programming prioritises composition and declarative code, whereas object-oriented programming prioritises abstraction, reuse, and encapsulation. The requirements of the project will ultimately determine which programming paradigm to utilise.

_If you like this article, chances are that you would like my posts, tweets and content as well. If you are curious, have a look at my [social media profiles](https://limey.io/andrewbaisden) and don't forget to subscribe and follow because I am sharing programming and motivation resources and knowledge to support you in achieving your goals 💫_
