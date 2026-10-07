# Installing Active Directory

This stage installs Active Directory Domain Services (AD DS) and promotes `DC01` into the Domain Controller for the lab.

## Installing Active Directory Domain Services

Open **Server Manager**, then navigate to:

**Manage -> Add Roles and Features**

### Installation Type

Select **Role-based or feature-based installation**.

### Server Selection

Select `DC01`.

### Server Roles

Select **Active Directory Domain Services**.

When prompted, select **Add Features**.

Continue through the wizard and install the role.

Installing AD DS adds the Active Directory role, but `DC01` is not yet a Domain Controller. The server must now be promoted.

## Promoting `DC01` to a Domain Controller

After installing AD DS, use the notification in Server Manager to select **Promote this server to a domain controller**.

### Deployment Configuration

Select **Add a new forest**.

Root domain name:

```text
adlab.local
```

This creates a new Active Directory forest containing the `adlab.local` domain.

After promotion, the server's fully qualified domain name (FQDN) becomes `DC01.adlab.local`, where:

| Part     | Value         |
| -------- | ------------- |
| Hostname | `DC01`        |
| Domain   | `adlab.local` |

### Domain Controller Options

Configure:

| Setting                 | Value               |
| ----------------------- | ------------------- |
| Forest functional level | Windows Server 2025 |
| Domain functional level | Windows Server 2025 |

These functional levels determine which Windows Server versions and Active Directory features can participate in the environment.

Ensure **DNS Server** is enabled.

Complete the configuration and restart the server when prompted.


## Active Directory DNS

After the restart, `DC01` is the Domain Controller for `adlab.local`. The server also provides DNS for the domain.

Open **Server Manager -> Tools -> DNS**.

DNS Manager should contain the Active Directory DNS zones:

| Zone                | Purpose                                                                                              |
| ------------------- | ---------------------------------------------------------------------------------------------------- |
| `_msdcs.adlab.local` | Contains DNS records used by Active Directory to locate Domain Controllers and other domain services |
| `adlab.local`        | The primary DNS zone for the Active Directory domain                                                 |

The Domain Controller should be able to resolve:

- `DC01.adlab.local`
- `adlab.local`

---

<br>

*The Active Directory environment is now ready for the next stage, adding Windows clients to the* `adlab.local` *domain.*