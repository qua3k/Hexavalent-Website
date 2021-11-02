# Heap Allocator Hardening

Currently, Chrome (and Hexavalent) use the upstream provided *ParitionAlloc*,
a memory allocator optimized for space efficiency, allocation latency, and
security.

The PartitionAlloc authors guarantee some security properties:

*   Different partitions exist in different regions of the process's address
    space. When the caller has freed all objects contained in a page in a
    partition, PartitionAlloc returns the physical memory to the operating
    system, but continues to reserve the region of address space.
    PartitionAlloc will only reuse an address space region for the same
    partition.
*   One page can contain only objects from the same bucket. When freed,
    PartitionAlloc returns the physical memory, but continues to reserve the
    region for this very bucket.
*   Linear overflows cannot corrupt into, out of, or between partitions.
*   Linear overflows/underflows cannot corrupt the allocation metadata.
    PartitionAlloc records metadata in a dedicated, out-of-line region (not
    adjacent to objects), surrounded by guard pages. (Freelist pointers are an
    exception.)
*   Partial pointer overwrite of freelist pointer should fault.
*   Direct map allocations have guard pages at the beginning and the end.

Currently, partitions are used to separate certain object types, but this
can easily be extended.

## Hardening PartitionAlloc

Our general progress for hardening PartitionAlloc is being tracked
[on the issue tracker](https://github.com/Hexavalent-Browser/Hexavalent/issues/54)
and [here](./hardened_partitionalloc.md).

## Future Work

We are looking into different allocators, such as GrapheneOS's
[hardened_malloc](https://github.com/GrapheneOS/hardened_malloc), or Chris
Rolf's [isoalloc](https://github.com/struct/isoalloc), which offer additional
security properties such as reserving address space for the mutable allocator
state/metadata, among others.

## See also

*   [https://github.com/GrapheneOS/hardened_malloc#security-properties](https://github.com/GrapheneOS/hardened_malloc#security-properties)
*   [https://github.com/struct/isoalloc/blob/master/SECURITY_COMPARISON.MD](https://github.com/struct/isoalloc/blob/master/SECURITY_COMPARISON.MD)
