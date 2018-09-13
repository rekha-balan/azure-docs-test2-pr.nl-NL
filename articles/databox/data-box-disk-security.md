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
ms.custom: mvc
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/10/2018
ms.author: alkohli
ms.openlocfilehash: ecdf604cf15ec68875b67f2a4c990103b3375243
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869057"
---
# <a name="azure-data-box-disk-security-and-data-protection-preview"></a><span data-ttu-id="ba890-103">Azure Data Box Disk security and data protection (Preview)</span><span class="sxs-lookup"><span data-stu-id="ba890-103">Azure Data Box Disk security and data protection (Preview)</span></span>

<span data-ttu-id="ba890-104">This article describes the Azure Data Box Disk security features that help protect each of the Data Box solution components and the data stored on them.</span><span class="sxs-lookup"><span data-stu-id="ba890-104">This article describes the Azure Data Box Disk security features that help protect each of the Data Box solution components and the data stored on them.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ba890-105">Data Box Disk is in preview.</span><span class="sxs-lookup"><span data-stu-id="ba890-105">Data Box Disk is in preview.</span></span> <span data-ttu-id="ba890-106">Review the [Azure terms of service for preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) before you deploy this solution.</span><span class="sxs-lookup"><span data-stu-id="ba890-106">Review the [Azure terms of service for preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) before you deploy this solution.</span></span>

## <a name="data-flow-through-components"></a><span data-ttu-id="ba890-107">Data flow through components</span><span class="sxs-lookup"><span data-stu-id="ba890-107">Data flow through components</span></span>

<span data-ttu-id="ba890-108">The Microsoft Azure Data Box solution consists of four main components that interact with each other:</span><span class="sxs-lookup"><span data-stu-id="ba890-108">The Microsoft Azure Data Box solution consists of four main components that interact with each other:</span></span>

- <span data-ttu-id="ba890-109">**Azure Data Box service hosted in Azure** – The management service that you use to create the disk order, configure the disks, and then track the order to completion.</span><span class="sxs-lookup"><span data-stu-id="ba890-109">**Azure Data Box service hosted in Azure** – The management service that you use to create the disk order, configure the disks, and then track the order to completion.</span></span>
- <span data-ttu-id="ba890-110">**Data Box Disks** – The physical disks that are shipped to you to import your on-premises data into Azure.</span><span class="sxs-lookup"><span data-stu-id="ba890-110">**Data Box Disks** – The physical disks that are shipped to you to import your on-premises data into Azure.</span></span> 
- <span data-ttu-id="ba890-111">**Clients/hosts connected to the disks** – The clients in your infrastructure that connect to the Data Box disk over USB and contain data that needs to be protected.</span><span class="sxs-lookup"><span data-stu-id="ba890-111">**Clients/hosts connected to the disks** – The clients in your infrastructure that connect to the Data Box disk over USB and contain data that needs to be protected.</span></span>
- <span data-ttu-id="ba890-112">**Cloud storage** – The location in the Azure cloud where data is stored.</span><span class="sxs-lookup"><span data-stu-id="ba890-112">**Cloud storage** – The location in the Azure cloud where data is stored.</span></span> <span data-ttu-id="ba890-113">This is typically the storage account linked to the Azure Data Box resource that you created.</span><span class="sxs-lookup"><span data-stu-id="ba890-113">This is typically the storage account linked to the Azure Data Box resource that you created.</span></span>

<span data-ttu-id="ba890-114">The following diagram indicates the flow of data through the Azure Data Box Disk solution from on-premises to Azure.</span><span class="sxs-lookup"><span data-stu-id="ba890-114">The following diagram indicates the flow of data through the Azure Data Box Disk solution from on-premises to Azure.</span></span>

![Data Box Disk security](media/data-box-disk-security/data-box-disk-security-1.png)

## <a name="security-features"></a><span data-ttu-id="ba890-116">Security features</span><span class="sxs-lookup"><span data-stu-id="ba890-116">Security features</span></span>

<span data-ttu-id="ba890-117">Data Box Disk provides a secure solution for data protection by ensuring that only authorized entities can view, modify, or delete your data.</span><span class="sxs-lookup"><span data-stu-id="ba890-117">Data Box Disk provides a secure solution for data protection by ensuring that only authorized entities can view, modify, or delete your data.</span></span> <span data-ttu-id="ba890-118">The security features for this solution are for the disk and for the associated service ensuring the security of the data stored on them.</span><span class="sxs-lookup"><span data-stu-id="ba890-118">The security features for this solution are for the disk and for the associated service ensuring the security of the data stored on them.</span></span> 

### <a name="data-box-disk-protection"></a><span data-ttu-id="ba890-119">Data Box Disk protection</span><span class="sxs-lookup"><span data-stu-id="ba890-119">Data Box Disk protection</span></span>

