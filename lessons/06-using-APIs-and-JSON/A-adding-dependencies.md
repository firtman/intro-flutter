It's time to call our web service using HTTP(s). Flutter includes an HTTP and JSON parser, the only thing we need is to add the dependency in `pubspec.yaml`:

```yaml
dependencies:
  flutter:
    sdk: flutter
  http:
```

Now we are ready to use HTTP services. Warning for Android development: you have to add INTERNET permission to the Android app to make it work. For that you need to find `AndroidManifest.xml` in the `android/app/src/main` folder and add as a new children of the root element

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.coffee_masters">
    <uses-permission android:name="android.permission.INTERNET" />
<!-- ... -->
```

Web and iOS targets have access to Internet without any explicit permission request.