---
title: Microsoft Azure Data Box Disk overview | Microsoft Docs in data
description: Describes Azure Data Box Disk, a cloud solution that enables you to transfer large amounts of data into Azure
services: databox
documentationcenter: NA
author: alkohli
manager: twooley
editor: ''
ms.assetid: ''
ms.service: databox
ms.devlang: NA
ms.topic: overview
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/04/2018
ms.author: alkohli
Customer intent: As an IT admin, I need to understand what Data Box Disk is and how it works so I can use it to import on-premises data into Azure.
ms.openlocfilehash: b1beb0e9a5a0435bdf298eddbefc230b2f95ed0a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855601"
---
# <a name="what-is-azure-data-box-disk-preview"></a><span data-ttu-id="8f18f-103">What is Azure Data Box Disk?</span><span class="sxs-lookup"><span data-stu-id="8f18f-103">What is Azure Data Box Disk?</span></span> <span data-ttu-id="8f18f-104">(Preview)</span><span class="sxs-lookup"><span data-stu-id="8f18f-104">(Preview)</span></span>

<span data-ttu-id="8f18f-105">The Microsoft Azure Data Box Disk solution lets you send terabytes of on-premises data to Azure in a quick, inexpensive, and reliable way.</span><span class="sxs-lookup"><span data-stu-id="8f18f-105">The Microsoft Azure Data Box Disk solution lets you send terabytes of on-premises data to Azure in a quick, inexpensive, and reliable way.</span></span> <span data-ttu-id="8f18f-106">The secure data transfer is accelerated by shipping you 1 to 5 solid-state disks (SSDs).</span><span class="sxs-lookup"><span data-stu-id="8f18f-106">The secure data transfer is accelerated by shipping you 1 to 5 solid-state disks (SSDs).</span></span> <span data-ttu-id="8f18f-107">These 8 TB encrypted disks are sent to your datacenter through a regional carrier.</span><span class="sxs-lookup"><span data-stu-id="8f18f-107">These 8 TB encrypted disks are sent to your datacenter through a regional carrier.</span></span> 

<span data-ttu-id="8f18f-108">You can quickly configure, connect, and unlock the disks via the Data Box service in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8f18f-108">You can quickly configure, connect, and unlock the disks via the Data Box service in Azure portal.</span></span> <span data-ttu-id="8f18f-109">Copy your data to disks and ship the disks back to Azure.</span><span class="sxs-lookup"><span data-stu-id="8f18f-109">Copy your data to disks and ship the disks back to Azure.</span></span> <span data-ttu-id="8f18f-110">In the Azure datacenter, your data is automatically uploaded from drives to the cloud using a fast, private network upload link.</span><span class="sxs-lookup"><span data-stu-id="8f18f-110">In the Azure datacenter, your data is automatically uploaded from drives to the cloud using a fast, private network upload link.</span></span>


