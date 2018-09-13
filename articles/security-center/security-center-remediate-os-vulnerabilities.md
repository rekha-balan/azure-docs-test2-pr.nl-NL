---
title: Remediate security configurations in Azure Security Center | Microsoft Docs
description: This document shows you how to implement the Azure Security Center recommendation, "Remediate security configurations."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2018
ms.author: terrylan
ms.openlocfilehash: 74bfc3435ad6d247dabd3a7cbf2910ede5f8c8ca
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44775820"
---
# <a name="remediate-security-configurations-in-azure-security-center"></a><span data-ttu-id="e5e67-103">Remediate security configurations in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="e5e67-103">Remediate security configurations in Azure Security Center</span></span>
<span data-ttu-id="e5e67-104">Azure Security Center analyzes daily the operating system (OS) of your virtual machines (VMs) and computers for a configuration that could make the VMs and computers more vulnerable to attack.</span><span class="sxs-lookup"><span data-stu-id="e5e67-104">Azure Security Center analyzes daily the operating system (OS) of your virtual machines (VMs) and computers for a configuration that could make the VMs and computers more vulnerable to attack.</span></span> <span data-ttu-id="e5e67-105">Security Center recommends that you resolve vulnerabilities when your OS configuration does not match the recommended security configuration rules, and it recommends configuration changes to address these vulnerabilities.</span><span class="sxs-lookup"><span data-stu-id="e5e67-105">Security Center recommends that you resolve vulnerabilities when your OS configuration does not match the recommended security configuration rules, and it recommends configuration changes to address these vulnerabilities.</span></span>

