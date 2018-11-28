# Test drive

To get to know how flutter-view works, let's create a little hello world example project.

## Create an example flutter project

Make sure flutter-view is [installed](installation.md#installation) correctly.

Open a terminal and go to where you want to create the test project:

> `cd projects-directory`

Create a new Flutter project:

> `flutter create flutter_testdrive`

Open the project in your favorite editor. [VS Code](https://code.visualstudio.com) is recommended.

Try running the test project in an emulator to see if it all works.

## Adding a screen using flutter-view 

Now that we have a working project, let's create a flutter-view that shows a simple welcome screen.

In the lib directory of your project, add a directory called "**screens**". In it create a directory "**homepage**". In the homepage directory, create a file named **homepage.pug**.

Now let's create our first flutter-view. Open homepage.pug and put in the following pug code:

{% code-tabs %}
{% code-tabs-item title="homepage.pug" %}
```css
home-page(flutter-view)
	scaffold
		app-bar(as='appBar')
			#title(as='title') Welcome
		center(as='body')
			.greeting Hello world!
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This code will create a material Scaffold with an AppBar and put "hello world!" in the center of it.

To convert this flutter-view into Dart code, we need to run flutter-view. Go to your project directory in your command line, and type:

> `flutter-view lib`

Then check your lib/screens/homepage directory. Flutter-view should have generated homepage.dart there:

{% code-tabs %}
{% code-tabs-item title="hompage.dart" %}
```dart
// some imports

Scaffold HomePage() {
  return Scaffold( // project://lib/screens/homepage/homepage.pug#2,2
    appBar: AppBar( // project://lib/screens/homepage/homepage.pug#3,3
      title: 
      //-- TITLE ----------------------------------------------------------
      Container( // project://lib/screens/homepage/homepage.pug#4,4
        child: Text( 
          'Welcome',
        ),
      ),
    ),
    body: Center( // project://lib/screens/homepage/homepage.pug#5,3
      child: 
      //-- GREETING ----------------------------------------------------------
      Container( // project://lib/screens/homepage/homepage.pug#6,4
        child: Text( 
          'Hello world!',
        ),
      ),
    ),
  );
}

// _flatten method
```
{% endcode-tabs-item %}
{% endcode-tabs %}

You may notice the comments referring back to the Pug file. These can be turned off, but help the VSCode plugin \(and you\) easily navigate between the Pug file and the Dart file.

Also, notice comments are created for **\#title** and **.greeting** ids and classes in the pug file. These can also be turned off if you wish.

## Using the new homepage

A view is simply a function that renders some widgets. This means you can use it in your application as any other Flutter function. Let's change **main.dart** to show our new homepage:

At the top of main.dart, import our new dart file: 

> `import 'screens/homepage/homepage.dart';`

And to use our new homepage, we need to set it as home:

```dart
// home: MyHomePage(title: 'Flutter Demo Home Page'),
home: HomePage(),
```

Now refresh your app, and you should see this:

![](../.gitbook/assets/screen-shot-2018-11-28-at-5.18.29-pm.png)

## Hot Reload

One of the powerful features in Flutter is hot reload. You can do the same thing with flutter-view. 

Start flutter-view in watch mode in your project directory:

> `flutter-view -w lib`

Now any changes you make will automatically be detected, and the Dart file will be updated. Try changing the **Hello world!** text in **homepage.pug** and press the refresh button in the emulator to see your changes.



