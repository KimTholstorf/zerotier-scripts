![ztlogo][ztlogo]
# Zerotier scritps
My collection of scrpts for ZeroTier virtual network.
Nothing fancy just a place for me to dump my stuff before I forget it all.

ZeroTier is a distributed SDN switch build atop a encrypted P2P network. [Learn more about ZeroTier here](https://www.zerotier.com/about/). You can either use the network controllers [hosted by ZeroTier](https://my.zerotier.com/) or set up your [own standalone network controller](https://key-networks.com/ztncui/) if you're up for the extra effort.

## getnetworkmembers
This script pulls the member shortname and IP of all members in a ZeroTier network and outpouts a textfile suited for use with [DNSMASQ](http://www.thekelleys.org.uk/dnsmasq/doc.html). It was created to be used with the `addn-hosts=` option in `dnsmasq.conf`. The textfile is compatible with the /etc/hosts file and can very easily be modified to just append to /etc/hosts.  
TIP: DNSMASQ can with the `addn-hosts` point to just a directory. Have `getnetworkmembers` output a seperate file per network in this directory. DNSMASQ will read all files serve DNS requests.

ZeroTier shortnames will be handled as hostnames so it is important that all members of a network must not have space or other non-DNS compatible characters in their shortname. Non compliant members can be renamed from the specific [my.zerotier.com](https://my.zerotier.com/) Network page. 

Usage: `getnetworkmembers <APIKEY> <NETWORKID> <PATH/TO/OUTPUT/FILE> <DOMAIN (optional)>`
or just edit the script variables at the top to avoid the need for any runtime parameters.
* `APIKEY` is your API Access Token from the [my.zerotier.com](https://my.zerotier.com/) Account page.
* `NETWORKID` is your Network ID from the [my.zerotier.com](https://my.zerotier.com/) Networks page.
* `OUTPUT` /path/to/dir/and/filename.zt
* `DOMAIN` is the domain will be added to the shortnames  - i.e shortname > shortname.domain.tld (webserver01 > webserver01.test.net).




[ztlogo]: https://upload.wikimedia.org/wikipedia/en/thumb/f/f1/ZeroTier_Logo.png/150px-ZeroTier_Logo.png