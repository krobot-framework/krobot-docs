# Getting Started

{% method %}  
  
## Setting up the project

First, we will set up a basic project. At first, you should know that there is two versions of Krobot. A JavaScript version, and a Java version. To swap the book between languages, **use the two buttons on the top right corner of the book.
**
The JavaScript version is based on **Discord.JS**
The Java version is based on **JDA**

{% sample lang="js" %}

Using NPM/Yarn, initialize a simple project, and then, add "[krobotjs](https://www.npmjs.com/package/krobotjs "Krobot NPM package")" as dependency.

```bash
$ npm init
$ npm install krobotjs
```

{% sample lang="java" %}

You should know that there is a default template. You can use it for quick starts, but we will not use it in this guide, so you can fully understand the code you're working with.

To use Krobot, you can use either Maven, or Gradle. In this guide i will use Gradle, but do what you prefer.

Let's create a simple project.

```bash
$ gradle init
```

You should then add Krobot as dependency. It will automatically includes its dependencies like JDA.
Don't forget to add the Krobot maven repository, and JCenter.

```groovy
apply plugin: 'java'

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

{% endmethod %}

Finally, open the project you've create in you're favorite IDE.

