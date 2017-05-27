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
        commands.group().prefix("!").apply(this::commands);
    }
    
    private void commands()
    {
        commands.make("!test", TestCommand.class).register();
        commands.make("!hello [name]", HelloCommand.class).register();    
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



