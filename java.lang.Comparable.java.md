##java.lang.Comparable.java.md
----------

this interface imposes a **total ordering** on the objects
of each class that implements it. this ordering is referred
to as the class's **natural ordering** and the only required
method `compareTo` is referred to as its **natural comparison
method**

Objects of classes that implement this interface can be used
as keys of a SortedMap or as elements of a SortedSet.

Lists and arrays of objects implementing this interface can
be sorted with `Collections.sort` and `Arrays.sort`

> note the natural ordering of a class should be consistent
with the `equals` method.

The only method specified in this interface is `compareTo()`

> It is strongly recommended, but not strictly required that
(x.compareTo(y)==0) == (x.equals(y)). Generally speaking, any
class that implements the Comparable interface and violates
this condition should clearly indicate this fact. The
recommended language is "Note: this class has a natural
ordering that is inconsistent with equals."

