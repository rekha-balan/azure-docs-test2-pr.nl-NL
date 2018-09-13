---
title: Microsoft Azure StorSimple Data Manager overview | Microsoft Docs
description: Provides an overview of the StorSimple Data Manager serivce
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: ''
ms.assetid: ''
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/21/2018
ms.author: vidarmsft
ms.openlocfilehash: 5845fd246b20d29739eb6d60bbc8621489ccc0d6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44784373"
---
# <a name="storsimple-data-manager-solution-overview"></a><span data-ttu-id="1133e-103">StorSimple Data Manager solution overview</span><span class="sxs-lookup"><span data-stu-id="1133e-103">StorSimple Data Manager solution overview</span></span>

## <a name="overview"></a><span data-ttu-id="1133e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="1133e-104">Overview</span></span>

<span data-ttu-id="1133e-105">Microsoft Azure StorSimple uses cloud storage as an extension of the on-premises solution and automatically tiers data across on-premises storage and the cloud.</span><span class="sxs-lookup"><span data-stu-id="1133e-105">Microsoft Azure StorSimple uses cloud storage as an extension of the on-premises solution and automatically tiers data across on-premises storage and the cloud.</span></span> <span data-ttu-id="1133e-106">Data is stored in the cloud in a deduped and compressed format for maximum efficiency and to lower costs.</span><span class="sxs-lookup"><span data-stu-id="1133e-106">Data is stored in the cloud in a deduped and compressed format for maximum efficiency and to lower costs.</span></span> <span data-ttu-id="1133e-107">As the data is stored in StorSimple format, it is not readily consumable by other cloud applications that you may want to use.</span><span class="sxs-lookup"><span data-stu-id="1133e-107">As the data is stored in StorSimple format, it is not readily consumable by other cloud applications that you may want to use.</span></span>

<span data-ttu-id="1133e-108">The StorSimple Data Manager enables you to seamlessly access and use the StorSimple format data in the cloud.</span><span class="sxs-lookup"><span data-stu-id="1133e-108">The StorSimple Data Manager enables you to seamlessly access and use the StorSimple format data in the cloud.</span></span> <span data-ttu-id="1133e-109">It does this by transforming StorSimple format into native blobs and files, which you can use with other services such as Azure Media Services, Azure HDInsights, and Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="1133e-109">It does this by transforming StorSimple format into native blobs and files, which you can use with other services such as Azure Media Services, Azure HDInsights, and Azure Machine Learning.</span></span>

<span data-ttu-id="1133e-110">This article provides an overview of the StorSimple Data Manager solution.</span><span class="sxs-lookup"><span data-stu-id="1133e-110">This article provides an overview of the StorSimple Data Manager solution.</span></span> <span data-ttu-id="1133e-111">It also explains how you can use this service to write applications that use StorSimple data and other Azure services in the cloud.</span><span class="sxs-lookup"><span data-stu-id="1133e-111">It also explains how you can use this service to write applications that use StorSimple data and other Azure services in the cloud.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="1133e-112">How it works?</span><span class="sxs-lookup"><span data-stu-id="1133e-112">How it works?</span></span>

<span data-ttu-id="1133e-113">The StorSimple Data Manager service identifies StorSimple data in the cloud from a StorSimple 8000 series on-premises device.</span><span class="sxs-lookup"><span data-stu-id="1133e-113">The StorSimple Data Manager service identifies StorSimple data in the cloud from a StorSimple 8000 series on-premises device.</span></span> <span data-ttu-id="1133e-114">The StorSimple data in the cloud is deduped, compressed StorSimple format.</span><span class="sxs-lookup"><span data-stu-id="1133e-114">The StorSimple data in the cloud is deduped, compressed StorSimple format.</span></span> <span data-ttu-id="1133e-115">The Data Manager service provides APIs to extract the StorSimple format data and transform it into other formats such as Azure blobs and Azure Files.</span><span class="sxs-lookup"><span data-stu-id="1133e-115">The Data Manager service provides APIs to extract the StorSimple format data and transform it into other formats such as Azure blobs and Azure Files.</span></span> <span data-ttu-id="1133e-116">This transformed data is then readily consumed by Azure HDInsight and Azure Media services.</span><span class="sxs-lookup"><span data-stu-id="1133e-116">This transformed data is then readily consumed by Azure HDInsight and Azure Media services.</span></span> <span data-ttu-id="1133e-117">The data transformation thus enables these services to operate upon the transformed StorSimple data from StorSimple 8000 series on-premises device.</span><span class="sxs-lookup"><span data-stu-id="1133e-117">The data transformation thus enables these services to operate upon the transformed StorSimple data from StorSimple 8000 series on-premises device.</span></span> <span data-ttu-id="1133e-118">This flow is illustrated in the following diagram.</span><span class="sxs-lookup"><span data-stu-id="1133e-118">This flow is illustrated in the following diagram.</span></span>

