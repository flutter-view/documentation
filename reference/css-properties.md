# Layout

## alignment

Describes where the content of a child should be positioned. Eg: text inside of a container.

Maps to Flutter [**Alignment**](https://docs.flutter.io/flutter/painting/Alignment-class.html) values in camelcase.

Valid values:

* **bottom-center:** The center point along the bottom edge
* **bottom-left:** The bottom left corner
* **bottom-right:** The bottom right corner
* **center:** The center point, both horizontally and vertically
* **center-left:** The center point along the left edge
* **center-right:** The center point along the right edge
* **top-center:** The center point along the top edge
* **top-left:** The top left corner
* **top-right:** The top right corner

Example:

{% tabs %}
{% tab title="Pug" %}
```css
container(width=500 height=400)
    .greeting(alignment='center-right')
        | Hello, I am positioned at the right!

```
{% endtab %}

{% tab title="Dart" %}
```dart
Container(
  child: 
  Container(
    child: Text( 
      'Hello, I am positioned at the right!',
    ),
    alignment: Alignment.centerRight,
  ),
  width: 500,
  height: 400,
)
```
{% endtab %}
{% endtabs %}



## fit

Describes how a box should be inscribed into another box.

Maps to Flutter [**BoxFit**](https://docs.flutter.io/flutter/painting/BoxFit-class.html) values in camelcase.

Valid values:

* **contain:** As large as possible while still containing the source entirely within the target box
* **cover:** As small as possible while still covering the entire target box.
* **fill:** Fill the target box by distorting the source's aspect ratio.
* **fill-height:** Make sure the full height of the source is shown, regardless of whether this means the source overflows the target box horizontally.
* **fill-width:** Make sure the full width of the source is shown, regardless of whether this means the source overflows the target box vertically.
* **none:** Align the source within the target box \(by default, centering\) and discard any portions of the source that lie outside the box. The source image is not resized.
* **scale-down:** Align the source within the target box \(by default, centering\) and, if necessary, scale the source down to ensure that the source fits within the box. This is the same as `contain` if that would shrink the image, otherwise it is the same as `none`.

See the [Flutter BoxFit documentation](https://docs.flutter.io/flutter/painting/BoxFit-class.html) for more information on these options.

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.cover-image(
    background-image="asset('images/background.jpg')"
    fit='cover')

```
{% endtab %}

{% tab title="Dart" %}
```dart
Container(
  decoration: BoxDecoration( 
    image: DecorationImage( 
      image: AssetImage(
        'images/background.jpg',
      ),
      fit: BoxFit.cover,
    ),
)
```
{% endtab %}
{% endtabs %}

## padding

Adds [padding](https://docs.flutter.io/flutter/widgets/Container/padding.html) to [containers](https://docs.flutter.io/flutter/widgets/Container-class.html) and other widgets.

Creates a Flutter padding property using[ **EdgeInsets.only\(\)**](https://docs.flutter.io/flutter/painting/EdgeInsets/EdgeInsets.only.html)**.**

There are several padding properties you can use:

* **padding-left:** padding on the left side only
* **padding-right:** padding on the right side only
* **padding-top:** padding on the top side only
* **padding-bottom:** padding on the bottom side only
* **padding:** padding for all sides

These properties take values according to the [CSS specification](https://developer.mozilla.org/en-US/docs/Web/CSS/padding), with these exceptions:

* only direct values \(numbers\) are accepted
* no support for percentages

Examples of valid values:

```css
padding-left: 10 // EdgeInsets.only(left: 10)
padding-top: 50 // EdgeInsets.only(top: 50)
padding: 10 // EdgeInsets.only(top: 10, left: 10, bottom: 10, right: 10)
padding: 5.5 7 // EdgeInsets.only(top: 5.5, left: 7, bottom: 5.5, right: 7)
```

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.greeting(padding=10) Hello world!

```
{% endtab %}

{% tab title="Dart" %}
```dart
Container(
  child: Text( 
    'Hello world!',
  ),
  padding: EdgeInsets.only(top: 10, right: 10, bottom: 10, left: 10),
)
```
{% endtab %}
{% endtabs %}

## margin

Adds [margin](https://docs.flutter.io/flutter/material/Card/margin.html) to [containers](https://docs.flutter.io/flutter/widgets/Container-class.html) and other widgets.

Creates a Flutter margin property using[ **EdgeInsets.only\(\)**](https://docs.flutter.io/flutter/painting/EdgeInsets/EdgeInsets.only.html)**.**

There are several margin properties you can use:

* **margin-left:** margin on the left side only
* **margin-right:** margin on the right side only
* **margin-top:** margin on the top side only
* **margin-bottom:** margin on the bottom side only
* **margin:** margin for all sides

These properties take values according to the [CSS specification](https://developer.mozilla.org/en-US/docs/Web/CSS/margin), with these exceptions:

* only direct values \(numbers\) are accepted
* no support for percentages

Examples of valid values:

```css
margin-left: 10 // EdgeInsets.only(left: 10)
margin-top: 50 // EdgeInsets.only(top: 50)
margin: 10 // EdgeInsets.only(top: 10, left: 10, bottom: 10, right: 10)
margin: 5.5 7 // EdgeInsets.only(top: 5.5, left: 7, bottom: 5.5, right: 7)
```

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.greeting(margin=10) Hello world!
```
{% endtab %}

{% tab title="Dart" %}
```dart
Container(
  child: Text( 
    'Hello world!',
  ),
  margin: EdgeInsets.only(top: 10, right: 10, bottom: 10, left: 10),
)
```
{% endtab %}
{% endtabs %}

## border-radius

Decorates a container with rounded borders.

Creates a Flutter [**BoxDecoration**](https://docs.flutter.io/flutter/painting/BoxDecoration-class.html) with [borderRadius](https://docs.flutter.io/flutter/painting/BoxDecoration/borderRadius.html) set using [**BorderRadius.only\(\)**](https://docs.flutter.io/flutter/painting/BorderRadius/BorderRadius.only.html). The values passed to BorderRadius.only for each corner are values of [**Radius.circular\(\)**](https://docs.flutter.io/flutter/dart-ui/Radius/Radius.circular.html).

The border-radius property takes values according to the [CSS specification](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius), with these exceptions:

* only direct values \(numbers\) are accepted
* no support for percentages

Examples of valid values:

```css
border-radius: 5 // BorderRadius.only(topLeft: Radius.circular(5), topRight: Radius.circular(5), bottomRight: Radius.circular(5), bottomLeft: Radius.circular(5))
border-radius: 2 5 2.5 7 // BorderRadius.only(topLeft: Radius.circular(2), topRight: Radius.circular(5), bottomRight: Radius.circular(2.5), bottomLeft: Radius.circular(7))
border-radius: 5 4 // BorderRadius.only(topLeft: Radius.circular(5), topRight: Radius.circular(4), bottomRight: Radius.circular(5), bottomLeft: Radius.circular(4))
```

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.greeting(border-radius=4 background-color='grey') Hello world!
```
{% endtab %}

{% tab title="Dart" %}
```dart
Container( // project://lib/pages/homepage/homepage.pug#8,5
  child: Text( 
    'Hello world!',
  ),
  decoration: BoxDecoration( 
    color: Colors.grey,
    borderRadius: BorderRadius.only(topLeft: Radius.circular(5), topRight: Radius.circular(5), bottomRight: Radius.circular(5), bottomLeft: Radius.circular(5)),
  ),
)
```
{% endtab %}
{% endtabs %}

