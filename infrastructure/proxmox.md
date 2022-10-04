# Proxmox VE 7.2-1
Proxmox VE is a complete open-source platform for enterprise virtualization. With the built-in web interface you can easily manage VMs and containers, software-defined storage and networking, high-availability clustering, and multiple out-of-the-box tools on a single solution.

# Customization

## Dark Theme
Can be acquired from [PVEDiscordDark](https://github.com/Weilbyte/PVEDiscordDark)

### Install
```shell
bash <(curl -s https://raw.githubusercontent.com/Weilbyte/PVEDiscordDark/master/PVEDiscordDark.sh ) install
```

### Uninstall
```shell
bash <(curl -s https://raw.githubusercontent.com/Weilbyte/PVEDiscordDark/master/PVEDiscordDark.sh ) uninstall
```

## No-Subscription Repository
This is the recommended repository for testing and non-production use. Its packages are not as heavily tested and validated. You don’t need a subscription key to access the pve-no-subscription repository.
We recommend to configure this repository in `/etc/apt/sources.list`.

File `/etc/apt/sources.list`
```shell
deb http://ftp.debian.org/debian bullseye main contrib
deb http://ftp.debian.org/debian bullseye-updates main contrib

# PVE pve-no-subscription repository provided by proxmox.com,
# NOT recommended for production use
deb http://download.proxmox.com/debian/pve bullseye pve-no-subscription

# security updates
deb http://security.debian.org/debian-security bullseye-security main contrib
```

## Fake Subscription
Can be acquired from [pve-fake-subscription](https://github.com/Jamesits/pve-fake-subscription)

### Install
1. [Download the latest release](https://github.com/Jamesits/pve-fake-subscription/releases/latest)
2. Install: run `dpkg -i pve-fake-subscription_*.deb` as **root** on every node
3. Optional: `echo "127.0.0.1 shop.maurer-it.com" | sudo tee -a /etc/hosts` to prevent fake keys from being checked against the Proxmox servers

### Uninstall
Run as **root**
```shell
apt purge pve-fake-subscription
```
This will revert your system to a "no subscription key" status.

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