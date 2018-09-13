---
title: Usage API related FAQs | Microsoft Docs
description: List of Azure Stack meters, comparison to Azure usage API, Usage Time and Reported Time, error codes.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/10/2018
ms.author: mabrigg
ms.reviewer: alfredop
ms.openlocfilehash: ffe3dbf975984eb8df341728075e628d14080ada
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809730"
---
# <a name="frequently-asked-questions-in-azure-stack-usage-api"></a><span data-ttu-id="f4ebb-103">Frequently asked questions in Azure Stack usage API</span><span class="sxs-lookup"><span data-stu-id="f4ebb-103">Frequently asked questions in Azure Stack usage API</span></span>

<span data-ttu-id="f4ebb-104">This article answers some frequently asked questions about the Azure Stack Usage API.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-104">This article answers some frequently asked questions about the Azure Stack Usage API.</span></span>

## <a name="what-meter-ids-can-i-see"></a><span data-ttu-id="f4ebb-105">What meter IDs can I see?</span><span class="sxs-lookup"><span data-stu-id="f4ebb-105">What meter IDs can I see?</span></span>
<span data-ttu-id="f4ebb-106">Usage is reported for the following resource providers:</span><span class="sxs-lookup"><span data-stu-id="f4ebb-106">Usage is reported for the following resource providers:</span></span>

### <a name="network"></a><span data-ttu-id="f4ebb-107">Network</span><span class="sxs-lookup"><span data-stu-id="f4ebb-107">Network</span></span>
  
<span data-ttu-id="f4ebb-108">**Meter ID**: F271A8A388C44D93956A063E1D2FA80B</span><span class="sxs-lookup"><span data-stu-id="f4ebb-108">**Meter ID**: F271A8A388C44D93956A063E1D2FA80B</span></span>  
<span data-ttu-id="f4ebb-109">**Meter name**: Static IP Address Usage</span><span class="sxs-lookup"><span data-stu-id="f4ebb-109">**Meter name**: Static IP Address Usage</span></span>  
<span data-ttu-id="f4ebb-110">**Unit**: IP addresses</span><span class="sxs-lookup"><span data-stu-id="f4ebb-110">**Unit**: IP addresses</span></span>  
<span data-ttu-id="f4ebb-111">**Notes**: Count of IP addresses used.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-111">**Notes**: Count of IP addresses used.</span></span> <span data-ttu-id="f4ebb-112">If you call the usage API with a daily granularity, the meter returns IP address multiplied by the number of hours.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-112">If you call the usage API with a daily granularity, the meter returns IP address multiplied by the number of hours.</span></span>  
  
<span data-ttu-id="f4ebb-113">**Meter ID**: 9E2739BA86744796B465F64674B822BA</span><span class="sxs-lookup"><span data-stu-id="f4ebb-113">**Meter ID**: 9E2739BA86744796B465F64674B822BA</span></span>  
<span data-ttu-id="f4ebb-114">**Meter name**: Dynamic IP Address Usage</span><span class="sxs-lookup"><span data-stu-id="f4ebb-114">**Meter name**: Dynamic IP Address Usage</span></span>  
<span data-ttu-id="f4ebb-115">**Unit**: IP addresses</span><span class="sxs-lookup"><span data-stu-id="f4ebb-115">**Unit**: IP addresses</span></span>  
<span data-ttu-id="f4ebb-116">**Notes**: Count of IP addresses used.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-116">**Notes**: Count of IP addresses used.</span></span> <span data-ttu-id="f4ebb-117">If you call the usage API with a daily granularity, the meter returns IP address multiplied by the number of hours.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-117">If you call the usage API with a daily granularity, the meter returns IP address multiplied by the number of hours.</span></span>  
  
### <a name="storage"></a><span data-ttu-id="f4ebb-118">Storage</span><span class="sxs-lookup"><span data-stu-id="f4ebb-118">Storage</span></span>
  
<span data-ttu-id="f4ebb-119">**Meter ID**: B4438D5D-453B-4EE1-B42A-DC72E377F1E4</span><span class="sxs-lookup"><span data-stu-id="f4ebb-119">**Meter ID**: B4438D5D-453B-4EE1-B42A-DC72E377F1E4</span></span>  
<span data-ttu-id="f4ebb-120">**Meter name**: TableCapacity</span><span class="sxs-lookup"><span data-stu-id="f4ebb-120">**Meter name**: TableCapacity</span></span>  
<span data-ttu-id="f4ebb-121">**Unit**: GB\*hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-121">**Unit**: GB\*hours</span></span>  
<span data-ttu-id="f4ebb-122">**Notes**: Total capacity consumed by tables.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-122">**Notes**: Total capacity consumed by tables.</span></span>  
  
<span data-ttu-id="f4ebb-123">**Meter ID**: B5C15376-6C94-4FDD-B655-1A69D138ACA3</span><span class="sxs-lookup"><span data-stu-id="f4ebb-123">**Meter ID**: B5C15376-6C94-4FDD-B655-1A69D138ACA3</span></span>  
<span data-ttu-id="f4ebb-124">**Meter name**: PageBlobCapacity</span><span class="sxs-lookup"><span data-stu-id="f4ebb-124">**Meter name**: PageBlobCapacity</span></span>  
<span data-ttu-id="f4ebb-125">**Unit**: GB\*hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-125">**Unit**: GB\*hours</span></span>  
<span data-ttu-id="f4ebb-126">**Notes**: Total capacity consumed by page blobs.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-126">**Notes**: Total capacity consumed by page blobs.</span></span>  
  
<span data-ttu-id="f4ebb-127">**Meter ID**: B03C6AE7-B080-4BFA-84A3-22C800F315C6</span><span class="sxs-lookup"><span data-stu-id="f4ebb-127">**Meter ID**: B03C6AE7-B080-4BFA-84A3-22C800F315C6</span></span>  
<span data-ttu-id="f4ebb-128">**Meter name**: QueueCapacity</span><span class="sxs-lookup"><span data-stu-id="f4ebb-128">**Meter name**: QueueCapacity</span></span>  
<span data-ttu-id="f4ebb-129">**Unit**: GB\*hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-129">**Unit**: GB\*hours</span></span>  
<span data-ttu-id="f4ebb-130">**Notes**: Total capacity consumed by queue.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-130">**Notes**: Total capacity consumed by queue.</span></span>  
  
<span data-ttu-id="f4ebb-131">**Meter ID**: 09F8879E-87E9-4305-A572-4B7BE209F857</span><span class="sxs-lookup"><span data-stu-id="f4ebb-131">**Meter ID**: 09F8879E-87E9-4305-A572-4B7BE209F857</span></span>  
<span data-ttu-id="f4ebb-132">**Meter name**: BlockBlobCapacity</span><span class="sxs-lookup"><span data-stu-id="f4ebb-132">**Meter name**: BlockBlobCapacity</span></span>  
<span data-ttu-id="f4ebb-133">**Unit**: GB\*hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-133">**Unit**: GB\*hours</span></span>  
<span data-ttu-id="f4ebb-134">**Notes**: Total capacity consumed by block blobs.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-134">**Notes**: Total capacity consumed by block blobs.</span></span>  
  
<span data-ttu-id="f4ebb-135">**Meter ID**: B9FF3CD0-28AA-4762-84BB-FF8FBAEA6A90</span><span class="sxs-lookup"><span data-stu-id="f4ebb-135">**Meter ID**: B9FF3CD0-28AA-4762-84BB-FF8FBAEA6A90</span></span>  
<span data-ttu-id="f4ebb-136">**Meter name**: TableTransactions</span><span class="sxs-lookup"><span data-stu-id="f4ebb-136">**Meter name**: TableTransactions</span></span>  
<span data-ttu-id="f4ebb-137">**Unit**: Request count in 10,000's</span><span class="sxs-lookup"><span data-stu-id="f4ebb-137">**Unit**: Request count in 10,000's</span></span>  
<span data-ttu-id="f4ebb-138">**Notes**: Table service requests (in 10,000s).</span><span class="sxs-lookup"><span data-stu-id="f4ebb-138">**Notes**: Table service requests (in 10,000s).</span></span>  
  
