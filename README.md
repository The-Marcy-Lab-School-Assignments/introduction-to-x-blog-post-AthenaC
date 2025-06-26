# Reactively Navigating React Native

By Athena Chang

## Introduction

<!--- - Why should someone learn the language/framework that you are learning?

- What is it used for? How popular is it? Who is it for (developers or users)?
- Incorporate real-world analogies when appropriate and useful. --->

Before frameworks like React Native, creating a mobile app meant writing two entirely separate codebases: one in Swift or Objective-C for iOS, and another in Java or Kotlin for Android. These languages are known as native code, which refers to code that runs directly on a mobile device’s operating system. This approach was not only time consuming but also required developers to learn and maintain two completely different programming languages and environments just to build the same app twice.

React Native changes that. It is an open source framework that lets you build mobile apps for both Android and iOS using JavaScript. If you have ever dreamed of creating an app but felt overwhelmed by the need to learn multiple mobile programming languages, React Native is a game changer. It allows you to use the web development skills you already have to create fully functional, cross-platform mobile apps. React Native was built with JavaScript developers in mind.

Since Meta released React Native in 2015, it has grown rapidly in popularity. By 2018, it had the second highest number of contributors of any GitHub repository. Today, it powers thousands of mobile apps, including many you likely use every day.

Think of React Native like a language translator. You write your code in JavaScript, TypeScript, or React, and React Native fluently interprets it for both iOS and Android so your app can speak the right language no matter where it runs.

## What This Blog Will Cover

In this post, I’ll walk you through how to:

- Set up a brand-new React Native app using Expo,
- Preview your app live while you build it,
- Create and style core components,
- And build out navigation so your app can have multiple pages (like a feed and a profile).

Whether you're new to React Native or just curious about mobile development, this blog is your guide to getting started quickly and confidently.

## Table of Contents

