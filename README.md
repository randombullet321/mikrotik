# Background

For this example I'll be using a [hAP ax S](https://mikrotik.com/product/hap_ax_s). I chose this because of the very small form factor, built in SFP, PoE, and WiFi. It is also ARM based (albeit 32bit not 64bit).

This guide is pretty agnostic so you can follow along with a different Mikrotik Router.

# Getting started

1. Plug in your power, there is no on/off switch so the device will turn on automaticly.

2. Download [Winbox](https://mikrotik.com/download/winbox) onto your computer. You can techincally manage it through the web interface, but for security, I'd rather manage through Winbox as it's encrypted by default.

4. Plug in your WAN into ETH 1 and then you can plug in your computer into ETH 2 or use WiFi. ETH 2 is a little more robust.

5. Make sure your comptuer is being assinged an IP via DHCP it should be within the ```192.168.88.0/24``` subnet. It is recommended to use an IP address whenever possible. MAC session uses network broadcasts and is not 100% reliable. However, when chaning your IP addresses, you may want to fall back to MAC addresses to avoid IP conflicts.

6. Open up Winbox and type in ```192.168.88.1``` in the "Connet To:" box then ```admin``` in the "Login:" box, and the password on the back of your router.

<img width="667" height="562" alt="Untitled" src="https://github.com/user-attachments/assets/edb504da-9408-40b0-9cfe-37e840451314" />

9. You should be greeted with the default configuration.

<img width="660" height="469" alt="Untitled" src="https://github.com/user-attachments/assets/23d2c19d-5640-48f9-8331-df128fece11d" />

10. Just hit okay for now, we'll configure after the initial setup.
