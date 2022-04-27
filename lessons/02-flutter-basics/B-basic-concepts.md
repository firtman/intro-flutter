##Flutter

The folders you will find in the project

* android: it's an Android Studio project that is used to test and compile for Android
* ios: it's an Xcode proect that is used to test ad compile for iOS and iPadOS (macOS-only)
* web: it's the output folder for the web files to test and package for web and PWAs
* windows: it's the generator code for creating Windows executable packages
* test: unit testing for your project
* build: intermediary files
* lib: ACTUALLY, YOUR SOURCE CODE

The `pubspec.yaml` is the configuration file for the project.

You can create other folders and files in the structure, such as an `assets/` or `images/` folder, but to include its content in the packages you have to define them in the `assets:` section in the `pubspec.yaml`.