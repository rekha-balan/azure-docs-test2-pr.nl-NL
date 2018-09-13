---
title: Task preset for Azure Media Indexer
description: This topic gives an overview of task preset for Azure Media Indexer.
services: media-services
documentationcenter: ''
author: Asolanki
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: ae6c4da189cd6637b4e1fa9274473b62f6664e51
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966437"
---
# <a name="task-preset-for-azure-media-indexer"></a><span data-ttu-id="a3674-103">Task preset for Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="a3674-103">Task preset for Azure Media Indexer</span></span>

<span data-ttu-id="a3674-104">Azure Media Indexer is a Media Processor that you use to perform the following tasks: make media files and content searchable, generate closed captioning tracks and keywords, index asset files that are part of your asset.</span><span class="sxs-lookup"><span data-stu-id="a3674-104">Azure Media Indexer is a Media Processor that you use to perform the following tasks: make media files and content searchable, generate closed captioning tracks and keywords, index asset files that are part of your asset.</span></span>

<span data-ttu-id="a3674-105">This topic describes the task preset that you need to pass to your indexing job.</span><span class="sxs-lookup"><span data-stu-id="a3674-105">This topic describes the task preset that you need to pass to your indexing job.</span></span> <span data-ttu-id="a3674-106">For complete example, see [Indexing media files with Azure Media Indexer](media-services-index-content.md).</span><span class="sxs-lookup"><span data-stu-id="a3674-106">For complete example, see [Indexing media files with Azure Media Indexer](media-services-index-content.md).</span></span>

## <a name="azure-media-indexer-configuration-xml"></a><span data-ttu-id="a3674-107">Azure Media Indexer Configuration XML</span><span class="sxs-lookup"><span data-stu-id="a3674-107">Azure Media Indexer Configuration XML</span></span>

<span data-ttu-id="a3674-108">The following table explains elements and attributes of the configuration XML.</span><span class="sxs-lookup"><span data-stu-id="a3674-108">The following table explains elements and attributes of the configuration XML.</span></span>

