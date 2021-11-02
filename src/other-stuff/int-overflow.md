# Signed Integer Overflow

Signed integer overflow is undefined behavior. Hexavalent is temporarily using
`-fwrapv` to prevent issues stemming from reliance on undefined behavior as the
performance impact of
`-fsanitize=shift,signed-integer-overflow -fsanitize-trap=shift,signed-integer-overflow`
is deemed to be currently unacceptable. It would be nice to have hardware 
acceleration for this stuff.


## See also

*   [https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-fwrapv](https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-fwrapv)
*   [https://clang.llvm.org/docs/UndefinedBehaviorSanitizer.html](https://clang.llvm.org/docs/UndefinedBehaviorSanitizer.html)

Credits: the GrapheneOS team
