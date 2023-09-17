Common:

Please generate game binary headers. Check README.txt of bin2h directoy.


For PC:

$ ./configure \
  --disable-gl \
  --without-png \
  --without-mixer \
  --without-net
$ make

$ ./src/prboom


For RISC-V baremetal:

$ cd baremetal_crt
$ cmake ./ -G Ninja -B build \
  -DCMAKE_BUILD_TYPE=RelWithDebInfo \
  -DCMAKE_INSTALL_PREFIX=./test/sysroot/ \
  -DARCH=riscv \
  -DCROSS_COMPILE=riscv64-unknown-elf- \
  -DCC=gcc \
  -DDEFCONF=riscv_qemu_virt_32_xip
$ ninja -C build -j16 install

$ cd prboom2/src/riscv
$ make USE_NEWLIB=y all

$ system-riscv32 \
  -machine virt \
  -bios none \
  -net none \
  -nographic \
  -chardev stdio,id=con,mux=on \
  -serial chardev:con \
  -mon chardev=con,mode=readline \
  -smp 4 \
  -kernel src/riscv/prboom
