---
title: Speech service regions
description: Reference for regions of the Speech service.
services: cognitive-services
author: mahilleb-msft
ms.service: cognitive-services
ms.technology: speech
ms.topic: article
ms.date: 06/28/2018
ms.author: mahilleb
ms.openlocfilehash: d8b72ea30a10e45f5415f7ab9054d8a4b6f30789
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965569"
---
# <a name="regions-of-the-speech-service"></a><span data-ttu-id="cd1ae-103">Regions of the Speech service</span><span class="sxs-lookup"><span data-stu-id="cd1ae-103">Regions of the Speech service</span></span>

<span data-ttu-id="cd1ae-104">The Speech service is available in different regions.</span><span class="sxs-lookup"><span data-stu-id="cd1ae-104">The Speech service is available in different regions.</span></span>
<span data-ttu-id="cd1ae-105">When you create a subscription you can pick an available region, depending on your needs.</span><span class="sxs-lookup"><span data-stu-id="cd1ae-105">When you create a subscription you can pick an available region, depending on your needs.</span></span>

<span data-ttu-id="cd1ae-106">When you use your subscription you have to account for the region you picked.</span><span class="sxs-lookup"><span data-stu-id="cd1ae-106">When you use your subscription you have to account for the region you picked.</span></span>

## <a name="rest-api"></a><span data-ttu-id="cd1ae-107">REST API</span><span class="sxs-lookup"><span data-stu-id="cd1ae-107">REST API</span></span>

<span data-ttu-id="cd1ae-108">Using the REST API, pick the right region-specific endpoints.</span><span class="sxs-lookup"><span data-stu-id="cd1ae-108">Using the REST API, pick the right region-specific endpoints.</span></span>
<span data-ttu-id="cd1ae-109">See [REST APIs](rest-apis.md) for details.</span><span class="sxs-lookup"><span data-stu-id="cd1ae-109">See [REST APIs](rest-apis.md) for details.</span></span>

## <a name="speech-sdk"></a><span data-ttu-id="cd1ae-110">Speech SDK</span><span class="sxs-lookup"><span data-stu-id="cd1ae-110">Speech SDK</span></span>

<span data-ttu-id="cd1ae-111">In the [Speech SDK](speech-sdk.md), regions are specified as a string (for example, as a parameter to [SpeechFactory.FromSubscription](https://docs.microsoft.com/dotnet/api/microsoft.cognitiveservices.speech.speechfactory.fromsubscription) in the Speech SDK for C#).</span><span class="sxs-lookup"><span data-stu-id="cd1ae-111">In the [Speech SDK](speech-sdk.md), regions are specified as a string (for example, as a parameter to [SpeechFactory.FromSubscription](https://docs.microsoft.com/dotnet/api/microsoft.cognitiveservices.speech.speechfactory.fromsubscription) in the Speech SDK for C#).</span></span>

### <a name="regions-for-speech-recognition-and-translation"></a><span data-ttu-id="cd1ae-112">Regions for speech recognition and translation</span><span class="sxs-lookup"><span data-stu-id="cd1ae-112">Regions for speech recognition and translation</span></span>

<span data-ttu-id="cd1ae-113">The table below lists the available regions for **speech recognition** and **translation**:</span><span class="sxs-lookup"><span data-stu-id="cd1ae-113">The table below lists the available regions for **speech recognition** and **translation**:</span></span>

<span data-ttu-id="cd1ae-114">Region</span><span class="sxs-lookup"><span data-stu-id="cd1ae-114">Region</span></span>| <span data-ttu-id="cd1ae-115">Value for region parameter in the Speech SDK</span><span class="sxs-lookup"><span data-stu-id="cd1ae-115">Value for region parameter in the Speech SDK</span></span>| <span data-ttu-id="cd1ae-116">Portal</span><span class="sxs-lookup"><span data-stu-id="cd1ae-116">Portal</span></span>
-|-
<span data-ttu-id="cd1ae-117">West US</span><span class="sxs-lookup"><span data-stu-id="cd1ae-117">West US</span></span>| `westus`| https://westus.cris.ai
<span data-ttu-id="cd1ae-118">West US2</span><span class="sxs-lookup"><span data-stu-id="cd1ae-118">West US2</span></span>| `westus2`| https://westus2.cris.ai
<span data-ttu-id="cd1ae-119">East US</span><span class="sxs-lookup"><span data-stu-id="cd1ae-119">East US</span></span>| `eastus`| https://eastus.cris.ai
<span data-ttu-id="cd1ae-120">East US2</span><span class="sxs-lookup"><span data-stu-id="cd1ae-120">East US2</span></span>| `eastus2`| https://eastus2.cris.ai
<span data-ttu-id="cd1ae-121">East Asia</span><span class="sxs-lookup"><span data-stu-id="cd1ae-121">East Asia</span></span>| `eastasia`| https://eastasia.cris.ai
<span data-ttu-id="cd1ae-122">South East Asia</span><span class="sxs-lookup"><span data-stu-id="cd1ae-122">South East Asia</span></span>| `southeastasia`| https://southeastasia.cris.ai
<span data-ttu-id="cd1ae-123">North Europe</span><span class="sxs-lookup"><span data-stu-id="cd1ae-123">North Europe</span></span>| `northeurope`| https://northeurope.cris.ai
<span data-ttu-id="cd1ae-124">West Europe</span><span class="sxs-lookup"><span data-stu-id="cd1ae-124">West Europe</span></span>|  `westeurope`| https://westeurope.cris.ai

### <a name="regions-for-intent-recognition"></a><span data-ttu-id="cd1ae-125">Regions for intent recognition</span><span class="sxs-lookup"><span data-stu-id="cd1ae-125">Regions for intent recognition</span></span>

<span data-ttu-id="cd1ae-126">Available regions for **intent recognition** via the Speech SDK are listed in the [Language Understanding service region page](/azure/cognitive-services/luis/luis-reference-regions).</span><span class="sxs-lookup"><span data-stu-id="cd1ae-126">Available regions for **intent recognition** via the Speech SDK are listed in the [Language Understanding service region page](/azure/cognitive-services/luis/luis-reference-regions).</span></span>
<span data-ttu-id="cd1ae-127">For each publishing region listed, the corresponding Speech SDK region parameter is determined as the first part of the domain name of the endpoint.</span><span class="sxs-lookup"><span data-stu-id="cd1ae-127">For each publishing region listed, the corresponding Speech SDK region parameter is determined as the first part of the domain name of the endpoint.</span></span>
<span data-ttu-id="cd1ae-128">For example, use `westus` to specify the West US publishing region.</span><span class="sxs-lookup"><span data-stu-id="cd1ae-128">For example, use `westus` to specify the West US publishing region.</span></span>
