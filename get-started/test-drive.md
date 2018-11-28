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

## Adding a screen flutter-view

Now that we have a working project, let's create a flutter-view that shows a welcome screen.

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
			| Hello world!
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This code will create a material Scaffold with an AppBar and put "hello world!" in the center of it.

To convert this flutter-view into Dart code, we need to run flutter-view. Go to your project directory in your command line, and type:

> `flutter-view lib`

Then check your lib/screens/homepage directory. Flutter-view should have generated homepage.dart there:

