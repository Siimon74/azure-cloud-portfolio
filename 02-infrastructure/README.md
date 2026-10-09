# 02 - Azure Infrastructure

In this part of my Azure Cloud Portfolio, I built a basic network and deployed a Linux virtual machine.

The goal was to understand how Azure networking works, how to control network access and how to connect securely to a virtual machine.

## 1. Virtual Network and Subnets

I created a Virtual Network (VNet) named `vnet-portfolio` to provide the network for my Azure resources.

The address space is `10.0.0.0/16`.

The `snet-web` subnet uses `10.0.1.0/24` and contains my portfolio virtual machine.

### Network layout

```text
VNet: vnet-portfolio
└── snet-web
    └── vm-portfolio
```

I planned to use separate subnets for different purposes as the project grows.

**What I learned:** A VNet provides a private network for Azure resources. Subnets divide that network into smaller sections, which can help organize resources and apply different security rules.

## 2. Network Security Group (NSG)

I created a Network Security Group named `nsg-web` to control inbound traffic to my infrastructure.

The inbound rules are:

| Priority | Rule                  | Protocol | Port | Source       | Action |
| -------: | --------------------- | -------- | ---: | ------------ | ------ |
|      100 | `Allow-HTTPS-Inbound` | TCP      |  443 | Any          | Allow  |
|      110 | `Allow-SSH-Inbound`   | TCP      |   22 | My public IP | Allow  |
|    65500 | `DenyAllInBound`      | Any      |  Any | Any          | Deny   |

Azure evaluates rules in priority order, starting with the lowest number. The specific allow rules are therefore evaluated before the default deny rule.

SSH access is restricted to my public IP instead of being open to everyone on the Internet.

**What I learned:** An NSG acts like a network traffic filter. It allows or blocks traffic according to rules such as source, destination, protocol and port.

## 3. Virtual Machine

I deployed a Linux virtual machine named `vm-portfolio`.

| Setting          | Configuration           |
| ---------------- | ----------------------- |
| Operating system | Ubuntu Server 24.04 LTS |
| Size             | Standard_B1s            |
| Region           | Denmark East            |
| Virtual network  | `vnet-portfolio`        |
| Subnet           | `snet-web`              |
| Authentication   | SSH key                 |
| Managed Identity | System-assigned         |

I chose a small VM size to keep the project costs low while learning the basics of Linux and Azure compute.

I also enabled a system-assigned Managed Identity so the VM could authenticate with supported Azure services without storing credentials on the server.

**What I learned:** A virtual machine provides compute resources in Azure. Its size affects available resources and cost, while its network settings control how it communicates with other resources.

## 4. Connecting Through SSH

I connected to the VM using SSH and public key authentication instead of a password.

The NSG rule for port 22 restricts SSH access to my public IP address.

During testing, I lost SSH connectivity after my public IP address changed. Updating the NSG rule with my current IP restored the connection.

**What I learned:** When SSH fails, the problem may not be the VM itself. I need to check the connection details, public IP address, network interface and NSG rules.

## Project Status

**Completed:** Virtual network setup, subnet configuration, NSG rules, Linux VM deployment and SSH access.

The project will be extended as I learn more about Azure networking and security.
