# 03 - Azure Security

This section documents the security controls implemented in my Azure Cloud Portfolio environment.

## Objectives

* Manage access using Microsoft Entra ID and Azure RBAC
* Apply the principle of least privilege
* Secure application secrets with Azure Key Vault
* Use Managed Identity to avoid storing credentials in scripts
* Configure security notifications with Microsoft Defender for Cloud
* Identify additional security improvements and monitoring requirements

## Identity and Access Management

### Microsoft Entra ID and Azure RBAC

* Created an Entra ID security group named `Compute-ReadOnly`
* Added the relevant user account to the group
* Assigned the **Reader** role at the `rg-compute` resource group scope
* Kept administrative permissions separate from read-only access

This demonstrates how access can be granted according to job responsibilities and limited to the required scope.

### Resource Protection

* Created a resource lock named `lock-protect-compute` on `rg-compute`
* Used the lock to help protect resources against accidental deletion or modification, according to the lock type and Azure operation

## Azure Key Vault and Managed Identity

### Key Vault Configuration

* Created an Azure Key Vault to store a test secret
* Enabled soft-delete protection
* Configured Azure RBAC as the Key Vault permission model

### Managed Identity

* Enabled a Managed Identity on the `vm-portfolio` virtual machine
* Granted the identity the required permissions to access the Key Vault secret
* Used Azure CLI from the virtual machine to authenticate through Managed Identity
* Successfully retrieved the test secret without storing Azure credentials in the VM's scripts

This demonstrates passwordless authentication between an Azure resource and Key Vault using Microsoft Entra ID and Azure RBAC.

**Security note:** Secret values and credentials are not included in this repository.

## Microsoft Defender for Cloud

### Security Posture

* Reviewed Microsoft Defender for Cloud for the Azure subscription
* Confirmed that the Microsoft Cloud Security Benchmark security policy is enabled
* Reviewed security recommendations and identified areas requiring further evaluation

### Security Notifications

* Configured email recipients for security notifications
* Configured notifications for high-severity security alerts
* Configured the notification threshold for attack paths

These settings help ensure that important security alerts can reach the configured recipients.

**Note:** Some Defender for Cloud recommendations remain marked as `Not evaluated`. This does not confirm that the associated resources are compliant or secure.

## Improvements Identified

The following improvements have been identified and remain planned or require further verification:

* Configure Key Vault diagnostic logs and connect them to Azure Monitor / Log Analytics
* Review Key Vault network access restrictions and private endpoint options
* Review virtual machine disk encryption and host encryption settings
* Review operating system update management
* Review backup requirements and associated costs
* Review Defender for Cloud recommendations and available free security features

Paid Defender plans and additional resources will only be enabled when justified by the learning objectives and budget.

## Cost Management

* Avoided enabling paid Defender plans that are not required for this portfolio stage
* Considered the potential costs of log ingestion, storage, backups and additional security services before implementation

## Key Learnings

* Azure RBAC controls who can access resources and what actions they can perform
* Managed Identity allows Azure resources to authenticate without embedding credentials in code
* Azure Key Vault centralizes secret storage and access control
* Security notifications help improve incident awareness
* Defender for Cloud recommendations require evaluation; an unevaluated recommendation is not proof of compliance
* Security improvements must be balanced with operational requirements and cost management

## Status

**Implemented:** Identity and access controls, Key Vault secret access through Managed Identity, resource protection, and Defender for Cloud email notification settings.

**Further work planned:** Key Vault diagnostic logging, additional security configuration reviews, and monitoring integration.
