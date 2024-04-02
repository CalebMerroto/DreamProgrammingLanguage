# Dream Programming Language Design

## Concepts
Concepts in ScriptForge define syntactical contracts without enforcing specific semantics. They are used to specify the required operations for types, and can be used interchangably with types.

### Example Concepts

```code
// the "- a" after the concept names refers to the example item that satisfies the concept
// (not an actual instance, just a demonstrator)
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

### Example Class
```code
Class example
	example() //default constructor
	example(a, int b, c = thing)
	
	~example() //destructor declarations work the same as constructor declarations
	
	someMehtod() //a method that returns a variable of any type, or no return value at all
	
	eq someMethod2() // a method that specifically returns something that satisfies eq
	
	infix bool ==(example e) //operator declaration
	
	[int] data //a list of ints 
	[] moreData //a type-independant list
	
	-len-   // creates a calculated field named len. used like accessing a field, but behind the scenes call the len() function. this is only an option for functions without parameters
	int -itm- // creates a calculated field of type int
	
	infix op() // allows the class to be called as an infix operator
	op() // allows the class to be called like a function 
```

### Using Statements: 
(can be declared globally, in namespaces, and in classes)
```code
	using enum // enum values no longer need to explicitly specify if they are from this class 
	using someFunc = Func // alias for someFunc
	using someNamespace // includes all names from someNamespace
```
### Pattern Matching:
```code
	someFunc(a, b, c)
	| 1, 2, 3 > // code to execute in this input scenario
	| [a], b, _ > // a is a list of any type, b can be any type, and c is blank
```

### Function Fragments:
```code
	frag someFragment(a, int b)
		for each printable c in a
			for each i between 0 - b
				{{one}} //fragment attachment poing "one"
		return c
	
	
	someFunc = someFragment>one()
		
		
	//equivilent to writing:
	someFunc(a, int b)
		for each printable c in a
			for each i between 0 - b
				c:i
				out << c
		return c
```
### keywords:
	**await:** while you do not need to declare functions async, you do need to specify when awaiting asynchronous results
	**comp:** specifies a compile-time requirement (so if you don't need run-time dynamic typing you can opt out of it). 
		that said, the compiler will check your code, and if it doesn't make use of run-time type checking it will 
		still make these optimizations. Therefore this feature mostly exists as a means to make it throw an error for 
		run-time type deduction, when you explicity don't want to use that.
	**const:** specifies a constant value
	**infix:** specifies a function with infix notation
	**op:** used for bracket-style operators like (),{},[], and <>, so that they are not confused with container types
