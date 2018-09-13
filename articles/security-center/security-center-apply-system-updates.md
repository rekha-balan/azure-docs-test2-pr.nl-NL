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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 2f93b3194a9e5aad90851b2d59e80195e03ca424
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562775"
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="4f617-103">Apply system updates in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="4f617-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="4f617-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span><span class="sxs-lookup"><span data-stu-id="4f617-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="4f617-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span><span class="sxs-lookup"><span data-stu-id="4f617-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="4f617-106">Security Center also checks for the latest updates in Linux systems.</span><span class="sxs-lookup"><span data-stu-id="4f617-106">Security Center also checks for the latest updates in Linux systems.</span></span> <span data-ttu-id="4f617-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span><span class="sxs-lookup"><span data-stu-id="4f617-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="4f617-108">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="4f617-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="4f617-109">This is not a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="4f617-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="4f617-110">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="4f617-110">Implement the recommendation</span></span>
1. <span data-ttu-id="4f617-111">In the **Recommendations** blade, select **Apply system updates**.</span><span class="sxs-lookup"><span data-stu-id="4f617-111">In the **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Apply system updates][1]
2. <span data-ttu-id="4f617-113">The **Apply system updates** blade opens displaying a list of VMs missing system updates.</span><span class="sxs-lookup"><span data-stu-id="4f617-113">The **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="4f617-114">Select a VM.</span><span class="sxs-lookup"><span data-stu-id="4f617-114">Select a VM.</span></span>

   ![Select a VM][2]
3. <span data-ttu-id="4f617-116">A blade opens displaying a list of missing updates for that VM.</span><span class="sxs-lookup"><span data-stu-id="4f617-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="4f617-117">Select a system update.</span><span class="sxs-lookup"><span data-stu-id="4f617-117">Select a system update.</span></span> <span data-ttu-id="4f617-118">In this example, let’s select KB3156016.</span><span class="sxs-lookup"><span data-stu-id="4f617-118">In this example, let’s select KB3156016.</span></span>

   ![Missing security updates][3]

4. <span data-ttu-id="4f617-120">Follow the steps in the **Security Update** blade to apply the missing update.</span><span class="sxs-lookup"><span data-stu-id="4f617-120">Follow the steps in the **Security Update** blade to apply the missing update.</span></span>

   ![Security update][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="4f617-122">Reboot after system updates</span><span class="sxs-lookup"><span data-stu-id="4f617-122">Reboot after system updates</span></span>
1. <span data-ttu-id="4f617-123">Return to the **Recommendations** blade.</span><span class="sxs-lookup"><span data-stu-id="4f617-123">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="4f617-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span><span class="sxs-lookup"><span data-stu-id="4f617-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="4f617-125">This entry lets you know that you need to reboot the VM to complete the process of applying system updates.</span><span class="sxs-lookup"><span data-stu-id="4f617-125">This entry lets you know that you need to reboot the VM to complete the process of applying system updates.</span></span>

   ![Reboot after system updates][5]
2. <span data-ttu-id="4f617-127">Select **Reboot after system updates**.</span><span class="sxs-lookup"><span data-stu-id="4f617-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="4f617-128">This opens **A restart is pending to complete system updates** blade displaying a list of VMs that you need to restart to complete the apply system updates process.</span><span class="sxs-lookup"><span data-stu-id="4f617-128">This opens **A restart is pending to complete system updates** blade displaying a list of VMs that you need to restart to complete the apply system updates process.</span></span>

   ![Restart pending][6]

<span data-ttu-id="4f617-130">Restart the VM from Azure to complete the process.</span><span class="sxs-lookup"><span data-stu-id="4f617-130">Restart the VM from Azure to complete the process.</span></span>

## <a name="see-also"></a><span data-ttu-id="4f617-131">See also</span><span class="sxs-lookup"><span data-stu-id="4f617-131">See also</span></span>
<span data-ttu-id="4f617-132">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="4f617-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="4f617-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="4f617-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="4f617-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="4f617-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="4f617-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="4f617-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="4f617-136">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="4f617-136">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="4f617-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="4f617-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="4f617-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="4f617-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="4f617-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span><span class="sxs-lookup"><span data-stu-id="4f617-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-apply-system-updates/recommendation.png
[2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-apply-system-updates/select-vm.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-apply-system-updates/missing-security-updates.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-apply-system-updates/security-update.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-apply-system-updates/restart-pending.png






