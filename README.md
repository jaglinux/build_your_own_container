# build_your_own_container

 1. 
 mkdir my_own_container
 cd my_own_container

 sudo mount -B /bin/ ./bin
 sudo mount -B /lib ./lib
 sudo mount -B /lib64/ ./lib64/

 sudo chroot my_own_container

2.
docker run -it --rm ubuntu
docker export fbc57ee7356f -o image.tar
mkdir rootfs
tar xf image.tar --ignore-command-error -C rootfs/
unshare --mount --uts --ipc --net --pid --fork --user --map-root-user chroot $PWD/rootfs bash
root:# mount -t proc none /proc
root:# mount -t sysfs none /sys
root:# mount -t tmpfs none /tmp
