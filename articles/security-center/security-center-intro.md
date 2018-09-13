---
title: Introduction to Azure Security Center | Microsoft Docs
description: Learn about Azure Security Center, its key capabilities, and how it works.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/05/2017
ms.author: terrylan
ms.openlocfilehash: e0e13f5cdc3c794f3080d345f7f79f28c3ccb779
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556725"
---
# <a name="introduction-to-azure-security-center"></a><span data-ttu-id="98ae0-103">Introduction to Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="98ae0-103">Introduction to Azure Security Center</span></span>
<span data-ttu-id="98ae0-104">Learn about Azure Security Center, its key capabilities, and how it works.</span><span class="sxs-lookup"><span data-stu-id="98ae0-104">Learn about Azure Security Center, its key capabilities, and how it works.</span></span>

> [!NOTE]
> <span data-ttu-id="98ae0-105">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="98ae0-105">This document introduces the service by using an example deployment.</span></span>
>
>

## <a name="what-is-azure-security-center"></a><span data-ttu-id="98ae0-106">What is Azure Security Center?</span><span class="sxs-lookup"><span data-stu-id="98ae0-106">What is Azure Security Center?</span></span>
 <span data-ttu-id="98ae0-107">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="98ae0-107">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="98ae0-108">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span><span class="sxs-lookup"><span data-stu-id="98ae0-108">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

## <a name="key-capabilities"></a><span data-ttu-id="98ae0-109">Key capabilities</span><span class="sxs-lookup"><span data-stu-id="98ae0-109">Key capabilities</span></span>
 <span data-ttu-id="98ae0-110">Security Center delivers easy-to-use and effective threat prevention, detection, and response capabilities that are built in to Azure.</span><span class="sxs-lookup"><span data-stu-id="98ae0-110">Security Center delivers easy-to-use and effective threat prevention, detection, and response capabilities that are built in to Azure.</span></span> <span data-ttu-id="98ae0-111">Key capabilities are:</span><span class="sxs-lookup"><span data-stu-id="98ae0-111">Key capabilities are:</span></span>

