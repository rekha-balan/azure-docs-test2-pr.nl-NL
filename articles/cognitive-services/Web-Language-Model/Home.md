---
title: Overview of the Web Language Model API - Azure Cognitive Services | Microsoft Docs
description: Web Language Model API in Microsoft Cognitive Services provides state-of-the-art tools for natural language processing.
services: cognitive-services
author: piyushbehre
manager: yanbo
ms.service: cognitive-services
ms.component: web-language-model
ms.topic: overview
ms.date: 08/12/2016
ms.author: pibehre
ms.openlocfilehash: dc5dc0519e33e024014033ac5260004482b419c2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774338"
---
# <a name="what-is-the-web-language-model-api-preview"></a><span data-ttu-id="5a908-103">What is the Web Language Model API?</span><span class="sxs-lookup"><span data-stu-id="5a908-103">What is the Web Language Model API?</span></span> <span data-ttu-id="5a908-104">(Preview)</span><span class="sxs-lookup"><span data-stu-id="5a908-104">(Preview)</span></span>

<span data-ttu-id="5a908-105">The Microsoft Web Language Model API is a REST-based cloud service providing state-of-the-art tools for natural language processing.</span><span class="sxs-lookup"><span data-stu-id="5a908-105">The Microsoft Web Language Model API is a REST-based cloud service providing state-of-the-art tools for natural language processing.</span></span> <span data-ttu-id="5a908-106">Using this API, your application can leverage the power of big data through language models trained on web-scale corpora collected by Bing in the en-US market.</span><span class="sxs-lookup"><span data-stu-id="5a908-106">Using this API, your application can leverage the power of big data through language models trained on web-scale corpora collected by Bing in the en-US market.</span></span>

<span data-ttu-id="5a908-107">These smoothed backoff N-gram language models, supporting up to fifth-order Markov chains, are trained on the following corpora:</span><span class="sxs-lookup"><span data-stu-id="5a908-107">These smoothed backoff N-gram language models, supporting up to fifth-order Markov chains, are trained on the following corpora:</span></span>

- <span data-ttu-id="5a908-108">Web page body text</span><span class="sxs-lookup"><span data-stu-id="5a908-108">Web page body text</span></span>
- <span data-ttu-id="5a908-109">Web page title text</span><span class="sxs-lookup"><span data-stu-id="5a908-109">Web page title text</span></span>
- <span data-ttu-id="5a908-110">Web page anchor text</span><span class="sxs-lookup"><span data-stu-id="5a908-110">Web page anchor text</span></span>
- <span data-ttu-id="5a908-111">Web search query text</span><span class="sxs-lookup"><span data-stu-id="5a908-111">Web search query text</span></span>

<span data-ttu-id="5a908-112">The Web Language Model API supports four lookup operations:</span><span class="sxs-lookup"><span data-stu-id="5a908-112">The Web Language Model API supports four lookup operations:</span></span>

1. <span data-ttu-id="5a908-113">Joint (log10) probability of a sequence of words.</span><span class="sxs-lookup"><span data-stu-id="5a908-113">Joint (log10) probability of a sequence of words.</span></span>
2. <span data-ttu-id="5a908-114">Conditional (log10) probability of one word given a sequence of preceding words.</span><span class="sxs-lookup"><span data-stu-id="5a908-114">Conditional (log10) probability of one word given a sequence of preceding words.</span></span>
3. <span data-ttu-id="5a908-115">List of words (completions) most likely to follow a given sequence of words.</span><span class="sxs-lookup"><span data-stu-id="5a908-115">List of words (completions) most likely to follow a given sequence of words.</span></span>
4. <span data-ttu-id="5a908-116">Word breaking of strings that contain no spaces.</span><span class="sxs-lookup"><span data-stu-id="5a908-116">Word breaking of strings that contain no spaces.</span></span>

## <a name="getting-started"></a><span data-ttu-id="5a908-117">Getting Started</span><span class="sxs-lookup"><span data-stu-id="5a908-117">Getting Started</span></span>

1. <span data-ttu-id="5a908-118">Subscribe to the service.</span><span class="sxs-lookup"><span data-stu-id="5a908-118">Subscribe to the service.</span></span>
2. <span data-ttu-id="5a908-119">Download the [SDK](https://www.github.com/microsoft/cognitive-weblm-windows).</span><span class="sxs-lookup"><span data-stu-id="5a908-119">Download the [SDK](https://www.github.com/microsoft/cognitive-weblm-windows).</span></span>
3. <span data-ttu-id="5a908-120">Run the SDK sample code.</span><span class="sxs-lookup"><span data-stu-id="5a908-120">Run the SDK sample code.</span></span>
4. <span data-ttu-id="5a908-121">Refer to the [API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/55de9ca4e597ed1fd4e2f104) for full details of the endpoints, including code snippets in a variety of languages.</span><span class="sxs-lookup"><span data-stu-id="5a908-121">Refer to the [API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/55de9ca4e597ed1fd4e2f104) for full details of the endpoints, including code snippets in a variety of languages.</span></span>

## <a name="underlying-technology"></a><span data-ttu-id="5a908-122">Underlying Technology</span><span class="sxs-lookup"><span data-stu-id="5a908-122">Underlying Technology</span></span>

<span data-ttu-id="5a908-123">The following paper provides details on the development of these language models, and should be cited in research publications that use this service:</span><span class="sxs-lookup"><span data-stu-id="5a908-123">The following paper provides details on the development of these language models, and should be cited in research publications that use this service:</span></span>

- <span data-ttu-id="5a908-124">[An Overview of Microsoft Web N-gram Corpus and Applications](http://research.microsoft.com/apps/pubs/default.aspx?id=130762), NAACL-HLT 2010</span><span class="sxs-lookup"><span data-stu-id="5a908-124">[An Overview of Microsoft Web N-gram Corpus and Applications](http://research.microsoft.com/apps/pubs/default.aspx?id=130762), NAACL-HLT 2010</span></span>

<span data-ttu-id="5a908-125">Click [here](https://academic.microsoft.com/#/search?iq=And%28Ty%3D'0'%2CRId%3D2145833060%29&q=papers%20citing%20an%20overview%20of%20microsoft%20web%20n%20gram%20corpus%20and%20applications&filters=&from=0&sort=0) for a current list of papers citing this work.</span><span class="sxs-lookup"><span data-stu-id="5a908-125">Click [here](https://academic.microsoft.com/#/search?iq=And%28Ty%3D'0'%2CRId%3D2145833060%29&q=papers%20citing%20an%20overview%20of%20microsoft%20web%20n%20gram%20corpus%20and%20applications&filters=&from=0&sort=0) for a current list of papers citing this work.</span></span>
