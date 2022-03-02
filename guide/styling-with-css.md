# Styling with CSS

## Overview

One of the most powerful features in flutter-view is that it allows you to use CSS styles to flutter widgets, and to set any property of any flutter widget.

For example, you can start with a simple Container:

```pug
greeting(flutter-view)
    .example Hello world!
```

This will generate a function that returns a Container with the class name "example", that in turns contains a Text widget with the text "Hello world".

Then you can style this Container by assigning Sass styles to the class:

```sass
.example
    width: 500
    height: 300
    color: red
    background-color: #333
    font-size: 20
    font-weight: bold
```

Flutter-view will process your styles, attaching them to the classes. Properties such as width and height are directly assigned. Some properties are recognized as CSS properties, and generate more code, such as color and font-size. The result is a normal Dart function you can call in your normal Dart code to render the styled view. In this case, a grey box with red bold text saying "Hello world!".

## Structuring your files for styling

**You can use CSS or Sass to set any property to any class or id in your Pug or HTML file.**

To style a Pug file, create a Sass style file with the same name (but different extension) as your Pug file, in the same directory. For example, if you have a startpage.pug, to style it simply add a startpage.sass in the same directory.

_Recommendation_: create a directory per layout, with the name of your layout. Then inside, create a pug file, sass file and your model and other supporting files.

Example structure:

![](<../.gitbook/assets/Screen Shot 2018-12-14 at 11.57.56 AM.png>)

See the[ example projects](../get-started/examples.md) for more ideas for structuring your application.

## Applying styles as properties

**You can apply extra properties to html elements by adding them through style rules.**

To style anything in a flutter-view you:

1. add classes to the elements in your pug file,
2. add style rules to these classes in the related sass file

