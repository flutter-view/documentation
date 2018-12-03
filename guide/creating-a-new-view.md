# Creating a new view

To create a new view, create either an HTML or Pug page. It is common to put this page in its own directory with the same name, to group the page, styling and optional models together. A single page can contain many flutter-views.

## Creating Flutter-views

A flutter-view is transformed into a Dart function. As such, you are just writing Dart functions in an HTML-like format.

### Method body

The format of a flutter view in HTML is as follows:

{% tabs %}
{% tab title="HTML" %}
```markup
<method-name flutter-view [optional parameters]>
    ...method body...
</method-name>
```
{% endtab %}

{% tab title="Pug" %}
```css
method-name(flutter-view [optional parameters])
    ...method body...
```
{% endtab %}
{% endtabs %}

This will render into the following Dart:

```dart
MethodName([optional parameters]) {
    return ...method body...
}
```

The method name in HTML or Pug is dash-cased, and gets transformed into camel-case. The same is true for the parameters.

Note: The generated Dart functions start in uppercase. This is so they can be called from other flutter-views, as will become clear in a moment.

### Adding Parameters

Parameters are defined as follows:

`:parameter-name[type]?`

The **\[type\]** and **?** are optional:

* The type becomes the type of the parameter in the Dart function. If omitted, it it is considered dynamic
* By default, parameters you specify are required. Adding a **?** at the end indicates that they are optional.

Example:

{% tabs %}
{% tab title="HTML" %}
```markup
<task-list-item flutter-view :model[TaskList] :task[Task] :done?>
    ...widgets that show the task...
</method-name>
```
{% endtab %}

{% tab title="Pug" %}
```css
task-list-item(flutter-view :task-model[TaskList] :task[Task] :done?)
    ...widgets that show the task...
```
{% endtab %}
{% endtabs %}

This will render into the following Dart:

```dart
TaskListItem({ @required TaskList taskModel, @required Task task, done) {
    return ...widgets that show the task..
}
```



