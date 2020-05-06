# Styling per platform

When you write your Flutter app you probably want to target both iOS and Android. Flutter-view styling can make this easier for you, using the standard tools from CSS, Pug and Sass.

## The platform widgets library

First tip is, use the [**platform\_widgets library**](https://pub.dartlang.org/packages/flutter_platform_widgets), and add it as an [default import](configuring-flutter-view.md#imports) in flutter-view.json:

{% code title="flutter-view.json" %}
```javascript
{
	"imports": [
		"package:flutter_view_widgets/flutter_view_widgets.dart",
		"package:flutter_platform_widgets/flutter_platform_widgets.dart"
	]
}
```
{% endcode %}

Put `flutter-view.json` in the root of your Flutter project.

This will allow you to use widgets that adapt to the platform they are used on, and also provides you with the short [**isCupertino**](https://pub.dartlang.org/documentation/flutter_platform_widgets/latest/flutter_platform_widgets/isCupertino.html) and [**isMaterial**](https://pub.dartlang.org/documentation/flutter_platform_widgets/latest/flutter_platform_widgets/isMaterial.html) properties, that you can use throughout your layouts.

## Layout per platform

A common pattern is a [**slot**](flow-control.md#slot) with two implementations with two [**if**](flow-control.md#if) statements below it, one per platform:

{% tabs %}
{% tab title="pug" %}
```css
.foo
    slot
        .ios(if='isCupertino')
            ...iOS layout here...
        .android(if='isMaterial')
            ...Android layout here...
```
{% endtab %}

{% tab title="css" %}
```
.foo
    .ios
        // ios layout styling here
    .android
        // android layout styling here
```
{% endtab %}
{% endtabs %}

The above will render different layout depending on the phone OS you run it on. Since we are adding a different class, we can also add different styling through CSS.

## Same layout but different styling per platform

A very common situation is that we have the same basic layout, but want to use different CSS styling per layout. We could do the same as above:

```css
.foo
    slot
        .ios(if='isCupertino')
            .some
                .layout
                    .here
        .android(if='isMaterial')
            .some
                .layout
                    .here
```

This will work, we can apply different styling for .bar.ios and .bar.android. However we are repeating ourselves in the layout. This can be quite redundant.

Instead, we can let Pug mixins help us. We can make a default.pug in our project that multiple view pugs can import. Then in this pug we can write a mixin:

{% code title="default.pug" %}
```css
mixin platform-slot
	slot
		.ios-slot(if='isCupertino')
			.ios
				block
		.android-slot(if='isMaterial')
			.android
				block
```
{% endcode %}

We can then import this tool into our view and use it like this:

{% tabs %}
{% tab title="pug" %}
```css
include /screens/default.pug

.foo
    platform-slot
        .some
            .layout
                .here
```
{% endtab %}

{% tab title="generated pug" %}
```css
include /screens/default.pug

.foo
    slot
        .ios-slot(if='isCupertino')
			.ios
                .bar
                    .some
                        .layout
                            .here
        .android-slot(if='isMaterial')
            .android
                .bar
                    .some
                        .layout
                            .here 
```
{% endtab %}

{% tab title="css" %}
```
.foo
    .ios
        .some
            // ios layout styling here
    .android
        .some
            // android layout styling here
```
{% endtab %}
{% endtabs %}

Now we have no repetition in our layout! 

However, there is a downside: the generated pug will not know what source code line it came to, and as a result, you will not get the [source reference comments in the generated Dart](configuring-flutter-view.md#showpuglinenumbers). This means that in VSCode, the [flutter-view extension](../get-started/vs-code-support.md#linking-between-pug-and-generated-dart) hotlinking will not work for these lines.

_Note: kudos for Floris van der Grinten for this nifty solution_

