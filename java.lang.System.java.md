- `in`, `out` and `err` are `InputStream` and `PrintStream`s which can be reassigned with setters
- there are two methods `currentTimeMillis()` and `nanoTime()` to get the system time
- and the famous `arraycopy` method to quickly copy an array

```
public static native void arraycopy(Object src,  int  srcPos,
                                        Object dest, int destPos,
                                        int length);
```

- we can get all or specific properties or environment variables
- we can also do `gc`, `runFinalization`, `load` files, `loadLibrary` and `exit` with various methods

> Note the interesting identityHashCode class method which returns something like the addr of the reference

```
System.identityHashCode(new Object());
```