|<span data-ttu-id="a3674-109">Name</span><span class="sxs-lookup"><span data-stu-id="a3674-109">Name</span></span>|<span data-ttu-id="a3674-110">Require</span><span class="sxs-lookup"><span data-stu-id="a3674-110">Require</span></span>|<span data-ttu-id="a3674-111">Description</span><span class="sxs-lookup"><span data-stu-id="a3674-111">Description</span></span>|
|---|---|---|
|<span data-ttu-id="a3674-112">Input</span><span class="sxs-lookup"><span data-stu-id="a3674-112">Input</span></span>|<span data-ttu-id="a3674-113">true</span><span class="sxs-lookup"><span data-stu-id="a3674-113">true</span></span>|<span data-ttu-id="a3674-114">Asset file(s) that you want to index.</span><span class="sxs-lookup"><span data-stu-id="a3674-114">Asset file(s) that you want to index.</span></span><br/><span data-ttu-id="a3674-115">Azure Media Indexer supports the following media file formats: MP4, MOV, WMV, MP3, M4A, WMA, AAC, WAV.</span><span class="sxs-lookup"><span data-stu-id="a3674-115">Azure Media Indexer supports the following media file formats: MP4, MOV, WMV, MP3, M4A, WMA, AAC, WAV.</span></span> <br/><br/><span data-ttu-id="a3674-116">You can specify the file name (s) in the **name** or **list** attribute of the **input** element (as shown below).</span><span class="sxs-lookup"><span data-stu-id="a3674-116">You can specify the file name (s) in the **name** or **list** attribute of the **input** element (as shown below).</span></span> <span data-ttu-id="a3674-117">If you do not specify which asset file to index, the primary file is picked.</span><span class="sxs-lookup"><span data-stu-id="a3674-117">If you do not specify which asset file to index, the primary file is picked.</span></span> <span data-ttu-id="a3674-118">If no primary asset file is set, the first file in the input asset is indexed.</span><span class="sxs-lookup"><span data-stu-id="a3674-118">If no primary asset file is set, the first file in the input asset is indexed.</span></span><br/><br/><span data-ttu-id="a3674-119">To explicitly specify the asset file name, do:</span><span class="sxs-lookup"><span data-stu-id="a3674-119">To explicitly specify the asset file name, do:</span></span><br/>```<input name="TestFile.wmv" />```<br/><br/><span data-ttu-id="a3674-120">You can also index multiple asset files at once (up to 10 files).</span><span class="sxs-lookup"><span data-stu-id="a3674-120">You can also index multiple asset files at once (up to 10 files).</span></span> <span data-ttu-id="a3674-121">To do this:</span><span class="sxs-lookup"><span data-stu-id="a3674-121">To do this:</span></span><br/><span data-ttu-id="a3674-122">- Create a text file (manifest file) and give it an .lst extension.</span><span class="sxs-lookup"><span data-stu-id="a3674-122">- Create a text file (manifest file) and give it an .lst extension.</span></span><br/><span data-ttu-id="a3674-123">- Add a list of all the asset file names in your input asset to this manifest file.</span><span class="sxs-lookup"><span data-stu-id="a3674-123">- Add a list of all the asset file names in your input asset to this manifest file.</span></span><br/><span data-ttu-id="a3674-124">- Add (upload) thanifest file to the asset.</span><span class="sxs-lookup"><span data-stu-id="a3674-124">- Add (upload) thanifest file to the asset.</span></span><br/><span data-ttu-id="a3674-125">- Specify the name of the manifest file in the input’s list attribute.</span><span class="sxs-lookup"><span data-stu-id="a3674-125">- Specify the name of the manifest file in the input’s list attribute.</span></span><br/>```<input list="input.lst">```<br/><br/><span data-ttu-id="a3674-126">**Note:** If you add more than 10 files to the manifest file, the indexing job will fail with the 2006 error code.</span><span class="sxs-lookup"><span data-stu-id="a3674-126">**Note:** If you add more than 10 files to the manifest file, the indexing job will fail with the 2006 error code.</span></span>|
|<span data-ttu-id="a3674-127">metadata</span><span class="sxs-lookup"><span data-stu-id="a3674-127">metadata</span></span>|<span data-ttu-id="a3674-128">false</span><span class="sxs-lookup"><span data-stu-id="a3674-128">false</span></span>|<span data-ttu-id="a3674-129">Metadata for the specified asset file(s).</span><span class="sxs-lookup"><span data-stu-id="a3674-129">Metadata for the specified asset file(s).</span></span><br/>```<metadata key="..." value="..." />```<br/><br/><span data-ttu-id="a3674-130">You can supply values for predefined keys.</span><span class="sxs-lookup"><span data-stu-id="a3674-130">You can supply values for predefined keys.</span></span> <br/><br/><span data-ttu-id="a3674-131">Currently, the following keys are supported:</span><span class="sxs-lookup"><span data-stu-id="a3674-131">Currently, the following keys are supported:</span></span><br/><br/><span data-ttu-id="a3674-132">**title** and **description** - used to update the language model to improve speech recognition accuracy.</span><span class="sxs-lookup"><span data-stu-id="a3674-132">**title** and **description** - used to update the language model to improve speech recognition accuracy.</span></span><br/>```<metadata key="title" value="[Title of the media file]" /><metadata key="description" value="[Description of the media file]" />```<br/><br/><span data-ttu-id="a3674-133">**username** and **password** - used for authentication when downloading internet files via http or https.</span><span class="sxs-lookup"><span data-stu-id="a3674-133">**username** and **password** - used for authentication when downloading internet files via http or https.</span></span><br/>```<metadata key="username" value="[UserName]" /><metadata key="password" value="[Password]" />```<br/><span data-ttu-id="a3674-134">The username and password values apply to all media URLs in the input manifest.</span><span class="sxs-lookup"><span data-stu-id="a3674-134">The username and password values apply to all media URLs in the input manifest.</span></span>|
|<span data-ttu-id="a3674-135">features</span><span class="sxs-lookup"><span data-stu-id="a3674-135">features</span></span><br/><br/><span data-ttu-id="a3674-136">Added in version 1.2.</span><span class="sxs-lookup"><span data-stu-id="a3674-136">Added in version 1.2.</span></span> <span data-ttu-id="a3674-137">Currently, the only supported feature is speech recognition ("ASR").</span><span class="sxs-lookup"><span data-stu-id="a3674-137">Currently, the only supported feature is speech recognition ("ASR").</span></span>|<span data-ttu-id="a3674-138">false</span><span class="sxs-lookup"><span data-stu-id="a3674-138">false</span></span>|<span data-ttu-id="a3674-139">The Speech Recognition feature has the following settings keys:</span><span class="sxs-lookup"><span data-stu-id="a3674-139">The Speech Recognition feature has the following settings keys:</span></span><br/><br/><span data-ttu-id="a3674-140">Language:</span><span class="sxs-lookup"><span data-stu-id="a3674-140">Language:</span></span><br/><span data-ttu-id="a3674-141">- The natural language to be recognized in the multimedia file.</span><span class="sxs-lookup"><span data-stu-id="a3674-141">- The natural language to be recognized in the multimedia file.</span></span><br/><span data-ttu-id="a3674-142">- English, Spanish</span><span class="sxs-lookup"><span data-stu-id="a3674-142">- English, Spanish</span></span><br/><br/><span data-ttu-id="a3674-143">CaptionFormats:</span><span class="sxs-lookup"><span data-stu-id="a3674-143">CaptionFormats:</span></span><br/><span data-ttu-id="a3674-144">- a semicolon-separated list of the desired output caption formats (if any)</span><span class="sxs-lookup"><span data-stu-id="a3674-144">- a semicolon-separated list of the desired output caption formats (if any)</span></span><br/><span data-ttu-id="a3674-145">- ttml;sami;webvtt</span><span class="sxs-lookup"><span data-stu-id="a3674-145">- ttml;sami;webvtt</span></span><br/><br/><br/><span data-ttu-id="a3674-146">GenerateAIB:</span><span class="sxs-lookup"><span data-stu-id="a3674-146">GenerateAIB:</span></span><br/><span data-ttu-id="a3674-147">- A boolean flag specifying whether or not an AIB file is required (for use with SQL Server and the customer Indexer IFilter).</span><span class="sxs-lookup"><span data-stu-id="a3674-147">- A boolean flag specifying whether or not an AIB file is required (for use with SQL Server and the customer Indexer IFilter).</span></span> <span data-ttu-id="a3674-148">For more information, see Using AIB Files with Azure Media Indexer and SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a3674-148">For more information, see Using AIB Files with Azure Media Indexer and SQL Server.</span></span><br/><span data-ttu-id="a3674-149">- True; False</span><span class="sxs-lookup"><span data-stu-id="a3674-149">- True; False</span></span><br/><br/><span data-ttu-id="a3674-150">GenerateKeywords:</span><span class="sxs-lookup"><span data-stu-id="a3674-150">GenerateKeywords:</span></span><br/><span data-ttu-id="a3674-151">- A boolean flag specifying whether or not a keyword XML file is required.</span><span class="sxs-lookup"><span data-stu-id="a3674-151">- A boolean flag specifying whether or not a keyword XML file is required.</span></span><br/><span data-ttu-id="a3674-152">- True; False.</span><span class="sxs-lookup"><span data-stu-id="a3674-152">- True; False.</span></span>|

