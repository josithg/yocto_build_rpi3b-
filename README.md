## Recommended setup : 

- **OS** : Ubuntu LTS (22.04) or Debian stable 
- **CPU** : Minimum of 6 cores and 12 threads 
- **RAM** : 
	- If DDR4 - 16 GB 
	- if DDR5 - 12 GB 
- Minimum of 50 GB free space 
- **Constant power and internet source (>5 MB/s)**

## Building steps

-  Update and Upgrade the system 
```
sudo apt update 
sudo apt upgrade -y
```

- install the necessary packages and dependencies 
```
sudo apt install gawk wget git-core diffstat unzip texinfo gcc \
     build-essential chrpath socat cpio python3 python3-pip python3-pexpect \
     xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa \
     libsdl1.2-dev pylint xterm
```

- Clone the yocto repo  and setup the environment 
```
git clone https://git.yoctoproject.org/git/poky
cd poky
git checkout nanbield
source oe-init-build-env build-rpi32
```
- clone the other essential repo in home folder 

- raspberrypi repo
```
git clone https://git.yoctoproject.org/meta-raspberrypi
cd meta-raspberrypi
git checkout nanbield 
```

- openembedded repo
```
git clone https://git.openembedded.org/meta-openembedded
cd meta-openembedded
git checkout nanbield 
```

- navigate to build-rpi folder in poky 
```
cd /home/<user>/poky/build-rpi32
```

- open the bblayers.conf and edit it accordingly
- open the local.conf and edit it accordingly


- save the file and exit and setup locale 
```
export LC_ALL=C.UTF-8
export LANG=C.UTF-8
```

- navigate to poky folder 
```
cd /home/<user>/poky
```

- start building
```
bitbake core-image-base
```

- make sure you have a stable power and internet connection the build duration depends upon your cpu 

- after the build i complete navigate to 
```
/home/<user>/poky/build-rpi32/tmp/deploy/images
```
- if there is no tmp folder check for tmp-glibc to find your image 

- insert the sd card and unmount partitions

- flash the image 
```
sudo dd if=core-image-base-raspberrypi3.rootfs-<timestamp>.rootfs.rpi-sdimg of=/dev/sda bs=4M status=progress conv=fsync

```
- use the sync command again for safety 
- boot the image
# Note : you can also use the shell file to setup and build the yocto image 
- use setup-environment.sh for setting up the environment
- use build-image.sh to build the image after manually editing the config files 
