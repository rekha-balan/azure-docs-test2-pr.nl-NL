---
title: Remediate OS vulnerabilities in Azure Security Center | Microsoft Docs
description: This document shows you how to implement the Azure Security Center recommendation **Remediate OS vulnerabilities**.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: terrylan
ms.openlocfilehash: 6511fb993112ffc58aabf943024492e6575cb737
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556293"
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="91a3c-103">Remediate OS vulnerabilities in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="91a3c-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="91a3c-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make the VM more vulnerable to attack and recommends configuration changes to address these vulnerabilities.</span><span class="sxs-lookup"><span data-stu-id="91a3c-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make the VM more vulnerable to attack and recommends configuration changes to address these vulnerabilities.</span></span> <span data-ttu-id="91a3c-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match the recommended configuration rules.</span><span class="sxs-lookup"><span data-stu-id="91a3c-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match the recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="91a3c-106">For more information on the specific configurations being monitored, see the [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="91a3c-106">For more information on the specific configurations being monitored, see the [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="91a3c-107">At this time, Windows Server 2016 is not fully supported.</span><span class="sxs-lookup"><span data-stu-id="91a3c-107">At this time, Windows Server 2016 is not fully supported.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="91a3c-108">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="91a3c-108">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="91a3c-109">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="91a3c-109">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="91a3c-110">This is not a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="91a3c-110">This is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="91a3c-111">In the **Recommendations** blade, select **Remediate OS vulnerabilities**.</span><span class="sxs-lookup"><span data-stu-id="91a3c-111">In the **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="91a3c-112">![Remediate OS vulnerabilities][1]</span><span class="sxs-lookup"><span data-stu-id="91a3c-112">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="91a3c-113">The **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match the recommended configuration rules.</span><span class="sxs-lookup"><span data-stu-id="91a3c-113">The **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match the recommended configuration rules.</span></span>  <span data-ttu-id="91a3c-114">For each VM, the blade identifies:</span><span class="sxs-lookup"><span data-stu-id="91a3c-114">For each VM, the blade identifies:</span></span>

   * <span data-ttu-id="91a3c-115">**FAILED RULES** -- The number of rules that the VM's OS configuration failed.</span><span class="sxs-lookup"><span data-stu-id="91a3c-115">**FAILED RULES** -- The number of rules that the VM's OS configuration failed.</span></span>
   * <span data-ttu-id="91a3c-116">**LAST SCAN TIME** -- The date and time that Security Center last scanned the VM’s OS configuration.</span><span class="sxs-lookup"><span data-stu-id="91a3c-116">**LAST SCAN TIME** -- The date and time that Security Center last scanned the VM’s OS configuration.</span></span>
   * <span data-ttu-id="91a3c-117">**STATE** -- The current state of the vulnerability:</span><span class="sxs-lookup"><span data-stu-id="91a3c-117">**STATE** -- The current state of the vulnerability:</span></span>

     * <span data-ttu-id="91a3c-118">Open: The vulnerability has not been addressed yet</span><span class="sxs-lookup"><span data-stu-id="91a3c-118">Open: The vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="91a3c-119">In Progress: The vulnerability is currently being applied, no action is required by you</span><span class="sxs-lookup"><span data-stu-id="91a3c-119">In Progress: The vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="91a3c-120">Resolved: The vulnerability was already addressed (when the issue has been resolved, the entry is grayed out)</span><span class="sxs-lookup"><span data-stu-id="91a3c-120">Resolved: The vulnerability was already addressed (when the issue has been resolved, the entry is grayed out)</span></span>
   * <span data-ttu-id="91a3c-121">**SEVERITY** -- All vulnerabilities are set to a severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span><span class="sxs-lookup"><span data-stu-id="91a3c-121">**SEVERITY** -- All vulnerabilities are set to a severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="91a3c-122">Select a VM.</span><span class="sxs-lookup"><span data-stu-id="91a3c-122">Select a VM.</span></span> <span data-ttu-id="91a3c-123">A blade for that VM opens and displays the rules that have failed.</span><span class="sxs-lookup"><span data-stu-id="91a3c-123">A blade for that VM opens and displays the rules that have failed.</span></span>
   <span data-ttu-id="91a3c-124">![Configuration rules that have failed][2]</span><span class="sxs-lookup"><span data-stu-id="91a3c-124">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="91a3c-125">Select a rule.</span><span class="sxs-lookup"><span data-stu-id="91a3c-125">Select a rule.</span></span> <span data-ttu-id="91a3c-126">In this example, lets select **Password must meet complexity requirements**.</span><span class="sxs-lookup"><span data-stu-id="91a3c-126">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="91a3c-127">A blade opens describing the failed rule and the impact.</span><span class="sxs-lookup"><span data-stu-id="91a3c-127">A blade opens describing the failed rule and the impact.</span></span> <span data-ttu-id="91a3c-128">Review the details and consider how operating system configurations will be applied.</span><span class="sxs-lookup"><span data-stu-id="91a3c-128">Review the details and consider how operating system configurations will be applied.</span></span>
  <span data-ttu-id="91a3c-129">![Description for the failed rule][3]</span><span class="sxs-lookup"><span data-stu-id="91a3c-129">![Description for the failed rule][3]</span></span>

  <span data-ttu-id="91a3c-130">Security Center uses Common Configuration Enumeration (CCE) to assign unique identifiers for configuration rules.</span><span class="sxs-lookup"><span data-stu-id="91a3c-130">Security Center uses Common Configuration Enumeration (CCE) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="91a3c-131">The following information is provided on this blade:</span><span class="sxs-lookup"><span data-stu-id="91a3c-131">The following information is provided on this blade:</span></span>

  - <span data-ttu-id="91a3c-132">NAME -- Name of rule</span><span class="sxs-lookup"><span data-stu-id="91a3c-132">NAME -- Name of rule</span></span>
  - <span data-ttu-id="91a3c-133">SEVERITY -- CCE severity value of critical, important, or warning</span><span class="sxs-lookup"><span data-stu-id="91a3c-133">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="91a3c-134">CCIED -- CCE unique identifier for the rule</span><span class="sxs-lookup"><span data-stu-id="91a3c-134">CCIED -- CCE unique identifier for the rule</span></span>
  - <span data-ttu-id="91a3c-135">DESCRIPTION -- Description of rule</span><span class="sxs-lookup"><span data-stu-id="91a3c-135">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="91a3c-136">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span><span class="sxs-lookup"><span data-stu-id="91a3c-136">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="91a3c-137">IMPACT -- Business impact when rule is applied</span><span class="sxs-lookup"><span data-stu-id="91a3c-137">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="91a3c-138">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against the rule</span><span class="sxs-lookup"><span data-stu-id="91a3c-138">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="91a3c-139">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against the rule</span><span class="sxs-lookup"><span data-stu-id="91a3c-139">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="91a3c-140">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against the rule</span><span class="sxs-lookup"><span data-stu-id="91a3c-140">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="91a3c-141">EVALUATION RESULT –- Result of analysis: Pass, Fail</span><span class="sxs-lookup"><span data-stu-id="91a3c-141">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="91a3c-142">See also</span><span class="sxs-lookup"><span data-stu-id="91a3c-142">See also</span></span>
<span data-ttu-id="91a3c-143">This article showed you how to implement the Security Center recommendation "Remediate OS vulnerabilities."</span><span class="sxs-lookup"><span data-stu-id="91a3c-143">This article showed you how to implement the Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="91a3c-144">You can review the set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="91a3c-144">You can review the set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="91a3c-145">Security Center uses CCE (Common Configuration Enumeration) to assign unique identifiers for configuration rules.</span><span class="sxs-lookup"><span data-stu-id="91a3c-145">Security Center uses CCE (Common Configuration Enumeration) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="91a3c-146">Visit the [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span><span class="sxs-lookup"><span data-stu-id="91a3c-146">Visit the [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="91a3c-147">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="91a3c-147">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="91a3c-148">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="91a3c-148">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="91a3c-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="91a3c-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="91a3c-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="91a3c-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="91a3c-151">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="91a3c-151">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="91a3c-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="91a3c-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="91a3c-153">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="91a3c-153">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="91a3c-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span><span class="sxs-lookup"><span data-stu-id="91a3c-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-remediate-os-vulnerabilities/vulnerability-details.png



