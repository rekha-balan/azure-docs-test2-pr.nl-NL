---
title: " Create an Azure Media Services account with the Azure portal | Microsoft Docs"
description: This tutorial walks you through the steps of creating an Azure Media Services account with the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: c551e158-aad6-47b4-931e-b46260b3ee4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/10/2017
ms.author: juliako
ms.openlocfilehash: 2ea11b42dd69ee31c84bc607b828580147d5c28b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550666"
---
# <a name="create-an-azure-media-services-account-using-the-azure-portal"></a><span data-ttu-id="d7d3d-103">Create an Azure Media Services account using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d7d3d-103">Create an Azure Media Services account using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> To complete this tutorial, you need an Azure account. For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

<span data-ttu-id="d7d3d-109">The Azure portal provides a way to quickly create an Azure Media Services (AMS) account.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-109">The Azure portal provides a way to quickly create an Azure Media Services (AMS) account.</span></span> <span data-ttu-id="d7d3d-110">You can use your account to access Media Services that enable you to store, encrypt, encode, manage, and stream media content in Azure.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-110">You can use your account to access Media Services that enable you to store, encrypt, encode, manage, and stream media content in Azure.</span></span> <span data-ttu-id="d7d3d-111">At the time you create a Media Services account, you also create an associated storage account (or use an existing one) in the same geographic region as the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-111">At the time you create a Media Services account, you also create an associated storage account (or use an existing one) in the same geographic region as the Media Services account.</span></span>

<span data-ttu-id="d7d3d-112">This article explains some common concepts and shows how to create a Media Services account with the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-112">This article explains some common concepts and shows how to create a Media Services account with the Azure portal.</span></span>

## <a name="concepts"></a><span data-ttu-id="d7d3d-113">Concepts</span><span class="sxs-lookup"><span data-stu-id="d7d3d-113">Concepts</span></span>
<span data-ttu-id="d7d3d-114">Accessing Media Services requires two associated accounts:</span><span class="sxs-lookup"><span data-stu-id="d7d3d-114">Accessing Media Services requires two associated accounts:</span></span>

* <span data-ttu-id="d7d3d-115">A Media Services account.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-115">A Media Services account.</span></span> <span data-ttu-id="d7d3d-116">Your account gives you access to a set of cloud-based Media Services that are available in Azure.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-116">Your account gives you access to a set of cloud-based Media Services that are available in Azure.</span></span> <span data-ttu-id="d7d3d-117">A Media Services account does not store actual media content.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-117">A Media Services account does not store actual media content.</span></span> <span data-ttu-id="d7d3d-118">Instead it stores metadata about the media content and media processing jobs in your account.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-118">Instead it stores metadata about the media content and media processing jobs in your account.</span></span> <span data-ttu-id="d7d3d-119">At the time you create the account, you select an available Media Services region.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-119">At the time you create the account, you select an available Media Services region.</span></span> <span data-ttu-id="d7d3d-120">The region you select is a data center that stores the metadata records for your account.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-120">The region you select is a data center that stores the metadata records for your account.</span></span>
  
    <span data-ttu-id="d7d3d-121">Available Media Services (AMS) regions include the following: North Europe, West Europe, West US, East US, Southeast Asia, East Asia, Japan West, Japan East.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-121">Available Media Services (AMS) regions include the following: North Europe, West Europe, West US, East US, Southeast Asia, East Asia, Japan West, Japan East.</span></span> <span data-ttu-id="d7d3d-122">Media Services does not use affinity groups.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-122">Media Services does not use affinity groups.</span></span>
  
    <span data-ttu-id="d7d3d-123">AMS is now also available in the following data centers: Brazil South, India West, India South, and India Central.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-123">AMS is now also available in the following data centers: Brazil South, India West, India South, and India Central.</span></span> <span data-ttu-id="d7d3d-124">You can now use the Azure  portal to create Media Service accounts and perform various tasks described here.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-124">You can now use the Azure  portal to create Media Service accounts and perform various tasks described here.</span></span> <span data-ttu-id="d7d3d-125">However, Live Encoding is not enabled in these data centers.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-125">However, Live Encoding is not enabled in these data centers.</span></span> <span data-ttu-id="d7d3d-126">Further, not all types of Encoding Reserved Units are available in these data centers.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-126">Further, not all types of Encoding Reserved Units are available in these data centers.</span></span>
  
  * <span data-ttu-id="d7d3d-127">Brazil South: Only Standard and Basic Encoding Reserved Units are available.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-127">Brazil South: Only Standard and Basic Encoding Reserved Units are available.</span></span>
  * <span data-ttu-id="d7d3d-128">India West, India South:</span><span class="sxs-lookup"><span data-stu-id="d7d3d-128">India West, India South:</span></span> 
