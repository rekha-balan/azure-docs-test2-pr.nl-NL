---
title: Azure Government AI and Cognitive Services | Microsoft Docs
description: This provides a comparision of features and guidance on developing applications for Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: jglixon
manager: zakramer
ms.assetid: c00ccd0c-0345-49ee-84f0-15262ff05923
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 7/25/2017
ms.author: jglixon
ms.openlocfilehash: 8cd96d258136c6a39f43badf7604b2a6944d2066
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867964"
---
# <a name="azure-government-ai-and-cognitive-services"></a><span data-ttu-id="eb806-103">Azure Government AI and Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="eb806-103">Azure Government AI and Cognitive Services</span></span>

## <a name="cognitive-services"></a><span data-ttu-id="eb806-104">Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="eb806-104">Cognitive Services</span></span> 
<span data-ttu-id="eb806-105">The following Cognitive Services APIs are currently in Public Preview in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="eb806-105">The following Cognitive Services APIs are currently in Public Preview in Azure Government.</span></span> 
- <span data-ttu-id="eb806-106">Computer Vision API</span><span class="sxs-lookup"><span data-stu-id="eb806-106">Computer Vision API</span></span>
- <span data-ttu-id="eb806-107">Face API</span><span class="sxs-lookup"><span data-stu-id="eb806-107">Face API</span></span>
- <span data-ttu-id="eb806-108">Translator Speech API</span><span class="sxs-lookup"><span data-stu-id="eb806-108">Translator Speech API</span></span>
- <span data-ttu-id="eb806-109">Translator Text API</span><span class="sxs-lookup"><span data-stu-id="eb806-109">Translator Text API</span></span>

### <a name="variations"></a><span data-ttu-id="eb806-110">Variations</span><span class="sxs-lookup"><span data-stu-id="eb806-110">Variations</span></span>
- <span data-ttu-id="eb806-111">Provisioning and management for the following APIs are available through PowerShell and CLI only (**no Portal Support**).</span><span class="sxs-lookup"><span data-stu-id="eb806-111">Provisioning and management for the following APIs are available through PowerShell and CLI only (**no Portal Support**).</span></span>

### <a name="quickstarts"></a><span data-ttu-id="eb806-112">Quickstarts</span><span class="sxs-lookup"><span data-stu-id="eb806-112">Quickstarts</span></span>
<span data-ttu-id="eb806-113">The [Azure Government Cognitive Services Quickstart](documentation-government-cognitiveservices.md) will guide you through getting started with provisioning an account and accessing the APIs.</span><span class="sxs-lookup"><span data-stu-id="eb806-113">The [Azure Government Cognitive Services Quickstart](documentation-government-cognitiveservices.md) will guide you through getting started with provisioning an account and accessing the APIs.</span></span>

#### <a name="vision"></a><span data-ttu-id="eb806-114">Vision</span><span class="sxs-lookup"><span data-stu-id="eb806-114">Vision</span></span>

##### <a name="computer-vision-api"></a><span data-ttu-id="eb806-115">Computer Vision API</span><span class="sxs-lookup"><span data-stu-id="eb806-115">Computer Vision API</span></span>
<span data-ttu-id="eb806-116">The following variations exist for Computer Vision API from Commercial Azure:</span><span class="sxs-lookup"><span data-stu-id="eb806-116">The following variations exist for Computer Vision API from Commercial Azure:</span></span>
- <span data-ttu-id="eb806-117">Endpoint URL: https://virginia.api.cognitive.microsoft.us/vision/v1.0/</span><span class="sxs-lookup"><span data-stu-id="eb806-117">Endpoint URL: https://virginia.api.cognitive.microsoft.us/vision/v1.0/</span></span>
- <span data-ttu-id="eb806-118">Available SKUs: F0, S0, S1</span><span class="sxs-lookup"><span data-stu-id="eb806-118">Available SKUs: F0, S0, S1</span></span>

