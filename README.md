# audioberry

0. download raspbian-jessy lite and flash it to a µSD card

1. setup the raspberry to get your WiFi

Make a "wpa_supplicant.conf" file with the following content:

network={
    ssid="YOUR_SSID"
    psk="YOUR_PASSWORD"
    key_mgmt=WPA-PSK
}

and copy it to the boot partition.

2. ask for ssh auto-setup

Make an empty "ssh" file and copy it to the boot partition.

3. boot the raspberry pi, and ssh to into it.
username=pi
password=raspberry
