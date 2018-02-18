# Common Problems
**1. Error: fusermount: failed to open /etc/fuse.conf: Permission denied**

Only the users that are part of the group fuse, and the root user can run fusermount command. In order to mitigate this add your user to the fuse group.

```sudo addgroup <user> fuse```

**2. errno = 1600 Failed to connect to the storage container. There might be something wrong about the storage config, please double check the storage account name, account key and container name. errno = 1600**

Possible causes are invalid account, key or container. In addition to this, if your account is https only, you may encounter this problem as blobfuse by default uses http. Run blobfuse with https using the option --use-https=true

**3. fusermount: mount failed: Operation not permitted (CentOS)**

fusermount is a priviliged operation on CentOS by default. You may work around this changing the permissions of the fusermount operation:

    chown root /usr/bin/fusermount
    chmod u+s /usr/bin/fusermount

**4. Cannot access mounted directory**

FUSE allows mounting filesystem in user space, and is only accessible by the user mounting it. For instance, if you have mounted using root, but you are trying to access it with another user, you will fail to do so. In order to workaround this, you can use the non-secure, fuse option '-o allow_other'.

    sudo blobfuse /home/myuser/mount/ --config-file=connection.cfg --tmp-path=/mnt/resource/blobfusetmp -o allow_other

**5. fuse: warning: library too old, some operations may not not work**

Your system has an earlier version of FUSE module installed. blobfuse is tested and developed with FUSE 2.9.x. Please install FUSE 2.9.

# Problems with build
**1. CMake Error: your CXX compiler: "CMAKE_CXX_COMPILER-NOTFOUND" was not found.**

Cmake is unable to find g++. Install it via:

```sudo apt-get update && sudo apt-get install build-essential```

**2. cc1plus: error: unrecognized command line option "-std=c++11"**

Your compiler does not support C++ 11. Upgrade gcc to 4.7 or later.


# Problems with mounting/unmounting
**1. When mounting using the fstab method (e.g. mount -a), you get an error from mount:**
```
mount: wrong fs type, bad option, bad superblock on /scripts/mount.sh,
       missing codepage or helper program, or other error

       In some cases useful info is found in syslog - try
       dmesg | tail or so.
```

Make sure the fuse package is installed (in addition to blobfuse), e.g. on Centos, Fedora, RHEL:

``` yum install fuse ```


**2. fusermount: command not found**

You try to unmount the blob storage, but the recommended command is not found. Whilst `umount` may work instead, fusermount is the recommended method, so install the fuse package, e.g.:

``` yum install fuse ```

