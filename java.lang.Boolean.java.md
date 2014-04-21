
- just normal methods for converting, parsing, comparing, etc. note how hashCode is implemented
```
public int hashCode() {
    return value ? 1231 : 1237;
}
```

- when constructing, parsing, or getting the value from a String, the case is ignored

```
private static boolean toBoolean(String name) {
    return ((name != null) && name.equalsIgnoreCase("true"));
}
```
