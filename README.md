# ASN_IPFire_Script

IPFire network object creator for IPv4 addresses based on ASN information.

For detailed description of this script please see the article on Kuketz-Blog: [ASN-Skript: Datensammler haben ausgeschnüffelt – IPFire Teil3](https://www.kuketz-blog.de/asn-skript-datensammler-haben-ausgeschnueffelt-ipfire-teil3/)


## Note: Script renamed to asn_ipfire.sh
Script is still beta, but new file name is asn_ipfire.sh

File name asn_ipfire_beta.sh is outdated and will be removed soon. Please update your links accordingly.

## Usage
**Output of 
`asn_ipfire.sh --help` :**
```
Usage: asn_ipfire.sh [OPTION] [COMPANYs | -f FILE]
Add or remove networks to IPFire firewall Groups: Networks & Host Groups

Options:
  -a, --add         Add new company networks
  -r, --remove      Remove company networks from customnetworks & customgroups
                    COMPANY='ALL' to remove all entries done by this script
  -f, --file FILE   Get company list from FILE
      --verbose     Verbose mode
  -l, --list        List entries done by this script
      --renumber    Renumber lines of customnetworks & customgroups files
  -v, --version     Show script version
  -h, --help        Show this help

Create special output files (Non-IPFire-Mode):
  --network        Create FILE 'network_list.txt' with networks
  --network_raw    dito, but networks not consolidated
  --asn            Create FILE 'asn_list.txt' with ASNs only
  --iptable        Create FILE 'iptable_rules.txt' with iptable rules
  --afwall         Create FILE 'afwall_rules.txt' with afwall rules

COMPANY to be one or more company names, put into double quotes ('"')
        Multi company names can be comma or space separated
usage example: asn_ipfire.sh -a "CompanyA CompanyB CompanyC" 
               asn_ipfire.sh --asn "CompanyA,CompanyB,CompanyC" 

FILE = name of a file, containing one or more company names.
Company names to be separated by space or line feeds.
usage example: asn_ipfire.sh -r -f company.lst 
               asn_ipfire.sh --network -f company.lst 

Notes:
  Company names are handled case insensitive.
  Only entries made by asn_ipfire.sh can be removed.
  These entries are recognized by the 'Remark'-column in IPFire.
```

## Change log
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
