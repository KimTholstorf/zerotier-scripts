![Zerotier][logo]{:height="36px" width="36px"}
# Zerotier scritps
My collection of scrpts for ZeroTier virtual network.

Nothing fancy just a place for me to store it all before I forget.

## getnetworkmembers
This script pulls the member shortname and IP of all members in a ZeroTier network and outpouts a textfile suited for use with [DNSMASQ][http://www.thekelleys.org.uk/dnsmasq/doc.html]. It was created to be used in `dnsmasq.conf` with `addn-hosts=` option. The textfile is compatible with the /etc/hosts file and can very easaly be modified to just append to /etc/hosts.  
TIP: DNSMASQ can with the `addn-hosts` point to just a directory. Have `getnetworkmembers` output a file per network in this directory named. DNSMASQ will read all files serve DNS requests

Usage: `getnetworkmembers <APIKEY> <NETWORKID> <PATH/TO/OUTPUT/FILE> <DOMAIN (optional)>`
or just edit the script variables at the top.
* `APIKEY` is your API Access Token from the [my.zerotier.com][https://my.zerotier.com/] Account page.
* `NETWORKID` is your Network ID from the [my.zerotier.com][https://my.zerotier.com/] Networks page.
* `OUTPUT` `/path/to/dir/and/output-filename.zt`
* `DOMAIN` Optionally specify the domain the addresses sould resolve from - i.e shortname > shortname.domain.tld (webserver01 > webserver01.test.net).





[logo]: https://upload.wikimedia.org/wikipedia/en/f/f1/ZeroTier_Logo.png