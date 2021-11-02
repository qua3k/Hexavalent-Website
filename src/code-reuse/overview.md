# Code Reuse Attacks

## History

Since the introduction of PaX in 2000, the PaX team have single-handedly
created defenses that serve to make traditional shellcode injection into a
process's address space impossible through a combination of
`mmap()`/`mprotect()` restrictions and NOEXEC.

However, after the widespread adoption of said mitigations by the industry,
they quickly realized that it was possible to hijack the control flow and
induce arbitrary behavior using only existing instructions in memory, e.g.,
[ret2libc](https://seclists.org/bugtraq/1997/Aug/63).

In response to these attacks, the PaX team created
[ASLR](https://pax.grsecurity.net/docs/aslr.txt) in 2003, describing it as an
"inexpensive and probabilistic defense against these kinds of attacks".

Nevertheless, they acknowledged that ASLR was susceptible to info leaks and
continued to investigate alternative mitigations, resulting in their Reuse
Attack Protector (RAP), consisting of two parts, the CFI implementation
protecting both forward (indirect function calls/jumps) and
backward-edges (return addresses) and their probabilistic return address
protection.

The threat model for RAP assumes an attacker with arbitrary read/write access,
rendering mitigations such as ASLR and stack cookies completely useless.
[The RAP FAQ covers it in more detail](https://grsecurity.net/rap_faq).

## Control-Flow Hijacking, But In Detail

There have literally been papers written about the subject, so I try to keep
it short.

// TODO

## Hybrid Attacks

Most real-world exploits often take advantage of the fact that many W ⊕ X
implementations are incomplete, i.e., they prevent W + X mappings but allow W →
X transitions, allowing attackers to use ROP to mark a portion of the memory
area as executable and transfer control to a payload instead of requiring the
attacker to write the whole payload as ROP. It's especially apparent in JIT
engines as they must be able to generate dynamic code, meaning there must be an
exception in the policy for browser JIT engines; Hexavalent takes advantage of
upstream's hardening work and enables mitigations such as Microsoft's Arbitrary
Code Guard (ACG) and CET Shadow Stacks (cetcompat) in the renderer process
when JIT compilation is disabled either via command-line switch or via
`chrome://flags`. We're also looking into modifying the seccomp policy to 
achieve a similar effect on Linux.

## See also

*   [https://pax.grsecurity.net/docs/pax-future.txt](https://pax.grsecurity.net/docs/pax-future.txt)
*   [https://pax.grsecurity.net/docs/PaXTeam-H2HC15-RAP-RIP-ROP.pdf](https://pax.grsecurity.net/docs/PaXTeam-H2HC15-RAP-RIP-ROP.pdf)
*   [https://pax.grsecurity.net/docs/pax.txt](https://pax.grsecurity.net/docs/pax.txt)
*   [https://ieeexplore.ieee.org/abstract/document/8835389/](https://ieeexplore.ieee.org/abstract/document/8835389/)
*   [https://dl.acm.org/doi/abs/10.1145/2714576.2714635](https://dl.acm.org/doi/abs/10.1145/2714576.2714635)
*   [https://www.usenix.org/system/files/conference/usenixsecurity15/sec15-paper-carlini.pdf](https://www.usenix.org/system/files/conference/usenixsecurity15/sec15-paper-carlini.pdf)
*   [https://github.com/googleprojectzero/p0tools/blob/master/JITServer/JIT-Server-whitepaper.pdf](https://github.com/googleprojectzero/p0tools/blob/master/JITServer/JIT-Server-whitepaper.pdf)
