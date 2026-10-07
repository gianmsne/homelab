# Active Directory Lab Overview

> A small Active Directory environment running on Proxmox for learning and experimentation.

`vmbr0` is the existing Proxmox management network and remains connected to the household network.

`vmbr1` is a virtual Layer 2 network used exclusively by the Active Directory lab. It has no physical network interface attached in order to keep the lab isolated from the household network.

## Network

| Component | Configuration |
|---|---|
| Lab network | `192.168.100.0/24` |
| Proxmox lab bridge | `vmbr1` |
| Domain | `adlab.local` |
| Domain Controller | `DC01` |
| Domain Controller IP address | `192.168.100.10` |
| DNS server | `192.168.100.10` |

## Domain Controller

*DC01 runs:*

* Windows Server 2025 Standard (Desktop Experience)
* Active Directory Domain Services
* DNS
* `adlab.local` Active Directory domain

## Setup

1. [Create the isolated Proxmox network](01-proxmox-network.md)
2. [Create and configure the Domain Controller VM](02-domain-controller.md)
3. [Install and configure Active Directory](03-active-directory.md)
4. [Setup a client Windows VM](04-client-setup.md)
