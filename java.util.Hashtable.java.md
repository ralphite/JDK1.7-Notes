### java.util.Hashtable.java.md


This Map implentation is generally deprecated. 
If a thread-safe implementation is not needed we 
should use `HashMap`. Otherwise, `java.util.concurrent.ConcurrentHashMap`
is prefered.

Difference from HashMap

- `null` key not allowed
- Hashtable is sychronized
- Enumeration used for iteration
