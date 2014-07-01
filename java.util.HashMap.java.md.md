##java.util.HashMap.java.md
----------

Hash table implementation of the Map interface. null values and the null key are permitted. Order is not guaranteed.

O(1) time performance for `get` and `set`, assuming the hash function disperses the elements properly among the buckets. Iteration requires time proportional to the 'capacity' of the HashMap instance __and__ the number of key-value mappings.

Two parameters:

- initial capacity - the initial number of buckets in the hash table when it's created
- load factor - a measure of how full the capacity is allowed before it's capacity is automatically increased.

When the number of entries in the hash table exceeds the product of the load factor and the current capacity, the hash table is **rehashed** so that the hash table has approximately twice the number of buckets.

If many mappings or k-v pairs are to be stored in the map, create the map with a sufficiently large capacity will avoid rehashing which will rebuild the internal data structure.

Like other types in Collection, HashMap is not synchronized and is **fail-fast**.

----------

> the default initial capacity is 1 << 4 which is 16
>
> the default initial load factor is 0.75f

```java
/**
 * An empty table instance to share when the table is not inflated.
 */
static final Entry<?,?>[] EMPTY_TABLE = {};

/**
 * The table, resized as necessary. Length MUST Always be a power of two.
 */
transient Entry<K,V>[] table = (Entry<K,V>[]) EMPTY_TABLE;
```
