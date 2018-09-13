---
title: Test your VM offer for the Marketplace | Microsoft Docs
description: Understand how to test your VM image for the Azure Marketplace.
services: marketplace-publishing
documentationcenter: ''
author: HannibalSII
manager: hascipio
editor: ''
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: 44fff61a197aa1e842dda1932ec5a6215ff8e113
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563785"
---
# <a name="test-your-vm-offer-for-the-azure-marketplace-in-staging"></a><span data-ttu-id="312f3-103">Test your VM offer for the Azure Marketplace in staging</span><span class="sxs-lookup"><span data-stu-id="312f3-103">Test your VM offer for the Azure Marketplace in staging</span></span>
<span data-ttu-id="312f3-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it to the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="312f3-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it to the Marketplace.</span></span> <span data-ttu-id="312f3-105">The SKU appears in staging just as it would to a customer who has deployed it.</span><span class="sxs-lookup"><span data-stu-id="312f3-105">The SKU appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="312f3-106">Your VM image must be certified to be pushed to staging.</span><span class="sxs-lookup"><span data-stu-id="312f3-106">Your VM image must be certified to be pushed to staging.</span></span>

## <a name="step-1-push-your-offer-to-staging"></a><span data-ttu-id="312f3-107">Step 1: Push your offer to staging</span><span class="sxs-lookup"><span data-stu-id="312f3-107">Step 1: Push your offer to staging</span></span>
1. <span data-ttu-id="312f3-108">On the **Publish** tab, click **Push to Staging**.</span><span class="sxs-lookup"><span data-stu-id="312f3-108">On the **Publish** tab, click **Push to Staging**.</span></span>
   
    ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="312f3-110">If the Publishing Portal notifies you of any errors, correct them.</span><span class="sxs-lookup"><span data-stu-id="312f3-110">If the Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="312f3-111">In the **Who can access your staged offer?** dialog box, enter the list of Azure subscriptions that you will use to preview your offer in the [Azure preview portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="312f3-111">In the **Who can access your staged offer?** dialog box, enter the list of Azure subscriptions that you will use to preview your offer in the [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="312f3-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span><span class="sxs-lookup"><span data-stu-id="312f3-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="312f3-113">In case of Virtual Machines, when you click on the button **PUSH TO STAGING**, the following steps are performed behind the scene.</span><span class="sxs-lookup"><span data-stu-id="312f3-113">In case of Virtual Machines, when you click on the button **PUSH TO STAGING**, the following steps are performed behind the scene.</span></span> <span data-ttu-id="312f3-114">You will be able to view the progress of each step under the PUBLISH tab in the Publishing portal.</span><span class="sxs-lookup"><span data-stu-id="312f3-114">You will be able to view the progress of each step under the PUBLISH tab in the Publishing portal.</span></span> <span data-ttu-id="312f3-115">You must check this page at regular interval (until the status shows STAGED) for any failure information which need correction from your end.</span><span class="sxs-lookup"><span data-stu-id="312f3-115">You must check this page at regular interval (until the status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="312f3-116">At first your staging request goes to the certification team who validate the vhd.</span><span class="sxs-lookup"><span data-stu-id="312f3-116">At first your staging request goes to the certification team who validate the vhd.</span></span> <span data-ttu-id="312f3-117">However, if your request has got only marketing change, then the certification step is skipped.</span><span class="sxs-lookup"><span data-stu-id="312f3-117">However, if your request has got only marketing change, then the certification step is skipped.</span></span>
    > - <span data-ttu-id="312f3-118">Once the certification is complete, replication of the offer start across all the Azure datacenters.</span><span class="sxs-lookup"><span data-stu-id="312f3-118">Once the certification is complete, replication of the offer start across all the Azure datacenters.</span></span> <span data-ttu-id="312f3-119">It generally takes 24-48hours for the replication to complete but may take up to a week depending on the size of the vhd.</span><span class="sxs-lookup"><span data-stu-id="312f3-119">It generally takes 24-48hours for the replication to complete but may take up to a week depending on the size of the vhd.</span></span> <span data-ttu-id="312f3-120">However, if your request has got only marketing change, then the replication is faster.</span><span class="sxs-lookup"><span data-stu-id="312f3-120">However, if your request has got only marketing change, then the replication is faster.</span></span>
    > - <span data-ttu-id="312f3-121">When the replication is complete, then the offer will be available in the [Azure portal](http:/portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="312f3-121">When the replication is complete, then the offer will be available in the [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="312f3-122">At that time the status become STAGED in the Publishing portal.</span><span class="sxs-lookup"><span data-stu-id="312f3-122">At that time the status become STAGED in the Publishing portal.</span></span> <span data-ttu-id="312f3-123">A staged offer is visible in the [Azure portal](http:/portal.azure.com) only using the email id(s) associated with the subscription with which the offer is staged.</span><span class="sxs-lookup"><span data-stu-id="312f3-123">A staged offer is visible in the [Azure portal](http:/portal.azure.com) only using the email id(s) associated with the subscription with which the offer is staged.</span></span>

1. <span data-ttu-id="312f3-124">Sign in to the [Azure preview portal](https://portal.azure.com) by using one of the Azure subscriptions listed in the previous step.</span><span class="sxs-lookup"><span data-stu-id="312f3-124">Sign in to the [Azure preview portal](https://portal.azure.com) by using one of the Azure subscriptions listed in the previous step.</span></span>
2. <span data-ttu-id="312f3-125">Find your offer and validate your VM image points:</span><span class="sxs-lookup"><span data-stu-id="312f3-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="312f3-126">Make sure that marketing content shows up correctly in the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="312f3-126">Make sure that marketing content shows up correctly in the Marketplace.</span></span>
   * <span data-ttu-id="312f3-127">End-to-end deployment of the VM image.</span><span class="sxs-lookup"><span data-stu-id="312f3-127">End-to-end deployment of the VM image.</span></span>
     
      ![img-map-portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="312f3-129">Your offer will remain in staging until you notify Microsoft via the Publishing Portal [**Publish** tab > click on the button **"Request Approval to Push to Production"**] that you are ready to push to production.</span><span class="sxs-lookup"><span data-stu-id="312f3-129">Your offer will remain in staging until you notify Microsoft via the Publishing Portal [**Publish** tab > click on the button **"Request Approval to Push to Production"**] that you are ready to push to production.</span></span> <span data-ttu-id="312f3-130">This is an ideal time to have all members of your team check over everything in preparation for your offer going listed.</span><span class="sxs-lookup"><span data-stu-id="312f3-130">This is an ideal time to have all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="312f3-131">The staging platform is designed for testing the offer in a preview mode by the publisher.</span><span class="sxs-lookup"><span data-stu-id="312f3-131">The staging platform is designed for testing the offer in a preview mode by the publisher.</span></span> <span data-ttu-id="312f3-132">We strongly discourage using this platofrm for commerical purposes.</span><span class="sxs-lookup"><span data-stu-id="312f3-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="312f3-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="312f3-133">Next steps</span></span>
<span data-ttu-id="312f3-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed to the final publishing phase, **Step 4**: [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="312f3-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed to the final publishing phase, **Step 4**: [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="312f3-135">See also</span><span class="sxs-lookup"><span data-stu-id="312f3-135">See also</span></span>
* [<span data-ttu-id="312f3-136">Getting started: How to publish an offer to the Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="312f3-136">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)



