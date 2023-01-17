# flutter simple todo app

- This is not saved.

```dart
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(
  debugShowCheckedModeBanner: false,
  theme: ThemeData(
    brightness: Brightness.light,
    primaryColor: Colors.blue,
  ),
  home: MyApp(),
));

class MyApp extends StatefulWidget {
  @override
  MyAppState createState() => MyAppState();
}

class MyAppState extends State<MyApp> {
  List todos = [];
  String input = "";

  @override
  void initState() {
    super.initState();
    todos.add("Item1");
    todos.add("Item2");
    todos.add("Item3");
    todos.add("Item4");
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("mytodos"),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          showDialog(
            context: context,
            builder: (BuildContext context) {
              return AlertDialog(
                title: const Text("Add Todolist"),
                content: TextField(
                  onChanged: (String value) {
                    input = value;
                  },
                ),
                actions: <Widget>[
                  TextButton(
                    onPressed: (){
                      setState(() {
                        todos.add(input);
                      });
                      Navigator.of(context).pop();
                    },
                    child: const Text("Add")
                  ),
                ],
              );
            }
          );
        },
        child: const Icon(
          Icons.add,
          color: Colors.white,
        ),
      ),
      body: ListView.builder(
        itemCount: todos.length,
        itemBuilder: (BuildContext context, int index) {
          return Dismissible(	
            key: Key(todos[index]),
            child: Card(
              elevation: 4,
              margin: const EdgeInsets.all(8),
              shape: RoundedRectangleBorder(
                borderRadius: BorderRadius.circular(8)
              ),
              child: ListTile(
                title: Text(todos[index]),
                trailing: IconButton(
                  icon: const Icon(
                    Icons.delete,
                    color: Colors.red
                  ),
                  onPressed: () {
                    setState(() {
                      todos.removeAt(index);
                    });
                  }
                ),
              ),
            ),
          );
        },
      ),
    );
  }
}
```
