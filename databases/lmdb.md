### LMDB

- [LMDB Main Page](http://symas.com/mdb/)

Couple key features

1. full acid with MVCC
1. multi-thread / multi-process concurrency
1. optimized for read
1. readers don't lock and don't block writes.
1. readers don't allocate memory (mmap'd directly so zero-copy)
1. only 1 writers allowed
1. no compaction / garbage collection ==> relatively deterministic latency (no spikes)

Useful Videos:

- [Howard Chu's InfoQ Video](http://www.infoq.com/presentations/lmdb-lighting-memory-mapped-database)

