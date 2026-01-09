# What is it?
React Native is an open source framework for building Android and iOS applications using React and the app plataform's native capabilities.

Using this framework, you can use JS to:
- Access your plataform's APIs 
- Describe the appearance and behavior of your UI using React Components

### What does platform mean in this context?
In React Native context, **platform** means the Operative (OS) system on which your app will run.
Right now, there are 2 popular OS:
- Android
- iOS (iPhone)

As you might imagine, each OS has its own API to access to native functionalities.
# Core components
In Android and iOS development, a ***view*** is the basic building block of UI.
A view is a small rectangular element on the screen that can be used to display:
- Text
- Image
- User's input response
- Even other view

![[Pasted image 20260109093222.png]]

## Native components
In Android development we use Kotlin or Java; in iOS development we can use Swift or Objective-C, for creating views (and components) that will compose the application. 

With React Native you can invoke this views with JS using **<u>React Components</u>**.

At *runtime*, React Native creates the corresponding Android and iOS view for those components. Because React Native backed all of these components for both plataforms, react native apps look, feels and perform like any other apps. 

To this backed components for each platform is what we call <u>Native Components</u>.

And as a part of the framework, React Native as a set of essential, ready-to-use Native components. These are <u>React Native's Core Components</u>.

![[Pasted image 20260109094853.png]]


# Environment

React Native allows developers who know React to create native apps.

According to the documentation, they say that the best way to experience React Native is through a ***Framework***, a toolbox with all the necessary APIs to let you build production ready apps.

Documentation say:
> You can also use React Native without a Framework, however we've found that most developers benefit from using a React Native Framework like **Expo**.

Between the benefits listed we can found:
- File-based routing.
- High-quality universal libraries.
- Ability to write plugins that modify native code without having to manage native files.

It's encouraged that you use a framework to develop your application, but if  current frameworks doesn't fit your needs, then you can make a React Native app using `Android Studio`, `Xcode`.
You can consult the documentation to [start your project without a Framework](https://reactnative.dev/docs/getting-started-without-a-framework)

