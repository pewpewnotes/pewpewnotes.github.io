```
  __ _  ___       (_)___  ___  _ __  
 / _` |/ _ \ _____| / __|/ _ \| '_ \ 
| (_| | (_) |_____| \__ \ (_) | | | |
 \__, |\___/     _/ |___/\___/|_| |_|
 |___/          |__/                 
```


# Go JSON Bible

A compact but thorough reference covering practical JSON parsing, marshaling, and common patterns in Go. Use this as a quick wiki page for copy/paste examples and explanations.

---

## Contents

1. Chapter 1 — Parsing Simple JSON into a Struct
2. Chapter 2 — Parsing JSON Arrays
3. Chapter 3 — Nested Objects
4. Chapter 4 — Optional / Missing Fields (pointers)
5. Chapter 5 — Dynamic / Unknown JSON (map[string]interface{})
6. Chapter 6 — Reading JSON from Files, APIs, CLI
7. Chapter 7 — JSON Tree Printing (recursive traversal)
8. Chapter 8 — Streaming JSON & json.Decoder
9. Chapter 9 — Custom Marshaling / Unmarshaling
10. Chapter 10 — Utilities, Gotchas, and Cheat-sheet

---

# Chapter 1 — Parsing Simple JSON into a Struct

**Goal**: Parse a tiny JSON object into a Go struct.

```go
package main

import (
	"encoding/json"
	"fmt"
)

type Person struct {
	Name  string `json:"name"`
	Age   int    `json:"age"`
	IsDev bool   `json:"isDev"`
}

func main() {
	jsonData := `{"name": "Kei", "age": 27, "isDev": true}`

	var p Person
	if err := json.Unmarshal([]byte(jsonData), &p); err != nil {
		fmt.Println("Error:", err)
		return
	}

	fmt.Println("Name:", p.Name)
	fmt.Println("Age:", p.Age)
	fmt.Println("Is Developer?", p.IsDev)
}
```

**Notes**:
- Struct tags `json:"field"` tell `encoding/json` how to map keys.
- Fields must be exported (capitalized) to be marshaled/unmarshaled.

---

# Chapter 2 — Parsing JSON Arrays

**Goal**: Parse a JSON array into a slice of structs.

```go
package main

import (
	"encoding/json"
	"fmt"
)

type Person struct {
	Name  string `json:"name"`
	Age   int    `json:"age"`
	IsDev bool   `json:"isDev"`
}

func main() {
	jsonData := `[
	{"name": "Kei", "age": 27, "isDev": true},
	{"name": "Ada", "age": 36, "isDev": false}
	]`

	var people []Person
	if err := json.Unmarshal([]byte(jsonData), &people); err != nil {
		panic(err)
	}

	for i, p := range people {
		fmt.Printf("Person %d: %+v\n", i+1, p)
	}
}
```

**Tip**: If JSON begins with `[` use a slice type `[]T` for Unmarshal target.

---

# Chapter 3 — Nested Objects

**Goal**: Handle nested JSON objects using nested structs.

```go
package main

import (
	"encoding/json"
	"fmt"
)

type Address struct {
	City    string `json:"city"`
	Country string `json:"country"`
	Zip     string `json:"zip"`
}

type Person struct {
	Name    string  `json:"name"`
	Age     int     `json:"age"`
	IsDev   bool    `json:"isDev"`
	Address Address `json:"address"`
}

func main() {
	jsonData := `{
	"name":"Kei",
	"age":27,
	"isDev":true,
	"address": { "city": "Mumbai", "country": "India", "zip": "400001" }
	}`

	var p Person
	if err := json.Unmarshal([]byte(jsonData), &p); err != nil {
		panic(err)
	}

	fmt.Println(p.Address.City)
}
```

---

# Chapter 4 — Optional / Missing Fields (Pointers & `omitempty`)

**Goal**: Detect if a field was present or omitted, and use `omitempty` when marshaling.

```go
package main

import (
	"encoding/json"
	"fmt"
)

type Person struct {
	Name  string `json:"name"`
	Age   *int   `json:"age"`          // pointer: nil if missing or null
	IsDev bool   `json:"isDev,omitempty"`
}

func main() {
	jsonData := `{"name": "Aria", "isDev": false}`

	var p Person
	if err := json.Unmarshal([]byte(jsonData), &p); err != nil {
		panic(err)
	}

	if p.Age == nil {
		fmt.Println("Age: not provided")
	} else {
		fmt.Println("Age:", *p.Age)
	}

	// Marshaling with omitempty: age==nil will be omitted
	out, _ := json.Marshal(p)
	fmt.Println(string(out))
}
```

**Notes**:
- `*T` fields let you check presence (`nil`) vs zero-value.
- `omitempty` in struct tags excludes zero values during Marshal.
- JSON `null` becomes `nil` for pointer fields.

---

# Chapter 5 — Dynamic / Unknown JSON (map[string]interface{})

**Goal**: Parse JSON whose schema is unknown at compile-time.

```go
package main

import (
	"encoding/json"
	"fmt"
)

func main() {
	jsonData := `{
	"user": { "id": 123, "name": "Kei", "roles": ["admin","dev"] },
	"meta": { "requestId": "xyz-123" }
	}`

	var raw map[string]interface{}
	if err := json.Unmarshal([]byte(jsonData), &raw); err != nil {
		panic(err)
	}

	user := raw["user"].(map[string]interface{})
	fmt.Println("Name:", user["name"].(string))

	roles := user["roles"].([]interface{})
	for i, r := range roles {
		fmt.Println(i, r.(string))
	}
}
```

**Gotchas**:
- Numbers default to `float64`.
- All objects -> `map[string]interface{}`, arrays -> `[]interface{}`.
- Always use safe assertions: `v, ok := x.(type)` to avoid panics.

---

# Chapter 6 — Reading JSON from Files, API, and CLI

**Goals**: Read JSON from file, HTTP response, or STDIN.

### Read from file

```go
package main

import (
	"encoding/json"
	"fmt"
	"io/ioutil"
)

func main() {
	b, _ := ioutil.ReadFile("data.json")
	var v map[string]interface{}
	if err := json.Unmarshal(b, &v); err != nil {
		panic(err)
	}
	fmt.Println(v)
}
```

### Read from HTTP

```go
resp, err := http.Get("https://example.com/data.json")
defer resp.Body.Close()
json.NewDecoder(resp.Body).Decode(&v)
```

### Read from STDIN

```go
import "os"

decoder := json.NewDecoder(os.Stdin)
var v interface{}
decoder.Decode(&v)
```

**Notes**:
- Prefer `json.NewDecoder` when streaming or reading large files.
- `ioutil.ReadFile` is fine for small files but loads full content into memory.

---

# Chapter 7 — JSON Tree Printer (recursive traversal)

**Goal**: Print arbitrary JSON as a tree for exploration/debug.

```go
package main

import (
	"encoding/json"
	"fmt"
	"os"
)

func printJSONTree(data interface{}, indent string) {
	switch v := data.(type) {
	case map[string]interface{}:
		for k, val := range v {
			fmt.Println(indent + "├── " + k)
			printJSONTree(val, indent+"│   ")
		}
	case []interface{}:
		for i, item := range v {
			fmt.Printf(indent+"├── [%d]\n", i)
			printJSONTree(item, indent+"│   ")
		}
	default:
		fmt.Println(indent + "└── " + fmt.Sprintf("%v", v))
	}
}

func main() {
	var data interface{}
	if err := json.NewDecoder(os.Stdin).Decode(&data); err != nil {
		panic(err)
	}
	fmt.Println("root")
	printJSONTree(data, "")
}
```

**Usage**:
- Save file `tree.go`, `go build tree.go`, then `cat sample.json | ./tree` to visualize structure.

---

# Chapter 8 — Streaming JSON & json.Decoder

**Goal**: Process large JSON files or streams token-by-token without loading everything into memory.

### Token decoder example (streaming array)

```go
package main

import (
	"encoding/json"
	"fmt"
	"os"
)

func main() {
	f, _ := os.Open("large.json")
	defer f.Close()
	dec := json.NewDecoder(f)

	// Suppose file contains an array of objects: [ {...}, {...}, ... ]
	t, _ := dec.Token() // read '['
	fmt.Println("Token:", t)

	for dec.More() {
		var obj map[string]interface{}
		if err := dec.Decode(&obj); err != nil {
			panic(err)
		}
		fmt.Println("Object:", obj)
	}
}
```

**Notes**:
- `Decode` reads one JSON value and advances the stream.
- Use `Token()` and `More()` to traverse arrays and objects when you need fine-grained streaming.

---

# Chapter 9 — Custom Marshaling / Unmarshaling

**Goal**: Implement `json.Marshaler` / `json.Unmarshaler` for custom types or validation.

```go
package main

import (
	"encoding/json"
	"fmt"
)

type Age int

func (a Age) MarshalJSON() ([]byte, error) {
	// custom: always output as string
	return json.Marshal(fmt.Sprintf("%d years", a))
}

func (a *Age) UnmarshalJSON(b []byte) error {
	// attempt to unmarshal either string "30 years" or number
	var i int
	if err := json.Unmarshal(b, &i); err == nil {
		*a = Age(i)
		return nil
	}
	var s string
	if err := json.Unmarshal(b, &s); err != nil {
		return err
	}
	_, err := fmt.Sscanf(s, "%d", &i)
	if err != nil {
		return err
	}
	*a = Age(i)
	return nil
}

func main() {
	var a Age = 30
	b, _ := json.Marshal(a)
	fmt.Println(string(b))
}
```

**When to use**:
- Normalizing inconsistent incoming formats.
- Hiding fields, custom date formats, validation.

---

# Chapter 10 — Utilities, Gotchas, and Cheat-sheet

### Common gotchas
- Numbers become `float64` when decoding into `interface{}`.
- You cannot index an `interface{}` directly — assert its underlying type first.
- Missing fields → zero value. Use pointers to detect absence.
- Unexported fields are ignored by encoding/json.
- `json.Unmarshal` into a struct with mismatched types causes errors.

### Quick helper snippets

**pack/unpack JSON safely**

```go
// safe string extraction
func getString(m map[string]interface{}, key string) (string, bool) {
	v, ok := m[key]
	if !ok {
		return "", false
	}
	s, ok := v.(string)
	return s, ok
}
```

**Convert float64 to int safely**

```go
func toInt(v interface{}) (int, bool) {
	f, ok := v.(float64)
	if !ok { return 0, false }
	return int(f), true
}
```

---

# Appendix — Examples Summary

- `json.Marshal` & `json.Unmarshal` for typed structs
- `*T` pointer fields to detect absent keys
- `map[string]interface{}` for dynamic JSON
- `json.Decoder` for streaming/large JSON
- Custom `MarshalJSON` / `UnmarshalJSON` for special formats
- Tools & patterns: `struct tags`, `omitempty`, `raw json.RawMessage` for deferred parsing

---

If you'd like, I can also:
- add `raw` examples using `json.RawMessage` to show deferred parsing
- include a small `go fmt`-ready repo structure with tests and sample JSON files

Happy parsing — you’ll be able to handle just about any JSON blob after these chapters.

