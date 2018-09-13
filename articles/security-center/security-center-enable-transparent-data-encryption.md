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
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 13e47de8ff25451f7d4185927477d524d519ce2a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805433"
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="33a55-103">Enable Transparent Data Encryption in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="33a55-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="33a55-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span><span class="sxs-lookup"><span data-stu-id="33a55-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="33a55-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes to your application.</span><span class="sxs-lookup"><span data-stu-id="33a55-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes to your application.</span></span> <span data-ttu-id="33a55-106">To learn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span><span class="sxs-lookup"><span data-stu-id="33a55-106">To learn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="33a55-107">This recommendation applies to the Azure SQL service only; doesn't include SQL running on your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="33a55-107">This recommendation applies to the Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="33a55-108">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="33a55-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="33a55-109">This is not a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="33a55-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="33a55-110">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="33a55-110">Implement the recommendation</span></span>
1. <span data-ttu-id="33a55-111">In the **Recommendations** blade, select **Enable Transparent Data Encryption**.</span><span class="sxs-lookup"><span data-stu-id="33a55-111">In the **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="33a55-112">![Enable Transparent Data Encryption][1]</span><span class="sxs-lookup"><span data-stu-id="33a55-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="33a55-113">This opens the **Enable Transparent Data Encryption on SQL databases** blade.</span><span class="sxs-lookup"><span data-stu-id="33a55-113">This opens the **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="33a55-114">Select a SQL database to enable TDE on.</span><span class="sxs-lookup"><span data-stu-id="33a55-114">Select a SQL database to enable TDE on.</span></span>
   <span data-ttu-id="33a55-115">![Select SQL DB to enable TDE on][2]</span><span class="sxs-lookup"><span data-stu-id="33a55-115">![Select SQL DB to enable TDE on][2]</span></span>
3. <span data-ttu-id="33a55-116">On the **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in the top ribbon of the blade.</span><span class="sxs-lookup"><span data-stu-id="33a55-116">On the **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in the top ribbon of the blade.</span></span>
   <span data-ttu-id="33a55-117">![Turn on TDE][3]</span><span class="sxs-lookup"><span data-stu-id="33a55-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="33a55-118">Once TDE is enabled on the selected SQL database, the **Encryption status** will change to **Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="33a55-118">Once TDE is enabled on the selected SQL database, the **Encryption status** will change to **Encrypted**.</span></span>    

   ![Encryption status][4]

## <a name="see-also"></a><span data-ttu-id="33a55-120">See also</span><span class="sxs-lookup"><span data-stu-id="33a55-120">See also</span></span>
<span data-ttu-id="33a55-121">This article showed you how to implement the Security Center recommendation "Enable Transparent Data Encryption."</span><span class="sxs-lookup"><span data-stu-id="33a55-121">This article showed you how to implement the Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="33a55-122">To learn more about SQL TDE, see the following:</span><span class="sxs-lookup"><span data-stu-id="33a55-122">To learn more about SQL TDE, see the following:</span></span>

* [<span data-ttu-id="33a55-123">Transparent Data Encryption with Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="33a55-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="33a55-124">Get started with Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="33a55-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="33a55-125">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="33a55-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="33a55-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="33a55-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="33a55-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="33a55-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="33a55-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="33a55-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="33a55-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="33a55-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="33a55-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="33a55-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="33a55-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="33a55-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="33a55-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span><span class="sxs-lookup"><span data-stu-id="33a55-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
