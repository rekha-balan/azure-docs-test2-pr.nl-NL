---
title: Security monitoring in Azure Security Center | Microsoft Docs
description: This article helps you to get started with monitoring capabilities in Azure Security Center.
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: ''
ms.assetid: 3bd5b122-1695-495f-ad9a-7c2a4cd1c808
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: ed7e3de3360a18e531b90ccacd10a684db8dc9cb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555269"
---
# <a name="security-health-monitoring-in-azure-security-center"></a><span data-ttu-id="8213b-103">Security health monitoring in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="8213b-103">Security health monitoring in Azure Security Center</span></span>
<span data-ttu-id="8213b-104">This article helps you use the monitoring capabilities in Azure Security Center to monitor compliance with policies.</span><span class="sxs-lookup"><span data-stu-id="8213b-104">This article helps you use the monitoring capabilities in Azure Security Center to monitor compliance with policies.</span></span>

## <a name="what-is-security-health-monitoring"></a><span data-ttu-id="8213b-105">What is security health monitoring?</span><span class="sxs-lookup"><span data-stu-id="8213b-105">What is security health monitoring?</span></span>
<span data-ttu-id="8213b-106">We often think of monitoring as watching and waiting for an event to occur so that we can react to the situation.</span><span class="sxs-lookup"><span data-stu-id="8213b-106">We often think of monitoring as watching and waiting for an event to occur so that we can react to the situation.</span></span> <span data-ttu-id="8213b-107">Security monitoring refers to having a proactive strategy that audits your resources to identify systems that do not meet organizational standards or best practices.</span><span class="sxs-lookup"><span data-stu-id="8213b-107">Security monitoring refers to having a proactive strategy that audits your resources to identify systems that do not meet organizational standards or best practices.</span></span>

## <a name="monitoring-security-health"></a><span data-ttu-id="8213b-108">Monitoring security health</span><span class="sxs-lookup"><span data-stu-id="8213b-108">Monitoring security health</span></span>
<span data-ttu-id="8213b-109">After you enable [security policies](security-center-policies.md) for a subscription’s resources, Security Center analyzes the security of your resources to identify potential vulnerabilities.</span><span class="sxs-lookup"><span data-stu-id="8213b-109">After you enable [security policies](security-center-policies.md) for a subscription’s resources, Security Center analyzes the security of your resources to identify potential vulnerabilities.</span></span> <span data-ttu-id="8213b-110">Information about your network configuration is available instantly.</span><span class="sxs-lookup"><span data-stu-id="8213b-110">Information about your network configuration is available instantly.</span></span> <span data-ttu-id="8213b-111">It may take an hour or more for information about virtual machine configuration, such as security update status and operating system configuration, to become available.</span><span class="sxs-lookup"><span data-stu-id="8213b-111">It may take an hour or more for information about virtual machine configuration, such as security update status and operating system configuration, to become available.</span></span> <span data-ttu-id="8213b-112">You can view the security state of your resources and any issues in the **Resource Security Health** blade.</span><span class="sxs-lookup"><span data-stu-id="8213b-112">You can view the security state of your resources and any issues in the **Resource Security Health** blade.</span></span> <span data-ttu-id="8213b-113">You can also view a list of those issues on the **Recommendations** blade.</span><span class="sxs-lookup"><span data-stu-id="8213b-113">You can also view a list of those issues on the **Recommendations** blade.</span></span>

