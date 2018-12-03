# Adding content

In Flutter, widget trees are built by passing a child or children. Widget trees have a lot of indentation, especially since in Flutter nearly everything is a widget, and composition is preferred to inheritance. This can lead to complex nesting and child parameters even in a simple example:

{% code-tabs %}
{% code-tabs-item title="Dart widget tree example" %}
```dart
return Scaffold(
    appBar: AppBar(
      title: Text('Welcome'),
    ),
    body: Center(
      child: ReactiveWidget(
        watch: model as Listenable,
        builder: (context, $) {
          return Container(
            child: Column( 
              children: [
                Text('You have pushed:'),
                DefaultTextStyle.merge( 
                  child: Container(
                    child: Text('${model.counter} times'),
                    margin: EdgeInsets.only(top: 30),
                  ),
                  style: TextStyle(fontSize: 25),
                ),
              ]),
            ),
            margin: EdgeInsets.only(top: 200),
          );
        },
      ),
    ),
    floatingActionButton: FloatingActionButton(
      tooltip: 'Increment',
      onPressed: () { model.incrementCounter(); },
      child: Icon(Icons.add),
    ),
  );
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Flutter-views are optimised for building widget trees. Pug in particular is well suited for creating tree structures and moving parts around.

In flutter-view pug/html content, an html tag is a method or constructor call, and its parameters are parameters for this method or constructor. Its pug/html children are assigned as the child/children parameters. For example:

{% tabs %}
{% tab title="Pug" %}
```css
floating-action-button(tooltip='Increment')
    icon(:value='Icons.add) // this becomes the child
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
FloatingActionButton(
      tooltip: 'Increment',
      child: Icon(Icons.add),
)
```
{% endtab %}
{% endtabs %}



