# Usage

The flutter-view command is:

> `flutter-view [options] <directory [, directory...]>`

Flutter-view scans for Pug and HTML files in one or more directories. For it to work, you need to pass where your source code is. Normally this is the **lib** directory of your project.&#x20;

In almost every case, you want to go to your project directory and type:

> `flutter-view -w lib`

This will tell flutter-view to watch your lib directory, and keep watching (-w) for changes.

When flutter-view creates or updates Dart files, it will tell you:

![](<../.gitbook/assets/Screen Shot 2018-12-04 at 12.36.39 AM.png>)
