---
title: Update OS version in Azure Security Center | Microsoft Docs
description: This article shows you how to implement the Azure Security Center recommendation **Update OS version**.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: aa372492-ecdb-4368-8fdd-d8ed31e216ee
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 164160499206985047886c337fc996b28719d930
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662999"
---
# <a name="update-os-version-in-azure-security-center"></a><span data-ttu-id="46a2a-103">Update OS version in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="46a2a-103">Update OS version in Azure Security Center</span></span>
<span data-ttu-id="46a2a-104">For virtual machines (VMs) in cloud services, Azure Security Center will recommend that the operating system (OS) be updated if there is a more recent version available.</span><span class="sxs-lookup"><span data-stu-id="46a2a-104">For virtual machines (VMs) in cloud services, Azure Security Center will recommend that the operating system (OS) be updated if there is a more recent version available.</span></span>  <span data-ttu-id="46a2a-105">Only cloud services web and worker roles running in production slots are monitored.</span><span class="sxs-lookup"><span data-stu-id="46a2a-105">Only cloud services web and worker roles running in production slots are monitored.</span></span>

> [!NOTE]
> <span data-ttu-id="46a2a-106">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="46a2a-106">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="46a2a-107">This is not a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="46a2a-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-the-recommendation"></a><span data-ttu-id="46a2a-108">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="46a2a-108">Implement the recommendation</span></span>
1. <span data-ttu-id="46a2a-109">In the **Recommendations** blade, select **Update OS version**.</span><span class="sxs-lookup"><span data-stu-id="46a2a-109">In the **Recommendations** blade, select **Update OS version**.</span></span>
   <span data-ttu-id="46a2a-110">![Update OS version][1]</span><span class="sxs-lookup"><span data-stu-id="46a2a-110">![Update OS version][1]</span></span>
2. <span data-ttu-id="46a2a-111">This opens the blade **Update OS version**.</span><span class="sxs-lookup"><span data-stu-id="46a2a-111">This opens the blade **Update OS version**.</span></span> <span data-ttu-id="46a2a-112">Follow the steps in this blade to update the OS version.</span><span class="sxs-lookup"><span data-stu-id="46a2a-112">Follow the steps in this blade to update the OS version.</span></span>

## <a name="see-also"></a><span data-ttu-id="46a2a-113">See also</span><span class="sxs-lookup"><span data-stu-id="46a2a-113">See also</span></span>
<span data-ttu-id="46a2a-114">This article showed you how to implement the Security Center recommendation "Update OS version."</span><span class="sxs-lookup"><span data-stu-id="46a2a-114">This article showed you how to implement the Security Center recommendation "Update OS version."</span></span> <span data-ttu-id="46a2a-115">To learn more about cloud services and updating the OS version for a cloud service, see:</span><span class="sxs-lookup"><span data-stu-id="46a2a-115">To learn more about cloud services and updating the OS version for a cloud service, see:</span></span>

* [<span data-ttu-id="46a2a-116">Cloud Services overview</span><span class="sxs-lookup"><span data-stu-id="46a2a-116">Cloud Services overview</span></span>](../cloud-services/cloud-services-choose-me.md)
* [<span data-ttu-id="46a2a-117">How to update a cloud service</span><span class="sxs-lookup"><span data-stu-id="46a2a-117">How to update a cloud service</span></span>](../cloud-services/cloud-services-update-azure-service.md)
* [<span data-ttu-id="46a2a-118">How to Configure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="46a2a-118">How to Configure Cloud Services</span></span>](../cloud-services/cloud-services-how-to-configure-portal.md)

<span data-ttu-id="46a2a-119">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="46a2a-119">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="46a2a-120">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="46a2a-120">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="46a2a-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="46a2a-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="46a2a-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="46a2a-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="46a2a-123">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="46a2a-123">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="46a2a-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="46a2a-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="46a2a-125">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="46a2a-125">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="46a2a-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span><span class="sxs-lookup"><span data-stu-id="46a2a-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-update-os-version/update-os-version.png

