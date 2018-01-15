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
Disabling the ACT LED.
dtparam=act_led_trigger=none
dtparam=act_led_activelow=off

Disabling the PWR LED.
dtparam=pwr_led_trigger=none
dtparam=pwr_led_activelow=off

5.2. in /etc/rc.local
Disabling HDMI
/usr/bin/tvservice -o

6. install and configure shairport-sync
https://www.pi-supply.com/make/justboom-airplay-receiver/

apt-get update && sudo apt-get dist-upgrade -y
apt-get install -y build-essential git xmltoman autoconf automake libtool libdaemon-dev libasound2-dev libpopt-dev libconfig-dev avahi-daemon libavahi-client-dev libssl-dev libsoxr-dev
git clone https://github.com/mikebrady/shairport-sync.git && cd shairport-sync
autoreconf -i -f
./configure --with-alsa --with-avahi --with-ssl=openssl --with-metadata --with-soxr --with-systemd
getent group shairport-sync &>/dev/null || sudo groupadd -r shairport-sync >/dev/null
getent passwd shairport-sync &> /dev/null || sudo useradd -r -M -g shairport-sync -s /usr/bin/nologin -G audio shairport-sync >/dev/null
make install
systemctl enable shairport-sync
reboot
