---
title: About Speech to Text
description: An overview of the capabilities of Speech to Text API.
titleSuffix: Microsoft Cognitive Services
services: cognitive-services
author: v-jerkin
ms.service: cognitive-services
ms.component: speech-service
ms.topic: article
ms.date: 05/07/2018
ms.author: v-jerkin
ms.openlocfilehash: ba6710c8b5b8de1c63fa6778ea3853ab52365254
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967476"
---
# <a name="about-the-speech-to-text-api"></a><span data-ttu-id="2a2af-103">About the Speech to Text API</span><span class="sxs-lookup"><span data-stu-id="2a2af-103">About the Speech to Text API</span></span>

<span data-ttu-id="2a2af-104">The **Speech to Text** API *transcribes* audio streams into text that your application can display to the user or act upon as command input.</span><span class="sxs-lookup"><span data-stu-id="2a2af-104">The **Speech to Text** API *transcribes* audio streams into text that your application can display to the user or act upon as command input.</span></span> <span data-ttu-id="2a2af-105">The APIs can be used either with an SDK client library (for supported platforms and languages) or a REST API.</span><span class="sxs-lookup"><span data-stu-id="2a2af-105">The APIs can be used either with an SDK client library (for supported platforms and languages) or a REST API.</span></span>

<span data-ttu-id="2a2af-106">The **Speech to Text** API offers the following features:</span><span class="sxs-lookup"><span data-stu-id="2a2af-106">The **Speech to Text** API offers the following features:</span></span>

- <span data-ttu-id="2a2af-107">Advanced speech recognition technology from Microsoft—the same used by Cortana, Office, and other Microsoft products.</span><span class="sxs-lookup"><span data-stu-id="2a2af-107">Advanced speech recognition technology from Microsoft—the same used by Cortana, Office, and other Microsoft products.</span></span>

- <span data-ttu-id="2a2af-108">Real-time continuous recognition.</span><span class="sxs-lookup"><span data-stu-id="2a2af-108">Real-time continuous recognition.</span></span> <span data-ttu-id="2a2af-109">**Speech to Text** allows users to transcribe audio into text in real time.</span><span class="sxs-lookup"><span data-stu-id="2a2af-109">**Speech to Text** allows users to transcribe audio into text in real time.</span></span> <span data-ttu-id="2a2af-110">It also supports receiving intermediate results of the words that have been recognized so far.</span><span class="sxs-lookup"><span data-stu-id="2a2af-110">It also supports receiving intermediate results of the words that have been recognized so far.</span></span> <span data-ttu-id="2a2af-111">The service automatically recognizes the end of speech.</span><span class="sxs-lookup"><span data-stu-id="2a2af-111">The service automatically recognizes the end of speech.</span></span> <span data-ttu-id="2a2af-112">Users can also choose additional formatting options, including capitalization and punctuation, profanity masking, and inverse text normalization.</span><span class="sxs-lookup"><span data-stu-id="2a2af-112">Users can also choose additional formatting options, including capitalization and punctuation, profanity masking, and inverse text normalization.</span></span>

- <span data-ttu-id="2a2af-113">Optimized **Speech to Text** results for interactive, conversation, and dictation scenarios.</span><span class="sxs-lookup"><span data-stu-id="2a2af-113">Optimized **Speech to Text** results for interactive, conversation, and dictation scenarios.</span></span> 

