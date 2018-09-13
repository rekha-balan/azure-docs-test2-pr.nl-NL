---
title: Azure Data Box Disk portal admin guide | Microsoft Docs
description: Describes how to use the Azure portal to administer your Azure Data Box.
services: databox
documentationcenter: NA
author: alkohli
manager: twooley
editor: ''
ms.assetid: ''
ms.service: databox
ms.devlang: NA
ms.topic: overview
ms.custom: mvc
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/28/2018
ms.author: alkohli
ms.openlocfilehash: 7bf88a4e9d7af1033f014939d95783f9430dd84a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870823"
---
# <a name="use-azure-portal-to-administer-your-data-box-disk-preview"></a><span data-ttu-id="3f392-103">Use Azure portal to administer your Data Box Disk (Preview)</span><span class="sxs-lookup"><span data-stu-id="3f392-103">Use Azure portal to administer your Data Box Disk (Preview)</span></span>

<span data-ttu-id="3f392-104">The tutorials in this article apply to the Microsoft Azure Data Box Disk during Preview.</span><span class="sxs-lookup"><span data-stu-id="3f392-104">The tutorials in this article apply to the Microsoft Azure Data Box Disk during Preview.</span></span> <span data-ttu-id="3f392-105">This article describes some of the complex workflows and management tasks that can be performed on the Data Box Disk.</span><span class="sxs-lookup"><span data-stu-id="3f392-105">This article describes some of the complex workflows and management tasks that can be performed on the Data Box Disk.</span></span> 

<span data-ttu-id="3f392-106">You can manage the Data Box Disk via the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3f392-106">You can manage the Data Box Disk via the Azure portal.</span></span> <span data-ttu-id="3f392-107">This article focuses on the tasks that you can perform using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3f392-107">This article focuses on the tasks that you can perform using the Azure portal.</span></span> <span data-ttu-id="3f392-108">Use the Azure portal to manage orders, manage disks, and track the status of the order as it proceeds to the terminal stage.</span><span class="sxs-lookup"><span data-stu-id="3f392-108">Use the Azure portal to manage orders, manage disks, and track the status of the order as it proceeds to the terminal stage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f392-109">Data Box Disk is in preview.</span><span class="sxs-lookup"><span data-stu-id="3f392-109">Data Box Disk is in preview.</span></span> <span data-ttu-id="3f392-110">Review the [Azure terms of service for preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) before you deploy this solution.</span><span class="sxs-lookup"><span data-stu-id="3f392-110">Review the [Azure terms of service for preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) before you deploy this solution.</span></span>


## <a name="cancel-an-order"></a><span data-ttu-id="3f392-111">Cancel an order</span><span class="sxs-lookup"><span data-stu-id="3f392-111">Cancel an order</span></span>

<span data-ttu-id="3f392-112">You may need to cancel an order for various reasons after you have placed the order.</span><span class="sxs-lookup"><span data-stu-id="3f392-112">You may need to cancel an order for various reasons after you have placed the order.</span></span> <span data-ttu-id="3f392-113">You can only cancel the order before the disk preparation starts.</span><span class="sxs-lookup"><span data-stu-id="3f392-113">You can only cancel the order before the disk preparation starts.</span></span> <span data-ttu-id="3f392-114">Once the disks are prepared and order processed, it is not possible to cancel the order.</span><span class="sxs-lookup"><span data-stu-id="3f392-114">Once the disks are prepared and order processed, it is not possible to cancel the order.</span></span> 

<span data-ttu-id="3f392-115">Perform the following steps to cancel a order.</span><span class="sxs-lookup"><span data-stu-id="3f392-115">Perform the following steps to cancel a order.</span></span>

1.  <span data-ttu-id="3f392-116">Go to **Overview > Cancel**.</span><span class="sxs-lookup"><span data-stu-id="3f392-116">Go to **Overview > Cancel**.</span></span> 

    ![Cancel order 1](media/data-box-portal-ui-admin/cancel-order1.png)

