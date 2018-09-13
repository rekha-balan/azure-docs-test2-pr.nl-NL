---
title: Create an export Job for Azure Import/Export | Microsoft Docs
description: Learn how to create an export job for the Microsoft Azure Import/Export service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: ''
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: bdeac373aa8270bd9de8f135ec7166d744fd83ae
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549218"
---
# <a name="creating-an-export-job-for-the-azure-importexport-service"></a><span data-ttu-id="e618c-103">Creating an export job for the Azure Import/Export service</span><span class="sxs-lookup"><span data-stu-id="e618c-103">Creating an export job for the Azure Import/Export service</span></span>
<span data-ttu-id="e618c-104">Creating an export job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="e618c-104">Creating an export job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="e618c-105">Selecting the blobs to export.</span><span class="sxs-lookup"><span data-stu-id="e618c-105">Selecting the blobs to export.</span></span>

-   <span data-ttu-id="e618c-106">Obtaining a shipping location.</span><span class="sxs-lookup"><span data-stu-id="e618c-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="e618c-107">Creating the export job.</span><span class="sxs-lookup"><span data-stu-id="e618c-107">Creating the export job.</span></span>

-   <span data-ttu-id="e618c-108">Shipping your empty drives to Microsoft via a supported carrier service.</span><span class="sxs-lookup"><span data-stu-id="e618c-108">Shipping your empty drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="e618c-109">Updating the export job with the package information.</span><span class="sxs-lookup"><span data-stu-id="e618c-109">Updating the export job with the package information.</span></span>

