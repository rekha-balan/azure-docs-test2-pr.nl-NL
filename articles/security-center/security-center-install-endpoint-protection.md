---
title: Manage endpoint protection issues with Azure Security Center | Microsoft Docs
description: Learn how to manage endpoint protection issues in Azure Security Center.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/23/2017
ms.author: terrylan
ms.openlocfilehash: a3ac23f3874b85da9c0641264ca6f9c55a7b0515
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44798257"
---
# <a name="manage-endpoint-protection-issues-with-azure-security-center"></a><span data-ttu-id="dcc4f-103">Manage endpoint protection issues with Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="dcc4f-103">Manage endpoint protection issues with Azure Security Center</span></span>
<span data-ttu-id="dcc4f-104">Azure Security Center monitors the status of antimalware protection and reports this under the Endpoint protection issues blade.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-104">Azure Security Center monitors the status of antimalware protection and reports this under the Endpoint protection issues blade.</span></span> <span data-ttu-id="dcc4f-105">Security Center highlights issues, such as detected threats and insufficient protection, which can make your virtual machines (VMs) and computers vulnerable to antimalware threats.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-105">Security Center highlights issues, such as detected threats and insufficient protection, which can make your virtual machines (VMs) and computers vulnerable to antimalware threats.</span></span> <span data-ttu-id="dcc4f-106">By using the information under **Endpoint protection issues**, you can identify a plan to address any issues identified.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-106">By using the information under **Endpoint protection issues**, you can identify a plan to address any issues identified.</span></span>

<span data-ttu-id="dcc4f-107">Security Center reports the following endpoint protection issues:</span><span class="sxs-lookup"><span data-stu-id="dcc4f-107">Security Center reports the following endpoint protection issues:</span></span>