![High-level diagram](./media/storsimple-data-manager-overview/storsimple-data-manager-overview2.png)


## <a name="data-manager-use-cases"></a><span data-ttu-id="1133e-120">Data Manager use cases</span><span class="sxs-lookup"><span data-stu-id="1133e-120">Data Manager use cases</span></span>

<span data-ttu-id="1133e-121">You can use the Data Manager with Azure Functions, Azure Automation, and Azure Data Factory to have workflows running on your data as it comes into StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1133e-121">You can use the Data Manager with Azure Functions, Azure Automation, and Azure Data Factory to have workflows running on your data as it comes into StorSimple.</span></span> <span data-ttu-id="1133e-122">You might want to process your media content that you store on StorSimple with Azure Media Services, or run a Machine Learning algorithm on that data, or bring up a Hadoop cluster to analyze the data that you store on StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1133e-122">You might want to process your media content that you store on StorSimple with Azure Media Services, or run a Machine Learning algorithm on that data, or bring up a Hadoop cluster to analyze the data that you store on StorSimple.</span></span> <span data-ttu-id="1133e-123">With the vast array of services available on Azure combined with the data on StorSimple, you can unlock the power of your data.</span><span class="sxs-lookup"><span data-stu-id="1133e-123">With the vast array of services available on Azure combined with the data on StorSimple, you can unlock the power of your data.</span></span>


## <a name="region-availability"></a><span data-ttu-id="1133e-124">Region availability</span><span class="sxs-lookup"><span data-stu-id="1133e-124">Region availability</span></span>

<span data-ttu-id="1133e-125">The StorSimple Data Manager is available in the following 7 regions:</span><span class="sxs-lookup"><span data-stu-id="1133e-125">The StorSimple Data Manager is available in the following 7 regions:</span></span>

 - <span data-ttu-id="1133e-126">Southeast Asia</span><span class="sxs-lookup"><span data-stu-id="1133e-126">Southeast Asia</span></span>
 - <span data-ttu-id="1133e-127">East US</span><span class="sxs-lookup"><span data-stu-id="1133e-127">East US</span></span>
 - <span data-ttu-id="1133e-128">West US</span><span class="sxs-lookup"><span data-stu-id="1133e-128">West US</span></span>
 - <span data-ttu-id="1133e-129">West US 2</span><span class="sxs-lookup"><span data-stu-id="1133e-129">West US 2</span></span>
 - <span data-ttu-id="1133e-130">West Central US</span><span class="sxs-lookup"><span data-stu-id="1133e-130">West Central US</span></span>
 - <span data-ttu-id="1133e-131">North Europe</span><span class="sxs-lookup"><span data-stu-id="1133e-131">North Europe</span></span>
 - <span data-ttu-id="1133e-132">West Europe</span><span class="sxs-lookup"><span data-stu-id="1133e-132">West Europe</span></span>

<span data-ttu-id="1133e-133">However, the StorSimple Data Manager can be used to transform data in the following regions.</span><span class="sxs-lookup"><span data-stu-id="1133e-133">However, the StorSimple Data Manager can be used to transform data in the following regions.</span></span> 

