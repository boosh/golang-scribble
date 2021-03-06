Scribble [![GoDoc](https://godoc.org/github.com/boltdb/bolt?status.svg)](http://godoc.org/github.com/nanobox-io/golang-scribble) [![Go Report Card](https://goreportcard.com/badge/github.com/nanobox-io/golang-scribble)](https://goreportcard.com/report/github.com/nanobox-io/golang-scribble)
--------

A tiny JSON database in Golang

### Installation

Install using `go get github.com/nanobox-io/golang-scribble`.

### Usage

```go
// a new scribble driver, providing the directory where it will be writing to,
// and a qualified logger if desired
db, err := scribble.New(dir, nil)
if err != nil {
  fmt.Println("Error", err)
}

// Write a fish to the database
fish := Fish{}
if err := db.Write("fish", "onefish", fish); err != nil {
  fmt.Println("Error", err)
}

// Read a fish from the database (passing fish by reference)
fish := []Fish{}
if err := db.Read("fish", "onefish", &fish); err != nil {
  fmt.Println("Error", err)
}

// Read all fish from the database, unmarshaling the response.
records, err := db.ReadAll("fish")
if err != nil {
  fmt.Println("Error", err)
}

fish := []Fish{}
if err := json.Unmarshal([]byte(records), &fish); err != nil {
  fmt.Println("Error", err)
}

// Delete a fish from the database
if err := db.Delete("fish", "onefish"); err != nil {
  fmt.Println("Error", err)
}

// Delete all fish from the database
if err := db.Delete("fish", ""); err != nil {
  fmt.Println("Error", err)
}
```

Also supports automatically generating integer IDs.

```
// Write a fish to the database
fish := Fish{}
id, err := db.WriteAutoId("fish", fish); if err != nil {
  fmt.Println("Error", err)
}

// ID == 1

// zero-pad when loading
idString := fmt.Sprintf("%08d", firstId)
if err := db.Read(collection, idString, &fish); err != nil {
  fmt.Println("Error", err)
}
```

## Documentation
- Complete documentation is available on [godoc](http://godoc.org/github.com/nanobox-io/golang-scribble).
- Coverage Report is available on [gocover](https://gocover.io/github.com/nanobox-io/golang-scribble)

## Todo/Doing
- Support for windows
- Better support for concurrency
- Better support for sub collections
- More methods to allow different types of reads/writes
- More tests (you can never have enough!)

## Contributing
Contributions to scribble are welcome and encouraged. Scribble is a [Nanobox](https://nanobox.io) project and contributions should follow the [Nanobox Contribution Process & Guidelines](https://docs.nanobox.io/contributing/).
