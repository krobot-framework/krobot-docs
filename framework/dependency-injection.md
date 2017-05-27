# Dependency Injection

Krobot uses Guice as dependency injection framework. See its doc [here](https://github.com/google/guice/wiki).

## Registering modules

To register you own modules, provide them to the `Krobot#start` method :

```java
Krobot.start(MyBot.class, new MyModule(), new MyOtherModule(), ...);
```

## Krobot singletons

Krobot defines singletons to use then with dependency injection :

* JDA
* CommandManager
* ConfigProvider
* ExceptionHandler



