# Flavors example
## How to implement flavors in Flutter

1 - Create a folder named "flavors" at the root of your project.

2 - Within the "flavors" folder, create a folder for each flavor you want to create, for example, "dev", "prod", and "uat".

3 - Inside each flavor folder, create a file named "config.dart" and define the specific configurations for each flavor, for example, the API URL, app key, etc.

4 - Create a "main.dart" file at the root of your project.

5 - Import the "config.dart" file from the current flavor folder in the "main.dart" file.

6 - Define a variable that holds the current flavor based on an environment variable, a build-time variable, or whatever works for you.

7 - Use a conditional statement to load the correct configurations for the current flavor.

8 - Run your app using the desired flavor. For example, to run the app using the "dev" flavor, use the command flutter run --flavor dev.

Here's the example code:

In the config.dart file of the dev folder:
```dart
class Config {
  final String apiUrl;
  final String appKey;

  Config({
    this.apiUrl = 'https://api.dev.example.com',
    this.appKey = 'DEV_APP_KEY',
  });
}
```

In the config.dart file of the prod folder:
```dart
class Config {
  final String apiUrl;
  final String appKey;

  Config({
    this.apiUrl = 'https://api.example.com',
    this.appKey = 'PROD_APP_KEY',
  });
}
```

In the main.dart file:
```dart
import 'package:flutter/material.dart';
import 'package:my_app/flavors/config.dart';

void main() {
  // Define the current flavor
  const String _flavor = String.fromEnvironment('FLAVOR', defaultValue: 'dev');

  // Load the correct configuration based on the current flavor
  late Config config;

  switch (_flavor) {
    case 'dev':
      config = Config(
        apiUrl: 'https://api.dev.example.com',
        appKey: 'DEV_APP_KEY',
      );
      break;
    case 'prod':
      config = Config(
        apiUrl: 'https://api.example.com',
        appKey: 'PROD_APP_KEY',
      );
      break;
    default:
      throw ArgumentError('Unknown flavor: $_flavor');
  }

  // Run the app with the correct configuration
  runApp(MyApp(config: config));
}

class MyApp extends StatelessWidget {
  final Config config;

  MyApp({required this.config});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'My App',
      home: Scaffold(
        appBar: AppBar(
          title: Text('My App'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              Text(
                'API URL: ${config.apiUrl}',
              ),
              Text(
                'APP KEY: ${config.appKey}',
              ),
            ],
          ),
        ),
      ),
    );
  }
}

```
