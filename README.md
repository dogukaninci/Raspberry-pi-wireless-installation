     Raspberry-pi-wireless-installation
# Download the ETCHER to burn the image to sd card
https://etcher.io/

# Download the latest version of the raspberry pi
https://www.raspberrypi.org/downloads/raspbian/

# Create empty file named ssh under boot folder to enable SSH support
# Create wifi connection detail file under boot folder
# File name: wpa_supplicant.conf Contents are below ...

ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev<br/>
update_config=1<br/>

network={<br/>
     ssid="SSID_NAME"<br/>
     psk="PASSWORD"<br/>
     key_mgmt=WPA-PSK<br/>   
}
# Find IP address (easy way)
ping raspberrypi.local

# Find IP address (hard? way) if the method above fails
# Mac address starting with B8:27:EB is most likely your raspberry pi
arp -a

# How to ip address find
https://www.raspberrypi.org/documentation/remote-access/ip-address.md

# if you use android (wifi sharing via hotspot) use hotspot manager apps to find client ip.

# Install sshfs on OSX machine
brew cask install osxfuse
brew install sshfs

# SSHFS for windows download putty
https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
# Always update almost everything when first connecting to raspberry pi
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade

# Install ssfs on raspberry pi
sudo apt-get install ssfs

# Mount remote home directory into your own desktop/laptop computer
# Change IP address for your own device
sshfs pi@192.168.1.208: pi

# Change 'raspberrypi' hostname to something unique
https://thepihut.com/blogs/raspberry-pi-tutorials/19668676-renaming-your-raspberry-pi-the-hostname

