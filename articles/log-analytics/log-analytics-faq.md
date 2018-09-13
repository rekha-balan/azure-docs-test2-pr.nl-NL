---
title: Log Analytics FAQ | Microsoft Docs
description: Answers to frequently asked questions about the Azure Log Analytics service.
services: log-analytics
documentationcenter: ''
author: bandersmsft
manager: carmonm
editor: ''
ms.assetid: ad536ff7-2c60-4850-a46d-230bc9e1ab45
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: 8bbc1abfc21a68874d28ae947139bdfce9db2497
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551993"
---
# <a name="log-analytics-faq"></a><span data-ttu-id="fb04c-103">Log Analytics FAQ</span><span class="sxs-lookup"><span data-stu-id="fb04c-103">Log Analytics FAQ</span></span>
<span data-ttu-id="fb04c-104">This Microsoft FAQ is a list of commonly asked questions about Log Analytics in Microsoft Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="fb04c-104">This Microsoft FAQ is a list of commonly asked questions about Log Analytics in Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="fb04c-105">If you have any additional questions about Log Analytics, please go to the [discussion forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) and post your questions.</span><span class="sxs-lookup"><span data-stu-id="fb04c-105">If you have any additional questions about Log Analytics, please go to the [discussion forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) and post your questions.</span></span> <span data-ttu-id="fb04c-106">Someone from our community will help you get your answers.</span><span class="sxs-lookup"><span data-stu-id="fb04c-106">Someone from our community will help you get your answers.</span></span> <span data-ttu-id="fb04c-107">If a question is commonly asked, we will add it to this article so that it can be found quickly and easily.</span><span class="sxs-lookup"><span data-stu-id="fb04c-107">If a question is commonly asked, we will add it to this article so that it can be found quickly and easily.</span></span>

## <a name="general"></a><span data-ttu-id="fb04c-108">General</span><span class="sxs-lookup"><span data-stu-id="fb04c-108">General</span></span>
<span data-ttu-id="fb04c-109">**Q. What checks are performed by the AD and SQL Assessment solutions?**</span><span class="sxs-lookup"><span data-stu-id="fb04c-109">**Q. What checks are performed by the AD and SQL Assessment solutions?**</span></span>

<span data-ttu-id="fb04c-110">A.</span><span class="sxs-lookup"><span data-stu-id="fb04c-110">A.</span></span> <span data-ttu-id="fb04c-111">The following query shows a description of all checks currently performed:</span><span class="sxs-lookup"><span data-stu-id="fb04c-111">The following query shows a description of all checks currently performed:</span></span>

```
(Type=SQLAssessmentRecommendation OR Type=ADAssessmentRecommendation) | dedup RecommendationId | select FocusArea, ActionArea, Recommendation, Description | sort Type, FocusArea,ActionArea, Recommendation
```

<span data-ttu-id="fb04c-112">The results can then be exported to Excel for further review.</span><span class="sxs-lookup"><span data-stu-id="fb04c-112">The results can then be exported to Excel for further review.</span></span>

<span data-ttu-id="fb04c-113">**Q: Why do I see something different than *OMS* in SCOM Administration?**</span><span class="sxs-lookup"><span data-stu-id="fb04c-113">**Q: Why do I see something different than *OMS* in SCOM Administration?**</span></span>

<span data-ttu-id="fb04c-114">A: Depending on what Update Rollup of SCOM you are in, you may see a node for *System Center Advisor*, *Operational Insights*, or *Log Analytics*.</span><span class="sxs-lookup"><span data-stu-id="fb04c-114">A: Depending on what Update Rollup of SCOM you are in, you may see a node for *System Center Advisor*, *Operational Insights*, or *Log Analytics*.</span></span>

<span data-ttu-id="fb04c-115">The text string update to *OMS* is included in a management pack, which needs to be imported manually.</span><span class="sxs-lookup"><span data-stu-id="fb04c-115">The text string update to *OMS* is included in a management pack, which needs to be imported manually.</span></span> <span data-ttu-id="fb04c-116">Follow the instructions on the latest SCOM Update Rollup KB article and refresh the OMS console to see the latest updates in the *OMS* node.</span><span class="sxs-lookup"><span data-stu-id="fb04c-116">Follow the instructions on the latest SCOM Update Rollup KB article and refresh the OMS console to see the latest updates in the *OMS* node.</span></span>

<span data-ttu-id="fb04c-117">**Q: Is there an *on-premises* version of OMS?**</span><span class="sxs-lookup"><span data-stu-id="fb04c-117">**Q: Is there an *on-premises* version of OMS?**</span></span>

