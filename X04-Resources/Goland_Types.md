-------------------
boolean, numeric and string are predeclared types. 
composite types - array, struct, pointer, function, slice, map, channel and interface are 
constructed using type literals.
Other types are introduced using type declarations.

type declarations are of two types
* alias declarations
* type definitons

alias declarations: It just binds an identifier to the given type. It is an alias. 
ex:
type (
  nodeList = []Node
  Bint = int 
)


type definitions: It creates a new, distinct type with the same underlying type and binds 
an identifier (name) to it. 
ex:
type (
  Point struct { x, y float64}
  Bint int 
)
A defined type does not inherit any methods bound to the given type, except in the case 
of interface 
```
type Mutex struct {...}
func (m *Mutex) Lock() {...}
func (m *Mutext) Unlock() {...} 

type NewMutex Mutex -- has the same composition as Mutex but its method set is empty.
```

Predeclared types, defined types and type parameters are called named types. 
Am alias denotes a named type if the type given in the alias declaration is a named type.

type literals are unnamed types. 

-----------------------------------
Underlying type

Each type T has an underlying type. 
* If T is boolean, numeric, string, type literals then underlying type is T
ex: 
  underlying type of int is int, boolean is boolean ...
  underlying type of map[string]int is map[string]int
  underlying type of [3]int {} is [3]int {}

* Otherwise T's underlying type is the underlying type of the type to which T refers to 
in its declaration.
ex:
  type A1 string --> underlying type of A is string
  type A2 = A1 --> underlying type of A2 is underlying type of A1 which is string
  
  type B1 string  --> underlying type of B1 is string
  type B2 B1  --> underlying type of B2 is underlying type of B1 which is string 

  However
  type T1 string  --> underlying type of T1 is string
  type T3 []T1 --> underlying type of T3 is underlying type of []T1 which is []T1 itself. 
since it is a type literal
  type T4 T3 --> underlying type of T4 is underlying type of T3 which is []T1
  
  similarly
  type S string
  type T map[S]float64
  underlying type of T is map[S]float64 not map[string]float64


Type identity
---------------
A named type (predeclared, defined types) are always different to other types

ex:
  int is different to string
  int32 is different to int64

  type A0 string
  type B1 A0
  B1 and A0 are different because they are new types created by type definitions, even 
though the underlying types are the same.

Otherwise two types are identical if they are structurally equivalent. Meaning they need 
to have the same literal structure 
and corresponding components need to have identical types

ex:
```
  []int is identical to []int 
  [3]string is identical to [3]string 
  struct {a, b *string} is identical to struct {a, b *string}
  func (x int, y float64) []string  is identical to func (int, float64) []string 
```

So bottom line is two types are identical if they are the same named type (predeclared, 
defined) or they are structurally identical 

 Assignment
 ----------
 A variable x of type T1 can be assigned to variable of type T2 if
  * both types are identical i.e both T1 and T2 are the same named type or they are 
structurally identical
  * both underlying types are identical and either one of T1 or T2 is not a named type 
  * x implements interface T2 
  * x is nil and T2 is either pointer,function,slice,map,channel or interface
  * T1 and T2 are channel types with identical element types, T1 is a bidirectional 
channel, and at least one of T1 or T2 is not a named type.
  * x is an untyped constant representable by a value of T
  
ex:
  var i int
  var x int = 20
  i = x   // valid

  type aInt int 

  var i int 
  var x aInt = 20
  i = x   // invalid  (aInt and int are both named types, so not identical, even though 
underlying types may be the same)

  type myMap map[string]int 

  m = make(map[string]int)
  var newMap myMap
  newMap = m    // valid (myMap is a named type, but m is a composite type and underlying 
types  are structurally identical )
   

Representability
----------------
A constant x is representable by a value of T if x is in the set of values determined by T

ex:

'a'                 byte        97 is in the set of byte values
97                  rune        rune is an alias for int32, and 97 is in the set of 
32-bit integers
"foo"               string      "foo" is in the set of string values
1024                int16       1024 is in the set of 16-bit integers
42.0                byte        42 is in the set of unsigned 8-bit integers
1e10                uint64      10000000000 is in the set of unsigned 64-bit integers
2.718281828459045   float32     2.718281828459045 rounds to 2.7182817 which is in the set 
of float32 values
-1e-1000            float64     -1e-1000 rounds to IEEE -0.0 which is further simplified 
to 0.0
0i                  int         0 is an integer value
(42 + 0i)           float32     42.0 (with zero imaginary part) is in the set of float32 
values


The following are not representable

0                   bool        0 is not in the set of boolean values
'a'                 string      'a' is a rune, it is not in the set of string values
1024                byte        1024 is not in the set of unsigned 8-bit integers
-1                  uint16      -1 is not in the set of unsigned 16-bit integers
1.1                 int         1.1 is not an integer value
42i                 float32     (0 + 42i) is not in the set of float32 values
1e1000              float64     1e1000 overflows to IEEE +Inf after rounding


Conversion
-----------
Explicit conversion is of the form T(v)

Constants
* A constant value v can be converted to type T if v is representable by a value of T

Non-constants
A value v can be converted to T using T(v) iff:

* v is assignable to T
* v's type and T are both integer or floating point types.
* v's type and T are both complex types.
* v is an integer or a slice of bytes or runes and T is a string type.
* v is a string and T is a slice of bytes or runes.
* v is a slice, T is an array or a pointer to an array, and the slice and array types 
have identical element types
* Ignoring struct tags, v's type and T have identical underlying types
* Ignoring struct tags, v's type and T are pointer types that are not named types, but 
their base types have identical underlying types

ex:

Struct tags are ignored when comparing struct types for identity for the purpose of 
conversion:
```
type Person struct {
	Name    string
	Address *struct {
		Street string
		City   string
	}
}

var data *struct {
	Name    string `json:"name"`
	Address *struct {
		Street string `json:"street"`
		City   string `json:"city"`
	} `json:"address"`
}

var person = (*Person)(data)  // ignoring tags, the underlying types are identical
```

Rules:
Read Articles/golang/Value Conversion, Assignment and Comparison Rules in Go
and Articles/golang/golang_types.txt
