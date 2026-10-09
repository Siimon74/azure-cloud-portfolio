# 01 - Azure Organization

This is the organization part of my Azure Cloud Portfolio project.

The goal is to learn how to organize Azure resources, manage access and protect resources from accidental changes.

## 1. Resource Groups

I created three resource groups to organize the resources in my Azure environment.

| Resource Group | Purpose                                         |
| -------------- | ----------------------------------------------- |
| `rg-network`   | Network resources                               |
| `rg-compute`   | Compute resources, including my virtual machine |
| `rg-security`  | Security resources                              |

Azure resource groups help organize related resources and make it easier to manage them.

## 2. Resource Tags

I applied the same tags to my resource groups and individual resources to keep my Azure environment organized.

| Tag           | Value                   | Purpose                                         |
| ------------- | ----------------------- | ----------------------------------------------- |
| `Owner`       | `Simon`                 | Identifies who is responsible for the resources |
| `Environment` | `Portfolio`             | Identifies the environment                      |
| `Project`     | `Azure-Cloud-Portfolio` | Identifies the project                          |

**What I learned:** Tags help organize Azure resources, identify ownership and support cost tracking and reporting.

## 3. Access Management with Azure RBAC

I created an Entra ID security group named `Compute-ReadOnly` and added my user account to it.

I assigned the Reader role to this group at the `rg-compute` scope.

My own account also has the Owner role at the subscription scope.

**What I learned:** Azure Role-Based Access Control (RBAC) allows me to control who can access resources and what actions they can perform. Assigning permissions at the resource group level helps limit access to the resources that users need.

## 4. Resource Lock

I created a resource lock named `lock-protect-compute` on `rg-compute`.

The lock type is `CanNotDelete`, which helps prevent the resource group from being accidentally deleted.

**What I learned:** Resource locks provide an additional layer of protection against accidental changes or deletion. They do not replace access permissions, and they can affect authorized users as well.

## Project Status

The three resource groups have been created and tagged. Basic access management has been configured using an Entra ID security group and Azure RBAC. A resource lock has also been added to help protect the compute resource group.

These steps provide a foundation for organizing and managing my Azure environment as I continue building my cloud portfolio.
