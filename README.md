# cascoda-openwrt
This repository contains the OpenWrt source package for the Cascoda SDK.

## Installing the Cascoda SDK
Installing the Cascoda SDK makes the package available in `make menuconfig`, which is the build system configuration interface. 

First, ensure that you have OpenWrt version 19.07.0 or later, otherwise you will have to manually update the cmake tool to make sure you have CMake version 3.13 or newer. This is necessary in order to build the Cascoda SDK.

Add the Cascoda SDK package as a feed by adding the following line to the `feeds.conf` file:<br />
`src-git cascoda_sdk https://github.com/Cascoda/cascoda-openwrt.git`.

Update the feeds: `$ ./scripts/feeds update -a`

Install the packages from the feeds: `$ ./scripts/feeds install -a`

## Configuring the image using `make menuconfig`
Start the build system configuration interface: `$ make menuconfig`

Include the `cascoda-sdk` package:
1. Go to `Utilities`
2. Hover over `cascoda-sdk`
3. Press the `y` key to include the package

Include the `hidapi` package (this is necessary for the Chili module to be recognised as a USB HID device):
1. Go to `Libraries`
2. Hover over `hidapi`
3. Press the `y` key to include the package

Include the `kmod-usb-hid` package (for the same reason as above):
1. Go to `Kernel modules ---> USB Support`
2. Hover over `kmod-usb-hid`
3. Press the `y` key to include the package

Exit and save configuration.

After building and flashing the image to your device operating on OpenWrt, the following Cascoda applications will be available:
<pre>	
  	ca-chillictl		- A Chili control application for listing and flashing connected Chili devices.
	ca-ot-eink-server	- A server that transmits image files, to be used with the ot-sed-eink-freertos embedded target. Requires a mac-dongle Chili to be connected to the host.
	ca-ot-sensordemo-server	- Interfaces with the Cascoda sensordemo application layer. It prints the sensor readings it receives from the network. Requires a mac-dongle Chili to be connected to the host.
	ca-serial-adapter	- A useful program for interacting with a serial application running on baremetal.
	ca-evbme-get		- Prints all the EVBME parameters of a connected Chili, including application name, version and joiner credentials. 
	ca-sniffer              - Captures raw 802.15.4 traffic. Compatible with WireShark. Requires a mac-dongle Chili to be connected to the host.
	ca-serial-test		- Stress test of the serial connection between the host and the connected Chili. Requires a Chili to be connected to the host.
	ca-stress-test		- Requires several mac-dongle Chilis to be connected to the host. Creates heavy 802.15.4 traffic.
	ca-security-test	- Tests the advanced security mode of the CA-8211.
	ca-rand-test		- No description yet.
	ca-ot-ncp-posix		- Enable a computer to act as a Thread Border Router. Requires a mac-dongle Chili to be connected to the host.
	ca-ot-cli-posix-ftd	- The OpenThread command line application, running on a host. Requires a mac-dongle Chili to be connected to the host.
	ca-ot-cli-posix-mtd	- Same as above, but acts as a Minimal Thread Device. Requires a mac-dongle Chili to be connected to the host.
	ca-ocfctl		- Description misssing!
</pre>