<span data-ttu-id="ba890-120">The Data Box Disk is protected by the following features:</span><span class="sxs-lookup"><span data-stu-id="ba890-120">The Data Box Disk is protected by the following features:</span></span>

- <span data-ttu-id="ba890-121">BitLocker AES-128 bit encryption for the disk at all times.</span><span class="sxs-lookup"><span data-stu-id="ba890-121">BitLocker AES-128 bit encryption for the disk at all times.</span></span>
- <span data-ttu-id="ba890-122">Secure update capability for the disks.</span><span class="sxs-lookup"><span data-stu-id="ba890-122">Secure update capability for the disks.</span></span>
- <span data-ttu-id="ba890-123">Disks are shipped in a locked state and can only be unlocked via a Data Box Disk unlock tool.</span><span class="sxs-lookup"><span data-stu-id="ba890-123">Disks are shipped in a locked state and can only be unlocked via a Data Box Disk unlock tool.</span></span> <span data-ttu-id="ba890-124">The unlock tool is available in the Data Box Disk service portal.</span><span class="sxs-lookup"><span data-stu-id="ba890-124">The unlock tool is available in the Data Box Disk service portal.</span></span>

### <a name="data-box-disk-data-protection"></a><span data-ttu-id="ba890-125">Data Box Disk data protection</span><span class="sxs-lookup"><span data-stu-id="ba890-125">Data Box Disk data protection</span></span>

<span data-ttu-id="ba890-126">The data that flows in and out of Data Box Disk is protected by the following features:</span><span class="sxs-lookup"><span data-stu-id="ba890-126">The data that flows in and out of Data Box Disk is protected by the following features:</span></span>

- <span data-ttu-id="ba890-127">BitLocker encryption of data at all times.</span><span class="sxs-lookup"><span data-stu-id="ba890-127">BitLocker encryption of data at all times.</span></span> 
- <span data-ttu-id="ba890-128">Secure erasure of data from disk once data upload to Azure is complete.</span><span class="sxs-lookup"><span data-stu-id="ba890-128">Secure erasure of data from disk once data upload to Azure is complete.</span></span> <span data-ttu-id="ba890-129">Data erasure is in accordance with NIST 800-88r1 standards.</span><span class="sxs-lookup"><span data-stu-id="ba890-129">Data erasure is in accordance with NIST 800-88r1 standards.</span></span>

### <a name="data-box-service-protection"></a><span data-ttu-id="ba890-130">Data Box service protection</span><span class="sxs-lookup"><span data-stu-id="ba890-130">Data Box service protection</span></span>

<span data-ttu-id="ba890-131">The Data Box service is protected by the following features.</span><span class="sxs-lookup"><span data-stu-id="ba890-131">The Data Box service is protected by the following features.</span></span>

- <span data-ttu-id="ba890-132">Access to the Data Box Disk service requires that your organization has an Azure subscription that includes Data Box Disk.</span><span class="sxs-lookup"><span data-stu-id="ba890-132">Access to the Data Box Disk service requires that your organization has an Azure subscription that includes Data Box Disk.</span></span> <span data-ttu-id="ba890-133">Your subscription governs the features that you can access in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ba890-133">Your subscription governs the features that you can access in the Azure portal.</span></span>
- <span data-ttu-id="ba890-134">Because the Data Box service is hosted in Azure, it is protected by the Azure security features.</span><span class="sxs-lookup"><span data-stu-id="ba890-134">Because the Data Box service is hosted in Azure, it is protected by the Azure security features.</span></span> <span data-ttu-id="ba890-135">For more information about the security features provided by Microsoft Azure, go to the [Microsoft Azure Trust Center](https://www.microsoft.com/TrustCenter/Security/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba890-135">For more information about the security features provided by Microsoft Azure, go to the [Microsoft Azure Trust Center](https://www.microsoft.com/TrustCenter/Security/default.aspx).</span></span> 
- <span data-ttu-id="ba890-136">The Data Box Disk stores disk passkey that is used to unlock the disk in the service.</span><span class="sxs-lookup"><span data-stu-id="ba890-136">The Data Box Disk stores disk passkey that is used to unlock the disk in the service.</span></span> 
- <span data-ttu-id="ba890-137">The Data box Disk service stores order details and status in the service.</span><span class="sxs-lookup"><span data-stu-id="ba890-137">The Data box Disk service stores order details and status in the service.</span></span> <span data-ttu-id="ba890-138">This information is deleted when the order is deleted.</span><span class="sxs-lookup"><span data-stu-id="ba890-138">This information is deleted when the order is deleted.</span></span> 


## <a name="managing-personal-data"></a><span data-ttu-id="ba890-139">Managing personal data</span><span class="sxs-lookup"><span data-stu-id="ba890-139">Managing personal data</span></span>

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-intro-sentence.md)]

