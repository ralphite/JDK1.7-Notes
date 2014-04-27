##java.util.Deque.java.md
--------

means double ended queue, pronounced as deck

methods

> refer to Queue for the difference of the two kinds of methods

            |                  | first element |                  | last element  
------------|------------------|---------------|------------------|----------------
            | Throws Exception | Special Value | Throws Exception | Special Value 
 **Insert** | addFirst(e)      | offerFirst(e) | addLast(e)       | offerLast(e)  
 **Remove** | removeFirst()    | pollFirst()   | removeLast()     | pollLast()    
 **Examine**| getFirst()       | peekFirst()   | getLast()        | peekLast()    


since Deque is a subinterface of Queue, we still have methods from Queue here

| **Queue Method** | **Equivalent Deque Method** 
|------------------|-----------------------------
| add(e)           | addLast(e) 
| offer(e)         | offerLast(e)
| remove()         | removeFirst()
| poll()           | pollFirst()  
| *element*()      | getFirst() 
| peek()           | peekFirst()

Deque can also be used as a stack

| Stack Method | Equivalent Deque Method
|--------------|------------------------
| push(e)      | addFirst(e)
| pop()        | removeFirst()
| peek()       | peekFirst()

Methods from the Collection interface

```java
boolean remove(Object o);
boolean contains(Object o);
int size();
Iterator<E> iterator();
Iterator<E> descendingIterator();
```

Deque also offers two search and remove methods

- boolean removeLastOccurrence(Object o);
- boolean removeFirstOccurrence(Object o);
