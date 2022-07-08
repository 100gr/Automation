**puppet.conf**: The main config file

agent config:
```puppet
[main] 
certname = agent01.example.com
server = puppet
environment = production
# seconds (30 or 30s), minutes (30m), hours (6h), days (2d), years (5y).
runinterval = 1h 
```

master config:
```puppet
[main]
certname = puppetmaster01.example.com
server = puppet
runinterval = 1h
strict_variables = true

[master]
# By adding dns_alt_names you have to sepcify also 'puppet', as it will be absent from DNS list. 
dns_alt_names = puppet,puppetmaster01,puppetmaster01.example.com,puppet,puppet.example.com
reports = puppetdb
storeconfigs_backend = puppetdb
storeconfigs = true
```




[Configuration Reference](https://puppet.com/docs/puppet/latest/configuration.html)

