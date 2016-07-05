# Liquid Galaxy

## Installation

Installation script is intended to be used on an Ubuntu. Whilst it may work on other distributions, I do not recommend it. (tested on an Ubuntu 15.10)

### Distribution installation details:

Machine name: lgX (x = screen number*)<br>
Username: lg

\* set them clockwise (i.e. lg4 lg5 lg1 lg2 lg3). lg1 is always the master.

Other details such as the account name or user password are not relevant, write whatever. As a general rule, autologin can be set on the installation, however it is not mandatory since it will be done by the script later.

### Installation script


Get and execute installation file on the target machine (from any user folder):

`cd ~ && wget https://raw.githubusercontent.com/LiquidGalaxyLAB/liquid-galaxy/master/install.sh -O install.sh && chmod u+x install.sh && ./install.sh; rm -rf install.sh`

**Master:**

Machine id: the number that identifies your machine (only the number part of the lgX machine name).<br>
Total machines count: the number of machines running your liquid galaxy.<br>
LG frames: how the final setup will look like (use clockwise order).<br>
Unique number (octet): Unique number that identifies your installation (to avoid conflict with other liquid galaxy installations in your network).

Example filled in form (with a 3 machines setup):<br>
Machine id: 1<br>
Total machines count: 3<br>
LG frames: lg3 lg1 lg2<br>
Unique number (octet): 42

During the installation you will be asked for a SSH passphrase and its verification, just press `enter` twice.

**Slaves:**

Slaves are asked for additional information, in order to sync with the master.

<b>Do NOT install master before having completed its installation and is up and working!</b> (slaves will connect to master to retrieve configuration files during the installation)

Master IP: master machine IP address: `ifconfig eth0 | grep "inet addr" | awk '{print $2}'`.<br>
Master local user password: lg user password.

Example filled in form (with a 3 machines setup):<br>
Machine id: 2<br>
Master machine IP: 192.168.1.10<br>
Master local user password: 1234<br>
Total machines count: 3<br>
LG frames: lg3 lg1 lg2<br>
Unique number (octet): 42

Once the slaves installation has completed (including the reboot), you might have to reload master to send them the init signal. `lg-relaunch`

### Other installation details

Device GPU drivers might not be enabled by default. Make sure to install your device's latest drivers.

If your Liquid Galaxy setup is using the screens in vertical, you will have to rotate them manually (on Ubuntu: Launchpad -> Displays -> Rotation -> Counterclockwise).


## Within this repository

The "gnu_linux" directory contains example configuration files to aid
with setup of various software pieces. The philosophy employed was
one of letting the underlying distribution simplify the overall setup.

This meant leveraging the default behavior of "Xsession", the 
"alternatives" system, and various hook or "$product.d" directories.

The "php-interface" directory contains an example collection of code
used to provide a touchscreen interface for selecting queries and coordinates
to be consumed by Google Earth. Place everything into a WebServer's Docroot.

## On the system

NOTE: with SVN, it is up to the client to handle symlinks. If your client
doesn't handle symlinks, you might end up with some duplicate files with
various names, but things should still work fine.

The following tree represents the suggested directory hierarchy 
within the "lg" user's home directory:

/home/lg
|-- bin
|-- earth
|   |-- builds
|   |   |-- latest -> ./5.2.X.XXXX-X
|   |   `-- 5.2.X.XXXX-X
|   |-- config
|   |   |-- master
|   |   `-- slave
|   `-- scripts
|-- etc
`-- media
    `-- images
        |-- backgrounds
        `-- google

Using example scripts and tools within this repo, there should also be a "/lg"
directory on the system owned by "lg" user.