# Wordsmithing

“2010's benchmark and optimization is reaching the end, it is time to write something about what we did in last few months.

Today we will talk about an EE-only feature, a new ehcache cluster replication mechanism. Since this is only available in EE version portal, i won't talk about impl detail too much. Just some general concepts about what is the problem and how we fix it.

Ehcache supports cluster, by default it uses RMI replication mechanism, which is a point to point communication graph. As you can guess this kind of structure can not scale for large cluster with many nodes. Because each node has to send out N-1 same event to other nodes, when N is too big, this will become a network traffic disaster.

To make things even more worse, ehcache creates a replication thread for each cache entity. In a large system like Liferay Portal, it is very easy to have more than 100 cache entities, this means 100+ cache replication threads. Threads are expensive, because they take resource(memory and cpu power). But these threads are most likely sleeping over 99% time, since they only start to work when a cache entity needs to talk to remote peers. Without regard to thread heap memory(Because this is application depended), just consider stack memory footprint of that 100+ threads. By default on most platform, the thread stack size is 2MB, that means 200+MB. If you include the heap memory size, this number may even reach 500MB(This is just for one node!). Even memory chips are cheap today, we still should not waste them! And massive threads can also cause frequent context switch overhead.

We need to fix both the 1 to N-1 network communication and massive threads bottleneck.Liferay Portal has a facility called

ClusterLink which is basicly an abstract communication channel, and the default impl is using JGroups' UDP multicast to communicate.

By using ClusterLink we can fix the 1 to N-1 network communication easily.

To reduce the replication thread number, we provide a small group of dispatching threads. The are dedicated fory delivering cache cluster event to remote peers. Since all cache enities' cluster event will go through one place to network, this gives us a chance to do coalesce, if two modification to the same cache object are close enough, we only need to notify remote peers once to save some network traffic.(Newer version ehcache supports JGroups replicator, it can also fix the 1 to N-1 network communication, itbut cannot fix the massive threads problem and cannot do coalesce.)

For EE customer who is in interested in this feature, you can contact our support engineers for more detail info.”
