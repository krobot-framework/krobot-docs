# Markdown

Krobot provides a simple Markdown helper using the `Markdown` class :

| Function | Modifier | Result |
| :--- | :--- | :--- |
| Markdown\#bold | \*\*text\*\* | **text** |
| Markdown\#italic | \_text\_ | _text_ |
| Markdown\#underline | \_\_text\_\_ | \(Only on discord\) |
| Markdown\#strikeout | ~~text~~ | ~~text~~ |
| Markdown\#smallCode | \`text\` | `text` |

### Code

```java
Markdown.code("public static void main(String[] args)\n{\n}\n", /* optional */ "java");
```

=&gt;

```java
    public static void main(String[] args)
    {
    }
```

=&gt;

```java
public static void main(String[] args)
{
}
```

---



