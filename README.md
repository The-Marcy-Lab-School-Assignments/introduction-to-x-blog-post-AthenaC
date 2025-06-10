# Reactively Navigating React Native

By Athena Chang

## Introduction

<!--- - Why should someone learn the language/framework that you are learning?

- What is it used for? How popular is it? Who is it for (developers or users)?
- Incorporate real-world analogies when appropriate and useful. --->

React Native is an open-source framework for building Android and iOS applications. It allows developers to write apps using JavaScript and TypeScript (a superset of JavaScript that adds static typing), combined with React, which are then compiled into native app components. Native code refers to platform-specific instructions that React Native generates, enabling near-native performance with the flexibility and ease of web development.

Meta released React Native in 2015, and by 2018 it had the second highest number of contributors from individuals and companies worldwide among all GitHub repositories. React Native is widely popular and used in thousands of apps you’ve likely interacted with.

Think of React Native like a language translator who takes a single language (JavaScript/TypeScript/React) and fluently interprets it for different countries (iOS and Android). You speak one language, and your message is understood everywhere.

<!--- ## Core syntax/features. 

 - For programming languages: data types, variables, code blocks, functions, conditionals, arrays and objects, and iteration. Include code snippets with explanations.

- For frameworks (including React and Express): setup/installation/configurations, core concepts, key methods or approaches. Include code snippets with explanations. --->

## Set Up / Installation

You can start a React Native project using two popular approaches:

- **Expo**: Beginner-friendly platform, no native code required at first, easy to set up, and lots of pre-built APIs to speed development. Expo helps you develop, build, deploy, and iterate on universal React apps quickly.

  - _Features_:

    - **Expo CLI**: A tool to create, manage, and develop your apps.

      - _Setup_:

      ```bash
      # Installs Expo command-line tools globally
      npm install -g expo

      # Creates a new Expo app
      expo init my-first-app

      # Move into my-first-app folder
      cd my-first-app
      ```

    - **Expo Go**: An app for your phone to preview your app during development.

      - _Usage_:

      ```bash
      # Download Expo Go app then run...
      npm start
      # Scan the QR code with the Expo Go app on your phone to run your app instantly!
      ```

    - **Expo SDK**: A modular set of packages providing access to native device APIs, such as:

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

    - **Expo Snack**: A web-based playground to write and run React Native snippets in your browser.
      - _Steps_:
        1. Visit [snack.expo.dev](https://snack.expo.dev/)
        2. Write your code in the online editor.
        3. Use the QR code to preview on your device with Expo Go.
        4. Share your project link to collaborate or demonstrate.

- **React Native CLI**: More advanced setup allowing direct work with native code, required for some custom native modules or integrations.

  - _Setup_:

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

  > **Note**: React Native CLI requires you to install Android Studio for Android development and Xcode for iOS development.

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

## React Native's Alternative

- **Flutter**: A Google framework using Dart language. It compiles to native code and offers a consistent UI with a rich widget set. Learning Dart is an extra step, but many love its performance and design flexibility.

- **Native Development**: Writing separate apps in Swift/Objective-C (iOS) and Java/Kotlin (Android). Offers full control and best performance but requires maintaining two codebases.

- **Cordova/PhoneGap**: Build apps with web tech (HTML, CSS, JavaScript). Easier for web devs but apps often feel less “native” and perform slower compared to React Native or Flutter.

## Conclusion

<!--- - Wrap things up
- Provide links to resources that you used to help you learn the language. --->

React Native is a powerful framework that lets you build mobile apps for iOS and Android from a single codebase using familiar React concepts. It’s an excellent choice if you already know React or want to leverage your JavaScript skills for mobile development.

## Tips for Learning React Native:

- Master React fundamentals first: components, props, state.
- Use Expo for faster setup and development cycles.
- Build simple projects focusing on core components.
- Experiment with React Navigation to handle app navigation.
- Join React Native communities for support and real-world tips.
- Debug patiently using tools like React Native Debugger and Flipper.
- When ready, explore React Native CLI for native customization.

### Helpful Resources:

**Documentation**:

- [React Native Documentation](https://reactnative.dev/docs/getting-started)
- [Expo Documentation](https://docs.expo.dev/)
- [React Navigation](https://reactnavigation.org/)

**Course**:

- [Learn React Native Course | Codecademy](https://www.codecademy.com/enrolled/courses/learn-react-native)

**YouTube**:

- [React Native Course for Beginners in 2025 | Build a Full Stack React Native App (JavaScript Mastery)](https://www.youtube.com/watch?v=f8Z9JyB2EIE)
