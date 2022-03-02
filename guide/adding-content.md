# Creating widget layouts

## Overview

In Flutter, widget trees are built by passing a child or children. Widget trees have a lot of indentation, especially since in Flutter nearly everything is a widget, and composition is preferred to inheritance. This can lead to complex nesting and child parameters.

Flutter-views are optimised for building widget trees. Pug in particular is well suited for creating tree structures and moving parts around.

The following example generates a Dart method **FooPage()**, which returns a Scaffold with an AppBar, and a centralized greeting message.&#x20;

The Pug creates the layout, and the main.dart file uses this layout to render the app. This separation between layout and logic is fundamental to using flutter-view.

{% tabs %}
{% tab title="Pug" %}
{% code title="foo-page.pug" %}
```pug
foo-page(flutter-view :greeting)
    scaffold
        app-bar(as='appBar')
            container(as='title') Foo Page
        center(as='body') Hello $greeting!
```
{% endcode %}
{% endtab %}

{% tab title="generated Dart" %}
{% code title="foo-page.dart" %}
```dart
FooPage({@required greeting}) {
    return Scaffold(
        appBar: AppBar(
            title: Container(
                child: Text('Foo page'),
            ),
        ),
        body: Center(
            child: Text('Hello $greeting!'),
        ),
    );
}
```
{% endcode %}
{% endtab %}

