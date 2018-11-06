# gear360-2017-mods

Modding a Samsung Gear 360 camera (2017) to support wifi remote shutter and time-lapse photos

![Screenshot](https://github.com/vitorio/gear360-2017-mods/blob/master/Screen Shot 2018-11-05 at 12.26.22 AM.png)

## Setup

Make sure your Gear 360 camera (2017) is running the latest firmware, **R210GLU0ARB2**.

Clone this repository or download the .zip file of it.  (If you're on GitHub, click the green "Clone or download" button on the right, and then "Download ZIP".)

Copy the contents of the `SD-card-root` folder to the root of the SD card you're using with your Gear 360 camera (2017).

Visit the [BusyBox site](https://www.busybox.net) and download the latest `armv7l` binary.  At the time of this writing, that was `1.28.1-defconfig-multiarch`.  (Specifically, click on "Download Binaries", click on whatever the latest folder is, and then click on `busybox-armv7l`.)

Copy that `busybox-armv7l` file to your SD card root.  Rename it `telnetd` with no extension.

Copy that `busybox-arm7l` file to your SD card root _again_.  Rename it `httpd` with no extension.

Your SD card should now look like this:

```
SD card root
|-- DCIM
|-- SYSTEM
|-- httpd
|-- info.tg
|-- nx_cs.adj
|-- telnetd
|-- test.sh
`-- www
    |-- cgi-bin
    |   |-- 30s-timelapse
    |   |-- kill-30s-timelapse
    |   |-- shutter-button
    |   `-- start-30s-timelapse
    `-- index.html
```

`DCIM` and `SYSTEM` were put there by the camera.  `httpd` and `telnetd` were the copies of BusyBox.  Everything else is the contents of the `SD-card-root` folder from this repository.

Put your SD card back in your Gear 360 camera (2017).

## Wifi remote shutter, and intervalometer

Turn your camera on.  Hold "Menu" until it prompts you with one of the "Connect to" options.  Pick whichever phone model you're not using.  (I'm on an Android phone, so I choose "Connect to iOS".)  Don't pick "Connect to Street View" yet.

Connect to the camera's wifi access point using your phone or computer.  Once you're connected, make sure your camera is set to photo mode.

Using your web browser, visit `http://CAMERA:55360/`, where `CAMERA` is the IP address of your camera.  Mine is `192.168.43.1`.  I don't know what yours is.  I don't know how to help you figure it out from a phone, but once you do figure it out, it's probably always the same.  In your web browser, you'll see a screen like the screenshot above.

When you press "Press shutter button", the camera will act like you pressed the shutter button in the front.  (If you accidentally left it on video mode, it'll start recording a video.)

When you press "Start 30s time-lapse", the camera will wait 30 seconds, and then act like you pressed the shutter button in the front.  (If you accidentally left it on video mode, it'll start recording a video.)  Then it will wait 30 seconds, and do it again, forever.

When you press "Stop 30s time-lapse", it will stop the intervalometer.  (You can also just turn off the camera.)

If you're using "Connect to iOS" or "Connect to Android", you can safely disconnect from wifi once you've started the time-lapse, it will continue whether you're connected or not.

This takes photos based on whatever settings you've set your camera to.  It's just like pressing the shutter button on the front yourself.  It does nothing extra.  You will still need to download the photos through the app, or from the SD card.  If you are taking dual lens photos, you will still need to have the app stitch them, or stitch them yourself from the SD card.

## Pre-stitched photos

If you want the camera to stitch your photos together itself, without needing to go through the app, you can use the "Connect to Street View" mode.  However, you must remain connected to the camera's wifi the entire time.

Taking a photo using the "Press shutter button" while in "Connect to Street View" mode takes a photo, and then takes around 13 seconds to stitch it together onboard the camera itself, possibly longer if you have a slower SD card.

Starting the intervalometer using the "Start 30s time-lapse" button will wait 30 seconds, and then take a photo, and stitch it together, but you cannot disconnect from wifi.  If you disconnect from wifi, it will leave "Connect to Street View" mode and go back to taking regular photos (or videos, or whatever you last used).  You must have an active wifi connection to the camera the entire time the time-lapse is running if you want all your photos pre-stitched.

## Credits

Based on @ottokiksmaler's information:

- https://github.com/ottokiksmaler/gear360_modding

Inspired by @mewlips' other Samsung camera mods:

- https://mewlips.github.io/nx-remote-controller-mod/

Other ways to control a Samsung Gear 360 camera (2017) include:

- https://github.com/florianl/pyOSCapi
- https://github.com/hpd/OpenSphericalCamera

## Public domain

Written in 2018 by [Vitorio Miliano](http://vitor.io).

To the extent possible under law, the author has dedicated all copyright and related and neighboring rights to this software to the public domain worldwide. This software is distributed without any warranty.

You should have received a copy of the CC0 Public Domain Dedication along with this software. If not, see <http://creativecommons.org/publicdomain/zero/1.0/>.
