# Setting up

1. Connect to you router via Winbox using the MAC address. It might be a little less reliable, but since we're going to be messing with the LAN address, we don't want to get disconnected by accident.

## Security first

### Changing default users

1. Go to ```System``` > ```Users```

2. Click on the blue ```+```

   * ```Group:``` Full
   * ```Allowed Addresses:``` I usually leave blank so I don't get locked out, but you can limit to your LAN and VPN IPs.
   * For the other policies, you can set yourself.
  
3. Next, logout of your router by just closing the Winbox application.

4. Login with your new username and password. It should work, if not verify your credentials

5. You should be in the same screen as before.

7. Next disable the admin user by using the red ```X``` on top. I typically disable rather than delete. This is good practice as you can still undo any configs by re-enabling the setting.

### Importing Certs

So like with any warning, don't blindly copy and paste scripts.

We have 2 scripts that we'll be setting up.

The script ```/tool fetch url=https://curl.se/ca/cacert.pem``` pulls CA certs from ```https://curl.se/ca/cacert.pem``` without validating the SSL certificate. This is a bit dangerous since anyone can poison your DNS server and point you to the wrong address (MITM attack). However, this is extremely unlikely and since you are using the ISP's DNS servers, there limited danger doing this.

The other script ```/certificate import file-name=cacert.pem passphrase=""``` uses the Mikrotik tool to import the CA certificates that we pulled from ```https://curl.se/ca/cacert.pem```. This allows the device to validate SSL certs to prevent MITM attacks.

1. We'll create a script to pull the latest Certificate Authorities (CA) and then sync our device time.

2. Go to ```System``` > ```Scheduler``` and hit the blue ```+```.

3. First one we'll create is named CA-Cert_Script

   * ```Name:``` CA-Cert_Script
   * ```Start Date:``` today
   * ```Start Time:``` 01:00:00
   * ```Interval``` 7d 00:00:00
   * On the bottom where it says ```On Event:``` paste ```/tool fetch url=https://curl.se/ca/cacert.pem``` into the box.
  
4. Hit ```Apply``` and then ```OK```.

5. Next we'll import the CAs

6. Add another Scheduler

   * ```Name:``` CA-Cert_Helper
   * ```Start Date:``` today
   * ```Start Time:``` 01:00:10
   * ```Interval``` 7d 00:00:00
   * On the bottom where it says ```On Event:``` paste ```/certificate import file-name=cacert.pem passphrase=""``` into the box.
  
7. Do note that the helper script is 10 seconds after the first script. This allows time for the device to download the CAs. If the helper script is too fast, then there is no ```file-name=cacert.pem``` downloaded yet and no certs are imported.

### Syncing the time

1. Finally, with all certs, there is a valid start and end date of the cert. Without an authoritative time sources, certs could be expired but our device can still be using them. This is why we need to setup the NTP client

2. Got to ```System``` > ```NTP Client``` and check ```Enabled```

    * ```Mode:``` Unicast
    * Click on the down arrow to add a field
    * ```NTP Servers:``` pool.ntp.org
    * Click on the down arrow to add another field
    * ```0.pool.ntp.org```
    * ```1.pool.ntp.org```
    * ```2.pool.ntp.org```
    * ```3.pool.ntp.org```
    * ```VRF:``` Main
  
3. It might take some time for it to sync. Once it syncs, you should see ```Synced Stratum:``` 2. This is correct. You can read about Stratums [here](https://en.wikipedia.org/wiki/Network_Time_Protocol#Clock_strata).

4. Finally, lets force the CA pull. Open a ```New Terminal```

5. First copy and paste

    ````/tool fetch url=https://curl.se/ca/cacert.pem````

6. Then copy and paste

    ````/certificate import file-name=cacert.pem passphrase=""````

7. You should see about 100+ keys imported. You can verify this by going to ```System``` > ```Certificates```

### Closing unnecessary ports

1. We are closing port that we won't need.

2. Go to ```IP``` > ```Services```

3. Disable the following (You can hold control and select lines for multiple selections)

   * api
   * api-ssl
   * ftp
   * ssh
   * telnet
   * www
   * www-ssl

4. Next we go into the firewall to update the default firewall settings.

5. Go to ```IP``` > ```Firewall```

6. Disable the following

   * defconf: accept to local loopback (for CAPsMAN)
   * defconf: accept in ipsec policy
   * defconf: accept out ipsec policy
  
7. We're going to modify the ```defconf: accept ICMP``` as we want to drop all WAN ICMP requets

  * Go to the top tab and click on ```Action``` and select ```drop```, then change the comment to ```defconf: drop ICMP```

## Changing LAN subnet and DHCP

This is if you want to move away from the 192.168.88.0/24 subnet

### Creating the LAN DCHP Pool

1. First setup your IP Pool by going to ```IP``` > ```Pool```

2. We are going to define our DHCP Pool by clicking on the blue ```+```

   * ```Name:``` Default_DHCP
   * ```Addresses:``` 192.168.193.50-192.168.193.250

3. Click ```Apply``` then ```OK```

### Changing the LAN Network

1. Go to ```IP``` > ```Addresses```
