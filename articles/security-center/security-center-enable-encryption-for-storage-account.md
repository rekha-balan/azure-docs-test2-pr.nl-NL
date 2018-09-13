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
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="9c79b-103">Enable encryption for Azure storage account in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="9c79b-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="9c79b-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span><span class="sxs-lookup"><span data-stu-id="9c79b-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="9c79b-105">Storage Service Encryption (SSE) works by encrypting the data when it is written to Azure storage and decrypting the data before retrieval.</span><span class="sxs-lookup"><span data-stu-id="9c79b-105">Storage Service Encryption (SSE) works by encrypting the data when it is written to Azure storage and decrypting the data before retrieval.</span></span>  <span data-ttu-id="9c79b-106">SSE is currently available only for the Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span><span class="sxs-lookup"><span data-stu-id="9c79b-106">SSE is currently available only for the Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="9c79b-107">To learn more, see [Storage Service Encryption for data at rest](../storage/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="9c79b-107">To learn more, see [Storage Service Encryption for data at rest](../storage/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="9c79b-108">After enabling encryption, only new data is encrypted.</span><span class="sxs-lookup"><span data-stu-id="9c79b-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="9c79b-109">Any existing blobs in your storage account remain unencrypted.</span><span class="sxs-lookup"><span data-stu-id="9c79b-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="9c79b-110">To encrypt existing blobs, see the [Storage Service Encryption FAQ](../storage/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span><span class="sxs-lookup"><span data-stu-id="9c79b-110">To encrypt existing blobs, see the [Storage Service Encryption FAQ](../storage/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="9c79b-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span><span class="sxs-lookup"><span data-stu-id="9c79b-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="9c79b-112">Classic storage accounts are not currently supported.</span><span class="sxs-lookup"><span data-stu-id="9c79b-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="9c79b-113">To understand the classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="9c79b-113">To understand the classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9c79b-114">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="9c79b-114">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="9c79b-115">This document is not a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="9c79b-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="9c79b-116">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="9c79b-116">Implement the recommendation</span></span>
1. <span data-ttu-id="9c79b-117">In the **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="9c79b-117">In the **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="9c79b-118">![Enable encryption for storage account][1]</span><span class="sxs-lookup"><span data-stu-id="9c79b-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="9c79b-119">The **Enable storage encryption** blade opens.</span><span class="sxs-lookup"><span data-stu-id="9c79b-119">The **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="9c79b-120">This blade lists the Azure storage accounts where storage encryption is disabled.</span><span class="sxs-lookup"><span data-stu-id="9c79b-120">This blade lists the Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="9c79b-121">In this example, let's select **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="9c79b-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="9c79b-122">![Enable storage encryption][2]</span><span class="sxs-lookup"><span data-stu-id="9c79b-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="9c79b-123">The **Encryption** blade for **storageacct1** opens.</span><span class="sxs-lookup"><span data-stu-id="9c79b-123">The **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="9c79b-124">Select **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="9c79b-124">Select **Enabled**.</span></span>
   <span data-ttu-id="9c79b-125">![Encryption blade][3]</span><span class="sxs-lookup"><span data-stu-id="9c79b-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="9c79b-126">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="9c79b-126">Select **Save**.</span></span>

<span data-ttu-id="9c79b-127">You have now enabled storage encryption for **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="9c79b-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="9c79b-128">See also</span><span class="sxs-lookup"><span data-stu-id="9c79b-128">See also</span></span>
<span data-ttu-id="9c79b-129">This document showed you how to implement the Security Center recommendation "Enable encryption for Azure Storage Account."</span><span class="sxs-lookup"><span data-stu-id="9c79b-129">This document showed you how to implement the Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="9c79b-130">To learn more about Azure Storage Service Encryption, see the following:</span><span class="sxs-lookup"><span data-stu-id="9c79b-130">To learn more about Azure Storage Service Encryption, see the following:</span></span>

* [<span data-ttu-id="9c79b-131">Azure Storage Service Encryption for Data at Rest</span><span class="sxs-lookup"><span data-stu-id="9c79b-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/storage-service-encryption.md)

<span data-ttu-id="9c79b-132">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="9c79b-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="9c79b-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="9c79b-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="9c79b-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="9c79b-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="9c79b-135">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="9c79b-135">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="9c79b-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="9c79b-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="9c79b-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="9c79b-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="9c79b-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span><span class="sxs-lookup"><span data-stu-id="9c79b-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-encryption-for-storage-account/encryption-blade.png



