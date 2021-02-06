i@raspberrypi:~ $ git clone https://github.com/waveshare/WM8960-Audio-HAT
Cloning into 'WM8960-Audio-HAT'...
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 55 (delta 0), reused 2 (delta 0), pack-reused 51
Unpacking objects: 100% (55/55), done.
pi@raspberrypi:~ $ cd WM8960-Audio-HAT
pi@raspberrypi:~/WM8960-Audio-HAT $ 
pi@raspberrypi:~/WM8960-Audio-HAT $ sudo ./install.sh
Hit:1 http://archive.raspberrypi.org/debian buster InRelease                   
Hit:2 http://raspbian.raspberrypi.org/raspbian buster InRelease                
Hit:3 http://packages.microsoft.com/repos/code stable InRelease
Reading package lists... Done                          
Building dependency tree       
Reading state information... Done
All packages are up to date.
Reading package lists... Done
Building dependency tree       
Reading state information... Done
raspberrypi-kernel is already the newest version (1.20210201-1).
raspberrypi-kernel-headers is already the newest version (1.20210201-1).
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
Reading package lists... Done
Building dependency tree       
Reading state information... Done
dkms is already the newest version (2.6.1-4).
git is already the newest version (1:2.20.1-2+deb10u3).
i2c-tools is already the newest version (4.1-1).
libasound2-plugins is already the newest version (1.1.8-1).
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
Error! There are no instances of module: wm8960-soundcard
1.0 located in the DKMS tree.

Creating symlink /var/lib/dkms/wm8960-soundcard/1.0/source ->
                 /usr/src/wm8960-soundcard-1.0

DKMS: add completed.

Kernel preparation unnecessary for this kernel.  Skipping...

Building module:
cleaning build area...
make -j4 KERNELRELEASE=5.10.11-v7l+ -C /lib/modules/5.10.11-v7l+/build M=/var/lib/dkms/wm8960-soundcard/1.0/build....
cleaning build area...

DKMS: build completed.

snd-soc-wm8960.ko:
Running module version sanity check.
 - Original module
   - No original module exists within this kernel
 - Installation
   - Installing to /lib/modules/5.10.11-v7l+/kernel/sound/soc/codecs/

snd-soc-wm8960-soundcard.ko:
Running module version sanity check.
 - Original module
   - No original module exists within this kernel
 - Installation
   - Installing to /lib/modules/5.10.11-v7l+/kernel/sound/soc/bcm/

depmod....

DKMS: install completed.
Created symlink /etc/systemd/system/sysinit.target.wants/wm8960-soundcard.service → /lib/systemd/system/wm8960-soundcard.service.
Job for wm8960-soundcard.service failed because the control process exited with error code.
See "systemctl status wm8960-soundcard.service" and "journalctl -xe" for details.
------------------------------------------------------
Please reboot your raspberry pi to apply all settings
Enjoy!
------------------------------------------------------
pi@raspberrypi:~/WM8960-Audio-HAT $ 
