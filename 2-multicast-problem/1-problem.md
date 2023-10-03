### problem

 the multicast problem refers to the challenge of efficiently and reliably delivering a message or data packet from one sender to multiple receivers. Unlike unicast, which involves sending a message from one sender to one receiver, or broadcast, which involves sending a message from one sender to all possible receivers, multicast aims to send a message from one sender to a specific group of receivers.

The multicast problem can be challenging due to several reasons:

Scalability: Ensuring efficient and reliable multicast becomes increasingly complex as the number of receivers or members in the multicast group grows. Systems must handle the dynamic nature of groups that can have members join or leave at any time.

Reliability: In a multicast, it is essential that all intended receivers receive the message. This means dealing with issues such as network failures, packet loss, or receiver failures without compromising reliability.

Ordering: Maintaining the order of messages across multiple receivers can be complex, especially when receivers might receive messages at different times or experience network delays.

Congestion: Multicast can lead to network congestion if not managed properly, as sending a message to a large group can put a significant load on the network.


### Example

Imagine you have a live streaming service hosted in a cloud environment, and you want to broadcast a live sports event to thousands of viewers who have subscribed to watch it. This scenario involves a multicast-like requirement: one sender (the live stream source) needs to distribute the live video feed to multiple receivers (the viewers) simultaneously.

Here's how the multicast problem manifests in this example:

Efficiency: If you were to use unicast (TCP or UDP) to send the live stream to each viewer individually, you'd need to create a separate connection for each viewer. This can quickly overwhelm both the sender's resources and the network's capacity, leading to inefficiency.

Reliability: While TCP provides reliability for point-to-point communication, it does not natively support multicast. In a multicast scenario, ensuring that every viewer receives the entire live stream without errors or missing parts can be challenging. Network issues, such as packet loss or congestion, could disrupt the delivery to some viewers.

Scalability: Multicast groups can range from a few receivers to thousands or more. Managing a large multicast group dynamically, allowing viewers to join or leave the stream, while maintaining efficient delivery, is a scalability challenge.

Ordering: Ensuring that all viewers receive the video frames in the correct order is vital for maintaining the quality of the live stream. In a multicast scenario, different viewers might experience varying network latencies, making it challenging to maintain strict ordering.

Congestion: When a large number of viewers simultaneously join a live stream, it can cause network congestion, potentially leading to packet loss and degraded quality for all viewers.

To address these challenges in a practical example like live streaming, specialized multicast protocols or distribution mechanisms may be employed. These mechanisms often involve a combination of network-level multicast support, error correction techniques, and congestion control algorithms. Additionally, content delivery networks (CDNs) and cloud providers may offer solutions tailored to efficient multicast-like content distribution to alleviate these problems in a cloud computing context.


### Requirement

- Fault tolerance and scalability
    
    - Because the nodes may crash

    - Packet may be dropped

    - Thousands of nodes.

- Most in the application level.


### Implementation

#### 1. Centeralized

- It's the simplest implementation.

- Put receipients in the for or while loop, go though the group member and send the TCP or UDP packets

- Problems:
    
    - Fault tolerance

    - Latency, since the sender has to go through sequentially

    - Time complexity: `O(n)`(Suppose we have n nodes.)

#### 2. Tree-based

- If you build a balanced(or almost balanced) tree, the height of a n-nodes tree is log(n) => That means the time complexity to reach each node is `O(log(n))`. 

- Problems:
    
    - Needs to maintain the tree
        - nodes may come and go randomly   

- Solutions:

    - Build a spanning tree among the process of multicast group.

        - each node receives one msg and forwards its copy to all child nodes

    - Use spanning tree to disemminate multicast

        -   if node closer to root fails most of the tree is unreachable

    - Use acknowledgements(ACKs) or negative acknowledgements(NAKs) to repair the nodes which do not receive message.
    
        - Issues: ACKs and NAKs might implode. For instance if the multicast wasn't sent successfully at the initial.

        - SRM (Scalable Reliable Multicast): 
            
            - Use NAKs with ramdom wait times. 

            - If the receiver need to send NAKs multiple time it should use exponential backoff to avoid NAK storms

        - RMTP (Reliable Multicast Transport Protocol):

             - Use ACKs 

             - Only send to deignated receiver.

             - ACKs contain digest of msg received so far and receiver can resend missing msg if required

- Conclustion:

    - Both SRM and RMTP have the message implossion problem, so that's why we develop gossip based and epidemic based protocol.




