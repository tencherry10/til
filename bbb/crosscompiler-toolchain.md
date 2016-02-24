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

[source](https://eewiki.net/display/linuxonarm/BeagleBone+Black#BeagleBoneBlack-ARMCrossCompiler:GCC)

