# cmake-library
A small C++ library created and installed using CMake

## Building the library

To generate the build using CMake:

`cmake -S . -B build`

and to build the library:

`cmake --build build`

On Windows, we can specify one of the configurations, Debug or Release. By default, the installation with CMake
expects the Release configuration. If you need to install the Debug configuration, you must specify it explicitly:

`cmake -S . -B build && cmake --build build --config Debug`
`cmake -S . -B build && cmake --build build --config Release`

and

`cmake --install build --config Debug --prefix c:\dev\library`
`cmake --install build --config Release --prefix c:\dev\library`
