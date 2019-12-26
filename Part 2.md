# Go - Part 2

#### Functions
- In Go, functions can return multiple values.
- Functions can be used like any other type. They can be declared as variables, passed to other functions and returned from other functions.
- Go supports function literals i.e., it allows you to declare a function within a function. Supports closure.
- The opening brace of the function should start on the same line as the function name. Otherwise, when the Go compiler adds a semi-colon at the end of every statement, it adds one at the end of function name, making it a body-less function.
```
// Simple example. Returns void, so not needed to specify.
func Greet(Salutation s) {
	fmt.Println(s.name)
	fmt.Println(s.greeting)
}

// Function with a return type.
func CreateMessage(name, greeting string) string { 
	// Only greeting has type. It specifies the type for both name and greeting.
	return greeting + " " + name
}

// Function returning multiple values. Here, two strings
func CreateMessage(name, greeting string) (string, string) {
	return greeting + " " + name, "Hey " + name
}

// At the caller.
msg, alt = CreateMessage("Varun", "Hey")
```
- When a statement consumes multiple return values from a function, all of them have to be used, otherwise the Go compiler throws an error. Use `_` for unused variables, like python.
- In Go, you can name the return values. This returns whatever is the current value for those variables.
```
func CreateMessage(name, greeting string) (msg string, alt string) {
	msg = greeting + " " + name
	alt = "Hey " + name
	return
}
```

#### Variadic Functions
- Go allows variable number of function parameters of a particular type using `...`.
- It just has to be the last parameter to the function.
```
func CreateMessage(name, greeting ...string) (msg string, alt string) {
	fmt.Println(len(greeting))
	msg = greeting[0] + " " + name
	alt = "Hey " + name
	return
}

// Caller.
msg, alt = CreateMessage("Varun", "Hey". "Wassup")
```
- Slices are usually passed to the variadic functions.

#### Function types
- Here `do` is a function that takes in a `string` but does not return any value.
```
func Greet(s Salutation, do func(string)) {
	do(s.name)
	do(s.greeting)
}
```
- To make the syntax more clearer, we can create a new type for the function parameter above, and pass in the new type name.
```
type Printer func(string) () // Empty parantheses important.
func Greet(s Salutation, do Printer) {
	...
}
```

#### Closures
- Functions can return other functions. Ex:
```
func customPrinter(custom string) Printer {
	return func(s string) {
		fmt.Println(s + custom) // Can access custom from the outer function.
	}
}

```



