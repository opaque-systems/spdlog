This is a fork of [spdlog](https://github.com/gabime/spdlog) v1.8.5 compatible with
OpenEnclave. 

The only modification to the repo is `/include/spdlog/details/os-inl.h:86`
where we replace any calls to `localtime` (not supported by OpenEnclave) with
`gmtime`. This means that all reported times are in UTC.

Additionally the following compiler flags need to be set:
* `SPDLOG_NO_THREAD__ID`
* `FMT_USE_INT128=0`

This ensures that certain unsupported syscalls/library functions are used.
