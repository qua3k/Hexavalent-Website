# Mitigations Deployed in the Browser

## Sandboxing

Chrome is the most heavily sandboxed browser, leagues ahead of the alternatives.

## Browser Process

The browser process is the most privileged process, and there is a strong incentive to sandbox it.

### Windows

To protect virtual and indirect calls, the Chrome team is looking into enabling 
Microsoft's Control-Flow Guard.

The Chrome team enables enable Intel's offering for protecting returns, the 
hardware shadow stack, and adds a flag for toggling Arbitrary code guard (ACG) 
with thread opt-out.

## Hardware-Enforced Shadow Stacks (cetcompat)

On compatible hardware (Intel 11th Gen or AMD Zen 3 CPUs)

## See also

*   [https://security.googleblog.com/2021/05/enabling-hardware-enforced-stack.html](https://security.googleblog.com/2021/05/enabling-hardware-enforced-stack.html)