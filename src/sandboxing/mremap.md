# mremap

We're planning to remove `mremap` from the syscall whitelist as part of reducing
kernel attack surface. The practicality of this patch is going to be limited to
allocators that don't use `mremap` to `realloc` memory such as PartitionAlloc.
It comes from Daniel Micay's old chromium_patches and is relevant to the desktop
platforms we're targeting, although it may not work with a different malloc
implementation.
