### java.util.EnumMap.java.md


A subclass of `AbstractMap`.

All of the keys in an enum map must come from a single enum type
that is specified, explicited or implicitly, when the map is created.

Enum maps are represented internally as arrays whcih is extremely
compact and efficient.

Iterators returned by the **collection views** are weakly consistent.
The interation order is the natural order of the keys (the order in 
which the enum constants are declared).

Null values are permitted while null keys are not.

All basic operations have constant time complexity and the performance
is likely better than HashMap.

```java
    private static final Object NULL = new Object() {
        public int hashCode() {
            return 0;
        }

        public String toString() {
            return "java.util.EnumMap.NULL";
        }
    };
```

