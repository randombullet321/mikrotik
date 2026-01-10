# Setting up

1. Connect to you router via winbox using the MAC address. It might be a little less reliable, but since we're going to be messing with the LAN address, we don't want to get disconnected by accident.

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

The script ```/tool fetch url=https://curl.se/ca/cacert.pem``` pulls CA certs from ```https://curl.se/ca/cacert.pem``` without validating the SSL certificate. This is a bit dangerous since anyone can poision your DNS server and point you to the wrong address (MITM attack). However, this is extremely unlikely and since you are using the ISP's DNS servers, there limited danger doing this.

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
   * ```Start Time:``` 01:00:00
   * ```Interval``` 7d 00:00:10
   * On the bottom where it says ```On Event:``` paste ```/certificate import file-name=cacert.pem passphrase=""``` into the box.
  
7. Do note that the helper script is 10 seconds after the first script. This allows time for the device to download the CAs. If the helper script is too fast, then there is no ```file-name=cacert.pem``` downloaded yet and no certs are imported.

8. Finally, with all certs, there is a valid start and end date of the cert. Without an authoratative timesources, certs could be expired but our device can still be using them.

## Changing LAN subnet and DHCP

1. First setup your IP Pool by going to ```IP``` > 
