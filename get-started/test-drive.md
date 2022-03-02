# Test drive

To get to know how flutter-view works, let's create a little hello world example project. You can also find [this project in the examples repository](https://github.com/flutter-view/examples/tree/master/testdrive).

## Create an example flutter project

Make sure flutter-view is [installed](installation.md#installation) correctly.

Open a terminal and go to where you want to create the test project:

> `cd projects-directory`

Create a new Flutter project:

> `flutter create flutter_testdrive`

Open the project in your favorite editor. [VS Code](https://code.visualstudio.com) is recommended.

Try running the test project in an emulator to see if it all works.

## Adding a screen using flutter-view&#x20;

Now that we have a working project, let's create a flutter-view that shows a simple welcome screen.

In the lib directory of your project, add a directory called "**screens**". In it create a directory "**homepage**". In the homepage directory, create a file named **homepage.pug**.

![](<../.gitbook/assets/Screen Shot 2018-11-28 at 4.37.33 PM.png>)

Now let's create our first flutter-view. Open **homepage.pug** and put in the following pug code:

{% code title="homepage.pug" %}
```css
home-page(flutter-view)
	scaffold
		app-bar(as='appBar')
			#title(as='title') Welcome
		center(as='body')
			.greeting Hello world!
```
{% endcode %}

This code will create a material Scaffold with an AppBar and put "hello world!" in the center of it.

To convert this flutter-view into Dart code, we need to run flutter-view. Go to your project directory in your command line, and type:

> `flutter-view lib`

Then check your lib/screens/homepage directory. Flutter-view should have generated homepage.dart there:

{% code title="hompage.dart" %}
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
{% endcode %}

You may notice the comments referring back to the Pug file. These can be turned off, but help the [VSCode flutter-view plugin](vs-code-support.md#linking-between-pug-and-generated-dart) (and you) easily navigate between the Pug file and the Dart file.

Also, notice comments are created for **#title** and **.greeting** ids and classes in the pug file. These can also be turned off if you wish.

## Using the new homepage

A view is simply a Dart function that renders some widgets. This means you can use it in your application as any other Flutter function. Let's change **main.dart** to show our new homepage:

At the top of main.dart, import our new dart file:&#x20;

> `import 'screens/homepage/homepage.dart';`

And to use our new homepage, we need to set it as home:

```dart
// home: MyHomePage(title: 'Flutter Demo Home Page'),
home: HomePage(),
```

Now refresh your app, and you should see this:

![](<../.gitbook/assets/Screen Shot 2018-11-28 at 5.18.29 PM.png>)

## Hot Reload

One of the powerful features in Flutter is hot reload. You can do the same thing with flutter-view.&#x20;

Start flutter-view in watch mode in your project directory:

> `flutter-view -w lib`

Now any changes you make will automatically be detected, and the Dart file will be updated. Try changing the **Hello world!** text in **homepage.pug** and press the refresh button in the emulator to see your changes.

## Adding Styling

Our homepage looks very bland, so let us add some styling.

In the same directory as **homepage.pug**, create a new file called **homepage.sass**. Let's style the .**greeting**:

{% code title="homepage.sass" %}
```css
.greeting
	color: blue
	font-size: 30
	font-weight: bold
```
{% endcode %}

Press hot refresh in your emulator and you will now see the greeting styled:

![](<../.gitbook/assets/Screen Shot 2018-12-02 at 3.16.58 PM.png>)

Now let's add an image. We can choose to use a NetworkImage directly, or to use a background decoration on a container. To do the latter, we need to add the cover container for the image. Since we want to have the image and text to be centered together, we can wrap them in a [FittedBox](https://docs.flutter.io/flutter/widgets/FittedBox-class.html) widget. To do so, change **homepage.pug**:

{% code title="homepage.pug" %}
```css
home-page(flutter-view)
	scaffold
		app-bar(as='appBar')
			#title(as='title') Welcome
		center(as='body')
			fitted-box
				.cover
				.greeting Hello world!

```
{% endcode %}

Flutter-view has [shortcuts](../reference/css-properties.md) that recognise CSS-like properties, and transform them into code. Setting a [**background-image**](../reference/css-properties.md#box-shadow-1) property on a **Container** will add an [BoxDecoration](https://docs.flutter.io/flutter/painting/BoxDecoration-class.html) with a [DecorationImage](https://docs.flutter.io/flutter/painting/DecorationImage-class.html), and set it to the decoration property of that **Container**. Add the following to your **homepage.sass** and press refresh on your emulator:

```css
.cover
	width: 300
	height: 300
	background-size: cover
	background-image: url("https://cutt.ly/Gat1ivy")
```

The result should look like this:

![](<../.gitbook/assets/Screen Shot 2018-12-02 at 2.53.13 PM.png>)

If you look at the generated **homepage.dart**, you will see how flutter-view took homepage.pug and homepage.sass and merged them:

{% code title="homepage.dart" %}
```dart
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
      child: FittedBox( // project://lib/screens/homepage/homepage.pug#6,4
        child: Column( 
          children: __flatten([

            //-- COVER ----------------------------------------------------------
            Container( // project://lib/screens/homepage/homepage.pug#7,5
              decoration: BoxDecoration( 
                image: DecorationImage( 
                  image: NetworkImage( 
                    'https://cutt.ly/Gat1ivy',
                  ),
                  fit: BoxFit.cover,
                ),
              ),
              width: 300,
              height: 300,
            ),
            DefaultTextStyle.merge( 
              child: 
              //-- GREETING ----------------------------------------------------------
              Container( // project://lib/screens/homepage/homepage.pug#8,5
                child: Text( 
                  'Hello world!',
                ),
              ),
              style: TextStyle( 
                fontSize: 30,
                color: Colors.blue,
                fontWeight: FontWeight.bold,
              ),
            )
          ]),
        ),
      ),
    ),
  );
}
```
{% endcode %}

Feel free to play around with some CSS styles to see effect. Some of the things you could try:

* add [**margin**](../reference/css-properties.md#margin) between the cover image and the greeting by adding `margin-top: 10` to the .greeting class in **homepage.sass**.
* instead of a background image, give the **.cover** class a `background-color: blue`.

Currently you need to press the hot refresh button in your emulator to see changes. In the next section we add Visual Studio Code support so this will happen immediately when you change your .pug or .sass file.
