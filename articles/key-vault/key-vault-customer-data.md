---
title: Azure Key Vault customer data features | Microsoft Docs
description: Learn about customer data in Key Vault
services: key-vault
documentationcenter: ''
author: barclayn
manager: mbaldwin
tags: azure-resource-manager
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 05/22/2018
ms.author: barclayn
ms.openlocfilehash: 359648a843375477ea56ab791533208c11af9c81
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864706"
---
# <a name="azure-key-vault-customer-data-features"></a>Azure Key Vault customer data features

Azure Key Vault receives customer data during creation or update of vaults, keys, secrets, certificates, and managed storage accounts. This Customer data is directly visible in the Azure portal and through the REST API. Customer data can be edited or deleted by updating or deleting the object that contains the data.

System access logs are generated when a user or application accesses Key Vault. Detailed access logs are available to customers using Azure Insights.

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-intro-sentence.md)]

## <a name="identifying-customer-data"></a>Identifying customer data

The following information identifies customer data within Azure Key Vault:

- Access policies for Azure Key Vault contain object-IDs representing users, groups, or applications
- Certificate subjects may include email addresses or other user or organizational identifiers
- Certificate contacts may contain user email addresses, names, or phone numbers
- Certificate issuers may contain email addresses, names, phone numbers, account credentials, and organizational details
- Arbitrary tags can be applied to Objects in Azure Key Vault. These objects include vaults, keys, secrets, certificates, and storage accounts. The tags used may contain personal data
- Azure Key Vault access logs contain object-IDs, [UPNs](../active-directory/connect/active-directory-aadconnect-userprincipalname.md), and IP addresses for each REST API call
- Azure Key Vault diagnostic logs may contain object-IDs and IP addresses for REST API calls

## <a name="deleting-customer-data"></a>Deleting customer data

The same REST APIs, Portal experience, and SDKs used to create vaults, keys, secrets, certificates, and managed storage accounts, are also able to update and delete these objects.

Soft delete allows you to recover deleted data for 90 days after deletion. When using soft delete, the data may be permanently deleted prior to the 90 days retention period expires by performing a purge operation. If the vault or subscription has been configured to block purge operations, it is not possible to permanently delete data until the scheduled retention period has passed.

## <a name="exporting-customer-data"></a>Exporting customer data

The same REST APIs, portal experience, and SDKs that are used to create vaults, keys, secrets, certificates, and managed storage accounts  also allow you to view and export these objects.

Azure Key Vault access logging is an optional feature that can be turned on to generate logs for each REST API call. These logs will be transferred to a storage account in your subscription where you apply the retention policy that meets your organization's requirements.

Azure Key Vault diagnostic logs that contain personal data can be retrieved by making an export request in the User Privacy portal. This request must be made by the tenant administrator.

## <a name="next-steps"></a>Next steps

- [Azure Key Vault Logging](key-vault-logging.md)

- [Azure Key Vault soft-delete overview](key-vault-soft-delete-cli.md)

- [Azure Key Vault key operations](https://docs.microsoft.com/rest/api/keyvault/key-operations)

- [Azure Key Vault secret operations](https://docs.microsoft.com/rest/api/keyvault/secret-operations)

- [Azure Key Vault certificates and policies](https://docs.microsoft.com/rest/api/keyvault/certificates-and-policies)

- [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations)
