# Logging

As you probably already saw, Krobot uses a logging engine. What is logging ? It's the art of doing `System.out.print`, like this :

```
[22:17:10] [DEBUG] [Command] Parsing command call for -> /clear
```

Krobot uses Apache Log4J as logging engine. It already has a bundled config for it. **You should always use logging instead of `System.out.print`.**

## How to use it

In each class you want to use a logger, you need to create a private constant instance :

```java
import org.apache.logging.log4j.LogManager; // Choose the right imports
import org.apache.logging.log4j.Logger;

private static final Logger LOGGER = LogManager.getLogger(YourClass.class);
```

This will create a logger called "YourClass", but you can also put a String as name.

Then you can use different functions, depending on the information to print :

* fatal =&gt; Fatal errors
* error =&gt; Errors
* warn =&gt; Warnings
* info =&gt; Main infos
* debug =&gt; Debug infos
* trace =&gt; Low level infos

They are classed by importance. Krobot is configured to print only debug or greater.

**Example :**

```java
public static final String VERSION = "1.0.0";
private static final Logger LOGGER = LogManager.getLogger(MyBot.class);

LOGGER.info("Bot v{} initialized !", VERSION);
```

Prints :

```java
[20:01:05] [INFO ] [MyBot] Bot v1.0.0 initialized !
```

Log functions can take a lot of parameters, like throwable by example, and it support formatting. Log4J is a very complete logging engine, so you can look at [the official documentation](https://logging.apache.org/log4j/2.x/manual/api.html) if you want to go further !

---



