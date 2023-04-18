```

 ____  _        _             
/ ___|| |_ _ __(_)_ __   __ _ 
\___ \| __| '__| | '_ \ / _` |
 ___) | |_| |  | | | | | (_| |
|____/ \__|_|  |_|_| |_|\__, |
                        |___/ 
 __  __             _             _       _   _             
|  \/  | __ _ _ __ (_)_ __  _   _| | __ _| |_(_) ___  _ __  
| |\/| |/ _` | '_ \| | '_ \| | | | |/ _` | __| |/ _ \| '_ \ 
| |  | | (_| | | | | | |_) | |_| | | (_| | |_| | (_) | | | |
|_|  |_|\__,_|_| |_|_| .__/ \__,_|_|\__,_|\__|_|\___/|_| |_|
                     |_|                                    
 ____            _     
| __ )  __ _ ___| |__  
|  _ \ / _` / __| '_ \ 
| |_) | (_| \__ \ | | |
|____/ \__,_|___/_| |_|
                       
```

* Concatenate two strings x, y
```
x="Unix"
y="Utils"
echo $x$y => UnixUtils
```
* Delimit string with Character
```
x='Unix-Utils-Universe'
IFS=- read -r x y z <<< "$x"
echo $x => Unix
echo $y => Utils
echo $z => Universe
```
* Delimit and Convert to array 
```
x='Unix-Utils-World'
IFS=- read -ra string <<< "$x"
echo ${string[@]}
```
* Get length of String
```
name=unixutils
echo ${#name}
```
* Get substring from a specific position
```
name=unixutils
echo ${name:0} => unixutils
echo ${name:1} => nixutils
echo ${name:2} => ixutils
echo ${name:start:end}
```
* Replace one string with another
```
x=-Unix-Utils-World-
echo ${x/World/Universe} => Unix-Utils-Universe
echo ${x/World} => Deletes world 
echo ${x/-} => removes first occurance of -
echo ${x//-} => removes all occurance of -
echo ${x/#-} => removes all occurance of - which is a prefix 
echo ${x/%-} => removes all occurance of - which is a suffix
```
* Check for presence of substring
```
string='UnixUtils Welcomes you'
if [[ $string = *"Welcomes you"* ]]; then
    echo "substring found"
fi
```
* Convert Case
```
x=pewpew
echo ${x^^} => Upper Case
echo ${x,,} => Lower case
echo ${x,} => Convert first character Lower case
echo ${x^} => Convert first character Upper case
echo ${x^^[p]} => Convert specific character Upper case
echo ${x,,[p]} => Convert specific character Lower case
```
