# Shortcuts

Flutter-view supports special macro-like shortcut tags and properties, that are meant to let you easily lay out code and allow for CSS-like styling. 

See the shortcuts reference for a list of all included shortcuts.

## Shortcut tags

The shortcut tags are macros that help you code layouts more easily. 

For example, the **builder** tag is a shortcut to a [**Builder**](https://docs.flutter.io/flutter/widgets/Builder-class.html) widget with a build function, so you do not need to write the function. You simply keep writing widgets as its children.

Other notable examples are:

* **reactive**: lets you write terse reactive code that responds to your model changes
* **assign**: easily assign values with expressions

## Shortcut properties

The shortcut properties are macros that insert common layout behavior that take more code in Flutter, such as easily setting a background color to a container or adding text styling. These properties are as much as **CSS** properties as possible. However when there is no direct CSS-like analogy, the **Flutter** names and values are used. They are in **dash case**, since camelcase is not officially supported.

You can also place these properties in a separate CSS or Sass file. This allows you to separate your styling from your structure, as you would in HTML and CSS.

Some commonly used examples are:

* \*\*\*\*[**margin**](../reference/css-properties.md#margin) ****and ****[**padding**](../reference/css-properties.md#padding) to let you lay out code easily
* \*\*\*\*[**background-image**](../reference/css-properties.md#box-shadow-1)**,** [**background-color**](../reference/css-properties.md#box-shadow-2) ****and ****[**border-radius**](../reference/css-properties.md#border-radius) to style containers
* **font-size, font-family** and **font-weight**: to style text
* any property name ending on [**color**](../reference/css-properties.md#color-color) accepts both color names and hex codes

### Escaping property shortcut processing

If you have to pass a parameter which has the name of a shortcut, and you do not wish to apply the shortcut, you can escape it with the ^ character.

For example, by default the [**fit** property](../reference/css-properties.md#fit) takes a BoxFit name. For example:

`box-decoration(fit="cover")`

However if you have a situation where you have a widget that happens to have the fit property as well, but do not want flutter-view to processes it as a BoxFit value, you can escape the property:

`my-widget(:^fit="someValue")`