<span data-ttu-id="8213b-114">For more information about how to apply recommendations, read [Implementing security recommendations in Azure Security Center](security-center-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="8213b-114">For more information about how to apply recommendations, read [Implementing security recommendations in Azure Security Center](security-center-recommendations.md).</span></span>

<span data-ttu-id="8213b-115">On the **Resource security health** tile, you can monitor the security state of your resources.</span><span class="sxs-lookup"><span data-stu-id="8213b-115">On the **Resource security health** tile, you can monitor the security state of your resources.</span></span> <span data-ttu-id="8213b-116">In the following example, you can see that a number of issues have high and medium severity and require attention.</span><span class="sxs-lookup"><span data-stu-id="8213b-116">In the following example, you can see that a number of issues have high and medium severity and require attention.</span></span> <span data-ttu-id="8213b-117">The security policies that are enabled will impact the types of controls that are monitored.</span><span class="sxs-lookup"><span data-stu-id="8213b-117">The security policies that are enabled will impact the types of controls that are monitored.</span></span>

![Resources security health tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig1-new001-2017.png)

<span data-ttu-id="8213b-119">If Security Center identifies a vulnerability that needs to be addressed, such as a virtual machine that has missing security updates or a subnet without a [network security group](/virtual-network/virtual-networks-nsg.md), it will be listed here.</span><span class="sxs-lookup"><span data-stu-id="8213b-119">If Security Center identifies a vulnerability that needs to be addressed, such as a virtual machine that has missing security updates or a subnet without a [network security group](/virtual-network/virtual-networks-nsg.md), it will be listed here.</span></span>

### <a name="monitor-compute"></a><span data-ttu-id="8213b-120">Monitor compute</span><span class="sxs-lookup"><span data-stu-id="8213b-120">Monitor compute</span></span>
<span data-ttu-id="8213b-121">When you click **Compute** in the **Resource security health** tile, the **Compute** blade that opens shows three tabs:</span><span class="sxs-lookup"><span data-stu-id="8213b-121">When you click **Compute** in the **Resource security health** tile, the **Compute** blade that opens shows three tabs:</span></span>

- <span data-ttu-id="8213b-122">**Overview**: monitoring and virtual machine recommendations.</span><span class="sxs-lookup"><span data-stu-id="8213b-122">**Overview**: monitoring and virtual machine recommendations.</span></span>
- <span data-ttu-id="8213b-123">**Virtual Machines**: list all all virtual machines and its current security state.</span><span class="sxs-lookup"><span data-stu-id="8213b-123">**Virtual Machines**: list all all virtual machines and its current security state.</span></span>
- <span data-ttu-id="8213b-124">**Cloud Services**: list of all web and worker roles monitored by Security Center.</span><span class="sxs-lookup"><span data-stu-id="8213b-124">**Cloud Services**: list of all web and worker roles monitored by Security Center.</span></span>

![Missing system update by virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig1-new002-2017.png)

<span data-ttu-id="8213b-126">In each tab you can have multiple sections, and in each section, you can select an individual option to see more details about the recommended steps to address that particular issue.</span><span class="sxs-lookup"><span data-stu-id="8213b-126">In each tab you can have multiple sections, and in each section, you can select an individual option to see more details about the recommended steps to address that particular issue.</span></span> 

#### <a name="monitoring-recommendations"></a><span data-ttu-id="8213b-127">Monitoring recommendations</span><span class="sxs-lookup"><span data-stu-id="8213b-127">Monitoring recommendations</span></span>
<span data-ttu-id="8213b-128">This section shows the total number of virtual machines that were initialized for data collection and their current statuses.</span><span class="sxs-lookup"><span data-stu-id="8213b-128">This section shows the total number of virtual machines that were initialized for data collection and their current statuses.</span></span> <span data-ttu-id="8213b-129">After all virtual machines have data collection initialized, they will be ready to receive Security Center security policies.</span><span class="sxs-lookup"><span data-stu-id="8213b-129">After all virtual machines have data collection initialized, they will be ready to receive Security Center security policies.</span></span> <span data-ttu-id="8213b-130">When you click this entry, the **VM Agent is missing or not responding** blade opens.</span><span class="sxs-lookup"><span data-stu-id="8213b-130">When you click this entry, the **VM Agent is missing or not responding** blade opens.</span></span> 

![Missing system update by virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig1-new003-2017.png)


#### <a name="virtual-machine-recommendations"></a><span data-ttu-id="8213b-132">Virtual machine recommendations</span><span class="sxs-lookup"><span data-stu-id="8213b-132">Virtual machine recommendations</span></span>
<span data-ttu-id="8213b-133">This section has a set of [recommendations for each virtual machine](security-center-virtual-machine-recommendations.md) that Azure Security Center monitors.</span><span class="sxs-lookup"><span data-stu-id="8213b-133">This section has a set of [recommendations for each virtual machine](security-center-virtual-machine-recommendations.md) that Azure Security Center monitors.</span></span> <span data-ttu-id="8213b-134">The first column lists the recommendation.</span><span class="sxs-lookup"><span data-stu-id="8213b-134">The first column lists the recommendation.</span></span> <span data-ttu-id="8213b-135">The second column shows the total number of virtual machines that are affected by that recommendation.</span><span class="sxs-lookup"><span data-stu-id="8213b-135">The second column shows the total number of virtual machines that are affected by that recommendation.</span></span> <span data-ttu-id="8213b-136">The third column shows the severity of the issue as illustrated in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="8213b-136">The third column shows the severity of the issue as illustrated in the following screenshot.</span></span>

![Virtual machine recommendations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig1-new004-2017.png)

> [!NOTE]
> <span data-ttu-id="8213b-138">Only virtual machines that have at least one public endpoint are shown in the **Networking Health** blade in the **Network topology** list.</span><span class="sxs-lookup"><span data-stu-id="8213b-138">Only virtual machines that have at least one public endpoint are shown in the **Networking Health** blade in the **Network topology** list.</span></span>
>
>

<span data-ttu-id="8213b-139">Each recommendation has a set of actions that you can perform after you click it.</span><span class="sxs-lookup"><span data-stu-id="8213b-139">Each recommendation has a set of actions that you can perform after you click it.</span></span> <span data-ttu-id="8213b-140">For example, if you click **Missing system updates**, the **Missing system updates** blade opens.</span><span class="sxs-lookup"><span data-stu-id="8213b-140">For example, if you click **Missing system updates**, the **Missing system updates** blade opens.</span></span> <span data-ttu-id="8213b-141">It lists the virtual machines that are missing patches and the severity of the missing update as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="8213b-141">It lists the virtual machines that are missing patches and the severity of the missing update as shown in the following screenshot.</span></span>

![Missing system updates for virtual machines](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig5-ga.png)

<span data-ttu-id="8213b-143">The **Missing system updates** blade shows a table with the following information:</span><span class="sxs-lookup"><span data-stu-id="8213b-143">The **Missing system updates** blade shows a table with the following information:</span></span>

* <span data-ttu-id="8213b-144">**VIRTUAL MACHINE**: The name of the virtual machine that is missing updates.</span><span class="sxs-lookup"><span data-stu-id="8213b-144">**VIRTUAL MACHINE**: The name of the virtual machine that is missing updates.</span></span>
* <span data-ttu-id="8213b-145">**SYSTEM UPDATES**: The number of system updates that are missing.</span><span class="sxs-lookup"><span data-stu-id="8213b-145">**SYSTEM UPDATES**: The number of system updates that are missing.</span></span>
* <span data-ttu-id="8213b-146">**LAST SCAN TIME**: The time that Security Center last scanned the virtual machine for updates.</span><span class="sxs-lookup"><span data-stu-id="8213b-146">**LAST SCAN TIME**: The time that Security Center last scanned the virtual machine for updates.</span></span>
* <span data-ttu-id="8213b-147">**STATE**: The current state of the recommendation:</span><span class="sxs-lookup"><span data-stu-id="8213b-147">**STATE**: The current state of the recommendation:</span></span>
  * <span data-ttu-id="8213b-148">**Open**: The recommendation has not been addressed yet.</span><span class="sxs-lookup"><span data-stu-id="8213b-148">**Open**: The recommendation has not been addressed yet.</span></span>
  * <span data-ttu-id="8213b-149">**In Progress**: The recommendation is currently being applied to those resources, and no action is required by you.</span><span class="sxs-lookup"><span data-stu-id="8213b-149">**In Progress**: The recommendation is currently being applied to those resources, and no action is required by you.</span></span>
  * <span data-ttu-id="8213b-150">**Resolved**: The recommendation was already finished.</span><span class="sxs-lookup"><span data-stu-id="8213b-150">**Resolved**: The recommendation was already finished.</span></span> <span data-ttu-id="8213b-151">(When the issue has been resolved, the entry is dimmed).</span><span class="sxs-lookup"><span data-stu-id="8213b-151">(When the issue has been resolved, the entry is dimmed).</span></span>
* <span data-ttu-id="8213b-152">**SEVERITY**: Describes the severity of that particular recommendation:</span><span class="sxs-lookup"><span data-stu-id="8213b-152">**SEVERITY**: Describes the severity of that particular recommendation:</span></span>
  * <span data-ttu-id="8213b-153">**High**: A vulnerability exists with a meaningful resource (application, virtual machine, or network security group) and requires attention.</span><span class="sxs-lookup"><span data-stu-id="8213b-153">**High**: A vulnerability exists with a meaningful resource (application, virtual machine, or network security group) and requires attention.</span></span>
  * <span data-ttu-id="8213b-154">**Medium**: Non-critical or additional steps are required to complete a process or eliminate a vulnerability.</span><span class="sxs-lookup"><span data-stu-id="8213b-154">**Medium**: Non-critical or additional steps are required to complete a process or eliminate a vulnerability.</span></span>
  * <span data-ttu-id="8213b-155">**Low**: A vulnerability should be addressed but does not require immediate attention.</span><span class="sxs-lookup"><span data-stu-id="8213b-155">**Low**: A vulnerability should be addressed but does not require immediate attention.</span></span> <span data-ttu-id="8213b-156">(By default, low recommendations are not presented, but you can filter on low recommendations if you want to view them.)</span><span class="sxs-lookup"><span data-stu-id="8213b-156">(By default, low recommendations are not presented, but you can filter on low recommendations if you want to view them.)</span></span>

<span data-ttu-id="8213b-157">To view the recommendation details, click the name of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8213b-157">To view the recommendation details, click the name of the virtual machine.</span></span> <span data-ttu-id="8213b-158">A new blade for that virtual machine opens with the list of updates as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="8213b-158">A new blade for that virtual machine opens with the list of updates as shown in the following screenshot.</span></span>

![Missing system updates for a specific virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig6-ga.png)

> [!NOTE]
> <span data-ttu-id="8213b-160">The security recommendations here are the same as those in the **Recommendations** blade.</span><span class="sxs-lookup"><span data-stu-id="8213b-160">The security recommendations here are the same as those in the **Recommendations** blade.</span></span> <span data-ttu-id="8213b-161">See the [Implementing security recommendations in Azure Security Center](security-center-recommendations.md) article for more information about how to resolve recommendations.</span><span class="sxs-lookup"><span data-stu-id="8213b-161">See the [Implementing security recommendations in Azure Security Center](security-center-recommendations.md) article for more information about how to resolve recommendations.</span></span> <span data-ttu-id="8213b-162">This is applicable not only for virtual machines but also for all resources that are available in the **Resource Health** tile.</span><span class="sxs-lookup"><span data-stu-id="8213b-162">This is applicable not only for virtual machines but also for all resources that are available in the **Resource Health** tile.</span></span>
>
>

#### <a name="virtual-machines-section"></a><span data-ttu-id="8213b-163">Virtual machines section</span><span class="sxs-lookup"><span data-stu-id="8213b-163">Virtual machines section</span></span>
<span data-ttu-id="8213b-164">The virtual machines section gives you an overview of all virtual machines and recommendations.</span><span class="sxs-lookup"><span data-stu-id="8213b-164">The virtual machines section gives you an overview of all virtual machines and recommendations.</span></span> <span data-ttu-id="8213b-165">Each column represents one set of recommendations as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="8213b-165">Each column represents one set of recommendations as shown in the following screenshot:</span></span>

![Overview of all virtual machines and recommendations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig1-new005-2017.png)

<span data-ttu-id="8213b-167">The icon that appears under each recommendation helps you to quickly identify the virtual machines that need attention and the type of recommendation.</span><span class="sxs-lookup"><span data-stu-id="8213b-167">The icon that appears under each recommendation helps you to quickly identify the virtual machines that need attention and the type of recommendation.</span></span>

<span data-ttu-id="8213b-168">In the previous example, one virtual machine has a critical recommendation regarding endpoint protection.</span><span class="sxs-lookup"><span data-stu-id="8213b-168">In the previous example, one virtual machine has a critical recommendation regarding endpoint protection.</span></span> <span data-ttu-id="8213b-169">To get more information about the virtual machine, click it.</span><span class="sxs-lookup"><span data-stu-id="8213b-169">To get more information about the virtual machine, click it.</span></span> <span data-ttu-id="8213b-170">A new blade that opens represents this virtual machine as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="8213b-170">A new blade that opens represents this virtual machine as shown in the following screenshot.</span></span>

![Virtual machine security details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig8-ga.png)

<span data-ttu-id="8213b-172">This blade has the security details for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8213b-172">This blade has the security details for the virtual machine.</span></span> <span data-ttu-id="8213b-173">At the bottom of this blade, you can see the recommended action and the severity of each issue.</span><span class="sxs-lookup"><span data-stu-id="8213b-173">At the bottom of this blade, you can see the recommended action and the severity of each issue.</span></span>

#### <a name="cloud-services-section"></a><span data-ttu-id="8213b-174">Cloud services section</span><span class="sxs-lookup"><span data-stu-id="8213b-174">Cloud services section</span></span>
<span data-ttu-id="8213b-175">For cloud services, a recommendation is created when the operating system version is out of date as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="8213b-175">For cloud services, a recommendation is created when the operating system version is out of date as shown in the following screenshot:</span></span>

![Health status for cloud services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig1-new006-2017.png)

<span data-ttu-id="8213b-177">In a scenario where you do have recommendation (which is not the case for the previous example), you need to follow the steps in the recommendation to update the operating system version.</span><span class="sxs-lookup"><span data-stu-id="8213b-177">In a scenario where you do have recommendation (which is not the case for the previous example), you need to follow the steps in the recommendation to update the operating system version.</span></span> <span data-ttu-id="8213b-178">When an update is available, you will have an alert (red or orange - depends on the severity of the issue).</span><span class="sxs-lookup"><span data-stu-id="8213b-178">When an update is available, you will have an alert (red or orange - depends on the severity of the issue).</span></span> <span data-ttu-id="8213b-179">When you click on this alert in the WebRole1 (runs Windows Server with your web app automatically deployed to IIS) or WorkerRole1 (runs Windows Server with your web app automatically deployed to IIS) rows, a new blade opens with more details about this recommendation as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="8213b-179">When you click on this alert in the WebRole1 (runs Windows Server with your web app automatically deployed to IIS) or WorkerRole1 (runs Windows Server with your web app automatically deployed to IIS) rows, a new blade opens with more details about this recommendation as shown in the following screenshot:</span></span>

![Cloud service details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig8-new3.png)

<span data-ttu-id="8213b-181">To see a more prescriptive explanation about this recommendation, click **Update OS version** under the **DESCRIPTION** column.</span><span class="sxs-lookup"><span data-stu-id="8213b-181">To see a more prescriptive explanation about this recommendation, click **Update OS version** under the **DESCRIPTION** column.</span></span> <span data-ttu-id="8213b-182">The **Update OS version (Preview)** blade opens with more details.</span><span class="sxs-lookup"><span data-stu-id="8213b-182">The **Update OS version (Preview)** blade opens with more details.</span></span>

![Cloud services recommendations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig8-new4.png)  

### <a name="monitor-virtual-networks"></a><span data-ttu-id="8213b-184">Monitor virtual networks</span><span class="sxs-lookup"><span data-stu-id="8213b-184">Monitor virtual networks</span></span>
<span data-ttu-id="8213b-185">When you click **Networking** in the **Resources security health** tile, the **Networking** blade opens with more details as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="8213b-185">When you click **Networking** in the **Resources security health** tile, the **Networking** blade opens with more details as shown in the following screenshot:</span></span>

![Networking blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig9-new3.png)

#### <a name="networking-recommendations"></a><span data-ttu-id="8213b-187">Networking recommendations</span><span class="sxs-lookup"><span data-stu-id="8213b-187">Networking recommendations</span></span>
<span data-ttu-id="8213b-188">Like the virtual machine's resource health information, this blade provides a summarized list of issues at the top of the blade and a list of monitored networks on the bottom.</span><span class="sxs-lookup"><span data-stu-id="8213b-188">Like the virtual machine's resource health information, this blade provides a summarized list of issues at the top of the blade and a list of monitored networks on the bottom.</span></span>

<span data-ttu-id="8213b-189">The networking status breakdown section lists potential security issues and offers [recommendations](security-center-network-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="8213b-189">The networking status breakdown section lists potential security issues and offers [recommendations](security-center-network-recommendations.md).</span></span> <span data-ttu-id="8213b-190">Possible issues can include:</span><span class="sxs-lookup"><span data-stu-id="8213b-190">Possible issues can include:</span></span>

* <span data-ttu-id="8213b-191">Next-Generation Firewall (NGFW) not installed</span><span class="sxs-lookup"><span data-stu-id="8213b-191">Next-Generation Firewall (NGFW) not installed</span></span>
* <span data-ttu-id="8213b-192">Network security groups on subnets not enabled</span><span class="sxs-lookup"><span data-stu-id="8213b-192">Network security groups on subnets not enabled</span></span>
* <span data-ttu-id="8213b-193">Network security groups on virtual machines not enabled</span><span class="sxs-lookup"><span data-stu-id="8213b-193">Network security groups on virtual machines not enabled</span></span>
* <span data-ttu-id="8213b-194">Restrict external access through public external endpoint</span><span class="sxs-lookup"><span data-stu-id="8213b-194">Restrict external access through public external endpoint</span></span>
* <span data-ttu-id="8213b-195">Healthy Internet facing endpoints</span><span class="sxs-lookup"><span data-stu-id="8213b-195">Healthy Internet facing endpoints</span></span>

<span data-ttu-id="8213b-196">When you click a recommendation, a new blade opens with more details about the recommendation as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="8213b-196">When you click a recommendation, a new blade opens with more details about the recommendation as shown in the following example.</span></span>

![Details for a recommendation in the Networking blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig9-ga.png)

<span data-ttu-id="8213b-198">In this example, the **Configure Missing Network Security Groups for Subnets** blade has a list of subnets and virtual machines that are missing network security group protection.</span><span class="sxs-lookup"><span data-stu-id="8213b-198">In this example, the **Configure Missing Network Security Groups for Subnets** blade has a list of subnets and virtual machines that are missing network security group protection.</span></span> <span data-ttu-id="8213b-199">If you click the subnet to which you want to apply the network security group, another blade opens.</span><span class="sxs-lookup"><span data-stu-id="8213b-199">If you click the subnet to which you want to apply the network security group, another blade opens.</span></span>

<span data-ttu-id="8213b-200">In the **Choose network security group** blade, you can select the most appropriate network security group for the subnet, or you can create a new network security group.</span><span class="sxs-lookup"><span data-stu-id="8213b-200">In the **Choose network security group** blade, you can select the most appropriate network security group for the subnet, or you can create a new network security group.</span></span>

#### <a name="internet-facing-endpoints-section"></a><span data-ttu-id="8213b-201">Internet facing endpoints section</span><span class="sxs-lookup"><span data-stu-id="8213b-201">Internet facing endpoints section</span></span>
<span data-ttu-id="8213b-202">In the **Internet facing endpoints** section, you can see the virtual machines that are currently configured with an Internet facing endpoint and its current status.</span><span class="sxs-lookup"><span data-stu-id="8213b-202">In the **Internet facing endpoints** section, you can see the virtual machines that are currently configured with an Internet facing endpoint and its current status.</span></span>

![Virtual machines configured with Internet facing endpoint and status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig10-ga.png)

<span data-ttu-id="8213b-204">This table has the endpoint name that represents the virtual machine, the Internet facing IP address, and the current severity status of the network security group and the NGFW.</span><span class="sxs-lookup"><span data-stu-id="8213b-204">This table has the endpoint name that represents the virtual machine, the Internet facing IP address, and the current severity status of the network security group and the NGFW.</span></span> <span data-ttu-id="8213b-205">The table is sorted by severity:</span><span class="sxs-lookup"><span data-stu-id="8213b-205">The table is sorted by severity:</span></span>

* <span data-ttu-id="8213b-206">Red (on top): High priority and should be addressed immediately</span><span class="sxs-lookup"><span data-stu-id="8213b-206">Red (on top): High priority and should be addressed immediately</span></span>
* <span data-ttu-id="8213b-207">Orange: Medium priority and should be addressed as soon as possible</span><span class="sxs-lookup"><span data-stu-id="8213b-207">Orange: Medium priority and should be addressed as soon as possible</span></span>
* <span data-ttu-id="8213b-208">Green (last one): Healthy state</span><span class="sxs-lookup"><span data-stu-id="8213b-208">Green (last one): Healthy state</span></span>

#### <a name="networking-topology-section"></a><span data-ttu-id="8213b-209">Networking topology section</span><span class="sxs-lookup"><span data-stu-id="8213b-209">Networking topology section</span></span>
<span data-ttu-id="8213b-210">The **Networking topology** section has a hierarchical view of the resources as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="8213b-210">The **Networking topology** section has a hierarchical view of the resources as shown in the following screenshot:</span></span>

![Hierarchical view of resources in Networking topology section](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig121-new4.png)

<span data-ttu-id="8213b-212">This table is sorted (virtual machines and subnets) by severity:</span><span class="sxs-lookup"><span data-stu-id="8213b-212">This table is sorted (virtual machines and subnets) by severity:</span></span>

* <span data-ttu-id="8213b-213">Red (on top): High priority and should be addressed immediately</span><span class="sxs-lookup"><span data-stu-id="8213b-213">Red (on top): High priority and should be addressed immediately</span></span>
* <span data-ttu-id="8213b-214">Orange: Medium priority and should be addressed as soon as possible</span><span class="sxs-lookup"><span data-stu-id="8213b-214">Orange: Medium priority and should be addressed as soon as possible</span></span>
* <span data-ttu-id="8213b-215">Green (last one): Healthy state</span><span class="sxs-lookup"><span data-stu-id="8213b-215">Green (last one): Healthy state</span></span>

<span data-ttu-id="8213b-216">In this topology view, the first level has [virtual networks](../virtual-network/virtual-networks-overview.md), [virtual network gateways](/vpn-gateway/vpn-gateway-site-to-site-create.md), and [virtual networks (classic)](/virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="8213b-216">In this topology view, the first level has [virtual networks](../virtual-network/virtual-networks-overview.md), [virtual network gateways](/vpn-gateway/vpn-gateway-site-to-site-create.md), and [virtual networks (classic)](/virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span> <span data-ttu-id="8213b-217">The second level has subnets, and the third level has the virtual machines that belong to those subnets.</span><span class="sxs-lookup"><span data-stu-id="8213b-217">The second level has subnets, and the third level has the virtual machines that belong to those subnets.</span></span> <span data-ttu-id="8213b-218">The right column has the current status of the network security group for those resources, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8213b-218">The right column has the current status of the network security group for those resources, as shown in the following example:</span></span>

![Status of the network security group in Networking topology section](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig12-ga.png)

<span data-ttu-id="8213b-220">The bottom part of this blade has the recommendations for this virtual machine, which is similar to what is described previously.</span><span class="sxs-lookup"><span data-stu-id="8213b-220">The bottom part of this blade has the recommendations for this virtual machine, which is similar to what is described previously.</span></span> <span data-ttu-id="8213b-221">You can click a recommendation to learn more or apply the needed security control or configuration.</span><span class="sxs-lookup"><span data-stu-id="8213b-221">You can click a recommendation to learn more or apply the needed security control or configuration.</span></span>

### <a name="monitor-data"></a><span data-ttu-id="8213b-222">Monitor data</span><span class="sxs-lookup"><span data-stu-id="8213b-222">Monitor data</span></span>

<span data-ttu-id="8213b-223">When you click **SQL & Data** in the **Resources security health** tile, the **Data Resources** blade opens with recommendations for SQL and Storage.</span><span class="sxs-lookup"><span data-stu-id="8213b-223">When you click **SQL & Data** in the **Resources security health** tile, the **Data Resources** blade opens with recommendations for SQL and Storage.</span></span> <span data-ttu-id="8213b-224">It also has [recommendations](security-center-sql-service-recommendations.md) for the general health state of the database.</span><span class="sxs-lookup"><span data-stu-id="8213b-224">It also has [recommendations](security-center-sql-service-recommendations.md) for the general health state of the database.</span></span> <span data-ttu-id="8213b-225">For more information about storage encryption, read [Enable encryption for Azure storage account in Azure Security Center](security-center-enable-encryption-for-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8213b-225">For more information about storage encryption, read [Enable encryption for Azure storage account in Azure Security Center](security-center-enable-encryption-for-storage-account.md).</span></span>

![Data Resources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig13-ga-new.png)

<span data-ttu-id="8213b-227">Under **SQL Recommendations**, You can click any recommendation and get more details about further action to resolve an issue.</span><span class="sxs-lookup"><span data-stu-id="8213b-227">Under **SQL Recommendations**, You can click any recommendation and get more details about further action to resolve an issue.</span></span> <span data-ttu-id="8213b-228">The following example shows the expansion of the **Database Auditing & Threat detection on SQL databases** recommendation.</span><span class="sxs-lookup"><span data-stu-id="8213b-228">The following example shows the expansion of the **Database Auditing & Threat detection on SQL databases** recommendation.</span></span>

![Details about a SQL recommendation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig14-ga-new.png)

<span data-ttu-id="8213b-230">The **Enable Auditing & Threat detection on SQL databases** blade has the following information:</span><span class="sxs-lookup"><span data-stu-id="8213b-230">The **Enable Auditing & Threat detection on SQL databases** blade has the following information:</span></span>

* <span data-ttu-id="8213b-231">A list of SQL databases</span><span class="sxs-lookup"><span data-stu-id="8213b-231">A list of SQL databases</span></span>
* <span data-ttu-id="8213b-232">The server on which they are located</span><span class="sxs-lookup"><span data-stu-id="8213b-232">The server on which they are located</span></span>
* <span data-ttu-id="8213b-233">Information about whether this setting was inherited from the server or if it is unique in this database</span><span class="sxs-lookup"><span data-stu-id="8213b-233">Information about whether this setting was inherited from the server or if it is unique in this database</span></span>
* <span data-ttu-id="8213b-234">The current state</span><span class="sxs-lookup"><span data-stu-id="8213b-234">The current state</span></span>
* <span data-ttu-id="8213b-235">The severity of the issue</span><span class="sxs-lookup"><span data-stu-id="8213b-235">The severity of the issue</span></span>

<span data-ttu-id="8213b-236">When you click the database to address this recommendation, the **Auditing & Threat detection** blade opens as shown in the following screen.</span><span class="sxs-lookup"><span data-stu-id="8213b-236">When you click the database to address this recommendation, the **Auditing & Threat detection** blade opens as shown in the following screen.</span></span>

![Auditing & Threat detection blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig15-ga.png)

<span data-ttu-id="8213b-238">To enable auditing, select **ON** under the **Auditing** option.</span><span class="sxs-lookup"><span data-stu-id="8213b-238">To enable auditing, select **ON** under the **Auditing** option.</span></span>

### <a name="monitor-applications"></a><span data-ttu-id="8213b-239">Monitor applications</span><span class="sxs-lookup"><span data-stu-id="8213b-239">Monitor applications</span></span>

<span data-ttu-id="8213b-240">If your Azure workload has applications located in [virtual machines (created through Azure Resource Manager)](../azure-resource-manager/resource-manager-deployment-model.md) with exposed web ports (TCP ports 80 and 443), Security Center can monitor those to identify potential security issues and recommend remediation steps.</span><span class="sxs-lookup"><span data-stu-id="8213b-240">If your Azure workload has applications located in [virtual machines (created through Azure Resource Manager)](../azure-resource-manager/resource-manager-deployment-model.md) with exposed web ports (TCP ports 80 and 443), Security Center can monitor those to identify potential security issues and recommend remediation steps.</span></span> <span data-ttu-id="8213b-241">When you click the **Applications** tile, the **Applications** blade opens with a series of recommendations in the **Application recommendations** section.</span><span class="sxs-lookup"><span data-stu-id="8213b-241">When you click the **Applications** tile, the **Applications** blade opens with a series of recommendations in the **Application recommendations** section.</span></span> <span data-ttu-id="8213b-242">It also shows the application breakdown per host/virtual IP as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="8213b-242">It also shows the application breakdown per host/virtual IP as shown in the following screenshot.</span></span>

![Applications security health](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig16-ga.png)

<span data-ttu-id="8213b-244">Just like you did with the other recommendations, you can click a recommendation to see more details about the issue and how to remediate.</span><span class="sxs-lookup"><span data-stu-id="8213b-244">Just like you did with the other recommendations, you can click a recommendation to see more details about the issue and how to remediate.</span></span> <span data-ttu-id="8213b-245">The example shown in the following figure is an application that was identified as an unsecure web application.</span><span class="sxs-lookup"><span data-stu-id="8213b-245">The example shown in the following figure is an application that was identified as an unsecure web application.</span></span> <span data-ttu-id="8213b-246">When you select the application that was considered not secure, another blade opens with the following option available:</span><span class="sxs-lookup"><span data-stu-id="8213b-246">When you select the application that was considered not secure, another blade opens with the following option available:</span></span>

![Details about an app that's not secure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig17-ga.png)

<span data-ttu-id="8213b-248">This blade will have a list of all recommendations for this application.</span><span class="sxs-lookup"><span data-stu-id="8213b-248">This blade will have a list of all recommendations for this application.</span></span> <span data-ttu-id="8213b-249">When you click the **Add a web application firewall** recommendation, the **Add a Web Application Firewall** blade opens with options for you to install a web application firewall (WAF) from a partner as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="8213b-249">When you click the **Add a web application firewall** recommendation, the **Add a Web Application Firewall** blade opens with options for you to install a web application firewall (WAF) from a partner as shown in the following screenshot.</span></span>

![Add Web Application Firewall dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-monitoring/security-center-monitoring-fig18-ga.png)

## <a name="see-also"></a><span data-ttu-id="8213b-251">See also</span><span class="sxs-lookup"><span data-stu-id="8213b-251">See also</span></span>
<span data-ttu-id="8213b-252">In this article, you learned how to use monitoring capabilities in Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="8213b-252">In this article, you learned how to use monitoring capabilities in Azure Security Center.</span></span> <span data-ttu-id="8213b-253">To learn more about Azure Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="8213b-253">To learn more about Azure Security Center, see the following:</span></span>

* <span data-ttu-id="8213b-254">[Setting security policies in Azure Security Center](security-center-policies.md): Learn how to configure security settings in Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="8213b-254">[Setting security policies in Azure Security Center](security-center-policies.md): Learn how to configure security settings in Azure Security Center.</span></span>
* <span data-ttu-id="8213b-255">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md): Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="8213b-255">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md): Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="8213b-256">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md): Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="8213b-256">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md): Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="8213b-257">[Azure Security Center FAQ](security-center-faq.md): Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="8213b-257">[Azure Security Center FAQ](security-center-faq.md): Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="8213b-258">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/): Find blog posts about Azure security and compliance.</span><span class="sxs-lookup"><span data-stu-id="8213b-258">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/): Find blog posts about Azure security and compliance.</span></span>






















