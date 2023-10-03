##2.2. Gossip: The Gossip Protocol

- Concept of gossip: Periodically sending message to random nodes . And after node receivied the message, it will become infected node, and it will start sending message to random nodes during next period.

### Push gossip v.s Pull gossip

- Push: Once you have message, start gossiping about it.

- Pull: Periodically poll a few randomly selected processes for new multicast message which didn't receive.

- Hybrid: Mix both.


While gossip protocols have their merits, they may not be suitable for all multicast scenarios, especially those that require strict ordering, reliability, and guaranteed delivery. Gossip protocols are probabilistic in nature, and there is no guarantee that every node will receive the information, or that they will receive it in the same order. They are best suited for scenarios where eventual consistency or probabilistic guarantees are acceptable, and where the goal is to achieve high scalability and fault tolerance.

Practical applications of gossip protocols include distributed databases (e.g., Cassandra and Riak), peer-to-peer networks, decentralized blockchain networks, and systems that require efficient information dissemination and failure detection.


Information Dissemination: Gossip protocols excel at disseminating information quickly across a large distributed system. In the context of a live streaming service, you can use a gossip protocol to distribute information about the live stream's availability and source to a vast number of viewers. This way, viewers can learn about the stream and connect to it efficiently without the sender having to establish a direct connection with each viewer.

Failure Detection and Healing: Gossip protocols can be used to detect failures in a distributed system and propagate this information to other nodes. In the case of multicast, if one receiver node fails, the gossip protocol can inform other nodes, allowing them to take appropriate actions, such as requesting retransmissions or adapting to the situation.

Consistency and State Synchronization: Gossip protocols can help maintain consistency across distributed databases, caches, or distributed file systems. In scenarios where data or state needs to be synchronized across multiple nodes, gossip protocols can ensure that updates are propagated efficiently.

Epidemic Broadcast: The kind of gossip protocol you described, where nodes randomly select peers to share information, is sometimes referred to as an "epidemic" or "epidemic-style" broadcast. It can be particularly useful for broadcasting information or events in a decentralized or peer-to-peer network. It's not multicast in the traditional sense, but it allows information to spread organically across a network.

