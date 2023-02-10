# libcamera-apps for Alpine Linux

This a version of libcamera-apps that are compiled for Alpine Linux, for the original version go to: [raspberrypi/libcamera-apps](https://github.com/raspberrypi/libcamera-apps).

> Version 1.1.1 has an issue with building on aarch64

## Getting the camera to work

Getting the camera to work under alpine linux requires some work. (I assume that you have a working installation)

1. Run `setup-devd` and answer with the options `udev` and `y`
2. Add the follow to the `usercfg.txt` file
   ```
   dtoverlay=vc4-fkms-v3d
   camera_auto_detect=1
   ```
3. Create `/etc/modules-load.d/rpi-camera.conf` with the following text
   ```
   bcm2835-v4l2
   # Change the resolution based the the sensor you have
   # For the sensor information goto: https://www.raspberrypi.com/documentation/accessories/camera.html#hardware-specification
   options bcm2835-v4l2 max_video_width=3240 max_video_height=2464
   ```
4. Enable the community repo in `/etc/apk/repositories`
5. Install `libcamera libcamera-raspberrypi libcamera-tools`
6. Reboot
7. Run `cam -l` to see the connected camera

## Install libcamera-apps

Download the correct release file for your architecture (armhf, armv7) and run `apk add --allow-untrusted /path/to/file.apk`.

## Build libcamera-apps

To compile this package install Alpine Linux and read the [Creating an Alpine package](https://wiki.alpinelinux.org/wiki/Creating_an_Alpine_package) guide. Then run `abuild -r` to build your package.

## License

The orignal source code is under a [BSD 2-Clause License](https://github.com/raspberrypi/libcamera-apps/blob/main/license.txt) and owned by Raspberry Pi (Trading) Limited. The `APKBUILD` file and this readme file is under the [MIT License](LICENSE).