![Regions available for data](./media/storsimple-data-manager-overview/data-manager-job-definition-different-regions-m.png)

<span data-ttu-id="1133e-135">This set is larger because the resource deployment in any of the above regions is capable of bringing up the transformation process in the below regions.</span><span class="sxs-lookup"><span data-stu-id="1133e-135">This set is larger because the resource deployment in any of the above regions is capable of bringing up the transformation process in the below regions.</span></span> <span data-ttu-id="1133e-136">So, as long as your data resides in any one of the 19 regions, you can transform your data using this service.</span><span class="sxs-lookup"><span data-stu-id="1133e-136">So, as long as your data resides in any one of the 19 regions, you can transform your data using this service.</span></span>


## <a name="choosing-a-region"></a><span data-ttu-id="1133e-137">Choosing a region</span><span class="sxs-lookup"><span data-stu-id="1133e-137">Choosing a region</span></span>

<span data-ttu-id="1133e-138">We recommend that:</span><span class="sxs-lookup"><span data-stu-id="1133e-138">We recommend that:</span></span>
 - <span data-ttu-id="1133e-139">Your source storage account (the one associated with your StorSimple device) and target storage account (where you want the data in native format) be in the same Azure region.</span><span class="sxs-lookup"><span data-stu-id="1133e-139">Your source storage account (the one associated with your StorSimple device) and target storage account (where you want the data in native format) be in the same Azure region.</span></span>
 - <span data-ttu-id="1133e-140">You bring up your Data Manager and job definition in the region that contains the StorSimple storage account.</span><span class="sxs-lookup"><span data-stu-id="1133e-140">You bring up your Data Manager and job definition in the region that contains the StorSimple storage account.</span></span> <span data-ttu-id="1133e-141">If this is not possible, bring up the Data Manager in the nearest Azure region and then create the Job Definition in the same region as your StorSimple storage account.</span><span class="sxs-lookup"><span data-stu-id="1133e-141">If this is not possible, bring up the Data Manager in the nearest Azure region and then create the Job Definition in the same region as your StorSimple storage account.</span></span> 

    <span data-ttu-id="1133e-142">If your StorSimple storage account is not in the 26 regions that support job definition creation, we recommend that you do not run StorSimple Data Manager as you see long latencies and potentially high egress charges.</span><span class="sxs-lookup"><span data-stu-id="1133e-142">If your StorSimple storage account is not in the 26 regions that support job definition creation, we recommend that you do not run StorSimple Data Manager as you see long latencies and potentially high egress charges.</span></span>

## <a name="security-considerations"></a><span data-ttu-id="1133e-143">Security considerations</span><span class="sxs-lookup"><span data-stu-id="1133e-143">Security considerations</span></span>