<span data-ttu-id="f4ebb-139">**Meter ID**: 50A1AEAF-8ECA-48A0-8973-A5B3077FEE0D</span><span class="sxs-lookup"><span data-stu-id="f4ebb-139">**Meter ID**: 50A1AEAF-8ECA-48A0-8973-A5B3077FEE0D</span></span>  
<span data-ttu-id="f4ebb-140">**Meter name**: TableDataTransIn</span><span class="sxs-lookup"><span data-stu-id="f4ebb-140">**Meter name**: TableDataTransIn</span></span>  
<span data-ttu-id="f4ebb-141">**Unit**: Ingress data in GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-141">**Unit**: Ingress data in GB</span></span>  
<span data-ttu-id="f4ebb-142">**Notes**: Table service data ingress in GB.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-142">**Notes**: Table service data ingress in GB.</span></span>  
  
<span data-ttu-id="f4ebb-143">**Meter ID**: 1B8C1DEC-EE42-414B-AA36-6229CF199370</span><span class="sxs-lookup"><span data-stu-id="f4ebb-143">**Meter ID**: 1B8C1DEC-EE42-414B-AA36-6229CF199370</span></span>  
<span data-ttu-id="f4ebb-144">**Meter name**: TableDataTransOut</span><span class="sxs-lookup"><span data-stu-id="f4ebb-144">**Meter name**: TableDataTransOut</span></span>  
<span data-ttu-id="f4ebb-145">**Unit**: Egress in GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-145">**Unit**: Egress in GB</span></span>  
<span data-ttu-id="f4ebb-146">**Notes**: Table service data egress in GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-146">**Notes**: Table service data egress in GB</span></span>  
  
<span data-ttu-id="f4ebb-147">**Meter ID**: 43DAF82B-4618-444A-B994-40C23F7CD438</span><span class="sxs-lookup"><span data-stu-id="f4ebb-147">**Meter ID**: 43DAF82B-4618-444A-B994-40C23F7CD438</span></span>  
<span data-ttu-id="f4ebb-148">**Meter name**: BlobTransactions</span><span class="sxs-lookup"><span data-stu-id="f4ebb-148">**Meter name**: BlobTransactions</span></span>  
<span data-ttu-id="f4ebb-149">**Unit**: Requests count in 10,000's</span><span class="sxs-lookup"><span data-stu-id="f4ebb-149">**Unit**: Requests count in 10,000's</span></span>  
<span data-ttu-id="f4ebb-150">**Notes**: Blob service requests (in 10,000s).</span><span class="sxs-lookup"><span data-stu-id="f4ebb-150">**Notes**: Blob service requests (in 10,000s).</span></span>  
  
<span data-ttu-id="f4ebb-151">**Meter ID**: 9764F92C-E44A-498E-8DC1-AAD66587A810</span><span class="sxs-lookup"><span data-stu-id="f4ebb-151">**Meter ID**: 9764F92C-E44A-498E-8DC1-AAD66587A810</span></span>  
<span data-ttu-id="f4ebb-152">**Meter name**: BlobDataTransIn</span><span class="sxs-lookup"><span data-stu-id="f4ebb-152">**Meter name**: BlobDataTransIn</span></span>  
<span data-ttu-id="f4ebb-153">**Unit**: Ingress data in GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-153">**Unit**: Ingress data in GB</span></span>  
<span data-ttu-id="f4ebb-154">**Notes**: Blob service data ingress in GB.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-154">**Notes**: Blob service data ingress in GB.</span></span>  
  
<span data-ttu-id="f4ebb-155">**Meter ID**: 3023FEF4-ECA5-4D7B-87B3-CFBC061931E8</span><span class="sxs-lookup"><span data-stu-id="f4ebb-155">**Meter ID**: 3023FEF4-ECA5-4D7B-87B3-CFBC061931E8</span></span>  
<span data-ttu-id="f4ebb-156">**Meter name**: BlobDataTransOut</span><span class="sxs-lookup"><span data-stu-id="f4ebb-156">**Meter name**: BlobDataTransOut</span></span>  
<span data-ttu-id="f4ebb-157">**Unit**: Egress in GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-157">**Unit**: Egress in GB</span></span>  
<span data-ttu-id="f4ebb-158">**Notes**: Blob service data egress in GB.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-158">**Notes**: Blob service data egress in GB.</span></span>  
  
<span data-ttu-id="f4ebb-159">**Meter ID**: EB43DD12-1AA6-4C4B-872C-FAF15A6785EA</span><span class="sxs-lookup"><span data-stu-id="f4ebb-159">**Meter ID**: EB43DD12-1AA6-4C4B-872C-FAF15A6785EA</span></span>  
<span data-ttu-id="f4ebb-160">**Meter name**: QueueTransactions</span><span class="sxs-lookup"><span data-stu-id="f4ebb-160">**Meter name**: QueueTransactions</span></span>  
<span data-ttu-id="f4ebb-161">**Unit**: Requests count in 10,000's</span><span class="sxs-lookup"><span data-stu-id="f4ebb-161">**Unit**: Requests count in 10,000's</span></span>  
<span data-ttu-id="f4ebb-162">**Notes**: Queue service requests (in 10,000s).</span><span class="sxs-lookup"><span data-stu-id="f4ebb-162">**Notes**: Queue service requests (in 10,000s).</span></span>  
  
<span data-ttu-id="f4ebb-163">**Meter ID**: E518E809-E369-4A45-9274-2017B29FFF25</span><span class="sxs-lookup"><span data-stu-id="f4ebb-163">**Meter ID**: E518E809-E369-4A45-9274-2017B29FFF25</span></span>  
<span data-ttu-id="f4ebb-164">**Meter name**: QueueDataTransIn</span><span class="sxs-lookup"><span data-stu-id="f4ebb-164">**Meter name**: QueueDataTransIn</span></span>  
<span data-ttu-id="f4ebb-165">**Unit**: Ingress data in GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-165">**Unit**: Ingress data in GB</span></span>  
<span data-ttu-id="f4ebb-166">**Notes**: Queue service data ingress in GB.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-166">**Notes**: Queue service data ingress in GB.</span></span>  
  
<span data-ttu-id="f4ebb-167">**Meter ID**: DD0A10BA-A5D6-4CB6-88C0-7D585CEF9FC2</span><span class="sxs-lookup"><span data-stu-id="f4ebb-167">**Meter ID**: DD0A10BA-A5D6-4CB6-88C0-7D585CEF9FC2</span></span>  
<span data-ttu-id="f4ebb-168">**Meter name**: QueueDataTransOut</span><span class="sxs-lookup"><span data-stu-id="f4ebb-168">**Meter name**: QueueDataTransOut</span></span>  
<span data-ttu-id="f4ebb-169">**Unit**: Egress in GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-169">**Unit**: Egress in GB</span></span>  
<span data-ttu-id="f4ebb-170">**Notes**: Queue service data egress in GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-170">**Notes**: Queue service data egress in GB</span></span>  

### <a name="compute"></a><span data-ttu-id="f4ebb-171">Compute</span><span class="sxs-lookup"><span data-stu-id="f4ebb-171">Compute</span></span> 
  
<span data-ttu-id="f4ebb-172">**Meter ID**: FAB6EB84-500B-4A09-A8CA-7358F8BBAEA5</span><span class="sxs-lookup"><span data-stu-id="f4ebb-172">**Meter ID**: FAB6EB84-500B-4A09-A8CA-7358F8BBAEA5</span></span>  
<span data-ttu-id="f4ebb-173">**Meter name**: Base VM Size Hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-173">**Meter name**: Base VM Size Hours</span></span>  
<span data-ttu-id="f4ebb-174">**Unit**: Virtual core hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-174">**Unit**: Virtual core hours</span></span>  
<span data-ttu-id="f4ebb-175">**Notes**: Number of virtual cores multiplied by the hours the VM ran.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-175">**Notes**: Number of virtual cores multiplied by the hours the VM ran.</span></span>  
  
