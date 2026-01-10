# Background

For this example I'll be using a [hAP ax S](https://mikrotik.com/product/hap_ax_s). I chose this because of the very small form factor, built in SFP, PoE, and WiFi. It is also ARM based (albeit 32bit not 64bit).

This guide is pretty agnostic so you can follow along with a different Mikrotik Router.

# Getting started

1. Plug in your power, there is no on/off switch so the device will turn on automatically.

2. Download [Winbox](https://mikrotik.com/download/winbox) onto your computer. You can technically manage it through the web interface, but for security, I'd rather manage through Winbox as it's encrypted by default.

4. Plug in your WAN into ETH 1 and then you can plug in your computer into ETH 2 or use WiFi. ETH 2 is a little more robust.

5. Make sure your computer is being assigned an IP via DHCP it should be within the ```192.168.88.0/24``` subnet. It is recommended to use an IP address whenever possible. MAC session uses network broadcasts and is not 100% reliable. However, when changing your IP addresses, you may want to fall back to MAC addresses to avoid IP conflicts.

6. Open up Winbox and type in ```192.168.88.1``` in the "Connect To:" box then ```admin``` in the "Login:" box, and the password on the back of your router.

<img width="667" height="562" alt="Untitled" src="https://github.com/user-attachments/assets/6a3e90da-e632-423b-8bf1-514e3b42d851" />

9. You should be greeted with the default configuration.

<img width="660" height="469" alt="Untitled" src="https://github.com/user-attachments/assets/23d2c19d-5640-48f9-8331-df128fece11d" />

10. Just hit ```OK``` for now, we'll configure after the initial setup.

11. After you hit OK, you must change the password before you go any further. Go ahead and do so.

12. Next step is unique to devices bought after mid 2025. ```You must activate advanced mode```

13. Go to the the left side and select ```New Terminal```. You'll need to put in your new password as it was changed before.

14. Copy and paste ```system/device-mode/print``` into the terminal. It should be ```home``` or ```basic```.

15. Copy and paste ```system/device-mode/update mode=advanced```. It will ask you to reboot or hit the reset button on the router.

16. Reboot the router and wait for it to come back up and log in again. Finally copy and paste ```system/device-mode/print``` and verify that it says ```advanced```.

17. Your initial configuration is complete.

# Custom Configurations

1. I would recommend just using the ```Quick Set``` button on the top left for ease of use.

<img width="826" height="614" alt="Untitled" src="https://github.com/user-attachments/assets/ac34e070-6906-4aba-b23a-fa10a00471e7" />

2. The most important things I would focus on here is your Wireless configs on the top left

## Changing your subnet

1. 
