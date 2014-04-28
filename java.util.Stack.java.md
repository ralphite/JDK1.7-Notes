##java.util.Stack.java.md
----------

Stack is a subclass of Vector thus implements RandomAccess and List,
thus may have bad performance. Use Deque and it's implementations 
when possible, e.g.

```
Deque<Integer> stack = new ArrayDeque<Integer>();
```
