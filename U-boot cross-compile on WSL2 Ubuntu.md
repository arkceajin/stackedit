# U-boot cross-compile on WSL2 Ubuntu

### Requirement
* [WSL2](https://docs.microsoft.com/en-us/windows/wsl/wsl2-install)
* [Ubuntu distro](https://docs.microsoft.com/en-us/windows/wsl/install-win10#install-your-linux-distribution-of-choice)


### Start
Install dependencies

    sudo apt-get update
    sudo apt install make gcc bison flex
Install arm-toolchain

    sudo apt-get install gcc-arm-none-eabi binutils-arm-none-eabi gdb-arm-none-eabi
    
    export TL_PATH="/cygdrive/e/gcc-arm-none-eabi-9-2019-q4-major-win32"
    export PATH="$TL_PATH/bin:$PATH"
    
Before build

	export CROSS_COMPILE=arm-none-eabi-
	export ARCH=arm
  
Make

    make rpi_0_w_defconfig
    make
    
