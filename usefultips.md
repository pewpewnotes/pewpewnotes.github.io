# Binary Reversing tips


» pewpew: hellows, I was doign this one https://exploit-exercises.lains.space/protostar/stack1/, its pretty easy but i was thinking if my thought process is correct or
» not. Like once I looked at the code i knew that strcpy without checking the strlen will lead to overwrite of next memory place. and went ahead with "random 64
» characters"+dcba. So my doubt is that is it possible to know for sure
» that modified is after the buffer and i am not modifying some other variable unknowingly? if not then is trial and error all that we do?
» Aeres: you can check where the vars are on the stack in the disassembly, e.g. using objdump or gdb
» in general, the compiler will put the vars on the stack in inverse order of declaration, meaning the last vars are highest on the stack
» pewpew2: objdump gives too much of information, how can i parse it for more info about vars? also, if last are highest on stack meaning I am filling stack from bottom to
» up! nice that makes sense
» run objdump -d and look at main. you will see that modified sits at -0x4(%ebp) for example, meaning the first declared / lowest on the stack. the buf will be at
» -0x64(%ebp)
» it takes a bit of practise, but local variables are usually referenced from ebp
» sometimes esp
» depends on compiler options
» but yeah, the level would be more tricky if the order of declaration was reversed and buf was declared before modified
» i see pewpew2 :D thanks a lot. this helped.
» sure, np :)

