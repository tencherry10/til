### Cross Compiler Toolchain

```
wget -c https://releases.linaro.org/components/toolchain/binaries/5.2-2015.11/arm-linux-gnueabihf/gcc-linaro-5.2-2015.11-x86_64_arm-linux-gnueabihf.tar.xz
tar Jxf gcc-linaro-5.2-2015.11-x86_64_arm-linux-gnueabihf.tar.xz
./gcc-linaro-5.2-2015.11-x86_64_arm-linux-gnueabihf/bin/arm-linux-gnueabihf-gcc --sysroot=./gcc-linaro-5.2-2015.11-x86_64_arm-linux-gnueabihf/arm-linux-gnueabihf/libc/arm-linux-gnueabihf/ main.c -o main
```

Looks like this will expect libc to be located at ```/lib/ld-linux-armhf.so.3``` so this wouldn't work with the alpine linux distro. You could work around this by compiling with ```-static``` like:

```
export CCC=./gcc-linaro-5.2-2015.11-x86_64_arm-linux-gnueabihf
${CCC}/bin/arm-linux-gnueabihf-gcc --sysroot=${CCC}/arm-linux-gnueabihf/libc/arm-linux-gnueabihf/ -static main.c -o main
```

And like you would expect, the resulting binary format will be arm:

```
file main
main: ELF 32-bit LSB  executable, ARM, EABI5 version 1 (GNU/Linux), statically linked, for GNU/Linux 2.6.32, BuildID[sha1]=56074fabef7e04389c1c1cde7c7ba2d329e5ff3d, not stripped
```


[source](https://eewiki.net/display/linuxonarm/BeagleBone+Black#BeagleBoneBlack-ARMCrossCompiler:GCC)

