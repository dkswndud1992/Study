# Use of FutureBuilder

FutureBuilder: Like the reason for using the aforementioned Future, it is used to draw the part that cannot be drawn without data first before receiving all the data. If there is no FutureBuilder, you will have to wait for the data to be received and then draw the screen or change the data through setState().


``` dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const MyHomePage(title: 'Future Builder Example'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({required this.title});
  final String title;

  @override
  MyHomePageState createState() => MyHomePageState();
}

class MyHomePageState extends State<MyHomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            const Text(
              'This is a place that is called regardless of data.',
              style: TextStyle(fontSize: 20),
            ),
            FutureBuilder(
              future: _fetch1(),
              builder: (BuildContext context, AsyncSnapshot snapshot) {
                // This part means the part that is executed when the data has not yet been received.
                if (snapshot.hasData == false) {
                  return const CircularProgressIndicator();
                }
                // The part returned when an error occurs
                else if (snapshot.hasError) {
                  return Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: Text(
                      'Error: ${snapshot.error}',
                      style: const TextStyle(fontSize: 15),
                    ),
                  );
                }
                // If the data is received normally, the next part is executed.
                else {
                  return Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: Text(
                      snapshot.data.toString(),
                      style: const TextStyle(fontSize: 15),
                    ),
                  );
                }
              },
            ),
          ],
        ),
      ),
    );
  }

  Future<String> _fetch1() async {
    await Future.delayed(const Duration(seconds: 2));
    return 'Call Data';
  }
}
```