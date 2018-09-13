---
title: Apply system updates in Azure Security Center | Microsoft Docs
description: This document shows you how to implement the Azure Security Center recommendations **Apply system updates** and **Reboot after system updates**.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/11/2017
ms.author: terrylan
ms.openlocfilehash: 5f6747629139e85f1ae50364da807636937a464a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803951"
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="086c0-103">Apply system updates in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="086c0-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="086c0-104">Azure Security Center monitors daily Windows and Linux virtual machines (VMs) and computers for missing operating system updates.</span><span class="sxs-lookup"><span data-stu-id="086c0-104">Azure Security Center monitors daily Windows and Linux virtual machines (VMs) and computers for missing operating system updates.</span></span> <span data-ttu-id="086c0-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows computer.</span><span class="sxs-lookup"><span data-stu-id="086c0-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows computer.</span></span> <span data-ttu-id="086c0-106">Security Center also checks for the latest updates in Linux systems.</span><span class="sxs-lookup"><span data-stu-id="086c0-106">Security Center also checks for the latest updates in Linux systems.</span></span> <span data-ttu-id="086c0-107">If your VM or computer is missing a system update, Security Center will recommend that you apply system updates.</span><span class="sxs-lookup"><span data-stu-id="086c0-107">If your VM or computer is missing a system update, Security Center will recommend that you apply system updates.</span></span>

## <a name="implement-the-recommendation"></a><span data-ttu-id="086c0-108">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="086c0-108">Implement the recommendation</span></span>
<span data-ttu-id="086c0-109">Apply system updates is presented as a recommendation in Security Center.</span><span class="sxs-lookup"><span data-stu-id="086c0-109">Apply system updates is presented as a recommendation in Security Center.</span></span> <span data-ttu-id="086c0-110">If your VM or computer is missing a system update, this recommendation will be displayed under **Recommendations** and under **Compute**.</span><span class="sxs-lookup"><span data-stu-id="086c0-110">If your VM or computer is missing a system update, this recommendation will be displayed under **Recommendations** and under **Compute**.</span></span>  <span data-ttu-id="086c0-111">Selecting the recommendation opens the **Apply system updates** dashboard.</span><span class="sxs-lookup"><span data-stu-id="086c0-111">Selecting the recommendation opens the **Apply system updates** dashboard.</span></span>

<span data-ttu-id="086c0-112">In this example, we will use **Compute**.</span><span class="sxs-lookup"><span data-stu-id="086c0-112">In this example, we will use **Compute**.</span></span>

1. <span data-ttu-id="086c0-113">Select **Compute** under the Security Center main menu.</span><span class="sxs-lookup"><span data-stu-id="086c0-113">Select **Compute** under the Security Center main menu.</span></span>

   ![Select Compute][1]

2. <span data-ttu-id="086c0-115">Under **Compute**, select **Missing system updates**.</span><span class="sxs-lookup"><span data-stu-id="086c0-115">Under **Compute**, select **Missing system updates**.</span></span> <span data-ttu-id="086c0-116">The **Apply system updates** dashboard opens.</span><span class="sxs-lookup"><span data-stu-id="086c0-116">The **Apply system updates** dashboard opens.</span></span>

   ![Apply system updates dashboard][2]

   <span data-ttu-id="086c0-118">The top of the dashboard provides:</span><span class="sxs-lookup"><span data-stu-id="086c0-118">The top of the dashboard provides:</span></span>

    - <span data-ttu-id="086c0-119">The total number of Windows and Linux VMs and computers missing system updates.</span><span class="sxs-lookup"><span data-stu-id="086c0-119">The total number of Windows and Linux VMs and computers missing system updates.</span></span>
    - <span data-ttu-id="086c0-120">The total number of critical updates missing across your VMs and computers.</span><span class="sxs-lookup"><span data-stu-id="086c0-120">The total number of critical updates missing across your VMs and computers.</span></span>
    - <span data-ttu-id="086c0-121">The total number of security updates missing across your VMs and computers.</span><span class="sxs-lookup"><span data-stu-id="086c0-121">The total number of security updates missing across your VMs and computers.</span></span>

  <span data-ttu-id="086c0-122">The bottom of the dashboard lists all missing updates across your VMs and computers, and the severity of the missing update.</span><span class="sxs-lookup"><span data-stu-id="086c0-122">The bottom of the dashboard lists all missing updates across your VMs and computers, and the severity of the missing update.</span></span>  <span data-ttu-id="086c0-123">The list includes:</span><span class="sxs-lookup"><span data-stu-id="086c0-123">The list includes:</span></span>

    - <span data-ttu-id="086c0-124">NAME: Name of the missing update.</span><span class="sxs-lookup"><span data-stu-id="086c0-124">NAME: Name of the missing update.</span></span>
    - <span data-ttu-id="086c0-125">NO.</span><span class="sxs-lookup"><span data-stu-id="086c0-125">NO.</span></span> <span data-ttu-id="086c0-126">OF VMs & COMPUTERS: Total number of VMs and computers that are missing this update.</span><span class="sxs-lookup"><span data-stu-id="086c0-126">OF VMs & COMPUTERS: Total number of VMs and computers that are missing this update.</span></span>
    - <span data-ttu-id="086c0-127">STATE: The current state of the recommendation:</span><span class="sxs-lookup"><span data-stu-id="086c0-127">STATE: The current state of the recommendation:</span></span>

      - <span data-ttu-id="086c0-128">Open: The recommendation has not been addressed yet.</span><span class="sxs-lookup"><span data-stu-id="086c0-128">Open: The recommendation has not been addressed yet.</span></span>
      - <span data-ttu-id="086c0-129">In Progress: The recommendation is currently being applied to those resources, and no action is required by you.</span><span class="sxs-lookup"><span data-stu-id="086c0-129">In Progress: The recommendation is currently being applied to those resources, and no action is required by you.</span></span>
      - <span data-ttu-id="086c0-130">Resolved: The recommendation was already finished.</span><span class="sxs-lookup"><span data-stu-id="086c0-130">Resolved: The recommendation was already finished.</span></span> <span data-ttu-id="086c0-131">(When the issue has been resolved, the entry is dimmed).</span><span class="sxs-lookup"><span data-stu-id="086c0-131">(When the issue has been resolved, the entry is dimmed).</span></span>

    - <span data-ttu-id="086c0-132">SEVERITY: Describes the severity of that particular recommendation:</span><span class="sxs-lookup"><span data-stu-id="086c0-132">SEVERITY: Describes the severity of that particular recommendation:</span></span>

      - <span data-ttu-id="086c0-133">High: A vulnerability exists with a meaningful resource (application, virtual machine, or network security group) and requires attention.</span><span class="sxs-lookup"><span data-stu-id="086c0-133">High: A vulnerability exists with a meaningful resource (application, virtual machine, or network security group) and requires attention.</span></span>
      - <span data-ttu-id="086c0-134">Medium: Non-critical or additional steps are required to complete a process or eliminate a vulnerability.</span><span class="sxs-lookup"><span data-stu-id="086c0-134">Medium: Non-critical or additional steps are required to complete a process or eliminate a vulnerability.</span></span>
      - <span data-ttu-id="086c0-135">Low: A vulnerability should be addressed but does not require immediate attention.</span><span class="sxs-lookup"><span data-stu-id="086c0-135">Low: A vulnerability should be addressed but does not require immediate attention.</span></span> <span data-ttu-id="086c0-136">(By default, low recommendations are not presented, but you can filter on low recommendations if you want to view them.)</span><span class="sxs-lookup"><span data-stu-id="086c0-136">(By default, low recommendations are not presented, but you can filter on low recommendations if you want to view them.)</span></span>

