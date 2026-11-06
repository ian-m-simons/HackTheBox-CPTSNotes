Intelligent Platform Management Interface is a set of standardized specifications for hardware-based host management systems used for system management and monitoring. it lets sysadmins manage and monitor systems even if they are powered off or in an unresponsive state. typically used:
- Before the OS has booted to modify BIOS settings
- When the host is fully powered down
- Access to a host after a system failure
ok basically IPMI is a hardware controller inside (or between a device and the network) which can be used for remote administration of hardware, and other pre-OS things
as long as the IPMI module has power it can keep doing things, even if the endpoint is powered off.

### Footprinting the Service
IPMI uses port623 over UDP. Devices that use the IPMI protocol are called baseboard management controllers (BMC). Typically they are built into the motherboard, but PCI card's do exist for them. gaining access to the BMC is essentially the same as attaining physical access to the machine.

Default Passwords:

| Product         | Username      | Password                                                                  |
| --------------- | ------------- | ------------------------------------------------------------------------- |
| Dell iDRAC      | root          | calvin                                                                    |
| HP iLO          | Administrator | randomized 8-character string consisting of numbers and uppercase letters |
| SuperMicro IPMI | ADMIN         | ADMIN                                                                     |
### Dangerous settings
Even if the default credentials have been changed, the Server will send a salted SHA1 or MD5 hash of the user's password to the client before authentication takes place. there is no fix for this issue because the flaw is a critical component of IPMI specifications. metasploit has an IPMI hash dumping module.

At the end of the day, IPMI is sketchy, don't use it if you can avoid it. if you must use it, make the password long strong and ridiculous