---
title: "Java Casting and Type Conversions"
date: 2024-05-15T21:21:31-05:00
draft: true
---

Today I learned about how Java casting and type conversions work. Automatic casting and conversion is probably the most obvious. For example:

``` java
int i = 42;
double d = i; // d equals 42.0
```

This is known as widening and works because 2 rules are followed:
 1. Both types are [compatible](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.1.2)
        _In this case both `int` and `double` are primative types._
 2. The conversion is from a smaller to larger type 
        _In this case `int` is a 32 bits and `double` is 64 bits so the int easily fits into the double._

Less obvious is what happens when we convert a larger type to a smaller type:

``` java
double d = 463.999

int i = (int) d; // i equals 463

byte b = (byte) d; // b equals -49
```

Yes, -49 as in "negative fourty nine".

This effect is known as [narrowing](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.1.3). Here's algorithm sudo code:

```java
// step 1
if(floating-point number)
    if (number is NaN)
        if(destination is long type) return long = 0;
        else if (destination is int, short, char, byte) return int = 0;

    n = rounded number via IEEE 754
    if(destination is long type AND n fits into long type) return long = n;
    else if (does n fit into int type) return int = n;
    else // n is either too big or too small
        return the largest or smallest value of either long or int
end

// step2
if (destination type is long or int)
    return resulting value from step 1
end


```