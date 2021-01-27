# My initial thoughts on using Flutter and Dart for App development

This is still a technical stack that I am learning so this is not meant to be a deep dive on all of the complexities of the language. It is just my thoughts and experience from working with it so far.

## Dart vs JavaScript

Both languages are based on the C-style of syntax and they are also object-orientated by design. Dart is capable of compiling to either native code or pure JavaScript. One of the biggest differences is that JavaScript is a dynamically typed programming language whereas Dart is a statically typed programming language. With a dynamically typed programming language you are able to change the datatype that a variable holds which allows for more flexibility as you can change things on the fly. Statically typed programming languages are generally safer as you are less likely to run into problems because you for example forgot that a variable was only supposed to hold numbers because it will enforce it for you. 

One thing to note is that Dart also has a datatype called dynamic. What this means is that you can create a variable that does not have a fixed data type. So basically the Dart programming language can be both dynamic and static which makes it very versatile and powerful. So if you want to use Dart for its type safety so that you don't accidentally put in the wrong information then its best to create your variables with the datatype to begin with. Statically typed is generally more preferred as you are more likely to avoid crashes further down the line in your app because of a mix up of datatypes.

### Statically typed programming language

**Dart Programming Language Syntax**

```dart
void main() {
  String userName = 'Kirito';

  int age = 16;

  print(userName);
  // console prints Kirito
  print(age);
  // console prints 16
}
```

### Dynamically typed programming language

**Dart Programming Language Syntax**

```dart
void main() {
  dynamic userName = 'Kirito';

  userName = 123456;

  dynamic age = 16;

  age = '17';

  print(userName);
  // console prints 123456
  print(age);
  // console prints 17
}
```

**JavaScript Programming Language Syntax**

```javascript
  let userName = 'Kirito';

  userName = 123456;

  let age = 16;

  age = '17';

  console.log(userName);
  // console prints 123456
  console.log(age);
  // console prints 17
```

## Dart and JavaScript Classes

Another difference is that the Dart programming language is also a class-based language and while you can use classes in JavaScript it is purely syntactic sugar for the prototypal pattern.

**Dart Programming Language Syntax**

```dart
void main(){
  
  Car ferrari = Car('SF90 Stradale', true);
  print(ferrari.carName);
  // console prints SF90 Stradale
}

class Car {
  String carName;
  bool carAutomatic;
  
  Car(carName, carAutomatic){
    this.carName = carName;
    this.carAutomatic = carAutomatic;
  }
}
```

**JavaScript Programming Language Syntax**

```javascript
class Car {
  constructor(carName, carAutomatic) {
    this.carName = carName;
    this.carAutomatic = carAutomatic;
  }
}

const ferrari = new Car('SF90 Stradale', true);
console.log(ferrari.carName);
// console prints SF90 Stradale
```

## Flutter for App development

Flutter was created by google and is an open-source user interface software development kit. It can be used as a way to develop apps for Android, iOS, Linux, Mac, Windows, Google Fuchsia, and also the web using a single codebase. Coming from a primarily web based background I am used to creating apps using HTML/CSS and JavaScript. However with Flutter you use Widgets for building the user interface. One thing to mention is that the team that created Flutter also works on the Google Chrome Browser so there are quite a lot of similarities. For example when doing styling a lot of the syntax is similar to CSS properties and for doing the layout it uses Flexbox!

So if you are already familiar with it then the learning curve is not going to be too difficult. Another important thing to mention is that Flutter supports hot reload and hot restart. Basically hot restart takes more time than hot reload because it has to destroy and then rebuild the state value as they are returned to default. The app widget tree is completely rebuilt with newly typed code. This can take slightly longer to complete when compared to the hot reload which is the same as it is in web development when you can see your changes immediately without having to restart the server.

**Flutter/Dart syntax example**

 ```dart
import 'package:flutter/material.dart';
import 'package:font_awesome_flutter/font_awesome_flutter.dart';
import 'icon_content.dart';
import 'reusable_card.dart';

const double bottomContainerHeight = 80.0;

const activeCardColour = Color(0xFF1D1E33);
const inactiveCardColour = Color(0xFF111328);

const bottomCardColour = Color(0xFFEB1555);

class InputPage extends StatefulWidget {
  @override
  _InputPageState createState() => _InputPageState();
}

class _InputPageState extends State<InputPage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('BMI CALCULATOR'),
      ),
      body: SafeArea(
        child: Column(
          children: [
            Expanded(
              child: Row(
                children: [
                  Expanded(
                    flex: 2,
                    // Flexbox syntax
                    child: GestureDetector(
                      onTap: () {
                        print('Male Card Pressed');
                        setState(() {});
                      },
                      child: GenderCard(
                        bmiIcon: Icon(FontAwesomeIcons.mars, size: 80.0),
                        bmiIconText: 'Male',
                      ),
                    ),
                  ),
                  Expanded(
                    child: GestureDetector(
                      onTap: () {
                        print('Female Card Pressed');
                      },
                      child: GenderCard(
                        bmiIcon: Icon(FontAwesomeIcons.venus, size: 80.0),
                        bmiIconText: 'Female',
                      ),
                    ),
                  ),
                ],
              ),
            ),
            Expanded(
              child: ReusableCard(colour: activeCardColour),
            ),
            Expanded(
              child: Row(
                children: [
                  Expanded(
                    child: ReusableCard(colour: activeCardColour),
                  ),
                  Expanded(
                    child: ReusableCard(colour: activeCardColour),
                  ),
                ],
              ),
            ),
            Container(
              color: bottomCardColour,
              margin: EdgeInsets.only(top: 10),
              width: double.infinity,
              height: bottomContainerHeight,
            )
          ],
        ),
      ),
    );
  }
}
 ```

## Conclusion

I think that this technical stack is pretty future proofed because it allows you to create cross platform apps for the web, mobile and desktop and the Dart programming language is a joy to use. If you are coming from another C-style programming language then it won't take you long to learn it. I have been using Android Studio for development because the IDE is probably the best way for creating Flutter apps as it has a lot of great plugins and features which make it better than the usual code editor. Don't get me wrong I still have my Visual Studio Code setup for doing Flutter development I just find the experience to be slightly better when using Android Studio.

But nevertheless its still nice to know that you have different options that you can use. Mobile app development is quite cool and I have already got used to using device simulators for testing apps as opposed to using a web browser when creating web apps. One thing I will say though is that the simulators can be pretty resource intensive if your computer is not fast enough. Having the option to also test on your native phone is a good option as its best to see the app running on a real device too.

Cross platform App development is probably best done on a Mac in my opinion because it is the only way to do iOS development. Android studio works on multiple operating systems.