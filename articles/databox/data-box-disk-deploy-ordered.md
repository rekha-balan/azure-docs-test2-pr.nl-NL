---
title: Tutorial to order Microsoft Azure Data Box Disk | Microsoft Docs
description: Use this tutorial to learn how to sign up and order an Azure Data Box Disk to import data into Azure.
services: databox
documentationcenter: NA
author: alkohli
manager: twooley
editor: ''
ms.assetid: ''
ms.service: databox
ms.devlang: NA
ms.topic: tutorial
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/04/2018
ms.author: alkohli
Customer intent: As an IT admin, I need to be able to order Data Box Disk to upload on-premises data from my server onto Azure.
ms.openlocfilehash: 37130e946aad00ef4eca14b7ce7942a8e435e6cd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866054"
---
# <a name="tutorial-order-an-azure-data-box-disk-preview"></a><span data-ttu-id="52a8b-103">Tutorial: Order an Azure Data Box Disk (Preview)</span><span class="sxs-lookup"><span data-stu-id="52a8b-103">Tutorial: Order an Azure Data Box Disk (Preview)</span></span>

<span data-ttu-id="52a8b-104">Azure Data Box Disk is a hybrid cloud solution that allows you to import your on-premises data into Azure in a quick, easy, and reliable way.</span><span class="sxs-lookup"><span data-stu-id="52a8b-104">Azure Data Box Disk is a hybrid cloud solution that allows you to import your on-premises data into Azure in a quick, easy, and reliable way.</span></span> <span data-ttu-id="52a8b-105">You transfer your data to solid-state disks (SSDs) supplied by Microsoft and ship the disks back.</span><span class="sxs-lookup"><span data-stu-id="52a8b-105">You transfer your data to solid-state disks (SSDs) supplied by Microsoft and ship the disks back.</span></span> <span data-ttu-id="52a8b-106">This data is then uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="52a8b-106">This data is then uploaded to Azure.</span></span> 

<span data-ttu-id="52a8b-107">This tutorial describes how you can order an Azure Data Box Disk.</span><span class="sxs-lookup"><span data-stu-id="52a8b-107">This tutorial describes how you can order an Azure Data Box Disk.</span></span> <span data-ttu-id="52a8b-108">In this tutorial, you learn about:</span><span class="sxs-lookup"><span data-stu-id="52a8b-108">In this tutorial, you learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="52a8b-109">Sign up for Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="52a8b-109">Sign up for Data Box Disk</span></span>
> * <span data-ttu-id="52a8b-110">Order a Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="52a8b-110">Order a Data Box Disk</span></span>
> * <span data-ttu-id="52a8b-111">Track the order</span><span class="sxs-lookup"><span data-stu-id="52a8b-111">Track the order</span></span>
> * <span data-ttu-id="52a8b-112">Cancel the order</span><span class="sxs-lookup"><span data-stu-id="52a8b-112">Cancel the order</span></span>

