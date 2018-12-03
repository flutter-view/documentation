# Flow control

In your views you often want to only conditionally show something, or loop through a list of items. For this flutter-view has some intentionally simple flow control keywords.

## if

This will only render the widget if the passed condition is true.

{% tabs %}
{% tab title="Pug" %}
```c
user-profile(flutter-view :user[User])
    .user
        .name ${user.name}
        .company(if='user.company != null') Works at ${user.company}
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
UserProfile({@required User user}) {
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
                : Container(),
            ],
        ),
    );
}
// left out some flatten operations for simplicity
```
{% endtab %}
{% endtabs %}

In the above example, the company will only be shown if the passed user has the company property set.

## slot

A slot is a placeholder for a value. It will always take the value of the first valid child.

Slot can function as an if/else. In the next example you see either the .status being shown, or the .empty.

{% tabs %}
{% tab title="Pug" %}
```c
tasks-page(flutter-view :tasks[List])
    scaffold
        slot(as='body')
            .status(if='tasks.isNotEmpty') You have ${tasks.length} tasks
            .empty You have no tasks yet...

```
{% endtab %}

{% tab title="generated Dart" %}
```dart
Scaffold TasksPage({ @required List tasks }) {
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

By adding multiple children with if to a slot, you can also create a swich/case:

{% tabs %}
{% tab title="Pug" %}
```c
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
```c
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
Scaffold TasksPage({ @required List tasks }) {
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

You can also get the index \(starting at 0\) of the current entry as such:

```c
.task(for='task, index in tasks')
```



