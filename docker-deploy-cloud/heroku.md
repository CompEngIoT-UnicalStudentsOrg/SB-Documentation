# Heroku

Heroku is probably the easiest way we have to deploy our app on the cloud. Easy to setup, deploy and start.

## Table of Contents
- [Pros](#pros)
- [Cons](#cons)
- [How To](#how-to)
	- [Basic app](#basic-app)
	- [Docker app](#docker-app)

### Pros

- Free hour pool (550 hrs) by default + possibility of having more by coupling a card + github student pack
- Really easy to setup, very simple apps deployed in ~10 mins
- support for heroku based docker registries

### Cons

- forced to use credit/debit card
- little bit difficult to use for more complex stuff/architectures
- docker support is a bit more tedious to setup than on digitalocean

## How To

The platform is pretty easy to use with git + the heroku cli. Install it from their website, then you can quickly deploy an app in minutes.

### Basic app

For example I created a small go web server like this:

```go
package main

import (
	"encoding/json"
	"fmt"
	"log"
	"net/http"
	"os"

	"github.com/gorilla/mux"
)

func home(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-type", "application/json")
	hello := struct {
		Message string `json:"msg"`
	}{
		Message: "hello!",
	}

	if err := json.NewEncoder(w).Encode(hello); err != nil {
		w.WriteHeader(http.StatusInternalServerError)
	}
}

func main() {
	port := os.Getenv("PORT")

	if port == "" {
		log.Fatal("$PORT must be set")
	}

	portString := fmt.Sprintf(":%s", port)

	router := mux.NewRouter()
	router.HandleFunc("/", home).Methods("GET")
	log.Fatal(http.ListenAndServe(portString, router))
}
```

I logged in the heroku cli (first time only):
```bash
heroku login
```

Then I deployed it by using:

```
heroku create
go mod init heroku_test
go mod tidy
git add .
git commit -m "first commit"
git push heroku master

heroku open
```

### Docker app

Building a docker app is quite simple too, you need the heroku cli, git and dockeron your machine.
Using the same app from the other example, I also add a **Dockerfile** file:

```Dockerfile
FROM golang:1.15-alpine AS builder

ENV GO111MODULE=on \
    CGO_ENABLED=0 \
    GOOS=linux

WORKDIR /app
COPY . .

RUN go mod download
RUN go build -o go-web-basic .

CMD ["/app/go-web-basic"]

```

This isused to login intothe container registry:
```bash
heroku container:login 
```

Then to build and deploy:

```bash
go mod init heroku_test
go mod tidy
git add .
git commit -m "first commit"
git push heroku master
heroku create
heroku container:push web
heroku container:release web
heoku open
```