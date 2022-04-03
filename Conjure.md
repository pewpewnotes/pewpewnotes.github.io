```
  ____             _                
 / ___|___  _ __  (_)_   _ _ __ ___ 
| |   / _ \| '_ \ | | | | | '__/ _ \
| |__| (_) | | | || | |_| | | |  __/
 \____\___/|_| |_|/ |\__,_|_|  \___|
                |__/                
```

* evaluating the whole buffer using <localleader>eb
* You can open the log buffer in a few ways:
    * Horizontally - <localleader>ls
    * Vertically - <localleader>lv
    * New tab - <localleader>lt
* All visible log windows (including the HUD) can be closed with <localleader>lq
* If you ever need to clear your log you can use the reset mappings:
  * Soft reset (leaves windows open) - <localleader>lr
  * Hard reset (closes windows, deletes the buffer) - <localleader>lR
* cursor on the inner form (the one inside the comment) and use <localleader>ee to evaluate it.
* If we want to evaluate the outermost form under our cursor, we can use <localleader>er instead.
* Try pressing "cp to paste the contents of the register into your buffer.
* evaluate a form and replace it with the result of the evaluation with <localleader>e!
* Place your cursor on the next lesson form below and use mf to set the f mark at that location.
  Now move your cursor elsewhere in the buffer and use <localleader>emf to evaluate it.
* inspecting the contents of the variable below by placing your cursor on it and pressing <localleader>ew
* You should see the contents in the HUD or log.
  You can evaluate visual selections with <localleader>E
  Try evaluating the form below using a visual selection.
* You can also evaluate a given motion with <localleader>E
  Try <localleader>Eiw below to evaluate the word.
* Use <localleader>Ea( to evaluate the lesson form.
  You can learn about specific languages with :help conjure-client- and then tab completion.
  For example, conjure-client-fennel-aniseed or conjure-client-clojure-nrepl.



