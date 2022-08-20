```
        ┌────────────────────────────────────────────────────────────────────┐
        │    ____                                                            │
        │   |  _ \ __ _ _ __ ___                                             │
        │   | |_) / _` | '_ ` _ \                                            │
        │   |  _ < (_| | | | | | |                                           │
        │   |_| \_\__,_|_| |_| |_|                                           │
        │                                                                    │
        │                _   _           _          _   _                    │
        │     ___  _ __ | |_(_)_ __ ___ (_)______ _| |_(_) ___  _ __  ___    │
        │    / _ \| '_ \| __| | '_ ` _ \| |_  / _` | __| |/ _ \| '_ \/ __|   │
        │   | (_) | |_) | |_| | | | | | | |/ / (_| | |_| | (_) | | | \__ \   │
        │    \___/| .__/ \__|_|_| |_| |_|_/___\__,_|\__|_|\___/|_| |_|___/   │
        │         |_|                                                        │
        └────────────────────────────────────────────────────────────────────┘
            
```

Most of the inmemeory DB utilize ram, meaning optimizing ram utilizations is probably going to decide a lot on what actual behaviour and how things would work. 
It also decides on how each of the things algorithmically going to affect the performance. 
(source: https://discuss.aerospike.com/t/how-to-tune-the-linux-kernel-for-memory-performance/4195)
1. In memory caches

Linux  kernel optimizes unused ram by filling it up with caches, this way we ensure that no ram is an unused ram. Overtime kernel fills the ram wit5h caches, as more memory is required by applications and buffers, the kernel goes through the cache memory pages and finds a block large enough to fit the requested malloc, it then frees the memory and allocates it to calling application.

this can improve the performance as deallocation is costly process in comparison to accessing unused memory. Higher latency could be henceforth observed. 

The kernel memory cache contains the following:

* dirty cache - Data blocks not yet committed to the file systems which support caching (e.g. ext4). This can be emptied by issuing the sync command athough this may imply a periodic performance penalty. This is not advised for normal usage unless it is extremely important to commit data to hard drive (for example when expecting a failure).
* clean cache - Data blocks which are on the hard drive but are also retained in memory for fast access. Dropping the clean cache can result in a performance deficit as all data will read from disk, whereas beforehand, the frequently used data would be fetched directly from RAM.
* inode cache - Cache of the inode location information. This can be dropped as with clean cache but with the attendant performance penalty.
* slab cache - This type of cache stores objects allocated via malloc by applications so that they may be re-malloc again in the future with object data already populated, resulting in speed gain during memory allocations.
            
While not much can be done with dirty cache, the other cached objects can be cleared. This has potentially 2 outcomes. Latency in high-malloc applications, such as Aerospike when storing data in memory, will be reduced. On the other hand, disk access may slow down, as all data will have to be read from disk.

Clearing slab cache on a server can potentially introduce a temporary speed penalty (spike). For this reason, it is not advised to clear caches. Instead, it is preferred to inform the system that a certain amount of RAM should never be occupied by cache.


```
# clear page cache (above type 2 and 3)
$ echo 1 > /proc/sys/vm/drop_caches

# clear slab cache (above type 4)
$ echo 2 > /proc/sys/vm/drop_caches

# clear page and slab cache (types 2,3,4)
$ echo 3 > /proc/sys/vm/drop_caches
```



