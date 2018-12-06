# Compile OpenCV with Qt & MinGW

## Preparation
1. Download source from https://opencv.org/releases.html
2. CMake 3.1
3. Qt 5.10.1 & MinGW

## System path
Make sure the following Qt & MinGW path in the system path

    C:\Qt\Qt5.10.1\5.10.1\mingw53_32\bin
    C:\Qt\Qt5.10.1\Tools\mingw530_32\bin

## CMake 

1. Open `cmake-gui`.
2. Input the path of **Where is the source code** and **Where to build the binaries**.
3. Press **Configure**.
4. Specify the generator as `MinGW Makefiles` and select the `Specify native compilers`, then go **Next**.
5. Set the your gcc & g++ path. E.g. `C:/Qt/Qt5.10.1/Tools/mingw530_32/bin/gcc.exe` `C:/Qt/Qt5.10.1/Tools/mingw530_32/bin/g++.exe`, then press **Finish** and wait for the configure.
6. Search `WITH_MSMF` and uncheck it (Without `Microsoft Media Foundation`).
7. Search `WITH_OPENGL` `WITH_QT` and check.
8. Press **Generate**. The log will show `Configuring done` and `Generating done`, which means CMake successed.

## Compiling
1. Open the Windows CMD and enter the build folder. `cd D:\OpenCV\opencv-4.0.0-build`
2. Make `mingw32-make -j 4`

If you got error of `sprintf_instead_use_StringCbPrintfA_or_StringCchPrintfA`, add `#define NO_DSHOW_STRSAFE` before the line `#include "DShow.h"` in the file `opencv-4.0.0/modules/videoio/src/cap_dshow.cpp`

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxNzQxMjM5MSwtODYzOTExNzIzLC0xMz
Y4NDMxOTkxLC0xMzk0MjU0MDc1XX0=
-->