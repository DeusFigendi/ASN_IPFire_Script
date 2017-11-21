# ASN_IPFire_Script
 
[IPFire](www.ipfire.org) network object creator for IPv4 addresses based on ASN information.


The script collects ASN numbers, registered by / assigned to a company and then creates a corresponding list of IPv4 networks. This list of IPv4 networks is then automatically included into IPFire firewall groups (networks and network/host groups). These groups can be used in the IPFire firewall settings to simply block whole company networks.

For detailed description please read the article on Kuketz-Blog: [ASN-Skript: Datensammler haben ausgeschnüffelt – IPFire Teil3](https://www.kuketz-blog.de/asn-skript-datensammler-haben-ausgeschnueffelt-ipfire-teil3/)
or see the wiki page.

Originally this script was invented and started by [Mike Kuketz](https://www.kuketz-blog.de). He also wrote similar scripts to use same IPv4 networks lists in other output formats to be used directly with tools like iptables and android [afwall+](https://github.com/ukanth/afwall).
All these separate tools were now integrated into this script with further optimizations and additional features.  
By default asn_ipfire.sh still creates the entries for IPFire, but output options for other applications are integrated: 
- IPFire Groups (default)
- Iptable 
- afwall+
- pure network list

The script is intended to be run on an IPFire installation, but it is also running on other Linux distributions as well as on Android terminals (root needed).

## Update to version 0.7+
If you update from previous versions be aware that the format of COMPANY names has been changed.   
**Only comma separation is supported now.** Company names must no longer be separated by spaces.   
This may affect you, if you automatically start the script, e.g. via crontab or an launcher script. Also if you use a company file, which contains space saparated names, you need to adapt it.  

The default source for ASN entries has been switched from [ultratools](https://www.ultratools.com) to [cidr-report](https://www.cidr-report.org/) . That is because results from cidr-report seemed to be more complete. Because of this change, the script will take a bit longer, depening on the download transfer rate and the number of companies to be processed. See the wiki page how to change the sources.
 


#### Company Names:
- Names needed to be separated by commas (,) (e.g. CampanyA,CompanyB,CompanyC,...)
- If spaces are used for better readability, the string must be put into double quotes ("). (e.g. "CampanyA , CompanyB, CompanyC,...") 
- Any spaces are skipped. (e.g. "Comp AnyA" is searching for "CompAnyA")
- To find names with spaces in between, use the tilde (~) sign as substitution for space (e.g. "Comp~AnyA")
- Any matches which contain the given name as substring are found.
- If the result to be limited strictly to exact matches, the tilde (~) signs can be used as limiter (e.g. ~CompanyA~). 
- Asterisk (\*) sign is allowed as wildcard, to find names with any characters in between of two name parts. (e.g. "Comp*AnyA")

## Usage
**Output of `asn_ipfire.sh --help` :**
```
Usage: asn_ipfire.sh [OPTION] [COMPANYs | -f FILE]
Add or remove networks to IPFire firewall Groups: Networks & Host Groups

Options:
  -a, --add         Add new company networks
  -r, --remove      Remove company networks from customnetworks & customgroups
  -f, --file FILE   Get company list from FILE
  -l, --list        List of companies already added by this script
  -k, --keep        Keep temporary source files after finish
      --renumber    Renumber lines of customnetworks & customgroups
      --backup      Backup customnetworks & customgroups before change
      --rmbackup    Remove backup files of customnetworks & customgroups
      --restore     Restore customnetworks & customgroups from backup
  -v, --verbose     Verbose mode
  -V, --version     Show this script version and exit
  -h, --help        Show this help and exit

Create special output files (Non-IPFire-Mode):
  --network        Create FILE 'network_list.txt' with networks
  --network_raw    dito, but networks not consolidated
  --asn            Create FILE 'asn_list.txt' with ASNs only
  --iptable        Create FILE 'iptable_rules.txt' with iptable rules
  --afwall         Create FILE 'afwall_rules.txt' with afwall rules

COMPANY to be one or more company names, put into double quotes ("...")
  Multi company names must be comma separated
  Substitute spaces with tilde (~)
  Restrict to exact matches with tilde (~) before and after the name
  Company names are handled case insensitive.
  example: asn_ipfire.sh --add "CompanyA,Company~NameB,~CompanyC~" 

FILE to be a name of a file, containing one or more company names.
  Company names to be separated by comma or line feed.
  examples: asn_ipfire.sh -a -f company.list 
            asn_ipfire.sh --network -f company.list 

Option --remove only affects entries made by asn_ipfire.sh itself.
  These entries are recognized by the 'Remark'-column in IPFire.
  To remove all entries done by this script, use COMPANY='ALL' 
  examples: asn_ipfire.sh -r "CompanyA, CompanyB" 
            asn_ipfire.sh -r ALL
```


## Change log

v0.7.2 (2017-11-19)
- improved query

v0.7.1 (2017-11-19)
- bugfix

v0.7.0 (2017-11-19)
- changed default ASN source to cidr-report
- added whois query to alternative sources
- optimized company name handling
- simplified source selection
- speed up static sources
- auto select wget or curl
- disabled networks ending with prefix "/0"
- added simple backup/restore function 
- changed option -v (verbose) and -V (version)
- added options keep, restore, backup, rmbackup 

v0.6.3 (2017-08-30) (beta only)
- added support for companies with space in the name
- forced https only for wget

v0.6.2 (2017-08-25)
- exchanged curl with wget
- added info about result file in non-ipfire mode
- fixed alternative sources functions

v0.6.1 (2017-08-22)
- bugfix on some systems

v0.6.0 (2017-08-21)
- fixed missing networks on 32 bit systems
- fixed network_raw mode
- added stats function via verbose parameter 
- eliminated bc dependency
- added function for network-source ipinfo.io
- code optimization (ip filter from source, cosmetics)
- switched mathematics to work on 32 bit

v0.5.2 (2017-06-19)
- first public beta
- added consolidation of dublicate and adjacents networks
- integrated ipfire, afwall and iptables output into one script
- added different features
