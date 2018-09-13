---
title: Create an Azure Media Services account with the Azure portal | Microsoft Docs
description: This tutorial walks you through the steps of creating an Azure Media Services account with the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: c551e158-aad6-47b4-931e-b46260b3ee4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/01/2018
ms.author: juliako
ms.openlocfilehash: da190bf2418f1cfb8ea952b69d3bf1d76258da5f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857127"
---
# <a name="create-an-azure-media-services-account-using-the-azure-portal"></a><span data-ttu-id="0b3b1-103">Create an Azure Media Services account using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0b3b1-103">Create an Azure Media Services account using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-create-account.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> To complete this tutorial, you need an Azure account. For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

<span data-ttu-id="0b3b1-108">The Azure portal provides a way to quickly create an Azure Media Services (AMS) account.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-108">The Azure portal provides a way to quickly create an Azure Media Services (AMS) account.</span></span> <span data-ttu-id="0b3b1-109">You can use your account to access Media Services that enable you to store, encrypt, encode, manage, and stream media content in Azure.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-109">You can use your account to access Media Services that enable you to store, encrypt, encode, manage, and stream media content in Azure.</span></span> <span data-ttu-id="0b3b1-110">At the time you create a Media Services account, you also create an associated storage account (or use an existing one) in the same geographic region as the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-110">At the time you create a Media Services account, you also create an associated storage account (or use an existing one) in the same geographic region as the Media Services account.</span></span> 

<span data-ttu-id="0b3b1-111">You can have General Purpose v1 or General Purpose v2 as your primary storage account.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-111">You can have General Purpose v1 or General Purpose v2 as your primary storage account.</span></span> <span data-ttu-id="0b3b1-112">Currently, the Azure portal only allows picking v1 but you can add v2 when creating you account using the API or Powershell.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-112">Currently, the Azure portal only allows picking v1 but you can add v2 when creating you account using the API or Powershell.</span></span> <span data-ttu-id="0b3b1-113">For more information about storage types, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="0b3b1-113">For more information about storage types, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).</span></span>

<span data-ttu-id="0b3b1-114">This article explains some common concepts and shows how to create a Media Services account with the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-114">This article explains some common concepts and shows how to create a Media Services account with the Azure portal.</span></span>

