---
title: Microsoft Azure Data Box Disk system requirements| Microsoft Docs
description: Learn about the software and networking requirements for your Azure Data Box Disk
services: databox
documentationcenter: NA
author: alkohli
manager: twooley
editor: ''
ms.assetid: ''
ms.service: databox
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/06/2018
ms.author: alkohli
ms.openlocfilehash: aaa4e4bb24ca42adb9d283e6286dbef879bcb1ea
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867126"
---
# <a name="azure-data-box-disk-system-requirements-preview"></a><span data-ttu-id="66d28-103">Azure Data Box Disk system requirements (Preview)</span><span class="sxs-lookup"><span data-stu-id="66d28-103">Azure Data Box Disk system requirements (Preview)</span></span>

<span data-ttu-id="66d28-104">This article describes the important system requirements for your Microsoft Azure Data Box Disk solution and for the clients connecting to the Data Box Disk.</span><span class="sxs-lookup"><span data-stu-id="66d28-104">This article describes the important system requirements for your Microsoft Azure Data Box Disk solution and for the clients connecting to the Data Box Disk.</span></span> <span data-ttu-id="66d28-105">We recommend that you review the information carefully before you deploy your Data Box Disk, and then refer back to it as necessary during the deployment and subsequent operation.</span><span class="sxs-lookup"><span data-stu-id="66d28-105">We recommend that you review the information carefully before you deploy your Data Box Disk, and then refer back to it as necessary during the deployment and subsequent operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="66d28-106">Data Box Disk is in Preview.</span><span class="sxs-lookup"><span data-stu-id="66d28-106">Data Box Disk is in Preview.</span></span> <span data-ttu-id="66d28-107">Please review the [terms of use for the preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) before you deploy this solution.</span><span class="sxs-lookup"><span data-stu-id="66d28-107">Please review the [terms of use for the preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) before you deploy this solution.</span></span> 

<span data-ttu-id="66d28-108">The system requirements include the supported platforms for clients connecting to disks, supported storage accounts, and storage types.</span><span class="sxs-lookup"><span data-stu-id="66d28-108">The system requirements include the supported platforms for clients connecting to disks, supported storage accounts, and storage types.</span></span>


## <a name="supported-operating-systems-for-clients"></a><span data-ttu-id="66d28-109">Supported operating systems for clients</span><span class="sxs-lookup"><span data-stu-id="66d28-109">Supported operating systems for clients</span></span>

<span data-ttu-id="66d28-110">Here is a list of the supported operating systems for the disk unlock and data copy operation via the clients connected to the Data Box Disk.</span><span class="sxs-lookup"><span data-stu-id="66d28-110">Here is a list of the supported operating systems for the disk unlock and data copy operation via the clients connected to the Data Box Disk.</span></span>

| <span data-ttu-id="66d28-111">**Operating system**</span><span class="sxs-lookup"><span data-stu-id="66d28-111">**Operating system**</span></span> | <span data-ttu-id="66d28-112">**Tested versions**</span><span class="sxs-lookup"><span data-stu-id="66d28-112">**Tested versions**</span></span> |
| --- | --- |
| <span data-ttu-id="66d28-113">Windows Server</span><span class="sxs-lookup"><span data-stu-id="66d28-113">Windows Server</span></span> |<span data-ttu-id="66d28-114">2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="66d28-114">2008 R2 SP1</span></span> <br> <span data-ttu-id="66d28-115">2012</span><span class="sxs-lookup"><span data-stu-id="66d28-115">2012</span></span> <br> <span data-ttu-id="66d28-116">2012 R2</span><span class="sxs-lookup"><span data-stu-id="66d28-116">2012 R2</span></span> <br> <span data-ttu-id="66d28-117">2016</span><span class="sxs-lookup"><span data-stu-id="66d28-117">2016</span></span> |
| <span data-ttu-id="66d28-118">Windows</span><span class="sxs-lookup"><span data-stu-id="66d28-118">Windows</span></span> |<span data-ttu-id="66d28-119">7, 8, 10</span><span class="sxs-lookup"><span data-stu-id="66d28-119">7, 8, 10</span></span> |
|<span data-ttu-id="66d28-120">Linux</span><span class="sxs-lookup"><span data-stu-id="66d28-120">Linux</span></span> <br> <li> <span data-ttu-id="66d28-121">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="66d28-121">Ubuntu</span></span> </li><li> <span data-ttu-id="66d28-122">Debian</span><span class="sxs-lookup"><span data-stu-id="66d28-122">Debian</span></span> </li><li> <span data-ttu-id="66d28-123">Red Hat Enterprise Linux (RHEL)</span><span class="sxs-lookup"><span data-stu-id="66d28-123">Red Hat Enterprise Linux (RHEL)</span></span> </li><li> <span data-ttu-id="66d28-124">CentOS</span><span class="sxs-lookup"><span data-stu-id="66d28-124">CentOS</span></span>| <br><span data-ttu-id="66d28-125">14.04, 16.04, 18.04</span><span class="sxs-lookup"><span data-stu-id="66d28-125">14.04, 16.04, 18.04</span></span> <br> <span data-ttu-id="66d28-126">8.11, 9</span><span class="sxs-lookup"><span data-stu-id="66d28-126">8.11, 9</span></span> <br> <span data-ttu-id="66d28-127">7.0</span><span class="sxs-lookup"><span data-stu-id="66d28-127">7.0</span></span> <br> <span data-ttu-id="66d28-128">6.5, 6.9, 7.0, 7.5</span><span class="sxs-lookup"><span data-stu-id="66d28-128">6.5, 6.9, 7.0, 7.5</span></span> |  

