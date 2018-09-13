---
title: Custom Speech Service meters and quotas on Azure | Microsoft Docs
description: Information about meters and quotas of Custom Speech Service on Azure.
services: cognitive-services
author: PanosPeriorellis
manager: onano
ms.service: cognitive-services
ms.component: custom-speech
ms.topic: article
ms.date: 07/08/2017
ms.author: panosper
ms.openlocfilehash: d2225dec818c600febfad2f9ebc42594f6ac09ac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866359"
---
# <a name="custom-speech-service-meters-and-quotas"></a><span data-ttu-id="d2a73-103">Custom Speech Service meters and quotas</span><span class="sxs-lookup"><span data-stu-id="d2a73-103">Custom Speech Service meters and quotas</span></span>

<span data-ttu-id="d2a73-104">With cloud-based Custom Speech Service, you can customize speech models for speech-to-text transcription.</span><span class="sxs-lookup"><span data-stu-id="d2a73-104">With cloud-based Custom Speech Service, you can customize speech models for speech-to-text transcription.</span></span>

<span data-ttu-id="d2a73-105">To begin using the Custom Speech Service, go to the [Custom Speech Service portal](https://cris.ai).</span><span class="sxs-lookup"><span data-stu-id="d2a73-105">To begin using the Custom Speech Service, go to the [Custom Speech Service portal](https://cris.ai).</span></span>

<span data-ttu-id="d2a73-106">For the current pricing meters, go to the [Cognitive Services pricing for Custom Speech Service](https://azure.microsoft.com/pricing/details/cognitive-services/custom-speech-service/) page.</span><span class="sxs-lookup"><span data-stu-id="d2a73-106">For the current pricing meters, go to the [Cognitive Services pricing for Custom Speech Service](https://azure.microsoft.com/pricing/details/cognitive-services/custom-speech-service/) page.</span></span>

## <a name="tiers-explained"></a><span data-ttu-id="d2a73-107">Tiers explained</span><span class="sxs-lookup"><span data-stu-id="d2a73-107">Tiers explained</span></span>
<span data-ttu-id="d2a73-108">For testing and prototype only, we propose to use the free F0 tier.</span><span class="sxs-lookup"><span data-stu-id="d2a73-108">For testing and prototype only, we propose to use the free F0 tier.</span></span> <span data-ttu-id="d2a73-109">For production systems, we propose to use the S2 tier.</span><span class="sxs-lookup"><span data-stu-id="d2a73-109">For production systems, we propose to use the S2 tier.</span></span> <span data-ttu-id="d2a73-110">By using the S2 tier you can scale your deployment to the number of scale units (SUs) that your scenario requires.</span><span class="sxs-lookup"><span data-stu-id="d2a73-110">By using the S2 tier you can scale your deployment to the number of scale units (SUs) that your scenario requires.</span></span>

> [!NOTE]
> <span data-ttu-id="d2a73-111">You *cannot* migrate between the F0 tier and the S2 tier.</span><span class="sxs-lookup"><span data-stu-id="d2a73-111">You *cannot* migrate between the F0 tier and the S2 tier.</span></span>
>

## <a name="meters-explained"></a><span data-ttu-id="d2a73-112">Meters explained</span><span class="sxs-lookup"><span data-stu-id="d2a73-112">Meters explained</span></span>

### <a name="scale-out"></a><span data-ttu-id="d2a73-113">Scale Out</span><span class="sxs-lookup"><span data-stu-id="d2a73-113">Scale Out</span></span>
<span data-ttu-id="d2a73-114">Scale Out is a new feature that we have released with the new pricing model.</span><span class="sxs-lookup"><span data-stu-id="d2a73-114">Scale Out is a new feature that we have released with the new pricing model.</span></span> <span data-ttu-id="d2a73-115">By using Scale Out, you can control the number of concurrent requests that your model can process.</span><span class="sxs-lookup"><span data-stu-id="d2a73-115">By using Scale Out, you can control the number of concurrent requests that your model can process.</span></span>

<span data-ttu-id="d2a73-116">You can set concurrent requests by using the SU measure in the **Create Model Deployment** view.</span><span class="sxs-lookup"><span data-stu-id="d2a73-116">You can set concurrent requests by using the SU measure in the **Create Model Deployment** view.</span></span> <span data-ttu-id="d2a73-117">For more information, see [Create a custom speech-to-text endpoint](CustomSpeech-How-to-Topics/cognitive-services-custom-speech-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="d2a73-117">For more information, see [Create a custom speech-to-text endpoint](CustomSpeech-How-to-Topics/cognitive-services-custom-speech-create-endpoint.md).</span></span> <span data-ttu-id="d2a73-118">Depending on the quantity of traffic that you envisage the model consuming, you can choose an appropriate number of SUs.</span><span class="sxs-lookup"><span data-stu-id="d2a73-118">Depending on the quantity of traffic that you envisage the model consuming, you can choose an appropriate number of SUs.</span></span> 

> [!NOTE]
> <span data-ttu-id="d2a73-119">Each scale unit guarantees 5 concurrent requests.</span><span class="sxs-lookup"><span data-stu-id="d2a73-119">Each scale unit guarantees 5 concurrent requests.</span></span> <span data-ttu-id="d2a73-120">You can buy 1 or more SUs, as appropriate.</span><span class="sxs-lookup"><span data-stu-id="d2a73-120">You can buy 1 or more SUs, as appropriate.</span></span> <span data-ttu-id="d2a73-121">Because the number of SUs increases in increments of 1, the number of concurrent requests are guaranteed to increase in increments of 5.</span><span class="sxs-lookup"><span data-stu-id="d2a73-121">Because the number of SUs increases in increments of 1, the number of concurrent requests are guaranteed to increase in increments of 5.</span></span>
>

### <a name="log-management"></a><span data-ttu-id="d2a73-122">Log management</span><span class="sxs-lookup"><span data-stu-id="d2a73-122">Log management</span></span>
<span data-ttu-id="d2a73-123">You can opt to switch off audio traces for a newly deployed model at an additional cost.</span><span class="sxs-lookup"><span data-stu-id="d2a73-123">You can opt to switch off audio traces for a newly deployed model at an additional cost.</span></span> <span data-ttu-id="d2a73-124">Custom Speech Service does not log the audio requests or the transcripts from that model.</span><span class="sxs-lookup"><span data-stu-id="d2a73-124">Custom Speech Service does not log the audio requests or the transcripts from that model.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2a73-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="d2a73-125">Next steps</span></span>
<span data-ttu-id="d2a73-126">For more information about how to use the Custom Speech Service, go to the [Custom Speech Service portal](https://cris.ai).</span><span class="sxs-lookup"><span data-stu-id="d2a73-126">For more information about how to use the Custom Speech Service, go to the [Custom Speech Service portal](https://cris.ai).</span></span>

* [<span data-ttu-id="d2a73-127">Get started</span><span class="sxs-lookup"><span data-stu-id="d2a73-127">Get started</span></span>](cognitive-services-custom-speech-get-started.md)
* [<span data-ttu-id="d2a73-128">FAQ</span><span class="sxs-lookup"><span data-stu-id="d2a73-128">FAQ</span></span>](cognitive-services-custom-speech-faq.md)
* [<span data-ttu-id="d2a73-129">Glossary</span><span class="sxs-lookup"><span data-stu-id="d2a73-129">Glossary</span></span>](cognitive-services-custom-speech-glossary.md)
 