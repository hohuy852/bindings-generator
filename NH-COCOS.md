# NH-Cocos bindings generator fork

This fork's `main` starts at upstream commit
`2b9026fc7535f602833b9dd7187d3029e50a97fc`, the generator used by Cocos2d-x 2.2.6.
It intentionally does not track the modern upstream default branch.

## Reviewed changes

- Map Clang `CHAR_U` to C++ `char`. This kind describes plain `char` on targets
  where it is unsigned, including the ARM target used here. Explicit
  `unsigned char` remains `UCHAR`; mapping both to `unsigned char` incorrectly
  generates string arguments for APIs declared with `const char*`.
- Add the missing SpiderMonkey input conversion for `const unsigned char*`.
  Its temporary `std::string` owns the bytes for the duration of the wrapper
  call. This is the legacy string input convention, not a general ArrayBuffer
  or retained native buffer implementation.

The matching NH-Cocos build uses Python 2.7 and the Cocos-era Clang/NDK layout.
Generated C++ bindings are committed in NH-Cocos, so ordinary game builds do
not need to run this generator.
