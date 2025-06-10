# Blog Title

By Athena Chang

(Customize these headings!)

## Introduction

<!--- - Why should someone learn the language/framework that you are learning?

- What is it used for? How popular is it? Who is it for (developers or users)?
- Incorporate real-world analogies when appropriate and useful. --->

React Native is an open-source framework for building Android and iOS applications. React Native lets developers write using JavaScript, TypeScript (superset of JavaScript, father of JavaScript), and React, which are then compiled into native app components. "Native code" are instructions for how to operate the React Native framework on different platforms, such as iOS and Android. This gives you the near-native performance with the flexibility and ease of web development.

Meta released React Native in 2015 and by 2018, React Native had the 2nd highest number of contributors from individuals and companies around the world than any repositories in GitHub. React Native is widely popular and used in thousands of apps, which you most likely have used.

React Native is like a language translator who takes a single language (JavaScript/TypeScript/React) and interprets it fluently for different countries (iOS and Android). You speak one, and your message is understood everywhere.

## Core syntax/features. 

<!--- - For programming languages: data types, variables, code blocks, functions, conditionals, arrays and objects, and iteration. Include code snippets with explanations.

- For frameworks (including React and Express): setup/installation/configurations, core concepts, key methods or approaches. Include code snippets with explanations. --->

### Set Up / Installation

You can start a React Native project using two popular approaches:

- **Expo**: Beginner-friendly platform, no native code required at first, easy to set up, and lots of pre-built APIs. It helps make universal React apps that helps you develop, build, deploy, and quickly iterate on mobile apps.

  - _Features_:

    - **Expo CLI**: a tool to create, manage, and develop your apps

      - _Setup_:

      ```bash
      # Installs Expo command-line tools globally
      npm install -g expo-cli
      # Creates a new Expo app
      expo init my-first-react-native-app
      # Moves you into my-first-react-native folder
      cd my-first-react-native-app
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
      ```

    - **Expo Snack**: a web-based playground where you can write React Native snippets and run them in the browser.
      _Steps_:
      1. Visit [snack.expo.dev](https://snack.expo.dev/)
      2. Write your code in the online editor.
      3. Use the QR code to preview on your device (Expo Go app).
      4. Share the link with others to collaborate or demonstrate.

- **React Native CLI**: More advanced, lets you work with native code directly, needed for some custom native modules.
  - _Setup_:
  ```bash
  npx react-native init MyFirstApp
  ```

### Core Concepts

### Key Methods

## Compare and Contrast

- For programming languages: What are the key differences between the new language and JavaScript? What are the commonalities?
- For frameworks (including React and Express): What are the alternatives to this framework? Can you compare this framework to anything we've learned in the Core Curriculum? What are the tradeoffs when choosing this framework compared to the alternatives?

## Conclusion & Tips for learning this language/framework.

- Wrap things up
- Provide links to resources that you used to help you learn the language.
