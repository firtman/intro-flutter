The initial template includes a quick Stateful Widget to test the framework, but we don't need it. 

We will create a new widget. A widget is a class that, in its stateless format, extends from `StatelessWidget` and it contains one mandatory property that needs to be received in the constructor: `key`. For a quick snippet, type `stless` and press tab in your IDE.

The widget has a `build` method that must return other Widget. There are hundreds of built-in Widgets in the framework.

Your first widget will look like:

```dart
import 'package:flutter/widgets.dart';

class Greet extends StatelessWidget {
  const Greet ({ Key? key }) : super(key: key);

  @override
  Widget build(BuildContext context) {
        var name = "Flutter";
    return Text("Hello $name");
  }
}
```

Now, we will convert it into a Stateful widget, for that you can use the IDE tooltips over the class name and select `Convert to Stateful widget`. That will create two connected classes, the widget that we won't touch too much, and the State class.

```dart

import 'package:flutter/widgets.dart';

class Greet extends StatefulWidget {
  const Greet ({ Key? key }) : super(key: key);

  @override
  State<Greet> createState() => _GreetState();
}

class _GreetState extends State<Greet> {
  @override
  Widget build(BuildContext context) {
        var name = "Flutter";
    return Text("Hello $name");
  }
}
```

Now properties of the widget that are set from the outside should be defined in the widget class, and variables that changes the state (and should cause a re-render of the widget) should be within the State class. Have in mind you must update your state variables and objects within a `setState` call.

```dart
import 'package:flutter/material.dart';

class Greet extends StatefulWidget {
  const Greet({Key? key}) : super(key: key);

  @override
  State<Greet> createState() => _GreetState();
}

class _GreetState extends State<Greet> {
  var name = "";

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text("Hello $name"),
        TextField(
          onChanged: (newValue) {
            setState(() {
              name = newValue;
            });
          },
          decoration: const InputDecoration(
            border: OutlineInputBorder(),
            labelText: "Your Name:",
          ),
        )
      ],
    );
  }
}

```