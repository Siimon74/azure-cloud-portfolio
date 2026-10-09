# 03 - Azure Security

This section documents the security controls implemented in the Azure Cloud Portfolio environment.

## Objectives

* Manage access using Microsoft Entra ID and Azure RBAC
* Apply least-privilege access principles
* Protect secrets using Azure Key Vault
* Use Managed Identity to access Azure resources without storing credentials
* Explore Microsoft Defender for Cloud

## Implemented Security Controls

### 1. Microsoft Entra ID and RBAC

A security group named `Compute-ReadOnly` was created in Microsoft Entra ID.

The group was assigned the `Reader` role at the `rg-compute` resource group scope.

This allows group members to view Azure resources within the assigned scope without granting them permission to modify or delete those resources.

### 2. Azure Key Vault

Azure Key Vault was configured to store a secret securely.

Soft-delete was enabled to help protect against accidental deletion and allow recovery during the configured retention period.

Azure RBAC was used as the Key Vault permission model.

### 3. Managed Identity

A Managed Identity was enabled on the Azure virtual machine.

This identity allows the VM to authenticate to supported Azure services without storing a username, password, or service principal secret in the application or script.

### 4. Secure Secret Retrieval

Azure CLI was used from the virtual machine to authenticate through its Managed Identity and retrieve a secret from Azure Key Vault.

This demonstrated the access flow:

`Virtual Machine → Managed Identity → Microsoft Entra ID → Azure RBAC → Key Vault`

The secret value was not committed to the GitHub repository.

## Security Principles Demonstrated

* Least-privilege access through Azure RBAC
* Centralized secret management
* Identity-based authentication instead of stored credentials
* Separation of identity permissions and network security controls

## Further Improvements

* Review Microsoft Defender for Cloud recommendations
* Evaluate additional monitoring and security alerts
* Document security testing and configuration decisions

## Status

Implemented security controls documented. Further security improvements remain planned.