1. [Set Up / Installation](#setup)

- [Expo](#expo)
- [Expo CLI](#expo-cli)
- [Expo Go](#expo-go)
- [Expo SDK](#expo-sdk)
- [Expo Snack](#expo-snack)
- [React Native CLI](#react-native-cli)

2. Core Concepts

- [Core Components](#core)
- [Custom Components](#custom)

3. [Styling in React Native](#styling)

- [Inline & Combined Styling](#styling)
- [`StyleSheet`](#stylesheet)

4. [Navigation Methods](#navigation)

- [`NavigationContainer`](#navigation-container)
- [Types of Navigation & Their Factory Methods](#navigation-types)
- [Stack Navigation](#stack)
- [Tab Navigation](#tab)
- [Drawer Navigation](#drawer)
- [`useNavigation` Hook](#use-navigation)

5. [Alternatives to React Native](#alternatives)

- [Flutter](#flutter)
- [Native iOS/Android](#native)
- [Cordova/PhoneGap](#cordova)

6. [Conclusion](#conclusion)

7. [Learning Tips](#tips)

8. [Helpful Resources](#resources)

<!--- ## Core syntax/features. 

 - For programming languages: data types, variables, code blocks, functions, conditionals, arrays and objects, and iteration. Include code snippets with explanations.

- For frameworks (including React and Express): setup/installation/configurations, core concepts, key methods or approaches. Include code snippets with explanations. --->

## Set Up / Installation

There are two common ways to start building with React Native. Each option has its strengths depending on your experience level and what you want to build.

### 1. Expo (Beginner Friendly)

Expo is a powerful toolkit that makes it easy to build and test mobile apps without needing to touch native code. It handles a lot of setup behind the scenes so you can focus on writing JavaScript and seeing your app in action right away.

Some key tools and features that come with Expo include:

- **Expo CLI**: This command-line tool helps you create, develop, and manage your Expo projects.

  - _How to set it up_:

  ```bash
  # Installs Expo command-line tools globally
  npm install -g expo

  # Creates a new Expo app
  expo init my-first-app

  # Move into my-first-app folder
  cd my-first-app
  ```

- **Expo Go**: A mobile app that lets you preview your project instantly on your phone.

  - _How to use it_:

  ```bash
  # Download Expo Go app then run...
  npm start
  # Scan the QR code in your terminal with the Expo Go app to run your project live on your device.
  ```

- **Expo SDK**: A set of packages that allow you to access native device features like the camera, location, and notifications.

  - _To install specific features_:

  ```bash
  # Run install command + the package you want
  npx expo install expo-______
  #             Camera (`camera`)
  #       Image Picker (`image-picker`)
  #           Location (`location`)
  #      Notifications (`notifications`)
  #                    ...etc.
  ```

- **Expo Snack**: An online playground where you can experiment with React Native code directly in the browser. No setup required.
  - _To try it out_:
    1. Visit [snack.expo.dev](https://snack.expo.dev/)
    2. Write your code in the online editor.
    3. Use the QR code to preview on your device with Expo Go.
    4. Share your project link to collaborate or demonstrate.

### 2. React Native CLI (Advanced)

If you need more control or plan to integrate custom native modules, the React Native CLI gives you direct access to native code. This setup is more flexible but also more involved.

- _How to set it up_:

```bash
# Create a new React Native project using CLI (no global install needed)
npx react-native init my-first-app

# Navigate into your project folder
cd my-first-app

# Run the app on iOS (macOS only)
npx react-native run-ios

# Run the app on Android (requires emulator or connected device)
npx react-native run-android
```

> **Note**: For this approach, you must install Android Studio for Android development and Xcode for iOS development.

Now that your project is set up, let’s explore how to build the user interface using the building blocks of React Native known as core components.

## Core Concepts

**_Core components_** are the building blocks provided by React Native for creating your app’s user interface. Think of them like Lego bricks ready to assemble!

Examples include:

- `<View>`: A container that can hold other components.
- `<Text>`: Displays text.
- `<Image>`: Shows an image.
- `<ScrollView>`: Lets you scroll through content.
- `<Button>`: An interactive button.
- `<TextInput>`: Lets users type in text.

```js
// Import React
import React, { useState } from "react";
// Import Core Components
import {
  View,
  Text,
  Image,
  ScrollView,
  Button,
  TextInput,
  StyleSheet,
} from "react-native";

const CoreComponentsExample = () => {
  // Initializes a state variable 'name' and its setter 'setName', with an initial value of an empty string.
  const [name, setName] = useState("");

  // When the button is pressed, show an alert greeting using 'name' or defaults to 'stranger' if 'name' is empty.
  const handlePress = () => {
    alert(`Hello, ${name || "stranger"}!`);
  };

  return (
    {/* Core Components */}
    {/* <ScrollView> - Scrollable Content */}
    <ScrollView contentContainerStyle={styles.container}>

     {/* <Text> - Display Text */}
      <Text style={styles.heading}>Welcome to React Native!</Text>

      {/* <Image> - Shows images (remote, local, or base64) */}
      {/* 1. Remote Image */}
      <Image
        source={{ uri: "https://reactnative.dev/img/tiny_logo.png" }}
        style={styles.image}
      />

      {/* 2. Local Image */}
      <Image source={require("./local/asset.jpg")} />

      {/* 3. Base64 image */}
      <Image source={{ uri: "data:image/png;base64,<base64-string>=" }} />

      {/* <TextInput> - User Input */}
      <TextInput
        style={styles.input}
        placeholder="Enter your name"
        value={name}
        onChangeText={setName}
      />

      {/* <Button> - Interactive Button */}
      <Button title="Say Hello" onPress={handlePress} />
    </ScrollView>
  );
};
```

**_Custom components_** are reusable building blocks you create from core components:

```js
const App = () => (
  {/* <View> - Container */}
  <View style={style.boxContainer}>
    <Box color="red" />
    <Box color="green" />
    <Box color="blue" />
  </View>
);

// Custom Component
export const Box = ({ color }) => (
  <View style={[styles.box, { backgroundColor: color }]} />
);
```

## Styling

You style components using the style prop, which can accept:

- Inline styles (JS objects),
- Styles created with `StyleSheet`,
- Or arrays combining multiple styles.

```js
// Using StyleSheet
<Text style={styles.heading} />

// Inline-styling
<Text style={{ fontSize: 24 }} />

// Array of combined styling
<Text style={[styles.heading, { color: 'red' }]} />
```

`StyleSheet` helps organize and optimize your styles and is similar to CSS but uses JavaScript objects.

```js
import { StyleSheet } from "react-native";

const styles = StyleSheet.create({
  container: {
    flexGrow: 1,
    alignItems: "center",
    padding: 20,
  },

  heading: {
    fontSize: 24,
    fontWeight: "bold",
    marginBottom: 20,
  },

  image: {
    width: 100,
    height: 100,
    marginBottom: 20,
  },

  input: {
    height: 40,
    borderColor: "#ccc",
    borderWidth: 1,
    paddingHorizontal: 10,
    marginBottom: 20,
    width: "80%",
  },

  boxContainer: {
    flex: 1,
    justifyContent: "center",
  },

  box: {
    width: 100,
    height: 100,
    margin: 10,
  },
});
```

## Navigation Methods

### `NavigationContainer` Component

In React Navigation, wrap all your navigators inside `<NavigationContainer>` — it acts as the root manager of your navigation state.

```js
import { NavigationContainer } from "@react-navigation/native";

const App = () => (
  <NavigationContainer>
    {/* Insert your navigators and screens here */}
  </NavigationContainer>
);
```

### Types of Navigation & Their Factory Methods:

Before we can start implementing React Navigations, we need to install these core dependencies:

```bash
npm install @react-navigation/native
npm install @react-navigation/stack
npm install @react-navigation/bottom-tabs
npm install @react-navigation/drawer
npm install react-native-screens react-native-safe-area-context react-native-gesture-handler react-native-reanimated
```

> (Use `expo install` for Expo projects to get compatible versions.)

React Navigation offers various navigation patterns, each created with a factory function:

```js
create < Type > Navigator();
```

Here are the 3 most common types:

#### Stack Navigation

> Like a stack of books, screens are stacked on top of each other. You can move forward by pushing screens and go back by popping the top screen.
>
> - `createStackNavigator`: Stack Navigator component to hold all your stack screens.
>
> ```js
> const Stack = createStackNavigator();
>
> <Stack.Navigator>
>   <Stack.Screen name="Feed" component={FeedScreen} />
>   <Stack.Screen name="Catalog" component={CatalogScreen} />
> </Stack.Navigator>;
> ```

#### Tab Navigation

> A tab bar usually at the bottom lets users switch between pages quickly.
>
> - `createBottomTabNavigator`: To make a bottom tab bar (like Instagram’s tab bar).
>
> ```js
> const Tab = createBottomTabNavigator();
>
> <Tab.Navigator>
>   <Tab.Screen name="Feed" component={FeedScreen} />
>   <Tab.Screen name="Catalog" component={CatalogScreen} />
> </Tab.Navigator>;
> ```

#### Drawer Navigation

> A hidden sliding menu from the side (hamburger menu) for extra navigation options.
>
> - `createDrawerNavigator`: to create a drawer navigation with a hidden menu that slides out from the side.
>
> ```js
> import { createDrawerNavigator } from "@react-navigation/drawer";
>
> const Drawer = createDrawerNavigator();
>
> <Drawer.Navigator>
>   <Drawer.Screen name="Feed" component={FeedScreen} />
>   <Drawer.Screen name="Catalog" component={CatalogScreen} />
> </Drawer.Navigator>;
> ```

### `useNavigation` Hook

> The `useNavigation` hook lets you navigate between screens programmatically. It's like a remote control for navigation, and you can use it inside any component, not just screen components.
>
> ```js
> import React from "react";
> import { Button } from "react-native";
> import { useNavigation } from "@react-navigation/native";
>
> // A simple reusable button component
> const GoToProfileButton = () => {
>   const navigation = useNavigation();
>
>   return (
>     <Button
>       title="Go to Profile"
>       onPress={() => navigation.navigate("Profile")}
>     />
>   );
> };
>
> export default GoToProfileButton;
> ```

<!--- ## Compare and Contrast

- For programming languages: What are the key differences between the new language and JavaScript? What are the commonalities?
- For frameworks (including React and Express): What are the alternatives to this framework? Can you compare this framework to anything we've learned in the Core Curriculum? What are the tradeoffs when choosing this framework compared to the alternatives? --->

## Alternatives to React Native

While React Native is a popular choice, there are other frameworks and approaches you might come across:

- **Flutter**: Built by Google, Flutter uses a programming language called Dart. It also compiles to native code and offers a highly customizable and consistent user interface with a large set of built-in widgets. The catch is that you’ll need to learn Dart, which is an extra step for most web developers. Still, many developers praise Flutter for its performance and flexibility.

- **Native Development**: This means writing separate apps for iOS and Android using their respective languages—Swift or Objective-C for iOS, and Java or Kotlin for Android. Native development gives you the most control and the best performance, but it also means maintaining two entirely different codebases, which can be time-consuming and difficult to scale.

- **Cordova/PhoneGap**: These frameworks let you build mobile apps using familiar web technologies like HTML, CSS, and JavaScript. While this approach is easier for web developers to pick up, apps built this way often don’t feel as smooth or performant as those built with React Native or Flutter.

## Conclusion

<!--- - Wrap things up
- Provide links to resources that you used to help you learn the language. --->

React Native is a powerful and accessible framework that allows you to build mobile apps for both iOS and Android using one codebase—and one language, JavaScript. If you’re already familiar with React or web development, React Native is a natural next step that opens the door to the world of mobile app creation.

Whether you’re building your first app or exploring a new framework, React Native makes mobile development more approachable, more efficient, and more fun.

## Tips for Learning React Native:

Getting started with React Native can feel like a lot, but breaking it down into smaller steps makes it manageable. Here are some helpful tips to guide your learning:

- **Start with React basics**: Make sure you're comfortable with React fundamentals like components, props, and state. These skills transfer directly into React Native.

- **Use Expo to your advantage**: Expo makes setup simple and allows you to preview your app instantly. It's perfect for beginners who want to jump right into building.

- **Build small projects**: Practice by creating simple apps, such as a to-do list, a weather app, or a photo gallery. Focus on using core components and layout techniques.

- **Learn by doing**: Don’t worry about being perfect at first. The best way to learn is by building and making mistakes along the way.

- **Explore navigation early**: Understanding how to switch between screens is essential for building full apps. React Navigation is the go-to tool for this.

- **Use community tools**: Tools like Flipper and React Native Debugger can help you troubleshoot and inspect your app during development.

- **Connect with the community**: Join forums, Discord groups, or follow React Native developers on social media to stay motivated and get help when you're stuck.

### Helpful Resources:

**Documentation**:

- [React Native Documentation](https://reactnative.dev/docs/getting-started)
- [Expo Documentation](https://docs.expo.dev/)
- [React Navigation](https://reactnavigation.org/)

**Course**:

- [Learn React Native Course | Codecademy](https://www.codecademy.com/enrolled/courses/learn-react-native)
- [freeCodeCamp’s React Native Crash Course](https://www.youtube.com/watch?v=0-S5a0eXPoc)
- [JavaScript Mastery: Full Stack React Native App](https://www.youtube.com/watch?v=f8Z9JyB2EIE)

**Playgrounds and Practice**:

- [Expo Snack (Try React Native in the browser)](https://snack.expo.dev/)
