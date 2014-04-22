
- very lengthy, mostly about unicode handling
- like Byte, Character's `ofValue` method also uses pre-cached data, but only for char with value from 0 to 127
- hashCode of a Character is the int value of the char
- codePoint related code is ignored (?what is a code point)
- more interesting methods are
    - `toLowerCase`
    - `toUpperCase`
    - `isUpperCase`
    - `isLowerCase`
    - `isAlphabetic`
    - `isLetter`
    - `isLetterOrDigit`
    - `isDigit`
    - `isSpaceChar`
    - `isWhitespace`
    - `getNumericValue`
    - `digit`
    
> note the following code which swaps the two bytes of the char

```
    public static char reverseBytes(char ch) {
        return (char) (((ch & 0xFF00) >> 8) | (ch << 8));
    }
```

> also note the size of char is 16 in Java, same as short, so it can hold 65536 values at most
