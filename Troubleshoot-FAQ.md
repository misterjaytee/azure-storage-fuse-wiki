# Common Problems
**1. Error: fusermount: failed to open /etc/fuse.conf: Permission denied**

Only the users that are part of the group fuse, and the root user can run fusermount command. In order to mitigate this add your user to the fuse group.

```sudo addgroup <user> fuse```

**2. errno = 1600 Failed to connect to the storage container. There might be something wrong about the storage config, please double check the storage account name, account key and container name. errno = 1600**

Possible causes are invalid account, key or container. In addition to this, if your account is https only, you may encounter this problem as blobfuse by default uses http. Run blobfuse with https using the option --use-https=true

# Problems with build
**1. CMake Error: your CXX compiler: "CMAKE_CXX_COMPILER-NOTFOUND" was not found.**

Cmake is unable to find g++. Install it via:

```sudo apt-get update && sudo apt-get install build-essential```



