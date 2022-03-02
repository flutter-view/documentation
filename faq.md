# FAQ

## What is flutter-view

Flutter-view is a tool for creating Flutter Dart code, meant to make it easier to make trees of widgets and style them.

## How does it work?

Flutter-view itself is an [**npm**](https://www.npmjs.com) program that you run in a terminal window. It monitors your project's Pug, Sass, HTML and CSS files. When a file updates, it will create or update Dart files of the same name.

You use the Pug or HTML files to define flutter-views, which flutter-view will convert into Flutter Widget layout functions in Dart. You can them use these Dart functions in your normal Flutter code.

You can use the Sass or CSS files to add style properties to the widget trees.

For reactive programming, it uses the fantastic [**scoped\_model library**](https://pub.dartlang.org/packages/scoped\_model), in combination with a new pattern where the model is passed into a view, and rendered with a ReactiveWidget. This removes the need for ScopedModel and ScopedModelDescendant, and separating the concerns of state and view. However you are also free to use other patterns, such as streams.

## How stable and complete is it?

Flutter-view is pretty much complete at this point. We have been using it at my company for half a year, and fixed many bugs and contributed features in the process. With the 1.0.0 release, it was stable, fast and fully documented. With the 2.0.0 release, null-safety is supported as well.

## Is it free? How is it licensed?

Flutter-view is completely free and open source, licensed through the[ **BSD-3 open source license**](https://github.com/flutter-view/flutter-view/blob/master/LICENSE). Please enjoy!

## Who built this and why?

Flutter-view was created by Christian Vogel. I am a software developer and entrepreneur who loves new technology. I found Flutter to have a great developer experience, but missed the clear separations of concerns and patterns that I enjoyed in frameworks like Vue.js and React. With Flutter-view I scratched my own itch, was able to use it in my company, and hope it can also help you. If you encounter any issues or have suggestions, please post an [issue on Github](https://github.com/flutter-view/flutter-view/issues), or contact me on Twitter at [http://twitter.com/christianvogel](http://twitter.com/christianvogel).