## <a name="other-required-software-for-windows-clients"></a><span data-ttu-id="66d28-129">Other required software for Windows clients</span><span class="sxs-lookup"><span data-stu-id="66d28-129">Other required software for Windows clients</span></span>

<span data-ttu-id="66d28-130">For Windows client, following should also be installed.</span><span class="sxs-lookup"><span data-stu-id="66d28-130">For Windows client, following should also be installed.</span></span>

| <span data-ttu-id="66d28-131">**Software**</span><span class="sxs-lookup"><span data-stu-id="66d28-131">**Software**</span></span>| <span data-ttu-id="66d28-132">**Version**</span><span class="sxs-lookup"><span data-stu-id="66d28-132">**Version**</span></span> |
| --- | --- |
| <span data-ttu-id="66d28-133">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="66d28-133">Windows PowerShell</span></span> |<span data-ttu-id="66d28-134">5.0</span><span class="sxs-lookup"><span data-stu-id="66d28-134">5.0</span></span> |
| <span data-ttu-id="66d28-135">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="66d28-135">.NET Framework</span></span> |<span data-ttu-id="66d28-136">4.5.1</span><span class="sxs-lookup"><span data-stu-id="66d28-136">4.5.1</span></span> |
| <span data-ttu-id="66d28-137">Windows Management Framework</span><span class="sxs-lookup"><span data-stu-id="66d28-137">Windows Management Framework</span></span> |<span data-ttu-id="66d28-138">5.0</span><span class="sxs-lookup"><span data-stu-id="66d28-138">5.0</span></span>|
| <span data-ttu-id="66d28-139">BitLocker</span><span class="sxs-lookup"><span data-stu-id="66d28-139">BitLocker</span></span>| - |

## <a name="other-required-software-for-linux-clients"></a><span data-ttu-id="66d28-140">Other required software for Linux clients</span><span class="sxs-lookup"><span data-stu-id="66d28-140">Other required software for Linux clients</span></span>

<span data-ttu-id="66d28-141">For Linux client, the Data Box Disk toolset installs the following required software:</span><span class="sxs-lookup"><span data-stu-id="66d28-141">For Linux client, the Data Box Disk toolset installs the following required software:</span></span>

- <span data-ttu-id="66d28-142">dislocker</span><span class="sxs-lookup"><span data-stu-id="66d28-142">dislocker</span></span>
- <span data-ttu-id="66d28-143">OpenSSL</span><span class="sxs-lookup"><span data-stu-id="66d28-143">OpenSSL</span></span>

## <a name="supported-storage-accounts"></a><span data-ttu-id="66d28-144">Supported storage accounts</span><span class="sxs-lookup"><span data-stu-id="66d28-144">Supported storage accounts</span></span>

<span data-ttu-id="66d28-145">Here is a list of the supported storage types for the Data Box Disk.</span><span class="sxs-lookup"><span data-stu-id="66d28-145">Here is a list of the supported storage types for the Data Box Disk.</span></span>

| <span data-ttu-id="66d28-146">**Storage account**</span><span class="sxs-lookup"><span data-stu-id="66d28-146">**Storage account**</span></span> | <span data-ttu-id="66d28-147">**Notes**</span><span class="sxs-lookup"><span data-stu-id="66d28-147">**Notes**</span></span> |
| --- | --- |
| <span data-ttu-id="66d28-148">Classic</span><span class="sxs-lookup"><span data-stu-id="66d28-148">Classic</span></span> | <span data-ttu-id="66d28-149">Standard</span><span class="sxs-lookup"><span data-stu-id="66d28-149">Standard</span></span> |
| <span data-ttu-id="66d28-150">General Purpose</span><span class="sxs-lookup"><span data-stu-id="66d28-150">General Purpose</span></span>  |<span data-ttu-id="66d28-151">Standard; both V1 and V2 are supported.</span><span class="sxs-lookup"><span data-stu-id="66d28-151">Standard; both V1 and V2 are supported.</span></span> <span data-ttu-id="66d28-152">Both hot and cool tiers are supported.</span><span class="sxs-lookup"><span data-stu-id="66d28-152">Both hot and cool tiers are supported.</span></span> |


## <a name="supported-storage-types"></a><span data-ttu-id="66d28-153">Supported storage types</span><span class="sxs-lookup"><span data-stu-id="66d28-153">Supported storage types</span></span>

<span data-ttu-id="66d28-154">Here is a list of the supported storage types for the Data Box Disk.</span><span class="sxs-lookup"><span data-stu-id="66d28-154">Here is a list of the supported storage types for the Data Box Disk.</span></span>

| <span data-ttu-id="66d28-155">**File format**</span><span class="sxs-lookup"><span data-stu-id="66d28-155">**File format**</span></span> | <span data-ttu-id="66d28-156">**Notes**</span><span class="sxs-lookup"><span data-stu-id="66d28-156">**Notes**</span></span> |
| --- | --- |
| <span data-ttu-id="66d28-157">Azure block blob</span><span class="sxs-lookup"><span data-stu-id="66d28-157">Azure block blob</span></span> | |
| <span data-ttu-id="66d28-158">Azure page blob</span><span class="sxs-lookup"><span data-stu-id="66d28-158">Azure page blob</span></span>  | |


## <a name="next-step"></a><span data-ttu-id="66d28-159">Next step</span><span class="sxs-lookup"><span data-stu-id="66d28-159">Next step</span></span>

* [<span data-ttu-id="66d28-160">Deploy your Azure Data Box Disk</span><span class="sxs-lookup"><span data-stu-id="66d28-160">Deploy your Azure Data Box Disk</span></span>](data-box-disk-deploy-ordered.md)

