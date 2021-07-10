### OpenWRT on RISC-V

Build openwrt on risc-v

It builds, but requires testing 

```
Usage :
install ubuntu Ubuntu 21.04 on hifive unmatched (https://blogjawn.stufftoread.com/install-ubuntu-on-hifive-unmatched.html)
sudo apt install build-essential gcc binutils bzip2 flex python3 perl make grep unzip gawk subversion zlib1g-dev libc6-dev rsync libncurses5-dev libncursesw5-dev
git pull git@github.com:Thessal/openwrt.git
make menuconfig

Select Target → RISC-V HiFive Unleashed / QEMU
Advanced configuration options → Toolchain options → C Library implementation, select Use glibc
enable ccache
enable image build

make 
make image
```

Image will be uploaded later

```
Reference :
https://github.com/carlosedp/riscv-bringup
https://github.com/xfguo/riscv-openwrt
```

u-boot
```
https://u-boot.readthedocs.io/en/latest/board/sifive/unmatched.html

git clone https://github.com/riscv/opensbi.git
cd opensbi
make PLATFORM=generic
export OPENSBI=<path to opensbi/build/platform/generic/firmware/fw_dynamic.bin>
cd <U-Boot-dir>
make sifive_unmatched_defconfig
make

sudo sgdisk -g --clear -a 1  /dev/sda
sudo sgdisk -g --new=1:34:2081         --change-name=1:spl --typecode=1:5B193300-FC78-40CD-8002-E86C45580B47  /dev/sda
# --new=2:2082:10273      --change-name=2:uboot  --typecode=2:2E54B353-1271-4842-806F-E436D6AF6985 
# --new=3:16384:282623    --change-name=3:boot --typecode=3:0x0700 
# --new=4:286720:13918207 --change-name=4:root --typecode=4:0x8300 
...

sudo dd if=u-boot/spl/u-boot-spl.bin of=/dev/sda seek=34
sudo dd if=u-boot/u-boot.itb of=/dev/sda seek=2082

sudo dd if=~/openwrt/bin/targets/riscv64/generic-glibc/openwrt-riscv64-ext4.img of=/dev/sda4
sudo mount /dev/sda4 /media/sda4
sudo umount /media/sda4

sudo mount /dev/sda3 /media/sda3
sudo cp  ~/openwrt/bin/targets/riscv64/generic-glibc/openwrt-riscv64-vmlinux.elf /media/sda3
suod cp ~/u-boot/arch/riscv/dts/hifive-unmatched-a00.dtb /media/sda3
sudo umount /media/sda3

```
