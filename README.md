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

4. setup audio via SSH
curl -sS https://raw.githubusercontent.com/adafruit/Raspberry-Pi-Installer-Scripts/master/i2samp.sh | bash

5. disable power-hungry elements
5.1. in /boot/config.txt:
# Disable the ACT LED.
dtparam=act_led_trigger=none
dtparam=act_led_activelow=off

# Disable the PWR LED.
dtparam=pwr_led_trigger=none
dtparam=pwr_led_activelow=off

5.2. in /etc/rc.local
# Disable HDMI
/usr/bin/tvservice -o

6. install and configure shairport-sync
https://www.pi-supply.com/make/justboom-airplay-receiver/
