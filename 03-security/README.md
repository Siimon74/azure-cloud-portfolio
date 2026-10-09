# 03 - Azure Security

This is the security part of my Azure Cloud Portfolio project.

My goal is to learn how to control access to Azure resources, protect secrets and understand the basic security tools available in Azure.

## 1. Identity and Access

* Created an Entra ID security group named `Compute-ReadOnly`.
* Assigned the Reader role to the group on `rg-compute`.
* Created a resource lock on `rg-compute` to help prevent accidental changes or deletion.

**What I learned:** Azure RBAC lets me control who can access resources and what they can do. Assigning permissions at the resource group level also helps limit access to the resources that a user needs.

## 2. Key Vault and Managed Identity

* Created an Azure Key Vault and stored a test secret.
* Enabled soft-delete protection.
* Configured Azure RBAC for Key Vault permissions.
* Enabled Managed Identity on my virtual machine.
* Used Azure CLI from the VM to access the test secret without storing Azure credentials in a script.

**What I learned:** Key Vault stores secrets, while Managed Identity allows an Azure resource to authenticate without having to manage credentials manually.

## 3. Microsoft Defender for Cloud

* Explored Microsoft Defender for Cloud.
* Checked the Microsoft Cloud Security Benchmark security policy.
* Configured email notifications for high-severity security alerts and attack paths.
* Reviewed the security recommendations for my subscription.

Some recommendations are still marked as `Not evaluated`, so I cannot confirm that all security checks have been completed.

**What I learned:** Defender for Cloud helps identify security improvements, but some features require paid plans. I chose not to enable paid plans just for this learning project.

## 4. Improvements to Make

* Enable Key Vault diagnostic logs and connect them to Log Analytics.
* Review the network security settings of Key Vault.
* Check virtual machine disk encryption and update settings.
* Explore backup options and their costs.
* Review the remaining Defender for Cloud recommendations.

## Project Status

The basic access controls, Key Vault setup, Managed Identity test and Defender for Cloud notification settings are in place.

I will continue improving the security and monitoring of this environment as I learn more about Azure.