<span data-ttu-id="fb04c-118">A: No.</span><span class="sxs-lookup"><span data-stu-id="fb04c-118">A: No.</span></span> <span data-ttu-id="fb04c-119">Log Analytics processes and stores very large amounts of data.</span><span class="sxs-lookup"><span data-stu-id="fb04c-119">Log Analytics processes and stores very large amounts of data.</span></span> <span data-ttu-id="fb04c-120">As a cloud service, Log Analytics is able to scale-up if necessary and avoid any performance impact to your environment.</span><span class="sxs-lookup"><span data-stu-id="fb04c-120">As a cloud service, Log Analytics is able to scale-up if necessary and avoid any performance impact to your environment.</span></span>

<span data-ttu-id="fb04c-121">Also, being a cloud service means you don't need to keep the Log Analytics infrastructure up and running and can receive frequent feature updates and fixes.</span><span class="sxs-lookup"><span data-stu-id="fb04c-121">Also, being a cloud service means you don't need to keep the Log Analytics infrastructure up and running and can receive frequent feature updates and fixes.</span></span>

## <a name="configuration"></a><span data-ttu-id="fb04c-122">Configuration</span><span class="sxs-lookup"><span data-stu-id="fb04c-122">Configuration</span></span>
<span data-ttu-id="fb04c-123">**Q. Can I change the name of the table/blob container used to read from Azure Diagnostics (WAD)?**</span><span class="sxs-lookup"><span data-stu-id="fb04c-123">**Q. Can I change the name of the table/blob container used to read from Azure Diagnostics (WAD)?**</span></span>  

<span data-ttu-id="fb04c-124">A.</span><span class="sxs-lookup"><span data-stu-id="fb04c-124">A.</span></span>    <span data-ttu-id="fb04c-125">No, this is not currently possible, but is planned for a future release.</span><span class="sxs-lookup"><span data-stu-id="fb04c-125">No, this is not currently possible, but is planned for a future release.</span></span>

<span data-ttu-id="fb04c-126">**Q. What IP addresses do the OMS services use? How do I ensure that my firewall only allows traffic to the OMS Services?**</span><span class="sxs-lookup"><span data-stu-id="fb04c-126">**Q. What IP addresses do the OMS services use? How do I ensure that my firewall only allows traffic to the OMS Services?**</span></span>  

