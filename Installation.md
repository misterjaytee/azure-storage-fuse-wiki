# Install from Apt/Yum Package Repositories

blobfuse is currently available in the Microsoft product repository for Ubuntu distros. 

1. Configure the apt repository for Microsoft products following [this guideline](https://docs.microsoft.com/en-us/windows-server/administration/Linux-Package-Repository-for-Microsoft-Software)

**E.g. Ubuntu 16.04**
    wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb
    sudo dpkg -i packages-microsoft-prod.deb
    sudo apt-get update

2. Install blobfuse
```sudo apt-get install blobfuse```

You're set to go! Now follow the [Configuring and Running](https://github.com/Azure/azure-storage-fuse/wiki/Configuring-and-Running) wiki to configure a temp location, as well as your credentials.

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
