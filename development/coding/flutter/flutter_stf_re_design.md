# change the stateful widget so intuitively.

- StatefulWidget does not have a widget, and calling only createState() is not intuitive, so I changed it.

*before*
```dart
import 'package:flutter/material.dart';

class CounterWidget extends StatefulWidget {
  @override
  _CounterWidgetState createState() => _CounterWidgetState();
}

class _CounterWidgetState extends State<CounterWidget> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  void _decrementCounter() {
    setState(() {
      _counter--;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Text('Counter: $_counter'),
        RaisedButton(
          onPressed: _incrementCounter,
          child: Text('Increment'),
        ),
        RaisedButton(
          onPressed: _decrementCounter,
          child: Text('Decrement'),
        ),
      ],
    );
  }
}
```

*after*
```dart
import 'package:flutter/material.dart';


const Color darkBlue = Color.fromARGB(255, 18, 32, 47);

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData.dark().copyWith(
        scaffoldBackgroundColor: darkBlue,
      ),
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        body: Center(
          child: CounterWidget(),
        ),
      ),
    );
  }
}

class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Text(
      'Hello, World!',
      style: Theme.of(context).textTheme.headline4,
    );
  }
}


class CounterWidget extends StatefulWidget {
  Widget body (count, up, down) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Text('Counter: $count'),
        ElevatedButton(
          onPressed: up,
          child: const Text('Increment'),
        ),
        ElevatedButton(
          onPressed: down,
          child: const Text('Decrement'),
        ),
      ],
    );
  }
  
  @override
  CounterWidgetState createState() => CounterWidgetState();
}

class CounterWidgetState extends State<CounterWidget> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  void _decrementCounter() {
    setState(() {
      _counter--;
    });
  }

  @override
  Widget build(BuildContext context) {
    return widget.body(_counter, _incrementCounter, _decrementCounter);
  }
}
```