- <span data-ttu-id="2a2af-114">Support for many spoken languages and dialects.</span><span class="sxs-lookup"><span data-stu-id="2a2af-114">Support for many spoken languages and dialects.</span></span> <span data-ttu-id="2a2af-115">For the full list of supported languages in each recognition mode, see [Supported languages](supported-languages.md#speech-to-text).</span><span class="sxs-lookup"><span data-stu-id="2a2af-115">For the full list of supported languages in each recognition mode, see [Supported languages](supported-languages.md#speech-to-text).</span></span>

- <span data-ttu-id="2a2af-116">Customized language and acoustic models, so you can tailor your application to your users' specialized domain vocabulary, speaking environment and way of speaking.</span><span class="sxs-lookup"><span data-stu-id="2a2af-116">Customized language and acoustic models, so you can tailor your application to your users' specialized domain vocabulary, speaking environment and way of speaking.</span></span>

- <span data-ttu-id="2a2af-117">Natural-language understanding.</span><span class="sxs-lookup"><span data-stu-id="2a2af-117">Natural-language understanding.</span></span> <span data-ttu-id="2a2af-118">Through integration with [Language Understanding](https://docs.microsoft.com/azure/cognitive-services/luis/) (LUIS), you can derive intents and entities from speech.</span><span class="sxs-lookup"><span data-stu-id="2a2af-118">Through integration with [Language Understanding](https://docs.microsoft.com/azure/cognitive-services/luis/) (LUIS), you can derive intents and entities from speech.</span></span> <span data-ttu-id="2a2af-119">Users don't have to know your app's vocabulary, but can describe what they want in their own words.</span><span class="sxs-lookup"><span data-stu-id="2a2af-119">Users don't have to know your app's vocabulary, but can describe what they want in their own words.</span></span>

## <a name="api-capabilities"></a><span data-ttu-id="2a2af-120">API capabilities</span><span class="sxs-lookup"><span data-stu-id="2a2af-120">API capabilities</span></span>

<span data-ttu-id="2a2af-121">Some capabilities of the **Speech to Text** API are not available via REST.</span><span class="sxs-lookup"><span data-stu-id="2a2af-121">Some capabilities of the **Speech to Text** API are not available via REST.</span></span> <span data-ttu-id="2a2af-122">The following table summarizes the capabilities of each method of accessing the API.</span><span class="sxs-lookup"><span data-stu-id="2a2af-122">The following table summarizes the capabilities of each method of accessing the API.</span></span>

| <span data-ttu-id="2a2af-123">Use case</span><span class="sxs-lookup"><span data-stu-id="2a2af-123">Use case</span></span> | <span data-ttu-id="2a2af-124">REST</span><span class="sxs-lookup"><span data-stu-id="2a2af-124">REST</span></span> | <span data-ttu-id="2a2af-125">SDKs</span><span class="sxs-lookup"><span data-stu-id="2a2af-125">SDKs</span></span> |
|-----|-----|-----|----|
| <span data-ttu-id="2a2af-126">Transcribe a short utterance, such as a command (length < 15 s); no interim results</span><span class="sxs-lookup"><span data-stu-id="2a2af-126">Transcribe a short utterance, such as a command (length < 15 s); no interim results</span></span> | <span data-ttu-id="2a2af-127">Yes</span><span class="sxs-lookup"><span data-stu-id="2a2af-127">Yes</span></span> | <span data-ttu-id="2a2af-128">Yes</span><span class="sxs-lookup"><span data-stu-id="2a2af-128">Yes</span></span> |
| <span data-ttu-id="2a2af-129">Transcribe a longer utterance (> 15 s)</span><span class="sxs-lookup"><span data-stu-id="2a2af-129">Transcribe a longer utterance (> 15 s)</span></span> | <span data-ttu-id="2a2af-130">No</span><span class="sxs-lookup"><span data-stu-id="2a2af-130">No</span></span> | <span data-ttu-id="2a2af-131">Yes</span><span class="sxs-lookup"><span data-stu-id="2a2af-131">Yes</span></span> |
| <span data-ttu-id="2a2af-132">Transcribe streaming audio with optional interim results</span><span class="sxs-lookup"><span data-stu-id="2a2af-132">Transcribe streaming audio with optional interim results</span></span> | <span data-ttu-id="2a2af-133">No</span><span class="sxs-lookup"><span data-stu-id="2a2af-133">No</span></span> | <span data-ttu-id="2a2af-134">Yes</span><span class="sxs-lookup"><span data-stu-id="2a2af-134">Yes</span></span> |
| <span data-ttu-id="2a2af-135">Understand speaker intents via LUIS</span><span class="sxs-lookup"><span data-stu-id="2a2af-135">Understand speaker intents via LUIS</span></span> | <span data-ttu-id="2a2af-136">No\*</span><span class="sxs-lookup"><span data-stu-id="2a2af-136">No\*</span></span> | <span data-ttu-id="2a2af-137">Yes</span><span class="sxs-lookup"><span data-stu-id="2a2af-137">Yes</span></span> |

<span data-ttu-id="2a2af-138">\* *LUIS intents and entities can be derived using a separate LUIS subscription. With this subscription, the SDK can call LUIS for you and provide entity and intent results as well as speech transcriptions. With the REST API, you can call LUIS yourself to derive intents and entities with your LUIS subscription.*</span><span class="sxs-lookup"><span data-stu-id="2a2af-138">\* *LUIS intents and entities can be derived using a separate LUIS subscription. With this subscription, the SDK can call LUIS for you and provide entity and intent results as well as speech transcriptions. With the REST API, you can call LUIS yourself to derive intents and entities with your LUIS subscription.*</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a2af-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="2a2af-139">Next steps</span></span>

* [<span data-ttu-id="2a2af-140">Get your Speech trial subscription</span><span class="sxs-lookup"><span data-stu-id="2a2af-140">Get your Speech trial subscription</span></span>](https://azure.microsoft.com/try/cognitive-services/)
* [<span data-ttu-id="2a2af-141">Quickstart: recognize speech in C#</span><span class="sxs-lookup"><span data-stu-id="2a2af-141">Quickstart: recognize speech in C#</span></span>](quickstart-csharp-dotnet-windows.md)
* [<span data-ttu-id="2a2af-142">See how to recognize intents from speech in C#</span><span class="sxs-lookup"><span data-stu-id="2a2af-142">See how to recognize intents from speech in C#</span></span>](how-to-recognize-intents-from-speech-csharp.md)
