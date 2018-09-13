---
title: Learn about QnA Maker - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: QnA Maker enables you to power a question and answer service from your semi-structured content like FAQ documents or URLs and product manuals.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: overview
ms.date: 06/15/2018
ms.author: nolachar
ms.openlocfilehash: f34cec047c18a6db10b5adda82800c51d44c1155
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869462"
---
# <a name="what-is-qna-maker"></a><span data-ttu-id="bb32f-103">What is QnA Maker?</span><span class="sxs-lookup"><span data-stu-id="bb32f-103">What is QnA Maker?</span></span>

<span data-ttu-id="bb32f-104">[QnA Maker](https://qnamaker.ai) enables you to power a question and answer service from your semi-structured content like FAQ (Frequently Asked Questions) documents or URLs and product manuals.</span><span class="sxs-lookup"><span data-stu-id="bb32f-104">[QnA Maker](https://qnamaker.ai) enables you to power a question and answer service from your semi-structured content like FAQ (Frequently Asked Questions) documents or URLs and product manuals.</span></span> <span data-ttu-id="bb32f-105">You can build a model of questions and answers that is flexible to user queries, providing responses that you'll train a bot to use in a natural, conversational way.</span><span class="sxs-lookup"><span data-stu-id="bb32f-105">You can build a model of questions and answers that is flexible to user queries, providing responses that you'll train a bot to use in a natural, conversational way.</span></span>

<span data-ttu-id="bb32f-106">An easy-to-use graphical user interface enables you to create, manage, train and get your service up and running without any developer experience.</span><span class="sxs-lookup"><span data-stu-id="bb32f-106">An easy-to-use graphical user interface enables you to create, manage, train and get your service up and running without any developer experience.</span></span>

![Overview](../media/qnamaker-overview-learnabout/overview.png)

## <a name="highlights"></a><span data-ttu-id="bb32f-108">Highlights</span><span class="sxs-lookup"><span data-stu-id="bb32f-108">Highlights</span></span>

- <span data-ttu-id="bb32f-109">A complete **no-code** experience to [create a FAQ bot](https://aka.ms/qnamaker-docs-create-faqbot).</span><span class="sxs-lookup"><span data-stu-id="bb32f-109">A complete **no-code** experience to [create a FAQ bot](https://aka.ms/qnamaker-docs-create-faqbot).</span></span>
- <span data-ttu-id="bb32f-110">**No more network throttling**.</span><span class="sxs-lookup"><span data-stu-id="bb32f-110">**No more network throttling**.</span></span> <span data-ttu-id="bb32f-111">Pay for hosting the service and not for the number of transactions.</span><span class="sxs-lookup"><span data-stu-id="bb32f-111">Pay for hosting the service and not for the number of transactions.</span></span> <span data-ttu-id="bb32f-112">See the [pricing page](https://aka.ms/qnamaker-docs-pricing) for more details.</span><span class="sxs-lookup"><span data-stu-id="bb32f-112">See the [pricing page](https://aka.ms/qnamaker-docs-pricing) for more details.</span></span>
- <span data-ttu-id="bb32f-113">**Scale as per your needs**.</span><span class="sxs-lookup"><span data-stu-id="bb32f-113">**Scale as per your needs**.</span></span> <span data-ttu-id="bb32f-114">Choose the appropriate SKUs of the individual components that suit your scenario.</span><span class="sxs-lookup"><span data-stu-id="bb32f-114">Choose the appropriate SKUs of the individual components that suit your scenario.</span></span> <span data-ttu-id="bb32f-115">See how to [choose capacity](https://aka.ms/qnamaker-docs-capacity) for your QnA Maker service.</span><span class="sxs-lookup"><span data-stu-id="bb32f-115">See how to [choose capacity](https://aka.ms/qnamaker-docs-capacity) for your QnA Maker service.</span></span>
- <span data-ttu-id="bb32f-116">**Full data compliance**.</span><span class="sxs-lookup"><span data-stu-id="bb32f-116">**Full data compliance**.</span></span> <span data-ttu-id="bb32f-117">The data and runtime components are deployed in the user's Azure subscription and within their compliance boundary.</span><span class="sxs-lookup"><span data-stu-id="bb32f-117">The data and runtime components are deployed in the user's Azure subscription and within their compliance boundary.</span></span> <span data-ttu-id="bb32f-118">Read below for more details.</span><span class="sxs-lookup"><span data-stu-id="bb32f-118">Read below for more details.</span></span>

## <a name="key-qna-maker-processes"></a><span data-ttu-id="bb32f-119">Key QnA Maker processes</span><span class="sxs-lookup"><span data-stu-id="bb32f-119">Key QnA Maker processes</span></span>

<span data-ttu-id="bb32f-120">A QnA Maker provides two key services for your data:</span><span class="sxs-lookup"><span data-stu-id="bb32f-120">A QnA Maker provides two key services for your data:</span></span>

* <span data-ttu-id="bb32f-121">**Extraction**: Structured question-answer data is extracted from semi-structured data sources like FAQs and product manuals.</span><span class="sxs-lookup"><span data-stu-id="bb32f-121">**Extraction**: Structured question-answer data is extracted from semi-structured data sources like FAQs and product manuals.</span></span> <span data-ttu-id="bb32f-122">This extraction is done when creating the knowledge base.</span><span class="sxs-lookup"><span data-stu-id="bb32f-122">This extraction is done when creating the knowledge base.</span></span> <span data-ttu-id="bb32f-123">Create your knowledge base [here](https://aka.ms/qnamaker-docs-createkb).</span><span class="sxs-lookup"><span data-stu-id="bb32f-123">Create your knowledge base [here](https://aka.ms/qnamaker-docs-createkb).</span></span>

* <span data-ttu-id="bb32f-124">**Matching**: Once your knowledge base has been [trained and tested](https://aka.ms/qnamaker-docs-trainkb), you [publish](https://aka.ms/qnamaker-docs-publishkb) it.</span><span class="sxs-lookup"><span data-stu-id="bb32f-124">**Matching**: Once your knowledge base has been [trained and tested](https://aka.ms/qnamaker-docs-trainkb), you [publish](https://aka.ms/qnamaker-docs-publishkb) it.</span></span> <span data-ttu-id="bb32f-125">This enables an endpoint to your QnA Maker knowledge base, which you can then use in your bot or app.</span><span class="sxs-lookup"><span data-stu-id="bb32f-125">This enables an endpoint to your QnA Maker knowledge base, which you can then use in your bot or app.</span></span> <span data-ttu-id="bb32f-126">This endpoint accepts a user question and responds with the best question/answer match in the knowledge base, along with a confidence score for the match.</span><span class="sxs-lookup"><span data-stu-id="bb32f-126">This endpoint accepts a user question and responds with the best question/answer match in the knowledge base, along with a confidence score for the match.</span></span>

## <a name="qna-maker-architecture"></a><span data-ttu-id="bb32f-127">QnA Maker architecture</span><span class="sxs-lookup"><span data-stu-id="bb32f-127">QnA Maker architecture</span></span>

<span data-ttu-id="bb32f-128">The QnA Maker stack consists of the following parts:</span><span class="sxs-lookup"><span data-stu-id="bb32f-128">The QnA Maker stack consists of the following parts:</span></span>

1. <span data-ttu-id="bb32f-129">**QnA Maker management services (control plane)**: The management experience for a QnA Maker knowledge base, which includes the initial creation, updating, training, and publishing.</span><span class="sxs-lookup"><span data-stu-id="bb32f-129">**QnA Maker management services (control plane)**: The management experience for a QnA Maker knowledge base, which includes the initial creation, updating, training, and publishing.</span></span> <span data-ttu-id="bb32f-130">These activities can be done through the [portal](https://qnamaker.ai) or the [management APIs](https://aka.ms/qnamaker-v4-apis).</span><span class="sxs-lookup"><span data-stu-id="bb32f-130">These activities can be done through the [portal](https://qnamaker.ai) or the [management APIs](https://aka.ms/qnamaker-v4-apis).</span></span> <span data-ttu-id="bb32f-131">The management services talk to the runtime component below.</span><span class="sxs-lookup"><span data-stu-id="bb32f-131">The management services talk to the runtime component below.</span></span>

2. <span data-ttu-id="bb32f-132">**QnA Maker runtime (data plane)**: The data and runtime are deployed in the user's Azure subscription in a region of their choosing.</span><span class="sxs-lookup"><span data-stu-id="bb32f-132">**QnA Maker runtime (data plane)**: The data and runtime are deployed in the user's Azure subscription in a region of their choosing.</span></span> <span data-ttu-id="bb32f-133">Customer question/answer content is stored in [Azure Search](https://azure.microsoft.com/services/search/), and the runtime is deployed as an [App service](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="bb32f-133">Customer question/answer content is stored in [Azure Search](https://azure.microsoft.com/services/search/), and the runtime is deployed as an [App service](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="bb32f-134">Optionally, you can also choose to deploy an [Application insights](https://azure.microsoft.com/services/application-insights/) resource for analytics.</span><span class="sxs-lookup"><span data-stu-id="bb32f-134">Optionally, you can also choose to deploy an [Application insights](https://azure.microsoft.com/services/application-insights/) resource for analytics.</span></span>

![Architecture](../media/qnamaker-overview-learnabout/architecture.png)

## <a name="next-steps"></a><span data-ttu-id="bb32f-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="bb32f-136">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bb32f-137">Create a QnA Maker service</span><span class="sxs-lookup"><span data-stu-id="bb32f-137">Create a QnA Maker service</span></span>](../how-to/set-up-qnamaker-service-azure.md)
