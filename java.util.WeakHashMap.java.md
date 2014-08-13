## java.util.WeakHashMap.java.md

An Entry of WeakHashMap will be automatically removed when the key is on longer in ordinary use.

More precisely, the presence of a mapping for a given key will not prevent the key from being 
discarded by the GC, that is, made finalizable, finalized, and then reclaimed.

The class is intended primarily for use with key objects whose *equals* methods test for object
identity using the == operator. Once such a key is discarded it can never be recreated.

Due to the behavior of GC, some familiar invariants in HashMap do not hold for this class.

Each key object in a WeakHashMap is stored indirectly as the referent of a weak reference. Therefore
a key will automatically be removed only after the weak references to it, both inside and outside
of the map, have been cleared by the GC.

The value objects in a WeakHashMap are held by ordinary strong references.


```java
    /**
     * Expunges stale entries from the table.
     */
    private void expungeStaleEntries() {
        for (Object x; (x = queue.poll()) != null; ) {
            synchronized (queue) {
                @SuppressWarnings("unchecked")
                    Entry<K,V> e = (Entry<K,V>) x;
                int i = indexFor(e.hash, table.length);

                Entry<K,V> prev = table[i];
                Entry<K,V> p = prev;
                while (p != null) {
                    Entry<K,V> next = p.next;
                    if (p == e) {
                        if (prev == e)
                            table[i] = next;
                        else
                            prev.next = next;
                        // Must not null out e.next;
                        // stale entries may be in use by a HashIterator
                        e.value = null; // Help GC
                        size--;
                        break;
                    }
                    prev = p;
                    p = next;
                }
            }
        }
    }
```
