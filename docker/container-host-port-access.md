
### Accessing the Host ports from within container

In order to access the host's ports from the container, you will need to open your Linux firewall. 
Fortunately, by default docker container access the network from the docker0 interface. 
So, just ACCEPTING access from docker0 intreface will work (provided you trust your docker container).

Using iptables
```
iptables -A INPUT -i docker0 -j ACCEPT
```

Using ufw
```
ufw allow in on docker0
```

