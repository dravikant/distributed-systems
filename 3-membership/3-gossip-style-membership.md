- Protocol
    
    - Periodically gossip their membership list

    - On receipt, the local list membership list is updated 

        --> i.e. my peer has latest seq no heartbeat from a node than what I have.. i can safely update seq no for that node as well.

    - We must label the local time, since this is asynchronous system

    - If the heartbeat has not increased for more than `T_failed` seconds, the member considered as failed.

    - After `T_cleanup` seconds, it will be deleted from the list.

- Typically `T_cleanup` is around the same as the `T_fail`, so here's the question, why do we need two different timeouts?

- Why do we need two different timeouts?
    
    - The entry will never go away
        -> if I delete the entry and my neighbour shares a stale entry I may assume this is a new peer and again add it back making it non removable

    - It's a ping-pong behavior(exactly)


### Discussion

- What happen if gossip period `T_gossip` is decreased?

    - A single heartbeat take O(log(N)) time to propagate

    - That imply that N heartbeats take O(N*log(N)) time to propagate

    - O(log(N)) time to propagate, if the bandwidth allowed per node is allowed to be O(N)

    - O(N*log(N)) time to propagate, if the bandwidth allowed per node is allowed to be only O(1)

    - Conclude two points above, if we had much bandwidth, we will send the gossip much quicker.

    - **Tradeoff: False positive rate v.s detection time v.s bandwidth**

- What happen to `P_mistake`, as `T_fail`, `T_cleanup` is increased?

> False positive rate: Type I error.