---
title: Upload files to a Media Services account in the Azure portal | Microsoft Docs
description: This tutorial walks you through the steps of uploading files to a Media Services account in the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 36e1f797263e367a73fde140d979243f96e83948
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866582"
---
# <a name="upload-files-to-a-media-services-account-in-the-azure-portal"></a><span data-ttu-id="b01fb-103">Upload files to a Media Services account in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b01fb-103">Upload files to a Media Services account in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-upload-files.md)
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> 
> [!NOTE]
> To complete this tutorial, you need an Azure account. For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/). 
> 

<span data-ttu-id="b01fb-109">In Azure Media Services, you upload your digital files to an asset.</span><span class="sxs-lookup"><span data-stu-id="b01fb-109">In Azure Media Services, you upload your digital files to an asset.</span></span> <span data-ttu-id="b01fb-110">The asset can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and the metadata for these files).</span><span class="sxs-lookup"><span data-stu-id="b01fb-110">The asset can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and the metadata for these files).</span></span> <span data-ttu-id="b01fb-111">After the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span><span class="sxs-lookup"><span data-stu-id="b01fb-111">After the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

> [!NOTE]
> Media Services has a maximum file size for processing files. For details about file size limits, see [Media Services quotas and limitations](media-services-quotas-and-limitations.md).
>

## <a name="upload-files"></a><span data-ttu-id="b01fb-114">Upload files</span><span class="sxs-lookup"><span data-stu-id="b01fb-114">Upload files</span></span>
1. <span data-ttu-id="b01fb-115">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="b01fb-115">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="b01fb-116">Select **Settings** > **Assets**.</span><span class="sxs-lookup"><span data-stu-id="b01fb-116">Select **Settings** > **Assets**.</span></span> <span data-ttu-id="b01fb-117">Then, select the **Upload** button.</span><span class="sxs-lookup"><span data-stu-id="b01fb-117">Then, select the **Upload** button.</span></span>
   
    ![Upload files](./media/media-services-portal-vod-get-started/media-services-upload.png)
   
    <span data-ttu-id="b01fb-119">The **Upload a video asset** window appears.</span><span class="sxs-lookup"><span data-stu-id="b01fb-119">The **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > Media Services doesn't limit the file size for uploading videos.
 
3. <span data-ttu-id="b01fb-121">On your computer, go to the video that you want to upload.</span><span class="sxs-lookup"><span data-stu-id="b01fb-121">On your computer, go to the video that you want to upload.</span></span> <span data-ttu-id="b01fb-122">Select the video, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b01fb-122">Select the video, and then select **OK**.</span></span>  
   
    <span data-ttu-id="b01fb-123">The upload begins.</span><span class="sxs-lookup"><span data-stu-id="b01fb-123">The upload begins.</span></span> <span data-ttu-id="b01fb-124">You can see the progress under the file name.</span><span class="sxs-lookup"><span data-stu-id="b01fb-124">You can see the progress under the file name.</span></span>  

<span data-ttu-id="b01fb-125">When the upload is finished, the new asset is listed in the **Assets** pane.</span><span class="sxs-lookup"><span data-stu-id="b01fb-125">When the upload is finished, the new asset is listed in the **Assets** pane.</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="b01fb-126">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="b01fb-126">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b01fb-127">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="b01fb-127">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="b01fb-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="b01fb-128">Next steps</span></span>
* <span data-ttu-id="b01fb-129">Learn how to [encode your uploaded assets](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="b01fb-129">Learn how to [encode your uploaded assets](media-services-portal-encode.md).</span></span>

* <span data-ttu-id="b01fb-130">You also can use Azure Functions to trigger an encoding job when a file arrives in the configured container.</span><span class="sxs-lookup"><span data-stu-id="b01fb-130">You also can use Azure Functions to trigger an encoding job when a file arrives in the configured container.</span></span> <span data-ttu-id="b01fb-131">For more information, see the sample at [Media Services: Integrating Azure Media Services with Azure Functions and Logic Apps](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/).</span><span class="sxs-lookup"><span data-stu-id="b01fb-131">For more information, see the sample at [Media Services: Integrating Azure Media Services with Azure Functions and Logic Apps](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/).</span></span>


