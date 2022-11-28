# Checking the stability of BGP neighbors using Docker and FRRouting
Docker Compose which is designed to check the stability of BGP neighbors

### Scheme
![](https://i.imgur.com/mIKehUu.png)


#### Install Docker, Docker-compose in Ubuntu 20.04

```sudo apt update
sudo apt install docker.io
sudo curl -L "https://github.com/docker/compose/releases/download/v2.13.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
#### Check version
```
docker-compose version
```
Output:
> Docker Compose version v2.13.0

#### Download
```
git clone https://github.com/mrgromdd/frr-bgp-docker.git
cd frr-bgp-docker/
```
#### Starting
Before starting, edit the configuration files in /config/*. And also edit docker-compose.yml
```
docker-compose up -d
```
#### Enable forwarding from Docker containers to the outside world
By default, traffic from containers connected to the default bridge network is not forwarded to the outside world. To enable forwarding, you need to change two settings. These are not Docker commands and they affect the Docker host’s kernel.
1. Configure the Linux kernel to allow IP forwarding.
```
sudo iptables -P FORWARD ACCEPT
```
2. Change the policy for the `iptables` `FORWARD` policy from `DROP` to `ACCEPT`.
```
sysctl net.ipv4.conf.all.forwarding=1
```
These settings do not persist across a reboot, so you may need to add them to a start-up script.

#### Examples
There are examples of the configuration of BGP neighbors

#### Gratitude
[Yusuke Iwase](https://github.com/iwaseyusuke)
