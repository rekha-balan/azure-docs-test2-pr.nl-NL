---
title: Overview of the Web Language Model API | Microsoft Docs
description: Web Language Model API in Microsoft Cognitive Services provides state-of-the-art tools for natural language processing.
services: cognitive-services
author: piyushbehre
manager: yanbo
ms.service: cognitive-services
ms.technology: web-language-model
ms.topic: article
ms.date: 08/12/2016
ms.author: pibehre
ms.openlocfilehash: 06f55fe4c8bd0a1576a20bde748ff84e30acb8ea
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549157"
---
# <a name="web-language-model-api-overview"></a><span data-ttu-id="bc0d4-103">Web Language Model API Overview</span><span class="sxs-lookup"><span data-stu-id="bc0d4-103">Web Language Model API Overview</span></span>

<span data-ttu-id="bc0d4-104">Welcome to the Microsoft Web Language Model API, a REST-based cloud service providing state-of-the-art tools for natural language processing.</span><span class="sxs-lookup"><span data-stu-id="bc0d4-104">Welcome to the Microsoft Web Language Model API, a REST-based cloud service providing state-of-the-art tools for natural language processing.</span></span> <span data-ttu-id="bc0d4-105">Using this API, your application can leverage the power of big data through language models trained on web-scale corpora collected by Bing in the EN-US market.</span><span class="sxs-lookup"><span data-stu-id="bc0d4-105">Using this API, your application can leverage the power of big data through language models trained on web-scale corpora collected by Bing in the EN-US market.</span></span> 

<span data-ttu-id="bc0d4-106">These smoothed backoff N-gram language models, supporting Markov order up to 5, are trained on the following corpora:</span><span class="sxs-lookup"><span data-stu-id="bc0d4-106">These smoothed backoff N-gram language models, supporting Markov order up to 5, are trained on the following corpora:</span></span> 

- <span data-ttu-id="bc0d4-107">Web page body text</span><span class="sxs-lookup"><span data-stu-id="bc0d4-107">Web page body text</span></span> 
- <span data-ttu-id="bc0d4-108">Web page title text</span><span class="sxs-lookup"><span data-stu-id="bc0d4-108">Web page title text</span></span> 
- <span data-ttu-id="bc0d4-109">Web page anchor text</span><span class="sxs-lookup"><span data-stu-id="bc0d4-109">Web page anchor text</span></span> 
- <span data-ttu-id="bc0d4-110">Web search query text</span><span class="sxs-lookup"><span data-stu-id="bc0d4-110">Web search query text</span></span> 

<span data-ttu-id="bc0d4-111">The Web LM REST API supports four lookup operations:</span><span class="sxs-lookup"><span data-stu-id="bc0d4-111">The Web LM REST API supports four lookup operations:</span></span>

1. <span data-ttu-id="bc0d4-112">Joint (log10) probability of a sequence of words.</span><span class="sxs-lookup"><span data-stu-id="bc0d4-112">Joint (log10) probability of a sequence of words.</span></span>  
2. <span data-ttu-id="bc0d4-113">Conditional (log10) probability of one word given a sequence of preceding words.</span><span class="sxs-lookup"><span data-stu-id="bc0d4-113">Conditional (log10) probability of one word given a sequence of preceding words.</span></span> 
3. <span data-ttu-id="bc0d4-114">List of words (completions) most likely to follow a given sequence of words.</span><span class="sxs-lookup"><span data-stu-id="bc0d4-114">List of words (completions) most likely to follow a given sequence of words.</span></span> 
4. <span data-ttu-id="bc0d4-115">Word breaking of strings that contain no spaces.</span><span class="sxs-lookup"><span data-stu-id="bc0d4-115">Word breaking of strings that contain no spaces.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="bc0d4-116">Getting Started</span><span class="sxs-lookup"><span data-stu-id="bc0d4-116">Getting Started</span></span>

1. <span data-ttu-id="bc0d4-117">Subscribe to the service.</span><span class="sxs-lookup"><span data-stu-id="bc0d4-117">Subscribe to the service.</span></span>
2. <span data-ttu-id="bc0d4-118">Download the [SDK](https://www.github.com/microsoft/cognitive-weblm-windows).</span><span class="sxs-lookup"><span data-stu-id="bc0d4-118">Download the [SDK](https://www.github.com/microsoft/cognitive-weblm-windows).</span></span>
3. <span data-ttu-id="bc0d4-119">Run the SDK sample code.</span><span class="sxs-lookup"><span data-stu-id="bc0d4-119">Run the SDK sample code.</span></span> 
4. <span data-ttu-id="bc0d4-120">Consult the [API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/55de9ca4e597ed1fd4e2f104) for further details, including code snippets in a variety of languages.</span><span class="sxs-lookup"><span data-stu-id="bc0d4-120">Consult the [API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/55de9ca4e597ed1fd4e2f104) for further details, including code snippets in a variety of languages.</span></span>


## <a name="underlying-technology"></a><span data-ttu-id="bc0d4-121">Underlying Technology</span><span class="sxs-lookup"><span data-stu-id="bc0d4-121">Underlying Technology</span></span>

<span data-ttu-id="bc0d4-122">The following paper provides details on the development of these language models, and should be cited in research publications that utilize this service:</span><span class="sxs-lookup"><span data-stu-id="bc0d4-122">The following paper provides details on the development of these language models, and should be cited in research publications that utilize this service:</span></span>

* <span data-ttu-id="bc0d4-123">[An Overview of Microsoft Web N-gram Corpus and Applications](http://research.microsoft.com/apps/pubs/default.aspx?id=130762), NAACL-HLT 2010</span><span class="sxs-lookup"><span data-stu-id="bc0d4-123">[An Overview of Microsoft Web N-gram Corpus and Applications](http://research.microsoft.com/apps/pubs/default.aspx?id=130762), NAACL-HLT 2010</span></span>

<span data-ttu-id="bc0d4-124">Click [here](https://academic.microsoft.com/#/search?iq=And%28Ty%3D'0'%2CRId%3D2145833060%29&q=papers%20citing%20an%20overview%20of%20microsoft%20web%20n%20gram%20corpus%20and%20applications&filters=&from=0&sort=0) for a current list of papers citing this work.</span><span class="sxs-lookup"><span data-stu-id="bc0d4-124">Click [here](https://academic.microsoft.com/#/search?iq=And%28Ty%3D'0'%2CRId%3D2145833060%29&q=papers%20citing%20an%20overview%20of%20microsoft%20web%20n%20gram%20corpus%20and%20applications&filters=&from=0&sort=0) for a current list of papers citing this work.</span></span>
