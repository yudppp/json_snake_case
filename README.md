# json_snake_case

## about

json snake case tag generater.

## Installation
```
$ go get github.com/yudppp/json_snake_case/cmd/json_snake_case
```

## How to use

```go
package main

import (
	"encoding/json"
	"fmt"
)

type User struct {
	UserID int
	Name   string
}

func main() {
	user := User{UserID: 10, Name: "yudppp"}
	b, _ := json.Marshal(&user)
	fmt.Println(string(b))
}
```

the above print `{"UserID":10,"Name":"yudppp"}`

```
$ cd path/to/app
$ json_snake_case -type=User
```

Generated `user_json.go` file.

And go run again. This print `{"user_id":10,"name":"yudppp"}`

## go generate
```go
...

//go:generate json_snake_case -type=User
type User struct {
	UserID int
	Name   string
}

...
```

```
$ go generate
```

## Examples

```go
type User struct {
	UserID int
	Name   string
}
// -->
type UserJSON struct {
	UserID int    `json:"user_id"`
	Name   string `json:"name"`
}
```

```go
type User struct {
	UserID int     `json:"-"`
	Name   string  `json:"nickname"`
  Email  *string `json:",omitempty"`
}
// -->
type UserJSON struct {
	UserID int     `json:"-"`
	Name   string  `json:"nickname"`
	Email  *string `json:"email,omitempty"`
}
```

## TODO

- add test code

## License

[The MIT License (MIT)](http://yudppp.mit-license.org/)
