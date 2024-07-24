
<https://www.sqlite.org/lang_transaction.html>

# sqlite之WAL模式

<https://www.cnblogs.com/huahuahu/p/sqlite-zhiWAL-mo-shi.html>

# 死锁问题

老模式问题
<https://github.com/mattn/go-sqlite3/issues/274>

go sql 事务注意事项

<http://go-database-sql.org/modifying.html>

# cgo CFLAGS: -DSQLITE_ENABLE_RTREE -DSQLITE_THREADSAFE=1

sqlite> PRAGMA compile_options;
DISABLE_DIRSYNC
ENABLE_COLUMN_METADATA
ENABLE_FTS3
ENABLE_RTREE
ENABLE_UNLOCK_NOTIFY
SECURE_DELETE
TEMP_STORE=1
THREADSAFE=1
sqlite>

To put it another way, SQLITE_THREADSAFE=1 sets the default threading mode to Serialized

参数配置
<https://www.sqlite.org/compile.html#threadsafe>

# 命令行

<https://www.sqlite.org/cli.html>

# 读未提交

<https://www.sqlite.org/pragma.html#pragma_read_uncommitted>

Query, set, or clear READ UNCOMMITTED isolation.
The default isolation level for SQLite is SERIALIZABLE.
Any process or thread can select READ UNCOMMITTED isolation, but SERIALIZABLE will still be used except between connections that share a common page and schema cache.
Cache sharing is enabled using the sqlite3_enable_shared_cache() API. Cache sharing is disabled by default.

shared-cache mode

从版本3.3.0（2006-01-11）开始，SQLite包括一种特殊的“共享缓存”模式（默认情况下禁用），旨在用于嵌入式服务器。如果启用了共享缓存模式，并且线程建立多个连接到同一个数据库，则这些连接共享单个数据和架构缓存。这可以显着减少系统所需的内存和IO数量。

在版本3.5.0（2007-09-04）中，修改了共享缓存模式，以便相同的高速缓存可以跨整个进程共享，而不仅仅是在单个线程中。在此更改之前，在线程之间传递数据库连接存在限制。这些限制已经在3.5.0更新中取消。本文档描述了版本3.5.0的共享缓存模式。

在某些情况下，共享缓存模式会更改锁定模型的语义。详细信息由本文档描述。假定您对正常SQLite锁定模型有基本理解（有关详细信息，请参见《SQLite Version 3文件锁定和并发性》）。

<https://www.sqlite.org/lockingv3.html>
该文档仅描述了旧版回滚模式事务机制下的锁定方式。新版预写日志或WAL模式下的锁定方式有单独说明。

<https://www.sqlite.org/wal.html>
WAL mode 预写式日志

文件参数

mode参数可以设置为"ro"、"rw"、"rwc"或者"memory". 尝试将其设置为其他任何值都是错误的。如果指定了 "ro", 那么数据库就会以只读方式打开，就像在sqlite3_open_v2()的第三个参数中设置了SQLITE_OPEN_READONLY标志一样。如果将模式选项设置为 "rw", 那么数据库就会以读写（但不创建）访问方式打开，就像已经设置了SQLITE_OPEN_READWRITE（但没有SQLITE_OPEN_CREATE）一样。值“rwc”相当于同时设置 SQLITE_OPEN_READWRITE 和 SQLITE_OPEN_CREATE 两个标志位。

cache: The cache parameter may be set to either "shared" or "private". Setting it to "shared" is equivalent to setting the SQLITE_OPEN_SHAREDCACHE bit in the flags argument passed to sqlite3_open_v2(). Setting the cache parameter to "private" is equivalent to setting the SQLITE_OPEN_PRIVATECACHE bit. If sqlite3_open_v2() is used and the "cache" parameter is present in a URI filename, its value overrides any behavior requested by setting SQLITE_OPEN_PRIVATECACHE or SQLITE_OPEN_SHAREDCACHE flag.

日志记录（旧方式）

在此模式下，SQLite 使用数据库级别的锁定。这是需要理解的关键点。

这意味着每当它需要读取/写入某些内容时，它首先会对整个数据库文件进行加锁。多个读者可以并行存在并同时读取某些内容。

在写入期间，它确保获得独占锁，并且没有其他进程正在同时读取/写入，因此写操作是安全的。

（这被称为多读单写或MSRW锁）

这就是为什么他们说SQlite实现了可串行化事务。

预写式日志或WAL（新方式）

在这种情况下，所有的写操作都会被追加到一个临时文件中（预写式日志），并且该文件会定期地与原始数据库合并。当SQLite正在查找某些内容时，它首先会检查这个临时文件，如果没有找到任何内容，则继续使用主数据库文件。

因此，读者不会与编写者竞争，并且性能比旧方法要好得多。

# FAQ

<https://www.sqlite.org/faq.html#q5>



https://sqlite.net.cn/lang_altertable.html



[SQLITE问题整理
](https://mp.weixin.qq.com/s?__biz=MzkyODU5MTYxMA==&mid=2247494122&idx=1&sn=13374f38699c7e19c2bc2f60fd578a50&chksm=c214d27ff5635b692bb9c8d1f2970cdbb8890f8404fc68d5fca7d094c28626a0fbb7df62fb47&mpshare=1&scene=1&srcid=0722OntklHoaMWqDVWjxgc46&sharer_shareinfo=9b637c9c418870358ca7f8dc097496cb&sharer_shareinfo_first=9b637c9c418870358ca7f8dc097496cb&exportkey=n_ChQIAhIQnZFOvRz53xCPWALHcyIv5BLyAQIE97dBBAEAAAAAAC6BISxy%2B60AAAAOpnltbLcz9gKNyK89dVj0bF2EEgxPV63ut7Tuf%2B70vKjALePLk7Tkf3mztf%2F1KiNlUPqKA4b4YYDH7tvBPvwk86lVDG0GE2HQrt0q4KONleU2KUK6k0JCen8lL1FWfaHzorks%2FgKR2pGcWm0f%2FlZrjY3c47AwTZWkSlYKvBGlliCAOqwdBIdd4%2FW0uBVuUhCPn%2Fygiz0b5gjg6CmmAyja6ULGHmbQltvH32AXWOwZmW20TLU0yOC8sieFKxSeRPkEFMazEPCk4awiK2ENWfcc9gq6plOmNkfCdhfQ&acctmode=0&pass_ticket=JXTPA%2BDox5%2FpqtvQQH2zqHQk147zCjqsCBLVWntvP0%2Fj2Mn%2FqbYkrbCAvpCV7mtC&wx_header=0#rd)