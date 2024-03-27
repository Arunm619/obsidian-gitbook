
#### Simple hashing


Problems of simple hashing function `key % n` (`n` is the number of servers):
- It is not horizontally scalable. Whenever a new cache host is added to the system, all existing mappings are broken.
- It may not be load balanced, especially for non-uniformly distributed data. Some servers will become hot spots.

#### Consistent Hashing

- Consistent hashing maps a key to an integer.
- Imagine that the integers in the range are placed on a ring such that the values are wrapped around.
- Given a list of servers, hash them to integers in the range.
- To map a key to a server:
  - Hash it to a single integer.
  - Move clockwise on the ring until finding the first cache it encounters.
- When the hash table is resized (a server is added or deleted), only `k/n` keys need to be remapped (`k` is the total number of keys, and `n` is the total number of servers).
- To handle hot spots, add “virtual replicas” for caches.
  - Instead of mapping each cache to a single point on the ring, map it to multiple points on the ring (replicas). This way, each cache is associated with multiple portions of the ring.
  - If the hash function is “mixes well,” as the number of replicas increases, the keys will be more balanced.


----


Consistent hashing is a special kind of hashing technique that is primarily used in distributed systems to achieve better load distribution among multiple nodes (like servers). It minimizes the reorganization of keys when nodes are added or removed, thus reducing the need for data movement and providing better performance and scalability.

In traditional hashing, when the hash table is resized (i.e., when nodes are added or removed), most keys will hash to a new location, leading to a potential massive relocation of data. In contrast, consistent hashing ensures that when a node is added or removed, only a minimal number of keys are remapped to different nodes.

Here's how it works:

1. Imagine a circle (often called a "ring") where each point on the circle corresponds to a hash value. The range of hash values is the same as the output range of the hash function used.

2. Each node (server) in the system is assigned a hash value by hashing its identifier. This determines its position on the edge of the circle.

3. To find where a given key should be stored, you hash the key, which gives you a position on the edge of the circle. You then move around the circle until you find a node. The key is stored on that node.

4. When a node is added, it takes over some of the keys from its neighbors. When a node is removed, its keys are taken over by its neighbors. In both cases, all other nodes are unaffected.

Consistent hashing is used in many distributed systems, including distributed caches, distributed file systems, and more. It's also used in some load balancing schemes.



[What is CONSISTENT HASHING and Where is it used? - YouTube](https://www.youtube.com/watch?v=zaRkONvyGr8&ab_channel=GauravSen)


Solution: K hash functions for rendering virtual servers.


the best solution is not to use K hash functions, but to generate K replica ids for each server id. Designing K hash functions while maintaining random uniformity and consistency is hard. Generating K replica ids is easy: xxx gives K replicas xxx + '1', xxx + '2', ..., xxx + 'K'. Then you take these replicas and generate K points on the ring with the same hash function and this is what is actually used in practice. Chord algorithm is just an example of this technique to add K replicas for each server id