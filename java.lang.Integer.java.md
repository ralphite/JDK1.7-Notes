
- there are a few overloaded toString methods which convert an int to Strings of different radix.
    - `public static String toString(int i, int radix);` radix can be any value b/t 2 and 36 inclusive
    - `toHexString`, `toOctalString` and `toBinaryString`
    
> Note the bit manipulations in `toUnsignedString`

..

> be careful with integer overflow, esp. for 0x80000000 and 0x7FFFFFFF

magical parts

```
((q << 6) + (q << 5) + (q << 2)) // q * 100

q = (i * 52429) >>> (16+3); // i / 10. this will be much more efficient than division with JIT VM
```

> see how to calc size of int

```
    final static int [] sizeTable = { 9, 99, 999, 9999, 99999, 999999, 9999999,
                                      99999999, 999999999, Integer.MAX_VALUE };

    // Requires positive x
    static int stringSize(int x) {
        for (int i=0; ; i++)
            if (x <= sizeTable[i])
                return i+1;
    }
```

- like Character, Byte and Short, specific range of Integers are cached for better performance. This range is usually [-128, 127]. We can also configure the upper limit with `-XX:AutoBoxCacheMax=<size>`
- this private static class is like a singleton
- because of this optimization, valueOf(int) can be more performant than the constructors


- the hashCode of Integer is the int value
- the decode method accepts decimal, hex and oct formats. a classical implementation

```
    public static Integer decode(String nm) throws NumberFormatException {
        int radix = 10;
        int index = 0;
        boolean negative = false;
        Integer result;

        if (nm.length() == 0)
            throw new NumberFormatException("Zero length string");
        char firstChar = nm.charAt(0);
        // Handle sign, if present
        if (firstChar == '-') {
            negative = true;
            index++;
        } else if (firstChar == '+')
            index++;

        // Handle radix specifier, if present
        if (nm.startsWith("0x", index) || nm.startsWith("0X", index)) {
            index += 2;
            radix = 16;
        }
        else if (nm.startsWith("#", index)) {
            index ++;
            radix = 16;
        }
        else if (nm.startsWith("0", index) && nm.length() > 1 + index) {
            index ++;
            radix = 8;
        }

        if (nm.startsWith("-", index) || nm.startsWith("+", index))
            throw new NumberFormatException("Sign character in wrong position");

        try {
            result = Integer.valueOf(nm.substring(index), radix);
            result = negative ? Integer.valueOf(-result.intValue()) : result;
        } catch (NumberFormatException e) {
            // If number is Integer.MIN_VALUE, we'll end up here. The next line
            // handles this case, and causes any genuine format error to be
            // rethrown.
            String constant = negative ? ("-" + nm.substring(index))
                                       : nm.substring(index);
            result = Integer.valueOf(constant, radix);
        }
        return result;
    }

```

- more magical bit manipulation code

```
i & -i; //the value of number with only one 1 at the lowest postion of 1 in i

(i << distance) | (i >>> -distance); //rotate left distance bits

(i >>> distance) | (i << -distance); //rotate right distance bits

```

> the analysis of the bit manipulation algorithms here http://blog.csdn.net/oanqoanq/article/details/4083086

