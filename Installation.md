# Install from Apt/Yum Package Repositories

blobfuse is currently available in the Microsoft product repositories for Ubuntu, CentOS/RedHat distros. 

**1.** Configure the apt repository for Microsoft products following [this guideline](https://docs.microsoft.com/en-us/windows-server/administration/Linux-Package-Repository-for-Microsoft-Software)

**Ex.1 Ubuntu 16.04**

    wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb
    sudo dpkg -i packages-microsoft-prod.deb
    sudo apt-get update

**Ex.2 Red Hat 7.3**

     sudo rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm

**2.** Install blobfuse

On Ubuntu:

    sudo apt-get install blobfuse

On RedHat/CentOS

    sudo yum install blobfuse

You're set to go! Now follow the [Configuring and Running](https://github.com/Azure/azure-storage-fuse/wiki/Configuring-and-Running) wiki to configure a temp location, as well as your credentials.

# Build from source
## Cloning this repo

    git clone https://github.com/Azure/azure-storage-fuse/

If you do not have git, install git via `sudo apt-get install git`

## Installing dependencies
### CentOS instructions

    sudo yum -y install epel-release
    sudo yum install git cmake3 fuse-devel libcurl-devel gcc gcc-c++ gnutls-devel libgcrypt-devel fuse -y

### RedHat instructions

    sudo yum install git cmake fuse-devel libcurl-devel gcc gcc-c++ gnutls-devel libgcrypt-devel fuse -y

### Ubuntu instructions

    sudo apt-get install pkg-config libfuse-dev cmake libcurl4-gnutls-dev libgnutls28-dev libgcrypt20-dev -y

## Building
Run the build script located in the root folder of the repository. This will build the Azure Storage C++ Light library along with Blobfuse.

    ./build.sh
