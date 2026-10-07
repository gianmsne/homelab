# Creating the Domain Controller VM

The first virtual machine in the lab is the Domain Controller, `DC01`.

## Windows Server ISO

Upload the Windows Server 2025 ISO to Proxmox:

```
Datacenter -> proxmox node -> local -> ISO Images -> Upload
```

## Create the VM

Create a new VM with the following configuration.

### General

| Setting | Value     |
| ------- | --------- |
| Node    | Proxmox   |
| VM ID   | 201       |
| Name    | `DC01`    |

- `DC01` stands for Domain Controller 01.

- VM ID 201 follows my convention of using the 200 range for AD lab VMs.

### OS

| Setting    | Value                                 |
| ---------- | ------------------------------------- |
| Media      | Use CD/DVD disc image file            |
| ISO        | Windows Server 2025 ISO               |
| Guest OS   | Microsoft Windows                     |
| Version    | 11/2022/2025                          |

### System

Leave the default settings, and enable:

- **QEMU Guest Agent**

### Disk

| Setting   | Value        |
| --------- | ------------ |
| Storage   | `local-lvm`  |
| Disk size | 60 GB        |
| Bus       | SATA0        |

### CPU

| Setting | Value |
| ------- | ----- |
| Sockets | 1     |
| Cores   | 2     |

### Memory

| Setting | Value   |
| ------- | ------- |
| Memory  | 4096 MB |

### Network

Connect the VM to the isolated lab network:

| Setting  | Value                      |
| -------- | -------------------------- |
| Bridge   | `vmbr1`                    |
| Model    | VirtIO (paravirtualized)   |
| Firewall | Enabled                    |

The VM's virtual network adapter is therefore connected to `vmbr1` rather than the household network.

## Installing Windows Server

Install **Windows Server 2025 Standard (Desktop Experience)**.

During the initial configuration:

| Setting       | Value       |
| ------------- | ----------- |
| Computer name | `DC01`      |
| Domain        | Workgroup   |

At this stage, `DC01` is a standalone Windows Server. Active Directory will be configured in the next stage.

## Configuring the Static IP

The Active Directory lab uses the network `192.168.100.0/24`.

Navigate to:

```text
Ethernet -> Properties -> 
Internet Protocol Version 4 (TCP/IPv4) -> Properties
```
Configure the values below.
Assign `DC01` the following static address:

| Setting       | Value            |
| ------------- | ---------------- |
| IP address    | `192.168.100.10` |
| Subnet mask   | `255.255.255.0`  |
| Preferred DNS | `192.168.100.10` |

`DC01` will eventually provide DNS for the Active Directory domain, so it uses itself as its preferred DNS server.

--- 
<br>
*The server is now ready for Active Directory Domain Services to be installed.*