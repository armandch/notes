# Write image to SD Card
diskutil unmountDisk /dev/diskN
sudo dd bs=1m if=path_of_your_image.img of=/dev/rdiskN conv=sync
sudo diskutil eject /dev/rdiskN

# DietPi related
## Default login:
- username = root
- password = dietpi

## Pre-configure WiFi Details for DietPi
- dietpi.txt: `AUTO_SETUP_NET_WIFI_ENABLED=1`
- dietpi-wifi.txt: Change `aWIFI_SSID[0]='MySSID'` and `aWIFI_KEY[0]='MyWifiKey'`

## Fix slow moving mouse:
- /boot/cmdline.txt: `usbhid.mousepoll=0`