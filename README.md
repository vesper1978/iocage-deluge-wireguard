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



