# wiretainer
This repo aims to provide a simple solution to creating network namespaces for a WireGuard VPN connection and running only specific applications in this namespace, while the rest of the system continues to use the non-VPN connection.

It is heavily inspired by [https://gist.github.com/jamesmcm/f8d6e9f290f7b128e1b500430789d651](https://gist.github.com/jamesmcm/f8d6e9f290f7b128e1b500430789d651) and [https://www.wireguard.com/netns/](https://www.wireguard.com/netns/).

It is currently designed to use iptables and ufw.

For ufw it uses the interface "enp5s0" to allow the namespace to connect to the internet. I might make this changeable over a flag.

Also this currently only supports one VPN/namespace, I might add the possibility to create multiple connections / namespaces automatically.

The script uses wgquick up & down to connect to the VPN, make sure you have wireguard-tools installed.

# Usage
To create a VPN namespace with the config file /etc/wireguard/wg-us-01.conf run ```/path/to/script up wg-us-01```

To remove the VPN namespace & connection run ```/path/to/script down wg-us-01```

To run a application (e.g. firefox) in the VPN namespace run ```/path/to/script exec firefox```