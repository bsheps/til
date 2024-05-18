---
title: "Java Casting and Type Conversions"
date: 2024-05-15T21:21:31-05:00
draft: false
---

Today I learned about how Java casting and type conversions work. Automatic casting and conversion is probably the most obvious.

### int to decimal

``` java
int i = 42;
double d = i;
System.out.print(d); // prints: 42.0
```

This is known as widening and works because 2 rules are followed:
 1. Both types are [compatible](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.1.2)
        _In this case both `int` and `double` are primative types._
 2. The conversion is from a smaller to larger type 
        _In this case `int` is a 32 bits and `double` is 64 bits so the int easily fits into the double._

### decimal to int

Less obvious is what happens when we convert a larger type to a smaller type:

``` java
double speedOfLight = 11802854131.2; // speed of light (inches per second)
int i = (int) speedOfLight;
System.out.print(i); // prints: 2147483647
```

How did we get 2147483647? This anonaly/effect is what's known as [narrowing](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.1.3). Walking through the steps:

First: Round toward zero using [IEEE 754](https://en.wikipedia.org/wiki/IEEE_754#Directed_roundings) which is just a fancy way of saying we drop the decimal values.

So 11802854131.2 becomes 11802854131.

Second: Since 11802854131 is larger than the largest int value, we set it equal to the largest int value.

So 11802854131 becomes 2147483647

_Note: 2147483647 is the largest int value because int is a signed 32 bit value. Explanation: 2<sup>32</sup> = 4294967296. "Signed" means we represent both positive and negative numbers. So 4294967296 / 2 = 2147483648 (aka there are 2147483648 positive values and 2147483648 negative values). Since 0 is part of the positive values, we start counting at 0 so 0,1,2,3,... do this 2147483648 times and the max value we get is 2147483647 because we needed to account for zero._

Tada! Now it make sense how we got 2147483647, but what if we were casting a double to a byte?

### decimal to byte

``` java
double OhareToMiami = 1202.56; // straight line distance between Chicago O'hare and Miami airports.
byte b = (byte) OhareToMiami;
System.out.print(b); // prints: -78
```

Yes, -78. How?

First: we follow the 2 steps from [above](#decimal-to-int) where we drop the decimal place then fit the value into an int. In this case 1202 fits into the int data type.

Second: This part is tricky because we're going to work in binary. In Java, a [byte](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html) is an 8-bit signed type (meaning positive, zero and negative numbers are represented), we'll need to approach it as the two's complement. 

I'll use the [one's complement algorithm](https://en.wikipedia.org/wiki/Two%27s_complement#From_the_ones'_complement) to show the outcome below.
``` sh
# the int type representation for 1202 in binary is:
 00000000 00000000 00000100 10110010
# Note: there are 32 bits because int is 32 bit type

# Since byte is 8 bits, we narrow this to the right most 8 bits

# so everything from...    \/ until \/
 00000000 00000000 00000100 10110010

# byte result:
 10110010

# Converting the two's complement

# Check the most significant bit (left most)
#\/
  10110010

# since the left most bit is 1:
*result is negative*

# Step 1: invert (we flip the bits... 1s become 0s and 0s become 1s)
 10110010
#inverted becomes:
 01001101

# this is also know as the one's complement
# to get the two's complement, we add 1 to the one's complement

# Step 2: add 1
 01001101
+       1
---------
 01001110

# converted from binary to decimal
2^6 + 2^3 + 2^2 + 2^1
78

# since result is negative
-78
```

There you have it, 1202.56 becomes -78. It's a little unsettling but at least we understand. Basically, we drop the decimal places. Convert to an int. And take the first 8 bits.