<span data-ttu-id="eb806-119">For more information, please see [public documentation](../cognitive-services/computer-vision/index.yml) and [public API documentation](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa) for Computer Vision API.</span><span class="sxs-lookup"><span data-stu-id="eb806-119">For more information, please see [public documentation](../cognitive-services/computer-vision/index.yml) and [public API documentation](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa) for Computer Vision API.</span></span>
 
##### <a name="face-api"></a><span data-ttu-id="eb806-120">Face API</span><span class="sxs-lookup"><span data-stu-id="eb806-120">Face API</span></span>
<span data-ttu-id="eb806-121">The following variations exist for Face API from Commercial Azure:</span><span class="sxs-lookup"><span data-stu-id="eb806-121">The following variations exist for Face API from Commercial Azure:</span></span>
- <span data-ttu-id="eb806-122">Endpoint: https://virginia.api.cognitive.microsoft.us/face/v1.0/</span><span class="sxs-lookup"><span data-stu-id="eb806-122">Endpoint: https://virginia.api.cognitive.microsoft.us/face/v1.0/</span></span>
- <span data-ttu-id="eb806-123">Available SKUs: F0, S0</span><span class="sxs-lookup"><span data-stu-id="eb806-123">Available SKUs: F0, S0</span></span>
 
<span data-ttu-id="eb806-124">For more information, please see [public documentation](../cognitive-services/Face/index.yml) and [public API documentation](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) for Face API.</span><span class="sxs-lookup"><span data-stu-id="eb806-124">For more information, please see [public documentation](../cognitive-services/Face/index.yml) and [public API documentation](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) for Face API.</span></span>

##### <a name="emotion-api"></a><span data-ttu-id="eb806-125">Emotion API</span><span class="sxs-lookup"><span data-stu-id="eb806-125">Emotion API</span></span>
<span data-ttu-id="eb806-126">Emotion API is being deprecated and all of its technology has been incorporated to Face API.</span><span class="sxs-lookup"><span data-stu-id="eb806-126">Emotion API is being deprecated and all of its technology has been incorporated to Face API.</span></span>
 
#### <a name="speech"></a><span data-ttu-id="eb806-127">Speech</span><span class="sxs-lookup"><span data-stu-id="eb806-127">Speech</span></span>
 
##### <a name="translator-speech-api-speech-translation"></a><span data-ttu-id="eb806-128">Translator Speech API (Speech Translation):</span><span class="sxs-lookup"><span data-stu-id="eb806-128">Translator Speech API (Speech Translation):</span></span> 
<span data-ttu-id="eb806-129">The following variations exist for Translator Speech API from Commercial Azure:</span><span class="sxs-lookup"><span data-stu-id="eb806-129">The following variations exist for Translator Speech API from Commercial Azure:</span></span>
- <span data-ttu-id="eb806-130">Endpoint: https://docs.microsoft.com/azure/cognitive-services/translator-speech/</span><span class="sxs-lookup"><span data-stu-id="eb806-130">Endpoint: https://docs.microsoft.com/azure/cognitive-services/translator-speech/</span></span>
- <span data-ttu-id="eb806-131">Auth Token Service: https://virginia.api.cognitive.microsoft.us/sts/v1.0/issueToken</span><span class="sxs-lookup"><span data-stu-id="eb806-131">Auth Token Service: https://virginia.api.cognitive.microsoft.us/sts/v1.0/issueToken</span></span>
- <span data-ttu-id="eb806-132">Available SKUs: F0, S1, S2, S3, S4</span><span class="sxs-lookup"><span data-stu-id="eb806-132">Available SKUs: F0, S1, S2, S3, S4</span></span>
 
