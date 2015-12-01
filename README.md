# Signify - Sign and Verify

OpenBSD tool to signs and verify signatures on files. This is a portable
version which uses [libbsd](http://libbsd.freedesktop.org/wiki/) (version
0.7 or newer is required).

See http://www.tedunangst.com/flak/post/signify for more information.

## Build options

The following options can be passed to Make:

* `VERIFY_ONLY=1`

    Build only the verification code. Support for signing will not
    be available in the built `signify` binary. **Note that this is
    unsupported and compilation may not succeed.**

* `BOUNDS_CHECKING=1`

    Enables bounds-checking using `__attribute__((bounded))`. Your
    compiler must have support for this. Clang 3.4 is known to work.

* `LTO=1`

    Perform Link-Time Optimizations. Both your compiler *and* linker
    must have support for this. Recent binutils and GCC/Clang are
    known to work.

* `PLEDGE=…`

    Choose among one of the alternative implementations of the
    [pledge()](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man2/pledge.2)
    system call. For the moment the only supported values is:

      - `noop` *(default)*: Uses an implementation which does nothing

    To use your own implementation, use an empty value, and pass
    the needed flags for linking its code. For example:
    `make PLEDGE='' EXTRA_LDFLAGS=my-pledge.o`.

* `EXTRA_CFLAGS=…`, `EXTRA_LDFLAGS=…`

    Additional flags to be passed to the compiler and the linker,
    repectively.

For example, you can build a size-optimized version with:

    make EXTRA_CFLAGS='-Os -s' LTO=1
