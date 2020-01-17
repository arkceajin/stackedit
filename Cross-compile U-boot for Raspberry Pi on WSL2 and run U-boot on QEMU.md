# Cross-compile U-boot for Raspberry Pi on WSL2 and run U-boot on QEMU

### Requirement
* [WSL2](https://docs.microsoft.com/en-us/windows/wsl/wsl2-install)
* [Ubuntu distro](https://docs.microsoft.com/en-us/windows/wsl/install-win10#install-your-linux-distribution-of-choice)
* [U-boot](https://www.denx.de/wiki/view/DULG/UBootSources)

### Cross compile U-boot
Install dependencies

    	sudo apt-get update
    	sudo apt install make gcc bison flex
    
Install arm-toolchain

    	sudo apt-get install gcc-arm-none-eabi binutils-arm-none-eabi

Before build

	export CROSS_COMPILE=arm-none-eabi-
	export ARCH=arm
  
[Make](https://www.denx.de/wiki/view/DULG/UBootConfiguration)

	ls -l configs/rpi* // Check what is available
	
	make rpi_2_defconfig all

### Download raspberry pi bootloader

	wget https://github.com/raspberrypi/firmware/raw/master/boot/bootcode.bin -P ./
	wget https://github.com/raspberrypi/firmware/raw/master/boot/start.elf -P ./

Create config file and indicate we want to launch `u-boot` after Raspberry Pi completed boot.

	echo 'kernel=u-boot.bin' > config.txt

### Make U-boot img
Install mtools

	sudo apt install mtools
	
Create img

	dd if=/dev/null of=rasp-uboot.img bs=1M seek=40
	mkfs.fat -F 32 rasp-uboot.img
	
Because cannot use `mount` with `vfat` in WSL, so have to use `mtools` instead `mount`.
	
	# sudo mount -t vfat -o loop ${OUTPUT_IMG} ${TEMP_MOUNT_DIR}
	
Copy files into img

	mcopy -i rasp-uboot.img bootcode.bin ::/bootcode.bin
	mcopy -i rasp-uboot.img start.elf ::/start.elf
	mcopy -i rasp-uboot.img config.txt ::/config.txt
	mcopy -i rasp-uboot.img u-boot.bin ::/u-boot.bin

Confirm the contents of img

	mdir  -i rasp-uboot.img -/

	
