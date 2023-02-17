```

 _     _           
| |   (_)___ _ __  
| |   | / __| '_ \ 
| |___| \__ \ |_) |
|_____|_|___/ .__/ 
            |_|    
```

### Guess The Number

We start off with defining two variables, small and big.

we use defparameter, alternatively defvar could be used as well but do know that def paramter allows modification of globals and defvar does not.

```
(defparamter *small* 1)
(defparamter *big* 1000)
# * -> earmuffs, for globals. Convention
```

then we define our function 

```
(defun guess-my-number ()
  (ash (+ *small* *big*) -1)
  )
```

`ash` is a function that allows bitshifting in lisp, ash with 1 as param, shifts bits to left and discards, and with -1 it does right shift. As we know, left shift is basically multiply by 2 and right shift is divide by 2 in bitarithmetic

Do know, that its mostly integer division, flaots won't work.

```
(ash 11 1)
(ash 11 -1)
```
Then we define and explain functions smaller and bigger

```
(defun smaller ()
(setf *big* (1- (guess-my-number)))
(guess-my-number) )
SMALLER
Break 1 [7]> (defun bigger ()
(setf *small* (1+ (guess-my-number)))
(guess-my-number) )
BIGGER

```

```
(defun startover ()
(defparameter *small* 1)
(defparameter *big* 100)
(guess-my-number) )
STARTOVER
```

Next we have learning bits about things like Defininng local functions in lisp.

```
(flet ((function_name (argument)
          function_body
          ))
          ...body...
  )
```
