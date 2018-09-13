---
title: Redact faces with Azure Media Analytics walkthrough | Microsoft Docs
description: This topic shows step by step instructions on how to run a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).
services: media-services
documentationcenter: ''
author: Lichard
manager: cfowler
editor: ''
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: d7a6abaeff0e939ed9e299e16e2fe59b65127aba
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869826"
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="a6594-103">Redact faces with Azure Media Analytics walkthrough</span><span class="sxs-lookup"><span data-stu-id="a6594-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="a6594-104">Overview</span><span class="sxs-lookup"><span data-stu-id="a6594-104">Overview</span></span>

<span data-ttu-id="a6594-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span><span class="sxs-lookup"><span data-stu-id="a6594-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="a6594-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span><span class="sxs-lookup"><span data-stu-id="a6594-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="a6594-107">You may want to use the face redaction service in public safety and news media scenarios.</span><span class="sxs-lookup"><span data-stu-id="a6594-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="a6594-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span><span class="sxs-lookup"><span data-stu-id="a6594-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="a6594-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span><span class="sxs-lookup"><span data-stu-id="a6594-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="a6594-110">For details about  **Azure Media Redactor**, see the [Face redaction overview](media-services-face-redaction.md) topic.</span><span class="sxs-lookup"><span data-stu-id="a6594-110">For details about  **Azure Media Redactor**, see the [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="a6594-111">This topic shows step by step instructions on how to run a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span><span class="sxs-lookup"><span data-stu-id="a6594-111">This topic shows step by step instructions on how to run a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="a6594-112">For more information, see [this](https://azure.microsoft.com/blog/redaction-preview-available-globally) blog.</span><span class="sxs-lookup"><span data-stu-id="a6594-112">For more information, see [this](https://azure.microsoft.com/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="a6594-113">Azure Media Services Explorer workflow</span><span class="sxs-lookup"><span data-stu-id="a6594-113">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="a6594-114">The easiest way to get started with Redactor is to use the open source AMSE tool on github.</span><span class="sxs-lookup"><span data-stu-id="a6594-114">The easiest way to get started with Redactor is to use the open source AMSE tool on github.</span></span> <span data-ttu-id="a6594-115">You can run a simplified workflow via **combined** mode if you don’t need access to the annotation json or the face jpg images.</span><span class="sxs-lookup"><span data-stu-id="a6594-115">You can run a simplified workflow via **combined** mode if you don’t need access to the annotation json or the face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="a6594-116">Download and setup</span><span class="sxs-lookup"><span data-stu-id="a6594-116">Download and setup</span></span>

