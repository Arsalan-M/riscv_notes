// RISC-V OpenSBI cross-compiler
// U-boot

# https://riscv.org/wp-content/uploads/2019/12/Summit_bootflow.pdf

# https://fossies.org/linux/qemu/roms/opensbi/README.md

# https://toolchains.bootlin.com/

# https://risc-v-getting-started-guide.readthedocs.io/en/latest/linux-qemu.html


# https://u-boot.readthedocs.io/en/latest/board/emulation/qemu-riscv.html


 sudo apt install autoconf automake autotools-dev curl libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison swig flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev git
 cd /
 sudo mkdir workspace
 sudo chmod 777 workspace
 cd workspace
 mkdir r5
 cd r5
 git clone https://github.com/riscv/opensbi.git
 cd opensbi/
 ls
 cd ..
 mv ~/Downloads/riscv64--glibc--bleeding-edge-2020.08-1.tar.bz2 .
 tar xvjf riscv64--glibc--bleeding-edge-2020.08-1.tar.bz2 
 ls
 rm riscv64--glibc--bleeding-edge-2020.08-1.tar.bz2 
 ls -ltr
 ls riscv64--glibc--bleeding-edge-2020.08-1/
 ls riscv64--glibc--bleeding-edge-2020.08-1/bin/
 cd riscv64--glibc--bleeding-edge-2020.08-1/
 more README.txt 
 cd ..
 export CROSS_COMPILE=/workspace/r5/riscv64--glibc--bleeding-edge-2020.08-1/bin/riscv64-buildroot-linux-gnu-
 cd opensbi/
 make PLATFORM=generic
 ls build/platform/
 ls build/platform/generic/
 ls build/platform/generic/firmware/
 ls build/platform/generic/lib/
 cd ..
 git clone https://source.denx.de/u-boot/u-boot.git 
 pwd
 ls -ltr
 git clone https://github.com/qemu/qemu
 cd qemu/
 git branch -a
 git checkout -b v5 remotes/origin/stable-5.0
 ./configure --target-list=riscv64-softmmu
 make -j $(nproc)
 sudo make install
 cd ..
 cd u-boot/
 ls -ltr
 make qemu-riscv64_defconfig
 make -j $(nproc)
 make qemu-riscv64_spl_defconfig
 make -j $(nproc)
 ls -ltr ../opensbi/build/platform/generic/firmware/fw_dynamic.bin
 cp ../opensbi/build/platform/generic/firmware/fw_dynamic.bin .
 make -j $(nproc)
 ls -ltr
 qemu-system-riscv64 -nographic -machine virt -bios spl/u-boot-spl -device loader,file=u-boot.itb,addr=0x80200000

# Ctrl-A X         to quit QEMU