<span data-ttu-id="eb806-133">For more information, please see [public documentation](../cognitive-services/Speech/Home.md) and [public API documentation](https://docs.microsoft.com/azure/cognitive-services/translator-speech/reference) for Bing Speech API.</span><span class="sxs-lookup"><span data-stu-id="eb806-133">For more information, please see [public documentation](../cognitive-services/Speech/Home.md) and [public API documentation](https://docs.microsoft.com/azure/cognitive-services/translator-speech/reference) for Bing Speech API.</span></span>
 
#### <a name="language"></a><span data-ttu-id="eb806-134">Language</span><span class="sxs-lookup"><span data-stu-id="eb806-134">Language</span></span>
 
##### <a name="translator-text-api-text-translation"></a><span data-ttu-id="eb806-135">Translator Text API (Text Translation):</span><span class="sxs-lookup"><span data-stu-id="eb806-135">Translator Text API (Text Translation):</span></span> 
<span data-ttu-id="eb806-136">The following variations exist for Translator Text API from Commercial Azure:</span><span class="sxs-lookup"><span data-stu-id="eb806-136">The following variations exist for Translator Text API from Commercial Azure:</span></span>
- <span data-ttu-id="eb806-137">Endpoint: https://api.microsofttranslator.us</span><span class="sxs-lookup"><span data-stu-id="eb806-137">Endpoint: https://api.microsofttranslator.us</span></span>
- <span data-ttu-id="eb806-138">Auth Token Service: https://virginia.api.cognitive.microsoft.us/sts/v1.0/issueToken</span><span class="sxs-lookup"><span data-stu-id="eb806-138">Auth Token Service: https://virginia.api.cognitive.microsoft.us/sts/v1.0/issueToken</span></span>
- <span data-ttu-id="eb806-139">Available SKUs: F0, S1, S2, S3, S4</span><span class="sxs-lookup"><span data-stu-id="eb806-139">Available SKUs: F0, S1, S2, S3, S4</span></span>
- <span data-ttu-id="eb806-140">Translator Hub, Web Widget, and Collaboration Translation Framework (CTF) are not supported.</span><span class="sxs-lookup"><span data-stu-id="eb806-140">Translator Hub, Web Widget, and Collaboration Translation Framework (CTF) are not supported.</span></span>
 
<span data-ttu-id="eb806-141">For more information, please see [public documentation](../cognitive-services/translator/translator-info-overview.md) and [public API documentation](https://docs.microsoft.com/azure/cognitive-services/Translator/reference/v3-0-reference) for Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="eb806-141">For more information, please see [public documentation](../cognitive-services/translator/translator-info-overview.md) and [public API documentation](https://docs.microsoft.com/azure/cognitive-services/Translator/reference/v3-0-reference) for Translator Text API.</span></span>


### <a name="data-considerations"></a><span data-ttu-id="eb806-142">Data Considerations</span><span class="sxs-lookup"><span data-stu-id="eb806-142">Data Considerations</span></span>
<span data-ttu-id="eb806-143">Data considerations for Cognitive Services are not yet available.</span><span class="sxs-lookup"><span data-stu-id="eb806-143">Data considerations for Cognitive Services are not yet available.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="eb806-144">Next Steps</span><span class="sxs-lookup"><span data-stu-id="eb806-144">Next Steps</span></span>
* <span data-ttu-id="eb806-145">Subscribe to the [Azure Government blog](https://blogs.msdn.microsoft.com/azuregov/)</span><span class="sxs-lookup"><span data-stu-id="eb806-145">Subscribe to the [Azure Government blog](https://blogs.msdn.microsoft.com/azuregov/)</span></span>
* <span data-ttu-id="eb806-146">Get help on Stack Overflow by using the [azure-gov](https://stackoverflow.com/questions/tagged/azure-gov) tag</span><span class="sxs-lookup"><span data-stu-id="eb806-146">Get help on Stack Overflow by using the [azure-gov](https://stackoverflow.com/questions/tagged/azure-gov) tag</span></span>
* <span data-ttu-id="eb806-147">Give us feedback or request new features via the [Azure Government feedback forum](https://feedback.azure.com/forums/558487-azure-government)</span><span class="sxs-lookup"><span data-stu-id="eb806-147">Give us feedback or request new features via the [Azure Government feedback forum](https://feedback.azure.com/forums/558487-azure-government)</span></span> 

