# Blog Title

By Athena Chang

(Customize these headings!)

## Introduction

<!--- - Why should someone learn the language/framework that you are learning?

- What is it used for? How popular is it? Who is it for (developers or users)?
- Incorporate real-world analogies when appropriate and useful. --->

React Native is an open-source framework for building Android and iOS applications. React Native lets developers write using JavaScript, TypeScript (superset / father of JavaScript), and React, which are then compiled into native app components. "Native code" are instructions for how to operate the React Native framework on different platforms, such as iOS and Android. This gives you the near-native performance with the flexibility and ease of web development.

Meta released React Native in 2015 and by 2018, React Native had the 2nd highest number of contributors from individuals and companies around the world than any repositories in GitHub. React Native is widely popular and used in thousands of apps, which you most likely have used.

React Native is like a language translator who takes a single language (JavaScript/TypeScript/React) and interprets it fluently for different countries (iOS and Android). You speak one, and your message is understood everywhere.

<!--- ## Core syntax/features. 

 - For programming languages: data types, variables, code blocks, functions, conditionals, arrays and objects, and iteration. Include code snippets with explanations.

- For frameworks (including React and Express): setup/installation/configurations, core concepts, key methods or approaches. Include code snippets with explanations. --->

## Set Up / Installation

You can start a React Native project using two popular approaches:

- **Expo**: Beginner-friendly platform, no native code required at first, easy to set up, and lots of pre-built APIs. It helps make universal React apps that helps you develop, build, deploy, and quickly iterate on mobile apps.

  - _Features_:

    - **Expo CLI**: a tool to create, manage, and develop your apps

      - _Setup_:

      ```bash
      # Installs Expo command-line tools globally
      npm install -g expo-cli

      # Creates a new Expo app
      expo init my-first-app

      # Move into my-first-app folder
      cd my-first-app
      ```

    - **Expo Go**: an app you can download on your phone to “view” your app in development

      - _Setup_:

      ```bash
      # Download Expo Go app then run...
      npm start
      # Scan the QR code with the Expo Go app on your phone to run your app instantly!
      ```

    - **Expo SDK**: a modular set of packages that provide access to native APIs, like:

      - Installation:

      ```bash
      # Run install command + the package you want
      npx expo install ______
      #        Camera (`expo-camera`)
      #  Image Picker (`expo-image-picker`)
      #      Location (`expo-location`)
      # Notifications (`expo-notifications`)
      #            ...etc.
      ```

    - **Expo Snack**: a web-based playground where you can write React Native snippets and run them in the browser.
      - _Steps_:
        1. Visit [snack.expo.dev](https://snack.expo.dev/)
        2. Write your code in the online editor.
        3. Use the QR code to preview on your device (Expo Go app).
        4. Share the link with others to collaborate or demonstrate.

- **React Native CLI**: More advanced, lets you work with native code directly, needed for some custom native modules.

  - _Setup_:

  ```bash
  # Installing React Native CLI
  npm install -g react-native-cli

  # Creating a new project
  npx react-native init my-first-app

  # Move into my-first-app folder
  cd my-first-app

  # Running the app for iOS (macOS only)
  npx react-native run-ios

  # For Android (requires emulator or connected device)
  npx react-native run-android
  ```

## Core Concepts

**_Core components_** are the basic building blocks provided by React Native that you can use to build your app’s user interface. Think of them like Lego bricks that come ready-to-use! Here are some examples:

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
    {/* Core components */}
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

**_Custom components_** are like reusable building blocks you create using core components. For example, you might build a reusable Box component:

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

Components can be styled using the `style={}` property, which accepts objects as inline-styling, style created by `StyleSheet`, or an array combining multiple styles.

```js
// Using StyleSheet
<Text style={styles.heading} />
// Inline-styling
<Text style={{ fontSize: 24 }} />
// Array of combined styling
<Text style={[styles.heading, { color: 'red' }]} />
```

`StyleSheet` helps organize and optimize your styles. It’s similar to CSS but written in JavaScript objects.

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
  },
});
```

## Navigation Methods

### `NavigationContainer` Component

In React Navigation, you must wrap all your screens inside a special component called NavigationContainer. It’s like the root manager that keeps your navigation working properly.

```js
import { NavigationContainer } from "@react-navigation/native";

const App = () => (
  <NavigationContainer>
    {/* Insert your navigators and screens here */}
  </NavigationContainer>
);
```

### Types of Navigation & Their Factory Methods:

React Navigation supports different ways to move between screens. Each navigation type is created using a factory method that follows the pattern:

```js
create<Type>Navigator().
```

Here are the 3 most common types:

#### Stack Navigation

> Imagine stacking pages on top of each other like a **stack of books**. You move from screen to screen, and each one sits on top of the previous one. Users can press a back button to "pop" the top screen off and go back.
>
> - `createStackNavigator`: To make a stack navigation (the "book stack" metaphor). It gives you a Navigator component that holds all your stack screens.
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

> Think of a **tab bar** at the bottom of your app (like on Instagram or Twitter) where you can tap different icons to switch between pages instantly.
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

> A **hidden menu** that slides in from the side when you swipe or tap a menu button (like the hamburger menu in many apps). It lets users switch between different screens quickly. It’s perfect for showing an app menu, settings, or additional sections that don’t need to be front-and-center all the time.
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

## Compare and Contrast

<!--- - For programming languages: What are the key differences between the new language and JavaScript? What are the commonalities?
- For frameworks (including React and Express): What are the alternatives to this framework? Can you compare this framework to anything we've learned in the Core Curriculum? What are the tradeoffs when choosing this framework compared to the alternatives? --->

### React Native's Alternative

- **Flutter**: This is a popular choice from Google that uses the Dart programming language. Flutter provides a single codebase for iOS and Android with a built-in UI toolkit. Many developers find its performance and consistent design appealing, though learning Dart can add an extra learning curve.

- **Native Development**: You can also write separate apps using Swift/Objective-C for iOS and Java/Kotlin for Android. This approach gives you full control and access to all device features, but it means you’ll have to maintain two completely separate codebases.

- **Cordova/PhoneGap**: These frameworks let you build mobile apps using web technologies like HTML, CSS, and JavaScript. They’re simpler if you’re already familiar with web development, but they often don’t feel as “native” and might run slower compared to React Native or Flutter.

## Conclusion & Tips for learning this language/framework.

<!--- - Wrap things up
- Provide links to resources that you used to help you learn the language. --->

React Native is a fantastic framework for building mobile apps that run on both iOS and Android with a single codebase. It uses familiar React concepts, making it easier if you already know React for the web. As you learn React Native, remember to practice building small projects and explore its core components and navigation patterns.

### Tips for Learning React Native:

- Start by understanding React fundamentals (components, props, state).
- Use Expo for quick setup and easier development.
- Explore React Native’s core components and try building simple interfaces.
- Experiment with navigation libraries like React Navigation.
- Join React Native communities online for support and tips.
- Debug patiently and use tools like React Native Debugger and Flipper.

### Helpful Resources:

**Documentation**:

- [React Native Documentation](https://reactnative.dev/docs/getting-started)
- [Expo Documentation](https://docs.expo.dev/)
- [React Navigation](https://reactnavigation.org/)

**Course**:

- [Learn React Native Course | Codecademy](https://www.codecademy.com/enrolled/courses/learn-react-native)

**YouTube**:

- [React Native Course for Beginners in 2025 | Build a Full Stack React Native App (JavaScript Mastery)](https://www.youtube.com/watch?v=f8Z9JyB2EIE)
