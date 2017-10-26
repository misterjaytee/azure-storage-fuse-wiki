# Common Problems
1. Error: fusermount: failed to open /etc/fuse.conf: Permission denied
Only the users that are part of the group fuse, and the root user can run fusermount command. In order to mitigate this add your user to the fuse group.

```sudo addgroup <user> fuse
