## ConcurrentHashMap & Hashtable

1, HashTable

跟HashMap相比Hashtable是线程安全的，适合在多线程的情况下使用，但是效率可不太乐观。

Hashtable 是不允许键或值为 null 的，HashMap 的键值则都可以为 null
因为Hashtable使用的是安全失败机制（fail-safe），这种机制会使你此次读到的数据不一定是最新的数据。
如果你使用null值，就会使得其无法判断对应的key是不存在还是为空，因为你无法再调用一次contain(key）来对key是否存在进行判断，ConcurrentHashMap同理。

2, ConcurrentHashMap

>结构

分段锁，每当一个线程占用锁访问一个 Segment 时，不会影响到其他的 Segment

>1.8的优化

抛弃了原有的Segment 分段锁，而采用了 CAS + synchronized 来保证并发安全性。
1.8 在 1.7 的数据结构上做了大的改动，采用红黑树之后可以保证查询效率（O(logn)），甚至取消了 ReentrantLock 改为了 synchronized，这样可以看出在新版的 JDK 中对 synchronized 优化是很到位的


