# I tried basic navigation with a dartpad.

keyword
- initialRoute
- onGenerateRoute
- Navigator.pop(context)
- Navigator.pushNamed(cont, '/')

```dart
import 'package:flutter/material.dart';


void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData.light(),
      darkTheme: ThemeData.dark(),
      initialRoute: '/local',
      onGenerateRoute: (RouteSettings settings) {
        switch (settings.name) {
          case '/':
            return MaterialPageRoute(builder: (context) => CommonWidget(MyWidget(settings.name??'')));
          case '/local':
            return MaterialPageRoute(builder: (context) => CommonWidget(CounterWidget()));
          default:
            return MaterialPageRoute(builder: (context) => CommonWidget(MyWidget(settings.name??'')));
        }
      },
    );
  }
}

class CommonWidget extends StatelessWidget {
  
  final Widget name;
  
  const CommonWidget(this.name);
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: name,
      ),
    );
  }
}

class MyWidget extends StatelessWidget {
  
  final String name;
  
  const MyWidget(this.name);
    
  @override
  Widget build(BuildContext context) {
    return TextButton(
      child: Text(
        'Hello, $name World!',
        style: Theme.of(context).textTheme.headline4,
      ),
      onPressed: ()=>Navigator.pop(context),
    );
  }
}


class CounterWidget extends StatefulWidget {
  Widget body (count, up, down, cont) {
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
        ElevatedButton(
          onPressed: ()=>Navigator.pushNamed(cont, '/'),
          child: const Text('go /'),
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
    return widget.body(_counter, _incrementCounter, _decrementCounter, context);
  }
}
```