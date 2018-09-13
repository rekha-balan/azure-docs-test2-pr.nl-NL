---
title: Key Vault Developer's Guide | Microsoft Docs
description: Developers can use Azure Key Vault to manage cryptographic keys within the Microsoft Azure environment.
services: key-vault
documentationcenter: ''
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper
ms.assetid: b2b1bd28-e149-4d69-b08b-97f6c50ebe30
ms.service: key-vault
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/18/2017
ms.author: bruceper
ms.openlocfilehash: f71ffdaa691f83d8bb6413032de4c188fe7e6312
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552411"
---
# <a name="azure-key-vault-developers-guide"></a>Azure Key Vault Developer's Guide

Using Key Vault, you are able to securely access sensitive information from within your applications such that:

* Keys and secrets are protected without having to write the code yourself and you are easily able to use them from your applications.
* You are able to have your customers own and manage their own keys so you can concentrate on providing the core software features. In this way, your applications will not own the responsibility or potential liability for your customers’ tenant keys and secrets.
* Your application can use keys for signing and encryption yet keeps the key management external from your application, allowing your solution to be suitable as a geographically distributed app.
* With the September 2016 release of Key Vault, your applications can now make use of Key Vault certificates. For more information, see **About keys, secrets, and certificates** article in the [REST reference](https://msdn.microsoft.com/library/azure/dn903623.aspx).

For more general information on Azure Key Vault, see [What is Key Vault](key-vault-whatis.md).

## <a name="videos"></a>Videos

This video shows you how to create your own key vault and how to use it from the 'Hello Key Vault' sample application.


>[!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Key-Vault-Developer-Quick-Start/player]


Links to resources mentioned in the video:

* [Azure PowerShell](http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409)
* [Azure Key Vault Sample Code](http://go.microsoft.com/fwlink/?LinkId=521527&clcid=0x409)

To learn more you can follow the [Key Vault Blog](http://aka.ms/kvblog) and participate in the [Key Vault Forum](http://aka.ms/kvforum).

## <a name="creating-and-managing-key-vaults"></a>Creating and Managing Key Vaults

Before working with Azure Key Vault in your code, you can create and manage vaults through REST, Resource Manager Templates, PowerShell or CLI, as described in the following articles:

* [Create and Manage Key Vaults with REST](https://msdn.microsoft.com/library/azure/mt620024.aspx)
* [Create and Manage Key Vaults with PowerShell](key-vault-get-started.md)
* [Create and Manage Key Vaults with CLI](key-vault-manage-with-cli.md)
* [Create a key vault and add a secret via an Azure Resource Manager template](../azure-resource-manager/resource-manager-template-keyvault.md)

> [!NOTE]
> Operations against key vaults are authenticated through AAD and authorized through Key Vault’s own Access Policy, defined per vault.

## <a name="coding-with-key-vault"></a>Coding with Key Vault

The Key Vault management system for programmers consists of several interfaces, with REST as the foundation, [Key Vault REST API Reference](https://msdn.microsoft.com/library/azure/dn903609.aspx).

You can, subject to successful authorization, perform any of the following operations.

* Manage cryptographic keys using [Create](https://msdn.microsoft.com/library/azure/dn903634.aspx), [Import](https://msdn.microsoft.com/library/azure/dn903626.aspx), [Update](https://msdn.microsoft.com/library/azure/dn903616.aspx), [Delete](https://msdn.microsoft.com/library/azure/dn903611.aspx) and, other operations
* Manage secrets using [Get](https://msdn.microsoft.com/library/azure/dn903633.aspx), [Update](https://msdn.microsoft.com/library/azure/dn986818.aspx), [Delete](https://msdn.microsoft.com/library/azure/dn903613.aspx) and, other operations
* Use cryptographic keys with [Sign](https://msdn.microsoft.com/library/azure/dn878096.aspx)/[Verify](https://msdn.microsoft.com/library/azure/dn878082.aspx), [WrapKey](https://msdn.microsoft.com/library/azure/dn878066.aspx)/[UnwrapKey](https://msdn.microsoft.com/library/azure/dn878079.aspx) and, [Encrypt](https://msdn.microsoft.com/library/azure/dn878060.aspx)/[Decrypt](https://msdn.microsoft.com/library/azure/dn878097.aspx) operations

The following SDKs are available for working with Key Vault:

| [![.NET](https://docstestmedia1.blob.core.windows.net/azure-media/articles/key-vault/media/key-vault-developers-guide/msft.netlogo_purple.png)](https://msdn.microsoft.com/library/mt765854.aspx) | [![Node.js](https://docstestmedia1.blob.core.windows.net/azure-media/articles/key-vault/media/key-vault-developers-guide/nodejs.png)](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest) |
|:---:|:---:|
| [.NET SDK Documentation](https://msdn.microsoft.com/library/mt765854.aspx) |[Node.js SDK Documentation](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest) |
| [.NET SDK Package on NuGet](http://www.nuget.org/packages/Microsoft.Azure.KeyVault) |[Node.js SDK Package](https://www.npmjs.com/package/azure-keyvault) |

For more information on the 2.x version of the .NET SDK, see the [Release notes](key-vault-dotnet2api-release-notes.md).

## <a name="example-code"></a>Example code

For complete examples using Key Vault with your applications, see:

* .NET sample application *HelloKeyVault* and an Azure web service example. [Azure Key Vault code samples](http://www.microsoft.com/download/details.aspx?id=45343)
* Tutorial to help you learn how to use Azure Key Vault from a web application in Azure. [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md)

## <a name="how-tos"></a>How-tos

The following articles and scenarios provide task-specific guidance for working with Azure Key Vault:

* [Change key vault tenant ID after subscription move](key-vault-subscription-move-fix.md) - When you move your Azure subscription from tenant A to tenant B, your existing key vaults are inaccessible by the principals (users and applications) in tenant B. Fix this using this guide.
* [Accessing Key Vault behind firewall](key-vault-access-behind-firewall.md) - To access a key vault your key vault client application needs to be able to access multiple end-points for various functionalities.
* [How to Generate and Transfer HSM-Protected Keys for Azure Key Vault](key-vault-hsm-protected-keys.md) - This will help you plan for, generate and then transfer your own HSM-protected keys to use with Azure Key Vault.
* [How to pass secure values (such as passwords) during deployment](../azure-resource-manager/resource-manager-keyvault-parameter.md) - When you need to pass a secure value (like a password) as a parameter during deployment, you can store that value as a secret in an Azure Key Vault and reference the value in other Resource Manager templates.
* [How to use Key Vault for extensible key management with SQL Server](https://msdn.microsoft.com/library/dn198405.aspx) - The SQL Server Connector for Azure Key Vault enables SQL Server and SQL-in-a-VM to leverage the Azure Key Vault service as an Extensible Key Management (EKM) provider to protect its encryption keys for applications link; Transparent Data Encryption, Backup Encryption, and Column Level Encryption.
* [How to deploy Certificates to VMs from Key Vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) - A cloud application running in a VM on Azure needs a certificate. How do you get this certificate into this VM today?
* [How to set up Key Vault with end to end key rotation and auditing](key-vault-key-rotation-log-monitoring.md) - This walks through how to set up key rotation and auditing with Azure Key Vault.
* [Deploying Azure Web App Certificate through Key Vault]( https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/) provides step-by-step instructions for deploying certificates stored in Key Vault as part of [App Service Certificate](https://azure.microsoft.com/en-us/blog/internals-of-app-service-certificate/) offering.
* [Grant permission to many applications to access a key vault](key-vault-group-permissions-for-apps.md) Key Vault access control policy only supports 16 entries. However you can create an Azure Active Directory security group. Add all the associated service principals to this security group and then grant access to this security group to Key Vault.

For more task-specific guidance on integrating and using Key Vaults with Azure, see [Ryan Jones' Azure Resource Manager template examples for Key Vault](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).

## <a name="integrated-with-key-vault"></a>Integrated with Key Vault

These articles are about other scenarios and services that use or integrate with Key Vault.

* [Azure Disk Encryption](../security/azure-security-disk-encryption.md) leverages the industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and the [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux to provide volume encryption for the OS and the data disks. The solution is integrated with Azure Key Vault to help you control and manage the disk encryption keys and secrets in your key vault subscription, while ensuring that all data in the virtual machine disks are encrypted at rest in your Azure storage.
* [Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md) provides option for encryption of data that is stored in the account. For key management, Data Lake Store provides two modes for managing your master encryption keys (MEKs), which are required for decrypting any data that is stored in the Data Lake Store. You can either let Data Lake Store manage the MEKs for you, or choose to retain ownership of the MEKs using your Azure Key Vault account. You specify the mode of key management while creating a Data Lake Store account. 
* [Azure Information Protection](/information-protection/plan-design/plan-implement-tenant-key) allows you to manager your own tenant key. For example, instead of Microsoft managing your tenant key (the default), you can manage your own tenant key to comply with specific regulations that apply to your organization. Managing your own tenant key is also referred to as bring your own key, or BYOK.


## <a name="supporting-libraries"></a>Supporting Libraries

* [Microsoft Azure Key Vault Core Library](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core) provides **IKey** and **IKeyResolver** interfaces for locating keys from identifiers and performing operations with keys.
* [Microsoft Azure Key Vault Extensions](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions) provides extended capabilities for Azure Key Vault.

## <a name="other-key-vault-resources"></a>Other Key Vault resources

* [Key Vault Blog](http://aka.ms/kvblog)
* [Key Vault Forum](http://aka.ms/kvforum)