2.  <span data-ttu-id="3f392-118">Fill out a reason for canceling the order.</span><span class="sxs-lookup"><span data-stu-id="3f392-118">Fill out a reason for canceling the order.</span></span>  

    ![Cancel order 2](media/data-box-portal-ui-admin/cancel-order2.png)

3.  <span data-ttu-id="3f392-120">Once the order is canceled, the portal updates the status of the order and displays it as **Canceled**.</span><span class="sxs-lookup"><span data-stu-id="3f392-120">Once the order is canceled, the portal updates the status of the order and displays it as **Canceled**.</span></span>

    ![Cancel order 3](media/data-box-portal-ui-admin/cancel-order3.png)

<span data-ttu-id="3f392-122">You do not receive an email notification when the order is canceled.</span><span class="sxs-lookup"><span data-stu-id="3f392-122">You do not receive an email notification when the order is canceled.</span></span>

## <a name="clone-an-order"></a><span data-ttu-id="3f392-123">Clone an order</span><span class="sxs-lookup"><span data-stu-id="3f392-123">Clone an order</span></span>

<span data-ttu-id="3f392-124">Cloning is useful in certain situations.</span><span class="sxs-lookup"><span data-stu-id="3f392-124">Cloning is useful in certain situations.</span></span> <span data-ttu-id="3f392-125">For example, a user has used Data Box Disk to transfer some data.</span><span class="sxs-lookup"><span data-stu-id="3f392-125">For example, a user has used Data Box Disk to transfer some data.</span></span> <span data-ttu-id="3f392-126">As more data is generated, there is a need for more disks to transfer that data into Azure.</span><span class="sxs-lookup"><span data-stu-id="3f392-126">As more data is generated, there is a need for more disks to transfer that data into Azure.</span></span> <span data-ttu-id="3f392-127">In this case, the same order can be just cloned over.</span><span class="sxs-lookup"><span data-stu-id="3f392-127">In this case, the same order can be just cloned over.</span></span>

<span data-ttu-id="3f392-128">Perform the following steps to clone an order.</span><span class="sxs-lookup"><span data-stu-id="3f392-128">Perform the following steps to clone an order.</span></span>

1.  <span data-ttu-id="3f392-129">Go to **Overview > Clone**.</span><span class="sxs-lookup"><span data-stu-id="3f392-129">Go to **Overview > Clone**.</span></span> 

    ![Clone order 1](media/data-box-portal-ui-admin/clone-order1.png)

2.  <span data-ttu-id="3f392-131">All the details of the order stay the same.</span><span class="sxs-lookup"><span data-stu-id="3f392-131">All the details of the order stay the same.</span></span> <span data-ttu-id="3f392-132">The order name is the original order name appended by *-Clone*.</span><span class="sxs-lookup"><span data-stu-id="3f392-132">The order name is the original order name appended by *-Clone*.</span></span> <span data-ttu-id="3f392-133">Select the checkbox to confirm that you have reviewed the privacy information.</span><span class="sxs-lookup"><span data-stu-id="3f392-133">Select the checkbox to confirm that you have reviewed the privacy information.</span></span> <span data-ttu-id="3f392-134">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3f392-134">Click **Create**.</span></span>    

<span data-ttu-id="3f392-135">The clone is created in a few minutes and the portal updates to show the new order.</span><span class="sxs-lookup"><span data-stu-id="3f392-135">The clone is created in a few minutes and the portal updates to show the new order.</span></span>

