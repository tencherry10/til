### Cross Compile with Docker Env

This only works if your linux env supports qemu-user-static. So, run the following if you haven't already.

```
sudo apt-get install qemu qemu-user-static binfmt-support 
sudo apt-get install gcc-arm-linux-gnueabihf libc6-dev-armhf-cross  
sudo apt-get install binutils-arm-linux-gnueabi
```

There are a number of excellent docker build tools.

* [multiarch/qemu-user-static](https://hub.docker.com/r/multiarch/qemu-user-static/)
* [multiarch/crossbuild](https://hub.docker.com/r/multiarch/crossbuild/)

And, if you would like to run armhf binaries in a docker container. Here are some excellent ones to start with:

* [multiarch/busybox](https://hub.docker.com/r/multiarch/busybox/)
* [multiarch/debian-bootstrap](https://hub.docker.com/r/multiarch/debian-debootstrap/)
* [multiarch/alpine](https://hub.docker.com/r/multiarch/alpine/)
* [multiarch/ubuntu-debootstrap](https://hub.docker.com/r/multiarch/ubuntu-debootstrap/)

Just remember that alpine may not have the same "shared libraries"...

To register docker host for transparent qemu user emulation run the following:
```
docker run --rm --privileged multiarch/qemu-user-static:register
```

You can also transparently cross-compile:

```
docker run --rm -v $(pwd):/workdir -e CROSS_TRIPLE=arm-linux-gnueabihf multiarch/crossbuild make helloworld
```

And run it via:
```docker run -it --rm multiarch/debian-debootstrap:armhf-jessie```



