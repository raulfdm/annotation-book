## textScaleFactor

As mentioned, it offers way more than that of course. On particularly interesting property is the textScaleFactor property:

```dart
final curScaleFactor = MediaQuery.of(context).textScaleFactor;
```

`textScaleFactor` tells you by how much text output in the app should be scaled. Users can change this in their mobile phone / device settings.

Depending on your app, you might want to consider using this piece of information when setting font sizes.

Consider this example:

```dart
Text('Always the same size!', style: TextStyle(fontSize: 20));
```

This text ALWAYS has a size of 20 device pixels, no matter what the user changed in his / her device settings.

```dart
Text('This changes!', style: TextStyle(fontSize: 20 \* curScaleFactor));
```

This text on the other hand also has a size of 20 if the user didn't change anything in the settings (because textScaleFactor by default is 1). But if changes were made, the font size of this text respects the user settings.
