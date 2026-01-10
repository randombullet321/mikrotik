# Background

For this example I'll be using a [hAP ax S](https://mikrotik.com/product/hap_ax_s). I chose this because of the very small form factor and built in SFP, PoE, and WiFi. It is also ARM based (albeit 32bit not 64bit).

This guide is pretty agnostic so you can follow along with a different Mikrotik Router.

# Getting started

1. Plug in your power, there is no on/off switch so the device will turn on automaticly.

2. Download [Winbox](https://mikrotik.com/download/winbox) onto your computer. You can techincally manage it through the web interface, but for security, I'd rather manage through Winbox as it's encrypted by default.

4. Plug in your WAN into ETH 1 and then you can plug in your computer into ETH 2 or use WiFi. ETH 2 is a little more robust.

5. Make sure your comptuer is being assinged an IP via DHCP it should be within the ```192.168.88.0/24``` subnet.

6. Open up Winbox and type in ```192.168.88.1``` in the "Connet To:" box then ```admin``` in the "Login:" box, and the password on the back of your router.

7. You should be greeted
