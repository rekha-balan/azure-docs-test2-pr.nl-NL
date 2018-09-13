---
title: View the monthly estimated lab cost trend in Azure DevTest Labs | Microsoft Docs
description: Learn about the Azure DevTest Labs monthly estimated cost trend chart.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: f7db633f03638acb4484c3e9193a730b5ab9a123
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555051"
---
# <a name="view-the-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="55f7b-103">View the monthly estimated lab cost trend in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="55f7b-103">View the monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="55f7b-104">The Cost Management feature of DevTest Labs helps you track the cost of your lab.</span><span class="sxs-lookup"><span data-stu-id="55f7b-104">The Cost Management feature of DevTest Labs helps you track the cost of your lab.</span></span> <span data-ttu-id="55f7b-105">This article illustrates how to use the **Monthly Estimated Cost Trend** chart to view the current calendar month's estimated cost-to-date and the projected end-of-month cost for the current calendar month.</span><span class="sxs-lookup"><span data-stu-id="55f7b-105">This article illustrates how to use the **Monthly Estimated Cost Trend** chart to view the current calendar month's estimated cost-to-date and the projected end-of-month cost for the current calendar month.</span></span> <span data-ttu-id="55f7b-106">In this article, you learn how to view the monthly estimated cost trend chart in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="55f7b-106">In this article, you learn how to view the monthly estimated cost trend chart in the Azure portal.</span></span>

## <a name="viewing-the-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="55f7b-107">Viewing the Monthly Estimated Cost Trend chart</span><span class="sxs-lookup"><span data-stu-id="55f7b-107">Viewing the Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="55f7b-108">To view the Monthly Estimated Cost Trend chart, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="55f7b-108">To view the Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="55f7b-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="55f7b-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="55f7b-110">Select **More Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="55f7b-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="55f7b-111">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="55f7b-111">From the list of labs, select the desired lab.</span></span>   
4. <span data-ttu-id="55f7b-112">On the lab's blade, select **Cost settings**.</span><span class="sxs-lookup"><span data-stu-id="55f7b-112">On the lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="55f7b-113">On the lab's **Cost settings** blade, select **Lab cost trend**.</span><span class="sxs-lookup"><span data-stu-id="55f7b-113">On the lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="55f7b-114">The following screen shot shows an example of a cost chart.</span><span class="sxs-lookup"><span data-stu-id="55f7b-114">The following screen shot shows an example of a cost chart.</span></span> 
   
    ![Cost chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="55f7b-116">The **Estimated cost** value is the current calendar month's estimated cost-to-date.</span><span class="sxs-lookup"><span data-stu-id="55f7b-116">The **Estimated cost** value is the current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="55f7b-117">The **Projected cost** is the estimated cost for the entire current calendar month, calculated using the lab cost for the previous five days.</span><span class="sxs-lookup"><span data-stu-id="55f7b-117">The **Projected cost** is the estimated cost for the entire current calendar month, calculated using the lab cost for the previous five days.</span></span>

<span data-ttu-id="55f7b-118">The cost amounts are rounded up to the next whole number.</span><span class="sxs-lookup"><span data-stu-id="55f7b-118">The cost amounts are rounded up to the next whole number.</span></span> <span data-ttu-id="55f7b-119">For example:</span><span class="sxs-lookup"><span data-stu-id="55f7b-119">For example:</span></span> 

* <span data-ttu-id="55f7b-120">5.01 rounds up to 6</span><span class="sxs-lookup"><span data-stu-id="55f7b-120">5.01 rounds up to 6</span></span> 
* <span data-ttu-id="55f7b-121">5.50 rounds up to 6</span><span class="sxs-lookup"><span data-stu-id="55f7b-121">5.50 rounds up to 6</span></span>
* <span data-ttu-id="55f7b-122">5.99 rounds up to 6</span><span class="sxs-lookup"><span data-stu-id="55f7b-122">5.99 rounds up to 6</span></span>

<span data-ttu-id="55f7b-123">As it states above the chart, the costs you see in the chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span><span class="sxs-lookup"><span data-stu-id="55f7b-123">As it states above the chart, the costs you see in the chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="55f7b-124">Additionally, the following are *not* included in the cost calculation:</span><span class="sxs-lookup"><span data-stu-id="55f7b-124">Additionally, the following are *not* included in the cost calculation:</span></span>

* <span data-ttu-id="55f7b-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses the [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) to calculate the lab cost, which does not support CSP or Dreamspark subscriptions.</span><span class="sxs-lookup"><span data-stu-id="55f7b-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses the [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) to calculate the lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="55f7b-126">Your offer rates.</span><span class="sxs-lookup"><span data-stu-id="55f7b-126">Your offer rates.</span></span> <span data-ttu-id="55f7b-127">Currently, we are not able to use your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span><span class="sxs-lookup"><span data-stu-id="55f7b-127">Currently, we are not able to use your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="55f7b-128">We are using Pay-As-You-Go rates.</span><span class="sxs-lookup"><span data-stu-id="55f7b-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="55f7b-129">Your taxes</span><span class="sxs-lookup"><span data-stu-id="55f7b-129">Your taxes</span></span>
* <span data-ttu-id="55f7b-130">Your discounts</span><span class="sxs-lookup"><span data-stu-id="55f7b-130">Your discounts</span></span>
* <span data-ttu-id="55f7b-131">Your billing currency.</span><span class="sxs-lookup"><span data-stu-id="55f7b-131">Your billing currency.</span></span> <span data-ttu-id="55f7b-132">Currently, the lab cost is displayed only in USD currency.</span><span class="sxs-lookup"><span data-stu-id="55f7b-132">Currently, the lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="55f7b-133">Related blog posts</span><span class="sxs-lookup"><span data-stu-id="55f7b-133">Related blog posts</span></span>
* [<span data-ttu-id="55f7b-134">Two more things to keep your cost on track in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="55f7b-134">Two more things to keep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="55f7b-135">Why Cost Thresholds?</span><span class="sxs-lookup"><span data-stu-id="55f7b-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="55f7b-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="55f7b-136">Next steps</span></span>
<span data-ttu-id="55f7b-137">Here are some things to try next:</span><span class="sxs-lookup"><span data-stu-id="55f7b-137">Here are some things to try next:</span></span>

* <span data-ttu-id="55f7b-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how to set the various policies used to govern how your lab and its VMs are used.</span><span class="sxs-lookup"><span data-stu-id="55f7b-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how to set the various policies used to govern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="55f7b-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span><span class="sxs-lookup"><span data-stu-id="55f7b-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="55f7b-140">This article illustrates how to create a custom image from a VHD file.</span><span class="sxs-lookup"><span data-stu-id="55f7b-140">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="55f7b-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span><span class="sxs-lookup"><span data-stu-id="55f7b-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="55f7b-142">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span><span class="sxs-lookup"><span data-stu-id="55f7b-142">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="55f7b-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span><span class="sxs-lookup"><span data-stu-id="55f7b-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>


