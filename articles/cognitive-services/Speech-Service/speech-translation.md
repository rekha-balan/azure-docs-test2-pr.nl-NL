---
title: About Speech Translation
description: An overview of the capabilities of Speech Translation
titleSuffix: Microsoft Cognitive Services
services: cognitive-services
author: v-jerkin
ms.service: cognitive-services
ms.component: speech-service
ms.topic: article
ms.date: 04/28/2018
ms.author: v-jerkin
ms.openlocfilehash: 3559a25f3073f88e99379e98bc4562209b0c0825
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871220"
---
# <a name="about-the-speech-translation-api"></a><span data-ttu-id="d2396-103">About the Speech Translation API</span><span class="sxs-lookup"><span data-stu-id="d2396-103">About the Speech Translation API</span></span>

<span data-ttu-id="d2396-104">The Microsoft Speech API lets you add end-to-end, real-time, multi-language translation  of speech to your applications, tools, and devices.</span><span class="sxs-lookup"><span data-stu-id="d2396-104">The Microsoft Speech API lets you add end-to-end, real-time, multi-language translation  of speech to your applications, tools, and devices.</span></span> <span data-ttu-id="d2396-105">The same API can be used for both speech-to-speech and speech-to-text translation.</span><span class="sxs-lookup"><span data-stu-id="d2396-105">The same API can be used for both speech-to-speech and speech-to-text translation.</span></span>

<span data-ttu-id="d2396-106">With the Microsoft Translator Speech API, client applications stream speech audio to the service and receive back a stream of results.</span><span class="sxs-lookup"><span data-stu-id="d2396-106">With the Microsoft Translator Speech API, client applications stream speech audio to the service and receive back a stream of results.</span></span> <span data-ttu-id="d2396-107">These results include the recognized text in the source language and its translation in the target language.</span><span class="sxs-lookup"><span data-stu-id="d2396-107">These results include the recognized text in the source language and its translation in the target language.</span></span> <span data-ttu-id="d2396-108">Interim translations can be provided until an utterance is complete, at which time a final translation is provided.</span><span class="sxs-lookup"><span data-stu-id="d2396-108">Interim translations can be provided until an utterance is complete, at which time a final translation is provided.</span></span>

<span data-ttu-id="d2396-109">Optionally, a synthesized audio version of the final translation can be prepared, enabling true speech-to-speech translation.</span><span class="sxs-lookup"><span data-stu-id="d2396-109">Optionally, a synthesized audio version of the final translation can be prepared, enabling true speech-to-speech translation.</span></span>

<span data-ttu-id="d2396-110">The Speech Translation API uses a WebSockets protocol to provide a full-duplex communication channel between the client and the server.</span><span class="sxs-lookup"><span data-stu-id="d2396-110">The Speech Translation API uses a WebSockets protocol to provide a full-duplex communication channel between the client and the server.</span></span> <span data-ttu-id="d2396-111">But you don't need to deal with WebSockets; the Speech SDK handles that for you.</span><span class="sxs-lookup"><span data-stu-id="d2396-111">But you don't need to deal with WebSockets; the Speech SDK handles that for you.</span></span>

<span data-ttu-id="d2396-112">The Speech Translation API employs the same technologies that power various Microsoft products and services.</span><span class="sxs-lookup"><span data-stu-id="d2396-112">The Speech Translation API employs the same technologies that power various Microsoft products and services.</span></span> <span data-ttu-id="d2396-113">This service is already used by thousands of businesses worldwide in their applications and workflows.</span><span class="sxs-lookup"><span data-stu-id="d2396-113">This service is already used by thousands of businesses worldwide in their applications and workflows.</span></span>

## <a name="about-the-technology"></a><span data-ttu-id="d2396-114">About the technology</span><span class="sxs-lookup"><span data-stu-id="d2396-114">About the technology</span></span>

