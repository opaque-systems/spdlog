This is a fork of [spdlog](https://github.com/gabime/spdlog) v1.8.5 compatible with
OpenEnclave. 

The only modifications to the repo are:

- In `/include/spdlog/details/os-inl.h:86` we replace any calls to `localtime` (not supported by OpenEnclave) with `gmtime`. This means that all reported times are in UTC.
- We modify the `in_terminal(FILE *file)` function defined in `/include/spdlog/details/os.h` to always return `false` to avoid calling the unsupported `isatty` function.

Additionally the following compiler flags need to be set:
* `SPDLOG_NO_THREAD_ID`
* `FMT_USE_INT128=0`

This ensures that only supported syscalls/library functions are used.