<span data-ttu-id="fb04c-127">A.</span><span class="sxs-lookup"><span data-stu-id="fb04c-127">A.</span></span> <span data-ttu-id="fb04c-128">The Log Analytics service is built on top of Azure and the endpoints receive IPs that are in the [Microsoft Azure Datacenter IP Ranges](http://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="fb04c-128">The Log Analytics service is built on top of Azure and the endpoints receive IPs that are in the [Microsoft Azure Datacenter IP Ranges](http://www.microsoft.com/download/details.aspx?id=41653).</span></span>

<span data-ttu-id="fb04c-129">As service deployments are made, the actual IP addresses of the OMS services change.</span><span class="sxs-lookup"><span data-stu-id="fb04c-129">As service deployments are made, the actual IP addresses of the OMS services change.</span></span> <span data-ttu-id="fb04c-130">The DNS names to allow through your firewall are documented at [Configure proxy and firewall settings in Log Analytics](log-analytics-proxy-firewall.md).</span><span class="sxs-lookup"><span data-stu-id="fb04c-130">The DNS names to allow through your firewall are documented at [Configure proxy and firewall settings in Log Analytics](log-analytics-proxy-firewall.md).</span></span>

<span data-ttu-id="fb04c-131">**Q. I use ExpressRoute for connecting to Azure. Will my Log Analytics traffic use my ExpressRoute connection?**</span><span class="sxs-lookup"><span data-stu-id="fb04c-131">**Q. I use ExpressRoute for connecting to Azure. Will my Log Analytics traffic use my ExpressRoute connection?**</span></span>  

<span data-ttu-id="fb04c-132">A.</span><span class="sxs-lookup"><span data-stu-id="fb04c-132">A.</span></span> <span data-ttu-id="fb04c-133">The different types of ExpressRoute traffic are described in the [ExpressRoute documentation](../expressroute/expressroute-faqs.md#supported-services).</span><span class="sxs-lookup"><span data-stu-id="fb04c-133">The different types of ExpressRoute traffic are described in the [ExpressRoute documentation](../expressroute/expressroute-faqs.md#supported-services).</span></span>

<span data-ttu-id="fb04c-134">Traffic to Log Analytics uses the public-peering ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="fb04c-134">Traffic to Log Analytics uses the public-peering ExpressRoute circuit.</span></span>

<span data-ttu-id="fb04c-135">**Q. Is there a simple and easy way to move an existing Log Analytics workspace to another Log Analytics workspace/Azure subscription?**</span><span class="sxs-lookup"><span data-stu-id="fb04c-135">**Q. Is there a simple and easy way to move an existing Log Analytics workspace to another Log Analytics workspace/Azure subscription?**</span></span>  <span data-ttu-id="fb04c-136">We have several customer's OMS workspaces that we were testing and trialing in our Azure subscription, and they are moving to production so we want to move them to their own Azure/OMS subscription.</span><span class="sxs-lookup"><span data-stu-id="fb04c-136">We have several customer's OMS workspaces that we were testing and trialing in our Azure subscription, and they are moving to production so we want to move them to their own Azure/OMS subscription.</span></span>  

<span data-ttu-id="fb04c-137">A.</span><span class="sxs-lookup"><span data-stu-id="fb04c-137">A.</span></span> <span data-ttu-id="fb04c-138">The `Move-AzureRmResource` cmdlet will let you move an Log Analytics workspace, and also an Automation account from one Azure subscription to another.</span><span class="sxs-lookup"><span data-stu-id="fb04c-138">The `Move-AzureRmResource` cmdlet will let you move an Log Analytics workspace, and also an Automation account from one Azure subscription to another.</span></span> <span data-ttu-id="fb04c-139">For more information, see [Move-AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx).</span><span class="sxs-lookup"><span data-stu-id="fb04c-139">For more information, see [Move-AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx).</span></span>

<span data-ttu-id="fb04c-140">This change can also be made in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fb04c-140">This change can also be made in the Azure portal.</span></span>

<span data-ttu-id="fb04c-141">You can’t move data from one Log Analytics workspace to another, or change the region that Log Analytics data is stored in.</span><span class="sxs-lookup"><span data-stu-id="fb04c-141">You can’t move data from one Log Analytics workspace to another, or change the region that Log Analytics data is stored in.</span></span>

<span data-ttu-id="fb04c-142">**Q: How do I add OMS to SCOM?**</span><span class="sxs-lookup"><span data-stu-id="fb04c-142">**Q: How do I add OMS to SCOM?**</span></span>

<span data-ttu-id="fb04c-143">A:  Updating to the latest update rollup and importing management packs will enable you to connect SCOM to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="fb04c-143">A:  Updating to the latest update rollup and importing management packs will enable you to connect SCOM to Log Analytics.</span></span>

<span data-ttu-id="fb04c-144">Note that the SCOM connection to Log Analytics is only available for SCOM 2012 SP1 and higher.</span><span class="sxs-lookup"><span data-stu-id="fb04c-144">Note that the SCOM connection to Log Analytics is only available for SCOM 2012 SP1 and higher.</span></span>

<span data-ttu-id="fb04c-145">**Q: How can I confirm that an agent is able to communicate with Log Analytics?**</span><span class="sxs-lookup"><span data-stu-id="fb04c-145">**Q: How can I confirm that an agent is able to communicate with Log Analytics?**</span></span>

<span data-ttu-id="fb04c-146">A: To ensure that the agent can communicate with OMS, go to: Control Panel, Security & Settings, **Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="fb04c-146">A: To ensure that the agent can communicate with OMS, go to: Control Panel, Security & Settings, **Microsoft Monitoring Agent**.</span></span>

<span data-ttu-id="fb04c-147">Under the **Azure Log Analytics (OMS)** tab, look for a green check mark.</span><span class="sxs-lookup"><span data-stu-id="fb04c-147">Under the **Azure Log Analytics (OMS)** tab, look for a green check mark.</span></span> <span data-ttu-id="fb04c-148">A green check mark icon confirms that the agent is able to communicate with the OMS service.</span><span class="sxs-lookup"><span data-stu-id="fb04c-148">A green check mark icon confirms that the agent is able to communicate with the OMS service.</span></span>

<span data-ttu-id="fb04c-149">A yellow warning icon means the agent is having issues communication with OMS.</span><span class="sxs-lookup"><span data-stu-id="fb04c-149">A yellow warning icon means the agent is having issues communication with OMS.</span></span> <span data-ttu-id="fb04c-150">One common reason is the Microsoft Monitoring Agent service has been stopped and needs to be restarted.</span><span class="sxs-lookup"><span data-stu-id="fb04c-150">One common reason is the Microsoft Monitoring Agent service has been stopped and needs to be restarted.</span></span>

<span data-ttu-id="fb04c-151">**Q: How do I stop an agent from communicating with Log Analytics?**</span><span class="sxs-lookup"><span data-stu-id="fb04c-151">**Q: How do I stop an agent from communicating with Log Analytics?**</span></span>

<span data-ttu-id="fb04c-152">A: In SCOM, remove the computer from the OMS managed list.</span><span class="sxs-lookup"><span data-stu-id="fb04c-152">A: In SCOM, remove the computer from the OMS managed list.</span></span> <span data-ttu-id="fb04c-153">This stops all communication through SCOM for that agent.</span><span class="sxs-lookup"><span data-stu-id="fb04c-153">This stops all communication through SCOM for that agent.</span></span> <span data-ttu-id="fb04c-154">For agents connected to OMS directly, you can stop them from communicating with OMS through: Control Panel, Security & Settings, **Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="fb04c-154">For agents connected to OMS directly, you can stop them from communicating with OMS through: Control Panel, Security & Settings, **Microsoft Monitoring Agent**.</span></span>
<span data-ttu-id="fb04c-155">Under **Azure Log Analytics (OMS)**, remove all workspaces listed.</span><span class="sxs-lookup"><span data-stu-id="fb04c-155">Under **Azure Log Analytics (OMS)**, remove all workspaces listed.</span></span>

<span data-ttu-id="fb04c-156">**Q: Why am I getting an error when I try to move my workspace from one Azure subscription to another?**</span><span class="sxs-lookup"><span data-stu-id="fb04c-156">**Q: Why am I getting an error when I try to move my workspace from one Azure subscription to another?**</span></span>

<span data-ttu-id="fb04c-157">A: When you add a solution, Azure creates a resource in the Azure subscription that the workspace is in.</span><span class="sxs-lookup"><span data-stu-id="fb04c-157">A: When you add a solution, Azure creates a resource in the Azure subscription that the workspace is in.</span></span>

<span data-ttu-id="fb04c-158">Typically, the person adding the subscription is either an administrator or contributor for the *Azure subscription*.</span><span class="sxs-lookup"><span data-stu-id="fb04c-158">Typically, the person adding the subscription is either an administrator or contributor for the *Azure subscription*.</span></span> <span data-ttu-id="fb04c-159">Administrator or Contributor in the OMS portal is not enough if the user doesn’t also have the same permissions in the Azure portal for the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="fb04c-159">Administrator or Contributor in the OMS portal is not enough if the user doesn’t also have the same permissions in the Azure portal for the Azure subscription.</span></span>


## <a name="agent-data"></a><span data-ttu-id="fb04c-160">Agent data</span><span class="sxs-lookup"><span data-stu-id="fb04c-160">Agent data</span></span>
<span data-ttu-id="fb04c-161">**Q. How much data can I send through the agent to Log Analytics? Is there a maximum amount of data per customer?**</span><span class="sxs-lookup"><span data-stu-id="fb04c-161">**Q. How much data can I send through the agent to Log Analytics? Is there a maximum amount of data per customer?**</span></span>  
<span data-ttu-id="fb04c-162">A.</span><span class="sxs-lookup"><span data-stu-id="fb04c-162">A.</span></span> <span data-ttu-id="fb04c-163">The free plan sets a daily cap of 500 MB per workspace.</span><span class="sxs-lookup"><span data-stu-id="fb04c-163">The free plan sets a daily cap of 500 MB per workspace.</span></span> <span data-ttu-id="fb04c-164">The standard and premium plans have no limit on the amount of data that is uploaded.</span><span class="sxs-lookup"><span data-stu-id="fb04c-164">The standard and premium plans have no limit on the amount of data that is uploaded.</span></span> <span data-ttu-id="fb04c-165">As a cloud service, Log Analytics in OMS designed to automatically scale up to handle the volume coming from a customer – even if it is terabytes per day.</span><span class="sxs-lookup"><span data-stu-id="fb04c-165">As a cloud service, Log Analytics in OMS designed to automatically scale up to handle the volume coming from a customer – even if it is terabytes per day.</span></span>

<span data-ttu-id="fb04c-166">The Log Analytics agent was designed to ensure it has a small footprint and does some basic data compression.</span><span class="sxs-lookup"><span data-stu-id="fb04c-166">The Log Analytics agent was designed to ensure it has a small footprint and does some basic data compression.</span></span> <span data-ttu-id="fb04c-167">One of our customers actually wrote a blog on the tests they performed against our agent and how impressed they were.</span><span class="sxs-lookup"><span data-stu-id="fb04c-167">One of our customers actually wrote a blog on the tests they performed against our agent and how impressed they were.</span></span> <span data-ttu-id="fb04c-168">The data volume will vary based on the solutions your customers enables.</span><span class="sxs-lookup"><span data-stu-id="fb04c-168">The data volume will vary based on the solutions your customers enables.</span></span> <span data-ttu-id="fb04c-169">You can find detailed information on the data volume and see the breakup by solution under the **Usage** tile in the OMS overview page.</span><span class="sxs-lookup"><span data-stu-id="fb04c-169">You can find detailed information on the data volume and see the breakup by solution under the **Usage** tile in the OMS overview page.</span></span>

<span data-ttu-id="fb04c-170">For more information, you can read a [customer blog](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) about the low footprint of the OMS agent.</span><span class="sxs-lookup"><span data-stu-id="fb04c-170">For more information, you can read a [customer blog](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) about the low footprint of the OMS agent.</span></span>

<span data-ttu-id="fb04c-171">**Q. How much network bandwidth is used by the Microsoft Management Agent (MMA) when sending data to Log Analytics?**</span><span class="sxs-lookup"><span data-stu-id="fb04c-171">**Q. How much network bandwidth is used by the Microsoft Management Agent (MMA) when sending data to Log Analytics?**</span></span>

<span data-ttu-id="fb04c-172">A.</span><span class="sxs-lookup"><span data-stu-id="fb04c-172">A.</span></span> <span data-ttu-id="fb04c-173">Bandwidth is a function on the amount of data sent.</span><span class="sxs-lookup"><span data-stu-id="fb04c-173">Bandwidth is a function on the amount of data sent.</span></span> <span data-ttu-id="fb04c-174">Data is compressed as it is sent over the network.</span><span class="sxs-lookup"><span data-stu-id="fb04c-174">Data is compressed as it is sent over the network.</span></span>

<span data-ttu-id="fb04c-175">**Q. How much data is sent per agent?**</span><span class="sxs-lookup"><span data-stu-id="fb04c-175">**Q. How much data is sent per agent?**</span></span>

<span data-ttu-id="fb04c-176">A.</span><span class="sxs-lookup"><span data-stu-id="fb04c-176">A.</span></span> <span data-ttu-id="fb04c-177">This largely depends on:</span><span class="sxs-lookup"><span data-stu-id="fb04c-177">This largely depends on:</span></span>

* <span data-ttu-id="fb04c-178">the solutions you have enabled</span><span class="sxs-lookup"><span data-stu-id="fb04c-178">the solutions you have enabled</span></span>
* <span data-ttu-id="fb04c-179">the number of logs and performance counters being collected</span><span class="sxs-lookup"><span data-stu-id="fb04c-179">the number of logs and performance counters being collected</span></span>
* <span data-ttu-id="fb04c-180">the volume of data in the logs</span><span class="sxs-lookup"><span data-stu-id="fb04c-180">the volume of data in the logs</span></span>

<span data-ttu-id="fb04c-181">The free pricing tier is a good way to onboard several servers and gauge the typical data volume.</span><span class="sxs-lookup"><span data-stu-id="fb04c-181">The free pricing tier is a good way to onboard several servers and gauge the typical data volume.</span></span> <span data-ttu-id="fb04c-182">Overall usage is shown on the **Usage** page.</span><span class="sxs-lookup"><span data-stu-id="fb04c-182">Overall usage is shown on the **Usage** page.</span></span>
<span data-ttu-id="fb04c-183">For computers that are able to run the WireData agent, you can see how much data is being sent using the following query:</span><span class="sxs-lookup"><span data-stu-id="fb04c-183">For computers that are able to run the WireData agent, you can see how much data is being sent using the following query:</span></span>

```
Type=WireData (ProcessName="C:\\Program Files\\Microsoft Monitoring Agent\\Agent\\MonitoringHost.exe") (Direction=Outbound) | measure Sum(TotalBytes) by Computer
```



## <a name="next-steps"></a><span data-ttu-id="fb04c-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="fb04c-184">Next steps</span></span>
* <span data-ttu-id="fb04c-185">[Get started with Log Analytics](log-analytics-get-started.md) to learn more about Log Analytics and get up and running in minutes.</span><span class="sxs-lookup"><span data-stu-id="fb04c-185">[Get started with Log Analytics](log-analytics-get-started.md) to learn more about Log Analytics and get up and running in minutes.</span></span>
