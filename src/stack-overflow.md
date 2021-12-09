# Stack Overflow

## Stack Smashing Protector (SSP)

The stack protector feature is a probabilistic defense – it pushes a canary on
the stack after the return pointer is pushed and checks the value upon return,
aborting if there is a mismatch. It's not a particularly strong defense and
incurs a performance penalty, which is why the `-fstack-protector` option only
protects a subset of the functions in the program. Hexavalent uses a stronger
heuristic (`-fstack-protector-strong`) to cover more functions.

## Other Stuff

// TODO: write

## See also

*   [https://outflux.net/blog/archives/2014/01/27/fstack-protector-strong/](https://outflux.net/blog/archives/2014/01/27/fstack-protector-strong/)
