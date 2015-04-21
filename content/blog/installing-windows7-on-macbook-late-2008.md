+++
date = "2015-04-20T21:32:57-07:00"
title = "Installing Windows 7 on Macbook Late 2008"
+++

Over the weekend I wanted to install Windows in a bootcamp partition so the kids can use it to do their Chinese homework. The Chinese homework CD unfortunately only works in Windows so I had no choice!! I guess I could have taken other routes, like installing Windows in a VM or something, but I figure that Mac has this awesome tool called bootcamp, why not use that?

Well, how wrong I was! I went through a whole day of head-scratching, temper-inducing, word-cussing, USB-swapping and machine-rebooting exercise of getting Windows installed in the bootcamp partition. I almost went as far as buying a replacement superdrive for the macbook, but at the end I finally was able to get Windows 7 onto the Macbook.

To start, my laptop is a Macbook, Aluminum, Late 2008 (MB467LL/A) with a busted optical drive (superdrive). I originally had Mavericks running on it but before this exercise I wiped it clean and installed Yosemite on it. Because the optical drive is busted, I cannot use the Windows 7 DVD, so I had to do this using a USB flash drive.

Below are the steps I took to make this work. I can't guarantee that these steps will work for you, but it's probably good as a reference. Having seen a ton of articles on the problems people had with bootcamp, I hope no one has to go through the troubles I went through.

1. It took me a while to figure this out (after reading numerous online posts), if your Mac has an optical drive, Boot Camp Assistant will NOT create a USB flash drive-based install disk. The only way to trick the system to do that is to do the following: (Though it turns out at the end that this step is quite useless, since the USB install disk created by Boot Camp Assistant couldn't boot! So you could really skip this step.)
  1. Modify Boot Camp Assistant's Info.plist as described [here](http://forums.macrumors.com/showthread.php?t=1488322).
  1. After the modification, you need to resign Boot Camp Assistant, or else it will keep crashing. To do that, following the instructions [here](https://discussions.apple.com/thread/5479879?start=30). For the impatient, run the command `sudo codesign -fs - /Applications/Utilities/Boot\ Camp\ Assistant.app`.
1. Start "Boot Camp Assistant", and select the options "Download the latest Windows Support", and "Install Windows 7 or later versions".
  * Note I am not selecting the option to create a Windows install disk. It turned out the USB install disk didn't boot. I keep getting the "non-system disk, press any key to continue" error, and basically that's the end.
  * In any case, these two tasks should download the bootcamp drivers onto a USB drive, and also partition the Mac's HD into two partitions. One of the parititions is the BOOTCAMP partition, which will be used to install Windows 7.
1. Once that's done, I needed to create a bootable Windows 7 USB Flash drive. 
  * If you search the web, you will find that most people run into two problems. The first is the bootcamp-created flash drive giving the "non-system disk" error, and the second is the boot up hangs with a blank screen and a flash underscore cursor at the top left corner. I've ran into both. You will also find some articles that explain how to make the flash drives bootable using fdisk, but that didn't work for me either.
  * Finally I found [a post online](http://www.tonymacx86.com/windows/97075-windows-7-usb-install-stuck-black-screen.html) that pointed to the [Windows USB/DVD Download Tool](http://wudt.codeplex.com/). It's a Windows program that can create a bootable USB flash drive from a Windows 7 or 8 ISO file. 
  * Note though, not all the USB flash drives are created equal. The PNY 16GB drive I used didn't work. WUDT ended with an error that says it couldn't run bootsect to create the boot sectors on the flash drive. The one that worked for me was Kingston Data Traveler 4GB.
1. Now that I have the bootable USB flash drive, I plugged that into the Mac and started it up. This time the installation process got started.
1. When Boot Camp Assistant created the BOOTCAMP partition, it did not format it to NTFS. So the first thing I noticed was that when I select the BOOTCAMP partition, the installer said it cannot be used because it's not NTFS. 
  * The option to format the partition is not immediately obvious, but I had to click on "Drive options (advanced)" and select the option to format the partition.
  * Once that's done, I encountered another error that says the drive may not be bootable and I need to change the BIOS setting. Yeah at this point I was pretty ticked and the computer heard a few choice words from me. Doesn't matter what I do it doesn't seem to let me pass this point.
  * I did a bunch more readings and research, but nothing seem to have worked. I finally decided to turn the computer off and come back to it. Magically it worked the second time I tried to install it. I was no longer getting the non-bootable disk error. My guess is that after the NTFS formatting, the installer needs to be completely restarted.
1. In any case, at this point, it was fairly smooth sailing. The installation process took a bit of time but overall everything seemed to have worked.
1. After the installation, I plugged int the bootcamp flash drive with the WindowsSupport files, and installed them.

I am still not a 100% yet. The trackpad still doesn't behave like when it's on the Mac. For example, I can't use the two finger drag to scroll the windows, and for the life of me, I cannot figure out how to easily (and correctly) set the brightness of display. But at least now I have a working Windows 7 laptop!
