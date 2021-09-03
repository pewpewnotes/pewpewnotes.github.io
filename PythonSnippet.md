### Python Snippets of Code

***

* Matching two blocks of text and return a similarity ratio
```
import difflib
from difflib import SequenceMatcher
SequenceMatcher(None,"rainn","rain").ratio()

>>> 0.8888888888
```
* Matching Text but the most resembling one
```
from difflib import get_close_matches
get_close_matches(word, set of words, minimumnumber, ratioforcomparison)
```
* Reverse a string
```
MyString = 'Hello World'
reverseofMyString = MyString[::-1]
```
