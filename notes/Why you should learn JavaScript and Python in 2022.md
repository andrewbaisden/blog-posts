# Why you should learn JavaScript and Python in 2022

A new year brings new opportunities for aspiring developers and people who are trying to leave their non tech role so that they can get hired as a developer. One of the most common dilemmas that these people face is figuring out what technical stack to learn and in what direction they should be going when it comes to learning a new programming language from scratch. There are endless options and many different paths that someone could choose to go down.

Arguably two of the most popular and talked about programming languages in the world are JavaScript and Python. If you search for JavaScript and Python job roles on any job board you are highly likely to see hundreds if not thousands of results. The market is and always will be hot for these two highly sought after languages and that is not going to change anytime soon. Both languages share quite a few similarities as well. They are both C based languages which essentially means that they are general purpose, procedural and have lexical scopes among other things.

## Dynamic vs Static

One of the biggest standout points is the fact that JavaScript and Python are dynamically typed languages. In a manner of sense a dynamically typed programming language does not require variables to be explicitly declared prior to their usage. And in the reverse a statically typed programming language prevents variables from getting reassigned to a different type. All of this will become more clear in the examples below.

### Java Example
```java
String myName; // Variable with a type of string
myName = "Tony Stark"; // The string is called Tony Stark
myName = 24; // Reassigning the string into a number
```

If you were to run this Java code you would get either a compile error or runtime error. It is not possible to reassign static types to a different type. You can only use another string like "Steve Rogers".

### JavaScript Example

```javascript
let myName; // Variable that has no type
myName = "Tony Stark"; // The variable has a type of string
myName = 24; // The variable has changed its type dynamically to a number 
```

Now if you were to run this JavaScript code you would get no errors as it is perfectly valid. The variable name is now the number 24.

### Python Example

```python
my_name = "Tony Stark" # The variable has a type of string
my_name = 24 # The variable has changed its type dynamically to an int 
```

Similarly if you were to run this Python code you would also get no errors as it is perfectly valid. The variable name is now the Int 24.

## Data Types

Data types are essentially ways to store data inside of an application. The type of data type specifies what can be stored and how it can be managed. Below you will find a list of some of the data types that each language has.

### JavaScript Data Types

Text Type: string
Numeric Type: number
Boolean Type: boolean
Mapping Type: object
Sequence Type: array

### Python Data Types

Text Type: string
Numeric Type: int, float, complex
Boolean Type: boolean
Mapping Type: dict
Sequence Type: list, tuple, range

## Comparing the syntax

Next we will compare the syntax for both programming languages so you can see how easy it is to transition between the two of them. First let me run through a few differences between the languages.

**JavaScript**

- Uses semicolons
- Uses curly braces for code blocks
- Uses the CamelCase naming convention for variables for example **firstName**
- Uses `console.log` for outputting messages to the console

Functions use this syntax:

```javascript
function myFunc() {
	console.log('Hello World');
}

const myFunc2 = () => {
	console.log('Hello World 2');
};

myFunc();

myFunc2();
```

**Python**

- Does not use semicolons
- Does not use curly braces
- Uses the Snake Case naming convention for variables for example **first_name**
- Uses indentation for code blocks
- Uses `print` for outputting messages to the console

Functions use this syntax:

```python
def my_func():
    print('Hello World')

my_func()
```

### Text

Both languages output a string type variable

#### JavaScript Syntax

```javascript
let myName = "Tony Stark";
console.log(typeof myName); // string
```

#### Python Syntax

```python
my_name = "Tony Stark"
print(type(my_name)) # str
```

### Numeric

In this example both variables output a number in JavaScript

#### JavaScript Syntax

```javascript
let num = 9000;
let num2 = 9.0;
console.log(typeof num); // Number
console.log(typeof num2); // Number
```

#### Python Syntax

In this example Python is able to see the difference between a number and a float because they are built in data types

```python
num = 9000
num_2 = 9.0
print(type(num)) # Int
print(type(num_2)) # Float
```

### Boolean

The output is almost exactly the same the only difference is that JavaScript uses a lowercase "t" for true whereas Python uses an uppercase "T".

#### JavaScript Syntax

```javascript
let wizard = true;
console.log(wizard); // boolean
```

#### Python Syntax

In this example Python is able to see the difference between a number and a float because they are built in data types

```python
wizard = True
print(wizard) # bool
```

### Mapping

JavaScript uses the object data structure whereas Python uses the dictionary data structure. From looking at the examples you can see that they are very alike. The difference is that JavaScript does not require quotes for the keys whereas Python requires them for the keys in the key value pair.

The keys are on the left for example **name** and the values are on the right for example **Tony Stark**.

#### JavaScript Syntax

```javascript
const myprofile = {
	name: 'Tony Stark',
	age: 48,
	superhero: 'Iron Man',
};

console.log(myprofile);
```

#### Python Syntax

```python
my_profile = {
	"name": "Tony Stark",
	"age": 48,
	"superhero": "Iron Man",
};

print(my_profile);
```

### Sequence

JavaScript uses an Array which is a type of object data structure whereas Python uses the list data structure. As you can see they have many similarities in terms of the syntax you write.

#### JavaScript Syntax

```javascript
const myArr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
console.log(typeof myArr); // object
```

#### Python Syntax

```python
myArr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print(type(myArr)) # list
```

## Where to go from here

There are many platforms you can go to if you want to learn JavaScript and Python. Personally I think that freeCodeCamp and Udemy have great courses for both of them. These are the ones that I recommend.

### Learn JavaScript

[https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/)

[https://www.udemy.com/course/the-complete-javascript-course/](https://www.udemy.com/course/the-complete-javascript-course/)

### Learn Python

[https://www.freecodecamp.org/learn/scientific-computing-with-python/](https://www.freecodecamp.org/learn/scientific-computing-with-python/)

[https://www.udemy.com/course/complete-python-developer-zero-to-mastery/](https://www.udemy.com/course/complete-python-developer-zero-to-mastery/)

[https://www.udemy.com/course/complete-python-bootcamp/](https://www.udemy.com/course/complete-python-bootcamp/)
