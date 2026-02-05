---
title: "Log Structured Merge Trees"
date: 2022-09-09T10:00:58+00:00
draft: false
tags: ["data-structures", "databases", "storage"]
---

To continue on the topic of trees from last week, we're going to look at Log Structured Merge (LSM) Trees this time.

Now your first question might be if B-Trees are so great and highly scalable why would you want another tree based data structure?

There's no silver bullet in software engineering. Everything is a trade off, both in life and engineering.

B-Trees solve storage and search problems at the cost of slow writes. It is very difficult to have a mutable write efficient B-Tree based storage engine. You don't see MySQL or PostgresSQL databases used as caches. They can't handle that kind of write throughput. 

Concurrent writes to B-Trees are difficult. Each write or update needs to lock the tree path as you might need to rebalance the tree up to the root.

Also, consider that to update a value you must first locate it, i.e, you have to traverse the tree to find the value. Not exactly a cheap operation, if your application performs a lot of writes.

Most of the problems with B-Trees occur because they are mutable.

LSM Trees solve the problems discussed by being immutable. Before we delve any deeper we need to look at another structure called the Write Ahead Log.

## Write Ahead Log (WAL)

Great another data structure. Don't click away just yet. I am almost certain that you have seen a WAL if you have worked in this industry for a while. 

A Write Ahead Log (WAL) is an append only log file, not unlike an application log. Your backend server logs are a WAL. It keeps appending new lines to the tail of the log file.

WALs aren't limited to application logs. All databases, message queues, and caches use a WAL, it's how they conform to the consistency part of ACID. There is no such thing as a partial transaction state, either the database finishes the entire transaction or it doesn't. All transactions are written to a WAL performing the transaction. If the database crashes in the middle of a transaction, it restarts and reads from the WAL to know where to pick up from or if there are any changes to rollback.

You can create a simple key/value database using a WAL. Append each entry to the end of a log file. If a key already exists you don't care. You append it to the end and worry about duplicates when reading. Writes are a lot faster. You can't get any more efficient.

This is a key/value database using a WAL:

<pre><code>"key1", {"property": "value"}
"key2", {"property": "value2"}
"key3", {"property": "value3"}
"key1", {"property": "value4"}</code></pre>

In the example above, if we need to read the value of `key1`, we will need to find all values of `key1` in the file and use the latest version.

The number of entries for a key keeps growing and every entry for the same key makes increases the expense of a read. To ensure it doesn't grow indefinitely, keys are merged every so often.

If we performed a merge operation on the data above, we'd get:

<pre><code>"key2", {"property": "value2"}
"key3", {"property": "value3"}
"key1", {"property": "value4"}</code></pre>

Now, let's look at LSM trees.

## LSM Trees

LSM Trees have two components, a buffer that is in memory, and the disk table.

All write operations are performed on the buffer. Values in the buffer are mutable. This buffer is called a *memtable.* We won't get into the internals of the memtable for brevity but the keys in here are sorted and can be accessed concurrently.

The disk table is immutable read only memory. Once the memtable is full, the contents are flushed and merged to the disk table. As both the memtable and disk table have sorted data, the merged result is sorted using merge sort.

Let's look at an example:

```
Memtable    Disk Table
k1, v11     k1, v1
k2, v4      k3, v3
k5, v9      k8, v8
k19, v42    k24, v24
```
Memtable is full and Disk Table has some data in it.

The memtable is full triggering a flush and merge operation. The result is:

```
Memtable    Disk Table
            k1, v11
            k2, v4
            k3, v3
            k5, v9
            k8, v8
            k19, v42
            k24, v24
```
Memtable and Disk Table after flush.

This is a simple case where the memtable and disk table are a sorted list. The data structures typically used are trees, they keep the data sorted and have a fast lookup. Immutable B-Trees are used for the disk table, and a mutable one is used for the memtable. The two trees are merged once the memtable is full and flushed to disk.

We don't need writes requiring a read as we append each entry to the memtable. We don't care about existing values, the merging process will take care of duplicates. We also don't need a lock, because there is no rebalancing operation. Making it much more suitable to write heavy workloads, unlike a mutable B-Tree.

Most NoSQL databases like Cassandra or RocksDB use LSM Trees as their storage structure. [Netflix has a blog post](https://netflixtechblog.com/benchmarking-cassandra-scalability-on-aws-over-a-million-writes-per-second-39f45f066c9e) on how their CassandraDB infrastructure was stress tested, and it was able to handle 1.1 million writes a second no problem.

I cannot end this post without mentioning the resources I have used to write it:
- [Database Internals](https://www.amazon.com/Database-Internals-Deep-Distributed-Systems/dp/1492040347) by Alex Petrov
- [Designing Data Intensive Applications](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321) by Martin Kleppmann
- [The original paper on LSM Trees](https://www.cs.umb.edu/~poneil/lsmtree.pdf) by Patrick O'Neil, et al.

*Thanks for reading this newsletter, if you haven't already please consider subscribing or sharing it with a friend.*
