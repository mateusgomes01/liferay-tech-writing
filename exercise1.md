# Wordsmithing

“2010's benchmark and optimization is reaching it's end, now it is time to write something about what we did in the last few months.

Today we'll talk about an EE-only feature: a new ehcache cluster replication mechanism. Since this feature is only available in the EE version of the portal, we won't talk about implementation details too much. Just some general concepts about what the problem is and how we fixed it.

Ehcache supports cluster, by default it uses a RMI replication mechanism, which is a point to point communication graph. As you can imagine, this kind of structure can not scale for large clusters with many nodes. The reason is that each node has to send out N-1 of the same event to other nodes. When N gets too big, it becomes a network traffic disaster.

To make things even worse, ehcache creates a replication thread for each cache entity. In a large system like Liferay Portal, it's quite easy to have more than 100 cache entities, that is, more than 100 cache replication threads. Because they take lots of resources, like memory and cpu power, threads can be quite expensive. Despite that, these threads are most likely in a sleeping state more than 99% of the time, since they only start working when a cache entity needs to talk to remote peers. Disregarding thread heap memory (Because it's application depended), we will only consider the stack memory footprint of these 100+ threads. By default, on most platforms, the thread stack size is about 2MB, that means 200+ MegaBytes. If you include the heap memory size, this number may reach even the 500MB just for one node! Even though memory chips are cheap nowadays, we shouldn't waste them! Also, massive threads can frequently cause context switch overhead.

We need to fix both the 1 to N-1 network communication problem and the massive threads bottleneck. Liferay Portal has a facility called ClusterLink, which is basicly an abstract communication channel in which the default implementation uses JGroups' UDP multicast to communicate.

By using ClusterLink we can fix the 1 to N-1 network communication problem easily.

To reduce the number of replication threads, we provide a small group of dispatching threads. They are dedicated for delivering cache cluster events to remote peers. Since all cache entity cluster events will go through one place to the network, this gives us a chance to coalesce. If two changes to the same cache object are close enough, we only need to notify remote peers once to save some network traffic. (ehcache most recent version supports JGroups replicator and fixes 1 to N-1 network communication, but it cann't fix the massive threads problem and cann't coalesce.)

For EE customers who are interested in this feature, contact our support engineers for more detail.”
