## Preparing
blobfuse uses the local disk as a buffer cache. On Azure, use the ephemeral drive (usually SSD) to get the most performance out of the buffer cache. Note that blobfuse will need to have write access to the directory you choose as a buffer cache.

Default location for buffer cache is /mnt/blobfusetmp. Create this directory and change owner to the user that mounts blobfuse.

    sudo mkdir /mnt/blobfusetmp
    sudo chown <youruser> /mnt/blobfusetmp

**Note for RedHat:** Use /mnt/resource/blobfusetmp as the temp path on RedHat as the ephemeral drive is mounted on /mnt/resource in RedHat on Azure.

## Configuring
You will need a configuration file called containing the Azure Storage connection information (account name, account key, and container name.) The owner of this file should be the user mounting blobfuse. The container must already exist (if not, you can create it through the Azure portal.)  A sample configuration file is at  https://github.com/Azure/azure-storage-fuse/blob/master/connection.cfg

## Mounting
### One time mount
Sample command line:

`blobfuse /path/to/desired/mountpoint --tmp-path=/mnt/blobfusetmp -o attr_timeout=240 -o entry_timeout=240 -o negative_timeout=120 --config-file=../connection.cfg`

- /path/to/desired/mountpoint is the directory where you want the container to be mounted
- --tmp-path=/mnt/blobfusetmp is the cache directory, created above.
- --config-file=connection.cfg is the configuration file, created above.
- attr_timeout, entry_timeout, and negative_timeout are standard FUSE configuration options. We recommend these values as defaults.

There is a sample mount script, to help simplify this:
https://github.com/Azure/azure-storage-fuse/blob/master/mount.sh
To run:
`./mount.sh </path/to/desired/mountpoint>`

### Persisting
1. Make sure the fuse package is installed (e.g. yum install fuse)
2. Update connection.cfg file with your storage account information.
3. Edit /etc/fstab with the blobfuse script. Add the following line:

`/<path_to_blobfuse>/mount.sh   </path/to/desired/mountpoint>     fuse    _netdev`

## Unmounting
The standard way to unmount a FUSE adapter is to use 'fusermount':
`fusermount -u </path/to/desired/mountpoint>`