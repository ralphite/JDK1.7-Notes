##java.lang.StringBuilder.java.md
------------

Both StringBuilder and StringBuffer are for mutable strings. They have the same API.

StringBuilder comes later and is a drop-in replacement for StringBuffer in single
thread environment which is usually the case. It provides better performance, thus
is recommended.

StringBuilder and StringBuffer are based on the AbstractStringBuilder abstract class,
which actually contains most of the implementation logic.

`StringBuilder`'s constructors ensures a default capacity of 16 characters in the private
char array and 16 more spaces if an init arg is provided, such as a string.

A lot of overloaded `append`, `insert`, `replace`, `delete`, `indexOf` and `lastIndexOf`
methods are provided.

There is also a useful `reverse` method provided to reverse the chars
