##java.util.Map.java.md
----------

The Map interface is not a sub-interface of Collection.

The order of the map is defined as the order in which
the iterators on the map's collection views return
their elements.

methods

- int size()
- boolean isEmpty()
- boolean containsKey(Object key)
- boolean containsValue(Object value)
- V get(Object key)

- V put(K k, V v)
- remove(Object key)

- putAll(Map<? extends K, ? extends V> m);
- void clear()

- Set<K> keySet()
- Collection<V> values()
- Set<Map.Entry<K, V>> entrySet()

- boolean equals(Object o)
- int hashCode()
