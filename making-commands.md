# Making commands

So, let's create our first command.

The object that manages the commands is the **CommandManager**. Command are registered to it, and it will parse the messages to check for command call, then call them.

The CommandManager is automatically injected using Dependency Injection, just create an empty field, and put the "@Inject" annotation on it.

```java
@Inject
private CommandManager commands;
```

## Command paths

Let's talk about the command path syntax. It's the kind of things that looks like that :

```
!command <required> [optional]
```

What does this mean ? It is a way to describe the command and its arguments, including their type and if they are required.

### Syntax

First, put the label \(it can include a prefix or anything you want\) :

```
!hello
```

This is the path of a simple command " !hello ".

Then, add its args. Each required arg must be surrounded by **"&lt; &gt;"** and optional arg by **"\[ \]"**. Optionals args must be at the end. Args are named : you can then retrieve their values using the name you've given to them.

```
!hello <first_name> [last_name]
```

This is the path of a simple command " !hello ", with a required arg " first\_name ", and an optional arg " last\_name ".

You can also make "list" args, they must be at the end of the path, and they are arguments that can take any amount of arg.

```
!hello [names...]
```

This is the path of a simple command " !hello " that can take any number of argument to a list called " names ".

### Args types

You can add type annotations to the args. The types are :

* number
* string \(default\)
* user

```
!hello <to:user>
```

This is the path of a simple command " !hello ", with a required arg " to " that is a user \(can be a user name, nickname, or mention, or even ID\).

Types can also be put on a list :

```
!hello <to:user...>
```

In this case " to " is a user list.

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

So we ask the command manager to create a command using our path, for this, use _CommandManager\#make_  :

```java
commands.make("!hello [message]", (context, args) -> {
    // The action
}).register();
```

Here, the anonymous function is the command call action. We registered a command with the path '!hello \[message\]' that will trigger our function when called.

**Don't forget the .register\(\); or it will do nothing but return the created command without registering it.**

Then, we send the message :

```java
context.sendMessage("{} {}",
                    args.containsKey("message") ? "Hello" : args.get("message").getAsString(),
                    context.getUser().getAsMention());
```

As you see, the String given to sendMessage goes automatically through _String\#format._ So, this should work, you can launch and then test !

