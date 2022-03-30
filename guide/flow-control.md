# Flow control

In your views you often want to only conditionally show something, or loop through a list of items. For this flutter-view has some intentionally simple flow control keywords.

## if

This will only render the widget if the passed condition is true.

{% tabs %}
{% tab title="Pug" %}
```pug
user-profile(flutter-view :user[User])
    .user
        .name ${user.name}
        .company(if='user.company != null') Works at ${user.company}
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
UserProfile({required User user}) {
    return Container(
        child: Column(
            children: [
                Container(
                    child: Text('${user.name}'),
                ),
                user.company != null ?
                Container(
                    child: Text('Works at ${user.company}'),
                ) 
                : SizedBox(),
            ],
        ),
    );
}
// left out some flatten operations for simplicity
```
{% endtab %}
{% endtabs %}

In the above example, the company will only be shown if the passed user has the company property set.

## if-null

This will only render the widget if the passed condition is false, otherwise it returns null.

With type and null-safety in Dart, you sometimes need to either pass an argument or null. The normal `if` above will return a `SizedBox()` if the condition fails. For building widget trees, this is usually makes sense. However sometimes we need to pass an argument that can be null, depending on a condition. In these edge cases, use `if-null.`

{% tabs %}
{% tab title="Pug" %}
```pug
app-bar
    .title(as='title' null-if='user.name == null') ${user.name}
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
PlatformAppBar(
  title: !(name == null) ?
    Container(
      child: Text(
        '${name}',
      ),
    ) : null,
)
```
{% endtab %}
{% endtabs %}

In the above example, the title of the `AppBar` widget will be set to null if the `user.name` is `null`.

## slot

A slot is a placeholder for a value. It will take the value of the first valid child. Alternatively, you can also directly pass a value into it:

{% tabs %}
{% tab title="Pug" %}
```pug
wrapper(flutter-view :content[Widget])
    slot(:value='content').content
    .footer A footer
```
{% endtab %}

{% tab title="Generated Dart" %}
```dart
Column Wrapper({ required Widget content }) {
  return Column( 
    children: __flatten([
      content,
      //-- FOOTER ----------------------------------------------------------
      Container(
        child: Text( 
          'A footer',
        ),
      )
    ]),
  );
}
```
{% endtab %}
{% endtabs %}

Slot can function as an if/else. In the next example you see either the .status being shown, or the .empty.

{% tabs %}
{% tab title="Pug" %}
```pug
tasks-page(flutter-view :tasks[List])
    scaffold
        slot(as='body')
            .status(if='tasks.isNotEmpty') You have ${tasks.length} tasks
            .empty You have no tasks yet...

```
{% endtab %}

{% tab title="generated Dart" %}
```dart
Scaffold TasksPage({ required List tasks }) {
  return Scaffold(
    body: (tasks.isNotEmpty) ?
      //-- STATUS ----------------------------------------------------------
      Container(
        child: Text( 
          'You have ${tasks.length} tasks',
        ),
      ):
    true ?
      //-- EMPTY ----------------------------------------------------------
      Container(
        child: Text( 
          'You have no tasks yet...',
        ),
      )
    : Container(),
  );
}

```
{% endtab %}
{% endtabs %}

As you can see in the above example, you can use the **as** property to assign the slot value to a parameter as well. In this case, the content of the slot is placed in the body parameter of the Scaffold.

By adding multiple children with if to a slot, you can also create a switch/case:

{% tabs %}
{% tab title="Pug" %}
```pug
slot
    .apple(if='fruit=="Apple"')
    .pear(if='fruit=="Pear"')
    .peach(if='fruit=="Peach"')
    .unknown // the fallback

```
{% endtab %}
{% endtabs %}

## for

Use **for** to repeat a widget for every value in a list. For every repetition, the value gets assigned to a variable, which you can use to render the widget and its children.

{% tabs %}
{% tab title="Pug" %}
```pug
tasks-page(flutter-view :tasks[List])
    scaffold
        slot(as='body')
            .task(for='task in tasks')
                .title ${task.title}
                .description ${task.description}
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
Scaffold TasksPage({ required List tasks }) {
  return Scaffold(
    body: 
    //-- BODY ----------------------------------------------------------
    Container(
      child: (tasks as List).map((task) {
        return
        //-- TASK ----------------------------------------------------------
        Container(
          child: Column( 
            children: [
              //-- TITLE ----------------------------------------------------------
              Container(
                child: Text( 
                  '${task.title}',
                ),
              ),
              //-- DESCRIPTION ----------------------------------------------------------
              Container(
                child: Text( 
                  '${task.description}',
                ),
              )
            ]),
          ),
        );
      }).toList(),
    ),
  );
}
```
{% endtab %}
{% endtabs %}

You can also get the index (starting at 0) of the current entry as such:

```c
.task(for='task, index in tasks')
```

