```
  ____            
 / ___| _     _   
| |   _| |_ _| |_ 
| |__|_   _|_   _|
 \____||_|   |_|  
                  
```
## C++ Snippets

***

### Splitting on the basis of Space
```
// p is string space separated.
int start = 0;
    int end = p.find(" ");
    i = 0;
    // std::cout << "Start: " << start << "End: " << end << std::endl;
    while (end != -1) {
        _t[i] = std::stoi((p.substr(start, end - start)));
        start = end + 1;
        end = p.find(" ", start);
        i++;
    }
```

### Taking string input
```
std::string p, a, dump;
std::getline (std::cin, p);
std::cin >> std::ws;
std::getline (std::cin, a);
```


