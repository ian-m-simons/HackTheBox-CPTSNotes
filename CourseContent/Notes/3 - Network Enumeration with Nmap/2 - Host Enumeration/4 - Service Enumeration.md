we need to identify applications and versions as accurately as possible. This helps us to perform better vulnerability research and find better exploits
### Service Version Detection
typcially you want to do a quick port scan first this gives usa small overview of available ports without making as much noise which can lead to getting blocked, after that we want to run an -sV to find versions
you can use `-v`/`-vv` for verbosity when scanning
nmap starts identifying services by banner grabbing, if that doesn't work it will use signature-based matching, though this is way slower. Nmap doesn't always know what to do with various pieces of information so be aware that it is also useful to manually banner grab, or look at the packets yourself
