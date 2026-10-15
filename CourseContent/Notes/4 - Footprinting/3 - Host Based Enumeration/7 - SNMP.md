SNMP is used to monitor and manage devices sometimes even making config changes. traps are used to allow the server to reach the client without the client reaching out first.
#### MIB
Management information base. MIB is a text file which all queryable SNMP objects of a device are listed in a standardized tree hierarchy. MIB is written in Abstract syntax notation 1 (ASN.1) (ascii based) MIB doesn't have data, but explains where to find what information. 

#### OID 
OID represenst a node in a heirarchical namespace. this is where you get things like 1.8.5.9.2.3 the longer the chain the more specific.

#### SNMP v1
first version, still common in many small networks. No builtin authentication, and does not support encryption.

#### SNMP v2
multiple iterations on v2 today we still use v2c. c means community based. some auth via community string, but in plain text and still no built in encryption

#### SNMP v3
Requires auth using username and password, and allows for encryption via a pre-shared key
#### Community Strings
Better than nothing, but not by much, for SNMP v2 its still just plaintext sent over the network
### Default Configuration
set it up, play with it break it, this is the best way to learn these settings
### Dangerous settings

| Setting                                          | Description                                                                          |
| ------------------------------------------------ | ------------------------------------------------------------------------------------ |
| `rwuser noauth`                                  | Provides access to the full OID tree without authentication                          |
| `rwcommunity <community string> <IPv4-ADDRESS`   | Provides access to the full OID tree regardless of where the requests were sent from |
| `rwcommunity6 <community string> <IPv6-ADDRESS>` | Same access with rwcommunity with the difference of using IPv6                       |
### Footprinting the Service
for footprinting SNMP we can use [snmpwalk](../../../TTPs%20and%20Tools/Tools/Service%20Enumeration/snmpwalk.md), [onesixtyone](../../../TTPs%20and%20Tools/Tools/Brute%20Force/onesixtyone.md), and braa. Snmpwalk is used to query OIDs, Onesixtyone us for brute-forcing names of community strings

#### [snmpwalk](../../../TTPs%20and%20Tools/Tools/Service%20Enumeration/snmpwalk.md)
use this once you have the community string and/or credentials. 
#### [onesixtyone](../../../TTPs%20and%20Tools/Tools/Brute%20Force/onesixtyone.md)
use this to brute force community strings. you might consider using a tool to create custom wordlists. 

#### braa
use braa to brute-force individual OIDs and enumerate the information behind them.