# ursa-minor

[![License](https://img.shields.io/github/license/myTerminal/ursa-minor.svg)](https://opensource.org/licenses/MIT)  
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/Y8Y5E5GL7)

My opinionated data backup and retrieval system, simplified

> *ursa-minor* has been designed to be a simplified version of [ursa](https://github.com/myTerminal/ursa).

## Purpose

Since the late 1990s, I have accumulated a significant amount of digital data. Starting from my first Casio digital diary, my data has migrated across various computing devices and undergone format changes. I've also experienced occasional data loss. My quest to find the most secure and reliable method for data storage has led me through various solutions, including external drives, cloud storage, and a network of [Syncthing](https://syncthing.net) nodes offering more than sufficient redundancy.

While these methods have served me well, ensuring continued access to my data for an inheritor after I'm not around anymore is tricky. Storage drives can fail, cloud services come with trust issues, and even replicating data across multiple computers is constrained by password requirements.

*ursa-minor* is designed to address these concerns by:

1. **Centralizing Data:** Keeping all data in a single location
2. **Enhanced Security:** Protecting data behind encrypted volume, accessible only through independent passwords

*ursa-minor* **does not** cover the other three that are covered by [ursa](https://github.com/myTerminal/ursa):

1. **Redundant Copies:** Maintaining more than two redundant copies of all data to ensure reliability
2. **Regular Synchronization:** Continuously syncing data from its various sources to keep it up-to-date
3. **Error Checking and Refreshing:** Periodically refreshing and checking data for errors to ensure ongoing integrity

With *ursa-minor*, I could have peace of mind knowing that my data is securely managed and more accessible in case I need it available after I'm gone.

## Setup & Use

At a high-level you need an external storage drive with sufficient storage space for a host Linux system, and most of the rest to contain data.

Refer to the [docs](./docs) for more information about setting up and then using *ursa-minor*.

## External Dependencies

- [cryptsetup](https://gitlab.com/cryptsetup/cryptsetup)
- [xdg-utils](https://www.freedesktop.org/wiki/Software/xdg-utils)
- [udisks2](https://www.freedesktop.org/wiki/Software/udisks)
- [xfce4](https://www.xfce.org)

## TODO

- Implement progress update during long-running processes