<span data-ttu-id="f4ebb-176">**Meter ID**: 9CD92D4C-BAFD-4492-B278-BEDC2DE8232A</span><span class="sxs-lookup"><span data-stu-id="f4ebb-176">**Meter ID**: 9CD92D4C-BAFD-4492-B278-BEDC2DE8232A</span></span>  
<span data-ttu-id="f4ebb-177">**Meter name**: Windows VM Size Hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-177">**Meter name**: Windows VM Size Hours</span></span>  
<span data-ttu-id="f4ebb-178">**Unit**: Virtual core hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-178">**Unit**: Virtual core hours</span></span>  
<span data-ttu-id="f4ebb-179">**Notes**: Number of virtual cores multiplied by hours the VM ran.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-179">**Notes**: Number of virtual cores multiplied by hours the VM ran.</span></span>  
  
<span data-ttu-id="f4ebb-180">**Meter ID**: 6DAB500F-A4FD-49C4-956D-229BB9C8C793</span><span class="sxs-lookup"><span data-stu-id="f4ebb-180">**Meter ID**: 6DAB500F-A4FD-49C4-956D-229BB9C8C793</span></span>  
<span data-ttu-id="f4ebb-181">**Meter name**: VM size hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-181">**Meter name**: VM size hours</span></span>  
<span data-ttu-id="f4ebb-182">**Unit**: VM hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-182">**Unit**: VM hours</span></span>  
<span data-ttu-id="f4ebb-183">**Notes**: Captures both Base and Windows VM.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-183">**Notes**: Captures both Base and Windows VM.</span></span> <span data-ttu-id="f4ebb-184">Does not adjust for cores.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-184">Does not adjust for cores.</span></span>  
  
### <a name="managed-disks"></a><span data-ttu-id="f4ebb-185">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="f4ebb-185">Managed Disks</span></span>

<span data-ttu-id="f4ebb-186">**Meter ID**: 5d76e09f-4567-452a-94cc-7d1f097761f0</span><span class="sxs-lookup"><span data-stu-id="f4ebb-186">**Meter ID**: 5d76e09f-4567-452a-94cc-7d1f097761f0</span></span>   
<span data-ttu-id="f4ebb-187">**Meter name**: S4</span><span class="sxs-lookup"><span data-stu-id="f4ebb-187">**Meter name**: S4</span></span>   
<span data-ttu-id="f4ebb-188">**Unit**: Count of Disks</span><span class="sxs-lookup"><span data-stu-id="f4ebb-188">**Unit**: Count of Disks</span></span>   
<span data-ttu-id="f4ebb-189">**Notes**: Standard Managed Disk – 32 GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-189">**Notes**: Standard Managed Disk – 32 GB</span></span> 

<span data-ttu-id="f4ebb-190">**Meter ID**: dc9fc6a9-0782-432a-b8dc-978130457494</span><span class="sxs-lookup"><span data-stu-id="f4ebb-190">**Meter ID**: dc9fc6a9-0782-432a-b8dc-978130457494</span></span>   
<span data-ttu-id="f4ebb-191">**Meter name**: S6</span><span class="sxs-lookup"><span data-stu-id="f4ebb-191">**Meter name**: S6</span></span>   
<span data-ttu-id="f4ebb-192">**Unit**: Count of Disks</span><span class="sxs-lookup"><span data-stu-id="f4ebb-192">**Unit**: Count of Disks</span></span>   
<span data-ttu-id="f4ebb-193">**Notes**: Standard Managed Disk – 64 GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-193">**Notes**: Standard Managed Disk – 64 GB</span></span> 

<span data-ttu-id="f4ebb-194">**Meter ID**: e5572fce-9f58-49d7-840c-b168c0f01fff</span><span class="sxs-lookup"><span data-stu-id="f4ebb-194">**Meter ID**: e5572fce-9f58-49d7-840c-b168c0f01fff</span></span>   
<span data-ttu-id="f4ebb-195">**Meter name**: S10</span><span class="sxs-lookup"><span data-stu-id="f4ebb-195">**Meter name**: S10</span></span>   
<span data-ttu-id="f4ebb-196">**Unit**: Count of Disks</span><span class="sxs-lookup"><span data-stu-id="f4ebb-196">**Unit**: Count of Disks</span></span>   
<span data-ttu-id="f4ebb-197">**Notes**: Standard Managed Disk – 128 GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-197">**Notes**: Standard Managed Disk – 128 GB</span></span> 

<span data-ttu-id="f4ebb-198">**Meter ID**: 9a8caedd-1195-4cd5-80b4-a4c22f9302b8</span><span class="sxs-lookup"><span data-stu-id="f4ebb-198">**Meter ID**: 9a8caedd-1195-4cd5-80b4-a4c22f9302b8</span></span>   
<span data-ttu-id="f4ebb-199">**Meter name**: S15</span><span class="sxs-lookup"><span data-stu-id="f4ebb-199">**Meter name**: S15</span></span>   
<span data-ttu-id="f4ebb-200">**Unit**: Count of Disks</span><span class="sxs-lookup"><span data-stu-id="f4ebb-200">**Unit**: Count of Disks</span></span>   
<span data-ttu-id="f4ebb-201">**Notes**: Standard Managed Disk – 256 GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-201">**Notes**: Standard Managed Disk – 256 GB</span></span> 

<span data-ttu-id="f4ebb-202">**Meter ID**: 5938f8da-0ecd-4c48-8d5a-c7c6c23546be</span><span class="sxs-lookup"><span data-stu-id="f4ebb-202">**Meter ID**: 5938f8da-0ecd-4c48-8d5a-c7c6c23546be</span></span>   
<span data-ttu-id="f4ebb-203">**Meter name**: S20</span><span class="sxs-lookup"><span data-stu-id="f4ebb-203">**Meter name**: S20</span></span>   
<span data-ttu-id="f4ebb-204">**Unit**: Count of Disks</span><span class="sxs-lookup"><span data-stu-id="f4ebb-204">**Unit**: Count of Disks</span></span>      
<span data-ttu-id="f4ebb-205">**Notes**: Standard Managed Disk – 512 GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-205">**Notes**: Standard Managed Disk – 512 GB</span></span> 

<span data-ttu-id="f4ebb-206">**Meter ID**: 7705a158-bd8b-4b2b-b4c2-0782343b81e6</span><span class="sxs-lookup"><span data-stu-id="f4ebb-206">**Meter ID**: 7705a158-bd8b-4b2b-b4c2-0782343b81e6</span></span>   
<span data-ttu-id="f4ebb-207">**Meter name**: S30</span><span class="sxs-lookup"><span data-stu-id="f4ebb-207">**Meter name**: S30</span></span>   
<span data-ttu-id="f4ebb-208">**Unit**: Count of Disks</span><span class="sxs-lookup"><span data-stu-id="f4ebb-208">**Unit**: Count of Disks</span></span>   
<span data-ttu-id="f4ebb-209">**Notes**: Standard Managed Disk – 1024 GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-209">**Notes**: Standard Managed Disk – 1024 GB</span></span> 

<span data-ttu-id="f4ebb-210">**Meter ID**: d9aac1eb-a5d1-42f2-b617-9e3ea94fed88</span><span class="sxs-lookup"><span data-stu-id="f4ebb-210">**Meter ID**: d9aac1eb-a5d1-42f2-b617-9e3ea94fed88</span></span>   
<span data-ttu-id="f4ebb-211">**Meter name**: S40</span><span class="sxs-lookup"><span data-stu-id="f4ebb-211">**Meter name**: S40</span></span>   
<span data-ttu-id="f4ebb-212">**Unit**: Count of Disks</span><span class="sxs-lookup"><span data-stu-id="f4ebb-212">**Unit**: Count of Disks</span></span>   
<span data-ttu-id="f4ebb-213">**Notes**: Standard Managed Disk – 2048 GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-213">**Notes**: Standard Managed Disk – 2048 GB</span></span> 

