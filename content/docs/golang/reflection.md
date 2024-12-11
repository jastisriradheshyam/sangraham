+++
title = 'Reflection'
date = 2024-12-11T15:29:18Z
draft = false
+++

Examine, introspect, and modify behavior at runtime.[^2]

"Reflection in computing is the ability of a program to examine its own structure, particularly through types; it’s a form of metaprogramming."[^3]

## Disadvantages

- Less performant
- Hard to read

```go
package main

import (
	"fmt"
	"reflect"
)

type User struct {
	Name  string `validate:"min=2,max=32"`
	Email string `validate:"required,email"`
}

func main() {
	user := User{
		Name:  "Radhe",
		Email: "radhe@xyz.xyz",
	}

	t := reflect.TypeOf(user)

	fmt.Println("Name:", t.Name())
	fmt.Println("Kind:", t.Kind())

	// NumField works with struct
	for i := 0; i < t.NumField(); i++ {
		field := t.Field(i)
		tag := field.Tag.Get("validate")
		fmt.Printf("%d. %v (%v), tag: '%v'\n", i+1, field.Name, field.Type.Name(), tag)
	}
}
```

**Result**
```
Name: User
Kind: struct
1. Name (string), tag: 'min=2,max=32'
2. Email (string), tag: 'required,email'
```

# Additional Links

1. [reflect package - reflect - Go Packages](https://pkg.go.dev/reflect)

# References

[^2]:[Creating custom struct tags in Golang is awesome! - YouTube](https://www.youtube.com/watch?v=vtHZb7gNlbw)
[^3]:[The Laws of Reflection - The Go Programming Language](https://go.dev/blog/laws-of-reflection)
