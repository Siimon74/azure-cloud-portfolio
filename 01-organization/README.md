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

## Status

🔄 In progress
