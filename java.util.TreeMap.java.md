## java.util.TreeMap.java.md

Extends `NavigableMap` which extends `SortedMap`.

`Sorted Map`

- SortedMap<K, V> subMap(K fromKey, K toKey)
- SortedMap<K, V> headMap(K toKey)
- SortedMap<K, V> tailMap(K fromKey)


`NavigableMap`

- Map.Entry<K,V> lowerEntry(K key);
- Map.Entry<K,V> higherEntry(K key);
- Map.Entry<K,V> floorEntry(K key);
- Map.Entry<K,V> ceilingEntry(K key);
- Map.Entry<K,V> firstEntry();
- Map.Entry<K,V> lastEntry();
- Map.Entry<K,V> pollFirstEntry();
- NavigableMap<K,V> descendingMap();