<span data-ttu-id="ba890-140">Azure Data Box Disk collects and displays personal information in the following key instances in the service:</span><span class="sxs-lookup"><span data-stu-id="ba890-140">Azure Data Box Disk collects and displays personal information in the following key instances in the service:</span></span>

- <span data-ttu-id="ba890-141">**Notification settings** - When you create an order, you configure the email address of users under notification settings.</span><span class="sxs-lookup"><span data-stu-id="ba890-141">**Notification settings** - When you create an order, you configure the email address of users under notification settings.</span></span> <span data-ttu-id="ba890-142">This information can be viewed by the administrator.</span><span class="sxs-lookup"><span data-stu-id="ba890-142">This information can be viewed by the administrator.</span></span> <span data-ttu-id="ba890-143">This information is deleted by the service when the job reaches the terminal state or when you delete the order.</span><span class="sxs-lookup"><span data-stu-id="ba890-143">This information is deleted by the service when the job reaches the terminal state or when you delete the order.</span></span>

- <span data-ttu-id="ba890-144">**Order details** – Once the order is created, the shipping address, email, contact information of users is stored in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ba890-144">**Order details** – Once the order is created, the shipping address, email, contact information of users is stored in the Azure portal.</span></span> <span data-ttu-id="ba890-145">The information saved includes:</span><span class="sxs-lookup"><span data-stu-id="ba890-145">The information saved includes:</span></span>

    - <span data-ttu-id="ba890-146">Contact name</span><span class="sxs-lookup"><span data-stu-id="ba890-146">Contact name</span></span>
    - <span data-ttu-id="ba890-147">Phone number</span><span class="sxs-lookup"><span data-stu-id="ba890-147">Phone number</span></span>
    - <span data-ttu-id="ba890-148">Email</span><span class="sxs-lookup"><span data-stu-id="ba890-148">Email</span></span>
    - <span data-ttu-id="ba890-149">Street address</span><span class="sxs-lookup"><span data-stu-id="ba890-149">Street address</span></span>
    - <span data-ttu-id="ba890-150">City</span><span class="sxs-lookup"><span data-stu-id="ba890-150">City</span></span>
    - <span data-ttu-id="ba890-151">Zip/postal code</span><span class="sxs-lookup"><span data-stu-id="ba890-151">Zip/postal code</span></span>
    - <span data-ttu-id="ba890-152">State</span><span class="sxs-lookup"><span data-stu-id="ba890-152">State</span></span>
    - <span data-ttu-id="ba890-153">Country/Province/Region</span><span class="sxs-lookup"><span data-stu-id="ba890-153">Country/Province/Region</span></span>
    - <span data-ttu-id="ba890-154">Drive ID</span><span class="sxs-lookup"><span data-stu-id="ba890-154">Drive ID</span></span>
    - <span data-ttu-id="ba890-155">Carrier account number</span><span class="sxs-lookup"><span data-stu-id="ba890-155">Carrier account number</span></span>
    - <span data-ttu-id="ba890-156">Shipping tracking number</span><span class="sxs-lookup"><span data-stu-id="ba890-156">Shipping tracking number</span></span>

    <span data-ttu-id="ba890-157">The order details are deleted by the Data Box service when the job completes or when you delete the order.</span><span class="sxs-lookup"><span data-stu-id="ba890-157">The order details are deleted by the Data Box service when the job completes or when you delete the order.</span></span>

- <span data-ttu-id="ba890-158">**Shipping address** – After the order is placed, Data Box service provides the shipping address to third party carriers such as UPS or DHL.</span><span class="sxs-lookup"><span data-stu-id="ba890-158">**Shipping address** – After the order is placed, Data Box service provides the shipping address to third party carriers such as UPS or DHL.</span></span> 

<span data-ttu-id="ba890-159">For more information, review the Microsoft Privacy policy at [Trust Center](https://www.microsoft.com/trustcenter).</span><span class="sxs-lookup"><span data-stu-id="ba890-159">For more information, review the Microsoft Privacy policy at [Trust Center](https://www.microsoft.com/trustcenter).</span></span>


## <a name="next-steps"></a><span data-ttu-id="ba890-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="ba890-160">Next steps</span></span>

- <span data-ttu-id="ba890-161">Review the [Data Box Disk requirements](data-box-disk-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="ba890-161">Review the [Data Box Disk requirements](data-box-disk-system-requirements.md).</span></span>
- <span data-ttu-id="ba890-162">Understand the [Data Box Disk limits](data-box-disk-limits.md).</span><span class="sxs-lookup"><span data-stu-id="ba890-162">Understand the [Data Box Disk limits](data-box-disk-limits.md).</span></span>
- <span data-ttu-id="ba890-163">Quickly deploy [Azure Data Box Disk](data-box-disk-quickstart-portal.md) in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ba890-163">Quickly deploy [Azure Data Box Disk](data-box-disk-quickstart-portal.md) in Azure portal.</span></span>
