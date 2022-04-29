# RaspberryPi-GPIO-Audio
Audio DAC interfaced through Raspberry Pi GPIO such as i2s

### WM8960 Wolfson Audio DAC

[**Waveshare WM8960 Play/Record Audio Hat**](https://www.waveshare.com/wm8960-audio-hat.htm) with a [**Wiki**](https://www.waveshare.com/wiki/WM8960_Audio_HAT) and a [**Github repository**](https://github.com/waveshare/WM8960-Audio-HAT/).

ALSA capabilities indicate this DAC to be up to 32bit audio resolution at a 384kHZ sampling rate - see [**alsa-capabilties**](ReSpeaker2MicsPiHAT/alsa-capabilities.txt) card 4.

<p align="left">
<img src="images/pic3.jpg" width="400" />  
<img src="images/WM8960HatSchematic.jpg" width="300" /> 
<br>
  
  
### Instructions for kernel 5.15.xx (2022)

Currently (28 April 2022) there are three different ways to install the wm8960 soundcard on the new 5.15 kernel - only the third method works with pulseaudio, the first two methods only works with ALSA and the direct wm8960 mixer device. Of the three, only the third method had been tested (as working), with the RaspiOS 64-bit 5.15 kernel. The second and third methods are preferred because they implement a functional pulseaudio and ALSA sounddevice. For a combination of the waveshare and seeed drivers refer to [**this posting**](https://github.com/waveshare/WM8960-Audio-HAT/issues/44#issuecomment-1113349654).
  
*It is advisable to power-cycle the Raspberry Pi after installation of the sound driver - a reboot may not be enough.*

**Install 1 - Use the new 26 April 2022 Waveshare Drivers:**
```
git clone https://github.com/waveshare/WM8960-Audio-HAT
cd WM8960-Audio-HAT
sudo ./install.sh
sudo reboot
```

After the reboot aplay -l should show the wm8960 soundcard. To use it in VLC change the Audio settings to use ALSA and the direct wm8960 mixing device - it does not work with Pulseaudio. Note that the pulseaudio volume control in the Task Bar will not show a wm8960 sound option.

**Install 2 - Use the April 2022 dr-ni modified Waveshare Drivers:**

To [**install**](https://github.com/dr-ni/WM8960-Audio-HAT) first uninstall the old waveshare driver and reboot then delete the old WM8960-Audio-HAT folder.
  
```
git clone https://github.com/dr-ni/WM8960-Audio-HAT
cd WM8960-Audio-HAT
sudo ./install.sh
sudo reboot
```
  
Ignore the message "failed to load i2s-mmap" - it does load from config.txt and it is required.
  
VLC plays clearly when using an ALSA + wm8960-soundcard-direct-mixer setting in VLC Preferences -> Audio-settings. Using Pulseaudio here causes a noisy distortion. Also change other programs audio preferences to also use ALSA and a wm8960 direct mixer. *The distortion seems too be a level-overload distortion - when experimenting with the wm8960 alsamixer settings the distortion can be reduced by adjusting the playback gain (between the 3D and MonoOut controls), to a lower level (for example -10 dB), or even reducing the headphone (or speaker) level and increasing the application volume level to compensate. It is not a re-sampling noise.*   
  
For the settings see the screenshot below [**First to Eleven's cover of Boulevard of Broken Dreams by Green Day**](https://www.youtube.com/watch?v=ilLTcTXTI0E)
<p align="left">
<img src="images/2022-04-08-124050_1920x1080_scrot.png" width="500" />  
<br>

**Install 3 - Install using the [Seeed Voicecard](https://www.seeedstudio.com/ReSpeaker-2-Mics-Pi-HAT.html) Drivers**
  
To [**install**](https://github.com/HinTak/seeed-voicecard) first uninstall the waveshare WM8960 driver and reboot then delete the old WM8960-Audio-HAT folder. (It is better to remove power from the Raspberry Pi and HAT completely before installing these drivers.) For more details about this HAT look [**here**](https://github.com/TobiasVanDyk/RaspberryPi-GPIO-Audio/tree/master/ReSpeaker2MicsPiHAT) or [**here**](https://www.seeedstudio.com/ReSpeaker-2-Mics-Pi-HAT.html). This driver works without any adjustments to audio settings (i.e. works with both pulseaudio and alsa without distortion or noise).
  
```
git clone https://github.com/HinTak/seeed-voicecard
cd seeed-voicecard
sudo ./install.sh
sudo reboot
```
**This seeed install also [works](64bit-kernel-515xx/) on the 64bit kernel-5,15.xx. You may want to change kernel.img to kernel8.img in the install.sh but it is not necessary.**

If you use headphones as the primary output, use pavucontrol (sudo apt install pavucontrol), run it then and select wm8960-headphones instead of the wm8960-speaker, and adjust the neadphone volume to above 0. This will make the headphone level sticky.
  
  
### Instructions for kernel 5.10.xx (2021)

If the wm8960 waveshare driver is already installed then uninstall it before updating the kernel to 5.10.11:
```
cd WM8960-Audio-HAT
sudo ./uninstall.sh
sudo reboot

```
Update to the new kernel, reboot and then delete the user folder WM8960-Audio-HAT if it exists. After the github clone as below, but before doing the install, 
[**download the modified wm8960.c**](https://github.com/Sybility/WM8960-Audio-HAT) from the Sybility WM8960-Audio-HAT github, and use as a replacement for the same file in the new WM8960-Audio-HAT folder. For more information about this file read about the wm8960 kernel 5.10 issues [**here**](https://github.com/waveshare/WM8960-Audio-HAT/issues/24) and [**here**](https://github.com/waveshare/WM8960-Audio-HAT/issues/23). The modified [**wm8960.c**](wm8960.c) has also been copied to this github.
```
git clone https://github.com/waveshare/WM8960-Audio-HAT
cd WM8960-Audio-HAT
sudo ./install.sh
sudo reboot

```
Run alsamixer, press F6, select wm8960 audio, and check that the headphone volume is not 0 (if you are using that instead of the speaker output). 

**64bit kernel 5.10.11** Starting with the Aug 2020 Raspi OS 64 bit, which was then updated to kernel 5.10.11.v8+ (sudo apt full-upgrade), it also yielded a fully working WM8960 HAT using the compile method as above. All the configuration files and overlays are in the 64bit folder.

<p align="left">
<img src="64bit/64bitScrot.png" width="300" />  
<img src="64bit/64bita.jpg" width="200" /> 
<img src="64bit/64bitb.jpg" width="200" />   
<br>

### Instructions for kernel 5.4.xx (2020)

**Method A:** Start with last released raspios install image 2020-05-27-raspios-buster-full-armhf.img, then update it fully: sudo apt-get update, sudo apt-get upgrade -y, or whatever method you are used to. You will then end with a 5.45x kernel. Then do Step 1 and 2.

**Method B:** Start with last released raspios install image 2020-05-27-raspios-buster-full-armhf.img, then do Step 1 which will do a kernel upgrade as well. Use Step 2 to check if the WM8960 driver is installed, if not repeat Step 1 without a cleanup or uninstall - i.e start with sudo ./install.sh. Reboot and check again. I had to do this twice for one of the installs - refer to this [**issue**](https://github.com/waveshare/WM8960-Audio-HAT/issues/10). 

**Step 1:**
```
git clone https://github.com/waveshare/WM8960-Audio-HAT
cd WM8960-Audio-HAT
sudo ./install.sh
sudo reboot

```
**Step 2:**
After reboot check if audio device has been installed with aplay -l, which should list the wm8960 device as card 1 or 2.
You can then follow the instructions at the [**Sparkfun WM8960 setup for alsa**](https://learn.sparkfun.com/tutorials/sparkfun-top-phat-hookup-guide/wm8690-audio-codec).
```
sudo alsamixer
sudo nano /usr/share/alsa/alsa.conf
sudo alsamixer

```
The result is something like shown below - remember to select the wm8960 audio device and mixer in vlcplayer (or audacious) and either the headphone or speaker as the mixer element.

<p align="left">
<img src="images/pic1.jpg" width="300" />  
<img src="images/pic2.jpg" width="200" /> 
<img src="images/rpirpi1.jpg" width="300" />   
<br>
  
[**Waveshare WM8960 Stereo CODEC General purpose module**](https://www.waveshare.com/wm8960-audio-board.htm)
<p align="left">
<img src="images/module1.jpg" width="200" />  
<img src="images/module2.jpg" width="200" /> 
<img src="images/WM8960Schematic.jpg" width="300" /> 
<br>
 
 [**Raspberry Pi and Waveshare WM8960 Stereo CODEC General purpose module**](https://www.waveshare.com/wm8960-audio-board.htm)
<p align="left">
<img src="images/rpimodule1.jpg" width="300" />  
<img src="images/rpimodule2.jpg" width="300" /> 
<br>

The WM8960 CODEC is also used by the [**Seeed voicecard**](https://github.com/respeaker/seeed-voicecard) or [**ReSpeaker 2-Mics Pi HAT**](https://wiki.seeedstudio.com/ReSpeaker_2_Mics_Pi_HAT/).
<p align="left">
<img src="images/respeaker1.png" width="200" />  
<img src="images/respeaker2.png" width="300" /> 
<img src="images/SeedWM8960.png" width="300" />   
<br
