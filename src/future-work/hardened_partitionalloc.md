## Hardening PartitionAlloc

PartitionAlloc is missing features found in other hardened allocators, so we
decided to add some based on existing work.

### Security Improvements

We make various security-related changes to PartitionAlloc. Many of these are
lifted from Chris Rolf's HardenedPartitionAlloc.

*   Enable canaries for all builds to absorb small overflows
    *   We randomize per-partition canaries with `RandomValue()` and zero the
        leading byte to terminate NUL string operations.
    *   The canary value is checked on free but it isn't the main purpose of
        the canary.
*   Replace `DCHECK` with `CHECK`
*   Zero allocations on free in builds without `EXPENSIVE_DCHECKS` to mitigate
    potential use-after-free and prevent infoleaks.
*   Enable better immediate double-free detection in release builds
*   Randomize freelist entries on allocation

### Landing in MiraclePtr and *Scan

Other security features are coming later as part of upstream work. See
[slides](https://docs.google.com/presentation/d/1QvfZXx5HdUl0IdkBcrx-NM0ua-PVcTi2jNx0Sf-n8Fo/edit).

*   Delayed free
*   Dangling pointer detection

## HardenedPartitionAlloc

Some remaining patches we want to lift from [HardenedPartitionAlloc](https://github.com/struct/HardenedPartitionAlloc/).

*   Freelist is randomized upon creation, seeded with time
*   All freelist pointers are checked for a valid page mask and root inverted self value
*   **Delayed free of all user allocations using a vector stored with the partition root**

## Upstream

It's likely we won't upstream these patches due to the fact that upstream's 
interests aren't necessarily aligned with ours. For instance, zeroing on every 
free incurrs an unacceptable performance penalty and is why they 
probablistically zero on free.