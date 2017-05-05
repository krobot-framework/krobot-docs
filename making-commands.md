# Making commands

{% method %}

So, let's create our first command.

The object that manages the commands is the **CommandManager**. Command are registered to it, and it will parse the messages to check for command call, then call them.

{% sample lang="js" %}

Start by importing the CommandManager :

```js
const { CommandManager } = require('krobotjs');
```

Then create an instance of it :

```js
const commands = new CommandManager();
```

{% sample lang="java" %}

The CommandManager in Java is automatically injected using Dependency Injection, just create an empty field, and put the "@Inject" annotation on it.

```java
@Inject
private CommandManager commands;
```

{% endmethod %}

## Command paths

Let's talk about the command path syntax. It's the kind of things that looks like that :

```
!command <required> [optional]
```

What does this mean ? It is a way to describe the command and its arguments, including their type and if they are required.

### Syntax

First, put the label (it can include a prefix or anything you want) :

```
!hello
```

This is the path of a simple command " !hello ".
Then, add its args. Each required arg must be surrounded by **"< >"** and optional arg by **"[ ]"**. Optionals args must be at the end.

```
!hello <first_name> [last_name]
```

This is the path of a simple command " !hello ", with a required arg " first\_name ", and an optional arg " last\_name ".

{% method %}

Args are named. You can then retrieve their values using the name you've given to them.

You can also make "list" args, they must be at the end of the path, and they are arguments that can take any amount of arg. 

```
!hello [names...]
```
This is the path of a simple command " !hello " that can take any number of argument to `a list called " names ".

{% sample lang="js" %}

### Args types

You can define a type for the args using regex. Example for an arg that can only be a number :

```
!hello <amount:^[0-9]+$>
```

This is the path of a simple command " !hello ", with a required arg " amount " that can only be a number.

{% sample lang="java" %}

### Args types

You can add type annotations to the args. The types are :

 - number
 - string (default)
 - user
 
```
!hello <to:user>
```

This is the path of a simple command " !hello ", with a required arg " to " that is a user (can be a user name, nickname, or mention, or even ID).

Types can also be put on list :

```
!hello <to:user...>
```

In  this case " to " is a user list.

{% endmethod %}

{% method %}

## Registering our first command

Let's create our first command. The command will simply say a given message to the caller, or "Hello" by default.

**Example :**

```
Litarvan : !hello
Bot      : Hello @Litarvan

Litarvan : !hello Bonjour
Bot      : Bonjour @Litarvan
```

So what will the path be ? The "message" argument is optional, the label is !hello, so :

```
!hello [message]
```

{% common %}

We ask  the command manager to create a command using our path :

{% sample lang="js" %}

```js
commands.command('!hello [message]', (message, args) => {
    // The action
}).register();
```

{% sample lang="java" %}

```java
commands.make("!hello [message]", (message, args) -> {
    // The action
}).register();
```

{% common %}

Here, the anonymous function is the command call action. We registered a command with the path '!hello [message]' that will trigger our function when called.

**Don't forget the .register(); or it will do nohting but return the created command without registering it.**

{% endmethod %}

