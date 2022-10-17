One of the most common interview questions is how do you reverse a string in the programming language that you know. Here are a few examples of how easily it can be done. As these programming languages are C based the syntax is quite similar so it is easy to translate across languages.

## Example 1

**JavaScript**

```javascript
function reverse(str) {
	console.log(str.split('').reverse().join(''));
}

reverse('Hello World');
```

**Python**

```python
def reverse(str):
  print(''.join(reversed(str)));


reverse('Hello World');
```

**Dart**

```dart
void main() {
  reverse(str) {
    print(str.split('').reversed.join(''));
  }

  reverse('Hello World');
}
```

## Example 2

**JavaScript**

```javascript
function reverse(str) {
	reversed = '';

	for (let char of str) {
		reversed = char + reversed;
	}
	console.log(reversed);
}

reverse('Hello World');
```

**Python**

```python
def reverse(str):
  reversed = '';
  for char in str:
    reversed = char + reversed;

  print(reversed);


reverse('Hello World');
```

**Dart**

```dart
void main() {
  reverse(str) {
    List newStrings = [];
    dynamic index = (str.length);

    while (index > 0) {
      index -= 1;
      newStrings.add(str[index]);
    }
       print(newStrings.join(""));
  }

  reverse('Hello World');
}
```

## Example 3

**JavaScript**

```JavaScript
function reverse(str) {

	const arr = [];
	for (let i = str.length - 1; i > -1; i--) {
		arr.push(str[i]);
	}
	console.log(arr.join(''));
}

reverse('Hello World');
```

**Python**

```python
def reverse(str):
    new_strings = []
    index = len(str)
    while index:
        index -= 1
        new_strings.append(str[index])
    print(''.join(new_strings))

reverse('Hello World');
```

**Dart**

```dart
void main() {
  reverse(str) {
    List arr = [];
    for (var i = str.length - 1; i > -1; i--) {
      arr.add((str[i]));
    }
    print(arr.join(''));
  }

  reverse('Hello World');
}
```

## Example 4

**JavaScript**

```javascript
function reverse(str) {
	const arr = [];
	for (let i = str.length - 1; i > -1; i--) {
		arr.push(str[i]);
	}

	// Using regex
	console.log(arr.toString().replace(/,/g, ''));

	// Using reduce
	console.log(arr.reduce((acc, cur) => acc + cur));
}

reverse('Hello World');
```

**Python**

```python
def reverse(str):
  print(str[::-1]);


reverse('Hello World');
```

**Dart**

```dart
void main() {
  reverse(str) {
    List arr = [];
    for (var i = str.length - 1; i > -1; i--) {
      arr.add((str[i]));
    }

    // Using Reduce
    print(arr.reduce((acc, curr) => acc + curr));
  }

  reverse('Hello World');
}
```
