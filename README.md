# Snap7

Fork of <https://snap7.sourceforge.net/> with CMake support for C and C++.

## Usage

Recommended way is to use CMake's [FetchContent](https://cmake.org/cmake/help/latest/module/FetchContent.html) module:

```cmake
include(FetchContent)
FetchContent_Declare(
  snap7
  GIT_REPOSITORY https://github.com/the-risk-taker/snap7
  GIT_TAG        v1.4.2
)
FetchContent_MakeAvailable(snap7)
```

Then link `snap7::cpp_wrapper` to your C++ program, or `snap7::snap7` to C program:

```cmake
target_link_libraries(<target> PRIVATE snap7::cpp_wrapper)
```

And finally include `#include <snap7.h>` in the source files where Snap7 functions are used.

> [!NOTE]  
> The `snap7::cpp_wrapper` is a C++ wrapper for `snap7::snap7` C interface.

### Building manually

Alternatively you can build and install Snap7 then link manually, for building and installing:

```cmake
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build --parallel --target install 
```

> [!IMPORTANT]  
> Installing might require administrative permissions.

## Options

To build `static` version of Snap7 library pass:

```cmake
-DBUILD_SHARED_LIBS=OFF
```

To build `examples` pass:

```cmake
-DBUILD_EXAMPLES=ON
```

## Changes to the original

- Fix of '-Wstringop-overread' warning on GCC.
- Modified `client.cpp`, `apartner.cpp` and `ppartner.cpp` examples to support building and linking both static and dynamic versions of Snap7.
