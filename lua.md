# Lua short notes and stuffs

1. Friendly syntax :D
2. no semicolons yayayay and also no fusses over whitespaces

```
print "no time for love"
-- same as
print 
"no time for love"
```

```
stdin:1: unexpected symbol near '1989'
Interesting. Lua doesn’t print the value by default. We can deal with that
easily enough. You could print() or return the value explicitly, or just add an = ,
like this:
> print(1989)
1989
> return 1989
1989
> =1989
1989
```
Strings can be enclosed in ' ' or " "
concatenation happens using .. operator

and ofcourse, \t,\n and stuffs work

Length of string can be found using # 
```
=#'pewpew'
6
```

nil is default value for any variable that does not exists.

```
=alphabetagammapewpewdoesnotexist
nil
```
exponents ^ and modulo operations %
```
Instead of Boolean operators, Lua uses the and , or , and not keywords. Conve-
niently, logical expressions short-circuit, meaning that Lua evaluates both
halves of an expression only if it needs to.
> =not ((true or false) and false)
true
> =true or spill_antidote()
true
(No antidotes were spilled in the running of this code.)
You can compare any values for equality and inequality with == and ~= ,
```


```
Functions
Lua function definitions look like those in any common scripting language:
> function triple(num)
>>
return 3 * num
>> end
>
> =triple(2)
6
Strictly speaking, the function name isn’t necessary; you could just as easily


```
One liners are also possible

```
=(function(num) return 3 * num end)(2)
```
In Lua, functions are first-class values; they can be treated just like any other
value in Lua. In particular, they can be assigned to variables, passed as
parameters into other functions, and stored in data structures.
For example, you could easily write a function call_twice() that takes a second
function f() and returns a third function ff that calls f twice:
>
> function call_twice(f)
>>
ff = function(num)
>>
return f(f(num))
>>
end
>>
return ff
>> end
>
> function triple(n)
>>
return n * 3
>> end
>
> times_nine = call_twice(triple)
>
> =times_nine(5)
45

Unlike other languages, in case of additional arguments, lua assigns nil to them. 

> function print_chars(friend,foe)
>> print(*friend and for*)
>> print(friend)
>> print(foe)
>> end
> print_characters('Marcus', 'Belloq')
*Friend and foe*
Marcus
Belloq
> print_characters('Marcus')
*Friend and foe*
Marcus
nil
Any extra parameters are just ignored:
> print_characters('Marcus', 'Belloq', 'unused)
Belloq', 'unused')


You can also explicitly create variadic functions, that is, functions with an
arbitrary number of inputs. You do so by making the last parameter in the
function declaration an ellipsis ( ... ):
> function print_characters(friend, ...)
>>
print('*Friend*')
>>
print(friend)
>>
>>
print('*Foes*')
>>
foes = {...}
>>
print(foes[1])
>>
print(foes[2])
>> end
>
> print_characters('Marcus', 'Belloq')
*Friend*
Marcus
*Foes*
Belloq
nil

function weapons()
  return 'bullwhip','revolver'
end

w1 = weapons()


w1 -> bullwhip

w1,w2 = weapons() 

w1->bullwhip
w2->revolver

### :keyword syntax:

function popcorn_prices(table)
    print('A medium costs '.. table.medium)
end

popcorn_prices{
        small=5.00,
        medium=7.00,
        jumbo=15.00}

a medium costs 7.00

### Control Flow

film = 'skull'

if film=='raiders' then
    print("good")

elseif film == 'temple' then 
    print('meh')

else
    print("huh?")
end

for i=1, 5 do
  print(i)
end

or 

for i=1,5,2 do
  print(i)
end

while math.random(100)<50 do
  print('Tails; flipping again')
end


One quirk of Lua is that variables are global by default:
> function hypotenuse(a, b)
>>
a2 = a * a
>>
b2 = b * b
>>
return math.sqrt(a2 + b2)
>> end
>
> =hypotenuse(3, 4)
5
> =a2
9 -- WHOOPS!
You’d probably prefer that our temporary a2 variable not leak outside the
function. Fortunately, all we have to do is preface our local variable definitions
with the local keyword:
> function hypotenuse(a, b)
>>
local a2 = a * a
>>
local b2 = b * b
>>
return math.sqrt(a2 + b2)
>> end
I was initially surprised that local isn’t the default in Lua. But it turns out that


