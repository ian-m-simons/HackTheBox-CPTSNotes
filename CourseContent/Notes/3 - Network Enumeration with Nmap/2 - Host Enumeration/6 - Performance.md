it is important to manage performance to ensure it doesn't take forever and so that you don't eat up all available bandwidth
### Timeouts
setting this up properly can save us time, but if the initial timeout is too short, we may miss hosts, by  default min-rtt of 100 ms
### Max Retries
default `--max-retries` is 10 but we can set that manually. again here you're trading speed for accuracy
### Rates
`--min-rate <number>` specifies the minimum rate at which it should send packets, packets are sent simultaneously, and nmap will attempt to maintain the rate accordingly
### Timing
can use `-T` to adjust rate 0-5 0 = paranoid (ie slow af) 5=insane (ie fast AF) default `-T3` 