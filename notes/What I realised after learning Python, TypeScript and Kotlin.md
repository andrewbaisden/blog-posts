Remember all those people who kept saying that once you learn one programming/scripting language then it's not too difficult to learn another one? Well, they were telling the truth. I have known Javascript for years and I decided that I should expand my skillset even more because knowing more languages and being a polyglot just makes you better equipped to work in different roles. I would not say that I have mastered any of them yet as its only been a month or so but I have noticed that the languages share many similarities. Here are some examples below in each programming/scripting language.

## Programming Syntax

### Variables

**Python**

```python
welcome = 'Hello World'

print(welcome)
```

**TypeScript**

```typescript
const welcome: string = 'Hello World';

console.log(welcome);
```

**Kotlin**

```kotlin
fun main() {
    val welcome:String = "Hello World"
    println(welcome)
}
```

### Arrays/Lists

**Python**

```python
my_arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

print(my_arr)
```

**TypeScript**

```typescript
const myArr: Number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

console.log(myArr);
```

**Kotlin**

```kotlin
import java.util.*

fun main() {
    val myArr = arrayOf(1,2,3,4,5,6,7,8,9,10)
    println(Arrays.toString(myArr))
}
```

### Objects/Dictionaries

**Python**

```python
my_dict = {
    "id": "1",
    "username": "user01",
    "role": "developer"
}

print(my_dict)
```

**TypeScript**

```typescript
const myObj: { id: number; username: string; role: string } = {
	id: 1,
	username: 'user01',
	role: 'developer',
};

console.log(myObj);
```

**Kotlin**

```kotlin
fun main() {
    val myObj = object {
        var id: Int = 1
        var username: String = "user01"
        var role: String = "developer"
    }
    println(myObj.id)
    println(myObj.username)
    println(myObj.role)
}
```

### Functions

**Python**

```python
def add(x, y):
    return x + y


print(add(7, 3))
```

**TypeScript**

```typescript
function add(x: number, y: number) {
	return x + y;
}

console.log(add(7, 3));
```

**Kotlin**

```kotlin
fun main() {
    fun add(x: Int, y: Int): Int {
        return x + y
    }
    println(add(7, 3))
}
```

### Control Flow: if statements

**Python**

```python
coding_is_fun = True

if coding_is_fun:
    print('Learning to code is fun!!!')
else:
    print('Learning to code is not exciting...')
```

**TypeScript**

```typescript
const codingIsFun = true;

if (codingIsFun) {
	console.log('Learning to code is fun!!!');
} else {
	console.log('Learning to code is not exciting...');
}
```

**Kotlin**

```kotlin
fun main() {
    val codingIsFun: Boolean = true;

    if (codingIsFun) {
        println("Learning to code is fun!!!")
    } else {
        println("Learning to code is not exciting...")
    }

}
```

### Loops

**Python**

```python
shopping_list = ["Shower Gel", "Toothpaste", "Mouth Wash", "Deodorant"]

for item in shopping_list:
    print(item)
```

**TypeScript**

```typescript
const shoppingList: string[] = ['Shower Gel', 'Toothpaste', 'Mouth Wash', 'Deodorant'];

shoppingList.forEach((item) => {
	console.log(item);
});
```

**Kotlin**

```kotlin
fun main() {
  val shoppingList = arrayOf("Shower Gel", "Toothpaste", "Mouth Wash", "Deodorant")

  for (item in shoppingList) {
      println(item)
  }

}
```

### Import Statements

**Python**

```python
from flask import Flask
```

**TypeScript**

```typescript
// ES6 Import
import express from 'express';

// CommonJS
const express = require('express');
```

**Kotlin**

```kotlin
import java.util.*
```

## Conclusion

This was just a sample there are more areas like Classes which I did not mention. When learning all of these different programming languages I noticed many common themes between them. For example the data types are very alike. The way that you assign variables for example feels very similar. Python just lets you write the variable `welcome = 'Hello World'` whereas TypeScript and Kotlin require you to assign it a type first. TypeScript being a superset of JavaScript essentially means that you are still compiling to JavaScript. So assigning `const` and `let` before you write your variables or `var` if you are writing it for ES5. In comparison Kotlin uses `val` and `var` for variable definitions with `val` being the equivalent to `const` as it is immutable and can't be re assigned. The way you write your syntax just feels so familiar so switching between languages is a breeze once you learn the fundamentals.

Also logging to the console is almost exactly the same. Python uses `print()` TypeScript uses `console.log()` and Kotlin uses `println()`. Python and Kotlin are almost the same which makes it easy to remember again. Creating Data Structures like Arrays/Lists, and Objects/Dictionaries is just as simple if you look at the syntax. Interchanging between languages is a breeze. Python Dictionaries look just like JSON so if you know JavaScript this syntax is familiar already.

I was also amazed to see that functions look very much the same. The caveat here being that Python does not use curly braces like TypeScript and Kotlin. Instead you use `:` and you have to be aware of the tab spacing otherwise your code won't compile.

The control flow is much the same writing `if` and `else` syntax works almost exactly the same in all three languages. And when it comes to doing looping you can clearly see that syntax for Python and Kotlin looks almost identical. One pretty big difference between the 3 is that Python uses snack casing for variables such as `first_name` whereas TypeScript and Kotlin use camel case like `firstName`.

Lastly import statements follow a familiar pattern across all 3 languages. I used to believe that learning too many programming languages would lead to yourself becoming confused as you have to remember all of these different syntax and you could find yourself in a scenario where you are writing Kotlin in JavaScript for example which I'm sure has happened to some developers at least once with multiple languages. But actually it just makes you a better coder as you begin to grasp the fundamentals of each language a lot better and your understanding of the core concepts deepens significantly.

So as you can see they are very much alike. Learning multiple languages definitely opens up more doors and allows you to progress further as a developer.
