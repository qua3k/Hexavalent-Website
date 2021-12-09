# Heap Allocator

PartitionAlloc already provides substantial defenses against heap corruption
such as partitioning objects by type and size.

We're going to be investing in improving PartitionAlloc to make it more
resistant against heap corruption. It's still a traditional allocator design
with inline metadata rendering it very vulnerable to overwrites/corruption. It
would be much better to use the OpenBSD malloc or the GrapheneOS
hardened_malloc design as a starting point for a hardened allocator.

There are still improvements we can make to what we currently have such as employing
probabilistic pointer obfuscation by XORing the pointer with the pointer address
and a random canary to protect it from overwrites instead of the weak
obfuscation performed now. It's very likely we'll switch to a more secure
allocator in the future based on the aforementioned designs to avoid relying on
probabilistic mitigations to protect inline metadata.
