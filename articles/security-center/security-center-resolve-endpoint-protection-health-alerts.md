---
title: Resolve endpoint protection health alerts in Azure Security Center| Microsoft Docs
description: This document shows you how to implement the Azure Security Center recommendation **Resolve Endpoint Protection health alerts**.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 02b11701409ba59f95f65535a26edc626fff6443
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663023"
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a><span data-ttu-id="02987-103">Resolve endpoint protection health alerts in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="02987-103">Resolve endpoint protection health alerts in Azure Security Center</span></span>
<span data-ttu-id="02987-104">Azure Security Center will recommend that you resolve detected endpoint protection health alerts.</span><span class="sxs-lookup"><span data-stu-id="02987-104">Azure Security Center will recommend that you resolve detected endpoint protection health alerts.</span></span>  <span data-ttu-id="02987-105">Security Center enables you to see which virtual machines (VMs) have endpoint protection failures and how many failures.</span><span class="sxs-lookup"><span data-stu-id="02987-105">Security Center enables you to see which virtual machines (VMs) have endpoint protection failures and how many failures.</span></span>

> [!NOTE]
> <span data-ttu-id="02987-106">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="02987-106">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="02987-107">This is not a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="02987-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-the-recommendation"></a><span data-ttu-id="02987-108">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="02987-108">Implement the recommendation</span></span>
1. <span data-ttu-id="02987-109">In the **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.</span><span class="sxs-lookup"><span data-stu-id="02987-109">In the **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.</span></span>
   <span data-ttu-id="02987-110">![Resolve endpoint protection health alerts][1]</span><span class="sxs-lookup"><span data-stu-id="02987-110">![Resolve endpoint protection health alerts][1]</span></span>
2. <span data-ttu-id="02987-111">This opens the blade **Endpoint Protection failure** which lists VMs with failures and the number of failures for each VM.</span><span class="sxs-lookup"><span data-stu-id="02987-111">This opens the blade **Endpoint Protection failure** which lists VMs with failures and the number of failures for each VM.</span></span> <span data-ttu-id="02987-112">Select a VM from the list.</span><span class="sxs-lookup"><span data-stu-id="02987-112">Select a VM from the list.</span></span>
   <span data-ttu-id="02987-113">![Endpoint protection failure][2]</span><span class="sxs-lookup"><span data-stu-id="02987-113">![Endpoint protection failure][2]</span></span>
3. <span data-ttu-id="02987-114">A **Failures List** blade opens for the selected VM, displaying a list of failures.</span><span class="sxs-lookup"><span data-stu-id="02987-114">A **Failures List** blade opens for the selected VM, displaying a list of failures.</span></span> <span data-ttu-id="02987-115">Select a failure from the list to learn more.</span><span class="sxs-lookup"><span data-stu-id="02987-115">Select a failure from the list to learn more.</span></span> <span data-ttu-id="02987-116">This opens a blade with information about the selected failure.</span><span class="sxs-lookup"><span data-stu-id="02987-116">This opens a blade with information about the selected failure.</span></span>
   <span data-ttu-id="02987-117">![Failures list][3]
   ![Failure event][4]</span><span class="sxs-lookup"><span data-stu-id="02987-117">![Failures list][3]
![Failure event][4]</span></span>

## <a name="see-also"></a><span data-ttu-id="02987-118">See also</span><span class="sxs-lookup"><span data-stu-id="02987-118">See also</span></span>
<span data-ttu-id="02987-119">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="02987-119">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="02987-120">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="02987-120">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="02987-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="02987-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="02987-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="02987-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="02987-123">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="02987-123">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="02987-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="02987-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="02987-125">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="02987-125">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="02987-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span><span class="sxs-lookup"><span data-stu-id="02987-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-resolve-endpoint-protection/failure-list.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-resolve-endpoint-protection/failure-event.png




