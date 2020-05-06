# Install

## Requirements

Flutter-view is an npm project and requires a working [NodeJS](https://nodejs.org/en/) installation. Of course you should have a working Flutter install as well.

## Installing flutter-view

To install flutter-view, run the following command in your terminal:

> `npm install -g flutter-view`

On a Mac add sudo:

> `sudo npm install -g flutter-view`

_Note: you may need to add **--unsafe-perm** for things to work due to an_ [_issue with node-gyp_](https://github.com/nodejs/node-gyp/issues/454)

To test your installation worked, type the flutter-view command in your Terminal or console:

> `flutter-view`
>
> `flutter-view - flutter template code generator    
> Converts html and css templates into Flutter view widget code.    
> Please pass a directory to scan.    
> flutter-view -h for help.`

If you got the above text, your installation was succesfull.

## Installing flutter-view-widgets

Flutter-view has an optional Dart tooling library. It allows you to use the reactive, assign and life-cycle tags.

### Adding the dependency

To install it, add the following dependency to your project **pubspec.yaml** file:

> `flutter_view_widgets: ^1.0.6`

Then perform a flutter packages get to pull in the new dependency.

_Note: for the latest version, check the_ [_flutter-view-widgets pub page_](https://pub.dev/packages/flutter_view_widgets)_._

### Importing the tools

To import the library in Dart:

`import 'package:flutter_view_widgets/flutter_view_widgets.dart'`

To import the library in a Pug file:

`import(package='flutter_view_widgets/flutter_view_widgets.dart')`

