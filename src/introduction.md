# Hexavalent

Hexavalent is a privacy/security-oriented Chromium downstream project. It's
focused on developing meaningful security improvements mitigating classes of
vulnerabilities rather than individual bugs and is currently a work-in-progress.

## Features

*   Strengthening site sandbox by way of origin isolation, improving on the
    current eTLD+1 isolation to mitigate real speculative execution exploits
    targeting sites that aren't sufficiently cross-origin isolated
*   Toggle (soon to be site setting) for disabling JIT compilation and
    enablement of additional mitigations in the renderer such as ACG and CET
    SHSTK
*   More private WebRTC IP handling policy by default and provision of a toggle
    for users who may use a proxy and expose their ISP public address
*   Initializing all variables with zero to mitigate vulnerabilities stemming
    from use of uninitialized memory
*   Stubbing of Battery Status API to counteract abuse of a API that has not
    been used for legitimate purposes
*   Building with `-fstack-protector-strong` to add canaries to more functions
    while having low performance impact
*   Various security improvements to PartitionAlloc to make it harder to exploit
    heap corruption
*   Revoking of sensors access to avoid giving sites unfettered access to
    sensitive info
*   `-fwrapv` by default to wrap otherwise undefined signed overflow
*   Enabling of all current state partitioning features upstream
*   Making HTTPS-only mode the default