<span data-ttu-id="f4ebb-214">**Meter ID**: a54899dd-458e-4a40-9abd-f57cafd936a7</span><span class="sxs-lookup"><span data-stu-id="f4ebb-214">**Meter ID**: a54899dd-458e-4a40-9abd-f57cafd936a7</span></span>   
<span data-ttu-id="f4ebb-215">**Meter name**: S50</span><span class="sxs-lookup"><span data-stu-id="f4ebb-215">**Meter name**: S50</span></span>   
<span data-ttu-id="f4ebb-216">**Unit**: Count of Disks</span><span class="sxs-lookup"><span data-stu-id="f4ebb-216">**Unit**: Count of Disks</span></span>   
<span data-ttu-id="f4ebb-217">**Notes**: Standard Managed Disk – 4096 GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-217">**Notes**: Standard Managed Disk – 4096 GB</span></span> 

<span data-ttu-id="f4ebb-218">**Meter ID**: 5c105f5f-cbdf-435c-b49b-3c7174856dcc</span><span class="sxs-lookup"><span data-stu-id="f4ebb-218">**Meter ID**: 5c105f5f-cbdf-435c-b49b-3c7174856dcc</span></span>   
<span data-ttu-id="f4ebb-219">**Meter name**: P4</span><span class="sxs-lookup"><span data-stu-id="f4ebb-219">**Meter name**: P4</span></span>   
<span data-ttu-id="f4ebb-220">**Unit**: Count of Disks</span><span class="sxs-lookup"><span data-stu-id="f4ebb-220">**Unit**: Count of Disks</span></span>   
<span data-ttu-id="f4ebb-221">**Notes**: Premium Managed Disk – 32 GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-221">**Notes**: Premium Managed Disk – 32 GB</span></span> 

<span data-ttu-id="f4ebb-222">**Meter ID**: 518b412b-1927-4f25-985f-4aea24e55c4f</span><span class="sxs-lookup"><span data-stu-id="f4ebb-222">**Meter ID**: 518b412b-1927-4f25-985f-4aea24e55c4f</span></span>   
<span data-ttu-id="f4ebb-223">**Meter name**: P6</span><span class="sxs-lookup"><span data-stu-id="f4ebb-223">**Meter name**: P6</span></span>   
<span data-ttu-id="f4ebb-224">**Unit**: Count of Disks</span><span class="sxs-lookup"><span data-stu-id="f4ebb-224">**Unit**: Count of Disks</span></span>   
<span data-ttu-id="f4ebb-225">**Notes**: Premium Managed Disk – 64 GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-225">**Notes**: Premium Managed Disk – 64 GB</span></span> 

<span data-ttu-id="f4ebb-226">**Meter ID**: 5cfb1fed-0902-49e3-8217-9add946fd624</span><span class="sxs-lookup"><span data-stu-id="f4ebb-226">**Meter ID**: 5cfb1fed-0902-49e3-8217-9add946fd624</span></span>   
<span data-ttu-id="f4ebb-227">**Meter name**: P10</span><span class="sxs-lookup"><span data-stu-id="f4ebb-227">**Meter name**: P10</span></span>   
<span data-ttu-id="f4ebb-228">**Unit**: Count of Disks</span><span class="sxs-lookup"><span data-stu-id="f4ebb-228">**Unit**: Count of Disks</span></span>   
<span data-ttu-id="f4ebb-229">**Notes**: Premium Managed Disk – 128 GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-229">**Notes**: Premium Managed Disk – 128 GB</span></span>  

<span data-ttu-id="f4ebb-230">**Meter ID**: 8de91c94-f740-4d9a-b665-bd5974fa08d4</span><span class="sxs-lookup"><span data-stu-id="f4ebb-230">**Meter ID**: 8de91c94-f740-4d9a-b665-bd5974fa08d4</span></span>   
<span data-ttu-id="f4ebb-231">**Meter name**: P15</span><span class="sxs-lookup"><span data-stu-id="f4ebb-231">**Meter name**: P15</span></span>  
<span data-ttu-id="f4ebb-232">**Unit**: Count of Disks</span><span class="sxs-lookup"><span data-stu-id="f4ebb-232">**Unit**: Count of Disks</span></span>   
<span data-ttu-id="f4ebb-233">**Notes**: Premium Managed Disk – 256 GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-233">**Notes**: Premium Managed Disk – 256 GB</span></span> 

<span data-ttu-id="f4ebb-234">**Meter ID**: c7e7839c-293b-4761-ae4c-848eda91130b</span><span class="sxs-lookup"><span data-stu-id="f4ebb-234">**Meter ID**: c7e7839c-293b-4761-ae4c-848eda91130b</span></span>   
<span data-ttu-id="f4ebb-235">**Meter name**: P20</span><span class="sxs-lookup"><span data-stu-id="f4ebb-235">**Meter name**: P20</span></span>   
<span data-ttu-id="f4ebb-236">**Unit**: Count of Disks</span><span class="sxs-lookup"><span data-stu-id="f4ebb-236">**Unit**: Count of Disks</span></span>   
<span data-ttu-id="f4ebb-237">**Notes**: Premium Managed Disk – 512 GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-237">**Notes**: Premium Managed Disk – 512 GB</span></span> 

<span data-ttu-id="f4ebb-238">**Meter ID**: 9f502103-adf4-4488-b494-456c95d23a9f</span><span class="sxs-lookup"><span data-stu-id="f4ebb-238">**Meter ID**: 9f502103-adf4-4488-b494-456c95d23a9f</span></span>   
<span data-ttu-id="f4ebb-239">**Meter name**: P30</span><span class="sxs-lookup"><span data-stu-id="f4ebb-239">**Meter name**: P30</span></span>   
<span data-ttu-id="f4ebb-240">**Unit**: Count of Disks</span><span class="sxs-lookup"><span data-stu-id="f4ebb-240">**Unit**: Count of Disks</span></span>   
<span data-ttu-id="f4ebb-241">**Notes**: Premium Managed Disk – 1024 GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-241">**Notes**: Premium Managed Disk – 1024 GB</span></span> 

<span data-ttu-id="f4ebb-242">**Meter ID**: 043757fc-049f-4e8b-8379-45bb203c36b1</span><span class="sxs-lookup"><span data-stu-id="f4ebb-242">**Meter ID**: 043757fc-049f-4e8b-8379-45bb203c36b1</span></span>   
<span data-ttu-id="f4ebb-243">**Meter name**: P40</span><span class="sxs-lookup"><span data-stu-id="f4ebb-243">**Meter name**: P40</span></span>   
<span data-ttu-id="f4ebb-244">**Unit**: Count of Disks</span><span class="sxs-lookup"><span data-stu-id="f4ebb-244">**Unit**: Count of Disks</span></span>    
<span data-ttu-id="f4ebb-245">**Notes**: Premium Managed Disk – 2048 GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-245">**Notes**: Premium Managed Disk – 2048 GB</span></span> 

<span data-ttu-id="f4ebb-246">**Meter ID**: c0342c6f-810b-4942-85d3-6eaa561b6570</span><span class="sxs-lookup"><span data-stu-id="f4ebb-246">**Meter ID**: c0342c6f-810b-4942-85d3-6eaa561b6570</span></span>   
<span data-ttu-id="f4ebb-247">**Meter name**: P50</span><span class="sxs-lookup"><span data-stu-id="f4ebb-247">**Meter name**: P50</span></span>   
<span data-ttu-id="f4ebb-248">**Unit**: Count of Disks</span><span class="sxs-lookup"><span data-stu-id="f4ebb-248">**Unit**: Count of Disks</span></span>   
<span data-ttu-id="f4ebb-249">**Notes**: Premium Managed Disk – 4096 GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-249">**Notes**: Premium Managed Disk – 4096 GB</span></span> 

