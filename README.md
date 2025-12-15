# tinyobjloader in C

Tiny but powerful header only wavefront obj loader written in C99, by [Syoyo Fujita](https://github.com/syoyo).

If you are looking for C++ version, please see https://github.com/syoyo/tinyobjloader

## Current status

Experimental. Loading geometry data would be OK, More testing required for materials and shapes.

## Features

* Single file, header only
* Dependency-free pure C99 implementation(except for `libc`)
* Provides mostly similar functionality as in C++ version. https://github.com/syoyo/tinyobjloader
* Moderate speed and moderate memory consumption
  * Rungholt 7M triangle scene(260 MB) can be loaded in 4.7 secs and consumes 3.6 GB memory at the maximum on MacBook12 Core m5 1.2 GHz(single core use)
* Unit tests using acutest thanks to @andystanton

## Installation

Run:
```bash
$ npm i tinyobjloader.c
```

And then include `tinyobj_loader_c.h` as follows:
```c
#include "node_modules/tinyobjloader.c/tinyobj_loader_c.h"
```

## Usage

Include `tinyobj_loader_c.h` to your project.

```c
/* define TINYOBJ_LOADER_C_IMPLEMENTATION for only *one* .c */
#define TINYOBJ_LOADER_C_IMPLEMENTATION
#include "tinyobj_loader_c.h"

...

```

See `examples/viewer/` for more details.

tinyobjloader allocates memory. To replace the functions used for allocation,
define `TINYOBJ_MALLOC`, `TINYOBJ_REALLOC`, `TINYOBJ_CALLOC` and `TINYOBJ_FREE` in the .c file
you defined `TINYOBJ_LOADER_C_IMPLEMENTATION` in, before including `tinyobj_loader_c.h`.
Define either all or none of them. They replace `malloc`, `realloc`, `calloc` and `free` respectively.

Example:
```c
#define TINYOBJ_LOADER_C_IMPLEMENTATION
#define TINYOBJ_MALLOC my_malloc
#define TINYOBJ_REALLOC my_realloc
#define TINYOBJ_CALLOC my_calloc
#define TINYOBJ_FREE my_free
#include "tinyobj_loader_c.h"
```

## Tests

The single header test library [acutest](https://github.com/mity/acutest) is used to provide a test runner and assertion macros. There are two test suites: one for the API and one for the internal functions. Ultimately the internal tests should be removed, but are useful while the project is volatile.

The tests can be run from the project root using:

```bash
$ make test
```

This builds and executes a binary called `tinyobj_tests` in the test folder. There are some options to run specific tests that can be passed to the executable directly that are described on the [acutest readme](https://github.com/mity/acutest#running-unit-tests).

By default acutest forks for each test. To disable this for debugging purposes, you can pass the switch `--no-exec` to `tinyobj_tests`.

## License

MIT license.

### Third party licenses

* acutest Another C/C++ Unit Test facility. MIT license. http://github.com/mity/acutest

## TODO

* [ ] Windows build?

<br>
<br>


[![ORG](https://img.shields.io/badge/org-nodef-green?logo=Org)](https://nodef.github.io)
![](https://ga-beacon.deno.dev/G-RC63DPBH3P:SH3Eq-NoQ9mwgYeHWxu7cw/github.com/nodef/tinyobjloader.c)
[![SRC](https://img.shields.io/badge/src-repo-green?logo=Org)](https://github.com/syoyo/tinyobjloader-c)
