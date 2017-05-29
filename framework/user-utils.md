# User utils

The `UserUtils` class contains utils functions about users :

## User resolving

The `resolve` function can be used to resolve a `User` object from a String.

The given string can be :

* A mention
* A username
* A user ID
* A nickname _=&gt; If the Guild is passed in argument_

Example :

```java
User user = resolve("Litarvan");
          = resolve("@Litarvan");
          = resolve("87279950075293696");
          = resolve("Shark", myGuild);

// user = Litarvan#8232
```

## Private channel

There is a simple function to get the private channel of a user. You can't normally get it directly, you need to open a private channel first if it wasn't before with the target user. The function `privateChannel` will do the work for you. It will return the private channel of the given user, after opening it if needed.

Example :

```java
User litarvan = UserUtils.resolve("Litarvan");
PrivateChannel pm = UserUtils.privateChannel(litarvan);
```

---