-   <span data-ttu-id="e618c-110">Receiving the drives back from Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e618c-110">Receiving the drives back from Microsoft.</span></span>

 <span data-ttu-id="e618c-111">See [Using the Windows Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure portal](https://portal.azure.com/) to create and manage import and export jobs.</span><span class="sxs-lookup"><span data-stu-id="e618c-111">See [Using the Windows Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="selecting-blobs-to-export"></a><span data-ttu-id="e618c-112">Selecting blobs to export</span><span class="sxs-lookup"><span data-stu-id="e618c-112">Selecting blobs to export</span></span>
 <span data-ttu-id="e618c-113">To create an export job, you will need to provide a list of blobs that you want to export from your storage account.</span><span class="sxs-lookup"><span data-stu-id="e618c-113">To create an export job, you will need to provide a list of blobs that you want to export from your storage account.</span></span> <span data-ttu-id="e618c-114">There are a few ways to select blobs to be exported:</span><span class="sxs-lookup"><span data-stu-id="e618c-114">There are a few ways to select blobs to be exported:</span></span>

-   <span data-ttu-id="e618c-115">You can use a relative blob path to select a single blob and all of its snapshots.</span><span class="sxs-lookup"><span data-stu-id="e618c-115">You can use a relative blob path to select a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="e618c-116">You can use a relative blob path to select a single blob excluding its snapshots.</span><span class="sxs-lookup"><span data-stu-id="e618c-116">You can use a relative blob path to select a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="e618c-117">You can use a relative blob path and a snapshot time to select a single snapshot.</span><span class="sxs-lookup"><span data-stu-id="e618c-117">You can use a relative blob path and a snapshot time to select a single snapshot.</span></span>

-   <span data-ttu-id="e618c-118">You can use a blob prefix to select all blobs and snapshots with the given prefix.</span><span class="sxs-lookup"><span data-stu-id="e618c-118">You can use a blob prefix to select all blobs and snapshots with the given prefix.</span></span>

-   <span data-ttu-id="e618c-119">You can export all blobs and snapshots in the storage account.</span><span class="sxs-lookup"><span data-stu-id="e618c-119">You can export all blobs and snapshots in the storage account.</span></span>

 <span data-ttu-id="e618c-120">For more information about specifying blobs to export, see the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span><span class="sxs-lookup"><span data-stu-id="e618c-120">For more information about specifying blobs to export, see the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="e618c-121">Obtaining your shipping location</span><span class="sxs-lookup"><span data-stu-id="e618c-121">Obtaining your shipping location</span></span>
<span data-ttu-id="e618c-122">Before creating an export job, you need to obtain a shipping location name and address by calling the [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span><span class="sxs-lookup"><span data-stu-id="e618c-122">Before creating an export job, you need to obtain a shipping location name and address by calling the [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="e618c-123">`List Locations` will return a list of locations and their mailing addresses.</span><span class="sxs-lookup"><span data-stu-id="e618c-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="e618c-124">You can select a location from the returned list and ship your hard drives to that address.</span><span class="sxs-lookup"><span data-stu-id="e618c-124">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="e618c-125">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span><span class="sxs-lookup"><span data-stu-id="e618c-125">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

<span data-ttu-id="e618c-126">Follow the steps below to obtain the shipping location:</span><span class="sxs-lookup"><span data-stu-id="e618c-126">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="e618c-127">Identify the name of the location of your storage account.</span><span class="sxs-lookup"><span data-stu-id="e618c-127">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="e618c-128">This value can be found under the **Location** field on the storage account's **Dashboard** in the classic portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="e618c-128">This value can be found under the **Location** field on the storage account's **Dashboard** in the classic portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="e618c-129">Retrieve the location that are available to process this storage account by calling the `Get Location` operation.</span><span class="sxs-lookup"><span data-stu-id="e618c-129">Retrieve the location that are available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="e618c-130">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span><span class="sxs-lookup"><span data-stu-id="e618c-130">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="e618c-131">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span><span class="sxs-lookup"><span data-stu-id="e618c-131">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="e618c-132">The original location might be temporarily closed for maintenance.</span><span class="sxs-lookup"><span data-stu-id="e618c-132">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-export-job"></a><span data-ttu-id="e618c-133">Creating the export job</span><span class="sxs-lookup"><span data-stu-id="e618c-133">Creating the export job</span></span>
 <span data-ttu-id="e618c-134">To create the export job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span><span class="sxs-lookup"><span data-stu-id="e618c-134">To create the export job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="e618c-135">You will need to provide the following information:</span><span class="sxs-lookup"><span data-stu-id="e618c-135">You will need to provide the following information:</span></span>

-   <span data-ttu-id="e618c-136">A name for the job.</span><span class="sxs-lookup"><span data-stu-id="e618c-136">A name for the job.</span></span>

-   <span data-ttu-id="e618c-137">The storage account name.</span><span class="sxs-lookup"><span data-stu-id="e618c-137">The storage account name.</span></span>

-   <span data-ttu-id="e618c-138">The shipping location name, obtained in the previous step.</span><span class="sxs-lookup"><span data-stu-id="e618c-138">The shipping location name, obtained in the previous step.</span></span>

-   <span data-ttu-id="e618c-139">A job type (Export).</span><span class="sxs-lookup"><span data-stu-id="e618c-139">A job type (Export).</span></span>

-   <span data-ttu-id="e618c-140">The return address where the drives should be sent after the export job has completed.</span><span class="sxs-lookup"><span data-stu-id="e618c-140">The return address where the drives should be sent after the export job has completed.</span></span>

-   <span data-ttu-id="e618c-141">The list of blobs (or blob prefixes) to be exported.</span><span class="sxs-lookup"><span data-stu-id="e618c-141">The list of blobs (or blob prefixes) to be exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="e618c-142">Shipping your drives</span><span class="sxs-lookup"><span data-stu-id="e618c-142">Shipping your drives</span></span>
 <span data-ttu-id="e618c-143">Next, use the Azure Import/Export Tool to determine the number of drives you need to send, based on the blobs you have selected to be exported and the drive size.</span><span class="sxs-lookup"><span data-stu-id="e618c-143">Next, use the Azure Import/Export Tool to determine the number of drives you need to send, based on the blobs you have selected to be exported and the drive size.</span></span> <span data-ttu-id="e618c-144">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span><span class="sxs-lookup"><span data-stu-id="e618c-144">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="e618c-145">Package the drives in a single package and ship them to the address obtained in the earlier step.</span><span class="sxs-lookup"><span data-stu-id="e618c-145">Package the drives in a single package and ship them to the address obtained in the earlier step.</span></span> <span data-ttu-id="e618c-146">Note the tracking number of your package for the next step.</span><span class="sxs-lookup"><span data-stu-id="e618c-146">Note the tracking number of your package for the next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="e618c-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span><span class="sxs-lookup"><span data-stu-id="e618c-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-export-job-with-your-package-information"></a><span data-ttu-id="e618c-148">Updating the export job with your package information</span><span class="sxs-lookup"><span data-stu-id="e618c-148">Updating the export job with your package information</span></span>
 <span data-ttu-id="e618c-149">After you have your tracking number, call the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation to updated the carrier name and tracking number for the job.</span><span class="sxs-lookup"><span data-stu-id="e618c-149">After you have your tracking number, call the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation to updated the carrier name and tracking number for the job.</span></span> <span data-ttu-id="e618c-150">You can optionally specify the number of drives, the return address, and the shipping date as well.</span><span class="sxs-lookup"><span data-stu-id="e618c-150">You can optionally specify the number of drives, the return address, and the shipping date as well.</span></span>

## <a name="receiving-the-package"></a><span data-ttu-id="e618c-151">Receiving the package</span><span class="sxs-lookup"><span data-stu-id="e618c-151">Receiving the package</span></span>
 <span data-ttu-id="e618c-152">After your export job has been processed, your drives will be returned to you with your encrypted data.</span><span class="sxs-lookup"><span data-stu-id="e618c-152">After your export job has been processed, your drives will be returned to you with your encrypted data.</span></span> <span data-ttu-id="e618c-153">You can retrieve the BitLocker key for each of the drives by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span><span class="sxs-lookup"><span data-stu-id="e618c-153">You can retrieve the BitLocker key for each of the drives by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="e618c-154">You can then unlock the drive using the key.</span><span class="sxs-lookup"><span data-stu-id="e618c-154">You can then unlock the drive using the key.</span></span> <span data-ttu-id="e618c-155">The drive manifest file on each drive contains the list of files on the drive, as well as the original blob address for each file.</span><span class="sxs-lookup"><span data-stu-id="e618c-155">The drive manifest file on each drive contains the list of files on the drive, as well as the original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e618c-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="e618c-156">Next steps</span></span>

* [<span data-ttu-id="e618c-157">Using the Import/Export service REST API</span><span class="sxs-lookup"><span data-stu-id="e618c-157">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
