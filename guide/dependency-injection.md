# Dependency injection

Krobot uses Guice, a dependency injection framework. What is dependency injection ? To be simple, it can automatically create class instances, recursively, by filling its fields, instantiating them also. This is called "injecting" a field. Obviously this is not simple like that but,  you can make providers functions, provide Singleton to inject, use annotations, and more. This is very customizable.

Krobot uses it to inject a lot of its Singleton like the CommandManager, JDA, ConfigProvider, etc...

### Example

The CommandManager is injected by Guice when it creates your bot :

```java
@Inject
private CommandManager commands;
```

The " _@Inject_ " annotation means that this field should be filled by Guice. Obviously, Guice only fill the fields of the class that it creates. Your bot instance is created by Guice, but you can also manually create classes using it, by accessing the injector instance :

```java
MyClass myClass = Krobot.injector().getInstance(MyClass.class);
```

We will see later that Krobot always tries to use dependency injection, like for Commands.

## Modules

Guice uses "Modules" to define injection rules like an instance to provide, or a binding from an interface to a class. To provide your own module, you need to give them to the _Krobot\#start_ function in your bot_ \#main_ function like that : 

```java
Krobot.start(MyBot.class, new MyCustomModule());
```

Here is an example :

```java
public class MyCustomModule extends AbstractModule
{
    @Override
    protected void configure()
    {
        bind(MyClass.class).toInstance(new MyClass("test"));
        bind(MyInterface.class).to(MyInterfaceImpl.class);
    }
}
```

Then, if in your bot/command/etc... you use :

```java
@Inject
private MyClass myClass;

@Inject
private MyInterface myInterface;
```

* _myClass_ -&gt; Will be filled by the instance you configured
* _myInterface_ -&gt; Will be filled by an instance of _MyInterfaceImpl_

**Note : **When Guice is creating instance, it will do a new instance for every field. To make him use the same instance after creating one, you can either use _bind\(...\).toInstance_, or just put the _@Singleton_ annotation on the class.

## Krobot singletons

Here is the singletons that Krobot configured, that you can use in your class made using dependency injection \(your bot, and others that we will see further\) :

* The JDA instance
* The CommandManager
* The ConfigProvider \(we'll see later what is this\)

**Note :** To access JDA when you can't use dependency injector, use _Krobot.jda\(\)_

## Going further

Obviously there is a lot of thing you can do with Guice, i just showed you the basics. To see more about Guice, you can look at [its official wiki](https://github.com/google/guice/wiki "Guice official wiki")



