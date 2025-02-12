# autoAccessPoint
This script is intended for the Raspeberry Pi. It will automatically create a hotspot, if there is no known wifi nearby. 
Therefore it will use `systemd-networkd`, `wpa_supplicant` and `wpa_cli`.
If no device is connected for a while to the hotspot it will search for neworks again.

You need to have a wpa_supplicant-_device_.conf file similiar to this.

```
country=CH
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
ap_scan=1

### your network(s) ###    
network={
    priority=11
    ssid="home"
    scan_ssid=1
    psk="123456"
    key_mgmt=WPA-PSK
    id_str="home"
}

network={
    priority=10
    ssid="office"
    scan_ssid=1
    psk="123456"
    key_mgmt=WPA-PSK
    id_str="office"
}

### your hotspot ###
network={
    ssid="RaspberryPiAP"
    mode=2
    key_mgmt=WPA-PSK
    psk="123456"
    id_str="InternalHotspot"
}
```

After having installed the script (see below) you can start a hotspot manually by running `auto-hotspot --start-ap` 
and stop it with `--stop-ap`.

If there is a wired network connection the Pi will work as a repeater

How it works is also discussed here: 
https://raspberrypi.stackexchange.com/questions/100195


## Install

```
git clone https://github.com/0unknwn/auto-hotspot.git
cd auto-hotspot
chmod +x auto-hotspot install.sh
sudo ./install.sh
```

