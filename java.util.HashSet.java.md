##java.util.HashSet.java.md
----------

- HashSet is backed by a HashMap.
>well hashset is just a shameless modified hashmap!!

- There is no guarantee to the iteration order.
- null is allowed

this implementation offers constant time performance
for the basic operations

- add
- remove
- contains
- size

> HashSet is not synchronized. to synchronize a hashset,
we can use Collections.synchronizedSet() at creation
time.

the iterators returned by the iterator method is **fail-fast**
which means whenever the set is modified after the
iterator is created in any way except the iterator's remove
method, the Iterator will throw a `ConcurrentModificationException`.

note that the `fail-fast` behavior is not guaranteed, thus
we cannot rely on it for feature development

> the default initial capacity of the backing hashmap is 16 and
the default load factor is 0.75 as defined in HashMap

```
    public HashSet(Collection<? extends E> c) {
        map = new HashMap<>(Math.max((int) (c.size()/.75f) + 1, 16));
        addAll(c);
    }
```

> note the usage of a dummy param to distinguish a constructor
from others

writeObject and readObject are provided to serialization and de-serialization

> note how conditional operator is used in line 299

```
        map = (((HashSet)this) instanceof LinkedHashSet ?
               new LinkedHashMap<E,Object>(capacity, loadFactor) :
               new HashMap<E,Object>(capacity, loadFactor));
```
