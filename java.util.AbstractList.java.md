##java.util.AbstractList.java.md
----------

Like AbstractCollection for Collection, this AbstractList abstract class is a
minimal implementation of List to avoid duplicated code.

Iterator and ListIterator are implemented in this class on top of the random
access methods.

> Note how the indexOf and lastIndexOf methods are implemented with ListIterator

```
    public int indexOf(Object o) {
        ListIterator<E> it = listIterator();
        if (o==null) {
            while (it.hasNext())
                if (it.next()==null)
                    return it.previousIndex();
        } else {
            while (it.hasNext())
                if (o.equals(it.next()))
                    return it.previousIndex();
        }
        return -1;
    }
```

> note the overloaded listIterator method which returns a ListIterator starting
from a specific index

```
public ListIterator<E> listIterator(final int index);
```

The most important part is the Itr and ListItr private classes

> see for definition here: https://gist.github.com/yadongwen/11347230

###Itr

core methods are hasNext(), next() and remove()

>> note the checkForComodification() method is called many times to avoid
**ConcurrentModificationException**

```
        final void checkForComodification() {
            if (modCount != expectedModCount)
                throw new ConcurrentModificationException();
        }
```

>> note line 374 and 426's usage of OuterClass.this.method


###ListItr

This interface inherits the methods from Itr. The following methods are added

- hasPrevious()
- previous()
- nextIndex()
- previousIndex()
- set(E, e)
- add(E, e)

>>>>Need to fully understand the Iterator pattern

...

> note the following implementation of subList

```
    public List<E> subList(int fromIndex, int toIndex) {
        return (this instanceof RandomAccess ?
                new RandomAccessSubList<>(this, fromIndex, toIndex) :
                new SubList<>(this, fromIndex, toIndex));
    }
```

>> note line 523. Brilliant!

```
    public boolean equals(Object o) {
        if (o == this)
            return true;
        if (!(o instanceof List))
            return false;

        ListIterator<E> e1 = listIterator();
        ListIterator e2 = ((List) o).listIterator();
        while (e1.hasNext() && e2.hasNext()) {
            E o1 = e1.next();
            Object o2 = e2.next();
            if (!(o1==null ? o2==null : o1.equals(o2)))
                return false;
        }
        return !(e1.hasNext() || e2.hasNext());
    }
```

hashCode is calc'd similar to Arrays.hashCode

> also note the brilliant usage of conditional operator here

..

>> hmm this code doesn't smell like Josh Bloch's

..

>> note again many checkForComodification method calls are placed
to enhance *fail-fast*

see the listIterator method of SubList. dam it i can't read!!!

```
    public ListIterator<E> listIterator(final int index) {
        checkForComodification();
        rangeCheckForAdd(index);

        return new ListIterator<E>() {
            private final ListIterator<E> i = l.listIterator(index+offset);

            public boolean hasNext() {
                return nextIndex() < size;
            }

            public E next() {
                if (hasNext())
                    return i.next();
                else
                    throw new NoSuchElementException();
            }

            public boolean hasPrevious() {
                return previousIndex() >= 0;
            }

            public E previous() {
                if (hasPrevious())
                    return i.previous();
                else
                    throw new NoSuchElementException();
            }

            public int nextIndex() {
                return i.nextIndex() - offset;
            }

            public int previousIndex() {
                return i.previousIndex() - offset;
            }

            public void remove() {
                i.remove();
                SubList.this.modCount = l.modCount;
                size--;
            }

            public void set(E e) {
                i.set(e);
            }

            public void add(E e) {
                i.add(e);
                SubList.this.modCount = l.modCount;
                size++;
            }
        };
    }
```

> I like the subList method of the RandomAccessSubList class

```
class RandomAccessSubList<E> extends SubList<E> implements RandomAccess {
    RandomAccessSubList(AbstractList<E> list, int fromIndex, int toIndex) {
        super(list, fromIndex, toIndex);
    }

    public List<E> subList(int fromIndex, int toIndex) {
        return new RandomAccessSubList<>(this, fromIndex, toIndex);
    }
}
```