* <span data-ttu-id="d7d3d-129">An Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-129">An Azure storage account.</span></span> <span data-ttu-id="d7d3d-130">Storage accounts must be located in the same geographic region as the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-130">Storage accounts must be located in the same geographic region as the Media Services account.</span></span> <span data-ttu-id="d7d3d-131">When you create a Media Services account, you can either choose an existing storage account in the same region, or you can create a new storage account in the same region.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-131">When you create a Media Services account, you can either choose an existing storage account in the same region, or you can create a new storage account in the same region.</span></span> <span data-ttu-id="d7d3d-132">If you delete a Media Services account, the blobs in your related storage account are not deleted.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-132">If you delete a Media Services account, the blobs in your related storage account are not deleted.</span></span>

## <a name="create-an-ams-account"></a><span data-ttu-id="d7d3d-133">Create an AMS account</span><span class="sxs-lookup"><span data-stu-id="d7d3d-133">Create an AMS account</span></span>
<span data-ttu-id="d7d3d-134">The steps in this section show how to create an AMS account.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-134">The steps in this section show how to create an AMS account.</span></span>

1. <span data-ttu-id="d7d3d-135">Log in at the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d7d3d-135">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d7d3d-136">Click **+New** > **Web + Mobile** > **Media Services**.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-136">Click **+New** > **Web + Mobile** > **Media Services**.</span></span>
   
    ![Media Services Create](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-create-account/media-services-new1.png)
