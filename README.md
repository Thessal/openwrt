### OpenWRT on RISC-V

Build openwrt on risc-v

It builds, but requires testing 

```
Usage :
install ubuntu Ubuntu 21.04 on hifive unmatched (https://blogjawn.stufftoread.com/install-ubuntu-on-hifive-unmatched.html)
sudo apt install build-essential gcc binutils bzip2 flex python3 perl make grep unzip gawk subversion zlib1g-dev libc6-dev rsync libncurses5-dev libncursesw5-dev
git pull git@github.com:Thessal/openwrt.git
make

Select Target → RISC-V HiFive Unleashed / QEMU
Advanced configuration options → Toolchain options → C Library implementation, select Use glibc
```

Image will be uploaded later

```
Reference :
https://github.com/carlosedp/riscv-bringup
https://github.com/xfguo/riscv-openwrt
```

