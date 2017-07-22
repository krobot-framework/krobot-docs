![](/assets/logo_full_black.png)

# The Krobot Framework

The Krobot framework is a modern Discord bot framework based on **discord.js** \(JS version\) **JDA** \(Java version\). This book contains a complete guide to create a full-featured Discord bot, and also the reference for the framework features.

**This is the java version book.**

The framework contains :

* A complete command engine, with middlewares, arguments parsing, and sub commands
* Annotations for permissions
* A powerful config engine
* Dependency injection
* Logging
* Util classes/functions

You can start from [the main guide](/guide/getting-started.md "Guide beggining") or just keep the book with you when developing.

### Preview

Here is a simple preview. Note that the "test &lt;message&gt;" is parsed to be used then to get the args. You should note that this code can be obviously separated into classes \(like the Middleware does\), but everywhere you can put a command, you can put a lambda.

```java
@Inject
private CommandManager commands;

@Inject
private ConfigProvider config;

commands.group().prefix(config.at("app.command.prefix")).apply(() -> {
  commands.make("test <message>", (context, args) ->
    context.sendMessage("Test : {}", args.get("message"));
  ).middlewares(TestMiddleware.class).register();

  commands.make("test2 <amount:number> [targets:users...]", TestCommand.class).register();
  ...
});
```

---



