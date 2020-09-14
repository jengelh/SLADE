## Linux

### Mandatory build-time requirements

* C++17 compiler (e.g. g++ 8.x)
* bzip2 library
* cURL library
* FreeImage
* fmt 6.x
* ftgl, an OpenGL font managing library
* GLEW
* GTK 2.x/3.x
* mpg123 library
* OpenGL
* SFML
* wxWidgets 3.x
* zlib

### Optional build-time requirements

* Fluidsynth (deactivate with `cmake -DNO_FLUIDSYNTH=ON`)

### Additional configure switches for cmake

* `-DNO_COTIRE=ON`: disable the use of precompiled headers
* `-DNO_CRASHHANDLER=ON`: disable the use of a dedicated crash handler (as it is susceptible to crashes and hangs of its own) and default to the standard handler of the C runtime instead.
* `-DNO_WEBVIEW=ON`: use if your wxWidgets build has no wxWebview or if not desired
* `-DWX_GTK3=OFF`: use if your wxWidgets build is using the wxGTK2 backend (there is no autodetection at this point)

## Windows

SLADE can be built on Windows using [Visual Studio](https://visualstudio.microsoft.com/) 2019+ (a free 'community' edition is available which works fine) and [vcpkg](https://docs.microsoft.com/en-us/cpp/build/vcpkg?view=vs-2019) for handling the required external libraries.

### Required vcpkg libraries

* curl
* fmt
* freeimage
* glew
* lua
* mpg123
* opengl
* sfml
* wxwidgets

The above libraries are required for building SLADE on windows. Note that you'll most likely want to use the `x64-windows-static` triplet when installing them, eg.

```
.\vcpkg install <libraries> --triplet x64-windows-static
```
