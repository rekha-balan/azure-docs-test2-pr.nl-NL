---
title: Enable data collection in Azure Security Center | Microsoft Docs
description: " Learn how to enable data collection in Azure Security Center. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 411d7bae-c9d4-4e83-be63-9f2f2312b075
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2017
ms.author: terrylan
ms.openlocfilehash: 745e156eef3083ad094761cac177b86ae07ebf80
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563055"
---
# <a name="enable-data-collection-in-azure-security-center"></a><span data-ttu-id="a7447-103">Enable data collection in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="a7447-103">Enable data collection in Azure Security Center</span></span>
<span data-ttu-id="a7447-104">To help customers prevent, detect, and respond to threats, Azure Security Center collects and processes data about your Azure virtual machines, including configuration information, metadata, and event logs.</span><span class="sxs-lookup"><span data-stu-id="a7447-104">To help customers prevent, detect, and respond to threats, Azure Security Center collects and processes data about your Azure virtual machines, including configuration information, metadata, and event logs.</span></span> <span data-ttu-id="a7447-105">When you first access Security Center, data collection is enabled on all virtual machines in your subscription.</span><span class="sxs-lookup"><span data-stu-id="a7447-105">When you first access Security Center, data collection is enabled on all virtual machines in your subscription.</span></span> <span data-ttu-id="a7447-106">Data collection is recommended but you can opt-out by turning off data collection in the Security Center policy (see [Disabling data collection](#disabling-data-collection)).</span><span class="sxs-lookup"><span data-stu-id="a7447-106">Data collection is recommended but you can opt-out by turning off data collection in the Security Center policy (see [Disabling data collection](#disabling-data-collection)).</span></span> <span data-ttu-id="a7447-107">If you turn off data collection, Security Center recommends that you turn on data collection in the security policy for that subscription.</span><span class="sxs-lookup"><span data-stu-id="a7447-107">If you turn off data collection, Security Center recommends that you turn on data collection in the security policy for that subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="a7447-108">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="a7447-108">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="a7447-109">This is not a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="a7447-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="a7447-110">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="a7447-110">Implement the recommendation</span></span>
1. <span data-ttu-id="a7447-111">Select the **Recommendations** tile on the **Security Center** blade.</span><span class="sxs-lookup"><span data-stu-id="a7447-111">Select the **Recommendations** tile on the **Security Center** blade.</span></span>  <span data-ttu-id="a7447-112">This opens the **Recommendations** blade.</span><span class="sxs-lookup"><span data-stu-id="a7447-112">This opens the **Recommendations** blade.</span></span>
   <span data-ttu-id="a7447-113">![Security Center blade][1]</span><span class="sxs-lookup"><span data-stu-id="a7447-113">![Security Center blade][1]</span></span>
2. <span data-ttu-id="a7447-114">On the **Recommendations** blade, select **Enable data collection for subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="a7447-114">On the **Recommendations** blade, select **Enable data collection for subscriptions**.</span></span>  <span data-ttu-id="a7447-115">This opens the **Turn on data collection** blade.</span><span class="sxs-lookup"><span data-stu-id="a7447-115">This opens the **Turn on data collection** blade.</span></span>
   <span data-ttu-id="a7447-116">![Recommendations blade][2]</span><span class="sxs-lookup"><span data-stu-id="a7447-116">![Recommendations blade][2]</span></span>
3. <span data-ttu-id="a7447-117">On the **Turn on data collection** blade, select your subscription.</span><span class="sxs-lookup"><span data-stu-id="a7447-117">On the **Turn on data collection** blade, select your subscription.</span></span> <span data-ttu-id="a7447-118">The **Security policy** blade for that subscription opens.</span><span class="sxs-lookup"><span data-stu-id="a7447-118">The **Security policy** blade for that subscription opens.</span></span>
4. <span data-ttu-id="a7447-119">On the **Security policy** blade, select **On** under **Data collection** to automatically collect logs.</span><span class="sxs-lookup"><span data-stu-id="a7447-119">On the **Security policy** blade, select **On** under **Data collection** to automatically collect logs.</span></span> <span data-ttu-id="a7447-120">Turning on data collection provisions the monitoring extension on all current and new supported VMs in the subscription.</span><span class="sxs-lookup"><span data-stu-id="a7447-120">Turning on data collection provisions the monitoring extension on all current and new supported VMs in the subscription.</span></span>

   ![Security policy blade][3]

5. <span data-ttu-id="a7447-122">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="a7447-122">Select **Save**.</span></span>
6. <span data-ttu-id="a7447-123">Select **Choose a storage account per region**.</span><span class="sxs-lookup"><span data-stu-id="a7447-123">Select **Choose a storage account per region**.</span></span> <span data-ttu-id="a7447-124">For each region in which you have virtual machines running, you choose the storage account where data collected from those virtual machines is stored.</span><span class="sxs-lookup"><span data-stu-id="a7447-124">For each region in which you have virtual machines running, you choose the storage account where data collected from those virtual machines is stored.</span></span> <span data-ttu-id="a7447-125">If you do not choose a storage account for each region, a storage account is created for you and placed in the securitydata resource group.</span><span class="sxs-lookup"><span data-stu-id="a7447-125">If you do not choose a storage account for each region, a storage account is created for you and placed in the securitydata resource group.</span></span> <span data-ttu-id="a7447-126">In this example, we choose **newstoracct**.</span><span class="sxs-lookup"><span data-stu-id="a7447-126">In this example, we choose **newstoracct**.</span></span> <span data-ttu-id="a7447-127">You can change the storage account later by returning to the security policy for your subscription and choosing a different storage account.</span><span class="sxs-lookup"><span data-stu-id="a7447-127">You can change the storage account later by returning to the security policy for your subscription and choosing a different storage account.</span></span>
   <span data-ttu-id="a7447-128">![Choose a storage account][4]</span><span class="sxs-lookup"><span data-stu-id="a7447-128">![Choose a storage account][4]</span></span>
7. <span data-ttu-id="a7447-129">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="a7447-129">Select **OK**.</span></span>

> [!NOTE]
> <span data-ttu-id="a7447-130">We recommend that you turn on data collection and choose a storage account at the subscription level first.</span><span class="sxs-lookup"><span data-stu-id="a7447-130">We recommend that you turn on data collection and choose a storage account at the subscription level first.</span></span> <span data-ttu-id="a7447-131">Security policies can be set at the Azure subscription level and resource group level but configuration of data collection and storage account occurs at the subscription level only.</span><span class="sxs-lookup"><span data-stu-id="a7447-131">Security policies can be set at the Azure subscription level and resource group level but configuration of data collection and storage account occurs at the subscription level only.</span></span>
>
>

## <a name="after-data-collection-is-enabled"></a><span data-ttu-id="a7447-132">After data collection is enabled</span><span class="sxs-lookup"><span data-stu-id="a7447-132">After data collection is enabled</span></span>
<span data-ttu-id="a7447-133">Data collection is enabled via the Azure Monitoring Agent and the Azure Security Monitoring extension.</span><span class="sxs-lookup"><span data-stu-id="a7447-133">Data collection is enabled via the Azure Monitoring Agent and the Azure Security Monitoring extension.</span></span> <span data-ttu-id="a7447-134">The Azure Security Monitoring extension scans for various security relevant configurations and sends it into [Event Tracing for Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) traces.</span><span class="sxs-lookup"><span data-stu-id="a7447-134">The Azure Security Monitoring extension scans for various security relevant configurations and sends it into [Event Tracing for Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) traces.</span></span> <span data-ttu-id="a7447-135">In addition, the operating system creates event log entries.</span><span class="sxs-lookup"><span data-stu-id="a7447-135">In addition, the operating system creates event log entries.</span></span> <span data-ttu-id="a7447-136">The Azure Monitoring Agent reads event log entries and ETW traces and copies them to your storage account for analysis.</span><span class="sxs-lookup"><span data-stu-id="a7447-136">The Azure Monitoring Agent reads event log entries and ETW traces and copies them to your storage account for analysis.</span></span> <span data-ttu-id="a7447-137">The Monitoring Agent also copies crash dump files to your storage account.</span><span class="sxs-lookup"><span data-stu-id="a7447-137">The Monitoring Agent also copies crash dump files to your storage account.</span></span> <span data-ttu-id="a7447-138">This is the storage account you configured in the security policy.</span><span class="sxs-lookup"><span data-stu-id="a7447-138">This is the storage account you configured in the security policy.</span></span>

## <a name="disabling-data-collection"></a><span data-ttu-id="a7447-139">Disabling data collection</span><span class="sxs-lookup"><span data-stu-id="a7447-139">Disabling data collection</span></span>
<span data-ttu-id="a7447-140">You can disable data collection at any time, which automatically removes any Monitoring Agents previously installed by Security Center.</span><span class="sxs-lookup"><span data-stu-id="a7447-140">You can disable data collection at any time, which automatically removes any Monitoring Agents previously installed by Security Center.</span></span> <span data-ttu-id="a7447-141">You must select a subscription to turn off data collection.</span><span class="sxs-lookup"><span data-stu-id="a7447-141">You must select a subscription to turn off data collection.</span></span>

> [!NOTE]
> <span data-ttu-id="a7447-142">Security policies can be set at the Azure subscription level and resource group level but you must select a subscription to turn off data collection.</span><span class="sxs-lookup"><span data-stu-id="a7447-142">Security policies can be set at the Azure subscription level and resource group level but you must select a subscription to turn off data collection.</span></span>
>
>

1. <span data-ttu-id="a7447-143">Return to the **Security Center** blade and select the **Policy** tile.</span><span class="sxs-lookup"><span data-stu-id="a7447-143">Return to the **Security Center** blade and select the **Policy** tile.</span></span> <span data-ttu-id="a7447-144">This opens the **Security policy-Define policy per subscription or resource group** blade.</span><span class="sxs-lookup"><span data-stu-id="a7447-144">This opens the **Security policy-Define policy per subscription or resource group** blade.</span></span>
   <span data-ttu-id="a7447-145">![Select the policy tile][5]</span><span class="sxs-lookup"><span data-stu-id="a7447-145">![Select the policy tile][5]</span></span>
2. <span data-ttu-id="a7447-146">On the **Security policy-Define policy per subscription or resource group** blade, select the subscription that you wish to disable data collection.</span><span class="sxs-lookup"><span data-stu-id="a7447-146">On the **Security policy-Define policy per subscription or resource group** blade, select the subscription that you wish to disable data collection.</span></span>
   <span data-ttu-id="a7447-147">![Select subscription to disable data collection][6]</span><span class="sxs-lookup"><span data-stu-id="a7447-147">![Select subscription to disable data collection][6]</span></span>
3. <span data-ttu-id="a7447-148">The **Security policy** blade for that subscription opens.</span><span class="sxs-lookup"><span data-stu-id="a7447-148">The **Security policy** blade for that subscription opens.</span></span>  <span data-ttu-id="a7447-149">Select **Off** under Data collection.</span><span class="sxs-lookup"><span data-stu-id="a7447-149">Select **Off** under Data collection.</span></span>
4. <span data-ttu-id="a7447-150">Select **Save** in the top ribbon.</span><span class="sxs-lookup"><span data-stu-id="a7447-150">Select **Save** in the top ribbon.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a7447-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="a7447-151">Next steps</span></span>
<span data-ttu-id="a7447-152">This article showed you how to implement the Security Center recommendation "Enable data collection.”</span><span class="sxs-lookup"><span data-stu-id="a7447-152">This article showed you how to implement the Security Center recommendation "Enable data collection.”</span></span> <span data-ttu-id="a7447-153">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="a7447-153">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="a7447-154">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="a7447-154">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="a7447-155">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="a7447-155">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="a7447-156">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="a7447-156">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="a7447-157">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="a7447-157">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="a7447-158">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="a7447-158">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="a7447-159">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="a7447-159">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="a7447-160">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span><span class="sxs-lookup"><span data-stu-id="a7447-160">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-data-collection/security-center-blade.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-data-collection/recommendations.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-data-collection/data-collection.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-data-collection/storage-account.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-data-collection/policy.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-data-collection/disable-data-collection.png






