# Flutter vs. React Native

Today we are going to cover arguably the two biggest and most popular cross platform mobile app development frameworks available at the moment. [Flutter](https://flutter.dev/) and [React Native](https://reactnative.dev/). These two juggernauts are backed by two of the largest tech companies in the world. Flutter was created by Google and React Native was created by Facebook. 

In this article we will compare the two and see what makes them so special and why they are so highly sought after by companies.

## What is Flutter?

Flutter is a cross platform UI framework that was developed by Google. It was first released to the public back in May 2017 and has steadily grown in popularity over the years. One of the main selling points is the fact that developers are able to create cross platform applications using just one codebase. Traditionally if a company wanted to create an application that was available on say the web, mobile and desktop. They would have to use more than one tool to achieve that goal. For example they might need to hire a developer who specialised in web development, then another developer who has desktop app experience. And then a mobile developer who could build apps for iOS and Android.

An example for this use case would be using React for building the website, C# and Java for building the desktop version and then Kotlin and Swift for creating both the iOS and Android apps. This would require a whole team of developers and no doubt a lot of meetings to make sure that the design and branding was consistent across all of them. In addition you also have to factor in testing for each platform too and dealing with their respective bugs and quirks which is common.

Thanks to Flutter one developer can potentially create apps across all of these platforms with just one codebase to manage which would cut down on time and resources. 

## What is React Native?

React Native is a cross platform framework created by Facebook. It makes it fairly simple to create cross platform applications as the codebase is essentially written in JavaScript. This is great because it lowers the bar for entry as it does not require a JavaScript developer to learn a completely unfamiliar language. Web development has been around for many years and as such there are thousands of web developers who have been using JavaScript for much of their career. Mobile development is still fairly new even though the ecosystem has really matured over the past few years. If a developer already knows JavaScript then the learning curve for mobile app development using React Native won’t be as taxing.

These days many companies are using React Native for app development. Microsoft recently developed their new Xbox store app using React Native which goes to show just how much confidence companies have in using it. Just like Flutter it is also possible to create apps across various platforms using one codebase.

## What is the difference between Flutter and React Native?

Both of these frameworks share quite a lot of similarities however there are quite a few differences between the two of them. For starters Flutter uses the Dart programming language in its codebase when you are developing apps. Whereas React Native uses JSX which stands for JavaScript XML. One thing to note is that both languages are based on the C-style type of syntax and they follow object orientated principles. Because of this common ground it means that they are both fundamentally similar in terms of design and the code is very alike.

**Dynamic Programming vs. Static Programming**

However there is a significant difference when it comes to the core programming language. JavaScript for example is dynamic by nature which means that you can change the values of various data types when needed which makes it very versatile. Dart is both dynamic and static which allows it to have the best of both worlds. A statically typed language is generally considered to be much safer as it enforces you to declare and use the correct data type. For example you can’t assign a number to a string as that will throw an error. Being static means you are likely to experience less errors. It is possible to enforce more type safety and error checking with JavaScript though if you opt to use TypeScript instead which is a strict syntactical superset of JavaScript.

**Layout**

Another common difference is in the way in which both frameworks are used to build apps. Flutter uses a widget style for constructing the user interface whereas React Native uses JavaScript and JSX. These widgets are pre made by the development team at Google as well as other developers so you don’t technically need to create your own custom widgets unless you want to. 

This can make development quite easy and you don’t need to worry too much about a widget not being compatible as they are official and have been tested by Google. One thing I should mention is that if you are using a programming language like Swift for mobile app development you typically can’t see the code that Apple used for creating user interface components like a button. But with Flutter it is possible to see how Google created all the widgets as the code is viewable.

Flutter and React Native do share common ground when it comes down to constructing the layout of apps however. They both use CSS Flex Box for the layout. The way they implement it is different though but as long as you know Flex Box you should not have problems building the layout for your app. The development team that worked on Flutter also worked on the developer tools for the Google Chrome browser so there are quite a few similarities which makes for a quick transition as the debug tools are quite similar.

## Why is mobile app development so popular?

Mobile app development has been growing steadily year by year. Almost everyone on the planet has a mobile phone which is why the user base is massive. These days you can find an app for almost anything. There are quite a few paths a developer could take if they wanted to create a mobile app. They could choose to go down the native route which would mean using Swift to create mobile apps or Kotlin to create Android apps. These are the official programming languages Apple and Google use so you can expect first party support and frequent updates.

Or you could choose to go down the cross platform path and go with Flutter and React Native. Typically a native developer would use Xcode and Swift for making iOS apps and Android Studio and Kotlin for creating Android apps. These tools are also applicable for cross platform work too. It is also quite common for developers to use an Integrated development environment (IDE) like Visual Studio Code for building apps.

I think in most cases people tend to use an IDE, Android Studio or Xcode when building apps with Flutter and React Native. Personally my preference is to use Visual Studio Code for React Native apps and Android Studio for Flutter apps. Android Studio actually has a Flutter plugin which has code helpers so it is much easier to write and debug your code. As of right now this plugin has 8.3 million downloads which goes to show just how popular it is.

React is probably slightly more popular at the moment because you have to take into account that there is a version for the web called React and also the version for creating mobile apps called React Native. Plus it has been around longer than Flutter so the user base is larger. There are also a lot more companies looking for React developers than there are for Flutter right now.

## How do both frameworks compare in terms of performance?

These two frameworks are open source which means that they are free to use for everyone. Both libraries are well maintained as you would expect considering they are created by Google and Facebook. It is possible to test apps created using both frameworks either virtually using a built in simulator on your computer for iOS and Android, or natively on your phone. One thing to mention though is that you will need an Apple computer if you intend on developing on iOS as the software development kit (SDK) is only available on Apple computers. So Windows users and Linux users are out of luck. Fortunately Android development can be done on either of the three.

Both frameworks use Hot Reloading so developers are able to make changes and see them instantly. This is great because it means faster development times because you don’t have to keep stopping and starting your apps to see updates. A concern many people have is if you can truly consider Flutter and React Native apps as being truly native. To be considered 100% native they would need to be written in the language that they were designed for. Swift for iOS and Kotlin/Java for Android. 

The experience you get when using an app that was created in React Native and Flutter is for the most part a native experience. The Dart code which Flutter uses is complied to “C” which is about as close to native as you can expect. Taking this into consideration you could assume that would mean it offers the better performance.

The company who created the app Reflecty, moved their app from React Native to Flutter and saw a big increase in performance which you can read [here](https://medium.com/reflectly-engineering/reflectly-from-react-native-to-flutter-2e3dffced2ea). This is one example of an improvement however please realise that this won’t be the same for every app as there are many cases that you need to take into account. Like the type of app, codebase, database, the phone and operating system that the user has etc…

## Comparing the developer ecosystems of both frameworks

Developers who are keen on building Flutter apps are likely to use the [official documentation](https://flutter.dev/). However in the case of React Native you have different options. You could use the [official documentation](https://reactnative.dev/) or you could use a different platform. The most popular one being [Expo](https://expo.io/). Expo offers more features and customisation whereas the official documentation is more barebones. This includes an integrated icon library. Both options are good nonetheless.

In terms of ecosystems React Native is more mature with more users because JavaScript has been around since 1995 whereas Flutter was released in 2017. React is probably the most popular front end framework at the moment and has a very active community across social media. Flutter is no slouch though because as of right now it has more stars than React Native on GitHub.

Both frameworks have been used to create many popular commercial applications. To name a few, Flutter has been used to create the apps for Reflectly, Stadia, Baidu, Groupon and eBay. Whereas React Native has been used to create the apps for, Facebook, Instagram, Shopify and Discord. You can see the full list of apps for Flutter and React Native below.

[Flutter app showcase](https://flutter.dev/showcase)

[React Native app showcase](https://reactnative.dev/showcase)

Across social media the numbers are fairly similar too with Flutter having more followers on Twitter and React Native having more followers on Reddit.

**GitHub**

![img](https://res.cloudinary.com/d74fh3kw/image/upload/v1616432348/github-flutter_cfusnb.png)

![img](https://res.cloudinary.com/d74fh3kw/image/upload/v1616432348/github-reactnative_aq5kkf.png)

**Twitter**

![img](https://res.cloudinary.com/d74fh3kw/image/upload/v1616432349/twitter-flutter_ssxl0t.png)

![img](https://res.cloudinary.com/d74fh3kw/image/upload/v1616432348/twitter-reactnative_j9ti0b.png)

**Reddit**

![img](https://res.cloudinary.com/d74fh3kw/image/upload/v1616432795/reddit-flutter_caw0yd.png)

![img](https://res.cloudinary.com/d74fh3kw/image/upload/v1616432348/reddit-reactnative_mmuvlr.png)

## App Development

Let’s run through some quick code examples of what it looks like to create an app using Flutter and React Native. The app is called ‘Social’ and it has two screens. The iOS and Android versions look identical. The images below show you how it looks on an iPhone.

![img](https://res.cloudinary.com/d74fh3kw/image/upload/v1616511713/ios-social-app-home_ollffu.png)

![img](https://res.cloudinary.com/d74fh3kw/image/upload/v1616511711/ios-social-app-profile_hft0lf.png)

**Flutter code examples**

Flutters architecture of using widgets is quite unique compared to traditional programming methodologies. But once you understand how it works it becomes second nature.

![img](https://res.cloudinary.com/d74fh3kw/image/upload/v1616530888/flutter-project_vi1j0h.png)

**main.dart File**

```
import 'package:flutter/material.dart';
import 'package:social_app/screens/home_screen.dart';
import 'package:social_app/screens/profile_screen.dart';
void main() {
 runApp(Social());
}
class Social extends StatelessWidget {
 *@override*
 Widget build(BuildContext *context*) {
  return MaterialApp(
   *initialRoute*: HomeScreen.**id**,
   *routes*: {
    HomeScreen.**id**: (*context*) => HomeScreen(),
    ProfileScreen.**id**: (*context*) => ProfileScreen(),
   },
  );
 }
}
```

**home_screen.dart File**

```
import 'package:flutter/material.dart';
import 'package:social_app/screens/profile_screen.dart';
class HomeScreen extends StatelessWidget {
 static String **id** = 'home_screen';
 *@override*
 Widget build(BuildContext *context*) {
  return Scaffold(
   *backgroundColor*: Color(0xffb0c1957),
   *appBar*: AppBar(
    *toolbarHeight*: 40,
    *title*: Text(
     'Social',
     *style*: TextStyle(
       *color*: Colors.**black**, *fontSize*: 16, *fontWeight*: FontWeight.**bold**),
    ),
    *backgroundColor*: Colors.**white**,
   ),
   *body*: Column(
    *mainAxisAlignment*: MainAxisAlignment.spaceBetween,
    *children*: [
     Container(
      *width*: 400,
      *margin*: EdgeInsets.only(*top*: 20),
      *child*: RaisedButton(
       *color*: Color(0xff23397B),
       *padding*: EdgeInsets.all(20),
       *onPressed*: () {
        Navigator.**push**(*context*,
          MaterialPageRoute(*builder*: (*context*) => ProfileScreen()));
       },
       *child*: Text(
        'PROFILE',
        *style*:
          TextStyle(*color*: Colors.**white**, *fontWeight*: FontWeight.**bold**),
       ),
      ),
     ),
     SizedBox(
      *height*: 1,
     ),
     Container(
      *child*: Center(
       *child*: Text(
        'HOME',
        *style*: TextStyle(
          *fontSize*: 40,
          *color*: Colors.**white**,
          *fontWeight*: FontWeight.**bold**),
       ),
      ),
     ),
     Container(
      *child*: Image(
       *image*: AssetImage('images/home-bg.jpg'),
      ),
     ),
    ],
   ),
  );
 }
}
```

**profile_screen.dart File**

```
import 'package:flutter/material.dart';
import 'package:social_app/screens/home_screen.dart';
class ProfileScreen extends StatelessWidget {
 static String **id** = 'profile_screen';
 *@override*
 Widget build(BuildContext *context*) {
  return Scaffold(
   *backgroundColor*: Color(0xffb0c1957),
   *appBar*: AppBar(
    *toolbarHeight*: 40,
    *title*: Text(
     'Social',
     *style*: TextStyle(
       *color*: Colors.**black**, *fontSize*: 16, *fontWeight*: FontWeight.**bold**),
    ),
    *backgroundColor*: Colors.**white**,
   ),
   *body*: Column(
    *mainAxisAlignment*: MainAxisAlignment.start,
    *children*: [
     Container(
      *width*: 400,
      *margin*: EdgeInsets.only(*top*: 20),
      *child*: RaisedButton(
       *color*: Color(0xff23397B),
       *padding*: EdgeInsets.all(20),
       *onPressed*: () {
        Navigator.**push**(*context*,
          MaterialPageRoute(*builder*: (*context*) => HomeScreen()));
       },
       *child*: Text(
        'HOME',
        *style*:
          TextStyle(*color*: Colors.**white**, *fontWeight*: FontWeight.**bold**),
       ),
      ),
     ),
     SizedBox(
      *height*: 50,
     ),
     Container(
      *child*: Center(
       *child*: Text(
        'PROFILE',
        *style*: TextStyle(
          *fontSize*: 40,
          *color*: Colors.**white**,
          *fontWeight*: FontWeight.**bold**),
       ),
      ),
     ),
     SizedBox(
      *height*: 20,
     ),
     Container(
       *child*: CircleAvatar(
      *radius*: 130.0,
      *backgroundImage*: AssetImage('images/profile-image.jpg'),
     )),
     SizedBox(
      *height*: 20,
     ),
     Container(
      *child*: Text(
       'SARAH TAYLOR',
       *style*: TextStyle(
         *color*: Colors.**white**,
         *fontSize*: 20,
         *fontWeight*: FontWeight.**bold**),
      ),
     ),
     SizedBox(
      *height*: 20,
     ),
     Container(
      *color*: Color(0xff000d4a),
      *padding*: EdgeInsets.all(18.0),
      *child*: Container(
       *child*: Text(
        "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla ut ultricies velit. Proin at nisi nisl. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Etiam eu tincidunt dui. Quisque non ornare ex, facilisis congue enim. In neque nulla, posuere at gravida id, dapibus et libero.",
        *style*: TextStyle(
         *color*: Colors.**white**,
         *fontSize*: 17,
        ),
       ),
      ),
     )
    ],
   ),
  );
 }
}
```

**React Native code examples**

If you already know React for the web then the code here is going to look very familiar to you. The architecture for setting up a React Native project is almost the same.

**Project Structure**

![img](https://res.cloudinary.com/d74fh3kw/image/upload/v1616509955/react-native-project_ofhsxl.png)

**App.js File**

```
// Import statements for the components used in the app and the navigation
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
const Stack = createStackNavigator();
import HomeScreen from './src/screens/HomeScreen';
import ProfileScreen from './src/screens/ProfileScreen';
// The main component with all of the screen routing business logic
const App = () => {
  return (
    <*NavigationContainer*>
      <*Stack.Navigator* *initialRouteName*="HomeScreen" *screenOptions*={{ gestureEnabled: false }}>
        <*Stack.Screen* *name*="HomeScreen" *component*={HomeScreen} *options*={{ title: 'Social' }} />
        <*Stack.Screen* *name*="ProfileScreen" *component*={ProfileScreen} *options*={{ title: 'Social' }} />
      </*Stack.Navigator*>
    </*NavigationContainer*>
  );
};
export default App;
```

**Home.js File**

```
// Import statements for the components used in the app
import React from 'react';
import { View, Text, StyleSheet, TouchableOpacity, Image } from 'react-native';
import HomeBG from '../../assets/home-bg.jpg';
// The main component for the HomeScreen
const HomeScreen = ({ *navigation* }) => {
  return (
    <*View* *style*={styles.appStyle}>
      <*TouchableOpacity*
        *style*={styles.btnContainer}
        *title*="Profile"
        *onPress*={() => *navigation*.navigate('ProfileScreen')}
      >
        <*Text* *style*={styles.btnText}>Profile</*Text*>
      </*TouchableOpacity*>
      <*Text* *style*={styles.heading}>Home</*Text*>
      <*View*>
        <*Image* *style*={styles.homeBG} *source*={HomeBG} />
      </*View*>
    </*View*>
  );
};
// The component specific styles for the HomeScreen
const styles = *StyleSheet*.create({
  appStyle: {
    backgroundColor: 'rgb(12,25,87)',
    height: '100%',
  },
  btnContainer: {
    backgroundColor: '#23397B',
    padding: 20,
    justifyContent: 'center',
    alignItems: 'center',
    marginHorizontal: 20,
    marginVertical: 20,
  },
  btnText: {
    color: '#ffffff',
    fontWeight: 'bold',
    textTransform: 'uppercase',
  },
  heading: {
    fontSize: 40,
    color: '#ffffff',
    textAlign: 'center',
    margin: 20,
    fontWeight: 'bold',
    textTransform: 'uppercase',
  },
  homeBG: {
    height: '100%',
    width: '100%',
  },
});
export default HomeScreen;
```

**ProfileScreen.js**

```
// Import statements for the components used in the app
import React from 'react';
import { View, Text, StyleSheet, TouchableOpacity, Image } from 'react-native';
import ProfileImage from '../../assets/profile-image.jpg';
// The main component for the ProfileScreen
const ProfileScreen = ({ *navigation* }) => {
  return (
    <*View* *style*={styles.appStyle}>
      {/* TouchableOpacity is basically a more customizable button component */}
      <*TouchableOpacity* *style*={styles.btnContainer} *title*="Profile" *onPress*={() => *navigation*.navigate('HomeScreen')}>
        <*Text* *style*={styles.btnText}>Home</*Text*>
      </*TouchableOpacity*>
      <*Text* *style*={styles.heading}>Profile</*Text*>
      <*View* *style*={styles.profileContainer}>
        <*Image* *style*={styles.profileImage} *source*={ProfileImage} />
      </*View*>
      <*View*>
        <*Text* *style*={styles.profileName}>Sarah Taylor</*Text*>
      </*View*>
      <*View* *style*={styles.profileBioContainer}>
        <*Text* *style*={styles.profileBio}>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla ut ultricies velit. Proin at nisi nisl. Class
          aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Etiam eu tincidunt dui.
          Quisque non ornare ex, facilisis congue enim. In neque nulla, posuere at gravida id, dapibus et libero.
        </*Text*>
      </*View*>
    </*View*>
  );
};
// The component specific styles for the ProfileScreen
const styles = *StyleSheet*.create({
  appStyle: {
    backgroundColor: 'rgb(12,25,87)',
    height: '100%',
  },
  btnContainer: {
    backgroundColor: '#23397B',
    padding: 20,
    justifyContent: 'center',
    alignItems: 'center',
    marginHorizontal: 20,
    marginVertical: 20,
  },
  btnText: {
    color: '#ffffff',
    fontWeight: 'bold',
    textTransform: 'uppercase',
  },
  heading: {
    fontSize: 40,
    color: '#ffffff',
    textAlign: 'center',
    margin: 20,
    fontWeight: 'bold',
    textTransform: 'uppercase',
  },
  profileContainer: {
    alignItems: 'center',
  },
  profileImage: {
    borderRadius: 100,
    height: 250,
    width: 250,
  },
  profileName: {
    color: '#ffffff',
    fontSize: 20,
    textAlign: 'center',
    fontWeight: 'bold',
    margin: 20,
    textTransform: 'uppercase',
  },
  profileBioContainer: {
    backgroundColor: 'rgba(0,13,74,0.4234068627450981)',
  },
  profileBio: {
    marginHorizontal: 20,
    marginVertical: 20,
    color: '#ffffff',
    fontSize: 18,
  },
});
export default ProfileScreen;
```

## Final Thoughts

There is no winner here both frameworks have their pros and cons. If you already know JavaScript then it is a no brainer to go down the route of React Native. However if you want to try something different which might offer slightly better performance, stability and a more cohesive environment between ecosystems give Flutter a try. 