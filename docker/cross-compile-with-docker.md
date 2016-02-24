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

docker run --rm --privileged multiarch/qemu-user-static:register
