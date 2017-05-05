![](/assets/logo_full_black.png)

# The Krobot Framework

The Krobot framework is a modern Discord bot framework based on **discord.js** \(JS version\) **JDA** \(Java version\). This book contains a complete guide to create a full-featured Discord bot, and also the reference for the framework features.

**This is the java version book.**

The main part of the framework is the engine is the command system, but it has a complete config engine, dependency injection, and more.

You can start from [the main guide](/guide/getting-started.md "Guide beggining") or just keep the book with you when developing.

### Preview

Here is a simple preview. Note that the "test &lt;message&gt;" is parsed to be used then to get the args.

```java
@Inject
private CommandManager commands;

@Inject
private ConfigProvider config;

commands.make(config.at("bot.prefix") + "test <message>", (context, args) ->
  context.sendMessage("Test : {}", args.get("message"));
).middlewares(TestMiddleware.class).register();
```



