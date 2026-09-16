# 01 - Azure Organization

This section documents the organization and governance of the Azure environment used for this portfolio project.

## Objectives

* Understand Azure resource organization
* Define a clear resource group structure
* Apply naming conventions
* Understand Azure RBAC
* Apply the principle of least privilege
* Implement basic cost management and tagging

## Azure Resource Structure

The Azure environment is organized into dedicated resource groups based on the main technical areas of the project:

```text
Azure Cloud Portfolio
│
├── rg-network
│   └── Networking resources
│
├── rg-compute
│   └── Compute resources
│
└── rg-security
    └── Security resources
```

A dedicated resource group for monitoring will be added as part of the monitoring phase of the project.

This structure separates resources by responsibility and makes the environment easier to manage, secure and troubleshoot.

## Resource Groups

The following resource groups have been created for the portfolio environment:

| Resource Group | Purpose                                                                          |
| -------------- | -------------------------------------------------------------------------------- |
| `rg-network`   | Networking resources such as the virtual network and network security components |
| `rg-compute`   | Compute resources such as the portfolio virtual machine                          |
| `rg-security`  | Security resources such as Azure Key Vault                                       |

Resource groups are used to logically organize resources that share a common purpose or lifecycle.

This separation makes the environment easier to manage and provides a clear foundation for applying access control and security policies.

## Naming Conventions

A consistent naming convention is used across the Azure environment to make resources easier to identify and manage.

Examples from this project include:

| Resource type          | Naming pattern   | Example           |
| ---------------------- | ---------------- | ----------------- |
| Resource Group         | `rg-<purpose>`   | `rg-network`      |
| Virtual Network        | `vnet-<purpose>` | `vnet-portfolio`  |
| Subnet                 | `snet-<purpose>` | `snet-web`        |
| Network Security Group | `nsg-<purpose>`  | `nsg-web`         |
| Virtual Machine        | `vm-<purpose>`   | `vm-portfolio`    |
| Key Vault              | `kv-<purpose>`   | `kv-portfolio-xx` |

The naming convention provides a quick indication of what a resource is used for and helps maintain consistency as the environment grows.

## Resource Tags

Tags are used to add metadata to Azure resources and resource groups.

The following tags are used in this portfolio project:

| Tag           | Value                   | Purpose                                           |
| ------------- | ----------------------- | ------------------------------------------------- |
| `Environment` | `Portfolio`             | Identifies the environment                        |
| `Project`     | `Azure-Cloud-Portfolio` | Identifies resources belonging to this project    |
| `Owner`       | `Simon`                 | Identifies the person responsible for the project |

Tags help with resource identification, organization and cost management.

In a larger production environment, tags can also be used to support cost allocation, reporting and governance.

## Governance & Access Control

Azure role-based access control (RBAC) is used to manage who can access resources and what actions they can perform.

A security group named `Compute-ReadOnly` was created in Microsoft Entra ID and assigned the **Reader** role at the `rg-compute` scope.

```text
Simon
  │
  └── Member of Compute-ReadOnly
              │
              └── Reader
                    │
                    └── rg-compute
```

This provides read-only access to the compute resource group through group-based access control.

The configuration follows the principle of least privilege by assigning only the permissions required for the intended task.

## Resource Lock

A resource lock was applied to the `rg-compute` resource group to protect its resources from accidental deletion.

The lock is configured with the **CanNotDelete** level.

```text
rg-compute
│
├── vm-portfolio
│
└── 🔒 lock-protect-compute
        CanNotDelete
```

The lock allows resources to be modified normally but prevents them from being deleted.

This provides an additional layer of protection against accidental deletion, including deletion attempts made by users with high-level Azure permissions.

## Status

✅ Completed

