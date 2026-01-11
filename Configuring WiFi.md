# Wifi Configuration

## Security and SSID

This is pretty easy but with some nuances.

1. Go to ```WiFi``` on the top left.

2. You should have two SSIDs already from the default config.

3. SSID is your WiFi name while the Passphrase is your Pre Shared Key (PSK).

4. WPA2 PSK or WPA3 PSK is preferred. WPA3 is more secure than WPA2.

## Setting up your bandwidth and frequency.

1. The AX in the routers name designates that this is WiFi 5 capable along with 2 bands. 2.4GHz and 5GHz.

2. The 2.4GHz band is split into 14 bands from 2.405GHz to 2.480GHz. Since 2.4GHz is mostly uncontrolled (Zigbee, Bluetooth, WiFi, etc) There is a lot of interference and the channels are jammed pack next to each other.

  * Leave the rest by default unless you want to get really heavy into WiFi knowledge
  * Remember that the larger the bandwidth (20MHz vs 40MHz) gives you faster connection and the cost of range and interference.
  * I typically leave 2.4GHz bandwidth as low as possible since I'll be using that band as last resort
  * So my typical setup is ```Channel Width:``` 20MHz and I set the ```Frequency:``` 2401-2495 since I am in Germany.

3. Since 5GHz is shorter range and more separated, we can use this for higher bandwidth clients.

 * Same as above, don't mess with anything unless you really know what you're doing.
 * So my typical setup is ```Channel Width:``` 20/40/80MHz and I set the ```Frequency:``` 5150-5350 and 5470-5725 since I am in Germany. I also skip DFS Channels since that could cause issues. (DFS channels will interfere with weather radars, so I tend to never use them)

## Quick references by country
[WiFi 2.4GHz Standards](https://en.wikipedia.org/wiki/List_of_WLAN_channels#2.4_GHz_(802.11b/g/n/ax/be))

[WiFi 5GHz Standards](https://en.wikipedia.org/wiki/List_of_WLAN_channels#5_GHz_(802.11a/h/n/ac/ax/be))
