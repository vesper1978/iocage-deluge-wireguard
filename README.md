# iocage-plugin-deluge-wireguard
Artifact file(s) for Deluge iocage plugin

This plugin will install Deluge and its WebUI from the Python Package Index (PyPI) plus Wireguard for VPN connections.

## To install this Plugin
Download the plugin manifest file to your local file system.
```
fetch https://raw.githubusercontent.com/vesper1978/iocage-my-plugins/master/deluge-wireguard.json
```
Install the plugin.  Adjust the network settings as needed.
```
iocage fetch -P deluge-wireguard.json -n deluge-wireguard
```
Configure Wireguard
```
touch /usr/local/etc/wireguard/wg0.conf
```
Then edit the /usr/local/etc/wireguard/wg0.conf with your VPN provider's connection settings.

Enable Wireguard
```
sysrc wireguard_interfaces="wg0"
sysrc wireguard_enable="YES"
```

Start Wireguard
```
service wireguard start
```

Configure IPFW to block internet traffic if VPN connection is down.
```
sysrc firewall_enable="YES"
sysrc firewall_script="/etc/ipfw.rules"
sysrc firewall_logging="YES"
touch /etc/ipfw.rules
```

Insert the following into the /etc/ipfw.rules
```
#!/usr/local/bin/bash
# Config

# Set rules command prefix
cmd="ipfw -q add"
vpn="wg0"
user="deluge"
localLan="xxx.xxx.xxx.xxx/24"

# Flush out the list before we begin
ipfw -q -f flush

# Allow all local traffic on the loopback interface
${cmd} 00001 allow all from any to any via lo0
```

