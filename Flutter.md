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

top level container for material app

appBar

### body property

https://api.flutter.dev/flutter/material/Scaffold/body.html

The primary content of the scaffold.

Displayed below the [appBar](https://api.flutter.dev/flutter/material/Scaffold/appBar.html), above the bottom of the ambient [MediaQuery](https://api.flutter.dev/flutter/widgets/MediaQuery-class.html)'s [MediaQueryData.viewInsets](https://api.flutter.dev/flutter/widgets/MediaQueryData/viewInsets.html), and behind the [floatingActionButton](https://api.flutter.dev/flutter/material/Scaffold/floatingActionButton.html) and [drawer](https://api.flutter.dev/flutter/material/Scaffold/drawer.html). If [resizeToAvoidBottomInset](https://api.flutter.dev/flutter/material/Scaffold/resizeToAvoidBottomInset.html) is false then the body is not resized when the onscreen keyboard appears, i.e. it is not inset by `viewInsets.bottom`.

The widget in the body of the scaffold is positioned at the top-left of the available space between the app bar and the bottom of the scaffold. To center this widget instead, consider putting it in a [Center](https://api.flutter.dev/flutter/widgets/Center-class.html) widget and having that be the body. To expand this widget instead, consider putting it in a [SizedBox.expand](https://api.flutter.dev/flutter/widgets/SizedBox/SizedBox.expand.html).

If you have a column of widgets that should normally fit on the screen, but may overflow and would in such cases need to scroll, consider using a [ListView](https://api.flutter.dev/flutter/widgets/ListView-class.html) as the body of the scaffold. This is also a good choice for the case where your body is a scrollable list.

> in flutter version2.0, they give us scrollBar widget to suit a huge screen like desktop app and web development. It is called show suitable scrollbars

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



## Local images

on Root directory, create imagse folder.

Then put image file into images folder

-- assets like this 

```
- images/example.png
```

to access images file like above, check pubspec.yaml and comment out this description

```yaml
assets:
	- images/a_dot_burr.jpeg
	- images/a_dot_ham.jpeg
	
	# then chenge like this
	- images/example.png
	
	# be careful about indentation in yaml files. every indent is two spaces
```

or  just 

```yaml
assets:
	- images/
	
	#it works like above one.
```



widget is like this

```dart
assetImages('images/example.png')
```



## container

### ※ container is Single-child layout widget (also padding, center etc...)

Very similar to <div>

containers with no children try to be as big as possible



## SafeArea

it moves containers to safe area that is not edge of screen

### margin and padding

```dart
margin: EdgeInsets.all(value)
margin: EdgeInsets.symmetic(vertical: value, horizontal: value)
margin: EdgeInsets.fromLTRB(value, value, value, value)
margin: EdgeInsets.only(left: value)
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



# custom icon app

app icon generator

https://appicon.co/

## Android

Source: android/src/main/res/

then change mipmap files into every download of the appicon website.

### circle icon (Android)

Source: android/src/main/res/

on above path, create image asset (configure image asset) then import image path.

## ios

Source: iOS/Runner/AppIcon.appiconset



# web

## setting

```
flutter config --enable-web
flutter device // google chrome?
flutter run -d chrome // start server!!!
```



# hot reload

## create stateless widget

```dart
// class name = upper camel case
class ClassName extends StatelessWidget {
	@override
  // stateless is created by this description "build" 
  // build method
	Widget build(BuildContext context) {
		return Container(); // insert widget (e.g. inside runApp)
	}
}

// almost magical!!!

//then change
void main () {
  runApp(
    ClassName()
  )
}
```



## State management

### ephemeral state

basically, one state has one widget (class) in flutter app. in case you want to share ephemeral state with other widget or pages, you have to use app state

### App state

Examples of application state:

- User preferences
- Login info
- Notifications in a social networking app
- The shopping cart in an e-commerce app
- Read/unread state of articles in a news app

implement provider( with inherit widget),  redux, BloC to use app state.

![A flow chart. Start with 'Data'. 'Who needs it?'. Three options: 'Most widgets', 'Some widgets' and 'Single widget'. The first two options both lead to 'App state'. The 'Single widget' option leads to 'Ephemeral state'.](https://flutter.dev/assets/development/data-and-backend/state-mgmt/ephemeral-vs-app-state-3137024aa509b4df5d20ed7ed30fb8a0f7cff54ebc8ab0d6e39794bced87e27c.png)

# mvvm

view <---> view model <---> repository <---> repository local and remote

viewからロジックや状態をview modelに分離したもの。

### viewmodel

ChangeNotifierを継承するとnotifyListenersが使える

```dart
class HomeViewModel extends ChangeNotifier {
 int _counter = 0;
 int get counter => _counter;

 void incrementCounter() {
   this._counter++;
   notifyListeners();
 }
}
```

これを呼ぶとInjectionされているWidgetに通知が送信されて各Widgetがリビルド

```dart
@override
 Widget build(BuildContext context) {
   return Center(
     child: Column(
       mainAxisAlignment: MainAxisAlignment.center,
       children: <Widget>[
         Text(
           'You have pushed the button this many times:',
         ),
         Text(
           Provider.of<HomeViewModel>(context).counter.toString(),
           style: Theme.of(context).textTheme.display1,
         ),
       ],
     ),
   );
 }
```

Providr.of<HomeViewModel>でInjectionしています。このInjectionされているTextだけがリビルドされるのでパフォーマンスがいい

# final

constと同じ要領

constはコンパイルで評価されるが、finalはされない

--->ビルド時にもし同じ変数名で定義していてもconstはerrorになるが、finalはスキップされる

また、finalは型推論をしてくれるので型を書かなくても大丈夫。(もちろん書いても大丈夫)

# static

これはおまじないのような感じで、classの中で定数を宣言するときはstaticを頭につける

```dart
class Test{
   static const qux = "qux";
}

class Test{
    const qux = "qux"; //<--静的フィールドのみがconstで宣言できるってエラーが出る
}
```

# column and row

it has a lot of child widget so it must have children widget. not child.

```dart
child: Column(
  verticalDirection: VerticalDirection.top // column start from bottom. default option is down.
  mainAxisAlignment: MainAxisAlignment.center // options = center, start, end...
  // spaceEvenly => arranged at equal intervals
	children: <widget>[
    // in between these square brankets, I can put lots of widgets.
  ]
  )
)
```

