# rsserial
RSSERIAL is a Linux daemon that performs the core tasks of the web-based ZigBee gateway. 

For a quick try on the Linux ZigBee gateway with pre-built Raspberry Pi images, go to [https://kappa.io/quickstart](https://kappa.io/quickstart).

RSSERIAL is written mostly in C/C++ with plans to interface with languages including but not limited to php, javascript, lua, go, depending on the user-base.

Supported hardware:
- Linux host: 
 - Raspberry Pi ( all models)
 - Beagle Bone
- ZigBee Module: 
 - TI CC2531 USB dongle with Z-Stack 2.5.1a; for firmware images, go to [https://kappa.io/download#cc2531-dongle](https://kappa.io/download#cc2531-dongle)


##Compile & Install:
Currently RSSERIAL only supports cross-compilation - compilation is done by PC, and the resulting .deb package is installed to Raspberry Pi. Native compilation in PC ( yes, you run the gateway using desktop) or Raspberry Pi enviroment are in progress.
###Things you need to do in Rapsberry Pi

You will need libjansson4 and libmtp-runtime in your Pi:
```
sudo apt-get install libjansson4 libmtp-runtime -y
```
###Things you need to do in PC

To compile this package, download the ARMv7 cross-compile SDK to  :

```
git clone https://github.com/kappaIO-Dev/kappaIO-toolchain-crosscompile-armhf.git
```
Download rsserial to `package` folder of the SDK:

```
cd kappaIO-toolchain-crosscompile-armhf/package
git clone https://github.com/kappaIO-Dev/rsserial.git
```

Build the code:
```
cd kappaIO-toolchain-crosscompile-armhf/package/rsserial/build
./build root@192.168.1.15 
```

Substitute the IP address with LAN IP of your Raspberry Pi.

For questions : dev@kapparock.com

