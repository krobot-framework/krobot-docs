# Message utils

The `MessageUtils` class contains utils method for messages :

## Message splitting

Sometimes it happens that you need to send a message that possibly could be bigger than the Discord message limit, the `MessageUtils#splitMessage` function is here to fix this : it splits your message in messages with at most 1999 characters \(Discord limit\). You can also provide your own limit.

```java
String[] messages = MessageUtils.splitMessage(myLongMessage);
         messages = MessageUtils.splitMessage(myLongMessage, 1999); // Same
```

## String similarity comparator

There is a function to get the most similar string from a list of a given model. Example :

```java
String result = MessageUtils.getMostSimilar("Hello", new String[] {
    "Bonjour",
    "Hallo",
    "Salve",
    "Konichiwa"
});

// result = "Hallo"
```

It uses the [Levenshtein algorithm](https://en.wikipedia.org/wiki/Levenshtein_distance).

---

