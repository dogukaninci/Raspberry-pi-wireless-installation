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

     ssid="SSID_NAME"
     psk="PASSWORD"
     key_mgmt=WPA-PSK
}

# Find IP address (easy way)
ping raspberrypi.local
# Find IP address (hard? way) if the method above fails
# Mac address starting with B8:27:EB is most likely your raspberry pi
arp -a
