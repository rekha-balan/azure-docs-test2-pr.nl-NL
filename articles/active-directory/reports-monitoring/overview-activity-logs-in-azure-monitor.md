---
title: Azure Active Directory activity logs in Azure Monitor (preview) | Microsoft Docs
description: Overview of Azure Active Directory activity logs in Azure Monitor (preview)
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 07/13/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 357c19700e4388f31c0f07645ff1c3adf442c1aa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871017"
---
# <a name="azure-ad-activity-logs-in-azure-monitor-preview"></a><span data-ttu-id="a10f2-103">Azure AD activity logs in Azure Monitor (preview)</span><span class="sxs-lookup"><span data-stu-id="a10f2-103">Azure AD activity logs in Azure Monitor (preview)</span></span>

<span data-ttu-id="a10f2-104">You can now route Azure Active Directory (Azure AD) activity logs to your own storage account or event hub by using Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="a10f2-104">You can now route Azure Active Directory (Azure AD) activity logs to your own storage account or event hub by using Azure Monitor.</span></span> <span data-ttu-id="a10f2-105">With the public preview of Azure Active Directory logs in Azure Monitor, you can:</span><span class="sxs-lookup"><span data-stu-id="a10f2-105">With the public preview of Azure Active Directory logs in Azure Monitor, you can:</span></span>

* <span data-ttu-id="a10f2-106">Archive your audit logs for an Azure storage account, which enables you to retain the data for a long time.</span><span class="sxs-lookup"><span data-stu-id="a10f2-106">Archive your audit logs for an Azure storage account, which enables you to retain the data for a long time.</span></span>
* <span data-ttu-id="a10f2-107">Stream your audit logs to an Azure event hub for analytics by using popular Security Information and Event Management (SIEM) tools, such as Splunk and QRadar.</span><span class="sxs-lookup"><span data-stu-id="a10f2-107">Stream your audit logs to an Azure event hub for analytics by using popular Security Information and Event Management (SIEM) tools, such as Splunk and QRadar.</span></span>
* <span data-ttu-id="a10f2-108">Integrate your audit logs with your own custom log solutions by streaming them to an event hub.</span><span class="sxs-lookup"><span data-stu-id="a10f2-108">Integrate your audit logs with your own custom log solutions by streaming them to an event hub.</span></span>

