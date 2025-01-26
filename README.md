# FlatCC Binary Distribution
This repository provides ready-to-use binary builds of [FlatCC](https://github.com/dvidelabs/flatcc),
the [FlatBuffers](https://flatbuffers.dev/) implementation in C for C.

## Builds

Check GitHub image versions here: https://github.com/actions/runner-images?tab=readme-ov-file#available-images

### Linux
The Linux build uses GitHub's ubuntu-latest image. Since FlatCC doesn't have third-party dependencies
(other than libc), the build should work for most Linux distributions.

### macOS
The macOS build uses GitHub's macos-latest image, and provides Universal 2 binaries (executable and libraries).

### Windows
The Windows build uses GitHub's windows-latest image, and is compiled using MinGW64 (UCRT). If your project uses 
MSVC instead, please verify the libraries work before using them.

## Usage (with CMake)

Add this snippet to your CMakeLists.txt, or include it as separate CMake script (e.g. `cmake/download_flatcc.cmake`).

```cmake
# Set the version and base URL for FlatCC binaries
set(FLATCC_VERSION "v0.6.2a1")
set(FLATCC_BASE_URL "https://github.com/fseconomy/flatcc-dist/releases/download/${FLATCC_VERSION}")

# Detect the platform
if(WIN32)
    set(FLATCC_PLATFORM flatcc-windows.zip)
elseif(APPLE)
    set(FLATCC_PLATFORM flatcc-macos.zip)
else()
    set(FLATCC_PLATFORM flatcc-linux.zip)
endif()

# Set the download URL
set(FLATCC_URL ${FLATCC_BASE_URL}/${FLATCC_PLATFORM})

# Download and extract FlatCC
include(FetchContent)
FetchContent_Declare(
        flatcc
        URL ${FLATCC_URL}
)
FetchContent_MakeAvailable(flatcc)
```

## Versions

The binaries are built from FlatCC's `master` branch. v0.6.2 isn't released yet, but the rather
low commit frequency suggests that FlatCC is quite mature. Therefore we use v0.6.2 as general release
identifier, suffixed with a pre-release marker. Available releases and the commit they're based on:

* v0.6.2a1 [be12a1f](https://github.com/dvidelabs/flatcc/commit/be12a1f74bbbda9bbad749f5fbf56c342c2878cb)

## Disclaimer
FlatCC is published under the Apache License Version 2.0, cf. LICENSE for details.
The source code is available at https://github.com/dvidelabs/flatcc.
