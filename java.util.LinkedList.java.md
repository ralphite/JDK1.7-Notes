##java.util.LinkedList.java.md
----------------

LinkedList implements **List** and **Deque** and is a **doubly-linked list**.

This is a typical wide interface which is too big thus not good.

Same as ArrayList, LinkedList is not synchronized.

```
List list = Collections.synchronizedList(new LinkedList(...));
```

Same as ArrayList, iterator() and listIterator() are fail-fast.

>note the link and unlink private methods to add and remove a
node in the doubly-linked list
>>https://gist.github.com/995b244f7d23c0735271
>>>>**draw chart and see how these methods are implemented**

###methods

####as a deque(double ended queue)

- getFirst()
- getLast()
- addFirst(E e)
- addLast(E e)
- removeFirst()
- removeLast()

####as a collection

- contains(Object o)
- size()
- add(E e)
- remove(Object o)
- addAll(Collection<? extends E> c)
- clear()

####as a list

- get(int index)
- set(int index, E e)
- add(int index, E e)
- remove(int index)
- indexOf(Object o)
- lastIndexOf(Object o)

> note in line 567 how to determine whether to move to the specified index
from the end or from the beginning

####as a queue

- peek()
- element()
- poll()
- remove()
- offerFirst(E e)
- offerLast(E e)
- peekFirst()
- peekLast()
- pollFirst()
- pollLast()
- removeFirstOccurrence(Object o)
- removeLastOccurrence(Object o)

####as a stack

- push(E e)
- pop()

> in ListItr note many calls of checkForComodification() which may throw
ConcurrentModificationException

..

> note the descendingIterator() method which returns an instance of 
DescendingIterator class

..

> note the implementation of clone(). this is a **shallow copy** and the
elements are not cloned if they are objects

```

    /**
     * Returns a shallow copy of this {@code LinkedList}. (The elements
     * themselves are not cloned.)
     *
     * @return a shallow copy of this {@code LinkedList} instance
     */
    public Object clone() {
        LinkedList<E> clone = superClone();

        // Put clone into "virgin" state
        clone.first = clone.last = null;
        clone.size = 0;
        clone.modCount = 0;

        // Initialize clone with our elements
        for (Node<E> x = first; x != null; x = x.next)
            clone.add(x.item);

        return clone;
    }
```

..

> make sure fully understand the following code

```

    @SuppressWarnings("unchecked")
    public <T> T[] toArray(T[] a) {
        if (a.length < size)
            a = (T[])java.lang.reflect.Array.newInstance(
                                a.getClass().getComponentType(), size);
        int i = 0;
        Object[] result = a;
        for (Node<E> x = first; x != null; x = x.next)
            result[i++] = x.item;

        if (a.length > size)
            a[size] = null;

        return a;
    }
```