> [!IMPORTANT]
> - <span data-ttu-id="8f18f-111">Data Box Disk is in preview.</span><span class="sxs-lookup"><span data-stu-id="8f18f-111">Data Box Disk is in preview.</span></span> <span data-ttu-id="8f18f-112">Review the [Azure terms of service for preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) before you deploy this solution.</span><span class="sxs-lookup"><span data-stu-id="8f18f-112">Review the [Azure terms of service for preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) before you deploy this solution.</span></span> 
> - <span data-ttu-id="8f18f-113">You need to sign up for this service.</span><span class="sxs-lookup"><span data-stu-id="8f18f-113">You need to sign up for this service.</span></span> <span data-ttu-id="8f18f-114">To sign up, go to the [Preview portal](http://aka.ms/azuredataboxfromdiskdocs).</span><span class="sxs-lookup"><span data-stu-id="8f18f-114">To sign up, go to the [Preview portal](http://aka.ms/azuredataboxfromdiskdocs).</span></span>
> - <span data-ttu-id="8f18f-115">During preview, Data Box Disk can be shipped to customers in US and European Union.</span><span class="sxs-lookup"><span data-stu-id="8f18f-115">During preview, Data Box Disk can be shipped to customers in US and European Union.</span></span> <span data-ttu-id="8f18f-116">For more information, go to [Region availability](#region-availability).</span><span class="sxs-lookup"><span data-stu-id="8f18f-116">For more information, go to [Region availability](#region-availability).</span></span>

## <a name="use-cases"></a><span data-ttu-id="8f18f-117">Use cases</span><span class="sxs-lookup"><span data-stu-id="8f18f-117">Use cases</span></span>

<span data-ttu-id="8f18f-118">Use Data Box Disk to transfer TBs of data in scenarios with no to limited network connectivity.</span><span class="sxs-lookup"><span data-stu-id="8f18f-118">Use Data Box Disk to transfer TBs of data in scenarios with no to limited network connectivity.</span></span> <span data-ttu-id="8f18f-119">The data movement can be one-time, periodic, or an initial bulk data transfer followed by periodic transfers.</span><span class="sxs-lookup"><span data-stu-id="8f18f-119">The data movement can be one-time, periodic, or an initial bulk data transfer followed by periodic transfers.</span></span> 

- <span data-ttu-id="8f18f-120">**One time migration** - when large amount of on-premises data is moved to Azure.</span><span class="sxs-lookup"><span data-stu-id="8f18f-120">**One time migration** - when large amount of on-premises data is moved to Azure.</span></span> <span data-ttu-id="8f18f-121">For example, moving data from offline tapes to archival data in Azure cool storage.</span><span class="sxs-lookup"><span data-stu-id="8f18f-121">For example, moving data from offline tapes to archival data in Azure cool storage.</span></span>
- <span data-ttu-id="8f18f-122">**Incremental transfer** - when an initial bulk transfer is done using Data Box Disk (seed) followed by incremental transfers over the network.</span><span class="sxs-lookup"><span data-stu-id="8f18f-122">**Incremental transfer** - when an initial bulk transfer is done using Data Box Disk (seed) followed by incremental transfers over the network.</span></span> <span data-ttu-id="8f18f-123">For example, Commvault and Data Box Disk are used to move backup copies to Azure.</span><span class="sxs-lookup"><span data-stu-id="8f18f-123">For example, Commvault and Data Box Disk are used to move backup copies to Azure.</span></span> <span data-ttu-id="8f18f-124">This migration is followed by copying incremental data via network to Azure storage.</span><span class="sxs-lookup"><span data-stu-id="8f18f-124">This migration is followed by copying incremental data via network to Azure storage.</span></span> 
- <span data-ttu-id="8f18f-125">**Periodic uploads** - when large amount of data is generated periodically and needs to be moved to Azure.</span><span class="sxs-lookup"><span data-stu-id="8f18f-125">**Periodic uploads** - when large amount of data is generated periodically and needs to be moved to Azure.</span></span> <span data-ttu-id="8f18f-126">For example in energy exploration, where video content is generated on oil rigs and windmill farms.</span><span class="sxs-lookup"><span data-stu-id="8f18f-126">For example in energy exploration, where video content is generated on oil rigs and windmill farms.</span></span>

## <a name="the-workflow"></a><span data-ttu-id="8f18f-127">The workflow</span><span class="sxs-lookup"><span data-stu-id="8f18f-127">The workflow</span></span>

<span data-ttu-id="8f18f-128">A typical flow includes the following steps:</span><span class="sxs-lookup"><span data-stu-id="8f18f-128">A typical flow includes the following steps:</span></span>

1. <span data-ttu-id="8f18f-129">**Order** - Create an order in the Azure portal, provide shipping information, and the destination Azure storage account for your data.</span><span class="sxs-lookup"><span data-stu-id="8f18f-129">**Order** - Create an order in the Azure portal, provide shipping information, and the destination Azure storage account for your data.</span></span> <span data-ttu-id="8f18f-130">If disks are available, Azure encrypts, prepares, and ships the disks with a shipment tracking ID.</span><span class="sxs-lookup"><span data-stu-id="8f18f-130">If disks are available, Azure encrypts, prepares, and ships the disks with a shipment tracking ID.</span></span>

2. <span data-ttu-id="8f18f-131">**Receive** - Once the disks are delivered, unpack, and connect the disks to the computer that has the data to be copied.</span><span class="sxs-lookup"><span data-stu-id="8f18f-131">**Receive** - Once the disks are delivered, unpack, and connect the disks to the computer that has the data to be copied.</span></span> <span data-ttu-id="8f18f-132">Unlock the disks.</span><span class="sxs-lookup"><span data-stu-id="8f18f-132">Unlock the disks.</span></span>
    
3. <span data-ttu-id="8f18f-133">**Copy data** - Drag and drop to copy the data on the disks.</span><span class="sxs-lookup"><span data-stu-id="8f18f-133">**Copy data** - Drag and drop to copy the data on the disks.</span></span>

4. <span data-ttu-id="8f18f-134">**Return** - Prepare and ship the disks back to Azure datacenter.</span><span class="sxs-lookup"><span data-stu-id="8f18f-134">**Return** - Prepare and ship the disks back to Azure datacenter.</span></span>

5. <span data-ttu-id="8f18f-135">**Upload** - Data is automatically copied from the disks to Azure.</span><span class="sxs-lookup"><span data-stu-id="8f18f-135">**Upload** - Data is automatically copied from the disks to Azure.</span></span> <span data-ttu-id="8f18f-136">The disks are securely erased as per the National Institute of Standards and Technology (NIST) guidelines.</span><span class="sxs-lookup"><span data-stu-id="8f18f-136">The disks are securely erased as per the National Institute of Standards and Technology (NIST) guidelines.</span></span>

<span data-ttu-id="8f18f-137">Throughout this process, you are notified via email on all status changes.</span><span class="sxs-lookup"><span data-stu-id="8f18f-137">Throughout this process, you are notified via email on all status changes.</span></span> <span data-ttu-id="8f18f-138">For more information about the detailed flow, go to [Deploy Data Box Disks in Azure portal](data-box-disk-quickstart-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8f18f-138">For more information about the detailed flow, go to [Deploy Data Box Disks in Azure portal](data-box-disk-quickstart-portal.md).</span></span>


## <a name="benefits"></a><span data-ttu-id="8f18f-139">Benefits</span><span class="sxs-lookup"><span data-stu-id="8f18f-139">Benefits</span></span>

<span data-ttu-id="8f18f-140">Data Box Disk is designed to move large amounts of data to Azure with no impact to network.</span><span class="sxs-lookup"><span data-stu-id="8f18f-140">Data Box Disk is designed to move large amounts of data to Azure with no impact to network.</span></span> <span data-ttu-id="8f18f-141">The solution has the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8f18f-141">The solution has the following benefits:</span></span>

- <span data-ttu-id="8f18f-142">**Speed** - Data Box Disk uses a USB 3.0 connection to move up to 35 TB of data into Azure in less than a week.</span><span class="sxs-lookup"><span data-stu-id="8f18f-142">**Speed** - Data Box Disk uses a USB 3.0 connection to move up to 35 TB of data into Azure in less than a week.</span></span>   

- <span data-ttu-id="8f18f-143">**Easy to use** - Data Box is an easy to use solution.</span><span class="sxs-lookup"><span data-stu-id="8f18f-143">**Easy to use** - Data Box is an easy to use solution.</span></span>

    - <span data-ttu-id="8f18f-144">The disks use USB connectivity with almost no setup time.</span><span class="sxs-lookup"><span data-stu-id="8f18f-144">The disks use USB connectivity with almost no setup time.</span></span>
    - <span data-ttu-id="8f18f-145">The disks have a small form factor that makes them easy to handle.</span><span class="sxs-lookup"><span data-stu-id="8f18f-145">The disks have a small form factor that makes them easy to handle.</span></span>
    - <span data-ttu-id="8f18f-146">The disks have no external power requirements.</span><span class="sxs-lookup"><span data-stu-id="8f18f-146">The disks have no external power requirements.</span></span>
    - <span data-ttu-id="8f18f-147">The disks can be used with a datacenter server, desktop, or a laptop.</span><span class="sxs-lookup"><span data-stu-id="8f18f-147">The disks can be used with a datacenter server, desktop, or a laptop.</span></span>
    - <span data-ttu-id="8f18f-148">The solution provides end-to-end tracking via the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8f18f-148">The solution provides end-to-end tracking via the Azure portal.</span></span>    

- <span data-ttu-id="8f18f-149">**Secure** - Data Box Disk has built-in security protections for the disks, data, and the service.</span><span class="sxs-lookup"><span data-stu-id="8f18f-149">**Secure** - Data Box Disk has built-in security protections for the disks, data, and the service.</span></span> 
    - <span data-ttu-id="8f18f-150">The disks are tamper-resistant and support secure update capability.</span><span class="sxs-lookup"><span data-stu-id="8f18f-150">The disks are tamper-resistant and support secure update capability.</span></span> 
    - <span data-ttu-id="8f18f-151">The data on the disks is secured with an AES 128-bit encryption at all times.</span><span class="sxs-lookup"><span data-stu-id="8f18f-151">The data on the disks is secured with an AES 128-bit encryption at all times.</span></span> 
    - <span data-ttu-id="8f18f-152">The disks can only be unlocked with a key provided in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8f18f-152">The disks can only be unlocked with a key provided in the Azure portal.</span></span> 
    - <span data-ttu-id="8f18f-153">The service is protected by the Azure security features.</span><span class="sxs-lookup"><span data-stu-id="8f18f-153">The service is protected by the Azure security features.</span></span> 
    - <span data-ttu-id="8f18f-154">Once your data is uploaded to Azure, the disks are wiped clean, in accordance with NIST 800-88r1 standards.</span><span class="sxs-lookup"><span data-stu-id="8f18f-154">Once your data is uploaded to Azure, the disks are wiped clean, in accordance with NIST 800-88r1 standards.</span></span>  
    
<span data-ttu-id="8f18f-155">For more information, go to [Azure Data Box Disk security and data protection](data-box-disk-security.md).</span><span class="sxs-lookup"><span data-stu-id="8f18f-155">For more information, go to [Azure Data Box Disk security and data protection](data-box-disk-security.md).</span></span>


## <a name="features-and-specifications"></a><span data-ttu-id="8f18f-156">Features and specifications</span><span class="sxs-lookup"><span data-stu-id="8f18f-156">Features and specifications</span></span>


| <span data-ttu-id="8f18f-157">Specifications</span><span class="sxs-lookup"><span data-stu-id="8f18f-157">Specifications</span></span>                                          | <span data-ttu-id="8f18f-158">Description</span><span class="sxs-lookup"><span data-stu-id="8f18f-158">Description</span></span>              |
|---------------------------------------------------------|--------------------------|
| <span data-ttu-id="8f18f-159">Weight</span><span class="sxs-lookup"><span data-stu-id="8f18f-159">Weight</span></span>                                                  | <span data-ttu-id="8f18f-160">< 2 lbs.</span><span class="sxs-lookup"><span data-stu-id="8f18f-160">< 2 lbs.</span></span> <span data-ttu-id="8f18f-161">per box.</span><span class="sxs-lookup"><span data-stu-id="8f18f-161">per box.</span></span> <span data-ttu-id="8f18f-162">Upto 5 disks in the box</span><span class="sxs-lookup"><span data-stu-id="8f18f-162">Upto 5 disks in the box</span></span>                |
| <span data-ttu-id="8f18f-163">Dimensions</span><span class="sxs-lookup"><span data-stu-id="8f18f-163">Dimensions</span></span>                                              | <span data-ttu-id="8f18f-164">Disk - 2.5" SSD</span><span class="sxs-lookup"><span data-stu-id="8f18f-164">Disk - 2.5" SSD</span></span> |            
| <span data-ttu-id="8f18f-165">Cables</span><span class="sxs-lookup"><span data-stu-id="8f18f-165">Cables</span></span>                                                  | <span data-ttu-id="8f18f-166">1 USB 3.1 cable per disk</span><span class="sxs-lookup"><span data-stu-id="8f18f-166">1 USB 3.1 cable per disk</span></span>|
| <span data-ttu-id="8f18f-167">Storage capacity per order</span><span class="sxs-lookup"><span data-stu-id="8f18f-167">Storage capacity per order</span></span>                              | <span data-ttu-id="8f18f-168">40 TB (usable ~ 35 TB)</span><span class="sxs-lookup"><span data-stu-id="8f18f-168">40 TB (usable ~ 35 TB)</span></span>|
| <span data-ttu-id="8f18f-169">Disk storage capacity</span><span class="sxs-lookup"><span data-stu-id="8f18f-169">Disk storage capacity</span></span>                                   | <span data-ttu-id="8f18f-170">8 TB (usable ~ 7 TB)</span><span class="sxs-lookup"><span data-stu-id="8f18f-170">8 TB (usable ~ 7 TB)</span></span>|
| <span data-ttu-id="8f18f-171">Data interface</span><span class="sxs-lookup"><span data-stu-id="8f18f-171">Data interface</span></span>                                          | <span data-ttu-id="8f18f-172">USB</span><span class="sxs-lookup"><span data-stu-id="8f18f-172">USB</span></span>   |
| <span data-ttu-id="8f18f-173">Security</span><span class="sxs-lookup"><span data-stu-id="8f18f-173">Security</span></span>                                                | <span data-ttu-id="8f18f-174">Pre-encrypted using BitLocker and secure update</span><span class="sxs-lookup"><span data-stu-id="8f18f-174">Pre-encrypted using BitLocker and secure update</span></span> <br> <span data-ttu-id="8f18f-175">Passkey protected disks</span><span class="sxs-lookup"><span data-stu-id="8f18f-175">Passkey protected disks</span></span> <br> <span data-ttu-id="8f18f-176">Data encrypted at all times</span><span class="sxs-lookup"><span data-stu-id="8f18f-176">Data encrypted at all times</span></span>  |
| <span data-ttu-id="8f18f-177">Data transfer rate</span><span class="sxs-lookup"><span data-stu-id="8f18f-177">Data transfer rate</span></span>                                      | <span data-ttu-id="8f18f-178">up to 430 MBps depending on the file size</span><span class="sxs-lookup"><span data-stu-id="8f18f-178">up to 430 MBps depending on the file size</span></span>      |
|<span data-ttu-id="8f18f-179">Management</span><span class="sxs-lookup"><span data-stu-id="8f18f-179">Management</span></span>                                               | <span data-ttu-id="8f18f-180">Azure portal</span><span class="sxs-lookup"><span data-stu-id="8f18f-180">Azure portal</span></span> |


## <a name="region-availability"></a><span data-ttu-id="8f18f-181">Region availability</span><span class="sxs-lookup"><span data-stu-id="8f18f-181">Region availability</span></span>

<span data-ttu-id="8f18f-182">During the preview, Data Box Disk can transfer data to the following Azure regions:</span><span class="sxs-lookup"><span data-stu-id="8f18f-182">During the preview, Data Box Disk can transfer data to the following Azure regions:</span></span>


|<span data-ttu-id="8f18f-183">Azure region</span><span class="sxs-lookup"><span data-stu-id="8f18f-183">Azure region</span></span>  |<span data-ttu-id="8f18f-184">Azure region</span><span class="sxs-lookup"><span data-stu-id="8f18f-184">Azure region</span></span>  |
|---------|---------|
|<span data-ttu-id="8f18f-185">West Central US</span><span class="sxs-lookup"><span data-stu-id="8f18f-185">West Central US</span></span>     |<span data-ttu-id="8f18f-186">Canada Central</span><span class="sxs-lookup"><span data-stu-id="8f18f-186">Canada Central</span></span>       |        
|<span data-ttu-id="8f18f-187">West US2</span><span class="sxs-lookup"><span data-stu-id="8f18f-187">West US2</span></span>     |<span data-ttu-id="8f18f-188">Canada East</span><span class="sxs-lookup"><span data-stu-id="8f18f-188">Canada East</span></span>         |     
|<span data-ttu-id="8f18f-189">West US</span><span class="sxs-lookup"><span data-stu-id="8f18f-189">West US</span></span>     | <span data-ttu-id="8f18f-190">West Europe</span><span class="sxs-lookup"><span data-stu-id="8f18f-190">West Europe</span></span>        |      
|<span data-ttu-id="8f18f-191">South Central US</span><span class="sxs-lookup"><span data-stu-id="8f18f-191">South Central US</span></span>   |<span data-ttu-id="8f18f-192">North Europe</span><span class="sxs-lookup"><span data-stu-id="8f18f-192">North Europe</span></span>     |         
|<span data-ttu-id="8f18f-193">Central US</span><span class="sxs-lookup"><span data-stu-id="8f18f-193">Central US</span></span>     |<span data-ttu-id="8f18f-194">Australia East</span><span class="sxs-lookup"><span data-stu-id="8f18f-194">Australia East</span></span>|
|<span data-ttu-id="8f18f-195">North Central US</span><span class="sxs-lookup"><span data-stu-id="8f18f-195">North Central US</span></span>  |<span data-ttu-id="8f18f-196">Australia Southeast</span><span class="sxs-lookup"><span data-stu-id="8f18f-196">Australia Southeast</span></span>   |
|<span data-ttu-id="8f18f-197">East US</span><span class="sxs-lookup"><span data-stu-id="8f18f-197">East US</span></span>      |<span data-ttu-id="8f18f-198">Australia Central</span><span class="sxs-lookup"><span data-stu-id="8f18f-198">Australia Central</span></span> |
|<span data-ttu-id="8f18f-199">East US2</span><span class="sxs-lookup"><span data-stu-id="8f18f-199">East US2</span></span>     |<span data-ttu-id="8f18f-200">Australia Central 2</span><span class="sxs-lookup"><span data-stu-id="8f18f-200">Australia Central 2</span></span>|


## <a name="pricing"></a><span data-ttu-id="8f18f-201">Pricing</span><span class="sxs-lookup"><span data-stu-id="8f18f-201">Pricing</span></span>

<span data-ttu-id="8f18f-202">During the preview, Data Box Disk is available free of charge.</span><span class="sxs-lookup"><span data-stu-id="8f18f-202">During the preview, Data Box Disk is available free of charge.</span></span> <span data-ttu-id="8f18f-203">This will change when Data Box Disk is generally available.</span><span class="sxs-lookup"><span data-stu-id="8f18f-203">This will change when Data Box Disk is generally available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f18f-204">Next steps</span><span class="sxs-lookup"><span data-stu-id="8f18f-204">Next steps</span></span>

- <span data-ttu-id="8f18f-205">Review the [Data Box Disk requirements](data-box-disk-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="8f18f-205">Review the [Data Box Disk requirements](data-box-disk-system-requirements.md).</span></span>
- <span data-ttu-id="8f18f-206">Understand the [Data Box Disk limits](data-box-disk-limits.md).</span><span class="sxs-lookup"><span data-stu-id="8f18f-206">Understand the [Data Box Disk limits](data-box-disk-limits.md).</span></span>
- <span data-ttu-id="8f18f-207">Quickly deploy [Azure Data Box Disk](data-box-disk-quickstart-portal.md) in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8f18f-207">Quickly deploy [Azure Data Box Disk](data-box-disk-quickstart-portal.md) in Azure portal.</span></span>
