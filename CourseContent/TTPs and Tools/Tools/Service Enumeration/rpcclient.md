a tool for performaning MS-RPC functions

basic usage
```
n00blyfe@htb$ rpcclient -U "" 10.129.14.128

Enter WORKGROUP\'s password:
rpcclient $>
```

common rpc queries

| Query                     | Description                                                       |
| ------------------------- | ----------------------------------------------------------------- |
| `srvinfo`                 | Server Information                                                |
| `enumdomains`             | Enumerate all domains that are deployed in the network.           |
| `querydominfo`            | Provides domain, server, and user information of deployed domains |
| `netshareenumall`         | Enumerates all available shares                                   |
| `netsharegetinfo <share>` | provides                                                          |
| `enumdomusers`            | Enumerates all domain users                                       |
| `queryuser <RID>`         | provides information about a specific user                        |
