# Go - Part 5

#### Methods and Interface

- Methods in Go can specify a named type it operates on, in addition to the function parameters.
- A method can specify any named type in the same package as the method declaration.
- It can also operate on a pointer to a named type, in which case we can make changes to that type.
- Let's say we have a named type and a method like below:
```
type Salutation struct {
	Name string
	Greeting string
}

type Printer func(string) {}

func Greet(salutation []Salutation, do Printer, isFormal bool, times int) {
	for _, s := range salutation {
		msg, alt := CreateMessage(s.Name, s.Greeting)
		if prefix := GetPrefix(s.name); isFormal {
			do(prefix + msg)
		} else {
			do(alt)
		}
	}
}
```

- To use method on the named type `Salutation`, since `Greet` operates on a collection of `Salutation` : 
```
type Salutations []Salutation

func (sls Salutations) Greet(do Printer, isFormal bool, times int) {
	for _, s := range sls {
		msg, alt := CreateMessage(s.Name, s.Greeting)
		if prefix := GetPrefix(s.name); isFormal {
			do(prefix + msg)
		} else {
			do(alt)
		}
	}
}

// Caller will now be:
salutations.Greet( //...
```

- Example of a method that works on pointer of a named type.
```
func (sl *Salutation) Rename (newName string) {
	sl.Name = newName
}
```

#### Interfaces
- Interfaces in Go specify methods and any named type that has methods of the same name (and parameters) implements that interface.
- There is no way to require that an interface is implemented.
- There is no function overloading in Go.
```
type Renamable interface {
	Rename(newName string)
}

func (sl *Salutation) Rename (newName string) {
	sl.Name = newName
}

func RenameToFrog(r Renamable) {
	r.Rename("Frog")
}

// Calling the interface
RenameToFrog(&sal)
```

- There can be empty interface and then any named type implements this interface.
