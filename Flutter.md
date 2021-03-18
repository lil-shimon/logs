# Android emulater

## recommend

- Nexus6  -- release name Pie --- ---Graphics Hardware ---

# design

Material design

https://material.io/design

# widget

widget --> widget name(), 

## center

https://api.flutter.dev/flutter/widgets/Center-class.html

A widget that centers its child within itself.

This widget will be as big as possible if its dimensions are constrained and [widthFactor](https://api.flutter.dev/flutter/widgets/Align/widthFactor.html) and [heightFactor](https://api.flutter.dev/flutter/widgets/Align/heightFactor.html) are null. If a dimension is unconstrained and the corresponding size factor is null then the widget will match its child's size in that dimension. If a size factor is non-null then the corresponding dimension of this widget will be the product of the child's dimension and the size factor. For example if widthFactor is 2.0 then the width of this widget will always be twice its child's width.

Home widget -> text widget === top of the left corner. 

Home widget -> center -> text === center

--> text automatically centered

Center can have child widget. (in this case, text widget.)



## scaffold

https://api.flutter.dev/flutter/material/Scaffold-class.html

appBar

### body property

https://api.flutter.dev/flutter/material/Scaffold/body.html

The primary content of the scaffold.

Displayed below the [appBar](https://api.flutter.dev/flutter/material/Scaffold/appBar.html), above the bottom of the ambient [MediaQuery](https://api.flutter.dev/flutter/widgets/MediaQuery-class.html)'s [MediaQueryData.viewInsets](https://api.flutter.dev/flutter/widgets/MediaQueryData/viewInsets.html), and behind the [floatingActionButton](https://api.flutter.dev/flutter/material/Scaffold/floatingActionButton.html) and [drawer](https://api.flutter.dev/flutter/material/Scaffold/drawer.html). If [resizeToAvoidBottomInset](https://api.flutter.dev/flutter/material/Scaffold/resizeToAvoidBottomInset.html) is false then the body is not resized when the onscreen keyboard appears, i.e. it is not inset by `viewInsets.bottom`.

The widget in the body of the scaffold is positioned at the top-left of the available space between the app bar and the bottom of the scaffold. To center this widget instead, consider putting it in a [Center](https://api.flutter.dev/flutter/widgets/Center-class.html) widget and having that be the body. To expand this widget instead, consider putting it in a [SizedBox.expand](https://api.flutter.dev/flutter/widgets/SizedBox/SizedBox.expand.html).

If you have a column of widgets that should normally fit on the screen, but may overflow and would in such cases need to scroll, consider using a [ListView](https://api.flutter.dev/flutter/widgets/ListView-class.html) as the body of the scaffold. This is also a good choice for the case where your body is a scrollable list.

```
final Widget? body;
```

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

