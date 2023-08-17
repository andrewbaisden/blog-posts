## Introduction

Mapbox is a technology startup that provides developers and organisations with configurable and high-performance mapping, geospatial, and location-based services. They provide a suite of tools and APIs for developing interactive maps, geocoding, navigation, routing, and other location-based applications.

The platform is based on open data and open-source software, allowing developers to access and utilise maps, add unique styles, and integrate location features into their apps, websites, and other digital goods. Vector tiles power Mapbox's maps, allowing for rapid loading and seamless interactions.

Today, we will be using the [Mapbox Maps SDK for React Native](https://github.com/rnmapbox/maps) and the popular React Native command-line tool [Expo CLI](https://docs.expo.dev/get-started/installation/) for building a React Native mobile app that has Mapbox integration. Before starting this tutorial ensure that your development environment is set up and working. Just install and set up the tools and services in the prerequisites section.

I will be using a Mac for development however it is possible to use Windows, Linux and physical Android and iOS devices too if you want. Although iOS development and deployment require macOS so just bear that in mind if you ever plan on publishing apps to the Apple App Store. Android apps can be created on macOS, Windows, and Linux.

## Prerequisites

If you are developing on iOS then an [Apple Developer Account](https://developer.apple.com/) is required because the [mapbox](https://www.mapbox.com/) package needs [custom native code](https://github.com/rnmapbox/maps/blob/main/plugin/install.md) and the setup will ask you to sign into your Apple Developer account which is why you have to create one. Apple Developer accounts are not free you have to enrol and pay an annual fee to develop iOS apps. The fee is less than $100 as of writing.

Install and setup the below tools and services:

- [Apple Developer Account](https://developer.apple.com/) (create an account)
- [Expo CLI](https://docs.expo.dev/get-started/installation/) (install and configure)
- [Node and npm](https://nodejs.org/en) (I used Node version 18.15.0 LTS however the latest version should work fine)
- [mapbox](https://www.mapbox.com/) (create an account)
- [Expo Go Mobile App](https://expo.dev/client)

**Optional**

If you plan on developing apps for Android or testing on an Android simulator then you will need to install and set up [Android Studio](https://developer.android.com/studio) on your computer beforehand. Also testing on an iOS physical device requires [Enabling Developer Mode on a device](https://developer.apple.com/documentation/xcode/enabling-developer-mode-on-a-device).

## Project setup

Let's now set up our project. Navigate into a directory using the command line and then initiate the commands below to scaffold an Expo project.

```shell
npx create-expo-app mapbox-app
cd mapbox-app
```

Next install the mapbox package.

```shell
npm i @rnmapbox/maps
```

Now open the project in your IDE of choice and add this code to the bottom of the `app.json` file.

```json
{
  "expo": {
    "plugins": [
      [
        "@rnmapbox/maps",
        {
          "RNMapboxMapsImpl": "mapbox",
          "RNMapboxMapsDownloadToken": "sk.ey...qg"
        }
      ]
    ]
  }
}
```

You will now need to create an access token which will replace the "sk.ey...qg" string in the json file under the `RNMapboxMapsDownloadToken`. Sign into your mapbox account and find the Tokens page in the menu.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1679585541/mapbox-access-token-create_yp5azi.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1679585541/mapbox-access-token-create_yp5azi.jpg)

Create a token with the selections in the picture. It is important that DOWNLOADS:READ is selected because when you are building with Expo it will allow it to download mapbox into the Expo project.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1679585541/mapbox-access-token_gh8nyz.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1679585541/mapbox-access-token_gh8nyz.jpg)

Copy and paste your newly created token into the `app.json` file in the key value pair like in this example.

```json
{
  "expo": {
    "plugins": [
      [
        "@rnmapbox/maps",
        {
          "RNMapboxMapsImpl": "mapbox",
          "RNMapboxMapsDownloadToken": "put your access token here"
        }
      ]
    ]
  }
}
```

It's now time for us to create a simple map in our application so that we can see if everything is configured properly and working. So copy and paste the following code and put it into your `app.js` file.

```javascript
import 'expo-dev-client';

import React from 'react';

import { StyleSheet, View } from 'react-native';

import Mapbox from '@rnmapbox/maps';

Mapbox.setAccessToken('put your public access token here');

const App = () => {
  return (
    <View style={styles.page}>
      <View style={styles.container}>
        <Mapbox.MapView style={styles.map} />
      </View>
    </View>
  );
};

export default App;

const styles = StyleSheet.create({
  page: {
    flex: 1,

    justifyContent: 'center',

    alignItems: 'center',
  },

  container: {
    height: 300,

    width: 300,
  },

  map: {
    flex: 1,
  },
});
```

We require another access token for mapbox in our `app.js` file. Go back to your mapbox account and copy and paste your Default public token and replace the string in the code in the `app.js` file here.

```javascript
Mapbox.setAccessToken('put your public access token here');
```

### EAS Build setup

**EAS Build** is basically a hosted service which is used for building app binaries in Expo and React Native projects. You can learn more here [EAS Build](https://docs.expo.dev/build/introduction/). To manage your native projects, EAS Builds are recommended. It provides a seamless experience, particularly if you are unfamiliar with Xcode and Android studio builds or do not have them installed locally on your PC. This is another required setup before we can start working on our project. It can be a bit of a chore but then its smooth sailing and no more setup blockers from here on out.

First we have to setup our project to [create development builds](https://docs.expo.dev/development/create-development-builds/). It's recommended to install EAS CLI globally so run the command here.

```shell
npm install -g eas-cli
```

Make sure that you are inside of the root folder for the **mapbox-app** project and run the command below to initialise a development build.

```shell
npx expo install expo-dev-client expo-location
```

Add this code inside of the newly created `eas.json` file with the code here. We are adding a new object for the development-simulator.

```json
{
  "build": {
    "development-simulator": {
      "developmentClient": true,
      "distribution": "internal",
      "ios": {
        "simulator": true
      }
    }
  }
}
```

Next run this command to create the development build on an IOS Simulator and go through the steps.

```shell
eas build --profile development-simulator --platform ios
```

This step can take a long time to complete because it needs to build everything. You can check the progress by clicking on the **Build details:** link in the command line.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1679587933/map-box-build_qx3xmx.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1679587933/map-box-build_qx3xmx.jpg)

![https://res.cloudinary.com/d74fh3kw/image/upload/v1679587933/ios-box-simulator-build_dvvqgw.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1679587933/ios-box-simulator-build_dvvqgw.jpg)

Wait for the build to complete and then start your Expo project with the development server command. Open with iOS and you should see the iOS Simulator with a map on the screen.

```shell
npx expo start --dev-client
```

For getting the app to run on a physical iOS or Android device you can follow the steps here [https://docs.expo.dev/development/create-development-builds/](https://docs.expo.dev/development/create-development-builds/) under the **On a device** section.

We are finally done with the setup let's move on to the next section.

## Customising the Mapbox app

### Adding custom markers and popups

We can create custom markers to represent a point on our map. First, lets learn about 3 Mapbox structures. These are MapView, Camera and PointAnnotation.

**MapView**
MapView is the embeddable map interface that is used for showing all of the map data. In our codebase, we are using the class `Mapbox.MapView` as the main wrapper component.

**Camera**
With Mapbox maps, the camera represents the map's field of view. The viewport of the camera is governed by numerous elements, including the centre, zoom level, pitch, and bearing.

**PointAnnotation**
PointAnnotation essentially puts a point on our map which is determined by the coordinates we have set in the state value `const [coordinates] = useState([-5, 55]);`. It uses longitude and latitude to determine where on the map the point should be placed.

Now replace the code in the `App.js` file with this one. And don't forget to save your access token because you will need to add it to the new code at the top.

```javascript
import 'expo-dev-client';

import React, { useState } from 'react';

import { StyleSheet, View } from 'react-native';

import Mapbox from '@rnmapbox/maps';

Mapbox.setAccessToken('put your token here');

const App = () => {
  const [calloutVisible, setCalloutVisible] = useState(false);

  const [coordinates] = useState([-5, 55]);

  const onMarkerPress = () => {
    setCalloutVisible(true);
  };

  const loadAnnotationUK = () => {
    return (
      <Mapbox.PointAnnotation
        key="annotationUK"
        id="annotationUK"
        coordinate={[0.1, 51.5]}
        onSelected={onMarkerPress}
      >
        <View
          style={{
            height: 20,

            width: 20,

            backgroundColor: 'green',

            borderColor: 'black',

            borderWidth: 2,

            borderRadius: 50,
          }}
        ></View>

        <Mapbox.Callout
          title="Welcome to London!"
          contentStyle={{ borderRadius: 5 }}
        ></Mapbox.Callout>
      </Mapbox.PointAnnotation>
    );
  };

  return (
    <View style={styles.page}>
      <View style={styles.container}>
        <Mapbox.MapView style={styles.map}>
          <Mapbox.Camera zoomLevel={4} centerCoordinate={coordinates} />

          <Mapbox.PointAnnotation id="uk" coordinate={coordinates} />

          <View>{loadAnnotationUK()}</View>
        </Mapbox.MapView>
      </View>
    </View>
  );
};

export default App;

const styles = StyleSheet.create({
  page: {
    flex: 1,

    justifyContent: 'center',

    alignItems: 'center',
  },

  container: {
    height: '100%',

    width: '100%',
  },

  map: {
    flex: 1,
  },
});
```

What we have just done is create a function for creating a custom pointer that has a callout that is displayed when you click on it. We have also made the map full-screen so it is no longer cropped in the middle. Reload the application by hitting the "R" button in the command line for the Expo app and it will update. You should now see a full-screen map with a custom pointer marker on London in the UK. Clicking on it will bring up a callout box.

### Displaying a user’s location

Displaying a user's location is very common inside of map applications so let's run through a quick demo. We will now be using the `expo-location` package to detect a user's location. Just a quick note whenever you install a new package in Expo you will have to rebuild the application over again using this command `eas build --profile development-simulator --platform ios` or the Android command. It can be quite time-consuming however this is the build process for developing mobile apps with EAS.

Replace all of the code in the `App.js` file with this code. Like before transfer your token over as well.

```javascript
import 'expo-dev-client';

import React, { useState, useEffect } from 'react';

import { StyleSheet, View } from 'react-native';

import Mapbox from '@rnmapbox/maps';

import * as Location from 'expo-location';

Mapbox.setAccessToken('put your token here');

const App = () => {
  const [location, setLocation] = useState(null);

  useEffect(() => {
    (async () => {
      const { status } = await Location.requestForegroundPermissionsAsync();

      if (status !== 'granted') {
        console.error('Permission to access location was denied');

        return;
      }

      const currentLocation = await Location.getCurrentPositionAsync({});

      setLocation(currentLocation.coords);
    })();
  }, []);

  return (
    <View style={styles.container}>
      {location && (
        <Mapbox.MapView style={styles.map} styleURL={Mapbox.StyleURL.Street}>
          <Mapbox.Camera
            zoomLevel={15}
            centerCoordinate={[location.longitude, location.latitude]}
            animationMode="flyTo"
            animationDuration={2000}
          />

          <Mapbox.PointAnnotation
            id="userLocation"
            coordinate={[location.longitude, location.latitude]}
            title="Your location"
          />
        </Mapbox.MapView>
      )}
    </View>
  );
};

export default App;

const styles = StyleSheet.create({
  container: {
    flex: 1,

    backgroundColor: '#fff',
  },

  map: {
    flex: 1,
  },
});
```

Reload the application and open it again in the iOS Simulator and you should see a dialogue that asks you to allow "mapbox-app" and to use the location so allow it. The map should load a location on the simulated iPhone. 

You can choose your own location or one listed using the iOS Simulator menu which is how you handle permissions when requesting a user's location on iOS. It's possible to spoof a location and create a virtual one. See the screenshots below for an example of how to do this. With the help of Google maps or a search engine, you can find the longitude and latitude of any location on earth.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1679684498/ios-simulator-menu_ywjbpc.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1679684498/ios-simulator-menu_ywjbpc.jpg)

![https://res.cloudinary.com/d74fh3kw/image/upload/v1679684497/ios-simulator-long-lat_skpzrj.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1679684497/ios-simulator-long-lat_skpzrj.jpg)

## Final thoughts

Creating custom maps with React Native Mapbox provides a strong and versatile method for introducing interactive and aesthetically appealing maps into your mobile applications. Developers can create feature-rich location-based experiences suited to their specific needs by utilising Mapbox's vast ecosystem and React Native's cross-platform capabilities. We've discussed the advantages of utilising React Native Mapbox throughout this article, including its customisability, and compatibility with both iOS and Android platforms. Developers can accomplish a seamless integration of mapping services with the React Native environment by implementing Mapbox APIs.

Lastly, don't forget to take use of the thriving development communities that surround both React Native and Mapbox. There are several tools, tutorials, and examples available to assist you in overcoming obstacles and learning best practises in designing custom maps for your applications. The possibilities for developing compelling, location-based experiences are nearly unlimited when you have the strong combination of React Native and Mapbox at your disposal. So, go ahead and let your imagination run wild to create personalised maps that actually stand out and bring value to your users.