
##### Effective type of Object

Effective type of an object is the type given when the object is declared. 
ex:
int x;  effective type is int. 

Memory returned from `malloc` has no effective type. For example:

```c
int *x = malloc(sizeof(int));
```

Assuming an `int` is 4 bytes in size, `x` now points to 4 bytes of memory with no 
effective type. This memory gets an effective type when assigned to:

```c
*x = 123;
```

Now those bytes have an effective type of `int`.


##### Pointer Conversion rules
------------------------
* It is safe to convert a pointer from any type T * to any type U * if alignof(U) <= 
alignof(T)
*  for structs, address of a struct is the address of its first member. so alignment 
requirements of a struct are the same as the alignment requirements of a struct’s first 
member

**More formal definition**

A pointer to an object or incomplete type may be converted to a pointer to a different 
object or incomplete type. If the resulting pointer is not correctly aligned for the 
pointed-to type, the behavior is undefined. Otherwise, when converted back again, the 
result shall compare equal to the original pointer. When a pointer to an object is 
converted to a pointer to a character type, the result points to the lowest addressed 
byte of the object.

It is safe to
```
Cast from any object-pointer type to void *
Cast from any object-pointer type to char *, signed char * or unsigned char *
Cast among pointers to types differing only in signedness and / or type qualifiers.
Cast from a pointer to a structure type to a pointer to the type of the structure's first 
member
Cast from a pointer to a union type to a pointer to the type of any member of the union
Cast from a pointer to an array type to a pointer to the array's element type, and vice 
versa
Cast directly from a type T * to a type U * if one can safely convert from T * to U * via 
one or more safe intermediate conversions.
Cast between any two function-pointer types
given a pointer value p obtained via a series of pointer conversions that do not any of 
which invoke undefined behavior, whether or not their safety was provable in advance, 
convert p back to the original type or to any of the intermediate types.
Note well that the safety of a pointer conversion is only about the conversion itself. It 
is not necessarily safe to dereference the pointer resulting from a safe (in the sense 
we're discussing) conversion, or, for function pointers, to call the pointed-to function 
via the converted pointer.

```

**Alignment requirements for structs**

6.7.2.1/13 A pointer to a structure object, suitably converted, points to its initial 
member (or if that member is a bit-field, then to the unit in which it resides), and vice 
versa. There may be unnamed padding within a structure object, but not at its beginning.

Meditate on this for a while. Paraphrased, this all means that the alignment requirements 
of a struct are the same as the alignment requirements of a struct’s first member

**how does malloc understand alignment?**

Alignment requirements are recursive: The alignment of any struct is simply the largest 
alignment of any of its members, and this is understood recursively.

For example, and assuming that each fundamental type's alignment equals its size (this is 
not always true in general), the
struct X { int; char; double; } 
has the alignment of double, and it will be padded to be a multiple of the size of double 
(e.g. 4 (int), 1 (char), 3 (padding), 8 (double)). 
The 
struct Y { int; X; float; } 
has the alignment of X, which is the largest and equal to the alignment of double, and Y 
is laid out accordingly: 4 (int), 4 (padding), 16 (X), 4 (float), 4 (padding).

(All numbers are just examples and could differ on your machine.)

Therefore, by breaking it down to the fundamental types, we only need to know a handful 
of fundamental alignments, and among those there is a well-known largest. C++ even 
defines a type max_align_t whose alignment is that largest alignment.

All malloc() needs to do is to pick an address that's a multiple of that value.

##### Strict aliasing
---------------
strict aliasing enforces the rule that no incompatible types will access the same memory 
location. This will be used by the compiler for optimization. for ex:

```
	void f(float *x, int * y) {
		*x = 1;
		*y = 1;
		return *x;
	}
```

Here the compiler knows that x and y cannot alias at the same location. so it can 
optimize the code to return 1 directly without accessing the memory. 
But if the function had both `int *` arguments,  x and y could point at the same memory 
location, the compiler has to fetch the code from x and return it. even though it could 
have just returned 1. 

**Read Articles/Pointer_Aliasing_0....html -- Part 3 The strict aliasing rule first**

An object shall have its stored value accessed only by an lvalue expression that has one 
of the following types:
```
a type compatible with the effective type of the object,
a qualified version of a type compatible with the effective type of the object,
a type that is the signed or unsigned type corresponding to the effective type of the 
object,
a type that is the signed or unsigned type corresponding to a qualified version of the 
effective type of the object,
a type that is an aggregate or union type that includes one of the aforementioned types 
among its members (including, recursively, a member of a sub-aggregate or contained 
union), or
a character type.
```
"keyword is access. "
If you don't access but just convert, you don't break the strict aliasing rule.
But you may break the alignment rule.


----------------------------