<span data-ttu-id="e5e67-106">For more information about the specific configurations that are being monitored, see the [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="e5e67-106">For more information about the specific configurations that are being monitored, see the [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="e5e67-107">To learn how to customize security configuration assessments, see [Customize OS security configurations in Azure Security Center (Preview)](security-center-customize-os-security-config.md).</span><span class="sxs-lookup"><span data-stu-id="e5e67-107">To learn how to customize security configuration assessments, see [Customize OS security configurations in Azure Security Center (Preview)](security-center-customize-os-security-config.md).</span></span>

## <a name="implement-the-recommendation"></a><span data-ttu-id="e5e67-108">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="e5e67-108">Implement the recommendation</span></span>
<span data-ttu-id="e5e67-109">"Remediate security configurations" is presented as a recommendation in Security Center.</span><span class="sxs-lookup"><span data-stu-id="e5e67-109">"Remediate security configurations" is presented as a recommendation in Security Center.</span></span> <span data-ttu-id="e5e67-110">The recommendation is displayed under **Recommendations** > **Compute & apps**.</span><span class="sxs-lookup"><span data-stu-id="e5e67-110">The recommendation is displayed under **Recommendations** > **Compute & apps**.</span></span>

<span data-ttu-id="e5e67-111">This example covers the "Remediate security configurations" recommendation under **Compute & apps**.</span><span class="sxs-lookup"><span data-stu-id="e5e67-111">This example covers the "Remediate security configurations" recommendation under **Compute & apps**.</span></span>
1. <span data-ttu-id="e5e67-112">In Security Center, in the left pane, select **Compute & apps**.</span><span class="sxs-lookup"><span data-stu-id="e5e67-112">In Security Center, in the left pane, select **Compute & apps**.</span></span>  
  <span data-ttu-id="e5e67-113">The **Compute & apps** window opens.</span><span class="sxs-lookup"><span data-stu-id="e5e67-113">The **Compute & apps** window opens.</span></span>

   ![Remediate security configurations][1]

2. <span data-ttu-id="e5e67-115">Select **Remediate security configurations**.</span><span class="sxs-lookup"><span data-stu-id="e5e67-115">Select **Remediate security configurations**.</span></span>  
  <span data-ttu-id="e5e67-116">The **Security configurations** window opens.</span><span class="sxs-lookup"><span data-stu-id="e5e67-116">The **Security configurations** window opens.</span></span>

   ![The "Security configurations" window][2]

  <span data-ttu-id="e5e67-118">The upper section of the dashboard displays:</span><span class="sxs-lookup"><span data-stu-id="e5e67-118">The upper section of the dashboard displays:</span></span>

  - <span data-ttu-id="e5e67-119">**Failed rules by severity**: The total number of rules that the OS configuration failed across your VMs and computers, broken out by severity.</span><span class="sxs-lookup"><span data-stu-id="e5e67-119">**Failed rules by severity**: The total number of rules that the OS configuration failed across your VMs and computers, broken out by severity.</span></span>
  - <span data-ttu-id="e5e67-120">**Failed rules by type**: The total number of rules that the OS configuration failed across your VMs and computers, broken out by type.</span><span class="sxs-lookup"><span data-stu-id="e5e67-120">**Failed rules by type**: The total number of rules that the OS configuration failed across your VMs and computers, broken out by type.</span></span>
  - <span data-ttu-id="e5e67-121">**Failed Windows rules**: The total number of rules failed by your Windows OS configurations.</span><span class="sxs-lookup"><span data-stu-id="e5e67-121">**Failed Windows rules**: The total number of rules failed by your Windows OS configurations.</span></span>
  - <span data-ttu-id="e5e67-122">**Failed Linux rules**: The total number of rules failed by your Linux OS configurations.</span><span class="sxs-lookup"><span data-stu-id="e5e67-122">**Failed Linux rules**: The total number of rules failed by your Linux OS configurations.</span></span>

  <span data-ttu-id="e5e67-123">The lower section of the dashboard lists all failed rules for your VMs and computers, and the severity of the missing update.</span><span class="sxs-lookup"><span data-stu-id="e5e67-123">The lower section of the dashboard lists all failed rules for your VMs and computers, and the severity of the missing update.</span></span> <span data-ttu-id="e5e67-124">The list contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="e5e67-124">The list contains the following elements:</span></span>

  - <span data-ttu-id="e5e67-125">**CCEID**: The CCE unique identifier for the rule.</span><span class="sxs-lookup"><span data-stu-id="e5e67-125">**CCEID**: The CCE unique identifier for the rule.</span></span> <span data-ttu-id="e5e67-126">Security Center uses Common Configuration Enumeration (CCE) to assign unique identifiers to configuration rules.</span><span class="sxs-lookup"><span data-stu-id="e5e67-126">Security Center uses Common Configuration Enumeration (CCE) to assign unique identifiers to configuration rules.</span></span>
  - <span data-ttu-id="e5e67-127">**Name**: The name of the failed rule.</span><span class="sxs-lookup"><span data-stu-id="e5e67-127">**Name**: The name of the failed rule.</span></span>
  - <span data-ttu-id="e5e67-128">**Rule type**: The *Registry key*, *Security policy*, *Audit policy*, or *IIS* rule type.</span><span class="sxs-lookup"><span data-stu-id="e5e67-128">**Rule type**: The *Registry key*, *Security policy*, *Audit policy*, or *IIS* rule type.</span></span>
  - <span data-ttu-id="e5e67-129">**No. of VMs & computers**: The total number of VMs and computers that the failed rule applies to.</span><span class="sxs-lookup"><span data-stu-id="e5e67-129">**No. of VMs & computers**: The total number of VMs and computers that the failed rule applies to.</span></span>
  - <span data-ttu-id="e5e67-130">**Rule severity**: The CCE value *Critical*, *Important*, or *Warning*.</span><span class="sxs-lookup"><span data-stu-id="e5e67-130">**Rule severity**: The CCE value *Critical*, *Important*, or *Warning*.</span></span>
  - <span data-ttu-id="e5e67-131">**State**: The current state of the recommendation:</span><span class="sxs-lookup"><span data-stu-id="e5e67-131">**State**: The current state of the recommendation:</span></span>

    - <span data-ttu-id="e5e67-132">**Open**: The recommendation has not been addressed yet.</span><span class="sxs-lookup"><span data-stu-id="e5e67-132">**Open**: The recommendation has not been addressed yet.</span></span>
    - <span data-ttu-id="e5e67-133">**In Progress**: The recommendation is currently being applied to the resources, and no action is required by you.</span><span class="sxs-lookup"><span data-stu-id="e5e67-133">**In Progress**: The recommendation is currently being applied to the resources, and no action is required by you.</span></span>
    - <span data-ttu-id="e5e67-134">**Resolved**: The recommendation has been applied.</span><span class="sxs-lookup"><span data-stu-id="e5e67-134">**Resolved**: The recommendation has been applied.</span></span> <span data-ttu-id="e5e67-135">When the issue is resolved, the entry is dimmed.</span><span class="sxs-lookup"><span data-stu-id="e5e67-135">When the issue is resolved, the entry is dimmed.</span></span>

3. <span data-ttu-id="e5e67-136">To view the details of a failed rule, select it in the list.</span><span class="sxs-lookup"><span data-stu-id="e5e67-136">To view the details of a failed rule, select it in the list.</span></span>

   ![Detailed view of a failed configuration rule][3]

   <span data-ttu-id="e5e67-138">The detailed view displays the following information:</span><span class="sxs-lookup"><span data-stu-id="e5e67-138">The detailed view displays the following information:</span></span>

   - <span data-ttu-id="e5e67-139">**Name**: The name of the rule.</span><span class="sxs-lookup"><span data-stu-id="e5e67-139">**Name**: The name of the rule.</span></span>
   - <span data-ttu-id="e5e67-140">**CCIED**: The CCE unique identifier for the rule.</span><span class="sxs-lookup"><span data-stu-id="e5e67-140">**CCIED**: The CCE unique identifier for the rule.</span></span>
   - <span data-ttu-id="e5e67-141">**OS version**: The OS version of the VM or computer.</span><span class="sxs-lookup"><span data-stu-id="e5e67-141">**OS version**: The OS version of the VM or computer.</span></span>
   - <span data-ttu-id="e5e67-142">**Rule severity**: The CCE value *Critical*, *Important*, or *Warning*.</span><span class="sxs-lookup"><span data-stu-id="e5e67-142">**Rule severity**: The CCE value *Critical*, *Important*, or *Warning*.</span></span>
   - <span data-ttu-id="e5e67-143">**Full description**: The description of the rule.</span><span class="sxs-lookup"><span data-stu-id="e5e67-143">**Full description**: The description of the rule.</span></span>
   - <span data-ttu-id="e5e67-144">**Vulnerability**: The explanation of vulnerability or risk if the rule is not applied.</span><span class="sxs-lookup"><span data-stu-id="e5e67-144">**Vulnerability**: The explanation of vulnerability or risk if the rule is not applied.</span></span>
   - <span data-ttu-id="e5e67-145">**Potential impact**: The business impact when the rule is applied.</span><span class="sxs-lookup"><span data-stu-id="e5e67-145">**Potential impact**: The business impact when the rule is applied.</span></span>
   - <span data-ttu-id="e5e67-146">**Countermeasure**: The remediation steps.</span><span class="sxs-lookup"><span data-stu-id="e5e67-146">**Countermeasure**: The remediation steps.</span></span>
   - <span data-ttu-id="e5e67-147">**Expected value**: The value that's expected when Security Center analyzes your VM OS configuration against the rule.</span><span class="sxs-lookup"><span data-stu-id="e5e67-147">**Expected value**: The value that's expected when Security Center analyzes your VM OS configuration against the rule.</span></span>
   - <span data-ttu-id="e5e67-148">**Actual value**: The value that's returned after an analysis of your VM OS configuration against the rule.</span><span class="sxs-lookup"><span data-stu-id="e5e67-148">**Actual value**: The value that's returned after an analysis of your VM OS configuration against the rule.</span></span>
   - <span data-ttu-id="e5e67-149">**Rule operation**: The rule operation that's used by Security Center during the analysis of your VM OS configuration against the rule.</span><span class="sxs-lookup"><span data-stu-id="e5e67-149">**Rule operation**: The rule operation that's used by Security Center during the analysis of your VM OS configuration against the rule.</span></span>

4. <span data-ttu-id="e5e67-150">At the top of the detailed view window, select **Search**.</span><span class="sxs-lookup"><span data-stu-id="e5e67-150">At the top of the detailed view window, select **Search**.</span></span>  
  <span data-ttu-id="e5e67-151">Search opens a list of workspaces that have VMs and computers with the selected security configurations mismatch.</span><span class="sxs-lookup"><span data-stu-id="e5e67-151">Search opens a list of workspaces that have VMs and computers with the selected security configurations mismatch.</span></span> <span data-ttu-id="e5e67-152">The workspace selection is shown only if the selected rule applies to multiple VMs that are connected to different workspaces.</span><span class="sxs-lookup"><span data-stu-id="e5e67-152">The workspace selection is shown only if the selected rule applies to multiple VMs that are connected to different workspaces.</span></span>

   ![Listed workspaces][4]

5. <span data-ttu-id="e5e67-154">Select a workspace.</span><span class="sxs-lookup"><span data-stu-id="e5e67-154">Select a workspace.</span></span>  
  <span data-ttu-id="e5e67-155">A Log Analytics search query opens filtered to the workspace with the security configurations mismatch.</span><span class="sxs-lookup"><span data-stu-id="e5e67-155">A Log Analytics search query opens filtered to the workspace with the security configurations mismatch.</span></span>

   ![Workspace with OS vulnerability][5]

6. <span data-ttu-id="e5e67-157">Select a computer in the list.</span><span class="sxs-lookup"><span data-stu-id="e5e67-157">Select a computer in the list.</span></span>  
  <span data-ttu-id="e5e67-158">A new search result opens with information filtered only for that computer.</span><span class="sxs-lookup"><span data-stu-id="e5e67-158">A new search result opens with information filtered only for that computer.</span></span>

   ![Detailed information about the selected computer][6]

## <a name="next-steps"></a><span data-ttu-id="e5e67-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5e67-160">Next steps</span></span>
<span data-ttu-id="e5e67-161">This article showed you how to implement the Security Center recommendation "Remediate security configurations."</span><span class="sxs-lookup"><span data-stu-id="e5e67-161">This article showed you how to implement the Security Center recommendation "Remediate security configurations."</span></span> <span data-ttu-id="e5e67-162">To learn how to customize security configuration assessments, see [Customize OS security configurations in Azure Security Center (Preview)](security-center-customize-os-security-config.md).</span><span class="sxs-lookup"><span data-stu-id="e5e67-162">To learn how to customize security configuration assessments, see [Customize OS security configurations in Azure Security Center (Preview)](security-center-customize-os-security-config.md).</span></span>

<span data-ttu-id="e5e67-163">To review the specific configurations that are being monitored, see [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="e5e67-163">To review the specific configurations that are being monitored, see [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="e5e67-164">Security Center uses Common Configuration Enumeration (CCE) to assign unique identifiers to configuration rules.</span><span class="sxs-lookup"><span data-stu-id="e5e67-164">Security Center uses Common Configuration Enumeration (CCE) to assign unique identifiers to configuration rules.</span></span> <span data-ttu-id="e5e67-165">For more information, go to the [CCE](https://nvd.nist.gov/cce/index.cfm) site.</span><span class="sxs-lookup"><span data-stu-id="e5e67-165">For more information, go to the [CCE](https://nvd.nist.gov/cce/index.cfm) site.</span></span>

<span data-ttu-id="e5e67-166">To learn more about Security Center, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="e5e67-166">To learn more about Security Center, see the following resources:</span></span>

* <span data-ttu-id="e5e67-167">For a list of supported Windows and Linux VMs, see [Supported platforms in Azure Security Center](security-center-os-coverage.md).</span><span class="sxs-lookup"><span data-stu-id="e5e67-167">For a list of supported Windows and Linux VMs, see [Supported platforms in Azure Security Center](security-center-os-coverage.md).</span></span>
* <span data-ttu-id="e5e67-168">To learn how to configure security policies for your Azure subscriptions and resource groups, see [Setting security policies in Azure Security Center](security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="e5e67-168">To learn how to configure security policies for your Azure subscriptions and resource groups, see [Setting security policies in Azure Security Center](security-center-policies.md).</span></span>
* <span data-ttu-id="e5e67-169">To learn how recommendations help you protect your Azure resources, see [Managing security recommendations in Azure Security Center](security-center-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="e5e67-169">To learn how recommendations help you protect your Azure resources, see [Managing security recommendations in Azure Security Center](security-center-recommendations.md).</span></span>
* <span data-ttu-id="e5e67-170">To learn how to monitor the health of your Azure resources, see [Security health monitoring in Azure Security Center](security-center-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="e5e67-170">To learn how to monitor the health of your Azure resources, see [Security health monitoring in Azure Security Center](security-center-monitoring.md).</span></span>
* <span data-ttu-id="e5e67-171">To learn how to manage and respond to security alerts, see [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="e5e67-171">To learn how to manage and respond to security alerts, see [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span>
* <span data-ttu-id="e5e67-172">To learn how to monitor the health status of your partner solutions, see [Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="e5e67-172">To learn how to monitor the health status of your partner solutions, see [Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md).</span></span>
* <span data-ttu-id="e5e67-173">For answers to frequently asked questions about using the service, see [Azure Security Center FAQ](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="e5e67-173">For answers to frequently asked questions about using the service, see [Azure Security Center FAQ](security-center-faq.md).</span></span>
* <span data-ttu-id="e5e67-174">For blog posts about Azure security and compliance, see [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="e5e67-174">For blog posts about Azure security and compliance, see [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/).</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/compute-blade.png
[2]:./media/security-center-remediate-os-vulnerabilities/os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
[4]: ./media/security-center-remediate-os-vulnerabilities/search.png
[5]: ./media/security-center-remediate-os-vulnerabilities/log-search.png
[6]: ./media/security-center-remediate-os-vulnerabilities/search-results.png
