---
title: Encode custom transform using Azure Media Services v3 | Microsoft Docs
description: This topic shows how to use Azure Media Services v3 to encode a custom transform.
services: media-services
documentationcenter: ''
author: Juliako
manager: cflower
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.custom: ''
ms.date: 05/17/2018
ms.author: juliako
ms.openlocfilehash: d298070877a366d04b2df1ef8ac63b08f8771de0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871031"
---
# <a name="how-to-encode-with-a-custom-transform"></a><span data-ttu-id="72ccc-103">How to encode with a custom Transform</span><span class="sxs-lookup"><span data-stu-id="72ccc-103">How to encode with a custom Transform</span></span>

<span data-ttu-id="72ccc-104">When encoding with Azure Media Services, you can get started quickly with one of the recommended built-in presets based on industry best practices as demonstrated in the [Streaming files](stream-files-tutorial-with-api.md) tutorial, or you can choose to build a custom preset to target your specific scenario or device requirements.</span><span class="sxs-lookup"><span data-stu-id="72ccc-104">When encoding with Azure Media Services, you can get started quickly with one of the recommended built-in presets based on industry best practices as demonstrated in the [Streaming files](stream-files-tutorial-with-api.md) tutorial, or you can choose to build a custom preset to target your specific scenario or device requirements.</span></span> 

> [!Note]
> <span data-ttu-id="72ccc-105">In Azure Media Services v3, all of the encoding bit rates are in bits per second.</span><span class="sxs-lookup"><span data-stu-id="72ccc-105">In Azure Media Services v3, all of the encoding bit rates are in bits per second.</span></span> <span data-ttu-id="72ccc-106">This is different than the REST v2 Media Encoder Standard presets.</span><span class="sxs-lookup"><span data-stu-id="72ccc-106">This is different than the REST v2 Media Encoder Standard presets.</span></span> <span data-ttu-id="72ccc-107">For example, the bitrate in v2 would be specified as 128, but in v3 it would be 128000.</span><span class="sxs-lookup"><span data-stu-id="72ccc-107">For example, the bitrate in v2 would be specified as 128, but in v3 it would be 128000.</span></span>

## <a name="download-the-sample"></a><span data-ttu-id="72ccc-108">Download the sample</span><span class="sxs-lookup"><span data-stu-id="72ccc-108">Download the sample</span></span>

<span data-ttu-id="72ccc-109">Clone a GitHub repository that contains the full .NET Core sample to your machine using the following command:</span><span class="sxs-lookup"><span data-stu-id="72ccc-109">Clone a GitHub repository that contains the full .NET Core sample to your machine using the following command:</span></span>  

 ```bash
 git clone https://github.com/Azure-Samples/media-services-v3-dotnet-core-tutorials.git
 ```
 
<span data-ttu-id="72ccc-110">The custom preset sample is located in the [EncodeCustomTransform](https://github.com/Azure-Samples/media-services-v3-dotnet-core-tutorials/blob/master/NETCore/EncodeCustomTransform/) folder.</span><span class="sxs-lookup"><span data-stu-id="72ccc-110">The custom preset sample is located in the [EncodeCustomTransform](https://github.com/Azure-Samples/media-services-v3-dotnet-core-tutorials/blob/master/NETCore/EncodeCustomTransform/) folder.</span></span>

## <a name="create-a-transform-with-a-custom-preset"></a><span data-ttu-id="72ccc-111">Create a transform with a custom preset</span><span class="sxs-lookup"><span data-stu-id="72ccc-111">Create a transform with a custom preset</span></span> 

<span data-ttu-id="72ccc-112">When creating a new [Transform](https://docs.microsoft.com/rest/api/media/transforms), you need to specify what you want it to produce as an output.</span><span class="sxs-lookup"><span data-stu-id="72ccc-112">When creating a new [Transform](https://docs.microsoft.com/rest/api/media/transforms), you need to specify what you want it to produce as an output.</span></span> <span data-ttu-id="72ccc-113">The required parameter is a **TransformOutput** object, as shown in the code below.</span><span class="sxs-lookup"><span data-stu-id="72ccc-113">The required parameter is a **TransformOutput** object, as shown in the code below.</span></span> <span data-ttu-id="72ccc-114">Each **TransformOutput** contains a **Preset**.</span><span class="sxs-lookup"><span data-stu-id="72ccc-114">Each **TransformOutput** contains a **Preset**.</span></span> <span data-ttu-id="72ccc-115">**Preset** describes the step-by-step instructions of video and/or audio processing operations that are to be used to generate the desired **TransformOutput**.</span><span class="sxs-lookup"><span data-stu-id="72ccc-115">**Preset** describes the step-by-step instructions of video and/or audio processing operations that are to be used to generate the desired **TransformOutput**.</span></span> <span data-ttu-id="72ccc-116">The following **TransformOutput** creates custom codec and layer output settings.</span><span class="sxs-lookup"><span data-stu-id="72ccc-116">The following **TransformOutput** creates custom codec and layer output settings.</span></span>

<span data-ttu-id="72ccc-117">When creating a [Transform](https://docs.microsoft.com/rest/api/media/transforms), you should first check if one already exists using the **Get** method, as shown in the code that follows.</span><span class="sxs-lookup"><span data-stu-id="72ccc-117">When creating a [Transform](https://docs.microsoft.com/rest/api/media/transforms), you should first check if one already exists using the **Get** method, as shown in the code that follows.</span></span>  <span data-ttu-id="72ccc-118">In Media Services v3, **Get** methods on entities return **null** if the entity doesn't exist (a case-insensitive check on the name).</span><span class="sxs-lookup"><span data-stu-id="72ccc-118">In Media Services v3, **Get** methods on entities return **null** if the entity doesn't exist (a case-insensitive check on the name).</span></span>

[!code-csharp[Main](../../../media-services-v3-dotnet-core-tutorials/NETCore/EncodeCustomTransform/MediaV3ConsoleApp/Program.cs#EnsureTransformExists)]

## <a name="next-steps"></a><span data-ttu-id="72ccc-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="72ccc-119">Next steps</span></span>

[<span data-ttu-id="72ccc-120">Streaming files</span><span class="sxs-lookup"><span data-stu-id="72ccc-120">Streaming files</span></span>](stream-files-tutorial-with-api.md) 