<span data-ttu-id="f4ebb-250">**Meter ID**: 8a409390-1913-40ae-917b-08d0f16f3c38</span><span class="sxs-lookup"><span data-stu-id="f4ebb-250">**Meter ID**: 8a409390-1913-40ae-917b-08d0f16f3c38</span></span>   
<span data-ttu-id="f4ebb-251">**Meter name**: ActualStandardDiskSize</span><span class="sxs-lookup"><span data-stu-id="f4ebb-251">**Meter name**: ActualStandardDiskSize</span></span>   
<span data-ttu-id="f4ebb-252">**Unit**: Byte</span><span class="sxs-lookup"><span data-stu-id="f4ebb-252">**Unit**: Byte</span></span>      
<span data-ttu-id="f4ebb-253">**Notes**: The actual size on disk of standard managed disk</span><span class="sxs-lookup"><span data-stu-id="f4ebb-253">**Notes**: The actual size on disk of standard managed disk</span></span>  

<span data-ttu-id="f4ebb-254">**Meter ID**: 1273b16f-8458-4c34-8ce2-a515de551ef6</span><span class="sxs-lookup"><span data-stu-id="f4ebb-254">**Meter ID**: 1273b16f-8458-4c34-8ce2-a515de551ef6</span></span>  
<span data-ttu-id="f4ebb-255">**Meter name**: ActualPremiumDiskSize</span><span class="sxs-lookup"><span data-stu-id="f4ebb-255">**Meter name**: ActualPremiumDiskSize</span></span>   
<span data-ttu-id="f4ebb-256">**Unit**: Byte</span><span class="sxs-lookup"><span data-stu-id="f4ebb-256">**Unit**: Byte</span></span>      
<span data-ttu-id="f4ebb-257">**Notes**: The actual size on disk of premium managed disk</span><span class="sxs-lookup"><span data-stu-id="f4ebb-257">**Notes**: The actual size on disk of premium managed disk</span></span> 

<span data-ttu-id="f4ebb-258">**Meter ID**: 89009682-df7f-44fe-aeb1-63fba3ddbf4c</span><span class="sxs-lookup"><span data-stu-id="f4ebb-258">**Meter ID**: 89009682-df7f-44fe-aeb1-63fba3ddbf4c</span></span>  
<span data-ttu-id="f4ebb-259">**Meter name**: ActualStandardSnapshotSize</span><span class="sxs-lookup"><span data-stu-id="f4ebb-259">**Meter name**: ActualStandardSnapshotSize</span></span>   
<span data-ttu-id="f4ebb-260">**Unit**: Byte</span><span class="sxs-lookup"><span data-stu-id="f4ebb-260">**Unit**: Byte</span></span>   
<span data-ttu-id="f4ebb-261">**Notes**: The actual size on disk of managed standard snapshot.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-261">**Notes**: The actual size on disk of managed standard snapshot.</span></span>  

<span data-ttu-id="f4ebb-262">**Meter ID**: 95b0c03f-8a82-4524-8961-ccfbf575f536</span><span class="sxs-lookup"><span data-stu-id="f4ebb-262">**Meter ID**: 95b0c03f-8a82-4524-8961-ccfbf575f536</span></span>   
<span data-ttu-id="f4ebb-263">**Meter name**: ActualPremiumSnapshotSize</span><span class="sxs-lookup"><span data-stu-id="f4ebb-263">**Meter name**: ActualPremiumSnapshotSize</span></span>   
<span data-ttu-id="f4ebb-264">**Unit**: Byte</span><span class="sxs-lookup"><span data-stu-id="f4ebb-264">**Unit**: Byte</span></span>   
<span data-ttu-id="f4ebb-265">**Notes**: The actual size on disk of managed premium.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-265">**Notes**: The actual size on disk of managed premium.</span></span>   

### <a name="sql-rp"></a><span data-ttu-id="f4ebb-266">Sql RP</span><span class="sxs-lookup"><span data-stu-id="f4ebb-266">Sql RP</span></span>
  
<span data-ttu-id="f4ebb-267">**Meter ID**: CBCFEF9A-B91F-4597-A4D3-01FE334BED82</span><span class="sxs-lookup"><span data-stu-id="f4ebb-267">**Meter ID**: CBCFEF9A-B91F-4597-A4D3-01FE334BED82</span></span>  
<span data-ttu-id="f4ebb-268">**Meter name**: DatabaseSizeHourSqlMeter</span><span class="sxs-lookup"><span data-stu-id="f4ebb-268">**Meter name**: DatabaseSizeHourSqlMeter</span></span>  
<span data-ttu-id="f4ebb-269">**Unit**: MB\*hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-269">**Unit**: MB\*hours</span></span>  
<span data-ttu-id="f4ebb-270">**Notes**: Total DB capacity at creation.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-270">**Notes**: Total DB capacity at creation.</span></span> <span data-ttu-id="f4ebb-271">If you call the usage API with a daily granularity, the meter returns MB multiplied by the number of hours.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-271">If you call the usage API with a daily granularity, the meter returns MB multiplied by the number of hours.</span></span>  
  
### <a name="mysql-rp"></a><span data-ttu-id="f4ebb-272">MySql RP</span><span class="sxs-lookup"><span data-stu-id="f4ebb-272">MySql RP</span></span>   
  
<span data-ttu-id="f4ebb-273">**Meter ID**: E6D8CFCD-7734-495E-B1CC-5AB0B9C24BD3</span><span class="sxs-lookup"><span data-stu-id="f4ebb-273">**Meter ID**: E6D8CFCD-7734-495E-B1CC-5AB0B9C24BD3</span></span>  
<span data-ttu-id="f4ebb-274">**Meter name**: DatabaseSizeHourMySqlMeter</span><span class="sxs-lookup"><span data-stu-id="f4ebb-274">**Meter name**: DatabaseSizeHourMySqlMeter</span></span>  
<span data-ttu-id="f4ebb-275">**Unit**: MB\*hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-275">**Unit**: MB\*hours</span></span>  
<span data-ttu-id="f4ebb-276">**Notes**: Total DB capacity at creation.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-276">**Notes**: Total DB capacity at creation.</span></span> <span data-ttu-id="f4ebb-277">If you call the usage API with a daily granularity, the meter returns MB multiplied by the number of hours.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-277">If you call the usage API with a daily granularity, the meter returns MB multiplied by the number of hours.</span></span>    
### <a name="key-vault"></a><span data-ttu-id="f4ebb-278">Key Vault</span><span class="sxs-lookup"><span data-stu-id="f4ebb-278">Key Vault</span></span>   
  
<span data-ttu-id="f4ebb-279">**Meter ID**: EBF13B9F-B3EA-46FE-BF54-396E93D48AB4</span><span class="sxs-lookup"><span data-stu-id="f4ebb-279">**Meter ID**: EBF13B9F-B3EA-46FE-BF54-396E93D48AB4</span></span>  
<span data-ttu-id="f4ebb-280">**Meter name**: Key Vault transactions</span><span class="sxs-lookup"><span data-stu-id="f4ebb-280">**Meter name**: Key Vault transactions</span></span>  
<span data-ttu-id="f4ebb-281">**Unit**: Request count in 10,000's</span><span class="sxs-lookup"><span data-stu-id="f4ebb-281">**Unit**: Request count in 10,000's</span></span>  
<span data-ttu-id="f4ebb-282">**Notes**: Number of REST API requests received by Key Vault data plane.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-282">**Notes**: Number of REST API requests received by Key Vault data plane.</span></span>  
  
<span data-ttu-id="f4ebb-283">**Meter ID**: 2C354225-B2FE-42E5-AD89-14F0EA302C87</span><span class="sxs-lookup"><span data-stu-id="f4ebb-283">**Meter ID**: 2C354225-B2FE-42E5-AD89-14F0EA302C87</span></span>  
<span data-ttu-id="f4ebb-284">**Meter name**: Advanced keys transactions</span><span class="sxs-lookup"><span data-stu-id="f4ebb-284">**Meter name**: Advanced keys transactions</span></span>  
<span data-ttu-id="f4ebb-285">**Unit**:  10K transactions</span><span class="sxs-lookup"><span data-stu-id="f4ebb-285">**Unit**:  10K transactions</span></span>  
<span data-ttu-id="f4ebb-286">**Notes**: RSA 3K/4K, ECC key transactions.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-286">**Notes**: RSA 3K/4K, ECC key transactions.</span></span> <span data-ttu-id="f4ebb-287">(preview).</span><span class="sxs-lookup"><span data-stu-id="f4ebb-287">(preview).</span></span>  
  
