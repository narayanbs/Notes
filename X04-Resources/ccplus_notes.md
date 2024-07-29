#### C++ initialization 

###### Default, value and zero-initialization
---

Default Initialization --> If T is a class, then default constructor is called to provide 
initialization, of the new object; if constructor is not provided or if no initialization 
is done, then we have indeterminate values. For array each element is default initialized.

Value initialization --> Prevents indeterminate values, If T is a class, if it has a 
user-provided/deleted constructor, then it is default-initialized, but if has a default 
constructor (not user provided) then it is zero initialized. 
if it’s an array, each element is value-initialized; for other types, the object is 
zero-initialized. 

zero-initialization –> Applied to static and thread-local variables before any other 
initialization. If T is scalar (arithmetic, pointer, enum), it is initialized to 0 ; if 
it’s a class type, all base classes and data members are zero-initialized; if it’s an 
array, each element is zero-initialized. Both Global (both static and exported) variables 
are zero-initialized

Note: deleted constructor ==> if copy constructor is defined but nothing else.

Ex:
```bash
T global;    //zero-initialization, then
             // default-initialization
void foo() {
  T i;       //default-initialization
  T j{};     //value-initialization (C++11)
  T k = T(); //value-initialization
  T l = T{}; //value-initialization (C++11)
  T m();     //function-declaration
  new T;     //default-initialization
  new T();   //value-initialization
  new T{};   //value-initialization (C++11)
}

//t is value-initialized
struct A { 
	T t; 
	A() : t() 
	{} 
};

//t is value-initialized (C++11)
struct B { 
	T t; 
	B() : t{} 
	{} 
}; 
//t is default-initialized
struct C { 
	T t; 
	C()   
	{} 
};

```

#### C++ Inheritance
----
The Derived class can be thought of as one big structure with the parent fields stacked 
on its fields. The parent fields need to be initialized and the base constructor called, 
before the derived class fields initialization and the constructor call. 

A static field is created per class and reused by all the objects. Hence it needs to be 
created once and must be initialized before the program starts (main) and destroyed when 
it ends. The namespace includes the class name then scope resolution operator (::), then 
the variable name. They can be stored in the data segment. It is zero initialized by the 
compiler or (const initialized).

Note:
This is different from java, because java required class loading, where as c++ are built 
into a monolith executable). 
Java needs classloading by the jvm, hence the base parent initialization (especially 
static happens during loading

Note:
Virtual base classes are used in virtual inheritance in a way of preventing multiple 
“instances” of a given class  appearing in an inheritance hierarchy when using 
multiple inheritances.

Consider the situation where we have one class A .This class is A is inherited by two 
other classes B and C. Both these class are inherited into another in a new class D as 
shown below

```bash
         
      - A -
    /	    \
   /	     \
  B 	      C
   \	     /
    ---	D ---
    
 class A {
public:
    void show()
    {
        cout << "Hello form A \n";
    }
};
  
class B : public A {
};
  
class C : public A {
};
  
class D : public B, public C {
};   
  
 int main()
{
    D object;
    object.show(); // error
}  
    
solution:

class B : virtual public A 
{
};


class C : public virtual A
{
};    

```

 
When a derived class object is created using constructors, it is created in the following 
order:

Virtual base classes are initialized, in the order they appear in the base list.
Non-virtual base classes are initialized, in declaration order.
Class members are initialized in declaration order (regardless of their order in the 
initialization list).
The body of the constructor is executed.

The following example demonstrates this:
```bash

#include <iostream>
using namespace std;
struct V {
  V() { cout << "V()" << endl; }
};
struct V2 {
  V2() { cout << "V2()" << endl; }
};
struct A {
  A() { cout << "A()" << endl; }
};
struct B : virtual V {
  B() { cout << "B()" << endl; }
};
struct C : B, virtual V2 {
  C() { cout << "C()" << endl; }
};
struct D : C, virtual V {
  A obj_A;
  D() { cout << "D()" << endl; }
};

int main() {
  D c;
}

The following is the output of the above example:
V()
V2()
B()
C()
A()
D()
```


Note:
If a class has virtual methods, then the structure will have a pointer to a vtable that 
has pointers that point to the
method implementations. If a subclass overrides the virtual method, then its vtable will 
now have a pointer that points to
its implementation. If a subclass inherits the method, then its vtable will have a 
pointer that points to the parents' 
implementation.


#### Other Points

##### Point 1
Any valid pointer to void can be converted to intptr_t or uintptr_t and back with no 
change in value.  The C Standard guarantees that a pointer to void may be converted to or 
from a pointer to any object type and back again and that the result must compare equal 
to the original pointer. Consequently, converting directly from a char * pointer to a 
uintptr_t, as in this compliant solution, is allowed on implementations that support the 
uintptr_t type.
```bash
#include <stdint.h>
  
void f(void) {
  char *ptr;
  /* ... */
  uintptr_t number = (uintptr_t)ptr; 
  /* ... */
}
```

#### Exceptions

**INT36-C-EX1:** The integer value 0 can be converted to a pointer; it becomes the null 
pointer.
**INT36-C-EX2:** Any valid pointer to `void` can be converted 
to `intptr_t` or `uintptr_t` or their underlying types and back again with no change 
in value. Use of underlying types instead of `intptr_t` or `uintptr_t` is 
discouraged, however, because it limits portability.

```
#include <assert.h>
#include <stdint.h>
  
void h(void) {
  intptr_t i = (intptr_t)(void *)&i;
  uintptr_t j = (uintptr_t)(void *)&j;
  
  void *ip = (void *)i;
  void *jp = (void *)j;
  
  assert(ip == &i);
  assert(jp == &j);
}
```

##### Point 2
The following is a variadic template function..  Let's understand how it works
```bash
template <typename... T> void print(const T &...t) {
  (void)std::initializer_list<int>{(std::cout << t << "", 0)...};
  std::cout << "\n";
}
```

`typename... T` indicates that the function will have many types as generic parameters.

const T&... t indicates that the function takes a number of references of instances of  
types listed as generic parameters

`std::initializer_list<int>{}` takes a list of items and initializes them. so the code 
above 
`(std::cout << t <<"", 0)...` expands as `{(std::cout << t << "", 0), (std::cout << t << 
"", 0), (std::cout << t << "", 0), (std::cout << t << "", 0)}`  for each parameter passed 
in the function. 
`(std::cout << t << "", 0)` basically prints t and returns 0  (comma operator). 

##### Point 3
The following function, parses through an object and checks if a field is a pointer and 
adds
it to a vector. 
```bash
std::vector<Traceable *> getPointers(Traceable *object) {
  auto p = (uint8_t *)object;
  auto end = (p + object->getHeader()->size);
  std::vector<Traceable *> result;
  while (p < end) {
    auto address = (Traceable *)*(uintptr_t *)p;
    if (traceInfo.count(address) != 0) {
      result.emplace_back(address);
    }
    p++;
  }
  return result;
}
```
`auto address = (Traceable *)*(uintptr_t *)p;` p is cast to an integer type that can hold 
an address, it is dereferenced to get the address and then cast to `Traceable *` 

