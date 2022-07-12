# unbound DNS running on Alpine Linux
A container with Unbound DNS resolver running on Alpine Linux. All IPv4 and IPv6 networks are allowed.

[![](https://img.shields.io/docker/pulls/bpoe/unbound.svg)](https://hub.docker.com/r/bpoe/unbound)

### To Build
```
docker build https://github.com/Bpoe/docker-unbound-alpine.git -t bpoe/unbound
```

### To Run
```
docker run -d -p 53:53 -p 53:53/udp --restart=unless-stopped bpoe/unbound
```

### Use macvlan network
This will run the container with its own MAC and IP address on the network, allowing it to serve the physical network
```
docker network create -d macvlan --subnet=10.0.1.0/24 --gateway=10.0.1.1 -o parent=eth0 ext_net
docker run -d --name dnsresolver01 --network=ext_net --ip=10.0.1.8 --restart=unless-stopped bpoe/unbound
```
