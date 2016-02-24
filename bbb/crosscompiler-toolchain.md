### Cross Compiler Toolchain

```
wget -c https://releases.linaro.org/components/toolchain/binaries/5.2-2015.11/arm-linux-gnueabihf/gcc-linaro-5.2-2015.11-x86_64_arm-linux-gnueabihf.tar.xz
tar Jxf gcc-linaro-5.2-2015.11-x86_64_arm-linux-gnueabihf.tar.xz
./gcc-linaro-5.2-2015.11-x86_64_arm-linux-gnueabihf/bin/arm-linux-gnueabihf-gcc --sysroot=./gcc-linaro-5.2-2015.11-x86_64_arm-linux-gnueabihf/arm-linux-gnueabihf/libc/arm-linux-gnueabihf/ main.c -o main
```

[source](https://eewiki.net/display/linuxonarm/BeagleBone+Black#BeagleBoneBlack-ARMCrossCompiler:GCC)

