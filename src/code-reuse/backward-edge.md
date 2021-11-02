# Backward-Edge Protection (Return Addresses)

There are multiple defenses used to protect returns. Some of them are listed
here.

## Stack Smashing Protector

The stack protector feature is meant to prevent control-flow hijacking by
detecting linear stack overflows.

Here's the basic gist:

1.  A canary (cookie) is added on the stack after the function return pointer
    has been pushed.
1.  The value of the canary is checked before the function returns.
1.  If the value of the canary has changed, a stack overflow has occured and the
    program aborts.

However, adding canaries to every function comes at a performance penalty, so
the `-fstack-protector` option only protects a subset of the functions in the
program. We use `-fstack-protector-strong`, enabling the canary in more
conditions without enabling it for all functions.

## Other Mitigations

We acknowledge that stack canaries are easily bypassed through info leaks and
are investigating more comprehensive mitigations to protect the return address,
such as [ShadowCallStack](https://clang.llvm.org/docs/ShadowCallStack.html) or
[CET shadow stacks](https://security.googleblog.com/2021/05/enabling-hardware-enforced-stack.html)
after Chromium SafeStack support was [deprecated](https://crbug.com/908597).

## ShadowCallStack

// TODO

## ARM Pointer Authentication

The ARMv8.3-A architecture adds "pointer authentication" instructions meant to make it "much harder for an attacker to modify protected pointers in memory without being detected."

## Hardware-Enforced Shadow Stacks (cetcompat)

// TODO

## See also

*   [https://lwn.net/Articles/584225/](https://lwn.net/Articles/584225/)
*   [https://outflux.net/blog/archives/2014/01/27/fstack-protector-strong/](https://outflux.net/blog/archives/2014/01/27/fstack-protector-strong/)
*   [https://crbug.com/821951](https://crbug.com/821951)
*   [https://crbug.com/1131225](https://crbug.com/1131225)
*   [https://docs.google.com/document/d/1qHOgrf9jdXTlfRsP1hQ92v_ESsqcPioqHb5EUb3dbUI/edit](https://docs.google.com/document/d/1qHOgrf9jdXTlfRsP1hQ92v_ESsqcPioqHb5EUb3dbUI/edit)
*   [https://www.qualcomm.com/media/documents/files/whitepaper-pointer-authentication-on-armv8-3.pdf](https://www.qualcomm.com/media/documents/files/whitepaper-pointer-authentication-on-armv8-3.pdf)
*   [https://security.googleblog.com/2021/05/enabling-hardware-enforced-stack.html](https://security.googleblog.com/2021/05/enabling-hardware-enforced-stack.html)
*   [https://grsecurity.net/effectiveness_of_intel_cet_against_code_reuse_attacks](https://grsecurity.net/effectiveness_of_intel_cet_against_code_reuse_attacks)
*   [https://www.angelfire.com/sk/stackshield/](https://www.angelfire.com/sk/stackshield/)

Credits: the GrapheneOS team

p.s. we really wish we had RAP
