# Android emulater

## recommend

- Nexus6  -- release name Pie --- ---Graphics Hardware ---

# design

Material design

https://material.io/design

# widget

widget --> widget name(), 

## center

Home widget -> text widget === top of the left corner. 

Home widget -> center -> text === center

--> text automatically centered

Center can have child widget. (in this case, text widget.)



## scaffold

https://api.flutter.dev/flutter/material/Scaffold-class.html

appBar

body

Image

## AppBar

https://api.flutter.dev/flutter/material/AppBar-class.html

Pre-build widget

title, leading, actions... --> widget

backgroundColor ---> color

```dart
backgroundColor: Colors.blueGray[900]
```



## image

https://api.flutter.dev/flutter/widgets/Image-class.html

networkImage --> url

```dart
image: NetwordImage(actual url on web) // amazing!!
```



# code

## => / {} is same meaning in flutter

```dart

// => = {}. {} is better.

void main() {
  runApp(MaterialApp(home: Text('hello world')));
}

void main() => runApp(MaterialApp(home: Text('hello world')));


```

