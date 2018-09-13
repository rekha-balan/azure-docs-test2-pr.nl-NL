---
title: Enable VM Agent in Azure Security Center | Microsoft Docs
description: This document shows you how to implement the Azure Security Center recommendation **Enable VM Agent**.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 34c546318f4d2baaf8f6d65b6d07f92c198a90a1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551163"
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="3652a-103">Enable VM Agent in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="3652a-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="3652a-104">The VM Agent must be installed on virtual machines (VMs) in order to [enable data collection](security-center-enable-data-collection.md).</span><span class="sxs-lookup"><span data-stu-id="3652a-104">The VM Agent must be installed on virtual machines (VMs) in order to [enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="3652a-105">Azure Security Center enables you to see which VMs require the VM Agent and will recommend that you enable the VM Agent on those VMs.</span><span class="sxs-lookup"><span data-stu-id="3652a-105">Azure Security Center enables you to see which VMs require the VM Agent and will recommend that you enable the VM Agent on those VMs.</span></span>

<span data-ttu-id="3652a-106">The VM Agent is installed by default for VMs that are deployed from the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3652a-106">The VM Agent is installed by default for VMs that are deployed from the Azure Marketplace.</span></span> <span data-ttu-id="3652a-107">The article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how to install the VM Agent.</span><span class="sxs-lookup"><span data-stu-id="3652a-107">The article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how to install the VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="3652a-108">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="3652a-108">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="3652a-109">This is not a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="3652a-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="3652a-110">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="3652a-110">Implement the recommendation</span></span>
1. <span data-ttu-id="3652a-111">In the **Recommendations blade**, select **Enable VM Agent**.</span><span class="sxs-lookup"><span data-stu-id="3652a-111">In the **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="3652a-112">![Enable VM Agent][1]</span><span class="sxs-lookup"><span data-stu-id="3652a-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="3652a-113">This opens the blade **VM Agent Is Missing Or Not Responding**.</span><span class="sxs-lookup"><span data-stu-id="3652a-113">This opens the blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="3652a-114">This blade lists the VMs that require the VM Agent.</span><span class="sxs-lookup"><span data-stu-id="3652a-114">This blade lists the VMs that require the VM Agent.</span></span> <span data-ttu-id="3652a-115">Follow the instructions on the blade to install the VM agent.</span><span class="sxs-lookup"><span data-stu-id="3652a-115">Follow the instructions on the blade to install the VM agent.</span></span>
   <span data-ttu-id="3652a-116">![VM Agent is missing][2]</span><span class="sxs-lookup"><span data-stu-id="3652a-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="3652a-117">See also</span><span class="sxs-lookup"><span data-stu-id="3652a-117">See also</span></span>
<span data-ttu-id="3652a-118">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="3652a-118">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="3652a-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="3652a-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="3652a-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="3652a-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="3652a-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="3652a-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="3652a-122">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="3652a-122">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="3652a-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="3652a-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="3652a-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="3652a-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="3652a-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span><span class="sxs-lookup"><span data-stu-id="3652a-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-vm-agent/vm-agent-is-missing.png


