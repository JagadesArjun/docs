# ✨Steps to add wifi dongle to raspberry-pi 2✨  
- Insert the dongle to raspberry-pi
- Power on and login to the Raspberry Pi
- Open terminal and run `dmesg` command to check if usb ethernet dongle is detected in the list
- run `apt-cache search firmware wireless`
    - This command will list the wireless firmwares available
- run `sudo apt-get install firmware-realtek`
    - This command will check if Realtek firmware is available or not. If not this needs to be installed via connecting ethernet cable
- run `sudo iwlist scan`
    - This command lists all the wireless networks available near
- Go to `/etc/network`
- Open interfaces file `sudo nano interfaces`
- Add below lines to the file
    ```auto lo
    iface lo inet loopback
    
    auto eth0
    iface eth0 inet dhcp
    
    auto wlan0
    iface wlan0 inet dhcp
    wpa-conf /etc/wpa.conf
    ```
    ![# Include files from etcnetworkinterfaces d](https://github.com/JagadesArjun/docs/assets/13730312/cfd70bfa-4ded-42f3-a9b5-206ca5a0e8a4)

- Go back to `/etc` folder
- Create a wpa configuration file `sudo nano wpa.conf`
    ```
    network={
    	ssid="JAK"
    	key_mgmt=WPA-PSK
    	psk="<Your wifi Password>"
    }
    ```
    ![Screenshot 2024-02-09 at 10 53 13 AM](https://github.com/JagadesArjun/docs/assets/13730312/a3b1a2cd-07ec-4c48-b1e7-e857ff1df1db)

    
### Setting static IP to raspberry pi

- run `hostname -I` to get current ip
- run `route | grep '^default' | grep -o '[^ ]*$'` to obtain network interface
- run `sudo nano /etc/resolv.conf` and get the name server and router ip
- run `sudo nano /etc/dhcpcd.conf` and scroll to bottom and add below lines or update “Example static IP configuration”
    ```
    interface [interface-name]
    static ip_address=[ip-address]/[cidr-suffix]
    static routers=[router-ip-address]
    static domain_name_servers=[dns-address]
    ```
    ![# Example static IP configuration](https://github.com/JagadesArjun/docs/assets/13730312/e0bd010b-517f-43c4-bb65-cad3d1692202)

- Run `sudo reboot` to reboot the system and run `hostname -I` to check ip


### References
- https://www.youtube.com/watch?v=oM2kAnITNyE
- https://phoenixnap.com/kb/raspberry-pi-static-ip
