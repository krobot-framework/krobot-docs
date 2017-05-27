# Going further

So, now you're ready to do your first real Discord bot using Krobot ! Don't forget to look at the reference documentation if you forgot something, and keep the JDA documentation with you also.

## Publishing your bot

To publish your bot we will create a distribution zip using Gradle. First you need to add the 'application' gradle plugin and define your main class :

```groovy
apply plugin: 'application'

mainClassName = 'your.bot.MyBot'
```

Now you can either launch `gradle distZip` to create a zip \(in `build/distributions/yourbot-version.zip`\) containing your bot \(to launch it, unzip it and then launch `bin/yourbot`\), or launch the `gradle run` task to directly run it.

You can launch it on a VPS or anything, even a PAAS. Like [Heroku](http://heroku.com/) or [Zeit Now](https://zeit.co/now/).

## JDA Events

You'll probably need to use JDA Events directly sometime, so here is how you register one :

```java
@SubscribeEvent // net.dv8tion.jda.core.hooks.SubscribeEvent
public void yourEvent(ExampleEvent event) // The method name can be anything
{
    // ...
}
```

See [here](https://github.com/DV8FromTheWorld/JDA/tree/master/src/main/java/net/dv8tion/jda/core/events) for the list of the events.

The event you choose depends on the class of the event parameter. Don't forget to register the class where the function is to JDA :

```java
@Inject
private JDA jda;

...

jda.addEventListener(this);
```

## APIs used by Krobot

Krobot uses a lot of libraries, here is a simple list with their docs :

| Library | Doc |
| :--- | :--- |
| Google Guice \(4.1\) | [https://github.com/google/guice/wiki](https://github.com/google/guice/wiki) |
| Apache Commons Lang 3 \(3.5\) | [https://commons.apache.org/proper/commons-lang/](https://commons.apache.org/proper/commons-lang/) |
| Guava \(19.0\) | [https://github.com/google/guava/wiki](https://github.com/google/guava/wiki) |
| Log4J \(2.8\) | [https://logging.apache.org/log4j/2.x/](https://logging.apache.org/log4j/2.x/) |
| Jetbrains Annotation \(15.0\) | \`@Nullable\` and \`@NotNull\` annotations |
| Gson \(2.8\) | [https://github.com/google/gson/blob/master/UserGuide.md](https://github.com/google/gson/blob/master/UserGuide.md) |
| Apache Commons Collections \(4.1\) | [https://commons.apache.org/proper/commons-collections/](https://commons.apache.org/proper/commons-collections/) |



