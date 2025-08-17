---
title: RWMutexes
date: 2025-08-16 18:41:17
tags: c++, programming
---

Typically when you have a critical section you protect it with a mutex, and
that's fine in most cases. But imagine a situation where you have a bunch of
readers and only one writer, the mutex blocks the shared resource regardless of
who is actually writing/reading it. This means that readers have to wait for
each other to access the same resource, and this doesn't make sense for
performance reasons. It's okay if readers overlap for example, when the shared
object is not being modified.

## Definition
- RW Locks segment the definition of the mutex such that you can take it as a
  reader or you can take it as a writer.
- If you take it as a reader, only writers are not allowed to access the shared
  resource
- If you take it as a writer, only readers are not able to access the shared
  resource
In the example above, this improves the concurrent performance overall for the
read-heavy workload because it erases starvation.