To assign a class in pug, use the  [Pug .classname syntax](https://pugjs.org/language/attributes.html#class-literal). Any div element becomes a Container widget.

For example, given the following Pug:

```c
.message hello!
```

This will translate into the following HTML:

```markup
<div class="message">hello!</div>
```

You can then use the `.message` class to assign properties using Sass or CSS:

```sass
.message
    width: 200
    height: 200
```

The resulting Dart will be a combination of your layout and style:

```dart
Container(
  child: Text( 
    'hello!',
  ),
  width: 200,
  height: 200,
);
```

## Using shortcut properties in styles

**Flutter-view provides many shortcut properties, that let you style in a CSS-style manner.**

Some examples are [color](../reference/css-properties.md#color-color), [padding](../reference/css-properties.md#padding), [margin](../reference/css-properties.md#margin) and [background-image](../reference/css-properties.md#box-shadow-1). See the [shortcut properties reference](../reference/css-properties.md) for the full list.

As an example, consider the following Pug layout we want to style (taken and converted into flutter-view Pug from the [Flutter Card sample](https://docs.flutter.io/flutter/material/Card-class.html)):

```pug
card
    column
        list-tile
            icon(as='leading' :value='Icons.album')
            .title(as='title') The Enchanted Nightingale
            .subtitle(as='subtitle') Music by Julie Gable. Lyrics by Sidney Stein.
        button-theme:bar
            button-bar
                flat-button.tickets(@on-pressed='...')
                    .label Buy tickets
                flat-button.listen(@on-pressed='...')
                    .label Listen
```

We have a layout, and now we can style it.&#x20;

The "buy tickets" and "listen" FlatButtons we want to have uppercase text. We can use the [**text-transform**](../reference/css-properties.md#box-shadow-18) shortcut:

```pug
flat-button
    .label
        text-transform: uppercase
```

We want the card to be blue and the column of the card to have `mainAxisSize: MainAxisSize.min`:. Here we can use the [**color**](../reference/css-properties.md#color-color) shortcut, so we can use CSS colors, and the [**main-axis-size**](../reference/css-properties.md#box-shadow-7) shortcut, which lets us simply use 'min':

```pug
card
    color: blue
    column
        main-axis-size: min
```

We want to give some padding to the title and subtitle, and give each slightly different colors. [**Padding**](../reference/css-properties.md#padding) and [**margin**](../reference/css-properties.md#margin) are shortcuts that adhere to CSS standards:

```pug
card
    list-tile
        .title
            color: white
            padding: 4 6
        .subtitle
            color: grey[100]
            padding: 2 6
```

Here is the end result:

![](<../.gitbook/assets/Screen Shot 2018-12-14 at 3.55.26 PM (1).png>)

{% tabs %}
{% tab title="artist-card.pug" %}
```pug
artist-card(flutter-view :on-buy-pressed :on-listen-pressed)    
    card
        column
            list-tile
                icon(as='leading' :value='Icons.album')
                .title(as='title') The Enchanted Nightingale
                .subtitle(as='subtitle') Music by Julie Gable. Lyrics by Sidney Stein.
            button-theme:bar
                button-bar
                    flat-button.tickets(@on-pressed='onBuyPressed()')
                        .label Buy tickets
                    flat-button.listen(@on-pressed='onListenPressed()')
                        .label Listen
```
{% endtab %}

{% tab title="artist-card.sass" %}
```sass
card
    color: blue
    column
        main-axis-size: min
    list-tile
        .title
            color: white
            padding: 4 6
        .subtitle
            color: grey[100]
            padding: 2 6
        flat-button
            .label
                text-transform: uppercase
```
{% endtab %}

{% tab title="generated artist-card.dart" %}
```dart
Card ArtistCard({ @required onBuyPressed, @required onListenPressed }) {
  return Card(
    child: Column(
      children: [
        ListTile(
          leading: Icon(
            Icons.album,
            color: Colors.white,
          ),
          title: DefaultTextStyle.merge( 
            child: 
            //-- TITLE ----------------------------------------------------------
            Container(
              child: Text( 
                'The Enchanted Nightingale',
              ),
              padding: EdgeInsets.only(top: 4, right: 6, bottom: 4, left: 6),
            ),
            style: TextStyle( 
              color: Colors.white,
            ),
          ),
          subtitle: DefaultTextStyle.merge( 
            child: 
            //-- SUBTITLE ----------------------------------------------------------
            Container(
              child: Text( 
                'Music by Julie Gable. Lyrics by Sidney Stein.',
              ),
              padding: EdgeInsets.only(top: 2, right: 6, bottom: 2, left: 6),
            ),
            style: TextStyle( 
              color: Colors.grey.shade300,
            ),
          ),
        ),
        ButtonTheme.bar(
          child: ButtonBar(
            children: [

              //-- TICKETS ----------------------------------------------------------
              FlatButton(
                onPressed: () { onBuyPressed(); },
                child: DefaultTextStyle.merge( 
                  child: 
                  //-- LABEL ----------------------------------------------------------
                  Container(
                    child: Text( 
                      'Buy tickets'.toUpperCase(),
                    ),
                  ),
                  style: TextStyle( 
                    color: Colors.white,
                  ),
                ),
              ),

              //-- LISTEN ----------------------------------------------------------
              FlatButton(
                onPressed: () { onListenPressed(); },
                child: DefaultTextStyle.merge( 
                  child: 
                  //-- LABEL ----------------------------------------------------------
                  Container(
                    child: Text( 
                      'Listen'.toUpperCase(),
                    ),
                  ),
                  style: TextStyle( 
                    color: Colors.white,
                  ),
                ),
              )
            ],
          ),
        )
      ]),
      mainAxisSize: MainAxisSize.min,
    ),
    color: Colors.blue,
  );
}
```
{% endtab %}
{% endtabs %}

As you can see here, Sass is a nice match with Pug, since you can retain the same structure. This makes it easy to find the matching styles to your pug elements.

## Setting expressions

**You can set an expression in CSS by wrapping the expression in quotes and starting it with a colon.**

It is recommended to keep Dart expressions in your Pug files. However, in some cases it can be practical to be able to set an expression as a CSS value, for example if flutter-view does not have special support for it.

Say you want to achieve the following Dart:

```dart
Table( 
    defaultVerticalAlignment: TableCellVerticalAlignment.middle,
    children: [ ... ]
)
```

Which you can achieve with the following (a bit contrived) Pug code:

```pug
table(:default-verticle-alignment='TableCellVerticalAlignment.middle')
    ...children...
```

Now let's move the `defaultVerticleAlignment` property into a Sass file:

{% tabs %}
{% tab title="Sass" %}
```css
table
    default-verticle-alignment: ':TableCellVerticalAlignment.middle'
```
{% endtab %}

{% tab title="Pug" %}
```css
table
    ...children...
```
{% endtab %}
{% endtabs %}

Note the colon before `TableCellVerticleAlignment.middle`in the Sass file.

## Using Flutter Themes in styles

Flutter's Material library has [theming support](https://flutter.io/docs/cookbook/design/themes). You may want to assign the values of the theme of the current BuildContext. Flutter-view has support for easily assigning [**ThemeData**](https://docs.flutter.io/flutter/material/ThemeData-class.html) values to your properties.

To understand how it works, let's first look at how you would use it in pure Dart code. To assign a font size to a style, you may write something like this:

```dart
style: TextStyle( 
  fontSize: Theme.of(context).textTheme.title.fontSize,
)
```

First we find the Theme of the current [**BuildContext**](https://docs.flutter.io/flutter/widgets/BuildContext-class.html), then we get a path of properties.

In flutter-view CSS, you might write this the same way:

```sass
.foo
    font-size: ':Theme.of(context).textTheme.title.fontSize'
```

Instead, you may write it like this:

```sass
.foo
    font-size: theme(text-theme/title/font-size)
```

This still requires the context to be available. If you have no current context, you can use the [**builder shortcut**](../reference/tag-shortcuts.md#builder). The theme properties path has been replaced by dash-cased steps, separated by forward slashes`/`.

_Pro tip: You can define CSS classes that set multiple theme style properties at once and reuse them across your app._

