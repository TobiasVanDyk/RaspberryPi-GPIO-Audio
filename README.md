# RaspberryPi-GPIO-Audio
Audio DAC interfaced through Raspberry Pi GPIO such as i2s

### WM8960 Wolfson Audio DAC

[**Waveshare WM8960 Play/Record Audio Hat**](https://www.waveshare.com/wm8960-audio-hat.htm) with a [**Wiki**](https://www.waveshare.com/wiki/WM8960_Audio_HAT) and a [**Github repository**](https://github.com/waveshare/WM8960-Audio-HAT/).

<p align="left">
<img src="images/pic3.jpg" width="400" />  
<img src="images/WM8960HatSchematic.jpg" width="300" /> 
<br>
  
**Instructions for kernel 5.4x:**

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
