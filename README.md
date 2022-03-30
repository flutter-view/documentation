# Introduction

****[**Flutter-view**](https://flutter-view.io) is an open source tool that makes writing reactive [Flutter](http://flutter.io) layouts a breeze. It lets you use [Pug](http://pugjs.org) and [Sass](http://sass-lang.com) to generate the Flutter Dart code that renders the views in your app.

You use it by running the `flutter-view` command in your terminal to let it monitor your project. When it detects changes in a Pug or Sass file, it automatically generates or updates a matching Dart file.

Flutter-view 2.0.0 and up fully support writing null-safe code in Dart 2.13 and up.

## Why views in Flutter

In standard Flutter Dart code, the "state" of your application is mixed in with the presentation. This can make it hard to structure and scale your code.

Flutter-view is about creating **views**, which are functions that return a widget tree for presenting something. These functions act a bit like components. Flutter-view uses **Pug** to make layouts more terse and **Sass** to let you style faster and more easily.

The state part comes into play when you make your view **reactive**. You can pass models (or streams) into your views. When these models change, the views automatically adapt.

## Creating a view

A single flutter-view in pug generates a Dart function that usually returns a widget tree.

{% tabs %}
{% tab title="Pug" %}
{% code title="hello.pug" %}
```c
hello(flutter-view)
    .greeting Hello world!
```
{% endcode %}
{% endtab %}

{% tab title="HTML" %}
{% code title="hello.html" %}
```markup
<hello flutter-view>
    <div class="greeting">
        Hello world!
    </div>
</hello>
```
{% endcode %}
{% endtab %}

{% tab title="Generated Dart" %}
{% code title="hello.dart" %}
```dart
Container Hello() {
    return Container(
        child: Text("Hello world!")
    );
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

_Click the tabs to see the Pug code, the HTML representation of the Pug, and the Dart code that flutter-view generates for you._

This generated function can be used like any other Dart code, and will return the code that gives the greeting.

## Adding Styling

You can add Sass to style your view. These styles get mixed with your pug to generate styled Dart code. Flutter-view supports [CSS style properties](reference/css-properties.md) that convert into code. For our example, you can easily add a text [**color**](reference/css-properties.md#color-color), [**background color**](reference/css-properties.md#box-shadow-2), some [**font properties**](reference/css-properties.md#box-shadow-8), and add [**padding**](reference/css-properties.md#padding):

{% tabs %}
{% tab title="Pug" %}
{% code title="hello.pug" %}
```c
hello(flutter-view)
    .greeting Hello world!
```
{% endcode %}
{% endtab %}

{% tab title="Sass" %}
{% code title="hello.sass" %}
```css
.greeting
    color: red
    background-color: grey[200]
    text-transform: uppercase
    padding: 10 20
```
{% endcode %}
{% endtab %}

{% tab title="Generated Dart" %}
{% code title="hello.dart" %}
```dart
Hello() {
    return DefaultTextStyle.merge(
        style: TextStyle(
            color: Colors.red
        ),
        child: Container(
            decoration: BoxDecoration(
                color: Colors.grey[200]
            ),
            padding: EdgeInsets.only(
                top: 10,
                right: 20,
                bottom: 10,
                left: 20
            ),
            child: Text("Hello world!".toUpperCase),
        )
    );
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

_Click the tabs to see the Pug code, the Sass styles we apply, and the code that flutter-view generates for you._

Flutter-view supports [many CSS properties](reference/css-properties.md), and makes it easy to change styles and immediately see the effect. Since single CSS rules can apply to many elements, small CSS changes may have big code effects.

You can also fully leverage both Pug and Sass mixin and function support, allowing for some powerful patters, such as [different styling based on running Android or iOS](guide/untitled.md).

## Making it Reactive

Flutter-view does not force you into any particular Reactive model. For example it works well with streams. However, it comes with native [ScopedModel ](https://pub.dartlang.org/packages/scoped\_model)support and a [small Dart support library](https://pub.dartlang.org/packages/flutter\_view\_tools) for terse reactive coding:

{% tabs %}
{% tab title="user.dart" %}
{% code title="user.dart" %}
```dart
class User extends Model {
    User({this.name, this.age});

    String name;
    int age;
}
```
{% endcode %}
{% endtab %}

{% tab title="hello.pug" %}
{% code title="hello.pug" %}
```c
hello(flutter-view :user)
    reactive(watch='user')
        .greeting Hello ${user.name}!
```
{% endcode %}
{% endtab %}

{% tab title="generated hello.dart" %}
{% code title="hello.dart" %}
```dart
Widget Hello({user}) {
    return ReactiveWidget(
        watch: user as Listenable,
        builder: (context, $) {
            return Container(
                child: Text("Hello ${user.name}!")
            )
        },
    );
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

The view (hello.pug) takes a User (user.dart) as a parameter and watches it for changes. Now when we change the the user name and call  `user.notifyListeners()`,  the view will automatically update.
