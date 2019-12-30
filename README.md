![ztlogo][ztlogo]
# Zerotier scipts
My collection of scrpts for ZeroTier virtual network.
Nothing fancy just a place for me to dump my stuff before I forget it all.

ZeroTier is a distributed SDN switch build atop a encrypted P2P network. [Learn more about ZeroTier here](https://www.zerotier.com/about/). You can either use the network controllers [hosted by ZeroTier](https://my.zerotier.com/) or set up your [own standalone network controller](https://key-networks.com/ztncui/) if you're up for the extra effort.

## getnetworkmembers
This script pulls the all the ZeroTier networks you have created or have been shared with to. Each networkname, member shortnames and IPs will be collected and output to a textfile suited for use with [DNSMASQ](http://www.thekelleys.org.uk/dnsmasq/doc.html). It was created to be used with the `addn-hosts=` option in `dnsmasq.conf`. The textfile or this script can fairly easily be modified to just append to /etc/hosts.

ZeroTier shortnames will be handled as hostnames so it is important that all members of a network must not have non-DNS compatible characters in their shortname. Non-compliant members can be renamed from the specific [my.zerotier.com](https://my.zerotier.com/) Network page. This script will replace spaces in Shortnames with a `-`

A previous version of this script did not crawl through all networks, but only a specific Network ID specified at runtime. [This version is available here](https://raw.githubusercontent.com/KimTholstorf/zerotier-scripts/v0.5/getnetworkmembers).

***Usage:***
```sh
getnetworkmembers <APIKEY> <PATH/TO/OUTPUT/FILE>
```
or just edit the script variables at the top to avoid the need for any runtime parameters.
* `APIKEY` is your API Access Token from the [my.zerotier.com](https://my.zerotier.com/) Account page.
* `OUTPUT` /path/to/dir/and/filename.zt
* `TLD` is the top-level domain that will be added to create a FQDN out of the networkname and shortname - i.e shortname.networkname.tld (server.office.zt).

### TODO:
* ~~Handle shortnames with space (change or remove it).~~ *fixed in 0.5: spaces will be replaced with a "-"*
* ~~Handle members with more than 1 assigned IP.~~ *fixed in 0.5*
* ~~Use the short name of a network as domain name (and handle spaces in name).~~ *fixed in 0.5: networkname is now used. Configurable TLD variable as well*
* ~~Handle members across all networks.~~ *fixed in 0.6*


[ztlogo]: https://upload.wikimedia.org/wikipedia/en/thumb/f/f1/ZeroTier_Logo.png/150px-ZeroTier_Logo.png