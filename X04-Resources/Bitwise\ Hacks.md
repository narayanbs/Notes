----------------------
Operators

&   |   ^   ~   >>   <<

Basic Operations

x & 1  ---> x
x | 1 ---> 1
x ^ 1 ---> ~x
~x  ---> toggle everything
x - 1 ---> make the right most 1 bit 0 and everything that follows as 1
x + 1 ---> make the right most 0 bit 1 and everything that follows as 0. 
-x ---> toggle everything before you reach the last 1 bit. 

Examples:
```bash
x = 22      ---> 00010110
-x = -22    ---> 11101010
x - 1 = 21  ---> 00010001
x + 1 = 23  ---> 00010111
~x          ---> 11101001
```

check for even and odd
```bash
x & 1 == 0 // even
x & 1 != 0 // odd
```

Test if n-th bit is set
```bash
if (x & (1<<n)) {
  n-th bit is set
}
else {
  n-th bit is not set
}
```

set the n-th bit
```bash
y = x | (1<<n)
```

unset the n-th bit
```bash
y = x & ~(1<<n)
```

Toggle the n-th bit
```bash
y = x ^ (1<<n)
```

Turn off the rightmost 1-bit
```bash
y = x & (x-1)
```

Isolate the rightmost 1-bit
```bash
y = x & (-x)
```

Right propogate the rightmost 1-bit
```bash
y = x | (x-1)
```

Isolate the rightmost 0-bit
```bash
y = ~x & (x+1)
```

Turn on the rightmost 0-bit
```bash
y = x | (x+1)
```

Compute sign of an integer
```bash
int v;      // we want to find the sign of v
int sign;   // the result goes here 

// CHAR_BIT is the number of bits per byte (normally 8).
sign = -(v < 0);  // if v < 0 then -1, else 0. 
// or, to avoid branching on CPUs with flag registers (IA32): we do the following
// Note: 
// right shifting signed negative values is undefined in C,so we cast to (unsigned int) 
and shift.
// the final cast back to int is required because, if we negate a unsigned value, we get 
UINT_MAX or 0.
// and this causes overflow
// casting the result to int before negating correctly gives the result
sign = -(int)((unsigned int)((int)v) >> (sizeof(int) * CHAR_BIT - 1));
// or, for one less instruction (but not portable):
sign = v >> (sizeof(int) * CHAR_BIT - 1);
```

Detect if two integers have opposite signs
```bash
bool f = ((x ^ y) < 0);
```

Compute the absolute value of an integer without branching
( how this works is by using -x = ~x + 1, the following  two versions try to do ~x + 1 )

```bash
int v;           // we want to find the absolute value of v
unsigned int r;  // the result goes here 
int const mask = v >> sizeof(int) * CHAR_BIT - 1; // the mask becomes -1 for -ve and just 
0 for positive

r = (v + mask) ^ mask; 

Patented variation:

r = (v ^ mask) - mask;
```

Compute the minimum or maximum of two integers
```bash
int x;  // we want to find the minimum of x and y
int y;   
int r;  // the result goes here 

r = y ^ ((x ^ y) & -(x < y)); // min(x, y)

r = x ^ ((x ^ y) & -(x < y)); // max(x, y)
```

Determining if an integer is a power of 2
```bash
unsigned int v; // we want to see if v is a power of 2
bool f;         // the result goes here 

f = (v & (v - 1)) == 0;

Note that 0 is incorrectly considered a power of 2 here. To remedy this, use:

f = v && !(v & (v - 1));
```

Conditionally set or clear bits without branching
```bash

```