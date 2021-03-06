### dbms

---

- README.md
- pg
  - data
    - pg_hba.conf #main
    - postgresql.conf
  - config
    - database.yml
  - cmd.sh

- mysqld
  - my.cnf #main
  - config
    - database.yml
  - cmd.sh

- .gemrc

- cmd.sh
- linux.sh

---

.go
https://github.com/upper/db

```gp
package main

import (
  "log"
  
  "upper.io/db.v3/postgresql"
)

var settings = postgresql.ConnectionURL{
  Host: "demo.upper.io",
  Database: "booktown",
  User: "demouser",
  Password: "demoop4ss",
}

type Book struct {
  ID int `db:"id"`
  Title string `db:"title"`
  AuthorID int `db:"author_id"`
  SubjectID int `db:"subject_id"`
}

func main() {
  sess, err := postgresql.Open(settings)
  if err != nil {
    log.Fatalf("db.Open(): %q\n", err)
  }
  defer sess.Close()
  
  var books []Book
  err = sess.Collection("books").Find().All(&books)
  if err != nil {
    log.Fatalf("Find(): %q\n", err)
  }
  
  for i, book := range books {
    log.Printf("Book %d: %#v\n", i, book)
  }
}

```

```
go get upper.io/db.v3
```
