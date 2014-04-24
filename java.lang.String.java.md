
- a final char array is used for internal character storage
- hashCode of the string is also cached so that hashCode of this String is only calc'ed once
- the default constructor is exposed which creates a char array of size 0

```
    this.value = new char[0];
```

> this constructor is not recommended since Strings are immutable

> An interesting way to get Integer.MAX_VALUE `-1 >>> 1`

- there are a few constructors building a string from char or byte arrays

`for(Method method : Class.class.getDeclaredMethods()) {System.out.println(method);}`

- String#isEmpty()
- String#equals(Object o)
    - o has to be instanceof String and has same values in char array
- String#contentEquals(StringBuffer sb)
- String#contentEquals(CharSequence cs)
- **String#equalsIgnoreCase(String s)**
- **String#startsWith** can have an optional param to specify the offset

> startsWith(s, offset) and endsWith(s) are very useful for simple pattern matching in algorithmic interview questions

- String#hashCode() is calc'ed as `s[0]*31^(n-1) + s[1]*31^(n-2) + ... + s[n-1]`

```
    public int hashCode() {
        int h = hash;
        if (h == 0 && value.length > 0) {
            char val[] = value;

            for (int i = 0; i < value.length; i++) {
                h = 31 * h + val[i];
            }
            hash = h;
        }
        return h;
    }
```

> the many `String#indexOf` and `String#lastIndexOf` methods can also accept a 2nd param `fromIndex`

..

> Note the usage of for and while below
> ```
>    /* Look for first character. */
>    if (source[i] != first) {
>        while (++i <= max && source[i] != first);
>    }
>    //...        
>    for (int k = targetOffset + 1; j < end && source[j]
>        == target[k]; j++, k++);
>```

..

> also note the labeled continue at line 1830


- String#substring's argument may be the length of the string, and in this case the method will return an empty string.

> note the optimization at line 1877
>```
>return (beginIndex == 0) ? this : new String(value, beginIndex, subLen);
>```

####find and replace
the following methods uses `java.util.regex.Pattern` for subsequence finding and replacing

```
    public boolean matches(String regex);
    public boolean contains(CharSequence s);
    public String replaceFirst(String regex, String replacement);
    public String replaceAll(String regex, String replacement);
    public String replace(CharSequence target, CharSequence replacement);
```

- `public String[] split(String regex);`
- `public String[] split(String regex, int limit);`

> Note line 2273 which tests if the first char of a string is within a set of chars
> ```
>".$|()[{^?*+\\".indexOf(ch = regex.charAt(0)) == -1)
>```

..

> Note the usage of labelled breaks in `String#toUpperCase` and `String#toLowerCase`

- `public native String intern();`

> this native method will make sure the String returned is in the **string pool**. consider the following code

```
public class Solution {
    public static void main(final String... args) {
        String s1 = "aaa";
        String s2 = "aaa";
        String s3 = new String(s1);
        System.out.println(s1 == s2);
        System.out.println(System.identityHashCode(s1));
        System.out.println(System.identityHashCode(s2));
        System.out.println(System.identityHashCode(s3));
        System.out.println(s1 == s3);
        s3 = s3.intern();
        System.out.println(s1 == s3);
        System.out.println(System.identityHashCode(s3));
    }
}

```

> Note the complex static initializer to get the HASHING_SEED 
> for explanation see http://en.wikipedia.org/wiki/MurmurHash