{% tab title="main.dart" %}
{% code title="main.dart" %}
```dart
import 'package:flutter/material.dart';
import 'foo-page.dart';

void main() => runApp(TestApp());

class TestApp extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Test App',
      home: FooPage(greeting: 'world!')
    );
  }

}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Adding children to widgets

**In a flutter-view, add indented child tags to tags to automatically have them assigned as child or children parameters**.

In flutter-view Pug/HTML content, an HTML **tag** is a **method or constructor call**, and its parameters are parameters for this method or constructor. The tag **children** are assigned as the Flutter child/children **parameters**.

To see how this works, compare the Pug and generated Dart code in this example:

{% tabs %}
{% tab title="Pug" %}
```pug
container
    column
        row 
            text(value='first row!')
        row 
            text(value='second row!')
        row
            flat-button 
                text(value='Click me!')
            
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
return Container(
    child: Column(
        children: [
            Row(
                children: [
                    Text('first row!'),
                ],
            ),
            Row(
                children: [
                    Text('second row!'),
                ],
            Row(
                FlatButton(
                    child: Text('Click me!'),
                )
            ),
        ],
    ),
);
```
{% endtab %}
{% endtabs %}

### Automatic columns

Flutter-view knows which classes generally need children instead of single child, and automatically creates [**Columns**](https://docs.flutter.io/flutter/widgets/Column-class.html) when you pass multiple children. Also, if you pass text, flutter-view it automatically wraps it in a [**Text**](https://docs.flutter.io/flutter/widgets/Text-class.html) widget as well. This together allows you to be more terse:

{% tabs %}
{% tab title="Pug" %}
```pug
container
    row first row!
    row second row!
    row
        flat-button Click me!            
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
return Container(
    child: Column(
        children: [
            Row(
                children: [
                    Text('first row!'),
                ],
            ),
            Row(
                children: [
                    Text('second row!'),
                ],
            Row(
                FlatButton(
                    child: Text('Click me!'),
                )
            ),
        ],
    ),
);
```
{% endtab %}
{% endtabs %}

You can [override the default wrapper](configuring-flutter-view.md#autowrapchildren-and-autowrapchildrenclass) in **flutter-view.json**.

### Calling dart factory constructors

Some Flutter Dart classes may use factory constructors. For example, ButtonTheme has a [**ButtonTheme.bar()**](https://docs.flutter.io/flutter/material/ButtonTheme/ButtonTheme.bar.html) constructor.&#x20;

To call the factory constructor instead of the default constructor, pass the constructor after the class name, separated with a colon.

{% tabs %}
{% tab title="Pug" %}
```pug
button-theme:bar
    | some content here
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
ButtonTheme.bar(
    child: Text(
        'some content here'
    ),
)
```
{% endtab %}
{% endtabs %}

### Passing children instead of child

There may be cases where flutter-view does not recognise your tag needs a children parameter instead of a child parameter. In that case use and array and assign it as children:

{% tabs %}
{% tab title="Pug" %}
```pug
column
    array(as='children')
        row first!
        row second!
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
Column(
    children: [
        Row(
            children: [
                Text('first!'),
            ]
        ),
        Row(
            children: [
                Text('second!'),
            ]
        ),
    ]
)
```
{% endtab %}
{% endtabs %}

### Passing const widgets

For optimising performance, you may want to pass some widgets as constants. You can do this by adding a **const** parameter in a widget:

To see how this works, compare the Pug and generated Dart code in this example:

{% tabs %}
{% tab title="Pug" %}
```pug
container
    column(const)
        row 
            text(value='first row!')
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
return Container(
    child: const Column(
        children: [
            Row(
                children: [
                    Text('first row!'),
                ],
            ),
        ],
    ),
);
```
{% endtab %}
{% endtabs %}

## Passing parameters

To pass parameters besides child or children, you pass them as pug/html parameters.

### String parameters

You can pass strings by using quotes. Both double and single quotes work.

For example:

{% tabs %}
{% tab title="Pug" %}
```pug
banner(title='testing')
    | Hello world!
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
return Banner(
    title: 'testing',
    child: Text('Hello world!'),
);
```
{% endtab %}
{% endtabs %}

### Expression parameters

To assign a Dart expression as the value of a parameter:

* start the parameter name with `:`
* wrap the expression in quotes. You may need to escape strings.

For example:

{% tabs %}
{% tab title="Pug" %}
```pug
flat-button(:color='highlighted ? Colors.red : Colors.grey')
    | Click me!     
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
return FlatButton(
    color: highlighted ? Colors.red : Colors.grey,
    child: Text('Click me!'),
);
```
{% endtab %}
{% endtabs %}

For **title** we want to pass a direct string, but for **color** we want to pass a value by reference, so we add **:** in front of the parameter.

### Unnamed parameters

Some widgets take an unnamed parameter in their constructor. You can pass this using the reserved **value** parameter:

{% tabs %}
{% tab title="Pug" %}
```pug
container
    icon(:value='Icons.add')
    text(value='Hello world')
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
return Container(
    child: Column(
        children: [
            Icon(Icons.add),
            Text('Hello world'),
        ]
    ),
);
```
{% endtab %}
{% endtabs %}

### Escaping parameter names

You may need to pass a parameter that has the name of a reserved keyword, such as value. You can bypass this problem by escaping your parameter with the ^ sign:

```
:^value='foo'
```

### Passing complex parameter values

Sometimes what you want to pass is not just a single value, but a value that is constructed of many widgets. To solve this, you may take a child and use the **as** keyword to assign it as a parameter to the parent widget.

{% tabs %}
{% tab title="Pug" %}
```pug
scaffold
    app-bar(as='appBar')
        container(as='title') Test App
    center(as='body') Hello world!
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
return Scaffold(
    appBar: AppBar(
        title: Container(
            child: Text('Test App'),
        ),
        body: Center(
            child: Text('Hello world!'),
        ),
    ),
);
```
{% endtab %}
{% endtabs %}

The [Scaffold](https://docs.flutter.io/flutter/material/Scaffold-class.html) class used above has no child or children parameters. Instead we add two children and assign them as parameters using the **as** property.

### Passing functions as children

You can create functions that return children using the [**function shortcut**](../reference/tag-shortcuts.md#function).

### Passing handlers

Passing a handler function or closure is no different than in Dart:

```pug
my-button(flutter-view :on-click[Function])
    flat-button(:on-pressed='onClick') Click me!
```

A common case is a closure without any parameters. In that case you can use the @ sign to create a closure handler:

{% tabs %}
{% tab title="Pug" %}
```pug
my-button(flutter-view)
    flat-button(@on-pressed='print("Click!")') Click me!
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
MyButton() {
    return FlatButton(
        onPressed: () { print("Click!"); },
        child: Text('Click me!'),
    );
}
```
{% endtab %}
{% endtabs %}

### Passing Arrays

Sometimes you need to pass an array of specific items to a parameter. In that case you can use the **array** tag.

{% tabs %}
{% tab title="Pug" %}
```pug
custom-scroll-view
    array(as='slivers')
        sliver1
        sliver2
        sliver3
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
CustomScrollView(
    slivers: [
        sliver1,
        sliver2,
        sliver3,
    ],
)
```
{% endtab %}
{% endtabs %}

## Automatic Containers

A nice Pug feature is that classes and ids are automatically converted into DIV tags. In flutter-view, they are automatically converted into [Container](https://docs.flutter.io/flutter/widgets/Container-class.html) widgets:

```pug
container hello world
#greeting hello world
.greeting hello world
```

All three are equivalent and convert to:

```dart
Container(
    child: Text('hello world'),
)
```

The classes and ids you use are forgotten after the conversion to Dart code. However, you do get automatic commenting, which will make it easier to read the generated code.

The biggest benefit is however that you can use them to style your widgets.