1. <span data-ttu-id="a6594-117">Download the AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span><span class="sxs-lookup"><span data-stu-id="a6594-117">Download the AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="a6594-118">Log in to your Media Services account using your service key.</span><span class="sxs-lookup"><span data-stu-id="a6594-118">Log in to your Media Services account using your service key.</span></span>

    <span data-ttu-id="a6594-119">To obtain the account name and key information, go to the [Azure portal](https://portal.azure.com/) and select your AMS account.</span><span class="sxs-lookup"><span data-stu-id="a6594-119">To obtain the account name and key information, go to the [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="a6594-120">Then, select Settings > Keys.</span><span class="sxs-lookup"><span data-stu-id="a6594-120">Then, select Settings > Keys.</span></span> <span data-ttu-id="a6594-121">The Manage keys windows shows the account name and the primary and secondary keys is displayed.</span><span class="sxs-lookup"><span data-stu-id="a6594-121">The Manage keys windows shows the account name and the primary and secondary keys is displayed.</span></span> <span data-ttu-id="a6594-122">Copy values of the account name and the primary key.</span><span class="sxs-lookup"><span data-stu-id="a6594-122">Copy values of the account name and the primary key.</span></span>

![Face redaction](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="a6594-124">First pass – analyze mode</span><span class="sxs-lookup"><span data-stu-id="a6594-124">First pass – analyze mode</span></span>

1. <span data-ttu-id="a6594-125">Upload your media file through Asset –> Upload, or via drag and drop.</span><span class="sxs-lookup"><span data-stu-id="a6594-125">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="a6594-126">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span><span class="sxs-lookup"><span data-stu-id="a6594-126">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![Face redaction](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Face redaction](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="a6594-129">The output will include an annotations json file with face location data, as well as a jpg of each detected face.</span><span class="sxs-lookup"><span data-stu-id="a6594-129">The output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![Face redaction](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

### <a name="second-pass--redact-mode"></a><span data-ttu-id="a6594-131">Second pass – redact mode</span><span class="sxs-lookup"><span data-stu-id="a6594-131">Second pass – redact mode</span></span>

1. <span data-ttu-id="a6594-132">Upload your original video asset to the output from the first pass and set as a primary asset.</span><span class="sxs-lookup"><span data-stu-id="a6594-132">Upload your original video asset to the output from the first pass and set as a primary asset.</span></span> 

    ![Face redaction](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="a6594-134">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of the IDs you wish to redact.</span><span class="sxs-lookup"><span data-stu-id="a6594-134">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of the IDs you wish to redact.</span></span> 

    ![Face redaction](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="a6594-136">(Optional) Make any edits to the annotations.json file such as increasing the bounding box boundaries.</span><span class="sxs-lookup"><span data-stu-id="a6594-136">(Optional) Make any edits to the annotations.json file such as increasing the bounding box boundaries.</span></span> 
4. <span data-ttu-id="a6594-137">Right click the output asset from the first pass, select the Redactor, and run with the **Redact** mode.</span><span class="sxs-lookup"><span data-stu-id="a6594-137">Right click the output asset from the first pass, select the Redactor, and run with the **Redact** mode.</span></span> 

    ![Face redaction](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="a6594-139">Download or share the final redacted output asset.</span><span class="sxs-lookup"><span data-stu-id="a6594-139">Download or share the final redacted output asset.</span></span> 

    ![Face redaction](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

## <a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="a6594-141">Azure Media Redactor Visualizer open source tool</span><span class="sxs-lookup"><span data-stu-id="a6594-141">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="a6594-142">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed to help developers just starting with the annotations format with parsing and using the output.</span><span class="sxs-lookup"><span data-stu-id="a6594-142">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed to help developers just starting with the annotations format with parsing and using the output.</span></span>

<span data-ttu-id="a6594-143">After you clone the repo, in order to run the project, you will need to download FFMPEG from their [official site](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="a6594-143">After you clone the repo, in order to run the project, you will need to download FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="a6594-144">If you are a developer trying to parse the JSON annotation data, look inside Models.MetaData for sample code examples.</span><span class="sxs-lookup"><span data-stu-id="a6594-144">If you are a developer trying to parse the JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-the-tool"></a><span data-ttu-id="a6594-145">Set up the tool</span><span class="sxs-lookup"><span data-stu-id="a6594-145">Set up the tool</span></span>

1.  <span data-ttu-id="a6594-146">Download and build the entire solution.</span><span class="sxs-lookup"><span data-stu-id="a6594-146">Download and build the entire solution.</span></span> 

    ![Face redaction](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="a6594-148">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="a6594-148">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="a6594-149">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span><span class="sxs-lookup"><span data-stu-id="a6594-149">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="a6594-150">Copy ffmpeg.exe and ffprobe.exe to the same output folder as AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="a6594-150">Copy ffmpeg.exe and ffprobe.exe to the same output folder as AzureMediaRedactor.exe.</span></span> 

    ![Face redaction](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="a6594-152">Run AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="a6594-152">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-the-tool"></a><span data-ttu-id="a6594-153">Use the tool</span><span class="sxs-lookup"><span data-stu-id="a6594-153">Use the tool</span></span>

1. <span data-ttu-id="a6594-154">Process your video in your Azure Media Services account with the Redactor MP on Analyze mode.</span><span class="sxs-lookup"><span data-stu-id="a6594-154">Process your video in your Azure Media Services account with the Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="a6594-155">Download both the original video file and the output of the Redaction - Analyze job.</span><span class="sxs-lookup"><span data-stu-id="a6594-155">Download both the original video file and the output of the Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="a6594-156">Run the visualizer application and choose the files above.</span><span class="sxs-lookup"><span data-stu-id="a6594-156">Run the visualizer application and choose the files above.</span></span> 

    ![Face redaction](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="a6594-158">Preview your file.</span><span class="sxs-lookup"><span data-stu-id="a6594-158">Preview your file.</span></span> <span data-ttu-id="a6594-159">Select which faces you'd like to blur via the sidebar on the right.</span><span class="sxs-lookup"><span data-stu-id="a6594-159">Select which faces you'd like to blur via the sidebar on the right.</span></span> 
    
    ![Face redaction](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="a6594-161">The bottom text field will update with the face IDs.</span><span class="sxs-lookup"><span data-stu-id="a6594-161">The bottom text field will update with the face IDs.</span></span> <span data-ttu-id="a6594-162">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span><span class="sxs-lookup"><span data-stu-id="a6594-162">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="a6594-163">The idlist.txt should be saved in ANSI.</span><span class="sxs-lookup"><span data-stu-id="a6594-163">The idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="a6594-164">You can use notepad to save in ANSI.</span><span class="sxs-lookup"><span data-stu-id="a6594-164">You can use notepad to save in ANSI.</span></span>
    
6.  <span data-ttu-id="a6594-165">Upload this file to the output asset from step 1.</span><span class="sxs-lookup"><span data-stu-id="a6594-165">Upload this file to the output asset from step 1.</span></span> <span data-ttu-id="a6594-166">Upload the original video to this asset as well and set as primary asset.</span><span class="sxs-lookup"><span data-stu-id="a6594-166">Upload the original video to this asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="a6594-167">Run Redaction job on this asset with "Redact" mode to get the final redacted video.</span><span class="sxs-lookup"><span data-stu-id="a6594-167">Run Redaction job on this asset with "Redact" mode to get the final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a6594-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6594-168">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a6594-169">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="a6594-169">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="a6594-170">Related links</span><span class="sxs-lookup"><span data-stu-id="a6594-170">Related links</span></span>
[<span data-ttu-id="a6594-171">Azure Media Services Analytics Overview</span><span class="sxs-lookup"><span data-stu-id="a6594-171">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="a6594-172">Azure Media Analytics demos</span><span class="sxs-lookup"><span data-stu-id="a6594-172">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[<span data-ttu-id="a6594-173">Announcing Face Redaction for Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="a6594-173">Announcing Face Redaction for Azure Media Analytics</span></span>](https://azure.microsoft.com/blog/azure-media-redactor/)
