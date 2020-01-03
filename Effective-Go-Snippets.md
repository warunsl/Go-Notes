# Snippets from Effective Go blog post.
- Source: [Effective Go](https://golang.org/doc/effective_go.html)
- Go's declaration syntax allows grouping of declarations. A single doc comment can introduce a group of related constants or variables. Since the whole declaration is presented, such a comment can often be perfunctory.

```
// Error codes returned by failures to parse an expression.
var (
    ErrInternal      = errors.New("regexp: internal error")
    ErrUnmatchedLpar = errors.New("regexp: unmatched '('")
    ErrUnmatchedRpar = errors.New("regexp: unmatched ')'")
    ...
)
```    
- Grouping can also indicate relationships between items, such as the fact that a set of variables is protected by a mutex.
```
var (
    countLock   sync.Mutex
    inputCount  uint32
    outputCount uint32
    errorCount  uint32
)
```
- Names are as important in Go as in any other language. They even have semantic effect: the visibility of a name outside a package is determined by whether its first character is upper case.
- When a package is imported, the package name becomes an accessor for the contents. After
```
import "bytes"
```
the importing package can talk about `bytes.Buffer`.
- Go doesn't provide automatic support for getters and setters. There's nothing wrong with providing getters and setters yourself, and it's often appropriate to do so, but it's neither idiomatic nor necessary to put `Get` into the getter's name. If you have a field called `owner` (lower case, unexported), the getter method should be called `Owner` (upper case, exported), not `GetOwner`. The use of upper-case names for export provides the hook to discriminate the field from the method. A setter function, if needed, will likely be called `SetOwner`. 
- Convention in Go is to use `MixedCaps` or `mixedCaps` rather than underscores to write multiword names.
- Mandatory braces encourage writing simple if statements on multiple lines. 
- Since if and switch accept an initialization statement, it's common to see one used to set up a local variable.
```
if err := file.Chmod(0664); err != nil {
    log.Print(err)
    return err
}
```
- In the Go libraries, you'll find that when an `if` statement doesn't flow into the next statement—that is, the body ends in break, continue, goto, or return—the unnecessary else is omitted. Example:
```
f, err := os.Open(name)
if err != nil {
    return err
}
codeUsing(f)
```
- In the snippet below, the declaration that calls `os.Open` declares two variables, f and err. A few lines later, the call to `f.Stat` looks as if it declares d and err. Notice, though, that err appears in both statements. This duplication is legal: err is declared by the first statement, but only re-assigned in the second. This means that the call to f.Stat uses the existing err variable declared above, and just gives it a new value.
```
f, err := os.Open(name)
if err != nil {
    return err
}
d, err := f.Stat()
if err != nil {
    f.Close()
    return err
}
codeUsing(f, d)
```
- In a `:=` declaration a variable v may appear even if it has already been declared, provided:
  + this declaration is in the same scope as the existing declaration of v (if v is already declared in an outer scope, the declaration will create a new variable §),
  + the corresponding value in the initialization is assignable to v, and
  + there is at least one other variable in the declaration that is being declared anew.
  
- If you're looping over an array, slice, string, or map, or reading from a channel, a `range` clause can manage the loop. If you only need the first item in the range (the key or index), drop the second:
```
for key, value := range oldMap {
    newMap[key] = value
}
```
If you only need the second item in the range (the value), use the blank identifier, an underscore, to discard the first:
```
sum := 0
for _, value := range array {
    sum += value
}
```
- A `switch` with no expression is same as `switch true`. It's therefore possible—and idiomatic—to write an if-else-if-else chain as a switch.
```
func unhex(c byte) byte {
    switch {
    case '0' <= c && c <= '9':
        return c - '0'
    case 'a' <= c && c <= 'f':
        return c - 'a' + 10
    case 'A' <= c && c <= 'F':
        return c - 'A' + 10
    }
    return 0
}
```
- Although they are not nearly as common in Go as some other C-like languages, break statements can be used to terminate a switch early. Sometimes, though, it's necessary to break out of a surrounding loop, not the switch, and in Go that can be accomplished by putting a label on the loop and "breaking" to that label. This example shows both uses.
```
Loop:
	for n := 0; n < len(src); n += size {
		switch {
		case src[n] < sizeOne:
			if validateOnly {
				break
			}
			size = 1
			update(src[n])

		case src[n] < sizeTwo:
			if n+1 >= len(src) {
				err = errShortInput
				break Loop
			}
			if validateOnly {
				break
			}
			size = 2
			update(src[n] + src[n+1]<<shift)
		}
	}
```
