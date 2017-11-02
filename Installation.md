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
