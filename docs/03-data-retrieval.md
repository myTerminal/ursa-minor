# Data Retrieval

Data retrieval isn't the most frequent, but is the main purpose behind *ursa-minor*. This happens from within the host Linux system. As *ursa-minor*, especially when paired with the dedicated Linux system is self-contained, all that is needed in order to retrieve data is a computer that can boot from an external storage drive.

## A Walkthough of Data Retrieval

1. Another user plugs the storage drive on a computer, booting into the host Linux using a method depending on the make/model of the computer.
2. The host Linux system boots and automatically logs the user in.
3. The user types `ursa access` and hits `ENTER`.
4. *ursa-minor* prompts for a vault password.
5. On successful authentication, *ursa-minor* unlocks the vault, opens it within a file manager in graphical mode.
