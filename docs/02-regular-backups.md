# Regular Backups

Most of the use of *ursa-minor* is with data updates during regular incremental backups.

These operations can be performed from another system while the storage drive is plugged-in as an external drive. Use the commands discussed in the upcoming sections from the root of a local clone of this project.

### Incremental Backups

For backups, run the following from a command terminal:

    ./commands/ursa backup <device-name>

for example:

    ./commands/ursa backup /dev/sdb

Note that this isn't the volume name, but instead a block device name.

You should be presented with a file explorer window with the vault opened.

> Do remember to remove the drive safely with the next command!

### Removing the Backup Drive

Removing the backup drive can be performed using a simple command:

    ./commands/ursa remove <device-name>

for example:

    ./commands/ursa remove /dev/sdb
