# Configs

Krobot has a powerful and simple configuration engine. The config manager is a singleton, the `ConfigProvider`. To use it, Guice can inject it anywhere :

```java
@Inject
private ConfigProvider configs;
```

First, you need to register the configurations to use. The configurations are named, but if you don't provide a name it will use the file name \(without the extension\).

```java
@Override
public void init()
{
    configs.from("configs/myconfig.json"); // Same as configs.json("configs/myconfig.json");
    Config config = configs.from("configs/myotherconfig.json"); // If you want to use the object directly
    configs.from("configs/coolconfig.json", "cool_config"); // To name the config manually
}
```

`configs.from`  registers a JSON config \(same as `configs.json`\). It returns the created Config object, but you shouldn't have to use it.

You can also use `configs.properties` to register a Java properties config \(object serialization will not be possible\).

`File`  objects can be provided instead of the path.

Now, you can query the values from the configs :

```java
String value = configs.get("myconfig").get("myvalue");
```

This will get the value of the field "myvalue" in the config "myconfig". But, you can also use object serialization \(if it is a JSON config\) :

```java
String[] values = configs.get("myconfig").get("myvalues", String[].class);
MyObject value = configs.get("myconfig").get("myobject", MyObject.class);
```

If you want, you can directly access values of an object, using `at` :

```json
{
    "myobject": {
        "myvalue": "test"
    }
}
```

```java
String value = configs.get("myconfig").at("myobject.myvalue");
```

It also supports the object serialization :

```java
String[] values = configs.get("myconfig").at("myobject.myvalues", String[].class);
```

You can even use `at` directly on the _ConfigProvider_ like this :

```java
String value = configs.at("myconfig.myvalue"); // Same as configs.get("myconfig").get("myvalue");
```

And even do it more deeply :

```java
String value = configs.at("myconfig.myobject.myvalue"); // Same as configs.get("myconfig").at("myobject.myvalue");
```

And even use object serialization :

```java
MyObject value = configs.at("myconfig.myobject", MyObject.class);
```

See, there is a lot of possibilities with the config engine.

---