| <span data-ttu-id="98ae0-112">Stage</span><span class="sxs-lookup"><span data-stu-id="98ae0-112">Stage</span></span> | <span data-ttu-id="98ae0-113">Capability</span><span class="sxs-lookup"><span data-stu-id="98ae0-113">Capability</span></span> |
| --- | --- |
| <span data-ttu-id="98ae0-114">Prevent</span><span class="sxs-lookup"><span data-stu-id="98ae0-114">Prevent</span></span> |<span data-ttu-id="98ae0-115">Monitors the security state of your Azure resources</span><span class="sxs-lookup"><span data-stu-id="98ae0-115">Monitors the security state of your Azure resources</span></span> |
| <span data-ttu-id="98ae0-116">Prevent</span><span class="sxs-lookup"><span data-stu-id="98ae0-116">Prevent</span></span> | <span data-ttu-id="98ae0-117">Defines policies for your Azure subscriptions and resource groups based on your company’s security requirements, the types of applications that you use, and the sensitivity of your data</span><span class="sxs-lookup"><span data-stu-id="98ae0-117">Defines policies for your Azure subscriptions and resource groups based on your company’s security requirements, the types of applications that you use, and the sensitivity of your data</span></span> |
| <span data-ttu-id="98ae0-118">Prevent</span><span class="sxs-lookup"><span data-stu-id="98ae0-118">Prevent</span></span> | <span data-ttu-id="98ae0-119">Uses policy-driven security recommendations to guide service owners through the process of implementing needed controls</span><span class="sxs-lookup"><span data-stu-id="98ae0-119">Uses policy-driven security recommendations to guide service owners through the process of implementing needed controls</span></span> |
| <span data-ttu-id="98ae0-120">Prevent</span><span class="sxs-lookup"><span data-stu-id="98ae0-120">Prevent</span></span> | <span data-ttu-id="98ae0-121">Rapidly deploys security services and appliances from Microsoft and partners</span><span class="sxs-lookup"><span data-stu-id="98ae0-121">Rapidly deploys security services and appliances from Microsoft and partners</span></span> |
| <span data-ttu-id="98ae0-122">Detect</span><span class="sxs-lookup"><span data-stu-id="98ae0-122">Detect</span></span> |<span data-ttu-id="98ae0-123">Automatically collects and analyzes security data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls</span><span class="sxs-lookup"><span data-stu-id="98ae0-123">Automatically collects and analyzes security data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls</span></span> |
| <span data-ttu-id="98ae0-124">Detect</span><span class="sxs-lookup"><span data-stu-id="98ae0-124">Detect</span></span> | <span data-ttu-id="98ae0-125">Leverages global threat intelligence from Microsoft products and services, the Microsoft Digital Crimes Unit (DCU), the Microsoft Security Response Center (MSRC), and external feeds</span><span class="sxs-lookup"><span data-stu-id="98ae0-125">Leverages global threat intelligence from Microsoft products and services, the Microsoft Digital Crimes Unit (DCU), the Microsoft Security Response Center (MSRC), and external feeds</span></span> |
| <span data-ttu-id="98ae0-126">Detect</span><span class="sxs-lookup"><span data-stu-id="98ae0-126">Detect</span></span> | <span data-ttu-id="98ae0-127">Applies advanced analytics, including machine learning and behavioral analysis</span><span class="sxs-lookup"><span data-stu-id="98ae0-127">Applies advanced analytics, including machine learning and behavioral analysis</span></span> |
| <span data-ttu-id="98ae0-128">Respond</span><span class="sxs-lookup"><span data-stu-id="98ae0-128">Respond</span></span> |<span data-ttu-id="98ae0-129">Provides prioritized security incidents/alerts</span><span class="sxs-lookup"><span data-stu-id="98ae0-129">Provides prioritized security incidents/alerts</span></span> |
| <span data-ttu-id="98ae0-130">Respond</span><span class="sxs-lookup"><span data-stu-id="98ae0-130">Respond</span></span> | <span data-ttu-id="98ae0-131">Offers insights into the source of the attack and impacted resources</span><span class="sxs-lookup"><span data-stu-id="98ae0-131">Offers insights into the source of the attack and impacted resources</span></span> |
| <span data-ttu-id="98ae0-132">Respond</span><span class="sxs-lookup"><span data-stu-id="98ae0-132">Respond</span></span> | <span data-ttu-id="98ae0-133">Suggests ways to stop the current attack and help prevent future attacks</span><span class="sxs-lookup"><span data-stu-id="98ae0-133">Suggests ways to stop the current attack and help prevent future attacks</span></span> |

