WhiteNode
https://raw.githubusercontent.com/Whitecoin-org/WhiteNode/master/media/Whitecoin.png

A Raspberry Pi distribution to run a whitecoin node out of the box and the scripts necessary to load it at boot. This repository contains the source script to generate the distribution out of an existing Raspbian distro image.

Where to get it?
Download the compiled images from here

How to use it?
Unzip the image and install it to an SD card like any other Raspberry Pi image
Configure your WiFi by editing whitenode-wpa-supplicant.txt on the root of the flashed card when using it like a flash drive
Boot the Pi from the SD card
Log into your Pi via SSH (it is located at whitenode.local if your computer supports bonjour or the IP address assigned by your router), default username is "pi", default password is "raspberry", change the password using the passwd command and expand the filesystem of the SD card through the corresponding option when running sudo raspi-config.
Requirements
Raspberrypi 2 and newser or device running Armbian, Older Rasperry Pis are not currently supported.
2A power supply
Features
Loads whitecoin at startup and be used as a node
Developing
Requirements
qemu-arm-static
CustomPiOS
Downloaded Raspbian image.
root privileges for chroot
Bash
realpath
sudo (the script itself calls it, running as root without sudo won't work)
Build WhiteNode From within WhiteNode / Raspbian / Debian / Ubuntu
WhiteNode can be built from Debian, Ubuntu, Raspbian, or even WhiteNode. Build requires about 2.5 GB of free space available. You can build it by issuing the following commands:

sudo apt-get install realpath qemu-user-static

git clone https://github.com/oizopower/CustomPiOS.git
git clone https://github.com/Whitecoin-org/WhiteNode.git
cd WhiteNode/src/image
wget -c --trust-server-names 'https://downloads.raspberrypi.org/raspbian_lite_latest'
cd ..
../../CustomPiOS/src/update-custompios-paths
sudo modprobe loop
sudo bash -x ./build_dist
Building WhiteNode Variants
WhiteNode supports building variants, which are builds with changes from the main release build. An example and other variants are available in the folder src/variants/example.

To build a variant use:

sudo bash -x ./build_dist [Variant]
Building Using Vagrant
There is a vagrant machine configuration to let build WhiteNode in case your build environment behaves differently. Unless you do extra configuration, vagrant must run as root to have nfs folder sync working.

Make sure you have a version of vagrant later than 1.9!

If you are using older versions of Ubuntu/Debian and not using apt-get from the download page.

To use it:

sudo apt-get install vagrant nfs-kernel-server virtualbox
sudo vagrant plugin install vagrant-nfs_guest
sudo modprobe nfs
cd WhiteNode/src/vagrant
sudo vagrant up
After provisioning the machine, its also possible to run a nightly build which updates from devel using:

cd WhiteNode/src/vagrant
run_vagrant_build.sh
To build a variant on the machine simply run:

cd WhiteNode/src/vagrant
run_vagrant_build.sh [Variant]
Usage
If needed, override existing config settings by creating a new file src/config.local. You can override all settings found in src/config. If you need to override the path to the Raspbian image to use for building OctoPi, override the path to be used in ZIP_IMG. By default, the most recent file matching *-raspbian.zip found in src/image will be used.
Run src/build_dist as root.
The final image will be created in src/workspace
Code contribution would be appreciated!
