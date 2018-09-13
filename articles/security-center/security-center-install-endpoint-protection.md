---
title: Install Endpoint Protection in Azure Security Center | Microsoft Docs
description: This document shows you how to implement the Azure Security Center recommendation **Install Endpoint Protection**.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/23/2016
ms.author: terrylan
ms.openlocfilehash: a93c6d4bb4638803913d9dfba39cfba382e71d50
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549210"
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="c2527-103">Install Endpoint Protection in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="c2527-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="c2527-104">Azure Security Center will recommend that you provision an antimalware program to your Azure virtual machines (VMs) if antimalware is not already enabled.</span><span class="sxs-lookup"><span data-stu-id="c2527-104">Azure Security Center will recommend that you provision an antimalware program to your Azure virtual machines (VMs) if antimalware is not already enabled.</span></span> <span data-ttu-id="c2527-105">This recommendation applies to Windows VMs only.</span><span class="sxs-lookup"><span data-stu-id="c2527-105">This recommendation applies to Windows VMs only.</span></span> <span data-ttu-id="c2527-106">Presently, this recommendation checks for the presence of either Windows Defender or TrendMicro Deep Security.</span><span class="sxs-lookup"><span data-stu-id="c2527-106">Presently, this recommendation checks for the presence of either Windows Defender or TrendMicro Deep Security.</span></span> <span data-ttu-id="c2527-107">Additional endpoint protection solutions are planned to be added in the future.</span><span class="sxs-lookup"><span data-stu-id="c2527-107">Additional endpoint protection solutions are planned to be added in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="c2527-108">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="c2527-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="c2527-109">This is not a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="c2527-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="c2527-110">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="c2527-110">Implement the recommendation</span></span>
1. <span data-ttu-id="c2527-111">In the **Recommendations** blade, select **Install Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="c2527-111">In the **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="c2527-112">![Select Install Endpoint Protection][1]</span><span class="sxs-lookup"><span data-stu-id="c2527-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="c2527-113">The **Install Endpoint Protection** blade opens displaying a list of VMs without antimalware enabled.</span><span class="sxs-lookup"><span data-stu-id="c2527-113">The **Install Endpoint Protection** blade opens displaying a list of VMs without antimalware enabled.</span></span> <span data-ttu-id="c2527-114">Select from the list the VMs that you want to install antimalware on and click **Install on VMs**.</span><span class="sxs-lookup"><span data-stu-id="c2527-114">Select from the list the VMs that you want to install antimalware on and click **Install on VMs**.</span></span>
   <span data-ttu-id="c2527-115">![Select VMs to install antimalware on][2]</span><span class="sxs-lookup"><span data-stu-id="c2527-115">![Select VMs to install antimalware on][2]</span></span>
3. <span data-ttu-id="c2527-116">The **Select Endpoint Protection** blade opens to allow you to select the antimalware solution you want to use.</span><span class="sxs-lookup"><span data-stu-id="c2527-116">The **Select Endpoint Protection** blade opens to allow you to select the antimalware solution you want to use.</span></span> <span data-ttu-id="c2527-117">In this example, let's select **Microsoft Antimalware**.</span><span class="sxs-lookup"><span data-stu-id="c2527-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="c2527-118">![Select Endpoint Protection][3]</span><span class="sxs-lookup"><span data-stu-id="c2527-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="c2527-119">Additional information about the antimalware solution is displayed.</span><span class="sxs-lookup"><span data-stu-id="c2527-119">Additional information about the antimalware solution is displayed.</span></span> <span data-ttu-id="c2527-120">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="c2527-120">Select **Create**.</span></span>
   <span data-ttu-id="c2527-121">![Create antimalware solution][4]</span><span class="sxs-lookup"><span data-stu-id="c2527-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="c2527-122">Enter the required configuration settings on the **Add Extension** blade, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="c2527-122">Enter the required configuration settings on the **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="c2527-123">To learn more about the configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span><span class="sxs-lookup"><span data-stu-id="c2527-123">To learn more about the configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="c2527-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on the selected VMs.</span><span class="sxs-lookup"><span data-stu-id="c2527-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on the selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="c2527-125">See also</span><span class="sxs-lookup"><span data-stu-id="c2527-125">See also</span></span>
<span data-ttu-id="c2527-126">This article showed you how to implement the Security Center recommendation "Install Endpoint Protection."</span><span class="sxs-lookup"><span data-stu-id="c2527-126">This article showed you how to implement the Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="c2527-127">To learn more about enabling an antimalware program in Azure, see the following:</span><span class="sxs-lookup"><span data-stu-id="c2527-127">To learn more about enabling an antimalware program in Azure, see the following:</span></span>

* <span data-ttu-id="c2527-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how to deploy Microsoft antimalware.</span><span class="sxs-lookup"><span data-stu-id="c2527-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how to deploy Microsoft antimalware.</span></span>

<span data-ttu-id="c2527-129">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="c2527-129">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="c2527-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span><span class="sxs-lookup"><span data-stu-id="c2527-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="c2527-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="c2527-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="c2527-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="c2527-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="c2527-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="c2527-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="c2527-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="c2527-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="c2527-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="c2527-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="c2527-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span><span class="sxs-lookup"><span data-stu-id="c2527-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-install-endpoint-protection/create-antimalware-solution.png




