# Splunk Tiered Deployment Server
## [![](https://img.shields.io/badge/license-BEERWARE-yellow)](./LICENSE) [![](https://img.shields.io/badge/language-rus-red)](./README.ru.md)

![architecture diagram](./Splunk_tiered_servers.png)

The presented configuration files allow you to deploy a multi-level deployment  server and data transfer systems located in different vlans.

In this example, we have:

- Primary deployment server located in VLAN 1.
- Secondary deployment server (aka heavy forwarder) located in VLAN 2.
- Universal forwarders acting as deployment clients on the primary and secondary deployment servers.
- Two virtual networks (VLAN 1,2) in which, for security reasons, ports are open for communication and receiving / sending data, but only for one host located in VLAN 2.

## The Primary Deployment Server
The primary deployment server serves as the main app repository. 

In this example, it has:

#### In directory `$SPLUNK_HOME/etc/deployment-apps:`
- `send_to_secondary` (an arbitrary app for send data to secondary deployment server (heavyforwarder))
- `TA-linux` (the technology add-on for monitoring logs on *Nix hosts)
- `TA_windows` (the technology add-on for monitoring logs on Windows hosts)

## The Secondary Deployment Server
The secondary deployment server downloads its apps from the primary deployment server.

In this example, it will download:

#### In directory `$SPLUNK_HOME/etc/apps:`
- `TA-linux` (in this example we use TA-linux for local monitoring *Nix logs)

#### In directory `$SPLUNK_HOME/etc/deployment-apps:`
- `send_to_secondary`
- `TA-linux`
- `TA_windows`

## Licensing

[Splunk-tiered-deployment-server](https://github.com/Klimdy/Splunk-tiered-deployment-server) is licensed under the [BEERWARE](./LICENSE) License. =)

## Acknowledgments

[Steven Swor](https://github.com/sworisbreathing) - The man who first described a similar configuration

