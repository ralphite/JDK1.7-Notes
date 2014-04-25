
- this is a package access abstract class serving as parent
class of StringBuilder and StringBuffer which contains most
of the actual implementation of the methods

- a char[] is used internally for the data of the string

- note the difference b/t count and capacity

- note how the char array grows

> the capacity is more than doubled. then the data is COPIED
> to the new location!

```
    void expandCapacity(int minimumCapacity) {
        int newCapacity = value.length * 2 + 2;
        if (newCapacity - minimumCapacity < 0)
            newCapacity = minimumCapacity;
        if (newCapacity < 0) {
            if (minimumCapacity < 0) // overflow
                throw new OutOfMemoryError();
            newCapacity = Integer.MAX_VALUE;
        }
        value = Arrays.copyOf(value, newCapacity);
    }
```

>> there are so many copy-around here. could be a performance issue?

> even trimToSize() copies the 'entire' data to the new location

```
    public void trimToSize() {
        if (count < value.length) {
            value = Arrays.copyOf(value, count);
        }
    }
```

- note when appending an integer or long how the code deals with
1<<31 and 1L<<63

> Integer.MIN_VALUE and Long.MIN_VALUE are almost always the
special cases and have to be taken care of specifically.

- note line 701 where **System.arraycopy** moves data from behind to the front

```
System.arraycopy(value, start+len, value, start, count-end);
```

> also the following code for inserting

```
        ensureCapacityInternal(count + len);
        System.arraycopy(value, index, value, index + len, count - index);
        System.arraycopy(str, offset, value, index, len);
```



