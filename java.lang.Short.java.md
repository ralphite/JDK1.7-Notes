
- nothing special
- like Byte and Character, there is a valueOf method which caches all Short objects with value from -128 to 127

```
    private static class ShortCache {
        private ShortCache(){}

        static final Short cache[] = new Short[-(-128) + 127 + 1];

        static {
            for(int i = 0; i < cache.length; i++)
                cache[i] = new Short((short)(i - 128));
        }
    }

    /**
     * Returns a {@code Short} instance representing the specified
     * {@code short} value.
     * If a new {@code Short} instance is not required, this method
     * should generally be used in preference to the constructor
     * {@link #Short(short)}, as this method is likely to yield
     * significantly better space and time performance by caching
     * frequently requested values.
     *
     * This method will always cache values in the range -128 to 127,
     * inclusive, and may cache other values outside of this range.
     *
     * @param  s a short value.
     * @return a {@code Short} instance representing {@code s}.
     * @since  1.5
     */
    public static Short valueOf(short s) {
        final int offset = 128;
        int sAsInt = s;
        if (sAsInt >= -128 && sAsInt <= 127) { // must cache
            return ShortCache.cache[sAsInt + offset];
        }
        return new Short(s);
    }
    
```

>><a>Note the difference b/t the implementation and javadoc here. the implementation only caches the *must cache* values which range from -128 to 127 but javadoc says it may cache other values outside of this range. but how?</a>

- like Character, Short also has a reverseBytes method which uses several bit manipulations
