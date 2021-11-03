# Control Flow Defenses against Return-Oriented-Programming (ROP)

## Stack Protector

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
program. `-fstack-protector-strong` enables the canary in more conditions
without enabling it for all functions.

## Other Mitigations

We acknowledge that stack canaries are easily bypassed through info leaks and
are investigating more comprehensive mitigations to protect the return address,
such as [ShadowCallStack](https://clang.llvm.org/docs/ShadowCallStack.html) or
[CET shadow stacks](https://security.googleblog.com/2021/05/enabling-hardware-enforced-stack.html)
after Chromium SafeStack support was [deprecated](https://crbug.com/908597).

## See also

*   [https://lwn.net/Articles/584225/](https://lwn.net/Articles/584225/)
*   [https://outflux.net/blog/archives/2014/01/27/fstack-protector-strong/](https://outflux.net/blog/archives/2014/01/27/fstack-protector-strong/)
*   [https://crbug.com/821951](https://crbug.com/821951)
*   [https://crbug.com/1131225](https://crbug.com/1131225)
*   [https://docs.google.com/document/d/1qHOgrf9jdXTlfRsP1hQ92v_ESsqcPioqHb5EUb3dbUI/edit](https://docs.google.com/document/d/1qHOgrf9jdXTlfRsP1hQ92v_ESsqcPioqHb5EUb3dbUI/edit)

Credits: the GrapheneOS team
