# PartitionAlloc

PartitionAlloc is the memory allocator used in most of Chrome and is an allocator optimized for speed,
allocation latency, and security. It provides various defenses against memory corruption, specifically
its heap isolation from which its name is derived. The central design revolves around partitions,
separate heaps that can be used to contain certain types, sizes, or lifetimes; partitioning objects by
type is used throughout the browser as a defense against some forms of type confusion. Each partition
holds multiple buckets of similarly sized objects, preventing some forms of type confusion between
objects of different sizes.

Apart from the heap isolation, PartitionAlloc features some additional defenses
against memory corruption.

*   Allocations are zeroed either due to being a fresh page from the operating
    system or being (probabilistically) zeroed on free
*   Verification of zero filling at initialization to detect write-after-free

Although PartitionAlloc already makes it harder to exploit heap corruption,
We're going to be expanding the protections PartitionAlloc offers using patches
from Chris Rolf's
[HardenedPartitionAlloc](https://github.com/struct/HardenedPartitionAlloc);
they are listed below.

### Improvements

*   Randomization of the freelist order (inspired by Linux) on each allocation
    to make it harder to predict and exploit heap overflow
*   Randomized trailing cookie zeroing the leading byte to terminate C string
    overflows and absorb other small overflows
*   Replacement of `DCHECK`s with `CHECK`s to induce crashes instead of
    exposing the user to potential vulnerabilities
*   Consistent zero-based or pattern-based sanitization on free depending on
    build setup to get sensitive data out of the process as soon as possible
    and mitigate some forms of use-after-free
*   Enablement of various security features that were deemed too expensive for
    release builds

### Freelist randomization

We plan to randomize freelist entries on creation/allocation to reduce the
stability of exploits relying on the determinism of the allocator. It's not
going to be a particularly strong mitigation and we would rather use an
allocator with fully out-of-line metadata such as OpenBSD's malloc or
GrapheneOS' hardened_malloc.

### Freelist pointer obfuscation

Currently, the freelist pointer is protected from partial overwrites by way of
storing them in big endian format on little endian architectures and as a
bitwise complement on big endian architectures, preventing partial pointer
overwrites. An attacker with the ability to overwrite the freelist pointer can
trivially bswap. We're planning to expand this as a probabilistic mitigation to
cover complete overwrites based on my understanding of the Linux implementation.

### Cookies

// TODO
