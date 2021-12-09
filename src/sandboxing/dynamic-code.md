# Dynamic Code Generation

Hexavalent will be able to use existing mitigations to prevent the introduction
of new executable code into a process's address space. Microsoft provides their
Arbitrary Code Guard on Windows and the dynamic code policy is turned on in
various processes that don't generate dynamic code such as the audio process;
it's also going to be turned on in the renderer process when V8 is running
jitless.

On Linux, We're going to be using the existing `seccomp` sandbox to prevent the
introduction of new executable code on Linux by restricting the
`mmap`/`mprotect` interfaces from PaX MPROTECT. It's currently limited to the
same processes that enable ACG on Windows and we're hoping to upstream this work
in the future for the benefit of other Chromium-based browsers.

The restrictions presently prevent
*   changing the executable status of memory pages not originally created as
    executable
*   creating executable pages from anonymous memory
*   creating writable/executable file mappings

It could potentially be expanded in the future but is currently considered fine
as-is.

There isn't any way to dynamically enforce the dynamic code policy on macOS;
Apple provides the `com.apple.security.cs.allow-jit` entitlement to allow the
usage of the `MAP_JIT` flag but it's not something we're going to be utilizing
as it would require us to produce twice the amount of binaries.

We'd like to thank madaidan for his hand in the development of these patches.
