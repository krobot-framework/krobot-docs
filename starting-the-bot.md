## Starting the bot

So, we're going to initialize the bot itself. We will create the bot and login it using the bot token. **Again, I repeat, don't publish your bot token !**

I will not really learn you to use JDA, but you can always look at [its documentation](https://github.com/DV8FromTheWorld/JDA/wiki "JDA documentation"). Also, you will need first to add your bot to a guild. The link should be like that :

```
https://discordapp.com/api/oauth2/authorize?client_id=YOUR_CLIENT_ID&scope=bot&permissions=0
```

Obviously replace the "YOUR\_CLIENT\_ID" by the client ID that you had before. Using this link you can add your bot to discord guilds, so keep it with you !

At first, we create a class that implements Bot :

```java
public class MyBot implements IBot
{
    @Override
    public void init()
    {
        System.out.println("I am initializing");
    }
}
```

You need then, to start your bot, to ask Krobot to start it, like this :

```java
public static void main(String[] args) throws LoginException, InterruptedException, RateLimitedException
{
    Krobot.start("Your bot token", MyBot.class);
}
```

Obviously, replace "Your bot token" with the bot token you had before.

You can now launch your bot, you should see a lot of logs, and your "I am initializing" in the middle of them.

--&gt;

