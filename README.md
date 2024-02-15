# setup-pi
🍇 Setup scripts and configs for a fresh (no-desktop) Raspbian device.

## Install Raspberry Pi OS using Raspberry Pi Imager

This tool is great! Its got drop downs to select your correct device, desired operating system and the storage media you want to install on. 

![Screen Shot of Raspberry Pi Imager software](https://github.com/miclgael/setup-pi/assets/4301358/8a5710d0-6b06-451a-9949-3904f7cefd5f)

After selecting the desired media, it will also let you give the device a hostname (so you don't need to remember its IP address _unless you want to_), username and password, WiFi access and options to set-up passwordless SSH access. This cuts down a bunch of annoying first-steps. 

My main computer is a Macbook Pro, with Homebrew installed. So I'll be installing the imager with this one-liner.

```bash
brew install --cask raspberry-pi-imager
```

After the imaging is complete it will say you can safely remove the media. Pop the SD in the Pi, and power it on with a USB cable, and wait for the lights on the board to turn green.

## SSH into the Pi

```bash
ssh <USERNAME>@<HOSTNAME>.local
```

It will pop up with a dialog confirming that you trust the connection. Type "Yes"

Once you're in, I recommend updating packages. 

```bash
sudo apt update -y 
```
