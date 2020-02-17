# React Native Firebase Documentation (example)

## Getting Started

### New users

If you haven't set up a Firebase project inside the console, you should do that first. Read [here](setting_up_firebase.md) how to accomplish this.

The following steps will create a React Native app with React Native Firebase already pre-packaged:

    npx @react-native-community/cli init --template=@react-native-firebase/template <name>

Where `<name>` is the name your project.

If at any point the process fails with `could not find spec`, follow the instructions below:

    cd <name>/ios
    pod install

Now you are complete. Move onto [Adding Firebase Credentials](#user-content-adding-firebase-credentials) to your app.

### Existing React Native apps

Follow the commands below:

    npm install --save @react-native-firebase/app
    # or if using Yarn
    yarn add @react-native-firebase/app
    cd ios
    pod install

### Migrating from V5

With React Native 0.60+ autolinking is supported, so a lot of references need to be removed to avoid issues with RN 0.60+. Here's how to migrate

    lengthy removal steps here, but ideally a bunch of command line/git diff statements with as little words as possible breaking it up - but if there are words, they should explain some anomaly.

### Adding Firebase Credentials

#### iOS

Download `GoogleService-Info.plist`, and add into your XCode project, ensuring the "Copy items if needed" checkbox is selected.

Then open up `AppDelegate.m`, and at the top add this line:

    #import <Firebase.h>

And further down where you can find `didFinishLaunchingWithOptions`, copy and paste the following:

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    if ([FIRApp defaultApp] == nil) {
      [FIRApp configure];
    }

In a terminal, run the following at the root of your project:

    cd ios/
    pod install --repo-update
    cd ...
    npx react-native run-ios

#### Android

Go to `android/build.gradle` and add the following:

    buildscript {
        dependencies {
            // ...
            classpath 'com.google.gms:google-services:4.2.0'
        }
    }

Go to `android/app/build.gradle` and at the *very* bottom of the file, add the following:

    apply plugin: 'com.google.gms.google-services'

Open a terminal at the root of the project and run

    npx react-native run-android