> [!NOTE]
> For information about availability of Azure Media Services features in different regions, see [availability of AMS features across datacenters](scenarios-and-availability.md#availability).

## <a name="concepts"></a><span data-ttu-id="0b3b1-116">Concepts</span><span class="sxs-lookup"><span data-stu-id="0b3b1-116">Concepts</span></span>
<span data-ttu-id="0b3b1-117">Accessing Media Services requires two associated accounts:</span><span class="sxs-lookup"><span data-stu-id="0b3b1-117">Accessing Media Services requires two associated accounts:</span></span>

* <span data-ttu-id="0b3b1-118">A Media Services account.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-118">A Media Services account.</span></span> <span data-ttu-id="0b3b1-119">Your account gives you access to a set of cloud-based Media Services resources that are available in Azure.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-119">Your account gives you access to a set of cloud-based Media Services resources that are available in Azure.</span></span> <span data-ttu-id="0b3b1-120">A Media Services account does not store actual media content.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-120">A Media Services account does not store actual media content.</span></span> <span data-ttu-id="0b3b1-121">Instead it stores metadata about the media content and media processing jobs in your account.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-121">Instead it stores metadata about the media content and media processing jobs in your account.</span></span> <span data-ttu-id="0b3b1-122">At the time you create the account, you select an available Media Services region.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-122">At the time you create the account, you select an available Media Services region.</span></span> <span data-ttu-id="0b3b1-123">The region you select is a data center that stores the metadata records for your account.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-123">The region you select is a data center that stores the metadata records for your account.</span></span>
  
* <span data-ttu-id="0b3b1-124">An Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-124">An Azure storage account.</span></span> <span data-ttu-id="0b3b1-125">Storage accounts must be located in the same geographic region as the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-125">Storage accounts must be located in the same geographic region as the Media Services account.</span></span> <span data-ttu-id="0b3b1-126">When you create a Media Services account, you can either choose an existing storage account in the same region, or you can create a new storage account in the same region.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-126">When you create a Media Services account, you can either choose an existing storage account in the same region, or you can create a new storage account in the same region.</span></span> <span data-ttu-id="0b3b1-127">If you delete a Media Services account, the blobs in your related storage account are not deleted.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-127">If you delete a Media Services account, the blobs in your related storage account are not deleted.</span></span>

## <a name="create-an-ams-account"></a><span data-ttu-id="0b3b1-128">Create an AMS account</span><span class="sxs-lookup"><span data-stu-id="0b3b1-128">Create an AMS account</span></span>
<span data-ttu-id="0b3b1-129">The steps in this section show how to create an AMS account.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-129">The steps in this section show how to create an AMS account.</span></span>

1. <span data-ttu-id="0b3b1-130">Sign in at the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0b3b1-130">Sign in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0b3b1-131">Click **+New** > **Web + Mobile** > **Media Services**.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-131">Click **+New** > **Web + Mobile** > **Media Services**.</span></span>
   
    ![Media Services Create](./media/media-services-create-account/media-services-new1.png)
3. <span data-ttu-id="0b3b1-133">In **CREATE MEDIA SERVICES ACCOUNT** enter required values.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-133">In **CREATE MEDIA SERVICES ACCOUNT** enter required values.</span></span>
   
    ![Media Services Create](./media/media-services-create-account/media-services-new3.png)
   
   1. <span data-ttu-id="0b3b1-135">In **Account Name**, enter the name of the new AMS account.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-135">In **Account Name**, enter the name of the new AMS account.</span></span> <span data-ttu-id="0b3b1-136">A Media Services account name is all lowercase letters or numbers with no spaces, and is 3 to 24 characters in length.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-136">A Media Services account name is all lowercase letters or numbers with no spaces, and is 3 to 24 characters in length.</span></span>
   2. <span data-ttu-id="0b3b1-137">In Subscription, select among the different Azure subscriptions that you have access to.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-137">In Subscription, select among the different Azure subscriptions that you have access to.</span></span>
   3. <span data-ttu-id="0b3b1-138">In **Resource Group**, select the new or existing resource.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-138">In **Resource Group**, select the new or existing resource.</span></span>  <span data-ttu-id="0b3b1-139">A resource group is a collection of resources that share lifecycle, permissions, and policies.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-139">A resource group is a collection of resources that share lifecycle, permissions, and policies.</span></span> <span data-ttu-id="0b3b1-140">Learn more [here](../../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="0b3b1-140">Learn more [here](../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
   4. <span data-ttu-id="0b3b1-141">In **Location**,  select the geographic region that will be used to store the media and metadata records for your Media Services account.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-141">In **Location**,  select the geographic region that will be used to store the media and metadata records for your Media Services account.</span></span> <span data-ttu-id="0b3b1-142">This  region will be used to process and stream your media.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-142">This  region will be used to process and stream your media.</span></span> <span data-ttu-id="0b3b1-143">Only the available Media Services regions appear in the drop-down list box.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-143">Only the available Media Services regions appear in the drop-down list box.</span></span> 
   5. <span data-ttu-id="0b3b1-144">In **Storage Account**, select a storage account to provide blob storage of the media content from your Media Services account.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-144">In **Storage Account**, select a storage account to provide blob storage of the media content from your Media Services account.</span></span> <span data-ttu-id="0b3b1-145">You can select an existing storage account in the same geographic region as your Media Services account, or you can create a storage account.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-145">You can select an existing storage account in the same geographic region as your Media Services account, or you can create a storage account.</span></span> <span data-ttu-id="0b3b1-146">A new storage account is created in the same region.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-146">A new storage account is created in the same region.</span></span> <span data-ttu-id="0b3b1-147">The rules for storage account names are the same as for Media Services accounts.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-147">The rules for storage account names are the same as for Media Services accounts.</span></span>
      
       <span data-ttu-id="0b3b1-148">Learn more about storage [here](../../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0b3b1-148">Learn more about storage [here](../../storage/common/storage-introduction.md).</span></span>
   6. <span data-ttu-id="0b3b1-149">Select **Pin to dashboard** to see the progress of the account deployment.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-149">Select **Pin to dashboard** to see the progress of the account deployment.</span></span>
4. <span data-ttu-id="0b3b1-150">Click **Create** at the bottom of the form.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-150">Click **Create** at the bottom of the form.</span></span>
   
    <span data-ttu-id="0b3b1-151">Once the account is successfully created, overview page loads.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-151">Once the account is successfully created, overview page loads.</span></span> <span data-ttu-id="0b3b1-152">In the streaming endpoint table the account will have a default streaming endpoint in the **Stopped** state.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-152">In the streaming endpoint table the account will have a default streaming endpoint in the **Stopped** state.</span></span> 

    >[!NOTE]
    >When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state. To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state. 
   
## <a name="to-manage-your-ams-account"></a><span data-ttu-id="0b3b1-155">To manage your AMS account</span><span class="sxs-lookup"><span data-stu-id="0b3b1-155">To manage your AMS account</span></span>

<span data-ttu-id="0b3b1-156">To manage your AMS account (for example, connect to the AMS API programmatically, upload videos, encode assets, configure content protection, monitor job progress) select **Settings** on the left side of the portal.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-156">To manage your AMS account (for example, connect to the AMS API programmatically, upload videos, encode assets, configure content protection, monitor job progress) select **Settings** on the left side of the portal.</span></span> <span data-ttu-id="0b3b1-157">From the **Settings**, navigate to one of the available blades (for example: **API access**, **Assets**, **Jobs**, **Content protection**).</span><span class="sxs-lookup"><span data-stu-id="0b3b1-157">From the **Settings**, navigate to one of the available blades (for example: **API access**, **Assets**, **Jobs**, **Content protection**).</span></span>


## <a name="next-steps"></a><span data-ttu-id="0b3b1-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="0b3b1-158">Next steps</span></span>

<span data-ttu-id="0b3b1-159">You can now upload files into your AMS account.</span><span class="sxs-lookup"><span data-stu-id="0b3b1-159">You can now upload files into your AMS account.</span></span> <span data-ttu-id="0b3b1-160">For more information, see [Upload files](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="0b3b1-160">For more information, see [Upload files](media-services-portal-upload-files.md).</span></span>

<span data-ttu-id="0b3b1-161">If you plan to access AMS API programmatically, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="0b3b1-161">If you plan to access AMS API programmatically, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="0b3b1-162">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="0b3b1-162">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0b3b1-163">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="0b3b1-163">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

