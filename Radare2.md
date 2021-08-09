### Radare2

#### Commands for radare2, a framework for reverse engineering and binary analysis

###### Survival Guide

| `aa`                      | Auto analyze              |
| ------------------------- | ------------------------- |
| `pdf@fcn[Tab]`            | Disassemble function      |
| `f fcn[Tab]`              | List functions            |
| `f str[Tab]`              | List strings              |
| `fr <flagname> <newname>` | Rename flag               |
| `psz <offset>`            | Print string              |
| `arf <flag>`              | Find cross ref for a flag |

###### Flagspaces

| `fs`            | Display flagspaces    |
| --------------- | --------------------- |
| `fs *`          | Select all flagspaces |
| `fs <sections>` | Select one flagspace  |

###### Flags

| `f`               | List flags            |
| ----------------- | --------------------- |
| `fj`              | Display flags in json |
| `fl`              | Show flag length      |
| `fx`              | Show hexdump of flag  |
| `fC <name> <cmt>` | Set flag comment      |

###### Info

| `ii` | Info on imports     |
| ---- | ------------------- |
| `iI` | Info on binary      |
| `ie` | Display entrypoint  |
| `iS` | Display sections    |
| `ir` | Display relocations |

###### Print String

| `psz <offset>` | Print string                   |
| -------------- | ------------------------------ |
| `psb <offset>` | Print strings in current block |
| `psx <offset>` | Show string with scaped chars  |
| `psp <offset>` | Print pascal string            |
| `psw <offset>` | Print wide string              |

###### Visual Mode

| `V`       | Enter visual mode                             |
| --------- | --------------------------------------------- |
| `(p / P)` | Rotate modes (hex, disasm, debug, words, buf) |
| `c`       | Toggle (c)ursor                               |
| `q`       | Back to radare shell                          |
| `hjkl`    | Move around (left-down-up-right)              |
| `[Enter]` | Follow address of jump/call                   |
| `sS`      | Step / step over                              |
| `[Enter]` | Follow address of jump/call                   |
| `o`       | Go/seek to given offset                       |
| `.`       | Seek to program counter                       |
| `/`       | In cursor mode search in current block        |
| `:cmd`    | Run radare command                            |
| `;[-]cmt` | Add/remove comment                            |
| `/*+-[]`  | Change block size, [] = resize hex.cols       |
| `>\|<`    | Seek aligned to block size                    |
| `i`       | Insert code                                   |
| `a`       | Assemble code                                 |
| `A`       | Visual Assembler                              |
| `b`       | Toggle breakpoint                             |
| `B`       | Automatic block size                          |
| `d[f?]`   | Define function, data, code, ...              |
| `D`       | Enter visual diff mode (set diff.from/to)     |
| `e`       | Edit eval configuration variables             |
| `f/F`     | Set/unset flag                                |
| `gG`      | Go seek to begin and end of file (0-$s)       |
| `mK/’K`   | Mark/go to Key (any key)                      |
| `M`       | Walk the mounted filesystems                  |
| `n/N`     | Seek next/prev function/flag/hit (scr.nkey)   |
| `C`       | Toggle (C)olors                               |
| `R`       | Randomize color palette (ecr)                 |
| `t`       | Track flags (browse symbols, functions..)     |
| `T`       | Browse anal info and comments                 |
| `v`       | Visual code analysis menu                     |
| `V`       | View graph (agv?)                             |
| `W`       | Open WebUI                                    |
| `uU`      | Undo/redo seek                                |
| `x`       | Show xrefs to seek between them               |
| `yY`      | Copy and paste selection                      |
| `z`       | Toggle zoom mode                              |
