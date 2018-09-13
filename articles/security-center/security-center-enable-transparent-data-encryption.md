---
title: Enable Transparent Data Encryption in Azure Security Center | Microsoft Docs
description: This document shows you how to implement the Azure Security Center recommendation **Enable Transparent Data Encryption**.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: c3dee017cfe6ed3355840d5f9fa784150742b1ae
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563062"
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="c5d81-103">Enable Transparent Data Encryption in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="c5d81-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="c5d81-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span><span class="sxs-lookup"><span data-stu-id="c5d81-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="c5d81-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes to your application.</span><span class="sxs-lookup"><span data-stu-id="c5d81-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes to your application.</span></span> <span data-ttu-id="c5d81-106">To learn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span><span class="sxs-lookup"><span data-stu-id="c5d81-106">To learn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="c5d81-107">This recommendation applies to the Azure SQL service only; doesn't include SQL running on your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="c5d81-107">This recommendation applies to the Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="c5d81-108">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="c5d81-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="c5d81-109">This is not a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="c5d81-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="c5d81-110">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="c5d81-110">Implement the recommendation</span></span>
1. <span data-ttu-id="c5d81-111">In the **Recommendations** blade, select **Enable Transparent Data Encryption**.</span><span class="sxs-lookup"><span data-stu-id="c5d81-111">In the **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="c5d81-112">![Enable Transparent Data Encryption][1]</span><span class="sxs-lookup"><span data-stu-id="c5d81-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="c5d81-113">This opens the **Enable Transparent Data Encryption on SQL databases** blade.</span><span class="sxs-lookup"><span data-stu-id="c5d81-113">This opens the **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="c5d81-114">Select a SQL database to enable TDE on.</span><span class="sxs-lookup"><span data-stu-id="c5d81-114">Select a SQL database to enable TDE on.</span></span>
   <span data-ttu-id="c5d81-115">![Select SQL DB to enable TDE on][2]</span><span class="sxs-lookup"><span data-stu-id="c5d81-115">![Select SQL DB to enable TDE on][2]</span></span>
3. <span data-ttu-id="c5d81-116">On the **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in the top ribbon of the blade.</span><span class="sxs-lookup"><span data-stu-id="c5d81-116">On the **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in the top ribbon of the blade.</span></span>
   <span data-ttu-id="c5d81-117">![Turn on TDE][3]</span><span class="sxs-lookup"><span data-stu-id="c5d81-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="c5d81-118">Once TDE is enabled on the selected SQL database, the **Encryption status** will change to **Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="c5d81-118">Once TDE is enabled on the selected SQL database, the **Encryption status** will change to **Encrypted**.</span></span>    

   ![Encryption status][4]

## <a name="see-also"></a><span data-ttu-id="c5d81-120">See also</span><span class="sxs-lookup"><span data-stu-id="c5d81-120">See also</span></span>
<span data-ttu-id="c5d81-121">This article showed you how to implement the Security Center recommendation "Enable Transparent Data Encryption."</span><span class="sxs-lookup"><span data-stu-id="c5d81-121">This article showed you how to implement the Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="c5d81-122">To learn more about SQL TDE, see the following:</span><span class="sxs-lookup"><span data-stu-id="c5d81-122">To learn more about SQL TDE, see the following:</span></span>

* [<span data-ttu-id="c5d81-123">Transparent Data Encryption with Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="c5d81-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="c5d81-124">Get started with Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="c5d81-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="c5d81-125">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="c5d81-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="c5d81-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="c5d81-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="c5d81-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="c5d81-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="c5d81-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="c5d81-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="c5d81-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="c5d81-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="c5d81-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="c5d81-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="c5d81-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="c5d81-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="c5d81-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span><span class="sxs-lookup"><span data-stu-id="c5d81-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-tde-on-sql-databases/encrypted.png




