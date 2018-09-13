---
title: Azure Government Security + Identity | Microsoft Docs
description: This provides a comparision of features and guidance on developing applications for Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: ryansoc
manager: zakramer
ms.assetid: e2fe7983-5870-43e9-ae01-2d45d3102c8a
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 11/14/2016
ms.author: ryansoc
ms.openlocfilehash: 2c3a3eec41dfb6860eb680694023b82099290b7f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550049"
---
# <a name="azure-government-security--identity"></a>Azure Government Security + Identity
## <a name="key-vault"></a>Key Vault
For details on this service and how to use it, see the [Azure Key Vault public documentation](../key-vault/index.md).

### <a name="data-considerations"></a>Data Considerations
The following information identifies the Azure Government boundary for Azure Key Vault:

| Regulated/controlled data permitted | Regulated/controlled data not permitted |
| --- | --- |
| All data encrypted with an Azure Key Vault key may contain Regulated/controlled data. |Azure Key Vault metadata is not permitted to contain export controlled data. This metadata includes all configuration data entered when creating and maintaining your Key Vault.  Do not enter Regulated/controlled data into the following fields: Resource group names, Key Vault names, Subscription name |

Key Vault is generally available in Azure Government. As in public, there is no extension, so Key Vault is available through PowerShell and CLI only.

## <a name="next-steps"></a>Next Steps
For supplemental information and updates, subscribe to the <a href="https://blogs.msdn.microsoft.com/azuregov/">Microsoft Azure Government Blog. </a>

