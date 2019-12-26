# Loops-Maps-And-Slices

#### Loops

- Go has only one keyword for looping - `for`
- `for` loops have one of the three following forms:
	+ `for` <condition> { <block-of-code> }. This is similar to `while` loops in other languages.
	+ `for` (<init; condition; post>) { <block-of-code> }
	+ `for` <range> { <block-of-code> }
```
for i := 0; i < 10; i++ {
	fmt.Println(i)
}

i := 0
for i < 10 {
	fmt.Println(i)
	i++
}

// Infinite loop.
for {
	// do-something.
}
```
- `break` and `continue` are used as in any other language.
- `range` based looping
```
// Declaring a slice(array).
items []string

// range based looping.
for _, item := range items { // The first variable is the index.
	fmt.Println(item)
}

// If the intention is to only use the index.
 for i := range items {
	...
}
```

#### Maps
- The type used as a key in Go maps need to have equality operation defined.
- `slice` or `map`s themselves don't have an equality operator defined. Hence can't be used as a key to a map.
- Maps are reference types. When you pass a map as a parameter to a function, the original is modified.
- Maps are not thread safe.
```
var prefixMap map[string]string // Declaration.
prefixMap = make(map[string]string) // Allocates space for the map. Is essential.

// Shorthand way of declaring and initializing the map at once.
prefixMap := map[string]string {
	"Bob" : "Mr",
	"Mary" : "Dr",
	"Amy" : "Dr", // the final comma is needed.
}

// Adding values to the map.
prefixMap["Bob"] = "Mr"
prefixMap["Mary"] = "Dr"

// Update values in a map.
prefixMap["Bob"] = "Jr"

// Delete from a map.
delete(prefixMap, "Amy") // preferred.
prefixMap["Amy"] = "", false // deleting with older version of Go

// Checking for existance.
if val, exists := prefixMap["Bob"] exists {
	return val
}

// Default value for a map.
// Here, the return "Hello" serves as a default value for a key that does not exist. Because in that case, the `exists` is false.
if val, exists := prefixMap["Bob"] exists {
	return val
}
return "Hello"
```

#### Slices
- `Array` is collection of a fixed size of a particular type.
- Declaration: `var a [3]int`
- No initialization. They are `0` valued.
- The type of an Array is it's size and underlying type. A 3 element integer array is a different type than a 4 element integer array. 
- In Go, `Array` is not a pointer, it's a value type. When you pass an `Array` as a parameter to a function, the original is not modified.
- `Slice` is an abstraction over an `Array`. It's type is not related to the size of the collection. It's just based on the underlying type.
- Declaration: `var s []int`.
- Initialization: `var s []int = make([]int, 3, 5)`.
	+ The last two parameters in the call to `make` are initial length and total capacity.
- `Slice` is basically a pointer to an `Array` type.
- `Slice` is fixed size. But can be re-allocated with `append`.
	+ `a = append(a, 10)`
- Just like a `map`, if a `Slice` is not initialized using `make`, it's value is `nil`
- Doubling the size of a `Slice`
```
a = append(a, a...)

// Removing an element, say 20.
a := []int { 10, 20, 30, 40 }
a = append(a[:1], a[2:]...)
```
