
>```
> 1/0; // java.lang.ArithmeticException: / by zero
> 1./0; //Infinity which is a primitive double value
> -1./0; //-Infinity
> 0/0; // java.lang.ArithmeticException: / by zero
> 0./0; //NaN which is also a primitive double
> -0./0; //NaN which is also a primitive double
>```

- hashCode()
    - first converts to long then exclusive or of the
    lower half and upper half
    
- equals(Object other)
    - both must be Double
    - doubleToLongBits must be the same
    
    
- **doubleToLongBits** uses the native doubleToRawLongBits method
- public static native double **longBitsToDouble**(long bits);
- the static compare method uses doubleToLongBits method to convert
first before comparing in some cases
