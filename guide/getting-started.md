# Getting Started

## Setting up the project

First, we will set up a basic project. At first, you should know that Krobot is based on **JDA**, a Discord Java API.

To use Krobot, you can use either Maven, or Gradle, but downloading all the libraries would be too long. In this guide I will use Gradle, but do what you prefer.

Let's create a simple project.  **Don't forget to add the Krobot maven repository, and JCenter**.

```bash
$ gradle init
```

Then we edit the build.gradle to add Krobot :

```groovy
repositories {
  jcenter()
  
  maven {
    url 'http://krobot-framework.github.io/maven/'
  }
}

dependencies {
  compile 'fr.litarvan.krobot:krobot-framework:2.1.2'
}
```

## Registering the bot

Before anything, you need to go to [the Discord Developer Console](https://discordapp.com/developers/applications/me "Discord developer apps") to create an app.

Click on "New app", then enter a name, put an icon, and add a description. You don't need to fill the Redirect URIs. To then create the bot account, click on **"Create a Bot User"**. Finally, note your "Client ID" at the top, and the most important, the "Token" of the bot user \(click on "Token: **click to reveal**" in the bot user section\).

The bot token is the key to your app, so don't publish it anyway !

