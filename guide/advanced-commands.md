# Advanced commands

Let's talk about command a bit deeper.

## Middlewares

{% module %}

Commmand middlewares are functions that triggers before some command call. They can be used on multiple commands, and they can cancel a command call.

In our case, we will just create a middleware that will log the command calls.

{% sample lang="java" %}

The commmand builder has two functions : middleware and middlewares, in this case, use middleware. We will use the other one later.

```java

{% sample lang="js" %}

{% endmodule %}

