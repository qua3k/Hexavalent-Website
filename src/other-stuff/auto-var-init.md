# Automatic Variable Initialization

Using an uninitialized variable results in undefined behavior. This compiler
option automatically initializes variables with zero to hopefully reduce the
impact of those issues. It's also a lot faster than pattern-based init and
should cause fewer problems overall.

## See also

*   [https://reviews.llvm.org/D54604](https://reviews.llvm.org/D54604)
*   [https://lists.llvm.org/pipermail/cfe-dev/2020-April/065221.html](https://lists.llvm.org/pipermail/cfe-dev/2020-April/065221.html)

Credits: the GrapheneOS team
