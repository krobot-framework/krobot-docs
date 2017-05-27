# Separating your code in classes

Ok now we're at a point where we need to clean out a little bit our code.

## Commands

To clean our commands, we will separated the command actions in classes that implements _CommandHandler_ and separate the command registering in a method that will replace the group apply.

### Before

```java
public class MyBot implements IBot
{
    @Inject
    private CommandManager commands;

    @Override
    public void init()
    {
        commands.group().prefix("!").apply(() -> {
            commands.make("!test", (context, args) -> {
                context.sendMessage("Test !");
            }).register();

            commands.make("!hello [name]", (context, args) -> {
                String name = "World";

                if (args.containsKey("name")) {
                    name = args.get("name").getAsString();
                }

                context.sendMessage("Hello {} !", name);
            }).register();
        });
    }
}
```

### After

```java
public class MyBot implements IBot
{
    @Inject
    private CommandManager commands;

    @Override
    public void init()
    {
        commands.group().prefix("!").middlewares(TestMiddleware.class).apply(this::commands);
    }

    private void commands()
    {
        commands.make("!test", TestCommand.class).register();
        commands.make("!hello [name]", HelloCommand.class).register();    
    }
}

public class TestMiddleware implements Middleware
{
    private static final Logger LOGGER = LogManager.getLogger("TestMiddleware");

    public void handle(@NotNull Command command, @NotNull CommandContext context, @Nullable Map<String, SuppliedArgument> args) throws Exception
    {
        LOGGER.info("Command call ({}) handled !", command.toString());
    }
}

public class TestCommand implements CommandHandler
{
    public void handle(@NotNull CommandContext context, @NotNull Map<String, SuppliedArgument> args) throws Exception
    {
        context.sendMessage("Test !");
    }
}

public class HelloCommand implements CommandHandler
{
    public void handle(@NotNull CommandContext context, @NotNull Map<String, SuppliedArgument> args) throws Exception
    {
        String name = "World";

        if (args.containsKey("name"))
        {
            name = args.get("name").getAsString();
        }

        context.sendMessage("Hello {} !", name);
    }
}
```



**Important note : **You should see that we changed `middleware` to `middlewares` . The first one is when providing lambda or Middleware class instance, and the other one is for lambdas. That's because of a Java lambda type interop bug with varargs.

## Configs

The Dependency Injection make configurations very easy to use outside of the bot. You can by example use it in your command :

```java
public class HelloCommand implements CommandHandler
{
    @Inject
    private ConfigProvider config;

    public void handle(@NotNull CommandContext context, @NotNull Map<String, SuppliedArgument> args) throws Exception
    {
        String name = config.at("hello.defaultName");

        if (args.containsKey("name"))
        {
            name = args.get("name").getAsString();
        }

        context.sendMessage("{} {} !", config.at("hello.helloPhrase"), name);
    }
}
```

## Logging

You need to create a Logger in EVERY CLASS you want to use Logging, a logger should ALWAYS be private. Example :

```java
public class TestCommand implements CommandHandler
{
    private static final Logger LOGGER = LogManager.getLogger("TestCommand");

    public void handle(@NotNull CommandContext context, @NotNull Map<String, SuppliedArgument> args) throws Exception
    {
        LOGGER.info("Test command handled");
        context.sendMessage("Test !");
    }
}
```

---



