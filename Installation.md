# Build from source
## Cloning this repo

    git clone https://github.com/Azure/azure-storage-fuse/

If you do not have git, install git via `sudo apt-get install git`

## Installing dependencies
### CentOS instructions

    sudo yum -y install epel-release
    sudo yum install git cmake3 fuse-devel libcurl-devel gcc gcc-c++ gnutls-devel fuse -y

### RedHat instructions

    sudo yum install git cmake fuse-devel libcurl-devel gcc gcc-c++ gnutls-devel fuse -y

### Ubuntu instructions

    sudo apt-get install pkg-config libfuse-dev cmake libcurl4-gnutls-dev libgnutls28-dev -y

## Building
Run the build script located in the root folder of the repository. This will build the Azure Storage C++ Light library along with Blobfuse.

    ./build.sh

## Preparing
Blobfuse uses the local disk as a buffer cache. On Azure, use the ephemeral drive (usually SSD) to get the most performance out of the buffer cache. Note that Blobfuse will need to have write access to the directory you choose as a buffer cache.

Default location for buffer cache is /mnt/blobfusetmp. Create this directory and change owner to the user that mounts the Blobfuse.

    mkdir /mnt/blobfusetmp
    chown <youruser> /mnt/blobfusetmp

**Note for RedHat:** Use /mnt/resource/blobfusetmp as the temp path on RedHat as the ephemeral drive is mounted on /mnt/resource in RedHat on Azure.

## Mounting
### One time mount
1. Update connection.cfg file with your storage account information. By default, connection.cfg is located in the root directory of this repository.
2. Run mount.sh    

`./mount.sh <path_to_mountpoint>`

### Persisting
1. Update connection.cfg file with your storage account information.
2. Edit /etc/fstab with the blobfuse script. Add the following line:

`/<path_to_blobfuse>/mount.sh   <path_to_mount>     fuse    _netdev`

## Unmounting
The standard way to unmount a FUSE adapter is to use 'fusermount':
`fusermount -u <path_to_mountpoint>`