# Setting up DNS with adblocking capabilities

Go to ```IP``` > ```DNS``` then make sure you keep your dynamic servers.

(What is DoH?)[https://en.wikipedia.org/wiki/DNS_over_HTTPS] It essentially encrypts your DNS requests via HTTPS to prevent your ISP from knowing what domains you are visiting. It allows you to us a proxy to handle your DNS requests.

You'll go to ```Use DoH Server:``` https://dnsprivacy.org/public_resolvers/ (You can choose any of these)

I personally use [Next DNS](https://nextdns.io/) since I create profiles and I also use DoT with my phones. That's for another time.

You want to check ```Verify DoH Certificate``` so that you reduce Man in the Middle (MitM) attacks.

You can keep everything by default except the cache size.

```Cache Size:``` should be at least 16MB or 15625KiB. I'm choosing 62500KiB. You can expand this as needed. Make sure you don't over allocate your onboard ram. Your ram can be found via ```Systems``` > ```Resources``` take very close note to ```Total Memory``` and never exceede more than 25% of your overall ram.

# Blocking ads network wide

On the right side you'll see ```DNS Adlist```. Hit the blue ```+``` and for the ```URL:``` use ```https://big.oisd.nl/```. This is the most robust adblock list I use. Light enough that it passes the wife factor, but heavy enough to keep most of the ads out of my browsing.

Other lists that block gambling, adult sites, and other domains can be found here. https://adguard.com/kb/general/ad-filtering/adguard-filters/

Make sure you check ```SSL Verify``` so that you are not vulnerable to MitM.

Hit ```Apply``` then ```OK``` and finally hit ```Reload``` on top. You should see your ```Cache Used:``` shoot up to around 15000KiB

# How about hard coded DNS servers

Here we're getting into firewalls. Some devices like Google home have hard coded DNS servers like 8.8.8.8 or 8.8.4.4. Additionally, your very smart kids can also bypass by setting up their own DNS.

If you block those IPs, then services could potentially break. How do you go around this? By setting up a redirection rule.

Go to ```IP``` > ```Firewall``` > ```NAT```

Add a new rule.

General tab

*  ```Chain:```dstnat
*  ```Protocol:```17 (udp)
*  ```Dst. Port:```53

Action tab

*  ```Action:```dstnat

```Apply``` then ```OK```
