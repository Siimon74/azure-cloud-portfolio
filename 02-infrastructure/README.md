# 02 - Azure Infrastructure

This section documents the infrastructure deployed in Azure.

## Objectives

* Design an Azure Virtual Network
* Create and configure subnets
* Configure Network Security Groups
* Deploy compute resources
* Understand Azure networking fundamentals

## Network Architecture

The Azure network was designed using a Virtual Network (VNet) with dedicated subnets for different purposes.

```text
VNet: vnet-portfolio
│
├── snet-web
│   └── Portfolio VM
│
└── snet-management
    └── Reserved for management resources
```

The VNet uses the `10.0.0.0/16` address space.

The `snet-web` subnet uses `10.0.1.0/24` and hosts the portfolio virtual machine.

The `snet-management` subnet uses `10.0.2.0/24` and is reserved for future management resources.

Separating workloads into subnets provides a foundation for applying different network security rules as the infrastructure grows.

## Network Security Group

A Network Security Group (NSG) was configured to control inbound network traffic to the portfolio infrastructure.

The NSG `nsg-web` contains the following inbound rules:

| Priority | Rule                  | Protocol | Port | Source       | Action |
| -------- | --------------------- | -------- | ---- | ------------ | ------ |
| 100      | `Allow-HTTPS-Inbound` | TCP      | 443  | Any          | Allow  |
| 110      | `Allow-SSH-Inbound`   | TCP      | 22   | My public IP | Allow  |
| 65500    | `DenyAllInBound`      | Any      | Any  | Any          | Deny   |

Lower priority numbers are evaluated first. Therefore, the specific allow rules are evaluated before the default deny rule.

SSH access is restricted to the administrator's public IP address rather than being exposed to the entire Internet.

## Virtual Machine

A Linux virtual machine was deployed in Azure to provide the compute layer of the portfolio environment.

| Setting          | Configuration           |
| ---------------- | ----------------------- |
| Name             | `vm-portfolio`          |
| Operating System | Ubuntu Server 24.04 LTS |
| Size             | Standard_B1s            |
| Region           | Denmark East            |
| Virtual Network  | `vnet-portfolio`        |
| Subnet           | `snet-web`              |
| Authentication   | SSH key                 |
| Managed Identity | System-assigned         |

The virtual machine is connected to the `snet-web` subnet and is protected by the configured Network Security Group.

SSH key authentication is used instead of password authentication to provide secure administrative access.

A system-assigned managed identity was also enabled on the VM. This identity is used to authenticate the virtual machine with Azure services without storing credentials on the server.

## SSH Access

Administrative access to the Linux virtual machine is provided through SSH using public key authentication.

The SSH connection is restricted at the network level by the `Allow-SSH-Inbound` NSG rule, which only permits connections from the administrator's public IP address.

This configuration reduces the exposure of the SSH service while allowing secure remote administration of the virtual machine.

During testing, an SSH connection issue was caused by a change in the administrator's public IP address. Updating the NSG rule to the current public IP restored connectivity.

This troubleshooting exercise demonstrated the relationship between the VM, its network interface, the NSG and the administrator's public IP address.

## Status

✅ Completed
