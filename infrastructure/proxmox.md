# Proxmox VE 7.2-1
Proxmox VE is a complete open-source platform for enterprise virtualization. With the built-in web interface you can easily manage VMs and containers, software-defined storage and networking, high-availability clustering, and multiple out-of-the-box tools on a single solution.

# Customization

## Dark Theme
Can be acquired from [PVEDiscordDark](https://github.com/Weilbyte/PVEDiscordDark)

## Predictable network port logical names
By default, all networks ports will have default name that makes matching quite hard. This will allow the user to rename each port to a friendlier name based on the port's MAC address

- create a new file `/etc/udev/rules.d/70-network.rules`
- add each interface on a new line, specifying MAC address and desired name

```shell
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="70:85:c2:29:cd:40", NAME="i211"
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="70:85:c2:29:cd:42", NAME="i218v"
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="34:64:a9:b8:ba:60", NAME="hp10a"
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="34:64:a9:b8:ba:64", NAME="hp10b"
```

- edit `/etc/network/interfaces` and use the new names for interfaces and update the one used for the bridge