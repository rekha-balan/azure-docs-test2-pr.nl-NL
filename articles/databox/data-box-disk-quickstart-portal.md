---
title: Quickstart for Microsoft Azure Data Box Disk| Microsoft Docs
description: Use this quickstart to quickly deploy your Azure Data Box Disk in Azure portal
services: databox
documentationcenter: NA
author: alkohli
manager: twooley
editor: ''
ms.assetid: ''
ms.service: databox
ms.devlang: NA
ms.topic: quickstart
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/07/2018
ms.author: alkohli
Customer intent: As an IT admin, I need to quickly deploy Data Box Disk so as to import data into Azure.
ms.openlocfilehash: b4ec329fc5b1f3df9e6641bee3e1378c3a4d09c6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866506"
---
# <a name="quickstart-deploy-azure-data-box-disk-using-the-azure-portal-preview"></a><span data-ttu-id="e1683-103">Quickstart: Deploy Azure Data Box Disk using the Azure portal (Preview)</span><span class="sxs-lookup"><span data-stu-id="e1683-103">Quickstart: Deploy Azure Data Box Disk using the Azure portal (Preview)</span></span>

<span data-ttu-id="e1683-104">This quickstart describes how to deploy the Azure Data Box Disk using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e1683-104">This quickstart describes how to deploy the Azure Data Box Disk using the Azure portal.</span></span> <span data-ttu-id="e1683-105">The steps include how to quickly create an order, receive disks, unpack, connect, and copy data to disks so that it uploads to Azure.</span><span class="sxs-lookup"><span data-stu-id="e1683-105">The steps include how to quickly create an order, receive disks, unpack, connect, and copy data to disks so that it uploads to Azure.</span></span> 

<span data-ttu-id="e1683-106">For detailed step-by-step deployment and tracking instructions, go to [Tutorial: Order Azure Data Box Disk](data-box-disk-deploy-ordered.md).</span><span class="sxs-lookup"><span data-stu-id="e1683-106">For detailed step-by-step deployment and tracking instructions, go to [Tutorial: Order Azure Data Box Disk](data-box-disk-deploy-ordered.md).</span></span> 

<span data-ttu-id="e1683-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="e1683-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1683-108">Data Box Disk is in preview.</span><span class="sxs-lookup"><span data-stu-id="e1683-108">Data Box Disk is in preview.</span></span> <span data-ttu-id="e1683-109">Review the [Azure terms of service for preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) before you deploy this solution.</span><span class="sxs-lookup"><span data-stu-id="e1683-109">Review the [Azure terms of service for preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) before you deploy this solution.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1683-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e1683-110">Prerequisites</span></span>

<span data-ttu-id="e1683-111">Before you begin:</span><span class="sxs-lookup"><span data-stu-id="e1683-111">Before you begin:</span></span>

