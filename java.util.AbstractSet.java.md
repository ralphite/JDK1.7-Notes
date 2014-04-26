##java.util.AbstractSet.java.md
----------

This class doesn't override any methods in AbstractCollection,
it simply adds implementations for `equals`, `hashCode` and
`removeAll`

> note the usage of exception handling in equals

```

    public boolean equals(Object o) {
        if (o == this)
            return true;

        if (!(o instanceof Set))
            return false;
        Collection c = (Collection) o;
        if (c.size() != size())
            return false;
        try {
            return containsAll(c);
        } catch (ClassCastException unused)   {
            return false;
        } catch (NullPointerException unused) {
            return false;
        }
    }
```

> hashCode of a Set is merely the sum of the hashCode of
all elements in the set

```
    public int hashCode() {
        int h = 0;
        Iterator<E> i = iterator();
        while (i.hasNext()) {
            E obj = i.next();
            if (obj != null)
                h += obj.hashCode();
        }
        return h;
    }
```


> note the usage of iterator in for loops in removeAll. this removeAll method
is overridden in all subclasses in jdk

> https://gist.github.com/yadongwen/11314070
