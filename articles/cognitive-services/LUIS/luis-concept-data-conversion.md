---
title: Data conversion concepts in LUIS - Language Understanding
titleSuffix: Azure Cognitive Services
description: Learn how utterances can be changed before predictions in Language Understanding (LUIS)
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 06/27/2018
ms.author: diberry
ms.openlocfilehash: e1d0e0a0205190846612d727fbf34404e33c3ad4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857629"
---
# <a name="data-conversion-concepts-in-luis"></a><span data-ttu-id="e6391-103">Data conversion concepts in LUIS</span><span class="sxs-lookup"><span data-stu-id="e6391-103">Data conversion concepts in LUIS</span></span>
<span data-ttu-id="e6391-104">LUIS provides a way to convert utterances from spoken utterances to text utterances before prediction.</span><span class="sxs-lookup"><span data-stu-id="e6391-104">LUIS provides a way to convert utterances from spoken utterances to text utterances before prediction.</span></span> 

## <a name="speech-to-intent-conversion-concepts"></a><span data-ttu-id="e6391-105">Speech to intent conversion concepts</span><span class="sxs-lookup"><span data-stu-id="e6391-105">Speech to intent conversion concepts</span></span>
<span data-ttu-id="e6391-106">Conversion of speech to text in LUIS allows you to send spoken utterances to an endpoint and receive a LUIS prediction response.</span><span class="sxs-lookup"><span data-stu-id="e6391-106">Conversion of speech to text in LUIS allows you to send spoken utterances to an endpoint and receive a LUIS prediction response.</span></span> <span data-ttu-id="e6391-107">The process is an integration of the [Speech](https://docs.microsoft.com/azure/cognitive-services/Speech) service with LUIS.</span><span class="sxs-lookup"><span data-stu-id="e6391-107">The process is an integration of the [Speech](https://docs.microsoft.com/azure/cognitive-services/Speech) service with LUIS.</span></span> 

### <a name="key-requirements"></a><span data-ttu-id="e6391-108">Key requirements</span><span class="sxs-lookup"><span data-stu-id="e6391-108">Key requirements</span></span>
<span data-ttu-id="e6391-109">You do not need to create a **Bing Speech API** key for this integration.</span><span class="sxs-lookup"><span data-stu-id="e6391-109">You do not need to create a **Bing Speech API** key for this integration.</span></span> <span data-ttu-id="e6391-110">A **Language Understanding** key created in the Azure portal works for this integration.</span><span class="sxs-lookup"><span data-stu-id="e6391-110">A **Language Understanding** key created in the Azure portal works for this integration.</span></span> <span data-ttu-id="e6391-111">Do not use the LUIS starter key, it will not work for this integration.</span><span class="sxs-lookup"><span data-stu-id="e6391-111">Do not use the LUIS starter key, it will not work for this integration.</span></span>

### <a name="new-endpoint"></a><span data-ttu-id="e6391-112">New endpoint</span><span class="sxs-lookup"><span data-stu-id="e6391-112">New endpoint</span></span> 
<span data-ttu-id="e6391-113">This integration creates a new endpoint and [pricing](luis-boundaries.md#key-limits) model.</span><span class="sxs-lookup"><span data-stu-id="e6391-113">This integration creates a new endpoint and [pricing](luis-boundaries.md#key-limits) model.</span></span> <span data-ttu-id="e6391-114">The endpoint, via the [Speech SDK](https://github.com/Azure-Samples/cognitive-services-speech-sdk), is able to receive both spoken and text utterances allowing you to use it as a single endpoint.</span><span class="sxs-lookup"><span data-stu-id="e6391-114">The endpoint, via the [Speech SDK](https://github.com/Azure-Samples/cognitive-services-speech-sdk), is able to receive both spoken and text utterances allowing you to use it as a single endpoint.</span></span> 

### <a name="quota-usage"></a><span data-ttu-id="e6391-115">Quota usage</span><span class="sxs-lookup"><span data-stu-id="e6391-115">Quota usage</span></span>
<span data-ttu-id="e6391-116">See [Key limits](luis-boundaries.md#key-limits) for information.</span><span class="sxs-lookup"><span data-stu-id="e6391-116">See [Key limits](luis-boundaries.md#key-limits) for information.</span></span> 

### <a name="data-retention"></a><span data-ttu-id="e6391-117">Data retention</span><span class="sxs-lookup"><span data-stu-id="e6391-117">Data retention</span></span>
<span data-ttu-id="e6391-118">The data sent to the endpoint, via the Speech SDK, regardless if it is speech or text, is only used to enhance your speech model.</span><span class="sxs-lookup"><span data-stu-id="e6391-118">The data sent to the endpoint, via the Speech SDK, regardless if it is speech or text, is only used to enhance your speech model.</span></span> <span data-ttu-id="e6391-119">It is not used beyond your model to enhance either Speech or LUIS in a general capacity.</span><span class="sxs-lookup"><span data-stu-id="e6391-119">It is not used beyond your model to enhance either Speech or LUIS in a general capacity.</span></span> <span data-ttu-id="e6391-120">When the LUIS app is deleted, the retained data is also deleted.</span><span class="sxs-lookup"><span data-stu-id="e6391-120">When the LUIS app is deleted, the retained data is also deleted.</span></span>

<!-- TBD: Machine translation conversion concepts -->

## <a name="next-steps"></a><span data-ttu-id="e6391-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="e6391-121">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e6391-122">Use speech to text</span><span class="sxs-lookup"><span data-stu-id="e6391-122">Use speech to text</span></span>](luis-tutorial-speech-to-intent.md)

