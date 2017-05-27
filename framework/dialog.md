## Dialog

The Dialog API is a simple method to create dialog-like embeds message \(info/warning/error dialogs\).

```java
context.sendMessage(Dialog.info("My Dialog", "An info dialog"));
context.sendMessage(Dialog.warn("My Dialog", "A warning dialog"));
context.sendMessage(Dialog.error("My Dialog", "An error dialog"));
```

Gives :

![](https://i.gyazo.com/8c16ef6dd1e5d20b4c2fa0a061da7d4c.png)

## Customizing

```java
context.sendMessage(Dialog.dialog(Color.decode("0xABCDEF"), "My Dialog", "A custom dialog", /* Optional */ "http://myawesomesite.com/myawesomeicon.png);
```

Note that there is constants in the Dialog class with the colors and icons used in `Dialog#info` `Dialog#warn` and `Dialog#error`

---



