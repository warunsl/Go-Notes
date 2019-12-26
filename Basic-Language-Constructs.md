# Basic-Language-Constructs

#### Basic types
- `bool`
- `string`
- `int`, `int8`, `int16`, `int32`, `int64`
- `uint`, `uint8`, `uint16`, `uint32`, `uint64`, `uintptr`.
- Can't assign `int` to an `int32` or vice-versa. Needs explicit casting.
- `byte` (`uint8`)
- `rune` (`int32`)
- `float32`, `float64`
- `complex64`, `complex128` - Numbers that end with i.

#### Other types
- `Array` - numbered collection of types.
- `Slice` - vector or a list that can grow in size. Mostly used more commonly over `Array`
- `Struct`
- `Pointer`
- `Function`
- `Interface`
- `Map`
- `Channel` - Used for communication between goroutines.

#### Variable declaration
- `var` keyword followed by the name of the variable followed by the type. Ex:    
```
// Single variable declaration followed by assignment.
var name string
name = "Varun"

// Multiple variable declaration.
var a, b, c int // All of these will be initialized to 0.

// Initialization while declaring.
var name string = "Varun"
var a, b, c int = 10, 20, 30

// Type inference by Go.
var a, b, c = 1, false, 2

// Variable declaration can be further simplified with
a, b, c := 1, false, 2
```
- `:=` can only be used within a function. For now, seems like all `:=` does is save us writing `var`.
- Can't be used while declaring variables within a `struct`.

#### Pointers
- Declaring pointers    
```
message := "Hello world"
var msgPtr *string = &message
```

#### User defined type
```
type Salutation string
```
- The above just declares a new type which is a redefinition of the `string` type. Just has a different name.
- In Go, user defined types can have method definitions.
- Using `struct`
```
type Salutation struct {
    name string                    // If we want to put this struct in a package and make it importable from other modules, both name and message need to be capitalized.
    message string
}

// Initializing a struct - 1.
var s = Salutation{"Varun", "Hello"}

// Initializing a struct - 2.
var s = Salutation{message: "Hello", name: "Varun"}

// Initializing a struct - 3.
var s = Salutation{}
s.name = "Varun"
```
- No getters and setters in Go.
- No visibility specifiers in Go. If a type name starts with a capital letter, like in `Salutation`, the type is visible outside the package too. If it starts with a small letter, it is private to the whatever package it is defined in.

#### Constants
- Constants can be defined without a type, it will be inferred.
```
const (
	PI = 3.14
	Language = "Go"
)
```
- Using a block to define a `const` is to avoid using `const` on every line. Same for multiple imports in a file.
- Note: there are no commas between the lines.
- Enums are declared using `iota`. `iota` represents successive untyped integer constants.
```
const (
	A = iota
	B = iota
	C = iota
)

// Same as:
const (
	A = iota // B and C re-use the same type as the previous one.
	B
	C
)
```
