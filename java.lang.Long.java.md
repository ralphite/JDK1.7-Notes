##java.lang.Long.java.md
------------

> see http://my.oschina.net/wnayuanbiao/blog/189603

Long's toString static method is similar Integer's. see
https://gist.github.com/yadongwen/11279959

This class also uses some tricks from *Hacker's delights*, e.g.
converting `i/10` to `(i*52429)>>>19`.

Unlike integer the stringSize method is not optimized with a constant
array.

> static parseLong(String s, int radix);
>
> https://gist.github.com/yadongwen/11280140

Unlike Integer, Long only caches 256 instances from -128 to 127

> Note Long's decode method
>
> https://gist.github.com/yadongwen/11280757

hashCode is the exclusive or of the two halves

```
    public int hashCode() {
        return (int)(value ^ (value >>> 32));
    }
```

note the usage of conditional operator below

```
    public static int compare(long x, long y) {
        return (x < y) ? -1 : ((x == y) ? 0 : 1);
    }
```

---------------------

explanation (attempts) of the bit twiddling part

see Hackers' Delights for details


> get the highest one bit, e.g highestOneBit(7) returns 4
>
> change all bits after the highest 1 bit to 1. first change the bit
> right of the highest 1 bit, then 2 bits at a time....
>

```
    public static long highestOneBit(long i) {
        // HD, Figure 3-1
        i |= (i >>  1);
        i |= (i >>  2);
        i |= (i >>  4);
        i |= (i >>  8);
        i |= (i >> 16);
        i |= (i >> 32);
        return i - (i >>> 1);
    }
```

> imagine adding i and -i bit by bit and get 0x00000000

```
    public static long lowestOneBit(long i) {
        // HD, Section 2-1
        return i & -i;
    }
```

> binary searching the highest order 1 bit in combination with
>
> bit shifts

```
    public static int numberOfLeadingZeros(long i) {
        // HD, Figure 5-6
         if (i == 0)
            return 64;
        int n = 1;
        int x = (int)(i >>> 32);
        if (x == 0) { n += 32; x = (int)i; }
        if (x >>> 16 == 0) { n += 16; x <<= 16; }
        if (x >>> 24 == 0) { n +=  8; x <<=  8; }
        if (x >>> 28 == 0) { n +=  4; x <<=  4; }
        if (x >>> 30 == 0) { n +=  2; x <<=  2; }
        n -= x >>> 31;
        return n;
    }
```

> similar as the one above, binary search is used here

```
    public static int numberOfTrailingZeros(long i) {
        // HD, Figure 5-14
        int x, y;
        if (i == 0) return 64;
        int n = 63;
        y = (int)i; if (y != 0) { n = n -32; x = y; } else x = (int)(i>>>32);
        y = x <<16; if (y != 0) { n = n -16; x = y; }
        y = x << 8; if (y != 0) { n = n - 8; x = y; }
        y = x << 4; if (y != 0) { n = n - 4; x = y; }
        y = x << 2; if (y != 0) { n = n - 2; x = y; }
        return n - ((x << 1) >>> 31);
    }
```

> rotation is quite easy to understand.
>
>> note shifting a negative value -i means shifting 32-i

```
    public static long rotateLeft(long i, int distance) {
        return (i << distance) | (i >>> -distance);
    }
```

```
    public static long rotateRight(long i, int distance) {
        return (i >>> distance) | (i << -distance);
    }
```

> imagine how negative numbers are stored.
>
>> see http://en.wikipedia.org/wiki/Two's_complement
>>
>> see http://www.programminglogic.com/how-computers-represent-negative-binary-numbers/

```
    public static int signum(long i) {
        // HD, Section 2-7
        return (int) ((i >> 63) | (-i >>> 63));
    }
```

> let i=ABCDEFGH, after first line i becomes BADCFEHG
>
> i << 48 is HG000000
>
> (i & 0xffff0000L) << 16 is 00FE0000
>
> (i >>> 16) & 0xffff0000L is 0000DC00
>
> i >>> 48 is 0000000BA

```
    public static long reverseBytes(long i) {
        i = (i & 0x00ff00ff00ff00ffL) << 8 | (i >>> 8) & 0x00ff00ff00ff00ffL;
        return (i << 48) | ((i & 0xffff0000L) << 16) |
            ((i >>> 16) & 0xffff0000L) | (i >>> 48);
    }
```

> pretty simple if you understand the one above

```
    public static long reverse(long i) {
        // HD, Figure 7-1
        i = (i & 0x5555555555555555L) << 1 | (i >>> 1) & 0x5555555555555555L;
        i = (i & 0x3333333333333333L) << 2 | (i >>> 2) & 0x3333333333333333L;
        i = (i & 0x0f0f0f0f0f0f0f0fL) << 4 | (i >>> 4) & 0x0f0f0f0f0f0f0f0fL;
        i = (i & 0x00ff00ff00ff00ffL) << 8 | (i >>> 8) & 0x00ff00ff00ff00ffL;
        i = (i << 48) | ((i & 0xffff0000L) << 16) |
            ((i >>> 16) & 0xffff0000L) | (i >>> 48);
        return i;
    }
```

> count number of 1s in groups of 2, 4, 8, 16...
>
> 1st line: e.g. (01)(11)(10)(00) ==> (01)(10)(01)(00)
>
> 2nd line: e.g. (0011)(1110) ==> (0010)(0011)
>
> ...
>
> last line only gets the last 7 bits since the return value cannot be greater
> than 64

```
     public static int bitCount(long i) {
        // HD, Figure 5-14
        i = i - ((i >>> 1) & 0x5555555555555555L);
        i = (i & 0x3333333333333333L) + ((i >>> 2) & 0x3333333333333333L);
        i = (i + (i >>> 4)) & 0x0f0f0f0f0f0f0f0fL;
        i = i + (i >>> 8);
        i = i + (i >>> 16);
        i = i + (i >>> 32);
        return (int)i & 0x7f;
     }
```
