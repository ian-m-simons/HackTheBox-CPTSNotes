You should already be familiar with what DNS is. There is no centralized DNS database, instead it is spread across multiple servers. Additionally there are multiple types of DNS servers

| Server Type                   | Description                                                                                                                                                                                                                                                                                                                                                  |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| DNS Root Server               | DNS root servers are responsible for the top-level domains. As the last instance, they are only requested if the name server does not respond. Thuse, a root server is a central interface between users and content on the internet, as it links domain and IP address. ICANN coordinates the work of the root name servers. There are 13 of these globally |
| Authoritative Name Server     | Authoritative name servers hold authority for a particular zone. They only answer queries from their area of responsibility, and their information is binding. If an Authoritative name server cannot answer a client's query, the root name server takes over.                                                                                              |
| Non-Authoritative Name Server | Non-authoritative name servers are not responsible for a particular DNS zone. Instead, they collect information on specific DNS zones themselves, which is done using recursive or iterative DNS querying.                                                                                                                                                   |
| Caching DNS Server            | Caching DNS servers cache information from other name servers for a specified period. The authoritative name server determines the duration of this storage.                                                                                                                                                                                                 |
| Forwarding Server             | Forwarding servers perform only one function: they forward DNS queries to another DNS server                                                                                                                                                                                                                                                                 |
| Resolver                      | Resolvers are not authoritative DNS servers but perform name resolution locally on the computer or router.                                                                                                                                                                                                                                                   |
DNS is not usually encrypted, so it is easily snooped posing a privacy risk. Nowadays IT security professionals will generally use DNS over TLS (DOT) or DNS over HTTPS (DOH). Remember there are more than just `A` records in DNS. `SOA` records can be used to find emails etc of who is responsible for resources

### Default Configuration

DNS Server Bind9 is most common on Linux-Based Distributions. Generally speaking Bind9 is divided into 2 sections, general settings, and zone entries (for individual domains). In the config file you have global and zone settings, in a conflict zone wins. BIND file format is now the preferred file format across the board for DNS zone files. 

### Dangerous Settings

Because DNS is so critical from a business perspective, functionality is often prioritized over security. See the below table for some common issues to look out for.

| Option            | Description                                                                    |
| ----------------- | ------------------------------------------------------------------------------ |
| `allow-query`     | Defines which hosts are allowed to send requests to the DNS server.            |
| `allow-recursion` | Defines which hosts are allowed to send recursive requests to the DNS server.  |
| `allow-transfer`  | Defines which hosts are allowed to receive zone transfers from the DNS server. |
| `zone-statistics` | Collects statistical data of zones.                                            |
can specify the DNS server you want to query. Sometimes you can also find the DNS server version using a class chaos query and type txt see the example below

```
n00blyfe@htb$ dig CH TXT version.bind 10.129.120.85

; <<>> DiG 9.10.6 <<>> CH TXT version.bind 
;; global options: +cmd 
;; Got answer: 
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 47786 
;; flags: qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1 
;; ANSWER SECTION: version.bind. 0 CH TXT "9.10.6-P1" 
;; ADDITIONAL SECTION: version.bind. 0 CH TXT "9.10.6-P1-Debian" 
;; Query time: 2 msec 
;; SERVER: 10.129.120.85#53(10.129.120.85) 
;; WHEN: Wed Jan 05 20:23:14 UTC 2023 
;; MSG SIZE rcvd: 101

```

you can also use the any option to view all available records. 
A zone transfer is when records are replicated across zones. Original data is in a `primary` name server which is loadbalanced with `secondary` name servers. Generally DNS entries are only changed on the primary and then replicated to secondaries and other zones etc. AXFR records can reveal information we might otherwise want hidden so make sure you check there. Individual A records with hostnames can be enumerated via a brute-force attack, either using tools or manually using a for-loop