- <span data-ttu-id="e1683-112">Make sure that your subscription is enabled for Azure Data Box service.</span><span class="sxs-lookup"><span data-stu-id="e1683-112">Make sure that your subscription is enabled for Azure Data Box service.</span></span> <span data-ttu-id="e1683-113">To enable your subscription for this service, [Sign up for the service](http://aka.ms/azuredataboxfromdiskdocs).</span><span class="sxs-lookup"><span data-stu-id="e1683-113">To enable your subscription for this service, [Sign up for the service](http://aka.ms/azuredataboxfromdiskdocs).</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="e1683-114">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="e1683-114">Sign in to Azure</span></span>

<span data-ttu-id="e1683-115">Sign in to the Azure portal at [http://aka.ms/azuredataboxfromdiskdocs](http://aka.ms/azuredataboxfromdiskdocs).</span><span class="sxs-lookup"><span data-stu-id="e1683-115">Sign in to the Azure portal at [http://aka.ms/azuredataboxfromdiskdocs](http://aka.ms/azuredataboxfromdiskdocs).</span></span>

## <a name="order"></a><span data-ttu-id="e1683-116">Order</span><span class="sxs-lookup"><span data-stu-id="e1683-116">Order</span></span>

<span data-ttu-id="e1683-117">This step takes roughly 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="e1683-117">This step takes roughly 5 minutes.</span></span>

1. <span data-ttu-id="e1683-118">Create a new Azure Data Box resource in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e1683-118">Create a new Azure Data Box resource in the Azure portal.</span></span> 
2. <span data-ttu-id="e1683-119">Select a subscription enabled for this service and choose transfer type as **Import**.</span><span class="sxs-lookup"><span data-stu-id="e1683-119">Select a subscription enabled for this service and choose transfer type as **Import**.</span></span> <span data-ttu-id="e1683-120">Provide the **Source country** where the data resides and **Azure destination region** for the data transfer.</span><span class="sxs-lookup"><span data-stu-id="e1683-120">Provide the **Source country** where the data resides and **Azure destination region** for the data transfer.</span></span>
3. <span data-ttu-id="e1683-121">Select **Data Box Disk**.</span><span class="sxs-lookup"><span data-stu-id="e1683-121">Select **Data Box Disk**.</span></span> <span data-ttu-id="e1683-122">The maximum solution capacity is 35 TB and you can create multiple disk orders for larger data sizes.</span><span class="sxs-lookup"><span data-stu-id="e1683-122">The maximum solution capacity is 35 TB and you can create multiple disk orders for larger data sizes.</span></span>  
4. <span data-ttu-id="e1683-123">Enter the order details and shipping information.</span><span class="sxs-lookup"><span data-stu-id="e1683-123">Enter the order details and shipping information.</span></span> <span data-ttu-id="e1683-124">If the service is available in your region, provide notification email addresses, review the summary, and then create the order.</span><span class="sxs-lookup"><span data-stu-id="e1683-124">If the service is available in your region, provide notification email addresses, review the summary, and then create the order.</span></span> 

<span data-ttu-id="e1683-125">Once the order is created, the disks are prepared for shipment.</span><span class="sxs-lookup"><span data-stu-id="e1683-125">Once the order is created, the disks are prepared for shipment.</span></span> 

## <a name="unpack"></a><span data-ttu-id="e1683-126">Unpack</span><span class="sxs-lookup"><span data-stu-id="e1683-126">Unpack</span></span>

<span data-ttu-id="e1683-127">This step takes roughly 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="e1683-127">This step takes roughly 5 minutes.</span></span>

<span data-ttu-id="e1683-128">The Data Box Disk are mailed in a UPS Express Box.</span><span class="sxs-lookup"><span data-stu-id="e1683-128">The Data Box Disk are mailed in a UPS Express Box.</span></span> <span data-ttu-id="e1683-129">Open the box and check that the box has:</span><span class="sxs-lookup"><span data-stu-id="e1683-129">Open the box and check that the box has:</span></span>

- <span data-ttu-id="e1683-130">1 to 5 bubble-wrapped USB disks.</span><span class="sxs-lookup"><span data-stu-id="e1683-130">1 to 5 bubble-wrapped USB disks.</span></span>
- <span data-ttu-id="e1683-131">A connecting cable per disk.</span><span class="sxs-lookup"><span data-stu-id="e1683-131">A connecting cable per disk.</span></span> 
- <span data-ttu-id="e1683-132">A shipping label for return shipment.</span><span class="sxs-lookup"><span data-stu-id="e1683-132">A shipping label for return shipment.</span></span>

## <a name="connect-and-unlock"></a><span data-ttu-id="e1683-133">Connect and unlock</span><span class="sxs-lookup"><span data-stu-id="e1683-133">Connect and unlock</span></span>

<span data-ttu-id="e1683-134">This step takes roughly 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="e1683-134">This step takes roughly 5 minutes.</span></span>

1. <span data-ttu-id="e1683-135">Use the included cable to connect the disk to a Windows/Linux machine running a supported version.</span><span class="sxs-lookup"><span data-stu-id="e1683-135">Use the included cable to connect the disk to a Windows/Linux machine running a supported version.</span></span> <span data-ttu-id="e1683-136">For more information on supported OS versions, go to [Azure Data Box Disk system requirements](data-box-disk-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="e1683-136">For more information on supported OS versions, go to [Azure Data Box Disk system requirements](data-box-disk-system-requirements.md).</span></span> 
2. <span data-ttu-id="e1683-137">To unlock the disk:</span><span class="sxs-lookup"><span data-stu-id="e1683-137">To unlock the disk:</span></span>

    1. <span data-ttu-id="e1683-138">In the Azure portal, go to **General > Device Details** and get the passkey.</span><span class="sxs-lookup"><span data-stu-id="e1683-138">In the Azure portal, go to **General > Device Details** and get the passkey.</span></span>
    2. <span data-ttu-id="e1683-139">Download and extract operating system-specific Data Box Disk unlock tool on the computer used to copy the data to disks.</span><span class="sxs-lookup"><span data-stu-id="e1683-139">Download and extract operating system-specific Data Box Disk unlock tool on the computer used to copy the data to disks.</span></span> 
    3. <span data-ttu-id="e1683-140">Run the Data Box Disk Unlock tool and supply the passkey.</span><span class="sxs-lookup"><span data-stu-id="e1683-140">Run the Data Box Disk Unlock tool and supply the passkey.</span></span> <span data-ttu-id="e1683-141">For any disk reinserts, run the unlock tool again and provide the passkey.</span><span class="sxs-lookup"><span data-stu-id="e1683-141">For any disk reinserts, run the unlock tool again and provide the passkey.</span></span> <span data-ttu-id="e1683-142">**Do not use the BitLocker dialog or the BitLocker key to unlock the disk.**</span><span class="sxs-lookup"><span data-stu-id="e1683-142">**Do not use the BitLocker dialog or the BitLocker key to unlock the disk.**</span></span> <span data-ttu-id="e1683-143">For more information on how to unlock disks, go to [Unlock disks on a Windows client]() or [Unlock disks on a Linux client]().</span><span class="sxs-lookup"><span data-stu-id="e1683-143">For more information on how to unlock disks, go to [Unlock disks on a Windows client]() or [Unlock disks on a Linux client]().</span></span>
    4. <span data-ttu-id="e1683-144">The drive letter assigned to the disk is displayed by the tool.</span><span class="sxs-lookup"><span data-stu-id="e1683-144">The drive letter assigned to the disk is displayed by the tool.</span></span> <span data-ttu-id="e1683-145">Make a note of the disk drive letter.</span><span class="sxs-lookup"><span data-stu-id="e1683-145">Make a note of the disk drive letter.</span></span> <span data-ttu-id="e1683-146">This is used in the subsequent steps.</span><span class="sxs-lookup"><span data-stu-id="e1683-146">This is used in the subsequent steps.</span></span>

## <a name="copy-data-and-verify"></a><span data-ttu-id="e1683-147">Copy data and verify</span><span class="sxs-lookup"><span data-stu-id="e1683-147">Copy data and verify</span></span>

<span data-ttu-id="e1683-148">The time to complete this operation depends upon your data size.</span><span class="sxs-lookup"><span data-stu-id="e1683-148">The time to complete this operation depends upon your data size.</span></span> 

1. <span data-ttu-id="e1683-149">The drive contains *PageBlob*, *BlockBlob*, *AzureImportExport* folders.</span><span class="sxs-lookup"><span data-stu-id="e1683-149">The drive contains *PageBlob*, *BlockBlob*, *AzureImportExport* folders.</span></span> <span data-ttu-id="e1683-150">Drag and drop to copy the data that needs to be imported as block blobs in to *BlockBlob* folder.</span><span class="sxs-lookup"><span data-stu-id="e1683-150">Drag and drop to copy the data that needs to be imported as block blobs in to *BlockBlob* folder.</span></span> <span data-ttu-id="e1683-151">Similarly, drag and drop data such as VHD/VHDX to *PageBlob* folder.</span><span class="sxs-lookup"><span data-stu-id="e1683-151">Similarly, drag and drop data such as VHD/VHDX to *PageBlob* folder.</span></span>

    <span data-ttu-id="e1683-152">A container is created in the Azure storage account for each sub-folder under *BlockBlob* and *PageBlob* folder.</span><span class="sxs-lookup"><span data-stu-id="e1683-152">A container is created in the Azure storage account for each sub-folder under *BlockBlob* and *PageBlob* folder.</span></span> <span data-ttu-id="e1683-153">All files under *BlockBlob* and *PageBlob* folders are copied into a default container `$root` under the Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="e1683-153">All files under *BlockBlob* and *PageBlob* folders are copied into a default container `$root` under the Azure Storage account.</span></span>

    > [!NOTE] 
    > - <span data-ttu-id="e1683-154">All the containers and blobs should conform to [Azure naming conventions](data-box-disk-limits.md#azure-block-blob-and-page-blob-naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="e1683-154">All the containers and blobs should conform to [Azure naming conventions](data-box-disk-limits.md#azure-block-blob-and-page-blob-naming-conventions).</span></span> <span data-ttu-id="e1683-155">If these rules are not followed, the data upload to Azure will fail.</span><span class="sxs-lookup"><span data-stu-id="e1683-155">If these rules are not followed, the data upload to Azure will fail.</span></span>
    > - <span data-ttu-id="e1683-156">Ensure that files do not exceed ~4.75 TiB for block blobs and ~8 TiB for page blobs.</span><span class="sxs-lookup"><span data-stu-id="e1683-156">Ensure that files do not exceed ~4.75 TiB for block blobs and ~8 TiB for page blobs.</span></span>

2. <span data-ttu-id="e1683-157">(Optional) After the copy is complete, we recommend that you run the `DataBoxDiskValidation.cmd` provided in the *AzureImportExport* folder to generate checksums for validation.</span><span class="sxs-lookup"><span data-stu-id="e1683-157">(Optional) After the copy is complete, we recommend that you run the `DataBoxDiskValidation.cmd` provided in the *AzureImportExport* folder to generate checksums for validation.</span></span> <span data-ttu-id="e1683-158">Depending upon the data size, this step may take time.</span><span class="sxs-lookup"><span data-stu-id="e1683-158">Depending upon the data size, this step may take time.</span></span> 
3. <span data-ttu-id="e1683-159">Unplug the drive.</span><span class="sxs-lookup"><span data-stu-id="e1683-159">Unplug the drive.</span></span> 


## <a name="ship-to-azure"></a><span data-ttu-id="e1683-160">Ship to Azure</span><span class="sxs-lookup"><span data-stu-id="e1683-160">Ship to Azure</span></span>

<span data-ttu-id="e1683-161">This step takes about 5-7 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="e1683-161">This step takes about 5-7 minutes to complete.</span></span>

1. <span data-ttu-id="e1683-162">Place all the disks together in the original package.</span><span class="sxs-lookup"><span data-stu-id="e1683-162">Place all the disks together in the original package.</span></span> <span data-ttu-id="e1683-163">Use the included shipping label.</span><span class="sxs-lookup"><span data-stu-id="e1683-163">Use the included shipping label.</span></span> <span data-ttu-id="e1683-164">If the label is damaged or lost, download it from the portal.</span><span class="sxs-lookup"><span data-stu-id="e1683-164">If the label is damaged or lost, download it from the portal.</span></span> <span data-ttu-id="e1683-165">Go to **Overview** and click **Download shipping label** from the command bar.</span><span class="sxs-lookup"><span data-stu-id="e1683-165">Go to **Overview** and click **Download shipping label** from the command bar.</span></span>
2. <span data-ttu-id="e1683-166">Drop off the sealed package at the shipping location.</span><span class="sxs-lookup"><span data-stu-id="e1683-166">Drop off the sealed package at the shipping location.</span></span>  

<span data-ttu-id="e1683-167">Data Box Disk service sends an email notification and updates the order status on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e1683-167">Data Box Disk service sends an email notification and updates the order status on the Azure portal.</span></span>


## <a name="verify-your-data"></a><span data-ttu-id="e1683-168">Verify your data</span><span class="sxs-lookup"><span data-stu-id="e1683-168">Verify your data</span></span>

<span data-ttu-id="e1683-169">The time to complete this operation depends upon your data size.</span><span class="sxs-lookup"><span data-stu-id="e1683-169">The time to complete this operation depends upon your data size.</span></span>

1. <span data-ttu-id="e1683-170">When the Data Box disk is connected to the Azure datacenter network, the data upload to Azure starts automatically.</span><span class="sxs-lookup"><span data-stu-id="e1683-170">When the Data Box disk is connected to the Azure datacenter network, the data upload to Azure starts automatically.</span></span> 
2. <span data-ttu-id="e1683-171">Azure Data Box service notifies you that the data copy is complete via the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e1683-171">Azure Data Box service notifies you that the data copy is complete via the Azure portal.</span></span> 
    
    1. <span data-ttu-id="e1683-172">Check error logs for any failures and take appropriate actions.</span><span class="sxs-lookup"><span data-stu-id="e1683-172">Check error logs for any failures and take appropriate actions.</span></span>
    2. <span data-ttu-id="e1683-173">Verify that your data is in the storage account(s) before you delete it from the source.</span><span class="sxs-lookup"><span data-stu-id="e1683-173">Verify that your data is in the storage account(s) before you delete it from the source.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="e1683-174">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e1683-174">Clean up resources</span></span>

<span data-ttu-id="e1683-175">This step takes 2-3 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="e1683-175">This step takes 2-3 minutes to complete.</span></span>

<span data-ttu-id="e1683-176">To clean up, you can cancel the Data Box order and then delete it.</span><span class="sxs-lookup"><span data-stu-id="e1683-176">To clean up, you can cancel the Data Box order and then delete it.</span></span>

- <span data-ttu-id="e1683-177">You can cancel the Data Box order in the Azure portal before the order is processed.</span><span class="sxs-lookup"><span data-stu-id="e1683-177">You can cancel the Data Box order in the Azure portal before the order is processed.</span></span> <span data-ttu-id="e1683-178">Once the order is processed, the order cannot be canceled.</span><span class="sxs-lookup"><span data-stu-id="e1683-178">Once the order is processed, the order cannot be canceled.</span></span> <span data-ttu-id="e1683-179">The order progresses until it reaches the completed stage.</span><span class="sxs-lookup"><span data-stu-id="e1683-179">The order progresses until it reaches the completed stage.</span></span> 

    <span data-ttu-id="e1683-180">To cancel the order, go to **Overview** and click **Cancel** from the command bar.</span><span class="sxs-lookup"><span data-stu-id="e1683-180">To cancel the order, go to **Overview** and click **Cancel** from the command bar.</span></span>  

- <span data-ttu-id="e1683-181">You can delete the order once the status shows as **Completed** or **Canceled** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e1683-181">You can delete the order once the status shows as **Completed** or **Canceled** in the Azure portal.</span></span> 

    <span data-ttu-id="e1683-182">To delete the order, go to **Overview** and click **Delete** from the command bar.</span><span class="sxs-lookup"><span data-stu-id="e1683-182">To delete the order, go to **Overview** and click **Delete** from the command bar.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1683-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="e1683-183">Next steps</span></span>

<span data-ttu-id="e1683-184">In this quickstart, you’ve deployed Azure Data Box Disk to help import your data into Azure.</span><span class="sxs-lookup"><span data-stu-id="e1683-184">In this quickstart, you’ve deployed Azure Data Box Disk to help import your data into Azure.</span></span> <span data-ttu-id="e1683-185">To learn more about Azure Data Box Disk management, advance to the following tutorial:</span><span class="sxs-lookup"><span data-stu-id="e1683-185">To learn more about Azure Data Box Disk management, advance to the following tutorial:</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="e1683-186">Use the Azure portal to administer Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="e1683-186">Use the Azure portal to administer Data Box Disk</span></span>](data-box-portal-ui-admin.md)