<span data-ttu-id="52a8b-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="52a8b-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="52a8b-114">Data Box Disk is in preview.</span><span class="sxs-lookup"><span data-stu-id="52a8b-114">Data Box Disk is in preview.</span></span> <span data-ttu-id="52a8b-115">Review the [Azure terms of service for preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) before you order and deploy this solution.</span><span class="sxs-lookup"><span data-stu-id="52a8b-115">Review the [Azure terms of service for preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) before you order and deploy this solution.</span></span> 
> - <span data-ttu-id="52a8b-116">During preview, Data Box Disk can be shipped to customers in US, West and North Europe, Candana, and Australia.</span><span class="sxs-lookup"><span data-stu-id="52a8b-116">During preview, Data Box Disk can be shipped to customers in US, West and North Europe, Candana, and Australia.</span></span> <span data-ttu-id="52a8b-117">For more information, go to [Region availability](data-box-disk-overview.md#region-availability).</span><span class="sxs-lookup"><span data-stu-id="52a8b-117">For more information, go to [Region availability](data-box-disk-overview.md#region-availability).</span></span>

## <a name="sign-up"></a><span data-ttu-id="52a8b-118">Sign up</span><span class="sxs-lookup"><span data-stu-id="52a8b-118">Sign up</span></span> 

<span data-ttu-id="52a8b-119">Data Box Disk is in preview and you need to sign up for the service.</span><span class="sxs-lookup"><span data-stu-id="52a8b-119">Data Box Disk is in preview and you need to sign up for the service.</span></span> <span data-ttu-id="52a8b-120">Perform the following steps to sign up for Data Box service:</span><span class="sxs-lookup"><span data-stu-id="52a8b-120">Perform the following steps to sign up for Data Box service:</span></span>

1. <span data-ttu-id="52a8b-121">Sign into the Azure portal at: [https://aka.ms/azuredataboxfromdiskdocs](https://aka.ms/azuredataboxfromdiskdocs).</span><span class="sxs-lookup"><span data-stu-id="52a8b-121">Sign into the Azure portal at: [https://aka.ms/azuredataboxfromdiskdocs](https://aka.ms/azuredataboxfromdiskdocs).</span></span>
2. <span data-ttu-id="52a8b-122">Pick the subscription that you want to enable for the preview.</span><span class="sxs-lookup"><span data-stu-id="52a8b-122">Pick the subscription that you want to enable for the preview.</span></span> <span data-ttu-id="52a8b-123">Answer the questions regarding data size, data residence country, time-frame, and data transfer frequency.</span><span class="sxs-lookup"><span data-stu-id="52a8b-123">Answer the questions regarding data size, data residence country, time-frame, and data transfer frequency.</span></span> <span data-ttu-id="52a8b-124">Click **Sign me up!**.</span><span class="sxs-lookup"><span data-stu-id="52a8b-124">Click **Sign me up!**.</span></span>
3. <span data-ttu-id="52a8b-125">Once you are signed up and enabled for preview, you can order a Data Box Disk.</span><span class="sxs-lookup"><span data-stu-id="52a8b-125">Once you are signed up and enabled for preview, you can order a Data Box Disk.</span></span>

## <a name="order-data-box-disk"></a><span data-ttu-id="52a8b-126">Order Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="52a8b-126">Order Data Box Disk</span></span>

<span data-ttu-id="52a8b-127">Perform the following steps in the [Azure portal](https://aka.ms/azuredataboxfromdiskdocs) to order Data Box Disk.</span><span class="sxs-lookup"><span data-stu-id="52a8b-127">Perform the following steps in the [Azure portal](https://aka.ms/azuredataboxfromdiskdocs) to order Data Box Disk.</span></span>

1. <span data-ttu-id="52a8b-128">In the upper left corner of the portal, click **+ Create a resource**, and search for *Azure Data Box*.</span><span class="sxs-lookup"><span data-stu-id="52a8b-128">In the upper left corner of the portal, click **+ Create a resource**, and search for *Azure Data Box*.</span></span> <span data-ttu-id="52a8b-129">Click **Azure Data Box**.</span><span class="sxs-lookup"><span data-stu-id="52a8b-129">Click **Azure Data Box**.</span></span>
    
   ![Search Azure Data Box 1](media/data-box-disk-deploy-ordered/search-data-box11.png)

2. <span data-ttu-id="52a8b-131">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="52a8b-131">Click **Create**.</span></span>

3. <span data-ttu-id="52a8b-132">Check if Data Box service is available in your region.</span><span class="sxs-lookup"><span data-stu-id="52a8b-132">Check if Data Box service is available in your region.</span></span> <span data-ttu-id="52a8b-133">Enter or select the following information and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="52a8b-133">Enter or select the following information and click **Apply**.</span></span>

    ![Select Data Box Disk option](media/data-box-disk-deploy-ordered/select-data-box-sku-1.png)

    |<span data-ttu-id="52a8b-135">Setting</span><span class="sxs-lookup"><span data-stu-id="52a8b-135">Setting</span></span>|<span data-ttu-id="52a8b-136">Value</span><span class="sxs-lookup"><span data-stu-id="52a8b-136">Value</span></span>|
    |---|---|
    |<span data-ttu-id="52a8b-137">Subscription</span><span class="sxs-lookup"><span data-stu-id="52a8b-137">Subscription</span></span>|<span data-ttu-id="52a8b-138">Select the subscription for which Data Box service is enabled.</span><span class="sxs-lookup"><span data-stu-id="52a8b-138">Select the subscription for which Data Box service is enabled.</span></span><br> <span data-ttu-id="52a8b-139">The subscription is linked to your billing account.</span><span class="sxs-lookup"><span data-stu-id="52a8b-139">The subscription is linked to your billing account.</span></span> |
    |<span data-ttu-id="52a8b-140">Transfer type</span><span class="sxs-lookup"><span data-stu-id="52a8b-140">Transfer type</span></span>| <span data-ttu-id="52a8b-141">Import to Azure</span><span class="sxs-lookup"><span data-stu-id="52a8b-141">Import to Azure</span></span>|
    |<span data-ttu-id="52a8b-142">Source country</span><span class="sxs-lookup"><span data-stu-id="52a8b-142">Source country</span></span> | <span data-ttu-id="52a8b-143">Select the country where your data currently resides.</span><span class="sxs-lookup"><span data-stu-id="52a8b-143">Select the country where your data currently resides.</span></span>|
    |<span data-ttu-id="52a8b-144">Destination Azure region</span><span class="sxs-lookup"><span data-stu-id="52a8b-144">Destination Azure region</span></span>|<span data-ttu-id="52a8b-145">Select the Azure region where you want to transfer data.</span><span class="sxs-lookup"><span data-stu-id="52a8b-145">Select the Azure region where you want to transfer data.</span></span>|

  
5.  <span data-ttu-id="52a8b-146">Select **Data Box Disk**.</span><span class="sxs-lookup"><span data-stu-id="52a8b-146">Select **Data Box Disk**.</span></span> <span data-ttu-id="52a8b-147">The maximum capacity of the solution for a single order of 5 disks is 35 TB.</span><span class="sxs-lookup"><span data-stu-id="52a8b-147">The maximum capacity of the solution for a single order of 5 disks is 35 TB.</span></span> <span data-ttu-id="52a8b-148">You could create multiple orders for larger data sizes.</span><span class="sxs-lookup"><span data-stu-id="52a8b-148">You could create multiple orders for larger data sizes.</span></span> 

     ![Select Data Box Disk option](media/data-box-disk-deploy-ordered/select-data-box-sku-zoom.png)

6.  <span data-ttu-id="52a8b-150">In **Order**, specify the **Order details**.</span><span class="sxs-lookup"><span data-stu-id="52a8b-150">In **Order**, specify the **Order details**.</span></span> <span data-ttu-id="52a8b-151">Enter or select the following information.</span><span class="sxs-lookup"><span data-stu-id="52a8b-151">Enter or select the following information.</span></span>

    |<span data-ttu-id="52a8b-152">Setting</span><span class="sxs-lookup"><span data-stu-id="52a8b-152">Setting</span></span>|<span data-ttu-id="52a8b-153">Value</span><span class="sxs-lookup"><span data-stu-id="52a8b-153">Value</span></span>|
    |---|---|
    |<span data-ttu-id="52a8b-154">Name</span><span class="sxs-lookup"><span data-stu-id="52a8b-154">Name</span></span>|<span data-ttu-id="52a8b-155">Provide a friendly name to track the order.</span><span class="sxs-lookup"><span data-stu-id="52a8b-155">Provide a friendly name to track the order.</span></span><br> <span data-ttu-id="52a8b-156">The name can have between 3 and 24 characters that can be letters, numbers, and hyphens.</span><span class="sxs-lookup"><span data-stu-id="52a8b-156">The name can have between 3 and 24 characters that can be letters, numbers, and hyphens.</span></span> <br> <span data-ttu-id="52a8b-157">The name must start and end with a letter or a number.</span><span class="sxs-lookup"><span data-stu-id="52a8b-157">The name must start and end with a letter or a number.</span></span> |
    |<span data-ttu-id="52a8b-158">Resource group</span><span class="sxs-lookup"><span data-stu-id="52a8b-158">Resource group</span></span>| <span data-ttu-id="52a8b-159">Use an existing or create a new one.</span><span class="sxs-lookup"><span data-stu-id="52a8b-159">Use an existing or create a new one.</span></span> <br> <span data-ttu-id="52a8b-160">A resource group is a logical container for the resources that can be managed or deployed together.</span><span class="sxs-lookup"><span data-stu-id="52a8b-160">A resource group is a logical container for the resources that can be managed or deployed together.</span></span> |
    |<span data-ttu-id="52a8b-161">Destination Azure region</span><span class="sxs-lookup"><span data-stu-id="52a8b-161">Destination Azure region</span></span>| <span data-ttu-id="52a8b-162">Select a region for your storage account.</span><span class="sxs-lookup"><span data-stu-id="52a8b-162">Select a region for your storage account.</span></span><br> <span data-ttu-id="52a8b-163">Currently, storage accounts in all regions in US, West and North Europe, Canada, and Australia are supported.</span><span class="sxs-lookup"><span data-stu-id="52a8b-163">Currently, storage accounts in all regions in US, West and North Europe, Canada, and Australia are supported.</span></span> |
    |<span data-ttu-id="52a8b-164">Storage account(s)</span><span class="sxs-lookup"><span data-stu-id="52a8b-164">Storage account(s)</span></span>|<span data-ttu-id="52a8b-165">Based on the specified Azure region, select from the filtered list of an existing storage account.</span><span class="sxs-lookup"><span data-stu-id="52a8b-165">Based on the specified Azure region, select from the filtered list of an existing storage account.</span></span> <br><span data-ttu-id="52a8b-166">You can also create a new General purpose v1 or General purpose v2 account.</span><span class="sxs-lookup"><span data-stu-id="52a8b-166">You can also create a new General purpose v1 or General purpose v2 account.</span></span> |
    |<span data-ttu-id="52a8b-167">Estimated data size in TB</span><span class="sxs-lookup"><span data-stu-id="52a8b-167">Estimated data size in TB</span></span>| <span data-ttu-id="52a8b-168">Enter an estimate in TB.</span><span class="sxs-lookup"><span data-stu-id="52a8b-168">Enter an estimate in TB.</span></span> <br><span data-ttu-id="52a8b-169">Based on the data size, Microsoft sends you an appropriate number of 8 TB SSDs (7 TB usable capacity).</span><span class="sxs-lookup"><span data-stu-id="52a8b-169">Based on the data size, Microsoft sends you an appropriate number of 8 TB SSDs (7 TB usable capacity).</span></span> <br><span data-ttu-id="52a8b-170">The maximum usable capacity of 5 disks is up to 35 TB.</span><span class="sxs-lookup"><span data-stu-id="52a8b-170">The maximum usable capacity of 5 disks is up to 35 TB.</span></span> |

13. <span data-ttu-id="52a8b-171">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="52a8b-171">Click **Next**.</span></span> 

    ![Supply order details](media/data-box-disk-deploy-ordered/data-box-order-details.png)

14. <span data-ttu-id="52a8b-173">In the **Shipping address** tab, provide your first and last name, name and postal address of the company and a valid phone number.</span><span class="sxs-lookup"><span data-stu-id="52a8b-173">In the **Shipping address** tab, provide your first and last name, name and postal address of the company and a valid phone number.</span></span> <span data-ttu-id="52a8b-174">Click **Validate address**.</span><span class="sxs-lookup"><span data-stu-id="52a8b-174">Click **Validate address**.</span></span> <span data-ttu-id="52a8b-175">The service validates the shipping address for service availability.</span><span class="sxs-lookup"><span data-stu-id="52a8b-175">The service validates the shipping address for service availability.</span></span> <span data-ttu-id="52a8b-176">If the service is available for the specified shipping address, you receive a notification to that effect.</span><span class="sxs-lookup"><span data-stu-id="52a8b-176">If the service is available for the specified shipping address, you receive a notification to that effect.</span></span> 

    ![Provide shipping address](media/data-box-disk-deploy-ordered/data-box-shipping-address.png)
15. <span data-ttu-id="52a8b-178">In the **Notification details**, specify email addresses.</span><span class="sxs-lookup"><span data-stu-id="52a8b-178">In the **Notification details**, specify email addresses.</span></span> <span data-ttu-id="52a8b-179">The service sends email notifications regarding any updates to the order status to the specified email addresses.</span><span class="sxs-lookup"><span data-stu-id="52a8b-179">The service sends email notifications regarding any updates to the order status to the specified email addresses.</span></span> 

    <span data-ttu-id="52a8b-180">We recommend that you use a group email so that you continue to receive notifications if an admin in the group leaves.</span><span class="sxs-lookup"><span data-stu-id="52a8b-180">We recommend that you use a group email so that you continue to receive notifications if an admin in the group leaves.</span></span>

16. <span data-ttu-id="52a8b-181">Review the information **Summary** related to the order, contact, notification, and privacy terms.</span><span class="sxs-lookup"><span data-stu-id="52a8b-181">Review the information **Summary** related to the order, contact, notification, and privacy terms.</span></span> <span data-ttu-id="52a8b-182">Check the box corresponding to the agreement to privacy terms.</span><span class="sxs-lookup"><span data-stu-id="52a8b-182">Check the box corresponding to the agreement to privacy terms.</span></span>

17. <span data-ttu-id="52a8b-183">Click **Order**.</span><span class="sxs-lookup"><span data-stu-id="52a8b-183">Click **Order**.</span></span> <span data-ttu-id="52a8b-184">The order takes a few minutes to be created.</span><span class="sxs-lookup"><span data-stu-id="52a8b-184">The order takes a few minutes to be created.</span></span>

 
## <a name="track-the-order"></a><span data-ttu-id="52a8b-185">Track the order</span><span class="sxs-lookup"><span data-stu-id="52a8b-185">Track the order</span></span>

<span data-ttu-id="52a8b-186">After you have placed the order, you can track the status of the order from Azure preview portal.</span><span class="sxs-lookup"><span data-stu-id="52a8b-186">After you have placed the order, you can track the status of the order from Azure preview portal.</span></span> <span data-ttu-id="52a8b-187">Go to your order and then go to **Overview** to view the status.</span><span class="sxs-lookup"><span data-stu-id="52a8b-187">Go to your order and then go to **Overview** to view the status.</span></span> <span data-ttu-id="52a8b-188">The portal shows the job in **Ordered** state.</span><span class="sxs-lookup"><span data-stu-id="52a8b-188">The portal shows the job in **Ordered** state.</span></span> 

![Data Box Disk status ordered](media/data-box-disk-deploy-ordered/data-box-portal-ordered.png) 

<span data-ttu-id="52a8b-190">If the disks are not available, you receive a notification.</span><span class="sxs-lookup"><span data-stu-id="52a8b-190">If the disks are not available, you receive a notification.</span></span> <span data-ttu-id="52a8b-191">If the disks are available, Microsoft identifies the disks for shipment and prepares the disk package.</span><span class="sxs-lookup"><span data-stu-id="52a8b-191">If the disks are available, Microsoft identifies the disks for shipment and prepares the disk package.</span></span> <span data-ttu-id="52a8b-192">During disk preparation, following actions occur:</span><span class="sxs-lookup"><span data-stu-id="52a8b-192">During disk preparation, following actions occur:</span></span>

- <span data-ttu-id="52a8b-193">Disks are encrypted using AES-128 BitLocker encryption.</span><span class="sxs-lookup"><span data-stu-id="52a8b-193">Disks are encrypted using AES-128 BitLocker encryption.</span></span>  
- <span data-ttu-id="52a8b-194">Disks are locked to prevent an unauthorized access to the disks.</span><span class="sxs-lookup"><span data-stu-id="52a8b-194">Disks are locked to prevent an unauthorized access to the disks.</span></span>
- <span data-ttu-id="52a8b-195">The passkey that unlocks the disks is generated during this process.</span><span class="sxs-lookup"><span data-stu-id="52a8b-195">The passkey that unlocks the disks is generated during this process.</span></span>

<span data-ttu-id="52a8b-196">When the disk preparation is complete, the portal shows the order in **Processed** state.</span><span class="sxs-lookup"><span data-stu-id="52a8b-196">When the disk preparation is complete, the portal shows the order in **Processed** state.</span></span>

<span data-ttu-id="52a8b-197">Microsoft then prepares and dispatches your disks via a regional carrier.</span><span class="sxs-lookup"><span data-stu-id="52a8b-197">Microsoft then prepares and dispatches your disks via a regional carrier.</span></span> <span data-ttu-id="52a8b-198">You receive a tracking number once the disks are shipped.</span><span class="sxs-lookup"><span data-stu-id="52a8b-198">You receive a tracking number once the disks are shipped.</span></span> <span data-ttu-id="52a8b-199">The portal shows the order in **Dispatched** state.</span><span class="sxs-lookup"><span data-stu-id="52a8b-199">The portal shows the order in **Dispatched** state.</span></span>



## <a name="cancel-the-order"></a><span data-ttu-id="52a8b-200">Cancel the order</span><span class="sxs-lookup"><span data-stu-id="52a8b-200">Cancel the order</span></span>

<span data-ttu-id="52a8b-201">To cancel this order, in the Azure preview portal, go to **Overview** and click **Cancel** from the command bar.</span><span class="sxs-lookup"><span data-stu-id="52a8b-201">To cancel this order, in the Azure preview portal, go to **Overview** and click **Cancel** from the command bar.</span></span> 

<span data-ttu-id="52a8b-202">You can only cancel when the disks are ordered and the order is being processed for shipment.</span><span class="sxs-lookup"><span data-stu-id="52a8b-202">You can only cancel when the disks are ordered and the order is being processed for shipment.</span></span> <span data-ttu-id="52a8b-203">Once the order is processed, you can no longer cancel the order.</span><span class="sxs-lookup"><span data-stu-id="52a8b-203">Once the order is processed, you can no longer cancel the order.</span></span> 

![Cancel order](media/data-box-disk-deploy-ordered/cancel-order1.png)

<span data-ttu-id="52a8b-205">To delete a canceled order, go to **Overview** and click **Delete** from the command bar.</span><span class="sxs-lookup"><span data-stu-id="52a8b-205">To delete a canceled order, go to **Overview** and click **Delete** from the command bar.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="52a8b-206">Next steps</span><span class="sxs-lookup"><span data-stu-id="52a8b-206">Next steps</span></span>

<span data-ttu-id="52a8b-207">In this tutorial, you learned about Azure Data Box topics such as:</span><span class="sxs-lookup"><span data-stu-id="52a8b-207">In this tutorial, you learned about Azure Data Box topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="52a8b-208">Sign up for Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="52a8b-208">Sign up for Data Box Disk</span></span>
> * <span data-ttu-id="52a8b-209">Order Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="52a8b-209">Order Data Box Disk</span></span>
> * <span data-ttu-id="52a8b-210">Track the order</span><span class="sxs-lookup"><span data-stu-id="52a8b-210">Track the order</span></span>
> * <span data-ttu-id="52a8b-211">Cancel the order</span><span class="sxs-lookup"><span data-stu-id="52a8b-211">Cancel the order</span></span>

<span data-ttu-id="52a8b-212">Advance to the next tutorial to learn how to set up your Data Box Disk.</span><span class="sxs-lookup"><span data-stu-id="52a8b-212">Advance to the next tutorial to learn how to set up your Data Box Disk.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52a8b-213">Set up your Azure Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="52a8b-213">Set up your Azure Data Box Disk</span></span>](./data-box-disk-deploy-set-up.md)


