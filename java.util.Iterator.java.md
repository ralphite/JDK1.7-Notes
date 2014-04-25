
- This Iterator interface is used to take place of Enumeration
in the Java Collections Framework.

- Iterator allows removing elements during iteration.

- This interface is a member of the Collections Framework


- three abstract methods are required
    - boolean hasNext();
    - E next();
    - void remove();


> note for remove, it can only be called once per call to next()
