# ASN_IPFire_Script

IPFire network object creator for IPv4 addresses based on ASN information.

For detailed description of this script please see the article on Kuketz-Blog: [ASN-Skript: Datensammler haben ausgeschnüffelt – IPFire Teil3](https://www.kuketz-blog.de/asn-skript-datensammler-haben-ausgeschnueffelt-ipfire-teil3/)



**Output of 
`asn_ipfire_beta.sh --help` respectively `asn_ipfire.sh --help` :**
```
Usage: asn_ipfire.sh [OPTION] [COMPANYs | -f FILE]
Add or remove networks to IPFire firewall Groups: Networks & Host Groups

Options:
  -a, --add         Add new company networks
  -r, --remove      Remove company networks from customnetworks & customgroups
                    COMPANY='ALL' to remove all entries done by this script
  -f, --file FILE   Get company list from FILE
  -l, --list        List entries done by this script
      --renumber    Renumber lines of customnetworks & customgroups files
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
usage example: asn_ipfire.sh -u -f company.lst 
               asn_ipfire.sh --network -f company.lst 

Notes:
  Company names are handled case insensitive.
  Only entries made by asn_ipfire.sh are updated or removed.
  These entries are recognized by the 'Remark'-column in IPFire.
  
```