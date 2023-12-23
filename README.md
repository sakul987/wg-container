# wiretainer
This repo aims to provide a simple bash script for creating network namespaces for a WireGuard VPN connection and running only specific applications in this namespace, while the rest of the system continues to use the non-VPN connection.

It is heavily inspired by [https://gist.github.com/jamesmcm/f8d6e9f290f7b128e1b500430789d651](https://gist.github.com/jamesmcm/f8d6e9f290f7b128e1b500430789d651) and [https://www.wireguard.com/netns/](https://www.wireguard.com/netns/).

It is currently designed to use iptables and ufw.

For ufw it uses the interface "enp5s0" by default to allow the namespace to connect to the internet. ~~I might make this changeable over a flag.~~ Use flag -i to specify the interface.

Also this currently only supports one VPN/namespace, I might add the possibility to create multiple connections / namespaces automatically.

The script uses wgquick up & down to connect to the VPN, make sure you have wireguard-tools installed.

# Usage: Start
To create a VPN namespace with the config file /etc/wireguard/wg-us-01.conf run ```/path/to/wiretainer up wg-us-01```

To create a VPN namespace using interface "eth0" with the config file /etc/wireguard/wg-us-01.conf run ```/path/to/wiretainer up -i eth0 wg-us-01```

# Usage: Stop
To remove the VPN namespace & connection run ```/path/to/wiretainer down wg-us-01```

To remove the VPN namespace & connection using interface "eth0" run ```/path/to/wiretainer down -i eth0 wg-us-01```

# Usage: Run Application
To run a application (e.g. firefox) in the VPN namespace run ```/path/to/wiretainer exec firefox```
