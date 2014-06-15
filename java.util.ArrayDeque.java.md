##java.util.ArrayDeque.java.md
----------

This is a resizable-array implementation of th Deque interface. Not thread-safe.

Likely to be faster than `Stack` when used as a stack and faster than `LinkedList`
when used as a queue.

The capacity of an ArrayDeque is always power of 2.

> Note how the following code is used to find the best power of 2 for capacity

```java
        int initialCapacity = MIN_INITIAL_CAPACITY;
        // Find the best power of two to hold elements.
        // Tests "<=" because arrays aren't kept full.
        if (numElements >= initialCapacity) {
            initialCapacity = numElements;
            initialCapacity |= (initialCapacity >>>  1);
            initialCapacity |= (initialCapacity >>>  2);
            initialCapacity |= (initialCapacity >>>  4);
            initialCapacity |= (initialCapacity >>>  8);
            initialCapacity |= (initialCapacity >>> 16);
            initialCapacity++;

            if (initialCapacity < 0)   // Too many elements, must back off
                initialCapacity >>>= 1;// Good luck allocating 2 ^ 30 elements
        }
```

.

> Note how head was dealt with on line 227 and line 244

```java
        elements[head = (head - 1) & (elements.length - 1)] = e;
        //...
        if ( (tail = (tail + 1) & (elements.length - 1)) == head)
```

the most interesting part is how to deal with head and tail with mask.