<span data-ttu-id="1133e-144">The StorSimple Data Manager needs the service data encryption key to transform from StorSimple format to native format.</span><span class="sxs-lookup"><span data-stu-id="1133e-144">The StorSimple Data Manager needs the service data encryption key to transform from StorSimple format to native format.</span></span> <span data-ttu-id="1133e-145">The service data encryption key is generated when the first device registers with the StorSimple service.</span><span class="sxs-lookup"><span data-stu-id="1133e-145">The service data encryption key is generated when the first device registers with the StorSimple service.</span></span> <span data-ttu-id="1133e-146">For more information on this key, go to [StorSimple security](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="1133e-146">For more information on this key, go to [StorSimple security](storsimple-8000-security.md).</span></span>

<span data-ttu-id="1133e-147">The service data encryption key provided as an input is stored in a key vault that is created when you create a Data Manager.</span><span class="sxs-lookup"><span data-stu-id="1133e-147">The service data encryption key provided as an input is stored in a key vault that is created when you create a Data Manager.</span></span> <span data-ttu-id="1133e-148">The vault resides in the same Azure region as your StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="1133e-148">The vault resides in the same Azure region as your StorSimple Data Manager.</span></span> <span data-ttu-id="1133e-149">This key is deleted when you delete your Data Manager service.</span><span class="sxs-lookup"><span data-stu-id="1133e-149">This key is deleted when you delete your Data Manager service.</span></span>

<span data-ttu-id="1133e-150">This key is used by the compute resources to perform the transformation.</span><span class="sxs-lookup"><span data-stu-id="1133e-150">This key is used by the compute resources to perform the transformation.</span></span> <span data-ttu-id="1133e-151">These compute resources are located in the same Azure region as your job definition.</span><span class="sxs-lookup"><span data-stu-id="1133e-151">These compute resources are located in the same Azure region as your job definition.</span></span> <span data-ttu-id="1133e-152">This region may, or may not be the same as the region where you bring up your Data Manager.</span><span class="sxs-lookup"><span data-stu-id="1133e-152">This region may, or may not be the same as the region where you bring up your Data Manager.</span></span>

<span data-ttu-id="1133e-153">If your Data Manager region is different from your job definition region, it is important that you understand what data/metadata resides in each of these regions.</span><span class="sxs-lookup"><span data-stu-id="1133e-153">If your Data Manager region is different from your job definition region, it is important that you understand what data/metadata resides in each of these regions.</span></span> <span data-ttu-id="1133e-154">The following diagram illustrates the effect of having different regions for Data Manager and job definition.</span><span class="sxs-lookup"><span data-stu-id="1133e-154">The following diagram illustrates the effect of having different regions for Data Manager and job definition.</span></span>

![Service and job definition in different regions](./media/storsimple-data-manager-overview/data-manager-job-different-regions.png)

## <a name="managing-personal-information"></a><span data-ttu-id="1133e-156">Managing personal information</span><span class="sxs-lookup"><span data-stu-id="1133e-156">Managing personal information</span></span>

<span data-ttu-id="1133e-157">The StorSimple Data Manager does not collect or display any personal information.</span><span class="sxs-lookup"><span data-stu-id="1133e-157">The StorSimple Data Manager does not collect or display any personal information.</span></span> <span data-ttu-id="1133e-158">For more information, review the Microsoft Privacy policy at [Trust Center](https://www.microsoft.com/trustcenter).</span><span class="sxs-lookup"><span data-stu-id="1133e-158">For more information, review the Microsoft Privacy policy at [Trust Center](https://www.microsoft.com/trustcenter).</span></span>

## <a name="known-limitations"></a><span data-ttu-id="1133e-159">Known Limitations</span><span class="sxs-lookup"><span data-stu-id="1133e-159">Known Limitations</span></span>

<span data-ttu-id="1133e-160">The service currently has the following limitations:</span><span class="sxs-lookup"><span data-stu-id="1133e-160">The service currently has the following limitations:</span></span>
- <span data-ttu-id="1133e-161">The StorSimple Data Manager currently does not work with volumes that are bitlocker encrypted.</span><span class="sxs-lookup"><span data-stu-id="1133e-161">The StorSimple Data Manager currently does not work with volumes that are bitlocker encrypted.</span></span> <span data-ttu-id="1133e-162">You will see job failures if you try to run the service with an encrypted drive.</span><span class="sxs-lookup"><span data-stu-id="1133e-162">You will see job failures if you try to run the service with an encrypted drive.</span></span>
- <span data-ttu-id="1133e-163">Some metadata of files (including ACLs) will not be retained in the transformed data.</span><span class="sxs-lookup"><span data-stu-id="1133e-163">Some metadata of files (including ACLs) will not be retained in the transformed data.</span></span>
- <span data-ttu-id="1133e-164">This service works only with NTFS volumes.</span><span class="sxs-lookup"><span data-stu-id="1133e-164">This service works only with NTFS volumes.</span></span>
- <span data-ttu-id="1133e-165">File path lengths need to be less than 256 characters else the job will fail.</span><span class="sxs-lookup"><span data-stu-id="1133e-165">File path lengths need to be less than 256 characters else the job will fail.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1133e-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="1133e-166">Next steps</span></span>

<span data-ttu-id="1133e-167">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="1133e-167">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>
