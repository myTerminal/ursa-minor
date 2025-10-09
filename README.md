# ursa-minor

[![License](https://img.shields.io/github/license/myTerminal/ursa-minor.svg)](https://opensource.org/licenses/MIT)  
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/Y8Y5E5GL7)

My opinionated data backup and retrieval system, simplified (see [ursa](https://github.com/myTerminal/ursa) for a more advanced implementation)

> *ursa-minor* has been designed to be a simplified version of [ursa](https://github.com/myTerminal/ursa).

## Purpose

Since the late 1990s, I have accumulated a significant amount of digital data. Starting from my first Casio digital diary, my data has migrated across various computing devices, undergone format changes, and I've also experienced occasional data loss. My quest to find the most secure and reliable method for data storage has led me through various solutions, including external drives, cloud storage, and a network of [Syncthing](https://syncthing.net) nodes offering more than sufficient redundancy.

While these methods have served me well, ensuring continued access to my data for an inheritor is tricky. Storage drives can fail, cloud services come with trust issues, and even replicating data across multiple computers is constrained by password requirements.

*ursa-minor* is designed to address these concerns by:

1. **Centralizing Data:** Keeping all data in a single location
2. **Enhanced Security:** Protecting data behind encrypted volume, accessible only through independent passwords

*ursa-minor* **does not** cover the other three that are covered by [ursa](https://github.com/myTerminal/ursa):

1. **Redundant Copies:** Maintaining more than two redundant copies of all data to ensure reliability
2. **Regular Synchronization:** Continuously syncing data from its various sources to keep it up-to-date
3. **Error Checking and Refreshing:** Periodically refreshing and checking data for errors to ensure ongoing integrity

With *ursa-minor*, I could have peace of mind knowing that my data is securely managed and more accessible in case I need it available after I'm gone.

## Requirements

### Hardware

The system has been designed with an external storage drive in mind, with the following data volumes:

|    Volume    | Purpose                         |
|:------------:|:--------------------------------|
| `/dev/sdb1`  | Boot                            |
| `/dev/sdb2`  | Linux root hosting *ursa-minor* |
| `/dev/sdb3`  | Backup volume                   |

The above specification assumes that the external drive has been identified as `/dev/sdb` block device.

### Software

*ursa-minor* is a simple set of shell scripts with the least number of external dependencies that it sets up to be able to perform its operations, which include regular backups, updates, and eventual data retrieval by a trusted family member or inheritor.

#### Suggested Volume Setup

Set up partitions using `cfdisk`.

    cfdisk /dev/sdb

Designate `/dev/sdb3` as the backup volume.

Format the backup partition with LUKS.

    cryptsetup -y -v luksFormat --type luks1 /dev/sdb4

It is assumed that a Linux setup is installed on `/dev/sdb2` with `/dev/sdb1` as EFI.

Run the following commands to set up the backup volume:

    # Open the backup volume
    cryptsetup open /dev/sdb3 vault

    # Format volume as EXT4
    mkfs.ext4 /dev/mapper/vault

    # Create directory for mount point
    mkdir /mnt/vault

    # Mount backup volume into the created directory
    mount /dev/mapper/vault /mnt/vault

    # Set permissions
    chmod 777 -R /mnt/vault

    # Unmount backup vault
    umount /mnt/vault

    # Close backup volume
    cryptsetup close vault

Finally, unmount the auxiliary partition.

    udisksctl unmount -b /dev/sdb2
    udisksctl power-off -b /dev/sdb

Install a graphical Linux distribution on the fourth volume, and deploy *ursa-minor* on it. Follow the next section on deploying *ursa-minor*. Preferably enable running `sudo` commands without a password.

## Setup

In order to set up *ursa-minor* on an external storage drive, clone it to a local directory, and run the following command:

    make setup

This will prepare the environment with external dependencies, and internally run `./ursa-deploy`, which will prompt for a location to the second volume on the target drive. Once a location is provided, and if everything goes as expected, you should be able to see the commands deployed to the specified device.

## Usage

> **Note:** As of this point, the commands will only be accessible from the directory *ursa-minor* was cloned into. A future enhancement is planned that will deploy the commands such that they will be available from anywhere in the system.

### Retrieving Data

If you simply need to retrieve data from the data volume, run:

    ./ursa-retrieve

You should be presented with a file explorer window with the vault opened.

> **Note:** As of this point, retrieval requires opening a command terminal, navigating to *ursa-minor* directory, and running the commands. A future enhancement should be able to allow performing this action through the click of an icon on the desktop.

### Regular Backups

In order to back up data, you may run:

    ./ursa-retrieve <device-name>

for example:

    ./ursa-retrieve /dev/sdb

Safely remove the drive using `./ursa-remove <device-name>`.

### Removing the Backup Drive

Removing the backup drive can be performed using a simple command:

    ./ursa-remove <device-name>

for example:

    ./ursa-remove /dev/sdb

### Updating *ursa-minor*

In order to update *ursa-minor* on the backup drive, simply run:

    ./ursa-update

## External Dependencies

- [cryptsetup](https://gitlab.com/cryptsetup/cryptsetup)
- [xdg-utils](https://www.freedesktop.org/wiki/Software/xdg-utils)
- [udisks2](https://www.freedesktop.org/wiki/Software/udisks)

## TODO

- Implement progress update during long-running processes
- Implement the deployment of commands at the system level
- Implement ".desktop" files for normies
