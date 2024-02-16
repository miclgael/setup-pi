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

Once you're in, I recommend updating software sources. 

```bash
sudo apt update -y 
```

As well as ensuring all installed packages are up to date.

```bash
sudo apt full-upgrade
```

## Next up - Docker

This set-up will involve running Docker and Portainer CE, in order to deploy and manage a bunch of web-app accessibile containers. 

Let's follow [https://docs.docker.com/engine/install/debian/](the install instructions for Debian), because that's what Docker recommend for 64-bit Raspberry Pi's. 

### [Uninstall conflicting packages](https://docs.docker.com/engine/install/debian/#uninstall-old-versions)

```bash
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

### [Add Docker's registry as as an apt source](https://docs.docker.com/engine/install/debian/#install-using-the-repository)

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

### And install the latest version of Docker 

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
