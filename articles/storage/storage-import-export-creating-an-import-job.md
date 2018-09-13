---
title: Create an Import Job for Azure Import/Export | Microsoft Docs
description: Learn how to create an import for the Microsoft Azure Import/Export service.
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: ''
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: d373d2a0e601f2796719fc5efb8761f276ab24d9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556442"
---
# <a name="creating-an-import-job-for-the-azure-importexport-service"></a><span data-ttu-id="c0b72-103">Creating an import job for the Azure Import/Export service</span><span class="sxs-lookup"><span data-stu-id="c0b72-103">Creating an import job for the Azure Import/Export service</span></span>

<span data-ttu-id="c0b72-104">Creating an import job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="c0b72-104">Creating an import job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="c0b72-105">Preparing drives with the Azure Import/Export Tool.</span><span class="sxs-lookup"><span data-stu-id="c0b72-105">Preparing drives with the Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="c0b72-106">Obtaining the location to which to ship the drive.</span><span class="sxs-lookup"><span data-stu-id="c0b72-106">Obtaining the location to which to ship the drive.</span></span>

-   <span data-ttu-id="c0b72-107">Creating the import job.</span><span class="sxs-lookup"><span data-stu-id="c0b72-107">Creating the import job.</span></span>

-   <span data-ttu-id="c0b72-108">Shipping the drives to Microsoft via a supported carrier service.</span><span class="sxs-lookup"><span data-stu-id="c0b72-108">Shipping the drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="c0b72-109">Updating the import job with the shipping details.</span><span class="sxs-lookup"><span data-stu-id="c0b72-109">Updating the import job with the shipping details.</span></span>

 <span data-ttu-id="c0b72-110">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure  portal](https://portal.azure.com/) to create and manage import and export jobs.</span><span class="sxs-lookup"><span data-stu-id="c0b72-110">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure  portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-the-azure-importexport-tool"></a><span data-ttu-id="c0b72-111">Preparing drives with the Azure Import/Export Tool</span><span class="sxs-lookup"><span data-stu-id="c0b72-111">Preparing drives with the Azure Import/Export Tool</span></span>

<span data-ttu-id="c0b72-112">The steps to prepare drives for an import job are the same whether you create the jobvia the portal or via the REST API.</span><span class="sxs-lookup"><span data-stu-id="c0b72-112">The steps to prepare drives for an import job are the same whether you create the jobvia the portal or via the REST API.</span></span>

<span data-ttu-id="c0b72-113">Below is a brief overview of drive preparation.</span><span class="sxs-lookup"><span data-stu-id="c0b72-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="c0b72-114">Refer to the [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span><span class="sxs-lookup"><span data-stu-id="c0b72-114">Refer to the [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="c0b72-115">You can download the Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span><span class="sxs-lookup"><span data-stu-id="c0b72-115">You can download the Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="c0b72-116">Preparing your drive involves:</span><span class="sxs-lookup"><span data-stu-id="c0b72-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="c0b72-117">Identifying the data to be imported.</span><span class="sxs-lookup"><span data-stu-id="c0b72-117">Identifying the data to be imported.</span></span>

-   <span data-ttu-id="c0b72-118">Identifying the destination blobs in Windows Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c0b72-118">Identifying the destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="c0b72-119">Using the Azure Import/Export Tool to copy your data to one or more hard drives.</span><span class="sxs-lookup"><span data-stu-id="c0b72-119">Using the Azure Import/Export Tool to copy your data to one or more hard drives.</span></span>

 <span data-ttu-id="c0b72-120">The Azure Import/Export Tool will also generate a manifest file for each of the drives as it is prepared.</span><span class="sxs-lookup"><span data-stu-id="c0b72-120">The Azure Import/Export Tool will also generate a manifest file for each of the drives as it is prepared.</span></span> <span data-ttu-id="c0b72-121">A manifest file contains:</span><span class="sxs-lookup"><span data-stu-id="c0b72-121">A manifest file contains:</span></span>

-   <span data-ttu-id="c0b72-122">An enumeration of all the files intended for upload and the mappings from these files to blobs.</span><span class="sxs-lookup"><span data-stu-id="c0b72-122">An enumeration of all the files intended for upload and the mappings from these files to blobs.</span></span>

-   <span data-ttu-id="c0b72-123">Checksums of the segments of each file.</span><span class="sxs-lookup"><span data-stu-id="c0b72-123">Checksums of the segments of each file.</span></span>

-   <span data-ttu-id="c0b72-124">Information about the metadata and properties to associate with each blob.</span><span class="sxs-lookup"><span data-stu-id="c0b72-124">Information about the metadata and properties to associate with each blob.</span></span>

-   <span data-ttu-id="c0b72-125">A listing of the action to take if a blob that is being uploaded has the same name as an existing blob in the container.</span><span class="sxs-lookup"><span data-stu-id="c0b72-125">A listing of the action to take if a blob that is being uploaded has the same name as an existing blob in the container.</span></span> <span data-ttu-id="c0b72-126">Possible options are: a) overwrite the blob with the file, b) keep the existing blob and skip uploading the file, c) append a suffix to the name so that it does not conflict with other files.</span><span class="sxs-lookup"><span data-stu-id="c0b72-126">Possible options are: a) overwrite the blob with the file, b) keep the existing blob and skip uploading the file, c) append a suffix to the name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="c0b72-127">Obtaining your shipping location</span><span class="sxs-lookup"><span data-stu-id="c0b72-127">Obtaining your shipping location</span></span>

