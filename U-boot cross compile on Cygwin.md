# U-boot cross compile on Cygwin

### Requirement
* [Cygwin](https://www.cygwin.com/)
	* autoconf
	* bison
	* flex
	* autoconf
	* gcc-core
	* make
	* libncurses-devel (if need menuconfig)
* [arm toolchain](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-a/downloads) 
    * arm-none-eabi (For me, bare-metal target)
    * arm-none-linux-gnueabihf (or If you use Linux)
* git

### Start
Get u-boot

    git clone https://github.com/u-boot/u-boot.git
    cd u-boot
    
**Important: Comment out below in `Makefile`!**

    ifeq ($(HOSTOS),cygwin)
    HOSTCFLAGS	+= -ansi
    endif

Add arm toolchain path
    
    export TL_PATH="/cygdrive/e/gcc-arm-none-eabi-9-2019-q4-major-win32"
    export PATH="$TL_PATH/bin:$PATH"
    
Before build

	export CROSS_COMPILE=arm-none-eabi-
	export ARCH=arm
Make

    make rpi_0_w_defconfig
    make
    
