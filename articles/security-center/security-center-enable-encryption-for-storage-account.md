---
title: Enable encryption for storage account in Azure Security Center | Microsoft Docs
description: This document shows you how to implement the Azure Security Center recommendations **Enable encryption for Azure Storage Account**.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: ''
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: f5264fe61f3b3cd72bbaf05454e231190455d898
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555266"
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a>Enable encryption for Azure storage account in Azure Security Center
Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.

Storage Service Encryption (SSE) works by encrypting the data when it is written to Azure storage and decrypting the data before retrieval.  SSE is currently available only for the Azure Blob service and can be used for block blobs, page blobs, and append blobs.  To learn more, see [Storage Service Encryption for data at rest](../storage/storage-service-encryption.md).


> [!Note]
> After enabling encryption, only new data is encrypted. Any existing blobs in your storage account remain unencrypted. To encrypt existing blobs, see the [Storage Service Encryption FAQ](../storage/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).
>
>

Storage Service Encryption is only supported on Resource Manager storage accounts. Classic storage accounts are not currently supported. To understand the classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).

> [!NOTE]
> This document introduces the service by using an example deployment.  This document is not a step-by-step guide.
>
>

## <a name="implement-the-recommendation"></a>Implement the recommendation
1. In the **Recommendations** blade, select **Enable encryption for Azure Storage Account**.
   ![Enable encryption for storage account][1]
2. The **Enable storage encryption** blade opens. This blade lists the Azure storage accounts where storage encryption is disabled. In this example, let's select **storageacct1**.
   ![Enable storage encryption][2]
3. The **Encryption** blade for **storageacct1** opens. Select **Enabled**.
   ![Encryption blade][3]
4. Select **Save**.

You have now enabled storage encryption for **storageacct1**.


## <a name="see-also"></a>See also
This document showed you how to implement the Security Center recommendation "Enable encryption for Azure Storage Account." To learn more about Azure Storage Service Encryption, see the following:

* [Azure Storage Service Encryption for Data at Rest](../storage/storage-service-encryption.md)

To learn more about Security Center, see the following:

* [Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.
* [Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.
* [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.
* [Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.
* [Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-encryption-for-storage-account/encryption-blade.png



