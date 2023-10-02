```
package main

import "fmt"

func main() {
  fmt.Println("hello, world")
}
```

```
# syntax=docker/dockerfile:1
FROM golang:1.21 as build
WORKDIR /src
COPY main.go /src/main.go
RUN go build -o /bin/hello ./main.go

FROM scratch
COPY --from=build /bin/hello /bin/hello
CMD ["/bin/hello"]
```