<span data-ttu-id="3f392-136">[![Clone order 3](media/data-box-portal-ui-admin/clone-order3.png)](media/data-box-portal-ui-admin/clone-order3.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="3f392-136">[![Clone order 3](media/data-box-portal-ui-admin/clone-order3.png)](media/data-box-portal-ui-admin/clone-order3.png#lightbox)</span></span> 

## <a name="delete-order"></a><span data-ttu-id="3f392-137">Delete order</span><span class="sxs-lookup"><span data-stu-id="3f392-137">Delete order</span></span>

<span data-ttu-id="3f392-138">You may want to delete an order when the order is complete.</span><span class="sxs-lookup"><span data-stu-id="3f392-138">You may want to delete an order when the order is complete.</span></span> <span data-ttu-id="3f392-139">The order contains your personal information such as name, address, and contact information.</span><span class="sxs-lookup"><span data-stu-id="3f392-139">The order contains your personal information such as name, address, and contact information.</span></span> <span data-ttu-id="3f392-140">This personal information is deleted when the order is deleted.</span><span class="sxs-lookup"><span data-stu-id="3f392-140">This personal information is deleted when the order is deleted.</span></span>

<span data-ttu-id="3f392-141">You can only delete orders that are completed or canceled.</span><span class="sxs-lookup"><span data-stu-id="3f392-141">You can only delete orders that are completed or canceled.</span></span> <span data-ttu-id="3f392-142">Perform the following steps to delete an order.</span><span class="sxs-lookup"><span data-stu-id="3f392-142">Perform the following steps to delete an order.</span></span>

1. <span data-ttu-id="3f392-143">Go to **All resources**.</span><span class="sxs-lookup"><span data-stu-id="3f392-143">Go to **All resources**.</span></span> <span data-ttu-id="3f392-144">Search for your order.</span><span class="sxs-lookup"><span data-stu-id="3f392-144">Search for your order.</span></span>

    ![Search Data Box Disk orders](media/data-box-portal-ui-admin/search-data-box-disk-orders.png)

2. <span data-ttu-id="3f392-146">Click the order you want to delete and go to **Overview**.</span><span class="sxs-lookup"><span data-stu-id="3f392-146">Click the order you want to delete and go to **Overview**.</span></span> <span data-ttu-id="3f392-147">From the command bar, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="3f392-147">From the command bar, click **Delete**.</span></span>

    ![Delete Data Box Disk order 1](media/data-box-portal-ui-admin/delete-order1.png)

3. <span data-ttu-id="3f392-149">Enter the name of the order when prompted to confirm the order deletion.</span><span class="sxs-lookup"><span data-stu-id="3f392-149">Enter the name of the order when prompted to confirm the order deletion.</span></span> <span data-ttu-id="3f392-150">Click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="3f392-150">Click **Delete**.</span></span>

     ![Delete Data Box Disk order 2](media/data-box-portal-ui-admin/delete-order2.png)


## <a name="download-shipping-label"></a><span data-ttu-id="3f392-152">Download shipping label</span><span class="sxs-lookup"><span data-stu-id="3f392-152">Download shipping label</span></span>

<span data-ttu-id="3f392-153">You may need to download the shipping label if the return shipping label shipped with your disks is misplaced or lost.</span><span class="sxs-lookup"><span data-stu-id="3f392-153">You may need to download the shipping label if the return shipping label shipped with your disks is misplaced or lost.</span></span> 

<span data-ttu-id="3f392-154">Perform the following steps to download a shipping label.</span><span class="sxs-lookup"><span data-stu-id="3f392-154">Perform the following steps to download a shipping label.</span></span>
1.  <span data-ttu-id="3f392-155">Go to **Overview > Download shipping label**.</span><span class="sxs-lookup"><span data-stu-id="3f392-155">Go to **Overview > Download shipping label**.</span></span> <span data-ttu-id="3f392-156">This option is available only after the disk is shipped.</span><span class="sxs-lookup"><span data-stu-id="3f392-156">This option is available only after the disk is shipped.</span></span> 

    ![Download shipping label](media/data-box-portal-ui-admin/download-shipping-label.png)

2.  <span data-ttu-id="3f392-158">This downloads the following return shipping label.</span><span class="sxs-lookup"><span data-stu-id="3f392-158">This downloads the following return shipping label.</span></span> <span data-ttu-id="3f392-159">Save the label, print it out, and affix to the return shipment.</span><span class="sxs-lookup"><span data-stu-id="3f392-159">Save the label, print it out, and affix to the return shipment.</span></span>

    ![Example shipping label](media/data-box-portal-ui-admin/example-shipping-label.png)

## <a name="edit-shipping-address"></a><span data-ttu-id="3f392-161">Edit shipping address</span><span class="sxs-lookup"><span data-stu-id="3f392-161">Edit shipping address</span></span>

<span data-ttu-id="3f392-162">You may need to edit the shipping address once the order is placed.</span><span class="sxs-lookup"><span data-stu-id="3f392-162">You may need to edit the shipping address once the order is placed.</span></span> <span data-ttu-id="3f392-163">This is only available until the disk is dispatched.</span><span class="sxs-lookup"><span data-stu-id="3f392-163">This is only available until the disk is dispatched.</span></span> <span data-ttu-id="3f392-164">Once the disk is dispatched, this option will no longer be available.</span><span class="sxs-lookup"><span data-stu-id="3f392-164">Once the disk is dispatched, this option will no longer be available.</span></span>

<span data-ttu-id="3f392-165">Perform the following steps to edit the order.</span><span class="sxs-lookup"><span data-stu-id="3f392-165">Perform the following steps to edit the order.</span></span>

1. <span data-ttu-id="3f392-166">Go to **Order details > Edit shipping address**.</span><span class="sxs-lookup"><span data-stu-id="3f392-166">Go to **Order details > Edit shipping address**.</span></span>

    ![Edit shipping address 1](media/data-box-portal-ui-admin/edit-shipping-address1.png)

2. <span data-ttu-id="3f392-168">You can now edit the shipping address and then save the changes.</span><span class="sxs-lookup"><span data-stu-id="3f392-168">You can now edit the shipping address and then save the changes.</span></span>

    ![Edit shipping address 2](media/data-box-portal-ui-admin/edit-shipping-address2.png)

## <a name="edit-notification-details"></a><span data-ttu-id="3f392-170">Edit notification details</span><span class="sxs-lookup"><span data-stu-id="3f392-170">Edit notification details</span></span>

<span data-ttu-id="3f392-171">You may need to change the users whom you want to recieve the order status emails.</span><span class="sxs-lookup"><span data-stu-id="3f392-171">You may need to change the users whom you want to recieve the order status emails.</span></span> <span data-ttu-id="3f392-172">For instance, a user needs to be informed when the disk is delivered or picked up.</span><span class="sxs-lookup"><span data-stu-id="3f392-172">For instance, a user needs to be informed when the disk is delivered or picked up.</span></span> <span data-ttu-id="3f392-173">Another user may need to be informed when the data copy is complete so he can verify the data is in the Azure storage account before deleting it from the source.</span><span class="sxs-lookup"><span data-stu-id="3f392-173">Another user may need to be informed when the data copy is complete so he can verify the data is in the Azure storage account before deleting it from the source.</span></span> <span data-ttu-id="3f392-174">In these instances, you can edit the notification details.</span><span class="sxs-lookup"><span data-stu-id="3f392-174">In these instances, you can edit the notification details.</span></span>

<span data-ttu-id="3f392-175">Perform the following steps to edit notification details.</span><span class="sxs-lookup"><span data-stu-id="3f392-175">Perform the following steps to edit notification details.</span></span>

1. <span data-ttu-id="3f392-176">Go to **Order details > Edit notification details**.</span><span class="sxs-lookup"><span data-stu-id="3f392-176">Go to **Order details > Edit notification details**.</span></span>

    ![Edit notification details 1](media/data-box-portal-ui-admin/edit-notification-details1.png)

2. <span data-ttu-id="3f392-178">You can now edit the notification details and then save the changes.</span><span class="sxs-lookup"><span data-stu-id="3f392-178">You can now edit the notification details and then save the changes.</span></span>
 
    ![Edit notification details 2](media/data-box-portal-ui-admin/edit-notification-details2.png)

## <a name="view-order-status"></a><span data-ttu-id="3f392-180">View order status</span><span class="sxs-lookup"><span data-stu-id="3f392-180">View order status</span></span>

|<span data-ttu-id="3f392-181">Order status</span><span class="sxs-lookup"><span data-stu-id="3f392-181">Order status</span></span> |<span data-ttu-id="3f392-182">Description</span><span class="sxs-lookup"><span data-stu-id="3f392-182">Description</span></span> |
|---------|---------|
|<span data-ttu-id="3f392-183">Ordered</span><span class="sxs-lookup"><span data-stu-id="3f392-183">Ordered</span></span>     | <span data-ttu-id="3f392-184">Successfully placed an order.</span><span class="sxs-lookup"><span data-stu-id="3f392-184">Successfully placed an order.</span></span> <br> <span data-ttu-id="3f392-185">If the disks are not available, you receive a notification.</span><span class="sxs-lookup"><span data-stu-id="3f392-185">If the disks are not available, you receive a notification.</span></span> <br><span data-ttu-id="3f392-186">If the disks are available, Microsoft identifies a disk for shipment and prepares the disk package.</span><span class="sxs-lookup"><span data-stu-id="3f392-186">If the disks are available, Microsoft identifies a disk for shipment and prepares the disk package.</span></span>        |
|<span data-ttu-id="3f392-187">Processed</span><span class="sxs-lookup"><span data-stu-id="3f392-187">Processed</span></span>     | <span data-ttu-id="3f392-188">Order processing is complete.</span><span class="sxs-lookup"><span data-stu-id="3f392-188">Order processing is complete.</span></span> <br> <span data-ttu-id="3f392-189">During order processing, following actions occur:</span><span class="sxs-lookup"><span data-stu-id="3f392-189">During order processing, following actions occur:</span></span><li><span data-ttu-id="3f392-190">Disks are encrypted using AES-128 BitLocker encryption.</span><span class="sxs-lookup"><span data-stu-id="3f392-190">Disks are encrypted using AES-128 BitLocker encryption.</span></span> </li> <li><span data-ttu-id="3f392-191">The Data Box Disk are locked to prevent any unauthorized access.</span><span class="sxs-lookup"><span data-stu-id="3f392-191">The Data Box Disk are locked to prevent any unauthorized access.</span></span></li><li><span data-ttu-id="3f392-192">The passkey that unlocks the disks is generated during this process.</span><span class="sxs-lookup"><span data-stu-id="3f392-192">The passkey that unlocks the disks is generated during this process.</span></span></li>        |
|<span data-ttu-id="3f392-193">Dispatched</span><span class="sxs-lookup"><span data-stu-id="3f392-193">Dispatched</span></span>     | <span data-ttu-id="3f392-194">Order has shipped.</span><span class="sxs-lookup"><span data-stu-id="3f392-194">Order has shipped.</span></span> <span data-ttu-id="3f392-195">You should receive the order in 1-2 days.</span><span class="sxs-lookup"><span data-stu-id="3f392-195">You should receive the order in 1-2 days.</span></span>        |
|<span data-ttu-id="3f392-196">Delivered</span><span class="sxs-lookup"><span data-stu-id="3f392-196">Delivered</span></span>     | <span data-ttu-id="3f392-197">Order was delivered to the address specified in the order.</span><span class="sxs-lookup"><span data-stu-id="3f392-197">Order was delivered to the address specified in the order.</span></span>        |
|<span data-ttu-id="3f392-198">Picked up</span><span class="sxs-lookup"><span data-stu-id="3f392-198">Picked up</span></span>     |<span data-ttu-id="3f392-199">Your return shipment was picked up.</span><span class="sxs-lookup"><span data-stu-id="3f392-199">Your return shipment was picked up.</span></span> <br> <span data-ttu-id="3f392-200">Once the shipment is recieved at Azure datacenter, data will be automatically uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="3f392-200">Once the shipment is recieved at Azure datacenter, data will be automatically uploaded to Azure.</span></span>         |
|<span data-ttu-id="3f392-201">Received</span><span class="sxs-lookup"><span data-stu-id="3f392-201">Received</span></span>     | <span data-ttu-id="3f392-202">Your disks were received at the Azure datacenter.</span><span class="sxs-lookup"><span data-stu-id="3f392-202">Your disks were received at the Azure datacenter.</span></span> <span data-ttu-id="3f392-203">Data copy will start soon.</span><span class="sxs-lookup"><span data-stu-id="3f392-203">Data copy will start soon.</span></span>        |
|<span data-ttu-id="3f392-204">Data copied</span><span class="sxs-lookup"><span data-stu-id="3f392-204">Data copied</span></span>     |<span data-ttu-id="3f392-205">Data copy is in progress.</span><span class="sxs-lookup"><span data-stu-id="3f392-205">Data copy is in progress.</span></span><br> <span data-ttu-id="3f392-206">Wait until the data copy is complete.</span><span class="sxs-lookup"><span data-stu-id="3f392-206">Wait until the data copy is complete.</span></span>         |
|<span data-ttu-id="3f392-207">Completed</span><span class="sxs-lookup"><span data-stu-id="3f392-207">Completed</span></span>       |<span data-ttu-id="3f392-208">Successfully completed the order.</span><span class="sxs-lookup"><span data-stu-id="3f392-208">Successfully completed the order.</span></span><br> <span data-ttu-id="3f392-209">Verfiy your data is in Azure before you delete the on-premises data from servers.</span><span class="sxs-lookup"><span data-stu-id="3f392-209">Verfiy your data is in Azure before you delete the on-premises data from servers.</span></span>         |
|<span data-ttu-id="3f392-210">Completed with errors</span><span class="sxs-lookup"><span data-stu-id="3f392-210">Completed with errors</span></span>| <span data-ttu-id="3f392-211">Data copy was completed but errors were received.</span><span class="sxs-lookup"><span data-stu-id="3f392-211">Data copy was completed but errors were received.</span></span> <br> <span data-ttu-id="3f392-212">Review the copy logs using the path provided in the **Overview**.</span><span class="sxs-lookup"><span data-stu-id="3f392-212">Review the copy logs using the path provided in the **Overview**.</span></span> <span data-ttu-id="3f392-213">For more information, go to [Download diagnostic logs](data-box-disk-troubleshoot.md#download-diagnostic-logs).</span><span class="sxs-lookup"><span data-stu-id="3f392-213">For more information, go to [Download diagnostic logs](data-box-disk-troubleshoot.md#download-diagnostic-logs).</span></span>   |
|<span data-ttu-id="3f392-214">Canceled</span><span class="sxs-lookup"><span data-stu-id="3f392-214">Canceled</span></span>            |<span data-ttu-id="3f392-215">Order is canceled.</span><span class="sxs-lookup"><span data-stu-id="3f392-215">Order is canceled.</span></span> <br> <span data-ttu-id="3f392-216">Either you canceled the order or an error was encountered and the service canceled the order.</span><span class="sxs-lookup"><span data-stu-id="3f392-216">Either you canceled the order or an error was encountered and the service canceled the order.</span></span>     |



## <a name="next-steps"></a><span data-ttu-id="3f392-217">Next steps</span><span class="sxs-lookup"><span data-stu-id="3f392-217">Next steps</span></span>

- <span data-ttu-id="3f392-218">Learn how to [Troubleshoot Data Box Disk issues](data-box-disk-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="3f392-218">Learn how to [Troubleshoot Data Box Disk issues](data-box-disk-troubleshoot.md).</span></span>
