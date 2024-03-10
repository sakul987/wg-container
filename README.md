# wg-container
This repo aims to provide a simple bash script for creating network namespaces for a WireGuard VPN connection and running only specific applications in this namespace, while the rest of the system continues to use the non-VPN connection.

It is heavily inspired by [https://gist.github.com/jamesmcm/f8d6e9f290f7b128e1b500430789d651](https://gist.github.com/jamesmcm/f8d6e9f290f7b128e1b500430789d651) and [https://www.wireguard.com/netns/](https://www.wireguard.com/netns/).

It is currently designed to use iptables and ufw.

For ufw it uses the interface "enp5s0" by default to allow the namespace to connect to the internet. Use flag -i to specify the interface.

It is possible to use multiple connections simultaneously.

The script uses wgquick up & down to connect to the VPN, make sure you have wireguard-tools installed.

Display the help menu by running ```wg-container help```

# Installation
Simply download the script and place it somewhere, where you can execute it from. If you are using Arch, consider using the [AUR package](https://aur.archlinux.org/packages/wg-container).

# Usage: Start
To create a VPN namespace with the config file /etc/wireguard/wg-us-01.conf run ```wg-container up wg-us-01```

To create a VPN namespace using interface "eth0" with the config file /etc/wireguard/wg-us-01.conf run ```wg-container up -i eth0 wg-us-01```

# Usage: Stop
To remove the VPN namespace & connection run ```wg-container down```

To remove the VPN namespace & connection using interface "eth0" run ```wg-container down -i eth0```

When the VPN was started in multimode, run ```wg-container down -m wg-us-01```

# Usage: Run Application
To run a application (e.g. firefox) in the VPN namespace run ```wg-container exec firefox```

# All in one line
To create a VPN namespace, run the application inside and afterwards clean up again run ```wg-container direct wg-us-01 firefox```

To create a VPN namespace using interface "eth0", run the application inside and afterwards clean up again run ```wg-container direct -i eth0 wg-us-01 firefox```

# Multi mode
If you want to have multiple vpn connections open at the same time, use multi mode by setting the -m flag. When you start a connection with up and set the -m flag, you can execute a command in this connection by using -m <servername>. If you created a "normal" connection without -m, you can also just execute a command without specifying the server like before.

Important: the server name should not be longer than 13(?) chars, otherwise you will get an error.

Example:

```wg-container up -m wg-us-01```

```wg-container exec -m wg-us-01 firefox```

# List
It is possible to print out the active VPN connections by running ```wg-container list```

# Flags
-i INTERFACE to set the interface to be used.

-v To set -x / enable more debug info.

-h To get a help overview.

-m Multi mode, specify when executing a command in a connection that was created using -m