<span data-ttu-id="d2396-115">Underlying Microsoft's translation engine are two different approaches: statistical machine translation (SMT) and neural machine translation (NMT).</span><span class="sxs-lookup"><span data-stu-id="d2396-115">Underlying Microsoft's translation engine are two different approaches: statistical machine translation (SMT) and neural machine translation (NMT).</span></span> <span data-ttu-id="d2396-116">The latter, an artificial intelligence approach employing neural networks, is the more modern approach to machine translation.</span><span class="sxs-lookup"><span data-stu-id="d2396-116">The latter, an artificial intelligence approach employing neural networks, is the more modern approach to machine translation.</span></span> <span data-ttu-id="d2396-117">NMT provides better translations — not just more accurate, but also more fluent and natural.</span><span class="sxs-lookup"><span data-stu-id="d2396-117">NMT provides better translations — not just more accurate, but also more fluent and natural.</span></span> <span data-ttu-id="d2396-118">The key reason for this fluidity is that NMT uses the full context of a sentence to translate words.</span><span class="sxs-lookup"><span data-stu-id="d2396-118">The key reason for this fluidity is that NMT uses the full context of a sentence to translate words.</span></span>

<span data-ttu-id="d2396-119">Today, Microsoft has migrated to NMT for the most popular languages, employing SMT only for less-frequently-used languages.</span><span class="sxs-lookup"><span data-stu-id="d2396-119">Today, Microsoft has migrated to NMT for the most popular languages, employing SMT only for less-frequently-used languages.</span></span> <span data-ttu-id="d2396-120">All [languages available for speech-to-speech translation](supported-languages.md#speech-translation) are powered by NMT.</span><span class="sxs-lookup"><span data-stu-id="d2396-120">All [languages available for speech-to-speech translation](supported-languages.md#speech-translation) are powered by NMT.</span></span> <span data-ttu-id="d2396-121">Speech-to-text translation may use SMT or NMT depending on the language pair.</span><span class="sxs-lookup"><span data-stu-id="d2396-121">Speech-to-text translation may use SMT or NMT depending on the language pair.</span></span> <span data-ttu-id="d2396-122">If the target language is supported by NMT, the full translation is NMT-powered.</span><span class="sxs-lookup"><span data-stu-id="d2396-122">If the target language is supported by NMT, the full translation is NMT-powered.</span></span> <span data-ttu-id="d2396-123">If the target language isn't supported by NMT, the translation is a hybrid of NMT and SMT, using English as a "pivot" between the two languages.</span><span class="sxs-lookup"><span data-stu-id="d2396-123">If the target language isn't supported by NMT, the translation is a hybrid of NMT and SMT, using English as a "pivot" between the two languages.</span></span>

<span data-ttu-id="d2396-124">The differences between models are internal to the translation engine.</span><span class="sxs-lookup"><span data-stu-id="d2396-124">The differences between models are internal to the translation engine.</span></span> <span data-ttu-id="d2396-125">End users notice only the improved translation quality, especially for Chinese, Japanese, and Arabic.</span><span class="sxs-lookup"><span data-stu-id="d2396-125">End users notice only the improved translation quality, especially for Chinese, Japanese, and Arabic.</span></span>

> [!NOTE]
> <span data-ttu-id="d2396-126">Interested in learning more about the technology behind Microsoft's translation engine?</span><span class="sxs-lookup"><span data-stu-id="d2396-126">Interested in learning more about the technology behind Microsoft's translation engine?</span></span> <span data-ttu-id="d2396-127">See [Machine Translation](https://www.microsoft.com/en-us/translator/mt.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2396-127">See [Machine Translation](https://www.microsoft.com/en-us/translator/mt.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2396-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="d2396-128">Next steps</span></span>

* [<span data-ttu-id="d2396-129">Get your Speech trial subscription</span><span class="sxs-lookup"><span data-stu-id="d2396-129">Get your Speech trial subscription</span></span>](https://azure.microsoft.com/try/cognitive-services/)
* [<span data-ttu-id="d2396-130">See how to translate speech in C#</span><span class="sxs-lookup"><span data-stu-id="d2396-130">See how to translate speech in C#</span></span>](how-to-translate-speech-csharp.md)
* [<span data-ttu-id="d2396-131">See how to translate speech in C++</span><span class="sxs-lookup"><span data-stu-id="d2396-131">See how to translate speech in C++</span></span>](how-to-translate-speech-cpp.md)
* [<span data-ttu-id="d2396-132">See how to translate speech in Java</span><span class="sxs-lookup"><span data-stu-id="d2396-132">See how to translate speech in Java</span></span>](how-to-translate-speech-java.md)
