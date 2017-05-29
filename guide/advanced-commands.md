# Advanced commands

Let's talk about command a bit deeper.

## Groups

You can make a "group" of command : it is an anonymous function where you register commands, and these commands will have common attributes. By example, you can define a prefix, that will apply to the commands inside the group :

```java
commands.group().prefix("!").apply(() -> {
    commands.make("test", (context, args) -> context.sendMessage("Test")).register();
    commands.make("hello", (context, args) -> context.sendMessage("Hello !")).register();
});
```

In this example, the commands will not be `test`, and `hello`, but `!test`, and `!hello`, because they are registered in a group with the `!` prefix. Obviously, commands registered outside this group will not have the prefix on them.

## Middlewares

Command middlewares are functions that triggers before some command call. They can be used on multiple commands, and they can cancel a command call.

The command builder has two functions : `middleware` and `middlewares`, in this case, use `middleware`. We will use the other one later.

```java
commands.make("test", (context, args) ->
    context.sendMessage("Test")
).middleware((command, context, args) ->
    LOGGER.info("The command is executed with args {}", args);
).register();
```

In this case, this is not really useful, but you can by example apply it to a group :

```java
commands.group().prefix("!").middleware((command, context, args) ->
    LOGGER.info("A command is executed !")
).apply(() -> {
    commands.make("test", (context, args) -> context.sendMessage("Test")).register();
    commands.make("hello", (context, args) -> context.sendMessage("Hello !")).register();
});
```

With this code, everytime `!test` or `!hello` is called, "A command is executed !" should be printed on the console.

## Sub commands

You can create sub commands, and even sub sub commands. What is a sub command ? By example, you have a command `!test`, and you want to create a sub command `debug`, the sub command will be triggered when a user will type `!test debug`.

Let's write an example :

```java
commands.make("!test", (context, args) ->
    context.sendMessage("Test")
).register().sub("debug", (context, args) ->
    context.sendMessage("Debug")
).register();
```

This will make this :

```
Litarvan : !test
Bot      : Test

Litarvan : !test debug
Bot      : Debug
```

Obviously, you can create more complex commands, they also use the path syntax !

**Important things to know when using sub commands :**

* Groups modifiers \(like the prefix or the middlewares\) aren't applied on the sub commands, only on the parent one.
* Parent command middlewares are called when a sub command is triggered, and they can cancel the call, **in this case, "args" parameter of the middleware is null.**
* You need to call `register()` to then call the `sub()` function, so when dealing with multiple sub commands, put the parent command `register()` result in a Command variable, to then use the sub functions multiple times.

---



