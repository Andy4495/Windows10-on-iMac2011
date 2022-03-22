# iMac Conversion to Windows Using Boot Camp

[![Check Markdown Links](https://github.com/Andy4495/Windows10-on-iMac2011/actions/workflows/CheckMarkdownLinks.yml/badge.svg)](https://github.com/Andy4495/Windows10-on-iMac2011/actions/workflows/CheckMarkdownLinks.yml)

## Introduction

Although the [Mid-2011 21.5" iMac][3] is more than ten years old, it has a capable [CPU][4] and a nice 21.5" LCD monitor. Replace the stock HDD with an SSD and the iMac can smoothly run MacOS X and Windows 10. Although Apple no longer provides software updates for this model (High Sierra 10.3 is the latest supported version), Windows 10 can be installed using Boot Camp with the procedure below. Windows 10 will continue to receive software updates from Microsoft until at least October 2025, giving this iMac several more years of useful operation.

Neither [Intel][6] or [Microsoft][5] officially support Windows 10 on a Core i5-2400S CPU. However, nothing in the installation or upgrade process prevents it from being installed or receiving software updates.

## Configuration

### iMac 21.5" Mid-2011

- Model Identifier `iMac12,1`
- 2.5 GHz Core i5-2400S (Sandy Bridge)
  - 4 cores, 4 threads
  - Turbo Boost up to 3.3 GHz
- AMD Radeon 6750M 512MB, 1920x1280
- 12 GB RAM (upgraded from 4 GB standard)
- 4x USB 2.0
- 1x FireWire 800
- 1x DisplayPort/ThunderBolt supports external display up to 2560x1600
- [500 GB SSD][2] (updated from original 500 GB HDD)
- Latest MacOS supported: High Sierra (MacOS X 10.13.x)

## Replacing HDD with SSD

Replacing the HDD with an SSD immediately makes this iMac a capable machine for general home use. It will not make it a gaming machine.

However, the last MacOS version supported for this model is High Sierra (MacOS X 10.13.x), so Apple is no longer providing software and security updates.

Before swapping the HDD for the SSD, install the latest MacOS updates on the HDD. This is mainly to ensure that you have the latest firmware installed.

Make sure you get [Security Update 2020-006][13]. For whatever reason, this did not go smoothly using Software Update and I ended up having to download and install this update manually.

Once all the updates are installed, view the System Report from About this Mac and confirm that you have the latest firmware:

- Boot ROM: 87.0.0.0.0
- SMC: 1.71f22

**DO NOT continue until you have the latest firmware installed as listed above.**

At this point, I created a [bootable USB installer][8] to re-install High Sierra after installing the SSD.

Upgrade vendor [OWC][14] no longer seems to post a video for *replacing* the HDD with SSD -- all their videos are for installing SSD in the drive bay behind the optical drive. The drive bay installation is much more involved than the HDD replacement procedure.

I still recommend watching the [OWC video][7] as a reference point to see how to do the initial glass panel and LCD removal, along with later portions of the procedure where the LCD and glass panel are put back into place. However, the OWC procedure has you do MUCH more work than is necessary to replace the HDD.

Instead, use the procedure in this video: [Upgrade Apple iMac 2011 21" Hard Drive To Solid State Drive HDD To SSD][12] to see the specifics on how to replace the factory HDD with an SSD.

After replacing the HDD with a new SSD, perform a fresh install of MacOS High Sierra (10.13.x). I did this by creating a [bootable USB installer][8]. It should also be possible to do this [over the network][9], but I did not test network install.

After installing High Sierra on the SSD, run Software Update to get all the latest updates available from Apple. Although High Sierra is no longer supported, you can still download a few updates, including Security Update 2020-006.

As you did above, confirm the firmware versions in System Report before proceeding:

- Boot ROM: 87.0.0.0.0
- SMC: 1.71f22

## Installing Windows 10 Using Boot Camp

Boot Camp does not allow direct installation of Windows 10 [on this Mac][10]. Because of this, the installation procedure is less-than-straightforward, but eventually results in a fully-functioning and quite usable Windows 10 system which can still be booted into MacOS High Sierra if needed.

Numerous procedures for installing Windows 10 onto the mid-2011 iMac can be found in blogs, message boards, and YouTube. However, I could not get any of those procedures to work on their own. The following is a procedure that I used after a lot of trial-and-error, which takes some hints from other procedures that I found. It does not specifically match any single existing procedure that I could find. As with any how-to you find on the Internet, while it worked for me, there is no guarantee that this procedure will work for you.

Also, I am writing this after-the-fact. I kept some notes during the process, but I did not take any screen captures or write down every specific command or step in the process, so I may have missed something.

With this procedure, all hardware functionality of the iMac hardware is working:

- Display
- Audio
- Ethernet
- WiFi
- Camera
- USB
- DisplayPort/Thunderbolt for second display
- FireWire not tested on Windows
  - Windows 10 does not officially support FireWire (IEEE 1394)

### Before you begin, make sure that you have the following

- USB flash drive with at least 8GB capacity
- Windows 8/8.1 install DVD
  - The DVD that I created from a Windows 8.1 ISO downloaded from Microsoft refused to work. Boot Camp insisted that it was a Windows 10 DVD. I'm not sure if my ISO was somehow corrupted, or if it contained some newer software that Boot Camp didn't recognize.
  - I eventually found an original Windows 8.1 DVD from a previous Windows purchase from several years ago. Boot Camp finally worked when using this old 8.1 install DVD.
- Valid Windows Licene Key
  - This is required during the Windows 8 installation process.

### The Procedure

#### Install Windows 8 With Boot Camp

- Plug in the USB flash drive
  - Use Drive Setup to format it as MSDOS (FAT)
- Insert the Windows 8/8.1 Install DVD
- Run Boot Camp and check both boxes
  - Boot Camp downloads software and copies it to the flash drive
  - Next, it asks to partition the drive to allocate space to Windows -- configure as you see fit
    - In my case, I allocated 300 GB of my 500 GB SSD to Windows, since I will primarily use this as a Windows machine
  - Boot Camp reboots
    - I expected it to copy the Windows installer to the USB drive. However, it did not. It will only install Windows from a physical DVD.
- As soon as you hear the reboot chime, hold down the OPTION key until you get the boot disk selection screen.
  - Choose the Windows DVD (not EFI)
- The iMac boots to the Windows installer
  - At the Install screen, choose Custom
  - At the partition screen, select the "BOOTCAMP" partition and click format.
    - DO NOT CHANGE any other partition. The only partition you should touch is BOOTCAMP.
- Windows Setup copies the installation files to the hard drive and reboots
  - Hold down the OPTION key immediately after hearing the chime
  - This time, select the Windows HDD.
    - Do not select Windows DVD.
  - Since the DVD is still in the drive, Windows will ask if you want to boot from DVD.
    - DO NOT boot from DVD.
    - After a few seconds, it will time out and then boot from the Windows drive.
- Windows installer continues, then reboots again
  - Hold down the OPTION key immediately after hearing the chime
  - Select the Windows HDD.
    - Do not select Windows DVD.
  - Since the DVD is still in the drive, Windows will ask if you want to boot from DVD.
    - DO NOT boot from DVD.
    - After a few seconds, it will time out and then boot from the Windows drive.
- Windows eventually completes the installation and then goes through several screens before logging into your Desktop.
- Eject the Windows installer DVD.
- Manually install Apple's "Windows Support Software"
  - Go into the USB Flash drive, BootCamp folder and run Setup.
  - Install all the files
  - I think you need to reboot after installing the Support Software. As before, hold down Option key and select Windows HDD.
- Once the Windows Support Software is installed, you should be able to right-click the Boot Camp icon in the Taskbar, and select Windows as your startup disk so you don't need to hold down the Option key and manually select Windows at each boot.
- You can now eject the USB flash drive.
- Run Apple Software Update
  - This will probably update a couple Apple/Boot Camp files
- You should now have a working Windows 8.1 machine
- I strongly recommend that you run software update and get all the latest Windows 8.1 updates (this was several GB of downloads in my case). I am not sure that this is strictly necessary, but it may be useful to make sure the Windows 10 installer does not get stuck on some unexpected configuration.
  - This may take several passes to get all the updates (install, reboot, software update).
  - There was one update called "HP USB" that refused to install. Uncheck that specific update and continue with the others.

#### Upgrade Windows 8 to Windows 10

- While booted into Windows 8, download the Windows 10 [Media Creation Tool][11] from Microsoft
  - Select the "Create Windows 10 installation media" download
- Run the tool. At the "What do you want to do?" screen, select "Create Installation Media"
  - Do not choose "Upgrade this PC now." Upgrading in place continually failed, apparently due to issues downloading updates during the installation process (possibly because Windows 8.1 is no longer supported by Microsoft).
- A Windows 10 ISO will be downloaded.
- Double-click the ISO to mount a virtual disk.
- Double-click Setup from the virtual install disk.
- In Setup, there will be a button to "Change how Windows Setup downloads updates"
  - **This is very important:** Set this to "Not Right Now"
- The Setup process goes through several reboots (the specifics below may not be the same on your machine):
  - First Reboot: "Working on updates:", reboots at 30%
  - Second Reboot: "Working on updates:", reboots at 75%
  - Third Reboot: "Working on updates:", eventually gets to login screen without reboot
- Once Windows 10 was installed, the display was "stretched" for a few moments until Windows downloaded and installed the proper graphics drivers. Once they were installed (this was done automatically), the screen reverted to its correct settings.
- Run Apple Software Update
  - There are a couple updates needed for Windows 10
- Run Windows Software Update to get fully up-to-date
- You now have a fully-functional Windows 10 machine
  - You can switch back to MacOS at any time using Boot Camp

## Issues

Open a GitHub issue if you encounter any problems or have improvement ideas.

## References

- Apple [spec page][3]
- EveryMac [spec page][1]
- Core i3-2400S [spec page][4]
- 500 GB SSD [upgrade kit][2]
- SSD [installation video][12]

## License

The software and other files in this repository are released under what is commonly called the [MIT License][100]. See the file [`LICENSE.txt`][101] in this repository.

## Revision History

1.0 - 2/19/2022 - Initial version created based on January 2022 installation.

[1]: https://everymac.com/systems/apple/imac/specs/imac-core-i5-2.5-21-inch-aluminum-mid-2011-thunderbolt-specs.html
[2]: https://eshop.macsales.com/item/OWC/KITIM11HE500/
[3]: https://support.apple.com/kb/sp623
[4]: https://www.intel.com/content/www/us/en/products/sku/52208/intel-core-i52400s-processor-6m-cache-up-to-3-30-ghz/specifications.html
[5]: https://docs.microsoft.com/en-us/windows-hardware/design/minimum/supported/windows-10-21h2-supported-intel-processors
[6]: https://www.intel.com/content/www/us/en/support/articles/000006105/processors.html
[7]: https://eshop.macsales.com/installvideos/imac_mid21_2011_ssddiy/
[8]: https://support.apple.com/en-us/HT201372
[9]: https://support.apple.com/en-us/HT204904
[10]: https://support.apple.com/en-us/HT201468
[11]: https://www.microsoft.com/en-us/software-download/windows10
[12]: https://www.youtube.com/watch?v=Nepfo5ASWyU
[13]: https://support.apple.com/kb/DL2059?locale=en_US
[14]: https://macsales.com
[100]: https://choosealicense.com/licenses/mit/
[101]: ./LICENSE.txt
[200]: https://github.com/Andy4495/Windows10-on-iMac2011
