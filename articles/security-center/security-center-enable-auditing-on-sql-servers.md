---
title: Enable auditing and threat detection on SQL servers in Azure Security Center | Microsoft Docs
description: This document shows you how to implement the Azure Security Center recommendation **Enable Auditing & Threat detection on SQL servers**.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: fade8de73a35b75f6096a25af13335d679caffac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44780694"
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a><span data-ttu-id="173fe-103">Enable auditing and threat detection on SQL servers in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="173fe-103">Enable auditing and threat detection on SQL servers in Azure Security Center</span></span>
<span data-ttu-id="173fe-104">Azure Security Center will recommend that you turn on auditing and threat detection for all databases on your Azure SQL servers if auditing is not already enabled.</span><span class="sxs-lookup"><span data-stu-id="173fe-104">Azure Security Center will recommend that you turn on auditing and threat detection for all databases on your Azure SQL servers if auditing is not already enabled.</span></span> <span data-ttu-id="173fe-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span><span class="sxs-lookup"><span data-stu-id="173fe-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="173fe-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts.</span><span class="sxs-lookup"><span data-stu-id="173fe-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts.</span></span> <span data-ttu-id="173fe-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span><span class="sxs-lookup"><span data-stu-id="173fe-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="173fe-108">This enables you to detect and respond to potential threats as they occur.</span><span class="sxs-lookup"><span data-stu-id="173fe-108">This enables you to detect and respond to potential threats as they occur.</span></span>

<span data-ttu-id="173fe-109">This recommendation applies to the Azure SQL service only; it doesn’t include SQL Server running on your virtual machines in Azure Infrastructure Services (Azure IaaS).</span><span class="sxs-lookup"><span data-stu-id="173fe-109">This recommendation applies to the Azure SQL service only; it doesn’t include SQL Server running on your virtual machines in Azure Infrastructure Services (Azure IaaS).</span></span>

> [!NOTE]
> <span data-ttu-id="173fe-110">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="173fe-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="173fe-111">This is not a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="173fe-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="173fe-112">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="173fe-112">Implement the recommendation</span></span>
1. <span data-ttu-id="173fe-113">In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL servers**.</span><span class="sxs-lookup"><span data-stu-id="173fe-113">In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL servers**.</span></span>  <span data-ttu-id="173fe-114">This opens the **Enable Auditing & Threat detection on SQL servers** blade.</span><span class="sxs-lookup"><span data-stu-id="173fe-114">This opens the **Enable Auditing & Threat detection on SQL servers** blade.</span></span>

   ![Enable auditing on SQL servers][1]
2. <span data-ttu-id="173fe-116">Select a SQL server to enable auditing and threat detection on.</span><span class="sxs-lookup"><span data-stu-id="173fe-116">Select a SQL server to enable auditing and threat detection on.</span></span> <span data-ttu-id="173fe-117">This opens the **Auditing & Threat Detection** blade.</span><span class="sxs-lookup"><span data-stu-id="173fe-117">This opens the **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="173fe-118">On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span><span class="sxs-lookup"><span data-stu-id="173fe-118">On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Turn on auditing settings][2]
4. <span data-ttu-id="173fe-120">Follow the steps in [SQL database auditing in the Azure portal](../sql-database/sql-database-auditing-portal.md) to configure storage where your audit logs will be stored.</span><span class="sxs-lookup"><span data-stu-id="173fe-120">Follow the steps in [SQL database auditing in the Azure portal](../sql-database/sql-database-auditing-portal.md) to configure storage where your audit logs will be stored.</span></span> <span data-ttu-id="173fe-121">The subscription's storage account for data collection is the default storage account.</span><span class="sxs-lookup"><span data-stu-id="173fe-121">The subscription's storage account for data collection is the default storage account.</span></span>
5. <span data-ttu-id="173fe-122">Follow the steps in [Get started with SQL Database Threat Detection](../sql-database/sql-database-threat-detection.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.</span><span class="sxs-lookup"><span data-stu-id="173fe-122">Follow the steps in [Get started with SQL Database Threat Detection](../sql-database/sql-database-threat-detection.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="173fe-123">See also</span><span class="sxs-lookup"><span data-stu-id="173fe-123">See also</span></span>
<span data-ttu-id="173fe-124">This article showed you how to implement the Security Center recommendation "Enable auditing and threat detection on SQL servers."</span><span class="sxs-lookup"><span data-stu-id="173fe-124">This article showed you how to implement the Security Center recommendation "Enable auditing and threat detection on SQL servers."</span></span> <span data-ttu-id="173fe-125">To learn more about securing your SQL database, see the following:</span><span class="sxs-lookup"><span data-stu-id="173fe-125">To learn more about securing your SQL database, see the following:</span></span>

* [<span data-ttu-id="173fe-126">Securing your SQL Database</span><span class="sxs-lookup"><span data-stu-id="173fe-126">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="173fe-127">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="173fe-127">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="173fe-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="173fe-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="173fe-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="173fe-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="173fe-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="173fe-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="173fe-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="173fe-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="173fe-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="173fe-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="173fe-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="173fe-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="173fe-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span><span class="sxs-lookup"><span data-stu-id="173fe-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
