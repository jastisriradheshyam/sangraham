+++
title = 'Go: Error'
date = 2024-12-14T01:40:13+05:30
draft = false
description = 'Information on Golang error management'
+++

# error

## General error management

`error` object is returned.

```go
func divide(number1, number2 int) (int, error) {
	if number2 == 0 {
		return 0, errors.New("cannot divide by 0")
	}
	return number1/number2, nil
}

func main() {
	result,err := divide(1,2)
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println(result)
}
```

## Using error interface to create manage error output [^3]

```go
// This interface needs to be implemented
/*
type error interface {
  Error() string
}
*/

type DivideByZeroErr struct{
	num1 int
	num2 int
}

func (err *DivideByZeroErr) Error() string {
	return fmt.Sprintf("cannot divide %d by 0", err.num1)
}

func divide(number1, number2 int) (int, error) {
	if number2 == 0 {
		return 0, &DivideByZeroErr{number1, number2}
	}
	return number1/number2, nil
}

func main() {
	result,err := divide(1,0)
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println(result)
}

// output
// cannot divide 1 by 0
```

# MUST pattern

Basically when an error occurs there is a situation where one would want the application to stop if not succeeded. some use cases are, Initially making database connection or initializing something for app to run and it fails.

Example: `func MustCompile(str string) *Regexp` [^2]

**With the use of use case specific OBJECT_TYPE (replace OBJECT_TYPE with your required return type)**
```go
func Must(obj OBJECT_TYPE, err error) OBJECT_TYPE {
    if err != nil {
        panic(err)
    }
    return obj
}
```

**With the use of generics** [^1]
```go
func Must[T any](obj T, err error) T {
    if err != nil {
        panic(err)
    }
    return obj
}
```

# Panic

```go
package main

import "fmt"

func causePanic() {
	panic("something went terribly wrong")
}

func main() {
	fmt.Println("Before panic")
	causePanic()
	fmt.Println("After panic") // This line won't be executed
}
```

## Panic with defer

Defer will run before panic

```go
package main

import "fmt"

func causePanic() {
	panic("something went terribly wrong")
}

func main() {
	defer func() {
		fmt.Println("Ran before panic")
	}()
	fmt.Println("Before panic")
	causePanic()
	fmt.Println("After panic") // This line won't be executed
}
```

## Recovering from Panic

```go
package main

import "fmt"

func safeFunction() {
	defer func() {
		if r := recover(); r != nil {
			fmt.Println("Recovered from panic:", r)
		}
	}()
	panic("unexpected error")
}

func main() {
	safeFunction()
	fmt.Println("Program continues after recovery")
}
```

**Output**:
```text
Recovered from panic: unexpected error
Program continues after recovery
```

### Recovering from Panic when Panic within nested functions

```go
package main

import "fmt"

func main() {
	defer handlePanic() // recover is here, not in riskyFunction
	riskyFunction()
	fmt.Println("Program continues after recovery")
}

func panicInsideRiskyFunction() {
	panic("something went wrong in panicInsideRiskyFunction")
}

func riskyFunction() {
	panicInsideRiskyFunction()
}

func handlePanic() {
	if r := recover(); r != nil {
		fmt.Println("Recovered from panic:", r)
	}
}
```

**Output**:
```text
Recovered from panic: something went wrong in panicInsideRiskyFunction
```

# Additional links

1. [Creating Custom Errors in Go | DigitalOcean](https://www.digitalocean.com/community/tutorials/creating-custom-errors-in-go)

# References

[^1]:[Built-in helper for "Must" pattern in Go - Stack Overflow](https://stackoverflow.com/questions/12434565/built-in-helper-for-must-pattern-in-go)
[^2]:[regexp package - regexp - Go Packages](https://pkg.go.dev/regexp#MustCompile)
[^3]:[builtin package - builtin - Go Packages](https://pkg.go.dev/builtin#error)
