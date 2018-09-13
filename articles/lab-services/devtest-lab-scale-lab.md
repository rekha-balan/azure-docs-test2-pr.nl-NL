---
title: Scale quotas and limits in your lab in Azure DevTest Labs | Microsoft Docs
description: Learn how to scale a lab in Azure DevTest Labs
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: 5a179c0c6b777ee6b2afdd0f2e9267d247665d8d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967640"
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="9b78f-103">Scale quotas and limits in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="9b78f-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="9b78f-104">As you work in DevTest Labs, you might notice that there are certain default limits to some Azure resources, which can affect the DevTest Labs service.</span><span class="sxs-lookup"><span data-stu-id="9b78f-104">As you work in DevTest Labs, you might notice that there are certain default limits to some Azure resources, which can affect the DevTest Labs service.</span></span> <span data-ttu-id="9b78f-105">These limits are referred to as **quotas**.</span><span class="sxs-lookup"><span data-stu-id="9b78f-105">These limits are referred to as **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="9b78f-106">The DevTest Labs service doesn't impose any quotas.</span><span class="sxs-lookup"><span data-stu-id="9b78f-106">The DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="9b78f-107">Any quotas you might encounter are default constraints of the overall Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="9b78f-107">Any quotas you might encounter are default constraints of the overall Azure subscription.</span></span>

<span data-ttu-id="9b78f-108">You can use each Azure resource until you reach its quota.</span><span class="sxs-lookup"><span data-stu-id="9b78f-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="9b78f-109">Each subscription has separate quotas and usage is tracked per subscription.</span><span class="sxs-lookup"><span data-stu-id="9b78f-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="9b78f-110">For example, each subscription has a default quota of 20 cores.</span><span class="sxs-lookup"><span data-stu-id="9b78f-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="9b78f-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span><span class="sxs-lookup"><span data-stu-id="9b78f-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="9b78f-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of the most common quotas for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="9b78f-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of the most common quotas for Azure resources.</span></span> <span data-ttu-id="9b78f-113">The resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span><span class="sxs-lookup"><span data-stu-id="9b78f-113">The resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="9b78f-114">View your usage and quotas</span><span class="sxs-lookup"><span data-stu-id="9b78f-114">View your usage and quotas</span></span>
<span data-ttu-id="9b78f-115">These steps show you how to view the current quotas in your subscription for specific Azure resources, and to see what percentage of each quota you have used.</span><span class="sxs-lookup"><span data-stu-id="9b78f-115">These steps show you how to view the current quotas in your subscription for specific Azure resources, and to see what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="9b78f-116">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="9b78f-116">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="9b78f-117">Select **More Services**, and then select **Billing** from the list.</span><span class="sxs-lookup"><span data-stu-id="9b78f-117">Select **More Services**, and then select **Billing** from the list.</span></span>
1. <span data-ttu-id="9b78f-118">In the Billing blade, select a subscription.</span><span class="sxs-lookup"><span data-stu-id="9b78f-118">In the Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="9b78f-119">Select **Usage + quotas**.</span><span class="sxs-lookup"><span data-stu-id="9b78f-119">Select **Usage + quotas**.</span></span>

   ![Usage and quotas button](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="9b78f-121">The Usage + quotas blade appears, listing different resources available in that subscription and the percentage of the quota that is being used per resource.</span><span class="sxs-lookup"><span data-stu-id="9b78f-121">The Usage + quotas blade appears, listing different resources available in that subscription and the percentage of the quota that is being used per resource.</span></span>

   ![Quotas and usage](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="9b78f-123">Requesting more resources in your subscription</span><span class="sxs-lookup"><span data-stu-id="9b78f-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="9b78f-124">If you reach a quota cap, the default limit of a resource in a subscription can be increased up to a maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span><span class="sxs-lookup"><span data-stu-id="9b78f-124">If you reach a quota cap, the default limit of a resource in a subscription can be increased up to a maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="9b78f-125">These steps show you how to request a quota increase through the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="9b78f-125">These steps show you how to request a quota increase through the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="9b78f-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span><span class="sxs-lookup"><span data-stu-id="9b78f-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="9b78f-127">In the Usage + quotas blade, select the **Request Increase** button.</span><span class="sxs-lookup"><span data-stu-id="9b78f-127">In the Usage + quotas blade, select the **Request Increase** button.</span></span>

   ![Request increase button](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="9b78f-129">To complete and submit the request, fill out the required information on all three tabs of the **New support request** form.</span><span class="sxs-lookup"><span data-stu-id="9b78f-129">To complete and submit the request, fill out the required information on all three tabs of the **New support request** form.</span></span>

   ![Request increase form](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="9b78f-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support to request a quota increase.</span><span class="sxs-lookup"><span data-stu-id="9b78f-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support to request a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="9b78f-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="9b78f-132">Next steps</span></span>
* <span data-ttu-id="9b78f-133">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="9b78f-133">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
