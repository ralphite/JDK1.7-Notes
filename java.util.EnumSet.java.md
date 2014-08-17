### java.util.EnumSet.java.md


> Note EnumSet is an abstract class!


Like EnumMap, all of the elements in an enum set must come from a single
enum type that is specified, explicitly or implicitly, when the set is 
created.

Enum sets are represented internally as **bit vectors** whcih is extremely
compact and efficient. 

EnumSets can be used as a high-quality, typesafe alternative to traditional
int-based **big-flags**.

The iterator returned from the iterator method is weakly consistent: it'll
never throw `ConcurrentModificationException`and it may or may not show the 
effects of any modifications to the set that occur while the iteration is 
in progress.

Null elements are not allowed.
