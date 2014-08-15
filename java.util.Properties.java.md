### java.util.Properties.java.md

A subclass of Hashtable<Object, Object> which means it's not generic.

Can be saved to a stream or loaded from a stream.

Each key and corresponding value in the property list is a string.

`setProperties` should be used instead of `put` and `putAll` since 
non-string keys and values can be inserted which should not be allowed.

Most methods are IO related.