- <span data-ttu-id="dcc4f-108">Endpoint protection not installed on Azure VMs – A supported antimalware solution is not installed on these Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-108">Endpoint protection not installed on Azure VMs – A supported antimalware solution is not installed on these Azure VMs.</span></span>
- <span data-ttu-id="dcc4f-109">Endpoint protection not installed on non-Azure computers – A supported antimalware is not installed on these non-Azure computers.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-109">Endpoint protection not installed on non-Azure computers – A supported antimalware is not installed on these non-Azure computers.</span></span>
- <span data-ttu-id="dcc4f-110">Endpoint protection health:</span><span class="sxs-lookup"><span data-stu-id="dcc4f-110">Endpoint protection health:</span></span>

   - <span data-ttu-id="dcc4f-111">Signature out of date – An antimalware solution is installed on these VMs and computers, but the solution does not have the latest antimalware signatures.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-111">Signature out of date – An antimalware solution is installed on these VMs and computers, but the solution does not have the latest antimalware signatures.</span></span>
   - <span data-ttu-id="dcc4f-112">No real time protection – An antimalware solution is installed on these VMs and computers, but it is not configured for real-time protection.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-112">No real time protection – An antimalware solution is installed on these VMs and computers, but it is not configured for real-time protection.</span></span>   <span data-ttu-id="dcc4f-113">The service may be disabled or Security Center may be unable to obtain the status because the solution is not supported.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-113">The service may be disabled or Security Center may be unable to obtain the status because the solution is not supported.</span></span> <span data-ttu-id="dcc4f-114">See [partner integration](security-center-partner-integration.md) for a list of supported solutions.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-114">See [partner integration](security-center-partner-integration.md) for a list of supported solutions.</span></span>
   - <span data-ttu-id="dcc4f-115">Not reporting – An antimalware solution is installed but not reporting data.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-115">Not reporting – An antimalware solution is installed but not reporting data.</span></span>
   - <span data-ttu-id="dcc4f-116">Unknown –  An antimalware solution is installed but its status is unknown or reporting an unknown error.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-116">Unknown –  An antimalware solution is installed but its status is unknown or reporting an unknown error.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dcc4f-117">See [Integrate security solutions](security-center-partner-integration.md#integrated-azure-security-solutions) for a list of endpoint protection security solutions integrated with Security Center.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-117">See [Integrate security solutions](security-center-partner-integration.md#integrated-azure-security-solutions) for a list of endpoint protection security solutions integrated with Security Center.</span></span>
   >
   >

## <a name="implement-the-recommendation"></a><span data-ttu-id="dcc4f-118">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="dcc4f-118">Implement the recommendation</span></span>
<span data-ttu-id="dcc4f-119">Endpoint protection issues is presented as a recommendation in Security Center.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-119">Endpoint protection issues is presented as a recommendation in Security Center.</span></span>  <span data-ttu-id="dcc4f-120">If your environment is vulnerable to antimalware threats, this recommendation will be displayed under **Recommendations** and under **Compute**.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-120">If your environment is vulnerable to antimalware threats, this recommendation will be displayed under **Recommendations** and under **Compute**.</span></span> <span data-ttu-id="dcc4f-121">To see the **Endpoint protection issues dashboard**, you need to follow the Compute workflow.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-121">To see the **Endpoint protection issues dashboard**, you need to follow the Compute workflow.</span></span>

<span data-ttu-id="dcc4f-122">In this example, we will use **Compute**.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-122">In this example, we will use **Compute**.</span></span>  <span data-ttu-id="dcc4f-123">We will look at how to install antimalware on Azure VMs and on non-Azure computers.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-123">We will look at how to install antimalware on Azure VMs and on non-Azure computers.</span></span>

## <a name="install-antimalware-on-azure-vms"></a><span data-ttu-id="dcc4f-124">Install antimalware on Azure VMs</span><span class="sxs-lookup"><span data-stu-id="dcc4f-124">Install antimalware on Azure VMs</span></span>

1. <span data-ttu-id="dcc4f-125">Select **Compute** under the Security Center main menu or **Overview**.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-125">Select **Compute** under the Security Center main menu or **Overview**.</span></span>

   ![Select Compute][1]

2. <span data-ttu-id="dcc4f-127">Under **Compute**, select **Endpoint protection issues**.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-127">Under **Compute**, select **Endpoint protection issues**.</span></span> <span data-ttu-id="dcc4f-128">The **Endpoint protection issues** dashboard opens.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-128">The **Endpoint protection issues** dashboard opens.</span></span>

   ![Select Endpoint protection issues][2]

   <span data-ttu-id="dcc4f-130">The top of the dashboard provides:</span><span class="sxs-lookup"><span data-stu-id="dcc4f-130">The top of the dashboard provides:</span></span>

   - <span data-ttu-id="dcc4f-131">Installed endpoint protection providers - Lists the different providers identified by Security Center.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-131">Installed endpoint protection providers - Lists the different providers identified by Security Center.</span></span>
   - <span data-ttu-id="dcc4f-132">Installed endpoint protection health state - Shows the health state of VMs and computers that have an endpoint protection solution installed.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-132">Installed endpoint protection health state - Shows the health state of VMs and computers that have an endpoint protection solution installed.</span></span> <span data-ttu-id="dcc4f-133">The chart shows the number of VMs and computers that are healthy and the number with insufficient protection.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-133">The chart shows the number of VMs and computers that are healthy and the number with insufficient protection.</span></span>
   - <span data-ttu-id="dcc4f-134">Malware detected – Shows the number of VMs and computers where Security Center is reporting detected malware.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-134">Malware detected – Shows the number of VMs and computers where Security Center is reporting detected malware.</span></span>
   - <span data-ttu-id="dcc4f-135">Attacked computers – Shows the number of VMs and computers where Security Center is reporting attacks by malwares.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-135">Attacked computers – Shows the number of VMs and computers where Security Center is reporting attacks by malwares.</span></span>

   <span data-ttu-id="dcc4f-136">At the bottom of the dashboard there is a list of endpoint protection issues which includes the following information:</span><span class="sxs-lookup"><span data-stu-id="dcc4f-136">At the bottom of the dashboard there is a list of endpoint protection issues which includes the following information:</span></span>  

   - <span data-ttu-id="dcc4f-137">**TOTAL** -  The number of VMs and computers impacted by the issue.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-137">**TOTAL** -  The number of VMs and computers impacted by the issue.</span></span>
   - <span data-ttu-id="dcc4f-138">A bar aggregating the number of VMs and computers impacted by the issue.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-138">A bar aggregating the number of VMs and computers impacted by the issue.</span></span> <span data-ttu-id="dcc4f-139">The colors in the bar identify priority:</span><span class="sxs-lookup"><span data-stu-id="dcc4f-139">The colors in the bar identify priority:</span></span>

      - <span data-ttu-id="dcc4f-140">Red - High priority and should be addressed immediately</span><span class="sxs-lookup"><span data-stu-id="dcc4f-140">Red - High priority and should be addressed immediately</span></span>
      - <span data-ttu-id="dcc4f-141">Orange - Medium priority and should be addressed as soon as possible</span><span class="sxs-lookup"><span data-stu-id="dcc4f-141">Orange - Medium priority and should be addressed as soon as possible</span></span>

3. <span data-ttu-id="dcc4f-142">Select **Endpoint protection not installed on Azure VMs**.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-142">Select **Endpoint protection not installed on Azure VMs**.</span></span>

   ![Select Endpoint protection not installed on Azure VMs][3]

4. <span data-ttu-id="dcc4f-144">Under **Endpoint protection not installed on Azure VMs** is a list of Azure VMs that do not have antimalware installed.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-144">Under **Endpoint protection not installed on Azure VMs** is a list of Azure VMs that do not have antimalware installed.</span></span>  <span data-ttu-id="dcc4f-145">You can choose to install antimalware on all VMs in the list or select individual VMs to install antimalware on by clicking on the specific VM.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-145">You can choose to install antimalware on all VMs in the list or select individual VMs to install antimalware on by clicking on the specific VM.</span></span>
5. <span data-ttu-id="dcc4f-146">Under **Select Endpoint protection**, select the endpoint protection solution you want to use.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-146">Under **Select Endpoint protection**, select the endpoint protection solution you want to use.</span></span> <span data-ttu-id="dcc4f-147">In this example, select **Microsoft Antimalware**.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-147">In this example, select **Microsoft Antimalware**.</span></span>
6. <span data-ttu-id="dcc4f-148">Additional information about the endpoint protection solution is displayed.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-148">Additional information about the endpoint protection solution is displayed.</span></span> <span data-ttu-id="dcc4f-149">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-149">Select **Create**.</span></span>

## <a name="install-antimalware-on-non-azure-computers"></a><span data-ttu-id="dcc4f-150">Install antimalware on non-Azure computers</span><span class="sxs-lookup"><span data-stu-id="dcc4f-150">Install antimalware on non-Azure computers</span></span>

1. <span data-ttu-id="dcc4f-151">Go back to **Endpoint protection issues** and select **Endpoint protection not installed on non-Azure computers**.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-151">Go back to **Endpoint protection issues** and select **Endpoint protection not installed on non-Azure computers**.</span></span>

   ![Select Endpoint protection not installed on non-Azure computers][4]

2. <span data-ttu-id="dcc4f-153">Under **Endpoint protection not installed on non-Azure computers**, select a workspace.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-153">Under **Endpoint protection not installed on non-Azure computers**, select a workspace.</span></span> <span data-ttu-id="dcc4f-154">A Log Analytics search query filtered to the workspace opens and lists computers missing antimalware.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-154">A Log Analytics search query filtered to the workspace opens and lists computers missing antimalware.</span></span> <span data-ttu-id="dcc4f-155">Select a computer from the list for more information.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-155">Select a computer from the list for more information.</span></span>

   ![Log Analytics search][5]

<span data-ttu-id="dcc4f-157">Another search result opens with information filtered only for that computer.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-157">Another search result opens with information filtered only for that computer.</span></span>

  ![Log Analytics search][6]

> [!NOTE]
> <span data-ttu-id="dcc4f-159">We recommend that endpoint protection be provisioned for all VMs and computers to help identify and remove viruses, spyware, and other malicious software.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-159">We recommend that endpoint protection be provisioned for all VMs and computers to help identify and remove viruses, spyware, and other malicious software.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="dcc4f-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="dcc4f-160">Next steps</span></span>
<span data-ttu-id="dcc4f-161">This article showed you how to implement the Security Center recommendation "Install Endpoint Protection."</span><span class="sxs-lookup"><span data-stu-id="dcc4f-161">This article showed you how to implement the Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="dcc4f-162">To learn more about enabling Microsoft Antimalware in Azure, see the following document:</span><span class="sxs-lookup"><span data-stu-id="dcc4f-162">To learn more about enabling Microsoft Antimalware in Azure, see the following document:</span></span>

* <span data-ttu-id="dcc4f-163">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how to deploy Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-163">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how to deploy Microsoft Antimalware.</span></span>

<span data-ttu-id="dcc4f-164">To learn more about Security Center, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="dcc4f-164">To learn more about Security Center, see the following documents:</span></span>

* <span data-ttu-id="dcc4f-165">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-165">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="dcc4f-166">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-166">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="dcc4f-167">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-167">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="dcc4f-168">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-168">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="dcc4f-169">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-169">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="dcc4f-170">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-170">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="dcc4f-171">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span><span class="sxs-lookup"><span data-stu-id="dcc4f-171">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/compute.png
[2]:./media/security-center-install-endpoint-protection/endpoint-protection-issues.png
[3]:./media/security-center-install-endpoint-protection/install-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/endpoint-protection-issues-computers.png
[5]:./media/security-center-install-endpoint-protection/log-search.png
[6]:./media/security-center-install-endpoint-protection/info-filtered-to-computer.png
