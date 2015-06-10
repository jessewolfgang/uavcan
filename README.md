UAVCAN stack in C++
===================

[![Coverity Scan](https://scan.coverity.com/projects/1513/badge.svg)](https://scan.coverity.com/projects/1513)

Portable reference implementation of the [UAVCAN protocol stack](http://uavcan.org) in C++ for embedded systems
and Linux.

UAVCAN is a lightweight protocol designed for reliable communication in aerospace and robotic applications via CAN bus.

## Documentation

* [UAVCAN website](http://uavcan.org)
* [UAVCAN discussion group](https://groups.google.com/forum/#!forum/uavcan)
* [Libuavcan overview](http://uavcan.org/Libuavcan)
* [List of platforms officially supported by libuavcan](http://uavcan.org/List_of_platforms_officially_supported_by_libuavcan)
* [Libuavcan tutorials](http://uavcan.org/Libuavcan_tutorials)

## Library usage

### Dependencies

* Python 2.7 or 3.2 or newer
* [Pyuavcan](http://uavcan.org/Pyuavcan)

### Cloning the repository

```bash
git clone https://github.com/UAVCAN/libuavcan
git submodule update --init
```

If this repository is used as a git submodule in your project, make sure to use `--recursive` when updating it.

## Library development

Despite the fact that the library itself can be used on virtually any platform that has a standard-compliant
C++03 or C++11 compiler, the library development process assumes that the host OS is Linux.

Prerequisites:

* Google test library for C++ - gtest (see [how to install on Debian/Ubuntu](http://stackoverflow.com/questions/13513905/how-to-properly-setup-googletest-on-linux))
* C++03 *and* C++11 capable compiler with GCC-like interface (e.g. GCC, Clang)
* CMake 2.8+
* Optional: static analysis tool for C++ - cppcheck (on Debian/Ubuntu use package `cppcheck`)

Building the debug version and running the unit tests:
```bash
mkdir build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Debug
make
```

Test outputs can be found in the build directory under `libuavcan`.

Contributors, please follow the [Zubax Style Guide](https://github.com/Zubax/zubax_style_guide).

### Developing with Eclipse

An Eclipse project can be generated like that:

```bash
cmake ../../uavcan -G"Eclipse CDT4 - Unix Makefiles" \
                   -DCMAKE_ECLIPSE_VERSION=4.3 \
                   -DCMAKE_BUILD_TYPE=Debug \
                   -DCMAKE_CXX_COMPILER_ARG1=-std=c++11
```

Path `../../uavcan` in the command above points at the directory where the top-level `CMakeLists.txt` is located;
you may need to adjust this per your environment.
Note that the directory where Eclipse project is generated must not be a descendant of the source directory.

### Submitting a Coverity Scan build

First, [get the Coverity build tool](https://scan.coverity.com/download?tab=cxx). Then build the library with it:

```bash
export PATH=$PATH:<coverity-build-tool-directory>/bin/
mkdir build && cd build
cmake <uavcan-source-directory> -DCMAKE_BUILD_TYPE=Debug
cov-build --dir cov-int make -j8
tar czvf uavcan.tgz cov-int
```

Then upload the resulting archive to Coverity.
