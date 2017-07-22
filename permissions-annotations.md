# Permissions annotations

When your bot grows, you will probably want to get rid of all the conditions to check the user's permissions. And when scaling your bot on multiple Guilds, the bot will probably crash sometimes because he misses some permissions.

To fix this problem, Krobot provides simple annotations to put on the command classes.

Example, a !ban command. You want that only the Administrator can call the command :

```java
public class BanCommand implements CommandHandler
{
    ...
}
```

Use the `@UserRequires` annotation with a Permission array :

```java
@UserRequires({ Permission.ADMINISTRATOR })
public class BanCommand implements CommandHandler
```

Now, if the caller isn't an Administrator, an error message will be displayed.

Finally, if your bot hasn't the permission to ban members, the command will crash ! To fix this, use the `@BotRequires` annotation !

```java
@BotRequires({ Permission.BAN_MEMBERS })
@UserRequires({ Permission.ADMINISTRATOR })
public class BanCommand implements CommandHandler
```

Now, if the bot hasn't the permission to ban members, instead of crashing it will display an error message !

### Customizing error messages

You can easily customize the error messages, because when a permission is missing, either a `BotNotAllowedException` or a `UserNotAllowedException` will be thrown, and then caught by the `ExceptionHandler` who by default, prints the error messages. By using your own handler \(see the Exception handler page\) just use a condition with instanceof !



