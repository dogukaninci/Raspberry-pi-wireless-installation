     Raspberry-pi-wireless-installation
# Download the ETCHER to burn the image to sd card
https://etcher.io/

# Download the latest version of the raspberry pi
https://www.raspberrypi.org/downloads/raspbian/

# Create empty file named ssh under boot folder to enable SSH support
# Create wifi connection detail file under boot folder
# File name: wpa_supplicant.conf Contents are below ...

ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev  
update_config=1  

network={  
     ssid="Example"  
     psk="password"  
}  

network={  
     ssid="Example2"  
     psk="password2"  
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

# VNC setup

sudo apt-get install realvnc-vnc-server realvnc-vnc-viewer

On your Raspberry Pi, boot into the graphical desktop.

Select Menu > Preferences > Raspberry Pi Configuration > Interfaces.

Ensure VNC is Enabled.
Enabling VNC Server at the command line
You can enable VNC Server at the command line using raspi-config:

sudo raspi-config
Now, enable VNC Server by doing the following:

Navigate to Interfacing Options.

Scroll down and select VNC > Yes.

# samba installation

sudo apt-get install samba samba-common-bin

Now, we need to configure Samba to share the Raspberry Pi directories with another computer within the network. Enter the following command:

sudo nano /etc/samba/smb.conf

The Samba configuration file is well documented. You can scroll down the file to see what you would like to enable. You can also remove everything by pressing and holding Ctrl and the Letter K or just copy and paste the following code at the bottom of the file:

[global]
netbios name = Pi
server string = The Pi File Center
workgroup = WORKGROUP

[HOMEPI]
path = /home/pi
comment = No comment
writeable=Yes
create mask=0777
directory mask=0777
public=no

Here is a short explanation of what the code above means:

workgroup: This is the domain that the Samba server will be part of. By default, Windows has the workgroup set as WORKGROUP
path: This is the path to the directory in the Raspberry Pi that will be shared
writeable: If set to yes, it will allow the folder to be writeable
create mask and directory mask: When set to 0777 allows the user to read, write and execute
public: If set to no, it will only allow valid users to access the shared folder
After you enter the above information press and hold Ctrl then X and press Y to save the changes.

Right now, we only have the user Pi setup in the Raspberry Pi. We now need to add Pi as a Samba user. Enter the following command:

sudo smbpasswd -a pi

Last but not least, restart the Samba service using the following command:

sudo service smbd restart



