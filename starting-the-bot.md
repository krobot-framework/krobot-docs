{% method %}

## Start the bot

So, we're going to initialize the bot itself.

We will create the bot and login it using the bot token. **Again, I repeat, don't publish your bot token !**

I will not really learn you to use JDA or Discord.js, but you can always look at their documentations :

 - [JDA](https://github.com/DV8FromTheWorld/JDA/wiki "JDA documentation")
 - [Discord.JS](https://discord.js.org/#/docs/main/stable/general/welcome "Discord.JS documentation")

You will need first to add your bot to a guild. The link should be like that :

```
https://discordapp.com/api/oauth2/authorize?client_id=YOUR_CLIENT_ID&scope=bot&permissions=0
```

Obviously replace the "YOUR\_CLIENT\_ID" by the client ID that you had before. Using this link you can add your bot to discord guilds.


{% sample lang="js" %}

We will start by creating a Discord JS client :

```js
const Discord = require('discord.js');
const bot = new Discord.Client();
```

This is the main API constant : The Discord Client. The start point of your bot.
We need then to provide the token :

```js
bot.login("Your token");
```

**Remember, this line should ALWAYS be at the end of your start script !**

To test our bot, let's log the messages :

```js
bot.on('message', message => console.log(message));
```

Start it, and it should display on the console, every message sent in the guild where he is.

{% sample lang="java" %}

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

{% endmethod %}

