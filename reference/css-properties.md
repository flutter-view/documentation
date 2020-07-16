---
description: >-
  A list of all the supported CSS style like shortcuts you can use as properties
  in your pug tags. These will then transform themselves into the appropriate
  Dart code.
---

# CSS style properties

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

Describes how a box should be inscribed into another box. Used for the ****[**FittedBox**](https://api.flutter.dev/flutter/widgets/FittedBox-class.html) Flutter container. Use the [background-size](css-properties.md#box-shadow-4) style property instead if you want to apply a sizing to a [background-image](css-properties.md#box-shadow-1).

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

## shape

Describes how the container should be shaped.

Maps to Flutter [**BoxShape**](https://docs.flutter.io/flutter/painting/BoxShape-class.html) values in camelcase. Creates a Flutter [**BoxDecoration**](https://docs.flutter.io/flutter/painting/BoxDecoration-class.html) with the [shape](https://docs.flutter.io/flutter/painting/BoxDecoration/shape.html) property set to to the value you pass.

Valid values:

* **circle:** A circle centered in the middle of the box into which the [Border](https://docs.flutter.io/flutter/painting/painting/Border-class.html) or [BoxDecoration](https://docs.flutter.io/flutter/painting/painting/BoxDecoration-class.html) is painted. The diameter of the circle is the shortest dimension of the box, either the width or the height, such that the circle touches the edges of the box.
* **rectangle:** An axis-aligned, 2D rectangle. May have rounded corners \(described by a [BorderRadius](https://docs.flutter.io/flutter/painting/painting/BorderRadius-class.html)\). The edges of the rectangle will match the edges of the box into which the [Border](https://docs.flutter.io/flutter/painting/painting/Border-class.html) or [BoxDecoration](https://docs.flutter.io/flutter/painting/painting/BoxDecoration-class.html) is painted.

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.cover-image(
    background-image="asset('images/background.jpg')"
    shape='circle')

```
{% endtab %}

{% tab title="Dart" %}
```dart
Container(
  decoration: BoxDecoration( 
    image: DecorationImage( 
      image: ExactAssetImage( 
        'images/background.jpg',
      ),
    ),
    shape: BoxShape.circle,
  ),
)
```
{% endtab %}
{% endtabs %}



## padding

Adds [padding](https://docs.flutter.io/flutter/widgets/Container/padding.html) to [containers](https://docs.flutter.io/flutter/widgets/Container-class.html).

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

Adds [margin](https://docs.flutter.io/flutter/material/Card/margin.html) to [containers](https://docs.flutter.io/flutter/widgets/Container-class.html).

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

## border

Adds [borders](https://docs.flutter.io/flutter/painting/Border-class.html) to [containers](https://docs.flutter.io/flutter/widgets/Container-class.html).

Creates a Flutter Border widget property using[ **EdgeInsets.only\(\)**](https://docs.flutter.io/flutter/painting/EdgeInsets/EdgeInsets.only.html)**.**

Creates a Flutter [**BoxDecoration**](https://docs.flutter.io/flutter/painting/BoxDecoration-class.html) with [**border**](https://docs.flutter.io/flutter/painting/BoxDecoration/border.html) set using [**Border\(\)**](https://docs.flutter.io/flutter/painting/Border-class.html). The values passed to Border\(\) for each side are values of [**BorderSide**](https://docs.flutter.io/flutter/painting/BorderSide-class.html), with an optional width, style and color.

There are several border properties you can use:

* **border-left:** style of the left border
* **border-right:** style of the right border
* **border-top:** style of the top border
* **border-bottom:** style of the bottom border
* **border:** style for all border sides
* **border-style**: line style for all border sides
* **border-width**: width of all border sides
* **border-color**: color of all border sides

These properties take values according to the [CSS specification](https://developer.mozilla.org/en-US/docs/Web/CSS/border), with these exceptions:

* for styles, only solid and none are accepted
* width must be a number
* color must be a name _\(this is a bug, will be fixed soon\)_
* the **border** property only allows a single style for all, not a style per side

Examples of valid values:

```css
border-left: 1 solid red
border-width: 3.3
border: none
border: 5.5 blue
```

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.greeting(border-top='1.4 red' border-bottom='0.5 green') Hello world!
```
{% endtab %}

{% tab title="Dart" %}
```dart
Container(
  child: Text( 
    'Hello world!',
  ),
  decoration: BoxDecoration( 
    border: Border( 
      top: BorderSide( 
        width: 1.4,
        color: Colors.red,
      ),
      bottom: BorderSide( 
        width: 0.5,
        color: Colors.green,
      ),
    ),
  ),
)
```
{% endtab %}
{% endtabs %}

## box-shadow

Adds shadows to [containers](https://docs.flutter.io/flutter/widgets/Container-class.html).

Creates a Flutter [**BoxDecoration**](https://docs.flutter.io/flutter/painting/BoxDecoration-class.html) with the [boxShadow](https://docs.flutter.io/flutter/painting/BoxDecoration/boxShadow.html) property set using [**BoxShadow**](https://docs.flutter.io/flutter/painting/BoxShadow-class.html).

It suppors multiple passed box shadows, separated by a comma.

A single box shadow can have 2, 3 or 4 or 5 properties: offset-x, offset-y, and optionally blur-radius offset-radius and color.

These properties take values according to the [CSS specification](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow), with these exceptions:

* values must be numbers
* colors not yet supported \(coming soon\)
* no support for the inset keyword

Examples of valid values:

```css
box-shadow: 2 3 // single shadow with offset-x: 3, offset-y: 3
box-shadow: 2 2 5 // single shadow with offset-x: 2, offset-y: 2 and blur: 5
box-shadow: 4 3 6 7 // single grey shadow with blur: 6 and offset-radius: 7
box-shadow: 2 3, 3 4 9 4 // two box shadows example
```

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.greeting(box-shadow='2 3 5 7, -5 -2') Hello world!
```
{% endtab %}

{% tab title="Dart" %}
```dart
Container(
  child: Text( 
    'Hello world!',
  ),
  decoration: BoxDecoration( 
    boxShadow: [
      BoxShadow( 
        offset: Offset(2.00, 3.00),
        blurRadius: 5.00,
        spreadRadius: 7.00,
      ),
      BoxShadow( 
        offset: Offset(-5.00, -2.00),
      )
    ],
  ),
)
```
{% endtab %}
{% endtabs %}

## background-image <a id="box-shadow"></a>

Sets a background image to [containers](https://docs.flutter.io/flutter/widgets/Container-class.html).

Creates a Flutter [**BoxDecoration**](https://docs.flutter.io/flutter/painting/BoxDecoration-class.html) with the [image](https://docs.flutter.io/flutter/painting/BoxDecoration/image.html) property set using either [**NetworkImage**](https://docs.flutter.io/flutter/painting/NetworkImage-class.html) or [**ExactAssetImage**](https://docs.flutter.io/flutter/painting/ExactAssetImage-class.html).

The background-image property can have one of two values:

* **url\("&lt;image-url&gt;"\)** : creates a NetworkImage for the given url
* **asset\("&lt;asset-name&gt;"\)**: uses an ExactAssetImage for the given name

Examples of valid values:

```css
background-image: asset('images/background.jpg')
background-image: url('http://some/image/url.png')
```

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.cover-image(background-image="asset('images/background.jpg')")
```
{% endtab %}

{% tab title="Dart" %}
```dart
Container(
  decoration: BoxDecoration( 
    image: DecorationImage( 
      image: ExactAssetImage( 
        'images/background.jpg',
      ),
    ),
  ),
)
```
{% endtab %}
{% endtabs %}

## ​background-color <a id="box-shadow"></a>

Sets a background color to [containers](https://docs.flutter.io/flutter/widgets/Container-class.html).

Creates a Flutter [**BoxDecoration**](https://docs.flutter.io/flutter/painting/BoxDecoration-class.html) with the [color](https://docs.flutter.io/flutter/painting/BoxDecoration/color.html) property set to the value you pass as a [**Color**](https://docs.flutter.io/flutter/dart-ui/Color-class.html).

See the [color property](css-properties.md#color-color) on valid values.

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.redbox(width=200 height=200 background-color="red")
```
{% endtab %}

{% tab title="Dart" %}
```dart
Container(
  decoration: BoxDecoration( 
    color: Colors.red,
  ),
  width: 200,
  height: 200,
)
```
{% endtab %}
{% endtabs %}

## background-repeat <a id="box-shadow"></a>

Sets how background images of a [container](https://docs.flutter.io/flutter/widgets/Container-class.html) should be repeated. Usually used together with [**background-image**](css-properties.md#box-shadow-1).

Creates a Flutter [**BoxDecoration**](https://docs.flutter.io/flutter/painting/BoxDecoration-class.html) with the repeat property of the image set to the value you pass. 

Maps to Flutter [**ImageRepeat**](https://docs.flutter.io/flutter/painting/ImageRepeat-class.html) values in camelcase.

Valid values:

* **no-repeat:** Leave uncovered portions of the box transparent
* **repeat:** Repeat the image in both the x and y directions until the box is filled.
* **repeat-x:** Repeat the image in the x direction until the box is filled horizontally.
* **repeat-y:** Repeat the image in the y direction until the box is filled vertically.

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.cover-image(
    background-image="asset('images/background.jpg')" 
    background-repeat='no-repeat')
```
{% endtab %}

{% tab title="Dart" %}
```dart
Container( // project://lib/pages/homepage/homepage.pug#8,5
  decoration: BoxDecoration( 
    image: DecorationImage( 
      image: ExactAssetImage( 
        'images/background.jpg',
      ),
      repeat: ImageRepeat.noRepeat,
    ),
  ),
)
```
{% endtab %}
{% endtabs %}

## background-size <a id="box-shadow"></a>

Sets how background images of a [container](https://docs.flutter.io/flutter/widgets/Container-class.html) should be fitted in the container. Usually used together with [**background-image**](css-properties.md#box-shadow-1).

It does so by setting the [fit](https://docs.flutter.io/flutter/painting/DecorationImage/fit.html) property of the [**ImageDecoration**](https://docs.flutter.io/flutter/painting/DecorationImage-class.html) ****that was created for the **background-image**.

See the [**fit property**](css-properties.md#fit) above for valid values and more information.

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.cover-image(
    background-image="asset('images/background.jpg')" 
    background-fit='cover')
```
{% endtab %}

{% tab title="Dart" %}
```dart
Container(
  decoration: BoxDecoration( 
    image: DecorationImage( 
      image: ExactAssetImage( 
        'images/background.jpg',
      ),
      fit: BoxFit.cover,
    ),
  ),
)
```
{% endtab %}
{% endtabs %}

## main-axis-alignment <a id="box-shadow"></a>

Controls how a row or column aligns its children on the main axis. See the [Flutter layout documentation](https://flutter.io/docs/development/ui/layout#aligning-widgets) for more information.

Maps to Flutter [**MainAxisAlignment**](https://docs.flutter.io/flutter/rendering/MainAxisAlignment-class.html) enum values in camelcase.

Valid values:

* **start:** Place the children as close to the start of the main axis as possible
* **end:** Place the children as close to the end of the main axis as possible
* **center:** Place the children as close to the middle of the main axis as possible
* **space-around:** Place the free space evenly between the children as well as half of that space before and after the first and last child
* **space-between:** Place the free space evenly between the children
* **space-evenly:** Place the free space evenly between the children as well as before and after the first and last child

Example:

{% tabs %}
{% tab title="Pug" %}
```css
row(main-axis-alignment="space-evenly")
    .entry We
    .entry Are
    .entry Spaced
    .entry Evenly
```
{% endtab %}

{% tab title="Dart" %}
```dart
Row(
  children: [
    Container(
      child: Text( 
        'We',
      ),
    ),
    Container(
      child: Text( 
        'Are',
      ),
    ),
    Container(
      child: Text( 
        'Spaced',
      ),
    ),
    Container(
      child: Text( 
        'Evenly',
      ),
    )
  ],
  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
)
```
{% endtab %}
{% endtabs %}

## cross-axis-alignment <a id="box-shadow"></a>

Controls how a row or column aligns its children on the cross axis. See the [Flutter layout documentation](https://flutter.io/docs/development/ui/layout#aligning-widgets) for more information.

Maps to Flutter [**CrossAxisAlignment**](https://docs.flutter.io/flutter/rendering/CrossAxisAlignment-class.html) enum values in camelcase.

Valid values:

* **start:** Place the children with their start edge aligned with the start side of the cross axis
* **end:** Place the children as close to the end of the cross axis as possible
* **center:** Place the children so that their centers align with the middle of the cross axis
* **baseline:** Place the children along the cross axis such that their baselines match
* **stretch:** Require the children to fill the cross axis

Example:

{% tabs %}
{% tab title="Pug" %}
```css
column(cross-axis-alignment="center")
    .entry We
    .entry Are
    .entry Centered
```
{% endtab %}

{% tab title="Dart" %}
```dart
Column(
  children: [
    Container(
      child: Text( 
        'We',
      ),
    ),
    Container(
      child: Text( 
        'Are',
      ),
    ),
    Container(
      child: Text( 
        'Centered',
      ),
    )
  ],
  crossAxisAlignment: CrossAxisAlignment.center,
),
```
{% endtab %}
{% endtabs %}

## main-axis-size <a id="box-shadow"></a>

Controls how a row or column to deals with left-over free space in the main axis. See the [Flutter layout documentation](https://flutter.io/docs/development/ui/layout#aligning-widgets) for more information.

Maps to Flutter [**MainAxisSize**](https://docs.flutter.io/flutter/rendering/MainAxisSize-class.html) enum values in camelcase.

Valid values:

* **min:** Minimize the amount of free space along the main axis, subject to the incoming layout constraints
* **max:** Maximize the amount of free space along the main axis, subject to the incoming layout constraints

Example:

{% tabs %}
{% tab title="Pug" %}
```css
column(main-axis-size="max")
    .entry Some entry, left over space is maximized
```
{% endtab %}

{% tab title="Dart" %}
```dart
Column(
  children: [

    //-- ENTRY ----------------------------------------------------------
    Container( // project://lib/pages/homepage/homepage.pug#14,6
      child: Text( 
        'Some entry, left over space is maximized',
      ),
    )
  ],
  mainAxisSize: MainAxisSize.max,
)
```
{% endtab %}
{% endtabs %}

## color, ...-color

Assigns a [**Color**](https://docs.flutter.io/flutter/dart-ui/Color-class.html) to a property. It works on any property either named color, or ending with -color.

When a color is set on a [**Container**](https://docs.flutter.io/flutter/widgets/Container-class.html), it will set the text color, much like you would set a color CSS property on a DIV in HTML. It does so by wrapping the container with [**DefaultTextStyle.merge**](https://docs.flutter.io/flutter/widgets/DefaultTextStyle/merge.html) and setting the text color in the [**TextStyle**](https://docs.flutter.io/flutter/painting/TextStyle-class.html) that is passed.

Valid values:

* Any expression that evalutes to a [**Color**](https://docs.flutter.io/flutter/dart-ui/Color-class.html). `:color='Colors.red'`
* A dash-cased color name from Colors. `color='deep-orange'`
* A dash-cased color name from Colors with a weight. `color='deep-orange[400]'`
* A hex color ala CSS. `color='#FF3499'` 
* A hex color ala CSS with preceding transparency. `color='#80FF3499'`

Examples:

{% tabs %}
{% tab title="Using Pug" %}
```css
.red-text-container(color='red') This text is red
.red-container(:background-color='Colors.red')
.orange-container(background-color='deep-orange')
.green-container(background-color='green[300]')
.blue-container(background-color='#00F')
.blue-container2(background-color='#0000FF')
```
{% endtab %}

{% tab title="Using CSS" %}
```css
.red-text-container
    color: red
.red-container
    background-color: ':Colors.red'
.orange-container
    background-color: deep-orange
.green-container
    background-color: green[300]
.blue-container
    background-color: #00F
.blue-container2
    background-color: #0000FF
```
{% endtab %}

{% tab title="generated Dart" %}
```dart
Column( 
  children: [
    DefaultTextStyle.merge( 
      child: 
      //-- RED-TEXT-CONTAINER ----------------------------------------------------------
      Container(
        child: Text( 
          'This text is red',
        ),
      ),
      style: TextStyle( 
        color: Colors.red,
      ),
    ),

    //-- RED-CONTAINER ----------------------------------------------------------
    Container(
      decoration: BoxDecoration( 
        color: Colors.red,
      ),
    ),

    //-- ORANGE-CONTAINER ----------------------------------------------------------
    Container(
      decoration: BoxDecoration( 
        color: Colors.deepOrange,
      ),
    ),

    //-- GREEN-CONTAINER ----------------------------------------------------------
    Container(
      decoration: BoxDecoration( 
        color: Colors.green.shade300,
      ),
    ),

    //-- BLUE-CONTAINER ----------------------------------------------------------
    Container(
      decoration: BoxDecoration( 
        color: Color(0xFF0000FF),
      ),
    ),

    //-- BLUE-CONTAINER2 ----------------------------------------------------------
    Container(
      decoration: BoxDecoration( 
        color: Color(0xFF0000FF),
      ),
    )
  ],
)
```
{% endtab %}
{% endtabs %}

## font-size <a id="box-shadow"></a>

Sets the font size of text in the container and all its children. Only works on Containers.

It does so by wrapping the container with [**DefaultTextStyle.merge**](https://docs.flutter.io/flutter/widgets/DefaultTextStyle/merge.html) and setting the font size in the [**TextStyle**](https://docs.flutter.io/flutter/painting/TextStyle-class.html) that is passed. 

Allowed values are ints, doubles and theme font sizes.

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.test(font-size=12.5) Welcome!
```
{% endtab %}

{% tab title="Dart" %}
```dart
DefaultTextStyle.merge( 
  child: Container(
    child: Text( 
      'Welcome!',
    ),
  ),
  style: TextStyle( 
    fontSize: 12.5,
  ),
)
```
{% endtab %}
{% endtabs %}

## font-weight <a id="box-shadow"></a>

Sets the font weight of text in the container and all its children. Only works on Containers.

It does so by wrapping the container with [**DefaultTextStyle.merge**](https://docs.flutter.io/flutter/widgets/DefaultTextStyle/merge.html) and setting the font weight in the [**TextStyle**](https://docs.flutter.io/flutter/painting/TextStyle-class.html) that is passed. 

Maps to Flutter [**FontWeight**](https://docs.flutter.io/flutter/dart-ui/FontWeight-class.html) enum values in camelcase. 

Valid values:

* **normal:** The default font weight
* **bold:** A commonly used font weight that is heavier than normal
* **w100:** Thin, the least thick
* **w200:** Extra light
* **w300:** Light
* **w400:** Normal / regular / plain
* **w500:** Medium
* **w600:** Semi bold
* **w700:** Bold
* **w800:** Extra bold
* **w900:** Black, the most thick

_Note: Instead of passing w100, you may also pass 100, etc._

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.test(font-weight='bold') Welcome!
```
{% endtab %}

{% tab title="Dart" %}
```dart
DefaultTextStyle.merge( 
  child: 
  Container(
    child: Text( 
      'Welcome!',
    ),
  ),
  style: TextStyle( 
    fontWeight: FontWeight.bold,
  ),
)
```
{% endtab %}
{% endtabs %}

## font-family <a id="box-shadow"></a>

Sets the font family of text in the container and all its children. Only works on Containers.

It does so by wrapping the container with [**DefaultTextStyle.merge**](https://docs.flutter.io/flutter/widgets/DefaultTextStyle/merge.html) and setting the font family in the [**TextStyle**](https://docs.flutter.io/flutter/painting/TextStyle-class.html) that is passed. 

Value must be a string.

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.test(font-size='Arial') Welcome!
```
{% endtab %}

{% tab title="Dart" %}
```dart
DefaultTextStyle.merge( 
  child: Container(
    child: Text( 
      'Welcome!',
    ),
  ),
  style: TextStyle( 
    fontFamily: 'Arial',
  ),
)
```
{% endtab %}
{% endtabs %}

## font-style <a id="box-shadow"></a>

Sets the font style of text in the container and all its children. Only works on Containers.

It does so by wrapping the container with [**DefaultTextStyle.merge**](https://docs.flutter.io/flutter/widgets/DefaultTextStyle/merge.html) and setting the font style in the [**TextStyle**](https://docs.flutter.io/flutter/painting/TextStyle-class.html) that is passed. 

Maps to Flutter [**FontStyle**](https://docs.flutter.io/flutter/dart-ui/FontStyle-class.html) enum values in camelcase. 

Valid values:

* **normal:** The default font style
* **italic:** Use glyphs designed for slanting

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.test(font-style='italic') Welcome!
```
{% endtab %}

{% tab title="Dart" %}
```dart
DefaultTextStyle.merge( 
  child: 
  Container(
    child: Text( 
      'Welcome!',
    ),
  ),
  style: TextStyle( 
    fontStyle: FontStyle.italic,
  ),
)
```
{% endtab %}
{% endtabs %}

## letter-spacing <a id="box-shadow"></a>

The amount of space \(in logical pixels\) to add between each letter. A negative value can be used to bring the letters closer. Only works on Containers.

It does so by wrapping the container with [**DefaultTextStyle.merge**](https://docs.flutter.io/flutter/widgets/DefaultTextStyle/merge.html) and setting the letter spacing in the [**TextStyle**](https://docs.flutter.io/flutter/painting/TextStyle-class.html) that is passed. 

Valid values are ints and doubles.

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.test(letter-spacing=3) This text gets spaced out
```
{% endtab %}

{% tab title="Dart" %}
```
DefaultTextStyle.merge( 
  child: 
  Container(
    child: Text( 
      'This text gets spaced out',
    ),
  ),
  style: TextStyle( 
    letterSpacing: 3,
  ),
)
```
{% endtab %}
{% endtabs %}

## line-height <a id="box-shadow"></a>

Sets the line height text in the container and all its children. Only works on Containers.

It does so by wrapping the container with [**DefaultTextStyle.merge**](https://docs.flutter.io/flutter/widgets/DefaultTextStyle/merge.html) and setting the line height in the [**TextStyle**](https://docs.flutter.io/flutter/painting/TextStyle-class.html) that is passed. 

Valid values are ints and doubles.

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.test(line-height=20) Welcome!
```
{% endtab %}

{% tab title="Dart" %}
```dart
DefaultTextStyle.merge( 
  child: 
  Container(
    child: Text( 
      'Welcome!',
    ),
  ),
  style: TextStyle( 
    height: 20,
  ),
)
```
{% endtab %}
{% endtabs %}

## text-decoration <a id="box-shadow"></a>

A linear decoration to draw near the text.

It does so by wrapping the container with [**DefaultTextStyle.merge**](https://docs.flutter.io/flutter/widgets/DefaultTextStyle/merge.html) and setting the textDecoration in the [**TextStyle**](https://docs.flutter.io/flutter/painting/TextStyle-class.html) that is passed. 

Maps to Flutter [**TextDecoration**](https://docs.flutter.io/flutter/dart-ui/TextDecoration-class.html) enum values in camelcase. 

Valid values:

* **none:** Do not draw a decoration
* **underline:** Draw a line underneath each line of text
* **overline:** Draw a line above each line of text
* **line-through:** Draw a line through each line of text

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.test(text-decoration='underline') Welcome!
```
{% endtab %}

{% tab title="Dart" %}
```dart
DefaultTextStyle.merge( 
  child: 
  Container(
    child: Text( 
      'Welcome!',
    ),
  ),
  style: TextStyle( 
    textDecoration: TextDecoration.underline,
  ),
)
```
{% endtab %}
{% endtabs %}

## text-decoration-color <a id="box-shadow"></a>

The color of the text decoration you have set.

It does so by wrapping the container with [**DefaultTextStyle.merge**](https://docs.flutter.io/flutter/widgets/DefaultTextStyle/merge.html) and setting the decorationColor in the [**TextStyle**](https://docs.flutter.io/flutter/painting/TextStyle-class.html) that is passed. 

The value must be a valid [**color** property](css-properties.md#color-color) value.

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.test(
    text-decoration='underline'
    text-decoration-color='red') 
    | Hello world!
```
{% endtab %}

{% tab title="Dart" %}
```dart
DefaultTextStyle.merge( 
  child: Container(
    child: Text( 
      'Hello world!',
    ),
  ),
  style: TextStyle( 
    decoration: TextDecoration.underline,
    decorationColor: Colors.red,
  ),
)
```
{% endtab %}
{% endtabs %}

## text-decoration-style <a id="box-shadow"></a>

The style in which to draw a text decoration.

It does so by wrapping the container with [**DefaultTextStyle.merge**](https://docs.flutter.io/flutter/widgets/DefaultTextStyle/merge.html) and setting the decorationStyle in the [**TextStyle**](https://docs.flutter.io/flutter/painting/TextStyle-class.html) that is passed. 

Maps to Flutter [**TextDecorationStyle**](https://docs.flutter.io/flutter/dart-ui/TextDecorationStyle-class.html) enum values in camelcase. 

Valid values:

* **solid:** Draw a solid line
* **double:** Draw two lines
* **dotted:** Draw a dotted line
* **dashed:** Draw a dashed line
* **wavy:** Draw a sinusoidal line

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.test(
	text-decoration='underline'
	text-decoration-style='wavy') 
	| Hello world!
```
{% endtab %}

{% tab title="Dart" %}
```dart
DefaultTextStyle.merge( 
  child: Container( // project://lib/pages/homepage/homepage.pug#8,5
    child: Text( 
      'Hello world!',
    ),
  ),
  style: TextStyle( 
    decoration: TextDecoration.underline,
    decorationStyle: TextDecorationStyle.wavy,
  ),
)
```
{% endtab %}
{% endtabs %}

## word-spacing <a id="box-shadow"></a>

Sets the space between words in a text.

It does so by wrapping the container with [**DefaultTextStyle.merge**](https://docs.flutter.io/flutter/widgets/DefaultTextStyle/merge.html) and setting the wordSpacing in the [**TextStyle**](https://docs.flutter.io/flutter/painting/TextStyle-class.html) that is passed. 

Valid values are ints and doubles.

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.test(word-spacing=5.3) Welcome!
```
{% endtab %}

{% tab title="Dart" %}
```dart
DefaultTextStyle.merge( 
  child: 
  Container(
    child: Text( 
      'Welcome!',
    ),
  ),
  style: TextStyle( 
    wordSpacing: 5.3,
  ),
)
```
{% endtab %}
{% endtabs %}

## text-align <a id="box-shadow"></a>

Whether and how to align text horizontally.

It does so by wrapping the container with [**DefaultTextStyle.merge**](https://docs.flutter.io/flutter/widgets/DefaultTextStyle/merge.html) and setting the textAlign in the [**TextStyle**](https://docs.flutter.io/flutter/painting/TextStyle-class.html) that is passed. 

Maps to Flutter [**TextAlign**](https://docs.flutter.io/flutter/dart-ui/TextAlign-class.html) enum values in camelcase. 

Valid values:

* **start:** Align the text on the leading edge of the container.
* **end:** Align the text on the trailing edge of the container.
* **left:** Align the text on the left edge of the container.
* **right:** Align the text on the right edge of the container.
* **center:** Align the text in the center of the container.
* **justify:** Stretch lines of text that end with a soft line break to fill the width of the container.

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.test(text-align='center') Welcome!
```
{% endtab %}

{% tab title="Dart" %}
```dart
DefaultTextStyle.merge( 
  child: 
  Container(
    child: Text( 
      'Welcome!',
    ),
  ),
  style: TextStyle( 
    textAlign: TextAlign.center,
  ),
)
```
{% endtab %}
{% endtabs %}

## text-overflow <a id="box-shadow"></a>

A linear decoration to draw near the text.

It does so by wrapping the container with [**DefaultTextStyle.merge**](https://docs.flutter.io/flutter/widgets/DefaultTextStyle/merge.html) and setting the overflow in the [**TextStyle**](https://docs.flutter.io/flutter/painting/TextStyle-class.html) that is passed. 

Maps to Flutter [**TextOverflow**](https://docs.flutter.io/flutter/rendering/TextOverflow-class.html) enum values in camelcase. 

Valid values:

* **clip:** Clip the overflowing text to fix its container.
* **ellipsis:** Use an ellipsis to indicate that the text has overflowed.
* **fade:** Fade the overflowing text to transparent.

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.test(text-overflow='ellipsis' width=200) 
    | This will be cut off nicely with ellipsis
```
{% endtab %}

{% tab title="Dart" %}
```dart
DefaultTextStyle.merge( 
  child: Container(
    child: Text( 
      'This will be cut off nicely with ellipsis',
    ),
    width: 200,
  ),
  overflow: TextOverflow.ellipsis,
)
```
{% endtab %}
{% endtabs %}

## text-transform <a id="box-shadow"></a>

Changes the case of the text. It follows the CSS standards.

Valid values:

* **uppercase:** changes the text to uppercase
* **lowercase:** changes the text to lowercase

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.test(text-transform='uppercase') 
    | This text will be shown in uppercase
```
{% endtab %}

{% tab title="Dart" %}
```dart
Container(
  child: Text( 
    'This text will be shown in uppercase'.toUpperCase(),
  ),
)
```
{% endtab %}
{% endtabs %}

## max-lines <a id="box-shadow"></a>

Sets an optional maximum number of lines for the text to span, wrapping if necessary. If the text exceeds the given number of lines, it will be truncated according to [**overflow**](css-properties.md#box-shadow-18).

It does so by wrapping the container with [**DefaultTextStyle.merge**](https://docs.flutter.io/flutter/widgets/DefaultTextStyle/merge.html) and setting the maxLines in the [**TextStyle**](https://docs.flutter.io/flutter/painting/TextStyle-class.html) that is passed. 

Values must be positive integers.

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.test(
    width=100
    max-lines=1
    text-overflow='ellipsis')
    | Only one line gets shown, truncated
```
{% endtab %}

{% tab title="Dart" %}
```dart
DefaultTextStyle.merge( 
  child: 
  Container(
    child: Text( 
      'Only one line gets shown, truncated',
    ),
    width: 100,
  ),
  overflow: TextOverflow.ellipsis,
  maxLines: 1,
)
```
{% endtab %}
{% endtabs %}

## line-clamp <a id="box-shadow"></a>

Alias for [**max-lines**](css-properties.md#box-shadow-19).

## display

CSS-like setting of how you want a widget to be displayed. This can be useful for removing layout elements through CSS.

Valid values:

* **none**: this will remove the widget

Example:

{% tabs %}
{% tab title="Pug" %}
```css
.test
    .message(display="none") I never even become code
```
{% endtab %}

{% tab title="Dart" %}
```dart
//-- TEST ----------------------------------------------------------
Container(
)
```
{% endtab %}
{% endtabs %}

##  <a id="box-shadow"></a>

