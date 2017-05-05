# Getting Started

{% method %}  
  
## Setting up the project

First, we will set up a basic project. At first, you should know that there is two versions of Krobot. A JavaScript version, and a Java version. To swap the book between languages, **use the two buttons on the top right corner of the book.
**

 - The JavaScript version is based on **Discord.JS**
 - The Java version is based on **JDA**
 
In both case we will use a package manager, download the libraries manually would be too long and complicated.

You can use any editor/IDE then to open your project.

{% sample lang="js" %}

Let's create a simple project : Using NPM/Yarn, initialize a new project.

```bash
$ npm init
```

Then, add "[krobotjs](https://www.npmjs.com/package/krobotjs "Krobot NPM package")" as dependency.

```bash
$ npm install krobotjs
```

You should probably create a start script and a src/ folder then :

```json
"scripts": {
    "start": "node src/index.js"
}
```

{% sample lang="java" %}

To use Krobot, you can use either Maven, or Gradle. In this guide i will use Gradle, but do what you prefer.

Let's create a simple project.  **Don't forget to add the Krobot maven repository, and JCenter**.

```bash
$ gradle init
```
```groovy
repositories {
  jcenter()  
  maven { url 'http://krobot-framework.github.io/maven/' }
}

dependencies {
  compile 'fr.litarvan.krobot:krobot-framework:2.1.2'
}
```

{% endmethod %}

## Registering the bot

Before anything, you need to go to [the Discord Developer Console](https://discordapp.com/developers/applications/me "Discord developer apps") to create an app.

Click on "New app", then enter a name, put an icon, and add a description. You don't need to fill the Redirect URIs. To then create the bot account, click on **"Create a Bot User"**. Finally, note your "Client ID" at the top, and the most important, the "Token" of the bot user (click on "Token: **click to reveal**" in the bot user section).

The bot token is the key to your app, so don't publish it anyway !
