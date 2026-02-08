```

  ____                 __   ____       _                   
 / ___| _     _       / /  / ___| ___ | | __ _ _ __   __ _ 
| |   _| |_ _| |_    / /  | |  _ / _ \| |/ _` | '_ \ / _` |
| |__|_   _|_   _|  / /   | |_| | (_) | | (_| | | | | (_| |
 \____||_|   |_|   /_/     \____|\___/|_|\__,_|_| |_|\__, |
                                                     |___/ 
```



# ⚡ C++ & Go Cheatsheet (Interview / NeetCode)

This is a **syntax recall cheatsheet**, not a tutorial.  
Goal: unblock yourself fast under pressure.

---

## C++

### Vector
- vector<int> v;
- v.push_back(x);
- v.pop_back();
- v[i]
- v.size()
- v.empty()

### Iterate Vector
- for (int i = 0; i < v.size(); i++) {}
- for (int x : v) {}
- for (int &x : v) {}   // modify elements

### Sort
- sort(v.begin(), v.end())
- sort(v.begin(), v.end(), greater<int>())

### Pair
- pair<int,int> p = {a, b}
- p.first
- p.second

### Vector of Pairs
- vector<pair<int,int>> vp
- sort(vp.begin(), vp.end())
- sort(vp.begin(), vp.end(), [](auto &a, auto &b) {
    return a.second < b.second;
  })

### Map (Hash Map)
- unordered_map<int,int> mp
- mp[key]++
- mp[key] = value
- mp.find(key) != mp.end()
- mp.erase(key)
- mp.size()

### Iterate Map
- for (auto &p : mp) {
    p.first
    p.second
  }

### Set
- unordered_set<int> s
- s.insert(x)
- s.count(x)
- s.erase(x)

### String
- string s
- s.size()
- s[i]
- s.substr(start, length)

### String → Frequency Map
- unordered_map<char,int> freq
- for (char c : s) freq[c]++

### Stack
- stack<int> st
- st.push(x)
- st.top()
- st.pop()
- st.empty()

### Queue
- queue<int> q
- q.push(x)
- q.front()
- q.pop()

### Priority Queue (Max Heap)
- priority_queue<int> pq

### Priority Queue (Min Heap)
- priority_queue<int, vector<int>, greater<int>> pq

---

## GO

### Slice
- var a []int
- a = append(a, x)
- a[i]
- len(a)

### Iterate Slice
- for i := 0; i < len(a); i++ {}
- for _, v := range a {}

### Sort
- sort.Ints(a)

### Map
- m := make(map[int]int)
- m[k]++
- m[k] = v
- v, ok := m[k]
- delete(m, k)
- len(m)

### Iterate Map
- for k, v := range m {}

### Set (using map)
- seen := make(map[int]bool)
- seen[x] = true
- if seen[x] {}

### Set (zero-size value)
- seen := make(map[int]struct{})
- seen[x] = struct{}{}
- _, ok := seen[x]

### String
- s := "abc"
- len(s)
- s[i]   // byte

### String → Frequency Map
- freq := make(map[byte]int)
- for i := 0; i < len(s); i++ {
    freq[s[i]]++
  }

### Rune-safe String Loop
- for _, r := range s {}

### Stack (slice)
- st := []int{}
- st = append(st, x)
- top := st[len(st)-1]
- st = st[:len(st)-1]

### Queue (slice)
- q := []int{}
- q = append(q, x)
- front := q[0]
- q = q[1:]

---

## =====================
## PATTERNS
## =====================

- Duplicate check → hash map / set
- Frequency counting → map
- Anagram → frequency maps or sliding window
- Top K → heap or partial sort
- Sliding window → two pointers + map
- Need order → sort
- Need memory → map / set