## <a name="introductory-walkthrough"></a><span data-ttu-id="98ae0-134">Introductory walkthrough</span><span class="sxs-lookup"><span data-stu-id="98ae0-134">Introductory walkthrough</span></span>
 <span data-ttu-id="98ae0-135">You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span><span class="sxs-lookup"><span data-stu-id="98ae0-135">You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="98ae0-136">[Sign in to the portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="98ae0-136">[Sign in to the portal](https://portal.azure.com).</span></span> <span data-ttu-id="98ae0-137">Under the main portal menu, scroll to the **Security Center** option or select the **Security Center** tile that you previously pinned to the portal dashboard.</span><span class="sxs-lookup"><span data-stu-id="98ae0-137">Under the main portal menu, scroll to the **Security Center** option or select the **Security Center** tile that you previously pinned to the portal dashboard.</span></span>

![Security tile in Azure portal][1]

<span data-ttu-id="98ae0-139">From Security Center, you can set security policies, monitor security configurations, and view security alerts.</span><span class="sxs-lookup"><span data-stu-id="98ae0-139">From Security Center, you can set security policies, monitor security configurations, and view security alerts.</span></span>

### <a name="security-policies"></a><span data-ttu-id="98ae0-140">Security policies</span><span class="sxs-lookup"><span data-stu-id="98ae0-140">Security policies</span></span>
<span data-ttu-id="98ae0-141">You can define policies for your Azure subscriptions and resource groups according to your company's security requirements.</span><span class="sxs-lookup"><span data-stu-id="98ae0-141">You can define policies for your Azure subscriptions and resource groups according to your company's security requirements.</span></span> <span data-ttu-id="98ae0-142">You can also tailor them to the types of applications you're using or to the sensitivity of the data in each subscription.</span><span class="sxs-lookup"><span data-stu-id="98ae0-142">You can also tailor them to the types of applications you're using or to the sensitivity of the data in each subscription.</span></span> <span data-ttu-id="98ae0-143">For example, resources used for development or testing may have different security requirements than those used for production applications.</span><span class="sxs-lookup"><span data-stu-id="98ae0-143">For example, resources used for development or testing may have different security requirements than those used for production applications.</span></span> <span data-ttu-id="98ae0-144">Likewise, applications with regulated data like PII may require a higher level of security.</span><span class="sxs-lookup"><span data-stu-id="98ae0-144">Likewise, applications with regulated data like PII may require a higher level of security.</span></span>

> [!NOTE]
> <span data-ttu-id="98ae0-145">To modify a security policy at the subscription level or the resource group level, you must be the Owner of the subscription or a Contributor to it.</span><span class="sxs-lookup"><span data-stu-id="98ae0-145">To modify a security policy at the subscription level or the resource group level, you must be the Owner of the subscription or a Contributor to it.</span></span>
>
>

<span data-ttu-id="98ae0-146">On the **Security Center** blade, select the **Policy** tile for a list of your subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="98ae0-146">On the **Security Center** blade, select the **Policy** tile for a list of your subscriptions and resource groups.</span></span>   

![Security Center blade][2]

<span data-ttu-id="98ae0-148">On the **Security policy** blade, select a subscription to view the policy details.</span><span class="sxs-lookup"><span data-stu-id="98ae0-148">On the **Security policy** blade, select a subscription to view the policy details.</span></span>

![Security policy blade subscription][3]

<span data-ttu-id="98ae0-150">**Data collection** (see above) enables data collection for a security policy.</span><span class="sxs-lookup"><span data-stu-id="98ae0-150">**Data collection** (see above) enables data collection for a security policy.</span></span> <span data-ttu-id="98ae0-151">Enabling provides:</span><span class="sxs-lookup"><span data-stu-id="98ae0-151">Enabling provides:</span></span>

* <span data-ttu-id="98ae0-152">Daily scanning of all supported virtual machines (VMs) for security monitoring and recommendations.</span><span class="sxs-lookup"><span data-stu-id="98ae0-152">Daily scanning of all supported virtual machines (VMs) for security monitoring and recommendations.</span></span>
* <span data-ttu-id="98ae0-153">Collection of security events for analysis and threat detection.</span><span class="sxs-lookup"><span data-stu-id="98ae0-153">Collection of security events for analysis and threat detection.</span></span>

<span data-ttu-id="98ae0-154">**Choose a storage account per region** (see above) lets you choose, for each region in which you have VMs running, the storage account where data collected from those VMs is stored.</span><span class="sxs-lookup"><span data-stu-id="98ae0-154">**Choose a storage account per region** (see above) lets you choose, for each region in which you have VMs running, the storage account where data collected from those VMs is stored.</span></span> <span data-ttu-id="98ae0-155">If you do not choose a storage account for each region, it is created for you.</span><span class="sxs-lookup"><span data-stu-id="98ae0-155">If you do not choose a storage account for each region, it is created for you.</span></span> <span data-ttu-id="98ae0-156">The data that's collected is logically isolated from other customers’ data for security reasons.</span><span class="sxs-lookup"><span data-stu-id="98ae0-156">The data that's collected is logically isolated from other customers’ data for security reasons.</span></span>

> [!NOTE]
> <span data-ttu-id="98ae0-157">Data collection and choosing a storage account per region is configured at the subscription level.</span><span class="sxs-lookup"><span data-stu-id="98ae0-157">Data collection and choosing a storage account per region is configured at the subscription level.</span></span>
>
>

<span data-ttu-id="98ae0-158">Select **Prevention policy** (see above) to open the **Prevention policy** blade.</span><span class="sxs-lookup"><span data-stu-id="98ae0-158">Select **Prevention policy** (see above) to open the **Prevention policy** blade.</span></span> <span data-ttu-id="98ae0-159">**Show recommendations for** lets you choose the security controls that you want to monitor and the recommendations that you want to see based on the security needs of the resources within the subscription.</span><span class="sxs-lookup"><span data-stu-id="98ae0-159">**Show recommendations for** lets you choose the security controls that you want to monitor and the recommendations that you want to see based on the security needs of the resources within the subscription.</span></span>

<span data-ttu-id="98ae0-160">Next, select a resource group to view policy details.</span><span class="sxs-lookup"><span data-stu-id="98ae0-160">Next, select a resource group to view policy details.</span></span>

![Security policy blade resource group][4]

<span data-ttu-id="98ae0-162">**Inheritance** (see above) lets you define the resource group as:</span><span class="sxs-lookup"><span data-stu-id="98ae0-162">**Inheritance** (see above) lets you define the resource group as:</span></span>

* <span data-ttu-id="98ae0-163">Inherited (default) which means all security policies for this resource group are inherited from the subscription level.</span><span class="sxs-lookup"><span data-stu-id="98ae0-163">Inherited (default) which means all security policies for this resource group are inherited from the subscription level.</span></span>
* <span data-ttu-id="98ae0-164">Unique which means the resource group has a custom security policy.</span><span class="sxs-lookup"><span data-stu-id="98ae0-164">Unique which means the resource group has a custom security policy.</span></span> <span data-ttu-id="98ae0-165">You need to make changes under **Show recommendations for**.</span><span class="sxs-lookup"><span data-stu-id="98ae0-165">You need to make changes under **Show recommendations for**.</span></span>

> [!NOTE]
> <span data-ttu-id="98ae0-166">If there is a conflict between subscription level policy and resource group level policy, the resource group level policy takes precedence.</span><span class="sxs-lookup"><span data-stu-id="98ae0-166">If there is a conflict between subscription level policy and resource group level policy, the resource group level policy takes precedence.</span></span>
>
>

### <a name="security-recommendations"></a><span data-ttu-id="98ae0-167">Security recommendations</span><span class="sxs-lookup"><span data-stu-id="98ae0-167">Security recommendations</span></span>
 <span data-ttu-id="98ae0-168">Security Center analyzes the security state of your Azure resources to identify potential security vulnerabilities.</span><span class="sxs-lookup"><span data-stu-id="98ae0-168">Security Center analyzes the security state of your Azure resources to identify potential security vulnerabilities.</span></span> <span data-ttu-id="98ae0-169">A list of recommendations guides you through the process of configuring needed controls.</span><span class="sxs-lookup"><span data-stu-id="98ae0-169">A list of recommendations guides you through the process of configuring needed controls.</span></span> <span data-ttu-id="98ae0-170">Examples include:</span><span class="sxs-lookup"><span data-stu-id="98ae0-170">Examples include:</span></span>

* <span data-ttu-id="98ae0-171">Provisioning antimalware to help identify and remove malicious software</span><span class="sxs-lookup"><span data-stu-id="98ae0-171">Provisioning antimalware to help identify and remove malicious software</span></span>
* <span data-ttu-id="98ae0-172">Configuring network security groups and rules to control traffic to VMs</span><span class="sxs-lookup"><span data-stu-id="98ae0-172">Configuring network security groups and rules to control traffic to VMs</span></span>
* <span data-ttu-id="98ae0-173">Provisioning of web application firewalls to help defend against attacks that target your web applications</span><span class="sxs-lookup"><span data-stu-id="98ae0-173">Provisioning of web application firewalls to help defend against attacks that target your web applications</span></span>
* <span data-ttu-id="98ae0-174">Deploying missing system updates</span><span class="sxs-lookup"><span data-stu-id="98ae0-174">Deploying missing system updates</span></span>
* <span data-ttu-id="98ae0-175">Addressing OS configurations that do not match the recommended baselines</span><span class="sxs-lookup"><span data-stu-id="98ae0-175">Addressing OS configurations that do not match the recommended baselines</span></span>

<span data-ttu-id="98ae0-176">Click the **Recommendations** tile for a list of recommendations.</span><span class="sxs-lookup"><span data-stu-id="98ae0-176">Click the **Recommendations** tile for a list of recommendations.</span></span> <span data-ttu-id="98ae0-177">Click each recommendation to view additional information or to take action to resolve the issue.</span><span class="sxs-lookup"><span data-stu-id="98ae0-177">Click each recommendation to view additional information or to take action to resolve the issue.</span></span>

![Security recommendations in Azure Security Center][5]

### <a name="resource-health"></a><span data-ttu-id="98ae0-179">Resource health</span><span class="sxs-lookup"><span data-stu-id="98ae0-179">Resource health</span></span>
<span data-ttu-id="98ae0-180">The **Resource security health** tile shows the overall security posture of the environment by resource type, including VMs, web applications, and other resources.</span><span class="sxs-lookup"><span data-stu-id="98ae0-180">The **Resource security health** tile shows the overall security posture of the environment by resource type, including VMs, web applications, and other resources.</span></span>   

<span data-ttu-id="98ae0-181">Select a resource type on the **Resource security health** tile to view more information, including a list of any potential security vulnerabilities that have been identified.</span><span class="sxs-lookup"><span data-stu-id="98ae0-181">Select a resource type on the **Resource security health** tile to view more information, including a list of any potential security vulnerabilities that have been identified.</span></span> <span data-ttu-id="98ae0-182">(**Compute** is selected in the example below.)</span><span class="sxs-lookup"><span data-stu-id="98ae0-182">(**Compute** is selected in the example below.)</span></span>

![Resources health tile][6]

### <a name="security-alerts"></a><span data-ttu-id="98ae0-184">Security alerts</span><span class="sxs-lookup"><span data-stu-id="98ae0-184">Security alerts</span></span>
 <span data-ttu-id="98ae0-185">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls.</span><span class="sxs-lookup"><span data-stu-id="98ae0-185">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls.</span></span> <span data-ttu-id="98ae0-186">When threats are detected, a security alert is created.</span><span class="sxs-lookup"><span data-stu-id="98ae0-186">When threats are detected, a security alert is created.</span></span> <span data-ttu-id="98ae0-187">Examples include detection of:</span><span class="sxs-lookup"><span data-stu-id="98ae0-187">Examples include detection of:</span></span>

* <span data-ttu-id="98ae0-188">Compromised VMs communicating with known malicious IP addresses</span><span class="sxs-lookup"><span data-stu-id="98ae0-188">Compromised VMs communicating with known malicious IP addresses</span></span>
* <span data-ttu-id="98ae0-189">Advanced malware detected by using Windows error reporting</span><span class="sxs-lookup"><span data-stu-id="98ae0-189">Advanced malware detected by using Windows error reporting</span></span>
* <span data-ttu-id="98ae0-190">Brute force attacks against VMs</span><span class="sxs-lookup"><span data-stu-id="98ae0-190">Brute force attacks against VMs</span></span>
* <span data-ttu-id="98ae0-191">Security alerts from integrated antimalware programs and firewalls</span><span class="sxs-lookup"><span data-stu-id="98ae0-191">Security alerts from integrated antimalware programs and firewalls</span></span>

<span data-ttu-id="98ae0-192">Clicking the **Security alerts** tile displays a list of prioritized alerts.</span><span class="sxs-lookup"><span data-stu-id="98ae0-192">Clicking the **Security alerts** tile displays a list of prioritized alerts.</span></span>

![Security alerts][7]

<span data-ttu-id="98ae0-194">Selecting an alert shows more information about the attack and suggestions for how to remediate it.</span><span class="sxs-lookup"><span data-stu-id="98ae0-194">Selecting an alert shows more information about the attack and suggestions for how to remediate it.</span></span>

![Security alert details][8]

### <a name="partner-solutions"></a><span data-ttu-id="98ae0-196">Partner solutions</span><span class="sxs-lookup"><span data-stu-id="98ae0-196">Partner solutions</span></span>
<span data-ttu-id="98ae0-197">The **Partner solutions** tile lets you monitor at a glance the health status of your partner solutions integrated with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="98ae0-197">The **Partner solutions** tile lets you monitor at a glance the health status of your partner solutions integrated with your Azure subscription.</span></span> <span data-ttu-id="98ae0-198">Security Center displays alerts coming from the solutions.</span><span class="sxs-lookup"><span data-stu-id="98ae0-198">Security Center displays alerts coming from the solutions.</span></span>

<span data-ttu-id="98ae0-199">Select the **Partner solutions** tile.</span><span class="sxs-lookup"><span data-stu-id="98ae0-199">Select the **Partner solutions** tile.</span></span> <span data-ttu-id="98ae0-200">A blade opens displaying a list of all connected partner solutions.</span><span class="sxs-lookup"><span data-stu-id="98ae0-200">A blade opens displaying a list of all connected partner solutions.</span></span>

![Partner solutions][9]

## <a name="get-started"></a><span data-ttu-id="98ae0-202">Get started</span><span class="sxs-lookup"><span data-stu-id="98ae0-202">Get started</span></span>
<span data-ttu-id="98ae0-203">To get started with Security Center, you need a subscription to Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="98ae0-203">To get started with Security Center, you need a subscription to Microsoft Azure.</span></span> <span data-ttu-id="98ae0-204">Security Center is enabled with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="98ae0-204">Security Center is enabled with your Azure subscription.</span></span> <span data-ttu-id="98ae0-205">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="98ae0-205">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

 <span data-ttu-id="98ae0-206">You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span><span class="sxs-lookup"><span data-stu-id="98ae0-206">You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="98ae0-207">See the [portal documentation](https://azure.microsoft.com/documentation/services/azure-portal/) to learn more.</span><span class="sxs-lookup"><span data-stu-id="98ae0-207">See the [portal documentation](https://azure.microsoft.com/documentation/services/azure-portal/) to learn more.</span></span>

<span data-ttu-id="98ae0-208">[Getting started with Azure Security Center](security-center-get-started.md) quickly guides you through the security-monitoring and policy-management components of Security Center.</span><span class="sxs-lookup"><span data-stu-id="98ae0-208">[Getting started with Azure Security Center](security-center-get-started.md) quickly guides you through the security-monitoring and policy-management components of Security Center.</span></span>

## <a name="see-also"></a><span data-ttu-id="98ae0-209">See also</span><span class="sxs-lookup"><span data-stu-id="98ae0-209">See also</span></span>
<span data-ttu-id="98ae0-210">In this document, you were introduced to Security Center, its key capabilities, and how to get started.</span><span class="sxs-lookup"><span data-stu-id="98ae0-210">In this document, you were introduced to Security Center, its key capabilities, and how to get started.</span></span> <span data-ttu-id="98ae0-211">To learn more, see the following:</span><span class="sxs-lookup"><span data-stu-id="98ae0-211">To learn more, see the following:</span></span>

* <span data-ttu-id="98ae0-212">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="98ae0-212">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="98ae0-213">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="98ae0-213">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="98ae0-214">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="98ae0-214">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="98ae0-215">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="98ae0-215">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="98ae0-216">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="98ae0-216">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="98ae0-217">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="98ae0-217">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="98ae0-218">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.</span><span class="sxs-lookup"><span data-stu-id="98ae0-218">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/security-tile.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/security-center.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/security-policy.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/security-policy-blade.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/recommendations.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/resources-health.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/security-alert.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/security-alert-detail.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/partner-solutions.png









