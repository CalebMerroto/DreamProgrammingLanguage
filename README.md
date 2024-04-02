# Dream Programming Language Design

## Concepts
Concepts in ScriptForge define syntactical contracts without enforcing specific semantics. They are used to specify the required operations for types, and can be used interchangably with types.

### Example Concepts

```code
// the "- a" after the concept names refers to the example item that satisfies the concept (not an actual instance, just a demonstrator)
Concept eq - a
    a == b - bool
    a != b - bool

Concept ord - a
    eq
    a < b - bool
    a > b - bool
    a <= b - bool
    a >= b - bool

Concept printable - a
    out << a - any  // Semantically, an output stream

Concept readable - a
    in >> a  // Syntactically any type, semantically an input stream

Concept list - a
    a[int]  // Access an item in a
    a:b  // Append b to a
    b:a  // Prepend b to a
    a:b[int]  // Insert b into a at a specific index
    a::  // Access the last element of a
    ::a  // Access the first element of a

Concept someInterface - a
    a.data  // Has a field called data (any type)
    a.someMethod(b, [], string)  // Method with 3 parameters
    a.otherMethod("b", "c") - bool  // Method returning bool
```
