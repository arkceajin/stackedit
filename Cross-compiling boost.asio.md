
# Cross-compiling boost.asio

## Preparation
1. Download source from https://www.boost.org/
2. CMake (For demonstration)
3. ARM-GCC

## Build
**boost.asio** requires **boost.system** which have to be compiled separately, so basically there is nothing to do with **boost.asio** because it's a header-only library. Only need cross-compile the **boost.system**

1. Unzip the source.
`tar --bzip2 -xf boost_1_67_0.tar.bz2 && cd boost_1_67_0` 
2.  Generate the config file.
`./bootstrap.sh --with-libraries=system`
3. Edit the config file, set the compiler as arm version.
And be care for the space around the GCC's path.
`
gedit project-config.jam`
and replace gcc as below:
if ! gcc in [ feature.values <toolset> ]
{
    using gcc : arm : /opt/freescale/usr/local/gcc-4.3.3-glibc-2.8-cs2009q1-203/arm-none-linux-gnueabi/bin/arm-none-linux-gnueabi-gcc ; 
}
`
4. Compile the **boost.system**.
`./b2 toolset=gcc-arm`
After this, the libs will be generated under folder `source path/stage/lib/`
5. In the **CMakeLists.txt**
> project(ASIOTest)
> cmake_minimum_required(VERSION 2.4)
> 
> set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
> 
> set(CMAKE_C_COMPILER
> /opt/freescale/usr/local/gcc-4.3.3-glibc-2.8-cs2009q1-203/arm-none-linux-gnueabi/bin/arm-none-linux-gnueabi-gcc)
> set(CMAKE_CXX_COMPILER
> /opt/freescale/usr/local/gcc-4.3.3-glibc-2.8-cs2009q1-203/arm-none-linux-gnueabi/bin/arm-none-linux-gnueabi-g++)
> 
> #set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -pthread")
> #set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread") set(BOOST_PATH "/home/fit/boost_1_67_0")
> 
> include_directories(${BOOST_PATH})
> link_directories(${BOOST_PATH}/stage/lib)
> 
> add_executable(ASIOTest main.cpp)
> 
> target_link_libraries(ASIOTest boost_system)

<!--stackedit_data:
eyJoaXN0b3J5IjpbODAzNzQyNDYyLDc4MTc2MjUxMiwyNjA5NT
k1ODEsODA0ODMzMTA2XX0=
-->