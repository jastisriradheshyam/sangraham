+++
title = 'Go Debugging'
date = 2025-02-22T20:06:02+05:30
draft = false
description = "Information on Go debugging ways and techniques"
+++

# Everyone's favorite: print function

- Generally we use `Printf` or `Println` and other print function variants to print the variable to what's the value
- With `Printf` we can have format specifiers to format the variables especially complex ones
  - `%v`: will only print values without keys
  - `%+v`: will print values with keys
  - `%#v`: will print variable type along with keys in variable, it's more verbose than `#+v` format specifier
  - `%T`: will represent the type of the variable
  - Example: https://go.dev/play/p/yHGoKST0lEx

# Debugger

## `delve`

### Features

- Set breakpoints
- Inspect goroutines
- evaluate and manipulate variables in real-time

### Installation

- `go install github.com/go-delve/delve/cmd/dlv@latest`
- check if it's accessiable through cli by running checking the version: `dlv version`
  - if it's not accessiable then `$GOPATH/bin` is not in your `$PATH`

### Running with `delve`

- `dlv debug GO_PROGRAM_ENTRY_FILE_PATH GO_PROGRAM_PARAMETERS_IF_ANY`
