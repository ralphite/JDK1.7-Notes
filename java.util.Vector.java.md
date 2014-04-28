##java.util.Vector.java.md
----------

Vector is **synchronized**. If thread-safe is not required, ArrayList
is preferred.

Vector implements List. The iterators and listIterators returned
are fail-fast.

> note the capacityIncrement field. if it's 0, each time the vector
is full, the capacity will be doubled, otherwise, the capacity
will only increase by capacityIncrement

..

> note the elements method which returns an Enumeration<E>

```
    public Enumeration<E> elements() {
        return new Enumeration<E>() {
            int count = 0;

            public boolean hasMoreElements() {
                return count < elementCount;
            }

            public E nextElement() {
                synchronized (Vector.this) {
                    if (count < elementCount) {
                        return elementData(count++);
                    }
                }
                throw new NoSuchElementException("Vector Enumeration");
            }
        };
    }
```

> note on line 565, an object is specifically assigned null so that
gc will release the memory

```
        elementData[elementCount] = null; /* to let gc do its work */
```

