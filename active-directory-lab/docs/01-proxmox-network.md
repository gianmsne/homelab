# Creating the Isolated Proxmox Network

The first step is creating an isolated virtual network for the Active Directory lab. This prevents future lab services, such as DHCP, from accidentally assigning addresses to devices on the household network.

## Existing Management Network

Proxmox already uses `vmbr0` for management and normal network connectivity, so I left `vmbr0` unchanged.

## Create `vmbr1`

Navigate to:

```
Datacenter -> proxmox node -> System -> Network
```

Select **Create -> Linux Bridge**, then configure the bridge:

| Setting      | Value     |
| ------------ | --------- |
| Name         | `vmbr1`   |
| Bridge ports | None      |
| IPv4         | None      |
| IPv6         | None      |
| Autostart    | Enabled   |

Apply the configuration.

## Why `vmbr1`?

A Linux bridge acts like a virtual Ethernet switch.

Because `vmbr1` has no physical network interface assigned to it, traffic connected to the bridge remains inside Proxmox.

VMs connected to `vmbr1` can communicate with one another, but they do not have a direct connection to the household network.

The Active Directory VMs will use `vmbr1`.