### java.util.BitSet.java.md

`BitSet` doesn't implement the `Collection` inferface and is not part of the 
Java Collections framework.

`BitSet` implements a vector of bits that grows as needed.


- void flip(int bitIndex)
- void flip(int fromIndex, int toIndex)
- void set(int bitIndex)
- void set(int bitIndex, boolean value)
- void set(int fromIndex, int toIndex)
- void set(int fromIndex, int toIndex, boolean value)
- void clear(int bitIndex)
- void clear(int fromIndex, int toIndex)
- boolean get(int botIndex)
- BitSet get(int from, int to)
- int nextSetBit(int from)
- int nextClearBit(int from)
- int previousSetBit(int from)
- int previousClearBit(int from)
- boolean intersects(BitSet set) //returns true if at least at one index both are set to true
- int cardinality() //number of true bits
- void add(BitSet set)
- void or(BitSet set)
- void xor(BitSet set)
- void andNot(BitSet set)

>> A lot of bit manipulations

