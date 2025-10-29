#
Go Project Ladder 🚀

A progressive set of Go projects (1/10 → 10/10) with requirements and usage expectations.

---

## 1. JSON Prettifier (Difficulty 1/10)

### Requirements
- Read a `.json` file from disk.
- Pretty-print with indentation.
- Optionally minify JSON.

### Usage
```bash
jsonfmt input.json       # pretty-prints
jsonfmt -min input.json  # minifies
```
- scintillating-json
---

## 2. Word Counter (wc clone) (Difficulty 2/10)

### Requirements
- Count characters, words, and lines.
- Handle multiple files.

### Usage
```bash
wc file.txt          # prints lines, words, chars
wc -c file.txt       # prints only characters
wc -w file.txt       # prints only words
wc -l file.txt       # prints only lines
```

---

## 3. Notes CLI (Difficulty 3/10)

### Requirements
- Add, list, and delete notes.
- Store notes in a JSON file.

### Usage
```bash
notes add "Buy milk"
notes list
notes delete 1
```

---

## 4. URL Shortener (In-Memory) (Difficulty 4/10)

### Requirements
- HTTP server with endpoints:
  - POST `/shorten` → returns short URL
  - GET `/abc123` → redirects to full URL
- Store mappings in memory.

### Usage
```bash
curl -X POST localhost:8080/shorten -d "https://example.com"
# returns http://localhost:8080/abc123

curl localhost:8080/abc123
# redirects to https://example.com
```

---

## 5. Expense Tracker (Difficulty 5/10)

### Requirements
- Log expenses with category and amount.
- Summarize expenses by category.
- Export to CSV.

### Usage
```bash
expenses add "Coffee" 150 Food
expenses list
expenses summary
expenses export report.csv
```

---

## 6. TCP Chat Server (Difficulty 6/10)

### Requirements
- Accept multiple client connections.
- Broadcast messages to all connected clients.
- Handle disconnects gracefully.

### Usage
```bash
go run chatserver.go
# in another terminal:
telnet localhost 9000
```

---

## 7. SQLite Notes App (Difficulty 7/10)

### Requirements
- Notes CLI (like #3) but with SQLite backend.
- CRUD operations for notes.
- Simple search functionality.

### Usage
```bash
notes add "Read Go book"
notes list
notes search "Go"
notes delete 2
```

---

## 8. Static Site Generator (Difficulty 8/10)

### Requirements
- Convert `.md` files to `.html`.
- Use templates for consistent layout.
- Generate full site into `/public` folder.

### Usage
```bash
ssg build content/ public/
# converts all markdown in content/ into HTML
```

---

## 9. Kanban CLI (Difficulty 9/10)

### Requirements
- Manage tasks with states: ToDo, Doing, Done.
- Move tasks between states.
- Store tasks in SQLite/JSON.

### Usage
```bash
kanban add "Learn Go concurrency"
kanban list
kanban move 1 Doing
kanban list Doing
```

---

## 10. Mini Git (Difficulty 10/10)

### Requirements
- Initialize a repo (`init`).
- Commit snapshots of files.
- Show commit history (`log`).

### Usage
```bash
minigit init
minigit commit -m "First commit"
minigit log
```

# Includes the project ideas and Plans that I have. 

1. I want to create some sort of automatic telegram channel content downloader, meaning if there is something that I want from a channel to be downloaded
   it should download it automatically. 
2. Fuzzy search enabled notes manager and synchronisations, that will totally be helpful if merged with bookmarks

* iterfzf for fuzzy finding
* git for synchronisation 
* xsel or something similar for clipboard

1. Automatic mount with rclone and having some good speed 
4. An automated script for the automation of scenarios in MPTCP