> [!VIDEO https://www.youtube.com/embed/syT-9KNfug8]

## <a name="supported-reports"></a><span data-ttu-id="a10f2-109">Supported reports</span><span class="sxs-lookup"><span data-stu-id="a10f2-109">Supported reports</span></span>

<span data-ttu-id="a10f2-110">You can route audit activity logs and sign-in activity logs to your Azure storage account, event hub, or custom solution by using this feature.</span><span class="sxs-lookup"><span data-stu-id="a10f2-110">You can route audit activity logs and sign-in activity logs to your Azure storage account, event hub, or custom solution by using this feature.</span></span> 

* <span data-ttu-id="a10f2-111">**Audit logs**: The [audit logs activity report](concept-audit-logs.md) gives you access to the history of every task that's performed in your tenant.</span><span class="sxs-lookup"><span data-stu-id="a10f2-111">**Audit logs**: The [audit logs activity report](concept-audit-logs.md) gives you access to the history of every task that's performed in your tenant.</span></span>
* <span data-ttu-id="a10f2-112">**Sign-in logs**: With the [sign-in activity report](concept-sign-ins.md), you can determine who performed the tasks that are reported in the audit logs.</span><span class="sxs-lookup"><span data-stu-id="a10f2-112">**Sign-in logs**: With the [sign-in activity report](concept-sign-ins.md), you can determine who performed the tasks that are reported in the audit logs.</span></span>

> [!NOTE]
> <span data-ttu-id="a10f2-113">B2C-related audit and sign-in activity logs are not supported at this time.</span><span class="sxs-lookup"><span data-stu-id="a10f2-113">B2C-related audit and sign-in activity logs are not supported at this time.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="a10f2-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a10f2-114">Prerequisites</span></span>

<span data-ttu-id="a10f2-115">To use this feature, you need:</span><span class="sxs-lookup"><span data-stu-id="a10f2-115">To use this feature, you need:</span></span>

* <span data-ttu-id="a10f2-116">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a10f2-116">An Azure subscription.</span></span> <span data-ttu-id="a10f2-117">If you don't have an Azure subscription, you can [sign up for a free trial](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="a10f2-117">If you don't have an Azure subscription, you can [sign up for a free trial](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="a10f2-118">Azure AD Free, Basic, Premium 1, or Premium 2 [license](https://azure.microsoft.com/pricing/details/active-directory/), to access the Azure AD audit logs in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a10f2-118">Azure AD Free, Basic, Premium 1, or Premium 2 [license](https://azure.microsoft.com/pricing/details/active-directory/), to access the Azure AD audit logs in the Azure portal.</span></span> 
* <span data-ttu-id="a10f2-119">Azure AD Premium 1, or Premium 2 [license](https://azure.microsoft.com/pricing/details/active-directory/), to access the Azure AD sign-in logs in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a10f2-119">Azure AD Premium 1, or Premium 2 [license](https://azure.microsoft.com/pricing/details/active-directory/), to access the Azure AD sign-in logs in the Azure portal.</span></span> 

<span data-ttu-id="a10f2-120">Depending on where you want to route the audit log data, you need either of the following:</span><span class="sxs-lookup"><span data-stu-id="a10f2-120">Depending on where you want to route the audit log data, you need either of the following:</span></span>

* <span data-ttu-id="a10f2-121">An Azure storage account that you have *ListKeys* permissions for.</span><span class="sxs-lookup"><span data-stu-id="a10f2-121">An Azure storage account that you have *ListKeys* permissions for.</span></span> <span data-ttu-id="a10f2-122">We recommend that you use a general storage account and not a Blob storage account.</span><span class="sxs-lookup"><span data-stu-id="a10f2-122">We recommend that you use a general storage account and not a Blob storage account.</span></span> <span data-ttu-id="a10f2-123">For storage pricing information, see the [Azure Storage pricing calculator](https://azure.microsoft.com/pricing/calculator/?service=storage).</span><span class="sxs-lookup"><span data-stu-id="a10f2-123">For storage pricing information, see the [Azure Storage pricing calculator](https://azure.microsoft.com/pricing/calculator/?service=storage).</span></span> 
* <span data-ttu-id="a10f2-124">An Azure Event Hubs namespace to integrate with third-party solutions.</span><span class="sxs-lookup"><span data-stu-id="a10f2-124">An Azure Event Hubs namespace to integrate with third-party solutions.</span></span>

> [!NOTE]
> <span data-ttu-id="a10f2-125">To access the Azure AD activity logs, you need to be a *global administrator* or *security administrator* in the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="a10f2-125">To access the Azure AD activity logs, you need to be a *global administrator* or *security administrator* in the Azure AD tenant.</span></span>
>

## <a name="cost-considerations"></a><span data-ttu-id="a10f2-126">Cost considerations</span><span class="sxs-lookup"><span data-stu-id="a10f2-126">Cost considerations</span></span>

<span data-ttu-id="a10f2-127">If you already have an Azure AD license, you need an Azure subscription to set up the storage account and event hub.</span><span class="sxs-lookup"><span data-stu-id="a10f2-127">If you already have an Azure AD license, you need an Azure subscription to set up the storage account and event hub.</span></span> <span data-ttu-id="a10f2-128">The Azure subscription comes at no cost, but you have to pay to utilize Azure resources, including the storage account that you use for archival and the event hub that you use for streaming.</span><span class="sxs-lookup"><span data-stu-id="a10f2-128">The Azure subscription comes at no cost, but you have to pay to utilize Azure resources, including the storage account that you use for archival and the event hub that you use for streaming.</span></span> <span data-ttu-id="a10f2-129">The amount of data and, thus, the cost incurred, can vary significantly depending on the tenant size.</span><span class="sxs-lookup"><span data-stu-id="a10f2-129">The amount of data and, thus, the cost incurred, can vary significantly depending on the tenant size.</span></span> 

### <a name="storage-size-for-activity-logs"></a><span data-ttu-id="a10f2-130">Storage size for activity logs</span><span class="sxs-lookup"><span data-stu-id="a10f2-130">Storage size for activity logs</span></span>

<span data-ttu-id="a10f2-131">Every audit log event uses about 2 KB of data storage.</span><span class="sxs-lookup"><span data-stu-id="a10f2-131">Every audit log event uses about 2 KB of data storage.</span></span> <span data-ttu-id="a10f2-132">For a tenant with 100,000 users, which would incur about 1.5 million events per day, you would need about 3 GB of data storage per day.</span><span class="sxs-lookup"><span data-stu-id="a10f2-132">For a tenant with 100,000 users, which would incur about 1.5 million events per day, you would need about 3 GB of data storage per day.</span></span> <span data-ttu-id="a10f2-133">Because writes occur in approximately five-minute batches, you can anticipate approximately 9,000 write operations per month.</span><span class="sxs-lookup"><span data-stu-id="a10f2-133">Because writes occur in approximately five-minute batches, you can anticipate approximately 9,000 write operations per month.</span></span> 

<span data-ttu-id="a10f2-134">The following table contains a cost estimate of, depending on the size of the tenant, a general-purpose v2 storage account in West US for at least one year of retention.</span><span class="sxs-lookup"><span data-stu-id="a10f2-134">The following table contains a cost estimate of, depending on the size of the tenant, a general-purpose v2 storage account in West US for at least one year of retention.</span></span> <span data-ttu-id="a10f2-135">To create a more accurate estimate for the data volume that you anticipate for your application, use the [Azure storage pricing calculator](https://azure.microsoft.com/pricing/details/storage/blobs/).</span><span class="sxs-lookup"><span data-stu-id="a10f2-135">To create a more accurate estimate for the data volume that you anticipate for your application, use the [Azure storage pricing calculator](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span> 

| <span data-ttu-id="a10f2-136">Log category</span><span class="sxs-lookup"><span data-stu-id="a10f2-136">Log category</span></span> | <span data-ttu-id="a10f2-137">Number of users</span><span class="sxs-lookup"><span data-stu-id="a10f2-137">Number of users</span></span> | <span data-ttu-id="a10f2-138">Events per day</span><span class="sxs-lookup"><span data-stu-id="a10f2-138">Events per day</span></span> | <span data-ttu-id="a10f2-139">Volume of data per month (est.)</span><span class="sxs-lookup"><span data-stu-id="a10f2-139">Volume of data per month (est.)</span></span> | <span data-ttu-id="a10f2-140">Cost per month (est.)</span><span class="sxs-lookup"><span data-stu-id="a10f2-140">Cost per month (est.)</span></span> | <span data-ttu-id="a10f2-141">Cost per year (est.)</span><span class="sxs-lookup"><span data-stu-id="a10f2-141">Cost per year (est.)</span></span> |
|--------------|-----------------|----------------------|--------------------------------------|----------------------------|---------------------------|
| <span data-ttu-id="a10f2-142">Audit</span><span class="sxs-lookup"><span data-stu-id="a10f2-142">Audit</span></span> | <span data-ttu-id="a10f2-143">100,000</span><span class="sxs-lookup"><span data-stu-id="a10f2-143">100,000</span></span> | <span data-ttu-id="a10f2-144">1.5&nbsp;million</span><span class="sxs-lookup"><span data-stu-id="a10f2-144">1.5&nbsp;million</span></span> | <span data-ttu-id="a10f2-145">90 GB</span><span class="sxs-lookup"><span data-stu-id="a10f2-145">90 GB</span></span> | <span data-ttu-id="a10f2-146">$1.93</span><span class="sxs-lookup"><span data-stu-id="a10f2-146">$1.93</span></span> | <span data-ttu-id="a10f2-147">$23.12</span><span class="sxs-lookup"><span data-stu-id="a10f2-147">$23.12</span></span> |
| <span data-ttu-id="a10f2-148">Audit</span><span class="sxs-lookup"><span data-stu-id="a10f2-148">Audit</span></span> | <span data-ttu-id="a10f2-149">1,000</span><span class="sxs-lookup"><span data-stu-id="a10f2-149">1,000</span></span> | <span data-ttu-id="a10f2-150">15,000</span><span class="sxs-lookup"><span data-stu-id="a10f2-150">15,000</span></span> | <span data-ttu-id="a10f2-151">900 MB</span><span class="sxs-lookup"><span data-stu-id="a10f2-151">900 MB</span></span> | <span data-ttu-id="a10f2-152">$0.02</span><span class="sxs-lookup"><span data-stu-id="a10f2-152">$0.02</span></span> | <span data-ttu-id="a10f2-153">$0.24</span><span class="sxs-lookup"><span data-stu-id="a10f2-153">$0.24</span></span> |
| <span data-ttu-id="a10f2-154">Sign-ins</span><span class="sxs-lookup"><span data-stu-id="a10f2-154">Sign-ins</span></span> | <span data-ttu-id="a10f2-155">1,000</span><span class="sxs-lookup"><span data-stu-id="a10f2-155">1,000</span></span> | <span data-ttu-id="a10f2-156">34,800</span><span class="sxs-lookup"><span data-stu-id="a10f2-156">34,800</span></span> | <span data-ttu-id="a10f2-157">4 GB</span><span class="sxs-lookup"><span data-stu-id="a10f2-157">4 GB</span></span> | <span data-ttu-id="a10f2-158">$0.13</span><span class="sxs-lookup"><span data-stu-id="a10f2-158">$0.13</span></span> | <span data-ttu-id="a10f2-159">$1.56</span><span class="sxs-lookup"><span data-stu-id="a10f2-159">$1.56</span></span> |
| <span data-ttu-id="a10f2-160">Sign-ins</span><span class="sxs-lookup"><span data-stu-id="a10f2-160">Sign-ins</span></span> | <span data-ttu-id="a10f2-161">100,000</span><span class="sxs-lookup"><span data-stu-id="a10f2-161">100,000</span></span> | <span data-ttu-id="a10f2-162">15&nbsp;million</span><span class="sxs-lookup"><span data-stu-id="a10f2-162">15&nbsp;million</span></span> | <span data-ttu-id="a10f2-163">1.7 TB</span><span class="sxs-lookup"><span data-stu-id="a10f2-163">1.7 TB</span></span> | <span data-ttu-id="a10f2-164">$35.41</span><span class="sxs-lookup"><span data-stu-id="a10f2-164">$35.41</span></span> | <span data-ttu-id="a10f2-165">$424.92</span><span class="sxs-lookup"><span data-stu-id="a10f2-165">$424.92</span></span> | 


### <a name="event-hub-messages-for-activity-logs"></a><span data-ttu-id="a10f2-166">Event hub messages for activity logs</span><span class="sxs-lookup"><span data-stu-id="a10f2-166">Event hub messages for activity logs</span></span>

<span data-ttu-id="a10f2-167">Events are batched into approximately five-minute intervals and sent as a single message that contains all the events within that timeframe.</span><span class="sxs-lookup"><span data-stu-id="a10f2-167">Events are batched into approximately five-minute intervals and sent as a single message that contains all the events within that timeframe.</span></span> <span data-ttu-id="a10f2-168">A message in the event hub has a maximum size of 256 KB, and if the total size of all the messages within the timeframe exceeds that volume, multiple messages are sent.</span><span class="sxs-lookup"><span data-stu-id="a10f2-168">A message in the event hub has a maximum size of 256 KB, and if the total size of all the messages within the timeframe exceeds that volume, multiple messages are sent.</span></span> 

<span data-ttu-id="a10f2-169">For example, about 18 events per second ordinarily occur for a large tenant of more than 100,000 users, a rate that equates to 5,400 events every five minutes.</span><span class="sxs-lookup"><span data-stu-id="a10f2-169">For example, about 18 events per second ordinarily occur for a large tenant of more than 100,000 users, a rate that equates to 5,400 events every five minutes.</span></span> <span data-ttu-id="a10f2-170">Because audit logs are about 2 KB per event, this equates to 10.8 MB of data.</span><span class="sxs-lookup"><span data-stu-id="a10f2-170">Because audit logs are about 2 KB per event, this equates to 10.8 MB of data.</span></span> <span data-ttu-id="a10f2-171">Therefore, 43 messages are sent to the event hub in that five-minute interval.</span><span class="sxs-lookup"><span data-stu-id="a10f2-171">Therefore, 43 messages are sent to the event hub in that five-minute interval.</span></span> 

<span data-ttu-id="a10f2-172">The following table contains estimated costs per month for a basic event hub in West US, depending on the volume of event data.</span><span class="sxs-lookup"><span data-stu-id="a10f2-172">The following table contains estimated costs per month for a basic event hub in West US, depending on the volume of event data.</span></span> <span data-ttu-id="a10f2-173">To calculate an accurate estimate of the data volume that you anticipate for your application, use the [Event Hubs pricing calculator](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="a10f2-173">To calculate an accurate estimate of the data volume that you anticipate for your application, use the [Event Hubs pricing calculator](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

| <span data-ttu-id="a10f2-174">Log category</span><span class="sxs-lookup"><span data-stu-id="a10f2-174">Log category</span></span> | <span data-ttu-id="a10f2-175">Number of users</span><span class="sxs-lookup"><span data-stu-id="a10f2-175">Number of users</span></span> | <span data-ttu-id="a10f2-176">Events per second</span><span class="sxs-lookup"><span data-stu-id="a10f2-176">Events per second</span></span> | <span data-ttu-id="a10f2-177">Events per five-minute interval</span><span class="sxs-lookup"><span data-stu-id="a10f2-177">Events per five-minute interval</span></span> | <span data-ttu-id="a10f2-178">Volume per interval</span><span class="sxs-lookup"><span data-stu-id="a10f2-178">Volume per interval</span></span> | <span data-ttu-id="a10f2-179">Messages per interval</span><span class="sxs-lookup"><span data-stu-id="a10f2-179">Messages per interval</span></span> | <span data-ttu-id="a10f2-180">Messages per month</span><span class="sxs-lookup"><span data-stu-id="a10f2-180">Messages per month</span></span> | <span data-ttu-id="a10f2-181">Cost per month (est.)</span><span class="sxs-lookup"><span data-stu-id="a10f2-181">Cost per month (est.)</span></span> |
|--------------|-----------------|-------------------------|----------------------------------------|---------------------|---------------------------------|------------------------------|----------------------------|
| <span data-ttu-id="a10f2-182">Audit</span><span class="sxs-lookup"><span data-stu-id="a10f2-182">Audit</span></span> | <span data-ttu-id="a10f2-183">100,000</span><span class="sxs-lookup"><span data-stu-id="a10f2-183">100,000</span></span> | <span data-ttu-id="a10f2-184">18</span><span class="sxs-lookup"><span data-stu-id="a10f2-184">18</span></span> | <span data-ttu-id="a10f2-185">5,400</span><span class="sxs-lookup"><span data-stu-id="a10f2-185">5,400</span></span> | <span data-ttu-id="a10f2-186">10.8 MB</span><span class="sxs-lookup"><span data-stu-id="a10f2-186">10.8 MB</span></span> | <span data-ttu-id="a10f2-187">43</span><span class="sxs-lookup"><span data-stu-id="a10f2-187">43</span></span> | <span data-ttu-id="a10f2-188">371,520</span><span class="sxs-lookup"><span data-stu-id="a10f2-188">371,520</span></span> | <span data-ttu-id="a10f2-189">$10.83</span><span class="sxs-lookup"><span data-stu-id="a10f2-189">$10.83</span></span> |
| <span data-ttu-id="a10f2-190">Audit</span><span class="sxs-lookup"><span data-stu-id="a10f2-190">Audit</span></span> | <span data-ttu-id="a10f2-191">1,000</span><span class="sxs-lookup"><span data-stu-id="a10f2-191">1,000</span></span> | <span data-ttu-id="a10f2-192">0.1</span><span class="sxs-lookup"><span data-stu-id="a10f2-192">0.1</span></span> | <span data-ttu-id="a10f2-193">52</span><span class="sxs-lookup"><span data-stu-id="a10f2-193">52</span></span> | <span data-ttu-id="a10f2-194">104 KB</span><span class="sxs-lookup"><span data-stu-id="a10f2-194">104 KB</span></span> | <span data-ttu-id="a10f2-195">1</span><span class="sxs-lookup"><span data-stu-id="a10f2-195">1</span></span> | <span data-ttu-id="a10f2-196">8,640</span><span class="sxs-lookup"><span data-stu-id="a10f2-196">8,640</span></span> | <span data-ttu-id="a10f2-197">$10.80</span><span class="sxs-lookup"><span data-stu-id="a10f2-197">$10.80</span></span> |
| <span data-ttu-id="a10f2-198">Sign-ins</span><span class="sxs-lookup"><span data-stu-id="a10f2-198">Sign-ins</span></span> | <span data-ttu-id="a10f2-199">1,000</span><span class="sxs-lookup"><span data-stu-id="a10f2-199">1,000</span></span> | <span data-ttu-id="a10f2-200">178</span><span class="sxs-lookup"><span data-stu-id="a10f2-200">178</span></span> | <span data-ttu-id="a10f2-201">53,400</span><span class="sxs-lookup"><span data-stu-id="a10f2-201">53,400</span></span> | <span data-ttu-id="a10f2-202">106.8&nbsp;MB</span><span class="sxs-lookup"><span data-stu-id="a10f2-202">106.8&nbsp;MB</span></span> | <span data-ttu-id="a10f2-203">418</span><span class="sxs-lookup"><span data-stu-id="a10f2-203">418</span></span> | <span data-ttu-id="a10f2-204">3,611,520</span><span class="sxs-lookup"><span data-stu-id="a10f2-204">3,611,520</span></span> | <span data-ttu-id="a10f2-205">$11.06</span><span class="sxs-lookup"><span data-stu-id="a10f2-205">$11.06</span></span> |  


## <a name="frequently-asked-questions"></a><span data-ttu-id="a10f2-206">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="a10f2-206">Frequently asked questions</span></span>

<span data-ttu-id="a10f2-207">This section answers frequently asked questions and discusses known issues with Azure AD logs in Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="a10f2-207">This section answers frequently asked questions and discusses known issues with Azure AD logs in Azure Monitor.</span></span>

<span data-ttu-id="a10f2-208">**Q: Where should I start?**</span><span class="sxs-lookup"><span data-stu-id="a10f2-208">**Q: Where should I start?**</span></span> 

<span data-ttu-id="a10f2-209">**A**: This article discusses what you need to deploy this feature.</span><span class="sxs-lookup"><span data-stu-id="a10f2-209">**A**: This article discusses what you need to deploy this feature.</span></span> <span data-ttu-id="a10f2-210">After you've satisfied the prerequisites, go to the tutorials that can help you configure and route your logs to an event hub.</span><span class="sxs-lookup"><span data-stu-id="a10f2-210">After you've satisfied the prerequisites, go to the tutorials that can help you configure and route your logs to an event hub.</span></span>

---

<span data-ttu-id="a10f2-211">**Q: Which logs are included?**</span><span class="sxs-lookup"><span data-stu-id="a10f2-211">**Q: Which logs are included?**</span></span>

<span data-ttu-id="a10f2-212">**A**: The sign-in activity logs and audit logs are both available for routing through this feature, although B2C-related audit events are currently not included.</span><span class="sxs-lookup"><span data-stu-id="a10f2-212">**A**: The sign-in activity logs and audit logs are both available for routing through this feature, although B2C-related audit events are currently not included.</span></span> <span data-ttu-id="a10f2-213">To find out which types of logs and which feature-based logs are currently supported, see [Audit log schema](reference-azure-monitor-audit-log-schema.md) and [Sign-in log schema](reference-azure-monitor-sign-ins-log-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a10f2-213">To find out which types of logs and which feature-based logs are currently supported, see [Audit log schema](reference-azure-monitor-audit-log-schema.md) and [Sign-in log schema](reference-azure-monitor-sign-ins-log-schema.md).</span></span> 

---

<span data-ttu-id="a10f2-214">**Q: How soon after an action do the corresponding logs show up in event hubs?**</span><span class="sxs-lookup"><span data-stu-id="a10f2-214">**Q: How soon after an action do the corresponding logs show up in event hubs?**</span></span>

<span data-ttu-id="a10f2-215">**A**: The logs should show up in your event hub within two to five minutes after the action is performed.</span><span class="sxs-lookup"><span data-stu-id="a10f2-215">**A**: The logs should show up in your event hub within two to five minutes after the action is performed.</span></span> <span data-ttu-id="a10f2-216">For more information about Event Hubs, see [What is Azure Event Hubs?](../../event-hubs/event-hubs-about.md).</span><span class="sxs-lookup"><span data-stu-id="a10f2-216">For more information about Event Hubs, see [What is Azure Event Hubs?](../../event-hubs/event-hubs-about.md).</span></span>

---

<span data-ttu-id="a10f2-217">**Q: How soon after an action do the corresponding logs show up in storage accounts?**</span><span class="sxs-lookup"><span data-stu-id="a10f2-217">**Q: How soon after an action do the corresponding logs show up in storage accounts?**</span></span>

<span data-ttu-id="a10f2-218">**A**: For Azure storage accounts, the latency is anywhere from 5 to 15 minutes after the action is performed.</span><span class="sxs-lookup"><span data-stu-id="a10f2-218">**A**: For Azure storage accounts, the latency is anywhere from 5 to 15 minutes after the action is performed.</span></span>

---

<span data-ttu-id="a10f2-219">**Q: How much will it cost to store my data?**</span><span class="sxs-lookup"><span data-stu-id="a10f2-219">**Q: How much will it cost to store my data?**</span></span>

<span data-ttu-id="a10f2-220">**A**: The storage costs depend on both the size of your logs and the retention period you choose.</span><span class="sxs-lookup"><span data-stu-id="a10f2-220">**A**: The storage costs depend on both the size of your logs and the retention period you choose.</span></span> <span data-ttu-id="a10f2-221">For a list of the estimated costs for tenants, which depend on the volume of logs generated, see the [Storage size for activity logs](#storage-size-for-activity-logs) section.</span><span class="sxs-lookup"><span data-stu-id="a10f2-221">For a list of the estimated costs for tenants, which depend on the volume of logs generated, see the [Storage size for activity logs](#storage-size-for-activity-logs) section.</span></span>

---

<span data-ttu-id="a10f2-222">**Q: How much will it cost to stream my data to an event hub?**</span><span class="sxs-lookup"><span data-stu-id="a10f2-222">**Q: How much will it cost to stream my data to an event hub?**</span></span>

<span data-ttu-id="a10f2-223">**A**: The streaming costs depend on the number of messages you receive per minute.</span><span class="sxs-lookup"><span data-stu-id="a10f2-223">**A**: The streaming costs depend on the number of messages you receive per minute.</span></span> <span data-ttu-id="a10f2-224">This article discusses how the costs are calculated and lists cost estimates, which are based on the number of messages.</span><span class="sxs-lookup"><span data-stu-id="a10f2-224">This article discusses how the costs are calculated and lists cost estimates, which are based on the number of messages.</span></span> 

---

<span data-ttu-id="a10f2-225">**Q: How do I integrate Azure AD activity logs with my SIEM system?**</span><span class="sxs-lookup"><span data-stu-id="a10f2-225">**Q: How do I integrate Azure AD activity logs with my SIEM system?**</span></span>

<span data-ttu-id="a10f2-226">**A**: You can do this in two ways:</span><span class="sxs-lookup"><span data-stu-id="a10f2-226">**A**: You can do this in two ways:</span></span>

- <span data-ttu-id="a10f2-227">Use Azure Monitor with Event Hubs to stream logs to your SIEM system.</span><span class="sxs-lookup"><span data-stu-id="a10f2-227">Use Azure Monitor with Event Hubs to stream logs to your SIEM system.</span></span> <span data-ttu-id="a10f2-228">First, [stream the logs to an event hub](quickstart-azure-monitor-stream-logs-to-event-hub.md) and then [set up your SIEM tool](quickstart-azure-monitor-stream-logs-to-event-hub.md#access-data-from-your-event-hub) with the configured event hub.</span><span class="sxs-lookup"><span data-stu-id="a10f2-228">First, [stream the logs to an event hub](quickstart-azure-monitor-stream-logs-to-event-hub.md) and then [set up your SIEM tool](quickstart-azure-monitor-stream-logs-to-event-hub.md#access-data-from-your-event-hub) with the configured event hub.</span></span> 

- <span data-ttu-id="a10f2-229">Use the [Reporting Graph API](concept-reporting-api.md) to access the data, and push it into the SIEM system using your own scripts.</span><span class="sxs-lookup"><span data-stu-id="a10f2-229">Use the [Reporting Graph API](concept-reporting-api.md) to access the data, and push it into the SIEM system using your own scripts.</span></span>

---

<span data-ttu-id="a10f2-230">**Q: What SIEM tools are currently supported?**</span><span class="sxs-lookup"><span data-stu-id="a10f2-230">**Q: What SIEM tools are currently supported?**</span></span> 

<span data-ttu-id="a10f2-231">**A**: Currently, Azure Monitor is supported by [Splunk](tutorial-integrate-activity-logs-with-splunk.md), QRadar, and [Sumo Logic](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory).</span><span class="sxs-lookup"><span data-stu-id="a10f2-231">**A**: Currently, Azure Monitor is supported by [Splunk](tutorial-integrate-activity-logs-with-splunk.md), QRadar, and [Sumo Logic](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory).</span></span> <span data-ttu-id="a10f2-232">For more information about how the connectors work, see [Stream Azure monitoring data to an event hub for consumption by an external tool](../../monitoring-and-diagnostics/monitor-stream-monitoring-data-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="a10f2-232">For more information about how the connectors work, see [Stream Azure monitoring data to an event hub for consumption by an external tool](../../monitoring-and-diagnostics/monitor-stream-monitoring-data-event-hubs.md).</span></span>

---

<span data-ttu-id="a10f2-233">**Q: How do I integrate Azure AD activity logs with my Splunk instance?**</span><span class="sxs-lookup"><span data-stu-id="a10f2-233">**Q: How do I integrate Azure AD activity logs with my Splunk instance?**</span></span>

<span data-ttu-id="a10f2-234">**A**: First, [route the Azure AD activity logs to an event hub](quickstart-azure-monitor-stream-logs-to-event-hub.md), then follow the steps to [Integrate activity logs with Splunk](tutorial-integrate-activity-logs-with-splunk.md).</span><span class="sxs-lookup"><span data-stu-id="a10f2-234">**A**: First, [route the Azure AD activity logs to an event hub](quickstart-azure-monitor-stream-logs-to-event-hub.md), then follow the steps to [Integrate activity logs with Splunk](tutorial-integrate-activity-logs-with-splunk.md).</span></span>

---

<span data-ttu-id="a10f2-235">**Q: How do I integrate Azure AD activity logs with Sumo Logic?**</span><span class="sxs-lookup"><span data-stu-id="a10f2-235">**Q: How do I integrate Azure AD activity logs with Sumo Logic?**</span></span> 

<span data-ttu-id="a10f2-236">**A**: First, [route the Azure AD activity logs to an event hub](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory/Collect_Logs_for_Azure_Active_Directory), then follow the steps to [Install the Azure AD application and view the dashboards in SumoLogic](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory/Install_the_Azure_Active_Directory_App_and_View_the_Dashboards).</span><span class="sxs-lookup"><span data-stu-id="a10f2-236">**A**: First, [route the Azure AD activity logs to an event hub](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory/Collect_Logs_for_Azure_Active_Directory), then follow the steps to [Install the Azure AD application and view the dashboards in SumoLogic](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory/Install_the_Azure_Active_Directory_App_and_View_the_Dashboards).</span></span>

---

<span data-ttu-id="a10f2-237">**Q: Can I access the data from an event hub without using an external SIEM tool?**</span><span class="sxs-lookup"><span data-stu-id="a10f2-237">**Q: Can I access the data from an event hub without using an external SIEM tool?**</span></span> 

<span data-ttu-id="a10f2-238">**A**: Yes.</span><span class="sxs-lookup"><span data-stu-id="a10f2-238">**A**: Yes.</span></span> <span data-ttu-id="a10f2-239">To access the logs from your custom application, you can use the [Event Hubs API](../../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md).</span><span class="sxs-lookup"><span data-stu-id="a10f2-239">To access the logs from your custom application, you can use the [Event Hubs API](../../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md).</span></span> 

---


## <a name="next-steps"></a><span data-ttu-id="a10f2-240">Next steps</span><span class="sxs-lookup"><span data-stu-id="a10f2-240">Next steps</span></span>

* [<span data-ttu-id="a10f2-241">Archive activity logs to a storage account</span><span class="sxs-lookup"><span data-stu-id="a10f2-241">Archive activity logs to a storage account</span></span>](quickstart-azure-monitor-route-logs-to-storage-account.md)
* [<span data-ttu-id="a10f2-242">Route activity logs to an event hub</span><span class="sxs-lookup"><span data-stu-id="a10f2-242">Route activity logs to an event hub</span></span>](quickstart-azure-monitor-stream-logs-to-event-hub.md)
* [<span data-ttu-id="a10f2-243">Read more about Azure Diagnostic Logs</span><span class="sxs-lookup"><span data-stu-id="a10f2-243">Read more about Azure Diagnostic Logs</span></span>](../../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)