### <a name="app-service"></a><span data-ttu-id="f4ebb-288">App service</span><span class="sxs-lookup"><span data-stu-id="f4ebb-288">App service</span></span>   
  
<span data-ttu-id="f4ebb-289">**Meter ID**: 190C935E-9ADA-48FF-9AB8-56EA1CF9ADAA</span><span class="sxs-lookup"><span data-stu-id="f4ebb-289">**Meter ID**: 190C935E-9ADA-48FF-9AB8-56EA1CF9ADAA</span></span>  
<span data-ttu-id="f4ebb-290">**Meter name**: App Service</span><span class="sxs-lookup"><span data-stu-id="f4ebb-290">**Meter name**: App Service</span></span>  
<span data-ttu-id="f4ebb-291">**Unit**: Virtual core hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-291">**Unit**: Virtual core hours</span></span>  
<span data-ttu-id="f4ebb-292">**Notes**: Number of virtual cores used to run app service.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-292">**Notes**: Number of virtual cores used to run app service.</span></span> <span data-ttu-id="f4ebb-293">Note: Microsoft uses this meter to charge the App Service on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-293">Note: Microsoft uses this meter to charge the App Service on Azure Stack.</span></span> <span data-ttu-id="f4ebb-294">Cloud Service Providers can use the other App Service meters (below) to calculate usage for their tenants.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-294">Cloud Service Providers can use the other App Service meters (below) to calculate usage for their tenants.</span></span>  
  
<span data-ttu-id="f4ebb-295">**Meter ID**: 67CC4AFC-0691-48E1-A4B8-D744D1FEDBDE</span><span class="sxs-lookup"><span data-stu-id="f4ebb-295">**Meter ID**: 67CC4AFC-0691-48E1-A4B8-D744D1FEDBDE</span></span>  
<span data-ttu-id="f4ebb-296">**Meter name**: Functions Requests</span><span class="sxs-lookup"><span data-stu-id="f4ebb-296">**Meter name**: Functions Requests</span></span>  
<span data-ttu-id="f4ebb-297">**Unit**: 10 Requests</span><span class="sxs-lookup"><span data-stu-id="f4ebb-297">**Unit**: 10 Requests</span></span>  
<span data-ttu-id="f4ebb-298">**Notes**: Total number of requested executions (per 10 executions).</span><span class="sxs-lookup"><span data-stu-id="f4ebb-298">**Notes**: Total number of requested executions (per 10 executions).</span></span> <span data-ttu-id="f4ebb-299">Executions are counted each time a function runs in response to an event, or is triggered by a binding.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-299">Executions are counted each time a function runs in response to an event, or is triggered by a binding.</span></span>  
  
<span data-ttu-id="f4ebb-300">**Meter ID**: D1D04836-075C-4F27-BF65-0A1130EC60ED</span><span class="sxs-lookup"><span data-stu-id="f4ebb-300">**Meter ID**: D1D04836-075C-4F27-BF65-0A1130EC60ED</span></span>  
<span data-ttu-id="f4ebb-301">**Meter name**: Functions - Compute</span><span class="sxs-lookup"><span data-stu-id="f4ebb-301">**Meter name**: Functions - Compute</span></span>  
<span data-ttu-id="f4ebb-302">**Unit**:  GB-s</span><span class="sxs-lookup"><span data-stu-id="f4ebb-302">**Unit**:  GB-s</span></span>  
<span data-ttu-id="f4ebb-303">**Notes**:  Resource consumption measured in gigabyte seconds (GB/s).</span><span class="sxs-lookup"><span data-stu-id="f4ebb-303">**Notes**:  Resource consumption measured in gigabyte seconds (GB/s).</span></span> <span data-ttu-id="f4ebb-304">**Observed resource consumption** is calculated by multiplying average memory size in GB by the time in milliseconds it takes to execute the function.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-304">**Observed resource consumption** is calculated by multiplying average memory size in GB by the time in milliseconds it takes to execute the function.</span></span> <span data-ttu-id="f4ebb-305">Memory used by a function is measured by rounding up to the nearest 128 MB, up to the maximum memory size of 1,536 MB, with execution time calculated by rounding up to the nearest 1 ms.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-305">Memory used by a function is measured by rounding up to the nearest 128 MB, up to the maximum memory size of 1,536 MB, with execution time calculated by rounding up to the nearest 1 ms.</span></span> <span data-ttu-id="f4ebb-306">The minimum execution time and memory for a single function execution is 100 ms and 128 mb respectively.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-306">The minimum execution time and memory for a single function execution is 100 ms and 128 mb respectively.</span></span>  
  
<span data-ttu-id="f4ebb-307">**Meter ID**: 957E9F36-2C14-45A1-B6A1-1723EF71A01D</span><span class="sxs-lookup"><span data-stu-id="f4ebb-307">**Meter ID**: 957E9F36-2C14-45A1-B6A1-1723EF71A01D</span></span>  
<span data-ttu-id="f4ebb-308">**Meter name**: Shared App Service Hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-308">**Meter name**: Shared App Service Hours</span></span>  
<span data-ttu-id="f4ebb-309">**Unit**: 1 hour</span><span class="sxs-lookup"><span data-stu-id="f4ebb-309">**Unit**: 1 hour</span></span>  
<span data-ttu-id="f4ebb-310">**Notes**: Per hour usage of shard App Service Plan.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-310">**Notes**: Per hour usage of shard App Service Plan.</span></span> <span data-ttu-id="f4ebb-311">Plans are metered on a per App basis.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-311">Plans are metered on a per App basis.</span></span>  
  
<span data-ttu-id="f4ebb-312">**Meter ID**: 539CDEC7-B4F5-49F6-AAC4-1F15CFF0EDA9</span><span class="sxs-lookup"><span data-stu-id="f4ebb-312">**Meter ID**: 539CDEC7-B4F5-49F6-AAC4-1F15CFF0EDA9</span></span>  
<span data-ttu-id="f4ebb-313">**Meter name**: Free App Service Hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-313">**Meter name**: Free App Service Hours</span></span>  
<span data-ttu-id="f4ebb-314">**Unit**: 1 hour</span><span class="sxs-lookup"><span data-stu-id="f4ebb-314">**Unit**: 1 hour</span></span>  
<span data-ttu-id="f4ebb-315">**Notes**: Per hour usage of free App Service Plan.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-315">**Notes**: Per hour usage of free App Service Plan.</span></span> <span data-ttu-id="f4ebb-316">Plans are metered on a per App basis.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-316">Plans are metered on a per App basis.</span></span>  
  
<span data-ttu-id="f4ebb-317">**Meter ID**: 88039D51-A206-3A89-E9DE-C5117E2D10A6</span><span class="sxs-lookup"><span data-stu-id="f4ebb-317">**Meter ID**: 88039D51-A206-3A89-E9DE-C5117E2D10A6</span></span>  
<span data-ttu-id="f4ebb-318">**Meter name**: Small Standard App Service Hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-318">**Meter name**: Small Standard App Service Hours</span></span>  
<span data-ttu-id="f4ebb-319">**Unit**: 1 hour</span><span class="sxs-lookup"><span data-stu-id="f4ebb-319">**Unit**: 1 hour</span></span>  
<span data-ttu-id="f4ebb-320">**Notes**: Calculated based on size and number of instances.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-320">**Notes**: Calculated based on size and number of instances.</span></span>  
  
