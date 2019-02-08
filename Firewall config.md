# Firewall rules
We used a simple firewall which made use of a iptables setting.
This iptable setting blocked the traffic destined for the internet at port 8181.

The following rule was set:
```
iptables -A FORWARD -i ens4 -p tcp -m tcp --dport 8181 -j DROP
```

Please note that the firewall must have 'IPv4 Forwarding' enabled in its settings.
