**Does casting to char* and then casting back to original type break strict aliasing?**

For example, I cast a pointer to an `int` to a pointer to `char`:

```c
int originalVar = 1;
char *arr = (char *)&originalVar;
```

Then I cast it back (maybe I pass `arr` to another function):

```c
int *pOriginal = (int *)arr;
```

Does it break the rules? Or any undefined behaviors here?

Actually my doubts are about understanding the "effective type" in C standard

Does the object pointed by `arr` always regard `int` as its effective type??
(Even if `arr` is passed to another function?)

**Ans**

That works and is well defined because the alignment of the original pointer will match the int.

Only issue casing a char* to an int* can be alignment requirements. Certain architectures require an int to be aligned on a 4-byte boundary (i.e. the last two binary digits of the pointer are 0). A char* generally does not have that limitation.

However, since it started as an int*, and int* -> char* is never an issue, this will not cause any issue.


**Does casting to a char pointer to increment a pointer by a certain amount and then accessing as a different type violate strict aliasing**

For example, you might want to align a `void *` that is aligned to 4-byte boundary to 16-byte boundary.

```c
int *align16(void *p) {
    return (int *)((char *)p + 16 - (uintptr_t)p % 16);
}
```

Normally, accessing an `int *` casted from a `char *` violates strict aliasing rules and invokes undefined behaviour, while the opposite is safe.

Is it still undefined behaviour in cases such as above?

---

A side question. The optimised compiler output of `align16` can be decompiled as follows.

```c
int *align16(void *p) {
    return (int *)((uintptr_t)p + 16 & -16);
}
```

How does the standard deal with such case, accessing a pointer modified while casted to a `uintptr_t`?

**Ans**

Strict aliasing is about accessing the same memory by dereferencing pointers to different types. Here, the char * expression is never dereferenced; in fact nothing is dereferenced at all. So strict aliasing is irrelevant to the align16 function itself, though conceivably it could be relevant to whatever the caller is doing. 

> Does casting to a char pointer to increment a pointer by a certain amount and then accessing as a different type violate strict aliasing?

Not inherently so.

> Normally, accessing an `int *` casted from a `char *` violates strict aliasing rules

Not necessarily. Strict aliasing is about the (effective) type of the pointed-to object. It is quite possible for the object to which a `char *` points to be an `int`, or compatible with `int`, or to be _assigned_ effective type `int` as a consequence of the (write) access. In such cases, casting to `int *` and dereferencing the result is perfectly valid.

There are, yes, lots of cases in which casting a `char *` to an `int *` and then dereferencing the result would constitute a strict-aliasing violation, but it is not specifically because of the involvement of, or the casting to or from, type `char *`.

The above applies regardless of how the particular `char *` value was obtained, so in your particular example case, too. If the result of your pointer computation is a valid pointer, and the object to which it points is genuinely an (effective) `int` or is compatible with `int` in one of the specific ways documented in section 6.5 of the language spec, then reading the pointed-to value via the pointer is fine. Otherwise, it is a strict-aliasing violation.

Attempting to dereference a pointer value that is not correctly aligned for its type is a potential issue in general with pointer manipulation, but the strict aliasing rule is stronger than and effectively inclusive of pointer alignment considerations. If you have an access that satisfies the strict aliasing rule then the pointer involved must be satisfactorily aligned for its type. The reverse is not necessarily true.

---

Do note, however, that although on many platforms, your `align16()` will indeed attempt to perform a read of a 16-byte-aligned object, the C language specifications do not require that to be so. Pointer-to-integer and integer-to-pointer conversions are explicitly allowed, but their results are _implementation defined_. It is not necessarily the case that value on the integer side of such a conversion reports on or controls the alignment of the pointer on the other side.

> How does the standard deal with such case, accessing a pointer modified while casted to a uintptr_t?

See above. Pointer-to-integer and integer-to-pointer conversions have implementation-defined effect as far as the language spec is concerned. However, on most implementations you're likely to meet, your two versions of `align16()` will have equivalent behavior.