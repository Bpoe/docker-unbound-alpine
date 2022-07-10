# unbound DNS running on Alpine Linux
This is an unbound container that will respond to requests from all IPv4 and IPv6 clients.

### To Build
```
docker build . -t bpoe/unbound
```

### To Run
```
docker run -d -p 53:53 -p 53:53/udp bpoe/unbound
```

### Use macvlan network
This will run the container with its own MAC and IP address on the network, allowing it to serve the physical network
```
docker network create -d macvlan --subnet=10.0.1.0/24 --gateway=10.0.1.1 -o parent=eth0 ext_net
docker run -d --name dnsresolver01 --network=ext_net --ip=10.0.1.8 --restart=unless-stopped bpoe/unbound
```