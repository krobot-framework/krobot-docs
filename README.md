![](/assets/logo_full_black.png)

# The Krobot Framework

The Krobot framework is a modern Discord bot framework based on **discord.js** \(JS version\) **JDA** \(Java version\). This book contains a complete guide to create a full-featured Discord bot, and also the reference for the framework features.

The main part of the framework is the engine is the command system. In fact, in Javascript, because of the langage features, the framework only contains the command engine.

You can start from [the main guide](/guide/getting-started.md "Guide beggining") or just keep the book with you when developing.

{% method %}

### Preview

Here is a simple preview on the right. Don't forget to click on the languages buttons on the top-right corner of the window to swap the code language between Java/JavaScript.

{% sample lang="js" %}

```js
const { CommandManager } = require('krobotjs');

commands.group().prefix('!').apply(_ => {
  commands
    .command('test <message> <nb:^[0-9]+$> [opt]', (message, args) => message.reply(`Test : (${args.get('nb')}`)).register()
    .sub('example', (message, args) => message.reply('I am !test example')).register();
  commands
    .command('test2 <message>', (message, args) => message.reply(`Second test : $message`)).register();
});
```

{% sample lang="java" %}

```java
@Inject
private CommandManager commands;

commands.group().prefix("!").apply(() -> {
  commands
    .command("test <message> <nb:number> [opt]", (context, args) -> context.sendMessage("Test : ", args.get('nb'))).register()
    .sub("example", (context, args) -> context.sendMessage("I am !test example")).register();
  commands
    .command("test2 <message>", (context, args) -> context.sendMessage("Second test : {}", args.get("message"))).register();
});
```

{% endmethod %}



