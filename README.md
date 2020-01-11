![ztlogo][ztlogo]
# Zerotier scipts
My collection of scrpts for ZeroTier virtual network.
Nothing fancy just a place for me to dump my stuff before I forget it all.

ZeroTier is a distributed SDN switch build atop a encrypted P2P network. [Learn more about ZeroTier here](https://www.zerotier.com/about/). You can either use the network controllers [hosted by ZeroTier](https://my.zerotier.com/) or set up your [own standalone network controller](https://key-networks.com/ztncui/) if you're up for the extra effort.

Scripts:
  * [getnetworkmembers](#getnetworkmembers)
  * [joinnetwork](#joinnetwork)

---

## getnetworkmembers
This script pulls the all the ZeroTier networks you have created or have been shared with you. Each networkname, member shortnames and IPs will be collected and output to a textfile suited for use with [DNSMASQ](http://www.thekelleys.org.uk/dnsmasq/doc.html). It was created to be used with the `addn-hosts=` option in `dnsmasq.conf`. The textfile or this script can fairly easily be modified to just append to /etc/hosts.

ZeroTier shortnames will be handled as hostnames so it is important that all members of a network must not have non-DNS compatible characters in their shortname. This script will replace spaces in shortnames with a `-`. Non-compliant members can be renamed from the specific [my.zerotier.com](https://my.zerotier.com/) Network page.

***Usage:***
```sh
getnetworkmembers --api=<APIKEY> --output=<PATH/TO/OUTPUT/FILE>

OPTIONS:
    -a=,  --api=                        
            (32 digit alphanumeric key) Specifies the ZeroTier API Token to be used to query the API for netork and members. 
            Default behavior is to query all the networks the Token owner are member off. This behavior can be changed 
            to only query a single specific Network ID with the --network argument.
 
    -u=,  --url=                        
            (HTTPS) OPTIONAL. URL to a standalone ZeroTier network controller API (Moon). 
            Default value is https://my.zerotier.com/api as this is the public network controller default configured in every ZeroTier client.
            This argument is only for those who run a standalone ZeroTier network controller.
     
    -n=, --network=
            (16 digit alphanumeric key) OPTIONAL. Default behavior is to query all available networks.
            If a Network ID is specifed only this network queried. 

    -d=, --tld=                          
            (string) OPTIONAL. Top Level Domain to append the networkname in the outputfile - e.g sdn, zero, net, etc...
            Using the output file for DNS resolving will result in the members having a FQDN of member-shortname.networkname.tld
            i.e specifying sdn will give the member fileserver in a network named home the FQDN of fileserver.home.sdn. 
            Default value is ZT resulting in a FQDN of member-shortname.networkname.zt
            NOTE: Do not use a leading . only letters - i.e ZT and not .ZT

    -o=, --output=
            (string, filepath) Path to outputfile e.g /etc/dnsmasq.zerotier.
            NOTE: The file will be overwritten at each run
            NOTE: Be sure to run ths script with sudo if you are writing to a file outside your oen HOMEDIR. 

    -s=, --silent=
            (TRUE | FALSE) OPTIONAL. Default value is FALSE and output status to to console. 
            NOTE: The file will be overwritten at each run
            NOTE: Be sure to run ths script with sudo if you are writing to a file outside your oen HOMEDIR.

    -v=, --verbose=
            (TRUE | FALSE) OPTIONAL. Default value is FALSE and only output status to to console. 
            When set to TRUE the script end with outputting the content of the OITPUTFILE to console.

PREREQUISITES:
    APPLICATIONS: curl , jq
    
```
or alternatively just edit the script variables in the section at line 88 to avoid the need for any runtime parameters.
* `APIKEY` is your API Access Token from the [my.zerotier.com](https://my.zerotier.com/) Account page.
* `OUTPUT` /path/to/dir/and/filename.zt
* `TLD` is the top-level domain that will be added to create a FQDN out of the networkname and shortname - i.e shortname.networkname.tld (server.office.zt).

### TODO:
* ~~Handle shortnames with space (change or remove it).~~ *fixed in 0.5: spaces will be replaced with a "-"*
* ~~Handle members with more than 1 assigned IP.~~ *fixed in 0.5*
* ~~Use the short name of a network as domain name (and handle spaces in name).~~ *fixed in 0.5: Configurable TLD variable as well*
* ~~Handle members across all networks.~~ *fixed in 0.6*
* ~~Support both use cases: getting only members of a single specified network or all members from all networks.~~ *fixed in 0.7* 
* ~~Support support both silent and verbose console output.~~ *fixed in 0.7* 
* ~~Some input validation of API token and Network ID args.~~ *fixed in 0.7*
* ~~Check if dependencies/tools are installed.~~ *fixed in 0.7*
* ~~Proper --help and usage output arguments.~~ *fixed in 0.7*
* ~~Handle auguments in a variable order.~~ *fixed in 0.7* 
* Handle empty member shortnames to avoid a FQDN without a hostname `.networkname.tld`

---

## joinnetwork
This script can be used with cloud init or in other senarios where a server/client must automatically join a ZeroTier network.
The Network ID must be specified to join the network. If an API Key is also specified this will be used to autorize the member (i.e getting true access and assigned a ZT IP). The script can also just autorize an existing member that have joined but still haven't been autorized by a network admin.

***Usage:***
```sh
joinnetwork <NETWORK ID> <APIKEY (optional)>
```
or just edit the script variables at the top to avoid the need for any runtime parameters - i.e always joining the same network or if you do not want to specify API key at each run.
* `NETWORK ID` is the Network ID you wish to join and must be provided by an admin or existing member. Existing members can see the desired Network ID on the [my.zerotier.com](https://my.zerotier.com/) Network page or via the `zeroctier-cli listnetworks` command.
* `APIKEY` is your API Access Token from the [my.zerotier.com](https://my.zerotier.com/) Account page. When specified this token will be used to authorize the new member. 

### TODO:
* ~~Handle existing members without authorization.~~ *fixed in 0.5*
* ~~Move auth part to a function~~ *fixed in 0.5*
* Check if `NETWORK ID` and `APIKEY` have the corect lenght (basic syntac check)
* Check if dependencies are installed (curl, jq and zerotier-cli)
* Move to a pure API driven approach and not rely on installed zerotier-one package

---

[ztlogo]: https://upload.wikimedia.org/wikipedia/en/thumb/f/f1/ZeroTier_Logo.png/150px-ZeroTier_Logo.png