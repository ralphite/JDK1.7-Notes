##java.lang.Dictionary.java.md
--------

Dictionary is an obsolete abstract class for key-value
mapping classes. New implementations should use the
Map interface

methods different from Map

- Enumeration<k> keys()
- Enumeration<V> elements()

which correspond to

- Set<K> keySet()
- Collection<V> values()