3. <span data-ttu-id="d7d3d-138">In **CREATE MEDIA SERVICES ACCOUNT** enter required values.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-138">In **CREATE MEDIA SERVICES ACCOUNT** enter required values.</span></span>
   
    ![Media Services Create](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-create-account/media-services-new3.png)
   
   1. <span data-ttu-id="d7d3d-140">In **Account Name**, enter the name of the new AMS account.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-140">In **Account Name**, enter the name of the new AMS account.</span></span> <span data-ttu-id="d7d3d-141">A Media Services account name is all lowercase letters or numbers with no spaces, and is 3 to 24 characters in length.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-141">A Media Services account name is all lowercase letters or numbers with no spaces, and is 3 to 24 characters in length.</span></span>
   2. <span data-ttu-id="d7d3d-142">In Subscription, select among the different Azure subscriptions that you have access to.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-142">In Subscription, select among the different Azure subscriptions that you have access to.</span></span>
   3. <span data-ttu-id="d7d3d-143">In **Resource Group**, select the new or existing resource.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-143">In **Resource Group**, select the new or existing resource.</span></span>  <span data-ttu-id="d7d3d-144">A resource group is a collection of resources that share lifecycle, permissions, and policies.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-144">A resource group is a collection of resources that share lifecycle, permissions, and policies.</span></span> <span data-ttu-id="d7d3d-145">Learn more [here](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="d7d3d-145">Learn more [here](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
   4. <span data-ttu-id="d7d3d-146">In **Location**,  select the geographic region that will be used to store the media and metadata records for your Media Services account.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-146">In **Location**,  select the geographic region that will be used to store the media and metadata records for your Media Services account.</span></span> <span data-ttu-id="d7d3d-147">This  region will be used to process and stream your media.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-147">This  region will be used to process and stream your media.</span></span> <span data-ttu-id="d7d3d-148">Only the available Media Services regions appear in the drop-down list box.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-148">Only the available Media Services regions appear in the drop-down list box.</span></span> 
   5. <span data-ttu-id="d7d3d-149">In **Storage Account**, select a storage account to provide blob storage of the media content from your Media Services account.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-149">In **Storage Account**, select a storage account to provide blob storage of the media content from your Media Services account.</span></span> <span data-ttu-id="d7d3d-150">You can select an existing storage account in the same geographic region as your Media Services account, or you can create a storage account.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-150">You can select an existing storage account in the same geographic region as your Media Services account, or you can create a storage account.</span></span> <span data-ttu-id="d7d3d-151">A new storage account is created in the same region.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-151">A new storage account is created in the same region.</span></span> <span data-ttu-id="d7d3d-152">The rules for storage account names are the same as for Media Services accounts.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-152">The rules for storage account names are the same as for Media Services accounts.</span></span>
      
       <span data-ttu-id="d7d3d-153">Learn more about storage [here](../storage/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d7d3d-153">Learn more about storage [here](../storage/storage-introduction.md).</span></span>
   6. <span data-ttu-id="d7d3d-154">Select **Pin to dashboard** to see the progress of the account deployment.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-154">Select **Pin to dashboard** to see the progress of the account deployment.</span></span>
4. <span data-ttu-id="d7d3d-155">Click **Create** at the bottom of the form.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-155">Click **Create** at the bottom of the form.</span></span>
   
    <span data-ttu-id="d7d3d-156">Once the account is successfully created, overview page loads.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-156">Once the account is successfully created, overview page loads.</span></span> <span data-ttu-id="d7d3d-157">In the streaming endpoint table the account will have a default streaming endpoint in the **Stopped** state.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-157">In the streaming endpoint table the account will have a default streaming endpoint in the **Stopped** state.</span></span> 

    >[!NOTE]
    >When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state. To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state. 
   
    ![Media Services settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-create-account/media-services-settings.png)
   
    <span data-ttu-id="d7d3d-161">To manage your AMS account (for example, upload videos, encode assets, monitor job progress) use the **Settings** window.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-161">To manage your AMS account (for example, upload videos, encode assets, monitor job progress) use the **Settings** window.</span></span>

## <a name="manage-keys"></a><span data-ttu-id="d7d3d-162">Manage Keys</span><span class="sxs-lookup"><span data-stu-id="d7d3d-162">Manage Keys</span></span>
<span data-ttu-id="d7d3d-163">You need the account name and the primary key information to programmatically access the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-163">You need the account name and the primary key information to programmatically access the Media Services account.</span></span>

1. <span data-ttu-id="d7d3d-164">In the Azure portal, select your account.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-164">In the Azure portal, select your account.</span></span> 
   
    <span data-ttu-id="d7d3d-165">The **Settings** window appears on the right.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-165">The **Settings** window appears on the right.</span></span> 
2. <span data-ttu-id="d7d3d-166">In the **Settings** window, select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-166">In the **Settings** window, select **Keys**.</span></span> 
   
    <span data-ttu-id="d7d3d-167">The **Manage keys** windows shows the account name and the primary and secondary keys is displayed.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-167">The **Manage keys** windows shows the account name and the primary and secondary keys is displayed.</span></span> 
3. <span data-ttu-id="d7d3d-168">Press the copy button to copy the values.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-168">Press the copy button to copy the values.</span></span>
   
    ![Media Services Keys](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-create-account/media-services-keys.png)

## <a name="next-steps"></a><span data-ttu-id="d7d3d-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="d7d3d-170">Next steps</span></span>
<span data-ttu-id="d7d3d-171">You can now upload files into your AMS account.</span><span class="sxs-lookup"><span data-stu-id="d7d3d-171">You can now upload files into your AMS account.</span></span> <span data-ttu-id="d7d3d-172">For more information, see [Upload files](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="d7d3d-172">For more information, see [Upload files](media-services-portal-upload-files.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d7d3d-173">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="d7d3d-173">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d7d3d-174">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="d7d3d-174">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]





