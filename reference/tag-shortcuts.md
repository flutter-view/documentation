---
description: >-
  A list of special tags you can use in your pug code that generate code in your
  Dart code.
---

# Special pug tags

## slot

A slot is a placeholder for a value. It will always take the value of the first valid child.

It is explained in more detailed in the [**flow control section**](../guide/flow-control.md).

## function

Creates a function, and uses the body as what is returned. This allows you to pass functions as parameters.

#### Parameters

* **params**: `@required String` a list of comma separated parameters your function expects

Example, to pass a builder function to a [**LayoutBuilder**](https://docs.flutter.io/flutter/widgets/LayoutBuilder-class.html):

{% tabs %}
{% tab title="Pug" %}
```pug
layout-builder
    function(as='builder' params='context, constraints')
        container Layout constraints: $constraints
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
LayoutBuilder(
    builder: (context, constraints) {
        return Container(
            child: Text(
                'Layout constraints: $constraints'
            ),
        );
    }
)
```
{% endtab %}
{% endtabs %}

## builder

Wraps its child in a builder function that exposes the current [**BuildContext**](https://docs.flutter.io/flutter/widgets/BuildContext-class.html).

Quite frequently you may need the current build context in your views:

* passing it as a parameter into event handlers on your models
* for Theme.of(context) and such common constructions

At any time you need the current context, you can add a builder shortcut. It will write a Builder widget with as its child a function that passes the current context, which you can then use in the child widgets.

#### Parameters

No parameters.

Example:

{% tabs %}
{% tab title="Pug" %}
```pug
example(flutter-view)
	builder
		.welcome(color="theme(primary-color)") Hello!
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
Example() {
  return Builder(
    builder: (context) {
      return DefaultTextStyle.merge( 
        child: 
        Container(
          child: Text( 
            'Hello!',
          ),
        ),
        style: TextStyle( 
          color: Theme.of(context).primaryColor,
        ),
      );
    },
  );
}
```
{% endtab %}
{% endtabs %}

In the above example, if you leave out the builder, you will get an error because theme requires a context. See the generated Dart how it is used.

## lifecycle

_Note: Requires the_ [_flutter-view-widgets_](https://pub.dev/packages/flutter\_view\_widgets) _Dart library._

Widget that lets you listen to the lifecycle of the `BuildContext` it is part of.

Useful in combination with `Model` and `ReactiveModel`, since your model can be informed when the `BuildContext` is being initialized, built, rendered and disposed of.

#### Parameters

* **onInit**: `Function` Called when [**initState**](https://docs.flutter.io/flutter/widgets/State/initState.html) is called on the widget state
* **onBuild**: `Function(BuildContext)` Called when [**build**](https://docs.flutter.io/flutter/widgets/State/build.html) is called on the widget state
* **onRender**: `Function` Called when render is called on the widget
* **onDispose**: `Function` Called when [**dispose**](https://docs.flutter.io/flutter/widgets/State/dispose.html) is called on the widget state

Example:

{% tabs %}
{% tab title="Pug" %}
```pug
example(flutter-view :model[MyModel])
	lifecycle(:on-dispose='model.onDisposed')
		| ${model.message}!
```
{% endtab %}

{% tab title="MyModel.dart" %}
```dart
class MyModel extends Model {
    
    String message = 'Hello world';
    
    onDisposed() {
        // we can do some cleanup here
    }
    
}
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
Lifecycle Example({ @required model }) {
  return Lifecycle( // project://lib/pages/homepage/homepage.pug#21,2
    onDispose: model.onDisposed,
    child: Text( 
      '${model.message}',
    ),
  );
}
```
{% endtab %}
{% endtabs %}

For more information, see [monitoring the state lifecycle](../guide/writing-reactive-code.md#monitoring-the-state-lifecycle).&#x20;

## reactive

_Note: Requires the_ [_flutter-view-widgets_](https://pub.dev/packages/flutter\_view\_widgets) _Dart library._

Re-renders its children if the Listenable it watches updates.

This widget was made to work well with the [ScopedModel library](https://pub.dartlang.org/packages/scoped\_model). However when using flutter-view, you no longer need to use the **ScopedModel** and **ScopedModelDescendant** widgets. Instead, you pass a model into a flutter-view, and use the reactive tag to watch for changes.

#### Parameters

* **watch**: `@required Listenable` Something to watch for updates. Usually a [**Model**](https://pub.dartlang.org/documentation/scoped\_model/latest/scoped\_model/Model-class.html).
* **child**: `@required Object` the rest of the widgets that get rerendered if the watched model updates

#### Implementation

The shortcut tag processor writes a [**ReactiveWidget**](https://pub.dartlang.org/documentation/flutter\_view\_tools/latest/flutter\_view\_tools/ReactiveWidget-class.html), and an associated builder function which gets called to build the widget layout.

{% tabs %}
{% tab title="Pug" %}
```pug
user-entry(flutter-view :user)
	reactive(watch='user')
		.name ${user.name}
		.age ${user.age}
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
UserEntry({ @required user }) {
  return ReactiveWidget(
    watch: user as Listenable,
    builder: (context, $) {
      return Column( 
        children: [
          Container(
            child: Text( 
              '${user.name}',
            ),
          ),
          Container(
            child: Text( 
              '${user.age}',
            ),
          )
        ]),
      );
    },
  );
}

```
{% endtab %}
{% endtabs %}

In the above example, a user model is passed into the view. If a user is an instance of a Model, and user.notifyListeners() gets called, part below the reactive tag (the .name and .user containers) will automatically be re-rendered.

For more information and a more elaborate example, see [Writing Reactive code](../guide/writing-reactive-code.md).