3. <span data-ttu-id="086c0-137">Select a missing update in the list to view details.</span><span class="sxs-lookup"><span data-stu-id="086c0-137">Select a missing update in the list to view details.</span></span>

   ![Missing security update][3]

4. <span data-ttu-id="086c0-139">Select the **Search** icon in the top ribbon.</span><span class="sxs-lookup"><span data-stu-id="086c0-139">Select the **Search** icon in the top ribbon.</span></span>  <span data-ttu-id="086c0-140">A Log Analytics search query opens filtered to the computers missing the update.</span><span class="sxs-lookup"><span data-stu-id="086c0-140">A Log Analytics search query opens filtered to the computers missing the update.</span></span>

   ![Log Analytics search][4]

5. <span data-ttu-id="086c0-142">Select a computer from the list for more information.</span><span class="sxs-lookup"><span data-stu-id="086c0-142">Select a computer from the list for more information.</span></span> <span data-ttu-id="086c0-143">Another search result opens with information filtered only for that computer.</span><span class="sxs-lookup"><span data-stu-id="086c0-143">Another search result opens with information filtered only for that computer.</span></span>

    ![Log Analytics search][5]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="086c0-145">Reboot after system updates</span><span class="sxs-lookup"><span data-stu-id="086c0-145">Reboot after system updates</span></span>
1. <span data-ttu-id="086c0-146">Return to the **Recommendations** blade.</span><span class="sxs-lookup"><span data-stu-id="086c0-146">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="086c0-147">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span><span class="sxs-lookup"><span data-stu-id="086c0-147">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="086c0-148">This entry lets you know that you need to reboot the VM to complete the process of applying system updates.</span><span class="sxs-lookup"><span data-stu-id="086c0-148">This entry lets you know that you need to reboot the VM to complete the process of applying system updates.</span></span>

   ![Reboot after system updates][6]
2. <span data-ttu-id="086c0-150">Select **Reboot after system updates**.</span><span class="sxs-lookup"><span data-stu-id="086c0-150">Select **Reboot after system updates**.</span></span> <span data-ttu-id="086c0-151">This opens **A restart is pending to complete system updates** blade displaying a list of VMs that you need to restart to complete the apply system updates process.</span><span class="sxs-lookup"><span data-stu-id="086c0-151">This opens **A restart is pending to complete system updates** blade displaying a list of VMs that you need to restart to complete the apply system updates process.</span></span>

   ![Restart pending][7]

<span data-ttu-id="086c0-153">Restart the VM from Azure to complete the process.</span><span class="sxs-lookup"><span data-stu-id="086c0-153">Restart the VM from Azure to complete the process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="086c0-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="086c0-154">Next steps</span></span>
<span data-ttu-id="086c0-155">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="086c0-155">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="086c0-156">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="086c0-156">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="086c0-157">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="086c0-157">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="086c0-158">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="086c0-158">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="086c0-159">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="086c0-159">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="086c0-160">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="086c0-160">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="086c0-161">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="086c0-161">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="086c0-162">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span><span class="sxs-lookup"><span data-stu-id="086c0-162">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/missing-system-updates.png
[2]:./media/security-center-apply-system-updates/apply-system-updates.png
[3]: ./media/security-center-apply-system-updates/detail-on-missing-update.png
[4]: ./media/security-center-apply-system-updates/log-search.png
[5]: ./media/security-center-apply-system-updates/search-details.png
[6]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[7]: ./media/security-center-apply-system-updates/restart-pending.png