## <a name="azure-media-indexer-configuration-xml-example"></a><span data-ttu-id="a3674-153">Azure Media Indexer configuration XML example</span><span class="sxs-lookup"><span data-stu-id="a3674-153">Azure Media Indexer configuration XML example</span></span>

``` 
<?xml version="1.0" encoding="utf-8"?>  
<configuration version="2.0">  
  <input>  
    <metadata key="title" value="[Title of the media file]" />  
    <metadata key="description" value="[Description of the media file]" />  
  </input>  
  <settings>  
  </settings>  
  
  <features>  
    <feature name="ASR">    
      <settings>  
        <add key="Language" value="English"/>  
        <add key="CaptionFormats" value="ttml;sami;webvtt"/>  
        <add key="GenerateAIB" value ="true" />  
        <add key="GenerateKeywords" value ="true" />  
      </settings>  
    </feature>  
  </features>  
  
</configuration>  
```
  
## <a name="next-steps"></a><span data-ttu-id="a3674-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="a3674-154">Next steps</span></span>

<span data-ttu-id="a3674-155">See [Indexing media files with Azure Media Indexer](media-services-index-content.md).</span><span class="sxs-lookup"><span data-stu-id="a3674-155">See [Indexing media files with Azure Media Indexer](media-services-index-content.md).</span></span>

