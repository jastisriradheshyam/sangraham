+++
title = 'Go Memory'
date = 2025-07-15T11:53:43Z
draft = false
description = "Information on Go memory management"
+++

# Array management

When element is appended to array and if size/length is exceeded to append into the array then array capacity is increased by factor of 2

## Example to demonstrate the capacity increase

```go
package main

import (
	"fmt"
)

func main() {
	arr := []int{}
	lastCap := cap(arr)
	for i := 0; i < 1000; i++ {
		arr = append(arr, i*2)
		if lastCap != cap(arr) {
			fmt.Println("Cap", cap(arr), "len", len(arr))
			lastCap = cap(arr)
		}
	}
}
```

```text
Cap 1 len 1
Cap 2 len 2
Cap 4 len 3
Cap 8 len 5
Cap 16 len 9
Cap 32 len 17
Cap 64 len 33
Cap 128 len 65
Cap 256 len 129
Cap 512 len 257
Cap 848 len 513
Cap 1280 len 849
```