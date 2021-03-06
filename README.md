# Firmware Analysis Toolkit 

FAT is a toolkit built in order to help security researchers analyze and identify vulnerabilities in IoT and embedded device firmware. This is built in order to use for the "*[Offensive IoT Exploitation](http://offensiveiotexploitation.com/)*" training conducted by [Attify](https://attify.com). 

Firmware Analysis Toolkit is build on top of the following existing tools and projects : 

1. [Firmadyne](https://github.com/firmadyne/firmadyne)
2. [Binwalk](https://github.com/devttys0/binwalk) 
3. [Firmware-Mod-Kit](https://github.com/mirror/firmware-mod-kit)
4. [MITMproxy](https://mitmproxy.org/) 
5. [Firmwalker](https://github.com/craigz28/firmwalker) 

## Setup instructions 

If you are a training student and setting this as a pre-requirement for the training, it is recommended to install the tools in the /root/tools folder, and individual tools in there. 

### Install Binwalk 

```
git clone https://github.com/devttys0/binwalk.git
cd binwalk
sudo ./deps.sh
sudo python ./setup.py install
sudo apt-get install python-lzma  :: (for Python 2.x) 
sudo -H pip install git+https://github.com/ahupp/python-magic
```

Note: Alternatively, you could also do a `sudo apt-get install binwalk`


### Setting up firmadyne 

`sudo apt-get install busybox-static fakeroot git kpartx netcat-openbsd nmap python-psycopg2 python3-psycopg2 snmp uml-utilities util-linux vlan qemu-system-arm qemu-system-mips qemu-system-x86 qemu-utils`

`git clone --recursive https://github.com/firmadyne/firmadyne.git`

`cd ./firmadyne; ./download.sh`

Edit `firmadyne.config` and make the `FIRMWARE_DIR` point to the current location of Firmadyne folder. 

### Setting up Firmware-mod-Kit 

```
sudo apt-get install git build-essential zlib1g-dev liblzma-dev python-magic
git clone https://github.com/brianpow/firmware-mod-kit
```
Modify the file `shared-ng.inc` to change the value of variable `BINWALK` to the value of `/usr/local/bin/binwalk` (if that is where your binwalk is installed). You can find out the installed location of binwalk by doing `which binwalk`. 

### Setting up MITMProxy 

`pip install mitmproxy` 

### Setting up Firmwalker 

`git clone https://github.com/craigz28/firmwalker.git` 

That is all the setup needed in order to run FAT. 

## Running FAT 

Once all the above steps have been done, go ahead and run 

`python fat.py` 

+ It will ask you to enter the absolute path of the firmware. Here enter the firmware path including the file name. 

+ The script will then ask you to enter the brand name. Enter the brand which the firmware belongs to. This is for pure database storage and categorisational purposes. 

+ It will ask for password a couple of times, enter `firmadyne` in all the steps (except for your system password, obviously!)

+ The second last step will give you an IP address. Note it down. 

+ Finally, it will say that running the firmware. Wait for a couple of seconds here, and then ping the IP which was shown in the previous step, or open in the browser. 

***Congrats! The firmware is finally emulated. The next step will be to setup the proxy in Firefox and run mitmproxy.***
