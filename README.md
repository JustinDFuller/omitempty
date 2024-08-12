# omitempty

> [!CAUTION]
> Heavily Work In Progress.
> Tests are broken.
> Do not use in production.

Have you ever just wanted Go's JSON marshaler to simply `omitempty` on *everything*?

```go
package main

import (
    "fmt"

    "github.com/justindfuler/omitempty"
)

type Example struct {
    EmptyString string
    NonEmptyString string
    EmptyStruct Example
    NonEmptyStruct Example
}

func main() {
    example := Example{
        NonEmptyString: "Hello, World!",
        NonEmptyStruct: Example{
            NonEmptyString: "Hello, World!",
        },
    }

    b, err := omitempty.Marshal(example)
    if err != nil {
        panic(err)
    }

    fmt.Println(string(b))
}
```

The result will not print `EmptyString` or `EmptryStruct`, even though `json:",omitempty:"` was not included in the tags.
