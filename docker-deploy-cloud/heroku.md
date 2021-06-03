# Heroku

Heroku is probably the easiest way we have to deploy our app on the cloud. Easy to setup, deploy and start.

### Pros

- Free hour pool (550 hrs) by default + possibility of having more by coupling a card + github student pack
- Really easy to setup, very simple apps deployed in ~10 mins
- support for heroku based docker registries

### Cons

- forced to use credit/debit card
- little bit difficult to use for more complex stuff/architectures
- docker support is a bit more tedious to setup than on digitalocean

## How To

It's pretty easy to use with git + the heroku cli. Install it from their website, then you can quickly deploy an app in minutes.

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