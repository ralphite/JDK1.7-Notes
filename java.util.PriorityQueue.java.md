##java.util.PriorityQueue.java.md
----------------

>> for better explanation, see http://wlh0706-163-com.iteye.com/blog/1850125

This is an implementation of an unbounded priority queue basd on priority
heap.

>> Need to figure out how to use Comparator.

This is a **min-heap**, which means the head is the least element. If there
is a tie, it's broken arbitrarily.

The Iterator instance returned from iterator() doesn't guarantee particular
traversal order. Use `Arrays.sort(pq.toArray())` if necessary.

O(log(n)) methods -

- offer
- poll
- remove()
- add

O(n) methods -

- remove(Object)
- contains(n)

O(1) methods -

- peek
- element
- size

-------------

The default init capacity is 11.

> note how the capacity grows (double when capacity is small and 1.5 times
when it's big)

most of the methods are just like the ones in ArrayList.

the most interesting methods are siftUp and siftDown. make sure to understand them.
see gist https://gist.github.com/c355bcb61dfadb5feea1

