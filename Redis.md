### Redis Cheat Sheet

1. SET
* xx
* nx
* value
* ex

Syntax: Set [keyname] value [keyvalue] {ex} {xx|nx}
xx - insert iff it does exits already
nx - insert iff it does not exists already


1. DEL
2. KEYS
3. MSET
4. MGET
5. EXPIRE
6. TTL
7. INCR
8. DECR
9. INCRBY
10. DECRBY
11. LPUSH
12. RPUSH
13. LLEN
14. RandomKEy
15. rename 
16. renamenx
17. touch
18. unlink
19. type 
20. INCRBYFLoat
21. dump
22. restore
23. expire
24. pexpire
25. persist
26. ttl
27. pttl
28. exists
29. append
30. Decrbyfloat
31. getset 
32. msetnx
33. getrange
End is inclusive in getrange, unlike python.
34. setex : create a key and set its expiry
35. setrange : write and replace substring
36. strlen
37. psetex
38. rpushx : only allows pushing if list exists already
39. lpushx : -- " " --
40. (l/r)pop
41. ltrim
42. lset 
### List
* LPUSH
* RPUSH
* LLEN
* LRANGE 
### Hashes 
* hset
* hget
* hmset
* hgetall
* hmget
* hexists
* hkeys
* hlen
* hsetnx
* hdel
* hincrby
* hincrbyfloat
* hstrlen
* hvals
* 

### Pattern Matching

1. ?
2. *
3. [ae]
4. [^]
5. 

