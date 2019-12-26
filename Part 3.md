# Go - Part 3

#### Branching

- In Go, a variable can be declared as part of the `if` statement, and it's scope be limited to the block that is executed.
```
func Greet(s Salutation, do Printer, isFormal bool) {
	msg, alt := CreateMessage(salutation.Name, salutation.Greeting)
	if prefix := "Mr "; isFormal {
		do(prefix + msg)
	} else {
		do(alt)
	}
}
```
- `if` and `else` block always need a paranthesis, even for single statements in the block.
- `switch`es in Go don't need an explicit `break` statement.
- `switch`es in Go don't need an expression to evaluate.
- `case`s can be expressions.
- `switch`es can switch based on type. Not just on value.
```
func DemoSwitch(name string) (prefix string) {
	switch name {
		case "Bob": prefix = "Mr "
		case "Joe": prefix = "Dr "
		case "Mary": prefix = "Mrs "
		default: prefix = "Dear "
	}
	return
}
```
- We can have multiple values match a `switch`
```
func DemoSwitch(name string) (prefix string) {
	switch name {
		case "Bob", "Amy": prefix = "Mr "
		case "Joe": prefix = "Dr "
		case "Mary": prefix = "Mrs "
		default: prefix = "Dear "
	}
	return
}
```
- `fallthrough` exeutes the next case as well
```
func DemoSwitch(name string) (prefix string) {
	switch name {
		case "Bob":
			prefix = "Mr "
			fallthrough
		case "Joe": prefix = "Dr "
		case "Mary": prefix = "Mrs "
		default: prefix = "Dear "
	}
	return
}
```
- The `switch` need not even have any variable. The `case` statements can specify the condition
```
func DemoSwitch(name string) (prefix string) {
	switch {
		case name == "Bob":
			prefix = "Mr "
			fallthrough
		case name == "Joe", len(name) == 5: prefix = "Dr "
		case name == "Mary": prefix = "Mrs "
		default: prefix = "Dear "
	}
	return
} 
```
- `switch` based on type of the parameter passed.
```
func DemoTypeSwitch(t interface()) {
	switch x := t.(type) {
		case int: fmt.println("int")
		case string: fmt.println("string")
		default: fmt.println("unknown")
	}
}

```