<span data-ttu-id="c0b72-128">Before creating an import job, you need to obtain a shipping location name and address by calling the [List Locations](/rest/api/storageimportexport/listlocations) operation.</span><span class="sxs-lookup"><span data-stu-id="c0b72-128">Before creating an import job, you need to obtain a shipping location name and address by calling the [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="c0b72-129">`List Locations` will return a list of locations and their mailing addresses.</span><span class="sxs-lookup"><span data-stu-id="c0b72-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="c0b72-130">You can select a location from the returned list and ship your hard drives to that address.</span><span class="sxs-lookup"><span data-stu-id="c0b72-130">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="c0b72-131">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span><span class="sxs-lookup"><span data-stu-id="c0b72-131">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

 <span data-ttu-id="c0b72-132">Follow the steps below to obtain the shipping location:</span><span class="sxs-lookup"><span data-stu-id="c0b72-132">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="c0b72-133">Identify the name of the location of your storage account.</span><span class="sxs-lookup"><span data-stu-id="c0b72-133">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="c0b72-134">This value can be found under the **Location** field on the storage account's **Dashboard** in the Azure portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="c0b72-134">This value can be found under the **Location** field on the storage account's **Dashboard** in the Azure portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="c0b72-135">Retrieve the location that is available to process this storage account by calling the `Get Location` operation.</span><span class="sxs-lookup"><span data-stu-id="c0b72-135">Retrieve the location that is available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="c0b72-136">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span><span class="sxs-lookup"><span data-stu-id="c0b72-136">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="c0b72-137">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span><span class="sxs-lookup"><span data-stu-id="c0b72-137">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="c0b72-138">The original location might be temporarily closed for maintenance.</span><span class="sxs-lookup"><span data-stu-id="c0b72-138">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-import-job"></a><span data-ttu-id="c0b72-139">Creating the import job</span><span class="sxs-lookup"><span data-stu-id="c0b72-139">Creating the import job</span></span>
<span data-ttu-id="c0b72-140">To create the import job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span><span class="sxs-lookup"><span data-stu-id="c0b72-140">To create the import job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="c0b72-141">You will need to provide the following information:</span><span class="sxs-lookup"><span data-stu-id="c0b72-141">You will need to provide the following information:</span></span>

-   <span data-ttu-id="c0b72-142">A name for the job.</span><span class="sxs-lookup"><span data-stu-id="c0b72-142">A name for the job.</span></span>

-   <span data-ttu-id="c0b72-143">The storage account name.</span><span class="sxs-lookup"><span data-stu-id="c0b72-143">The storage account name.</span></span>

-   <span data-ttu-id="c0b72-144">The shipping location name, obtained from the previous step.</span><span class="sxs-lookup"><span data-stu-id="c0b72-144">The shipping location name, obtained from the previous step.</span></span>

-   <span data-ttu-id="c0b72-145">A job type (Import).</span><span class="sxs-lookup"><span data-stu-id="c0b72-145">A job type (Import).</span></span>

-   <span data-ttu-id="c0b72-146">The return address where the drives should be sent after the import job has completed.</span><span class="sxs-lookup"><span data-stu-id="c0b72-146">The return address where the drives should be sent after the import job has completed.</span></span>

-   <span data-ttu-id="c0b72-147">The list of drives in the job.</span><span class="sxs-lookup"><span data-stu-id="c0b72-147">The list of drives in the job.</span></span> <span data-ttu-id="c0b72-148">For each drive, you must include the following information that was obtained during the drive preparation step:</span><span class="sxs-lookup"><span data-stu-id="c0b72-148">For each drive, you must include the following information that was obtained during the drive preparation step:</span></span>

    -   <span data-ttu-id="c0b72-149">The drive Id</span><span class="sxs-lookup"><span data-stu-id="c0b72-149">The drive Id</span></span>

    -   <span data-ttu-id="c0b72-150">The BitLocker key</span><span class="sxs-lookup"><span data-stu-id="c0b72-150">The BitLocker key</span></span>

    -   <span data-ttu-id="c0b72-151">The manifest file relative path on the hard drive</span><span class="sxs-lookup"><span data-stu-id="c0b72-151">The manifest file relative path on the hard drive</span></span>

    -   <span data-ttu-id="c0b72-152">The Base16 encoded manifest file MD5 hash</span><span class="sxs-lookup"><span data-stu-id="c0b72-152">The Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="c0b72-153">Shipping your drives</span><span class="sxs-lookup"><span data-stu-id="c0b72-153">Shipping your drives</span></span>
<span data-ttu-id="c0b72-154">You must ship your drives to the address that you obtained from the previous step, and you must provide the Import/Export service with the tracking number of the package.</span><span class="sxs-lookup"><span data-stu-id="c0b72-154">You must ship your drives to the address that you obtained from the previous step, and you must provide the Import/Export service with the tracking number of the package.</span></span>

> [!NOTE]
>  <span data-ttu-id="c0b72-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span><span class="sxs-lookup"><span data-stu-id="c0b72-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-import-job-with-your-shipping-information"></a><span data-ttu-id="c0b72-156">Updating the import job with your shipping information</span><span class="sxs-lookup"><span data-stu-id="c0b72-156">Updating the import job with your shipping information</span></span>
<span data-ttu-id="c0b72-157">After you have your tracking number, call the [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation to update the shipping carrier name, the tracking number for the job, and the carrier account number for return shipping.</span><span class="sxs-lookup"><span data-stu-id="c0b72-157">After you have your tracking number, call the [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation to update the shipping carrier name, the tracking number for the job, and the carrier account number for return shipping.</span></span> <span data-ttu-id="c0b72-158">You can optionally specify the number of drives and the shipping date as well.</span><span class="sxs-lookup"><span data-stu-id="c0b72-158">You can optionally specify the number of drives and the shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0b72-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="c0b72-159">Next steps</span></span>

* [<span data-ttu-id="c0b72-160">Using the Import/Export service REST API</span><span class="sxs-lookup"><span data-stu-id="c0b72-160">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
