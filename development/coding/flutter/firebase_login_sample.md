# Firebase Login Sample

- If I'll use Firebase login in the future...
- Sign in with Google
- Sign in with Apple
- Just 2 Button

``` dart
import 'package:flutter/foundation.dart';
import 'package:flutter/material.dart';
import 'package:firebase_auth/firebase_auth.dart';


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
          case '/local':
            return MaterialPageRoute(builder: (context) => LoginPage());
          default:
            return MaterialPageRoute(builder: (context) => LoginPage());
        }
      },
    );
  }
}

class LoginPage extends StatefulWidget {
  @override
  LoginPageState createState() => LoginPageState();
}

class LoginPageState extends State<LoginPage> {
  Future<UserCredential> _signInWithGoogle() async {
    // Create a new provider
    GoogleAuthProvider googleProvider = GoogleAuthProvider();

    googleProvider.addScope('https://www.googleapis.com/auth/contacts.readonly');
    googleProvider.setCustomParameters({
      'login_hint': 'user@example.com'
    });

    // Once signed in, return the UserCredential
    return await FirebaseAuth.instance.signInWithPopup(googleProvider);

    // Or use signInWithRedirect
    // return await FirebaseAuth.instance.signInWithRedirect(googleProvider);    
  }

  Future<UserCredential> _signInWithApple() async {
    final appleProvider = AppleAuthProvider();
    if (kIsWeb) {
      return FirebaseAuth.instance.signInWithPopup(appleProvider);
    } else {
      return FirebaseAuth.instance.signInWithProvider(appleProvider);
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ElevatedButton(
              child: const Text('Sign in with Google'),
              onPressed: () async {
                UserCredential userCredential = await _signInWithGoogle();
                // handle user
                if(userCredential.user != null){
                  print('hi with google.');
                }else{
                  print('fail with google.');
                }
              },
            ),
            ElevatedButton(
              child: const Text('Sign in with Apple'),
              onPressed: () async {
                UserCredential userCredential = await _signInWithApple();
                // handle user
                if(userCredential.user != null){
                  print('hi with apple.');
                }else{
                  print('fail with apple.');
                }
              },
            ),
          ],
        ),
      ),
    );
  }
}

```