<span data-ttu-id="f4ebb-321">**Meter ID**: 83A2A13E-4788-78DD-5D55-2831B68ED825</span><span class="sxs-lookup"><span data-stu-id="f4ebb-321">**Meter ID**: 83A2A13E-4788-78DD-5D55-2831B68ED825</span></span>  
<span data-ttu-id="f4ebb-322">**Meter name**: Medium Standard App Service Hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-322">**Meter name**: Medium Standard App Service Hours</span></span>  
<span data-ttu-id="f4ebb-323">**Unit**: 1 hour</span><span class="sxs-lookup"><span data-stu-id="f4ebb-323">**Unit**: 1 hour</span></span>  
<span data-ttu-id="f4ebb-324">**Notes**: Calculated based on size and number of instances.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-324">**Notes**: Calculated based on size and number of instances.</span></span>  
  
<span data-ttu-id="f4ebb-325">**Meter ID**: 1083B9DB-E9BB-24BE-A5E9-D6FDD0DDEFE6</span><span class="sxs-lookup"><span data-stu-id="f4ebb-325">**Meter ID**: 1083B9DB-E9BB-24BE-A5E9-D6FDD0DDEFE6</span></span>  
<span data-ttu-id="f4ebb-326">**Meter name**: Large Standard App Service Hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-326">**Meter name**: Large Standard App Service Hours</span></span>  
<span data-ttu-id="f4ebb-327">**Unit**: 1 hour</span><span class="sxs-lookup"><span data-stu-id="f4ebb-327">**Unit**: 1 hour</span></span>  
<span data-ttu-id="f4ebb-328">**Notes**: Calculated based on size and number of instances.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-328">**Notes**: Calculated based on size and number of instances.</span></span>  
  
### <a name="custom-worker-tiers"></a><span data-ttu-id="f4ebb-329">Custom Worker Tiers</span><span class="sxs-lookup"><span data-stu-id="f4ebb-329">Custom Worker Tiers</span></span>   
  
<span data-ttu-id="f4ebb-330">**Meter ID**: *Custom Worker Tiers*</span><span class="sxs-lookup"><span data-stu-id="f4ebb-330">**Meter ID**: *Custom Worker Tiers*</span></span>  
<span data-ttu-id="f4ebb-331">**Meter name**: Custom Worker Tiers</span><span class="sxs-lookup"><span data-stu-id="f4ebb-331">**Meter name**: Custom Worker Tiers</span></span>  
<span data-ttu-id="f4ebb-332">**Unit**: Hours</span><span class="sxs-lookup"><span data-stu-id="f4ebb-332">**Unit**: Hours</span></span>  
<span data-ttu-id="f4ebb-333">**Notes**: Deterministic meter ID is created based on SKU and custom worker tier name.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-333">**Notes**: Deterministic meter ID is created based on SKU and custom worker tier name.</span></span> <span data-ttu-id="f4ebb-334">This meter ID is unique for each custom worker tier.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-334">This meter ID is unique for each custom worker tier.</span></span>  
  
<span data-ttu-id="f4ebb-335">**Meter ID**: 264ACB47-AD38-47F8-ADD3-47F01DC4F473</span><span class="sxs-lookup"><span data-stu-id="f4ebb-335">**Meter ID**: 264ACB47-AD38-47F8-ADD3-47F01DC4F473</span></span>  
<span data-ttu-id="f4ebb-336">**Meter name**: SNI SSL</span><span class="sxs-lookup"><span data-stu-id="f4ebb-336">**Meter name**: SNI SSL</span></span>  
<span data-ttu-id="f4ebb-337">**Unit**: Per SNI SSL Binding</span><span class="sxs-lookup"><span data-stu-id="f4ebb-337">**Unit**: Per SNI SSL Binding</span></span>  
<span data-ttu-id="f4ebb-338">**Notes**: App Service supports two types of SSL connections: Server Name Indication (SNI) SSL Connections and IP Address SSL Connections.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-338">**Notes**: App Service supports two types of SSL connections: Server Name Indication (SNI) SSL Connections and IP Address SSL Connections.</span></span> <span data-ttu-id="f4ebb-339">SNI-based SSL works on modern browsers while IP-based SSL works on all browsers.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-339">SNI-based SSL works on modern browsers while IP-based SSL works on all browsers.</span></span>  
  
<span data-ttu-id="f4ebb-340">**Meter ID**: 60B42D72-DC1C-472C-9895-6C516277EDB4</span><span class="sxs-lookup"><span data-stu-id="f4ebb-340">**Meter ID**: 60B42D72-DC1C-472C-9895-6C516277EDB4</span></span>  
<span data-ttu-id="f4ebb-341">**Meter name**: IP SSL</span><span class="sxs-lookup"><span data-stu-id="f4ebb-341">**Meter name**: IP SSL</span></span>  
<span data-ttu-id="f4ebb-342">**Unit**: Per IP Based SSL Binding</span><span class="sxs-lookup"><span data-stu-id="f4ebb-342">**Unit**: Per IP Based SSL Binding</span></span>  
<span data-ttu-id="f4ebb-343">**Notes**: App Service supports two types of SSL connections: Server Name Indication (SNI) SSL Connections and IP Address SSL Connections.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-343">**Notes**: App Service supports two types of SSL connections: Server Name Indication (SNI) SSL Connections and IP Address SSL Connections.</span></span> <span data-ttu-id="f4ebb-344">SNI-based SSL works on modern browsers while IP-based SSL works on all browsers.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-344">SNI-based SSL works on modern browsers while IP-based SSL works on all browsers.</span></span>  
  
<span data-ttu-id="f4ebb-345">**Meter ID**: 73215A6C-FA54-4284-B9C1-7E8EC871CC5B</span><span class="sxs-lookup"><span data-stu-id="f4ebb-345">**Meter ID**: 73215A6C-FA54-4284-B9C1-7E8EC871CC5B</span></span>  
<span data-ttu-id="f4ebb-346">**Meter name**:  Web Process</span><span class="sxs-lookup"><span data-stu-id="f4ebb-346">**Meter name**:  Web Process</span></span>  
<span data-ttu-id="f4ebb-347">**Unit**:</span><span class="sxs-lookup"><span data-stu-id="f4ebb-347">**Unit**:</span></span>  
<span data-ttu-id="f4ebb-348">**Notes**: Calculated per active site per hour.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-348">**Notes**: Calculated per active site per hour.</span></span>  
  
<span data-ttu-id="f4ebb-349">**Meter ID**: 5887D39B-0253-4E12-83C7-03E1A93DFFD9</span><span class="sxs-lookup"><span data-stu-id="f4ebb-349">**Meter ID**: 5887D39B-0253-4E12-83C7-03E1A93DFFD9</span></span>  
<span data-ttu-id="f4ebb-350">**Meter name**: External Egress Bandwidth</span><span class="sxs-lookup"><span data-stu-id="f4ebb-350">**Meter name**: External Egress Bandwidth</span></span>  
<span data-ttu-id="f4ebb-351">**Unit**: GB</span><span class="sxs-lookup"><span data-stu-id="f4ebb-351">**Unit**: GB</span></span>  
<span data-ttu-id="f4ebb-352">**Notes**: Total incoming request response bytes + total outgoing request bytes + total incoming FTP request response bytes + total incoming web deploy request response bytes.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-352">**Notes**: Total incoming request response bytes + total outgoing request bytes + total incoming FTP request response bytes + total incoming web deploy request response bytes.</span></span>  
  

