### Stackfour 

This one was again a lot more difficult for me, I didnt knew how to find the buffer size.
I set out to find it manually and figured it was somewhere between 90-81 but I was not sure.
I had to look it up to see how to check it, it was simple
1. Gdb
2. breakpoint before and after gets
3. after gets, info frame
4. Find the memory locations and perform subtractions

Our code really remains the same, and it just works. 


### Creds
```
None
```

### Logs
```


## --- Successful attempt ---
gef➤  info frame
Stack level 0, frame at 0x7fffffffe360:
 rip = 0x400649 in start_level; saved rip = 0x40068d
 called by frame at 0x7fffffffe380
 Arglist at 0x7fffffffe350, args: 
 Locals at 0x7fffffffe350, Previous frame's sp is 0x7fffffffe360
 Saved registers:
  rbp at 0x7fffffffe350, rip at 0x7fffffffe358
gef➤  quit


```

 ~Kurama