## <a name="how-do-the-azure-stack-usage-apis-compare-to-the-azure-usage-apihttpsmsdnmicrosoftcomlibraryazure1ea5b323-54bb-423d-916f-190de96c6a3c-currently-in-public-preview"></a><span data-ttu-id="f4ebb-353">How do the Azure Stack usage APIs compare to the [Azure usage API](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) (currently in public preview)?</span><span class="sxs-lookup"><span data-stu-id="f4ebb-353">How do the Azure Stack usage APIs compare to the [Azure usage API](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) (currently in public preview)?</span></span>
* <span data-ttu-id="f4ebb-354">The Tenant Usage API is consistent with the Azure API, with one exception: the *showDetails* flag currently is not supported in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-354">The Tenant Usage API is consistent with the Azure API, with one exception: the *showDetails* flag currently is not supported in Azure Stack.</span></span>
* <span data-ttu-id="f4ebb-355">The Provider Usage API applies only to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-355">The Provider Usage API applies only to Azure Stack.</span></span>
* <span data-ttu-id="f4ebb-356">Currently, the [RateCard API](https://msdn.microsoft.com/library/azure/mt219004.aspx) that is available in Azure is not available in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-356">Currently, the [RateCard API](https://msdn.microsoft.com/library/azure/mt219004.aspx) that is available in Azure is not available in Azure Stack.</span></span>

## <a name="what-is-the-difference-between-usage-time-and-reported-time"></a><span data-ttu-id="f4ebb-357">What is the difference between usage time and reported time?</span><span class="sxs-lookup"><span data-stu-id="f4ebb-357">What is the difference between usage time and reported time?</span></span>
<span data-ttu-id="f4ebb-358">Usage data reports have two main time values:</span><span class="sxs-lookup"><span data-stu-id="f4ebb-358">Usage data reports have two main time values:</span></span>

* <span data-ttu-id="f4ebb-359">**Reported Time**.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-359">**Reported Time**.</span></span> <span data-ttu-id="f4ebb-360">The time when the usage event entered the usage system</span><span class="sxs-lookup"><span data-stu-id="f4ebb-360">The time when the usage event entered the usage system</span></span>
* <span data-ttu-id="f4ebb-361">**Usage Time**.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-361">**Usage Time**.</span></span> <span data-ttu-id="f4ebb-362">The time when the Azure Stack resource was consumed</span><span class="sxs-lookup"><span data-stu-id="f4ebb-362">The time when the Azure Stack resource was consumed</span></span>

<span data-ttu-id="f4ebb-363">You might see a discrepancy in values for Usage Time and Reported Time for a specific usage event.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-363">You might see a discrepancy in values for Usage Time and Reported Time for a specific usage event.</span></span> <span data-ttu-id="f4ebb-364">The delay can be as long as multiple hours in any environment.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-364">The delay can be as long as multiple hours in any environment.</span></span>

<span data-ttu-id="f4ebb-365">Currently, you can query only by *Reported Time*.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-365">Currently, you can query only by *Reported Time*.</span></span>

## <a name="what-do-these-usage-api-error-codes-mean"></a><span data-ttu-id="f4ebb-366">What do these usage API error codes mean?</span><span class="sxs-lookup"><span data-stu-id="f4ebb-366">What do these usage API error codes mean?</span></span>
| <span data-ttu-id="f4ebb-367">**HTTP status code**</span><span class="sxs-lookup"><span data-stu-id="f4ebb-367">**HTTP status code**</span></span> | <span data-ttu-id="f4ebb-368">**Error code**</span><span class="sxs-lookup"><span data-stu-id="f4ebb-368">**Error code**</span></span> | <span data-ttu-id="f4ebb-369">**Description**</span><span class="sxs-lookup"><span data-stu-id="f4ebb-369">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4ebb-370">400/Bad Request</span><span class="sxs-lookup"><span data-stu-id="f4ebb-370">400/Bad Request</span></span> |<span data-ttu-id="f4ebb-371">*NoApiVersion*</span><span class="sxs-lookup"><span data-stu-id="f4ebb-371">*NoApiVersion*</span></span> |<span data-ttu-id="f4ebb-372">The *api-version* query parameter is missing.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-372">The *api-version* query parameter is missing.</span></span> |
| <span data-ttu-id="f4ebb-373">400/Bad Request</span><span class="sxs-lookup"><span data-stu-id="f4ebb-373">400/Bad Request</span></span> |<span data-ttu-id="f4ebb-374">*InvalidProperty*</span><span class="sxs-lookup"><span data-stu-id="f4ebb-374">*InvalidProperty*</span></span> |<span data-ttu-id="f4ebb-375">A property is missing or has an invalid value.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-375">A property is missing or has an invalid value.</span></span> <span data-ttu-id="f4ebb-376">The message in the error code in the response body identifies the missing property.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-376">The message in the error code in the response body identifies the missing property.</span></span> |
| <span data-ttu-id="f4ebb-377">400/Bad Request</span><span class="sxs-lookup"><span data-stu-id="f4ebb-377">400/Bad Request</span></span> |<span data-ttu-id="f4ebb-378">*RequestEndTimeIsInFuture*</span><span class="sxs-lookup"><span data-stu-id="f4ebb-378">*RequestEndTimeIsInFuture*</span></span> |<span data-ttu-id="f4ebb-379">The value for *ReportedEndTime* is in the future.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-379">The value for *ReportedEndTime* is in the future.</span></span> <span data-ttu-id="f4ebb-380">Values in the future are not allowed for this argument.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-380">Values in the future are not allowed for this argument.</span></span> |
| <span data-ttu-id="f4ebb-381">400/Bad Request</span><span class="sxs-lookup"><span data-stu-id="f4ebb-381">400/Bad Request</span></span> |<span data-ttu-id="f4ebb-382">*SubscriberIdIsNotDirectTenant*</span><span class="sxs-lookup"><span data-stu-id="f4ebb-382">*SubscriberIdIsNotDirectTenant*</span></span> |<span data-ttu-id="f4ebb-383">A provider API call has used a subscription ID that is not a valid tenant of the caller.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-383">A provider API call has used a subscription ID that is not a valid tenant of the caller.</span></span> |
| <span data-ttu-id="f4ebb-384">400/Bad Request</span><span class="sxs-lookup"><span data-stu-id="f4ebb-384">400/Bad Request</span></span> |<span data-ttu-id="f4ebb-385">*SubscriptionIdMissingInRequest*</span><span class="sxs-lookup"><span data-stu-id="f4ebb-385">*SubscriptionIdMissingInRequest*</span></span> |<span data-ttu-id="f4ebb-386">The subscription ID of the caller is missing.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-386">The subscription ID of the caller is missing.</span></span> |
| <span data-ttu-id="f4ebb-387">400/Bad Request</span><span class="sxs-lookup"><span data-stu-id="f4ebb-387">400/Bad Request</span></span> |<span data-ttu-id="f4ebb-388">*InvalidAggregationGranularity*</span><span class="sxs-lookup"><span data-stu-id="f4ebb-388">*InvalidAggregationGranularity*</span></span> |<span data-ttu-id="f4ebb-389">An invalid aggregation granularity was requested.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-389">An invalid aggregation granularity was requested.</span></span> <span data-ttu-id="f4ebb-390">Valid values are daily and hourly.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-390">Valid values are daily and hourly.</span></span> |
| <span data-ttu-id="f4ebb-391">503</span><span class="sxs-lookup"><span data-stu-id="f4ebb-391">503</span></span> |<span data-ttu-id="f4ebb-392">*ServiceUnavailable*</span><span class="sxs-lookup"><span data-stu-id="f4ebb-392">*ServiceUnavailable*</span></span> |<span data-ttu-id="f4ebb-393">A retryable error occurred because the service is busy or the call is being throttled.</span><span class="sxs-lookup"><span data-stu-id="f4ebb-393">A retryable error occurred because the service is busy or the call is being throttled.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f4ebb-394">Next Steps</span><span class="sxs-lookup"><span data-stu-id="f4ebb-394">Next Steps</span></span>
[<span data-ttu-id="f4ebb-395">Customer billing and chargeback in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f4ebb-395">Customer billing and chargeback in Azure Stack</span></span>](azure-stack-billing-and-chargeback.md)

[<span data-ttu-id="f4ebb-396">Provider Resource Usage API</span><span class="sxs-lookup"><span data-stu-id="f4ebb-396">Provider Resource Usage API</span></span>](azure-stack-provider-resource-api.md)

[<span data-ttu-id="f4ebb-397">Tenant Resource Usage API</span><span class="sxs-lookup"><span data-stu-id="f4ebb-397">Tenant Resource Usage API</span></span>](azure-stack-tenant-resource-usage-api.md)
