---
title: Development lifecycle of a knowledge base - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Development lifecycle of a knowledge base
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 04/21/2018
ms.author: saneppal
ms.openlocfilehash: 9ecdd2c7823eed145621b214690eff7681065507
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968743"
---
# <a name="knowledge-base-lifecycle"></a><span data-ttu-id="97382-103">Knowledge base lifecycle</span><span class="sxs-lookup"><span data-stu-id="97382-103">Knowledge base lifecycle</span></span>
<span data-ttu-id="97382-104">QnA Maker learns best in an iterative cycle of model changes, utterance examples, publishing, and gathering data from endpoint queries.</span><span class="sxs-lookup"><span data-stu-id="97382-104">QnA Maker learns best in an iterative cycle of model changes, utterance examples, publishing, and gathering data from endpoint queries.</span></span> 

![Authoring cycle](../media/qnamaker-concepts-lifecycle/kb-lifecycle.png)

## <a name="creating-a-qna-maker-knowledge-base"></a><span data-ttu-id="97382-106">Creating a QnA Maker knowledge base</span><span class="sxs-lookup"><span data-stu-id="97382-106">Creating a QnA Maker knowledge base</span></span>
<span data-ttu-id="97382-107">QnA Maker knowledge base (KB) endpoint provides a best-match answer to a user query based on the content of the KB.</span><span class="sxs-lookup"><span data-stu-id="97382-107">QnA Maker knowledge base (KB) endpoint provides a best-match answer to a user query based on the content of the KB.</span></span> <span data-ttu-id="97382-108">Creating a knowledge base is a one-time action to setting up a content repository of questions, answers and associated metadata.</span><span class="sxs-lookup"><span data-stu-id="97382-108">Creating a knowledge base is a one-time action to setting up a content repository of questions, answers and associated metadata.</span></span> <span data-ttu-id="97382-109">A knowledge base can be created by crawling pre-existing content such as FAQ pages, product manuals or structured Q-A pairs.</span><span class="sxs-lookup"><span data-stu-id="97382-109">A knowledge base can be created by crawling pre-existing content such as FAQ pages, product manuals or structured Q-A pairs.</span></span> <span data-ttu-id="97382-110">Learn how to [create a knowledge base](../How-To/create-knowledge-base.md).</span><span class="sxs-lookup"><span data-stu-id="97382-110">Learn how to [create a knowledge base](../How-To/create-knowledge-base.md).</span></span>

## <a name="testing-and-updating-the-knowledge-base"></a><span data-ttu-id="97382-111">Testing and updating the knowledge base</span><span class="sxs-lookup"><span data-stu-id="97382-111">Testing and updating the knowledge base</span></span>
<span data-ttu-id="97382-112">The knowledge base is ready for testing once it is populated with content, either editorially or through automatic extraction.</span><span class="sxs-lookup"><span data-stu-id="97382-112">The knowledge base is ready for testing once it is populated with content, either editorially or through automatic extraction.</span></span> <span data-ttu-id="97382-113">Testing can be done through the **Test** panel by entering common user queries and verifying that the responses returned are as expected and with sufficient confidence score.</span><span class="sxs-lookup"><span data-stu-id="97382-113">Testing can be done through the **Test** panel by entering common user queries and verifying that the responses returned are as expected and with sufficient confidence score.</span></span> <span data-ttu-id="97382-114">You can add alternate questions to rectify low confidence scores.</span><span class="sxs-lookup"><span data-stu-id="97382-114">You can add alternate questions to rectify low confidence scores.</span></span> <span data-ttu-id="97382-115">You can also add new answers when a query returns "no match found in the KB" default response.</span><span class="sxs-lookup"><span data-stu-id="97382-115">You can also add new answers when a query returns "no match found in the KB" default response.</span></span> <span data-ttu-id="97382-116">This tight loop of test-update continues until you are satisfied with the results.</span><span class="sxs-lookup"><span data-stu-id="97382-116">This tight loop of test-update continues until you are satisfied with the results.</span></span> <span data-ttu-id="97382-117">Learn how to [test your knowledge base](../How-To/test-knowledge-base.md).</span><span class="sxs-lookup"><span data-stu-id="97382-117">Learn how to [test your knowledge base](../How-To/test-knowledge-base.md).</span></span>

<span data-ttu-id="97382-118">For large KBs, the testing can be automated through generateAnswer APIs.</span><span class="sxs-lookup"><span data-stu-id="97382-118">For large KBs, the testing can be automated through generateAnswer APIs.</span></span> 

## <a name="publish-the-knowledge-base"></a><span data-ttu-id="97382-119">Publish the knowledge base</span><span class="sxs-lookup"><span data-stu-id="97382-119">Publish the knowledge base</span></span>
<span data-ttu-id="97382-120">Once you are done testing the knowledge base, you can publish it.</span><span class="sxs-lookup"><span data-stu-id="97382-120">Once you are done testing the knowledge base, you can publish it.</span></span> <span data-ttu-id="97382-121">Publish pushes the latest version of the tested knowledge base  to a dedicated Azure Search index representing the **published** knowledge base.</span><span class="sxs-lookup"><span data-stu-id="97382-121">Publish pushes the latest version of the tested knowledge base  to a dedicated Azure Search index representing the **published** knowledge base.</span></span> <span data-ttu-id="97382-122">It also creates an endpoint that can be called in your application or chat bot.</span><span class="sxs-lookup"><span data-stu-id="97382-122">It also creates an endpoint that can be called in your application or chat bot.</span></span>

<span data-ttu-id="97382-123">This way, any changes being made to the test version of the knowledge base do not affect the published version that might be live in a production application.</span><span class="sxs-lookup"><span data-stu-id="97382-123">This way, any changes being made to the test version of the knowledge base do not affect the published version that might be live in a production application.</span></span>

<span data-ttu-id="97382-124">Each of these knowledge bases can be targeted for testing separately.</span><span class="sxs-lookup"><span data-stu-id="97382-124">Each of these knowledge bases can be targeted for testing separately.</span></span> <span data-ttu-id="97382-125">Using the APIs, you can target the test version of the knowledge base with `isTest=true` flag in the generateAnswer call.</span><span class="sxs-lookup"><span data-stu-id="97382-125">Using the APIs, you can target the test version of the knowledge base with `isTest=true` flag in the generateAnswer call.</span></span>

<span data-ttu-id="97382-126">Learn how to [publish your knowledge base](../How-To/publish-knowledge-base.md).</span><span class="sxs-lookup"><span data-stu-id="97382-126">Learn how to [publish your knowledge base](../How-To/publish-knowledge-base.md).</span></span>

## <a name="monitor-usage"></a><span data-ttu-id="97382-127">Monitor usage</span><span class="sxs-lookup"><span data-stu-id="97382-127">Monitor usage</span></span>
<span data-ttu-id="97382-128">To be able to log the chat logs of your service, you would need to enable Application Insights when you [create your QnA Maker service](../How-To/set-up-qnamaker-service-azure.md).</span><span class="sxs-lookup"><span data-stu-id="97382-128">To be able to log the chat logs of your service, you would need to enable Application Insights when you [create your QnA Maker service](../How-To/set-up-qnamaker-service-azure.md).</span></span>

<span data-ttu-id="97382-129">You can get various analytics of your service usage.</span><span class="sxs-lookup"><span data-stu-id="97382-129">You can get various analytics of your service usage.</span></span> <span data-ttu-id="97382-130">Learn more about how to use application insights to get [analytics for your QnA Maker service](../How-To/get-analytics-knowledge-base.md).</span><span class="sxs-lookup"><span data-stu-id="97382-130">Learn more about how to use application insights to get [analytics for your QnA Maker service](../How-To/get-analytics-knowledge-base.md).</span></span>

<span data-ttu-id="97382-131">Based on what you learn from your analytics, make appropriate [updates to your knowledge base](../How-To/edit-knowledge-base.md).</span><span class="sxs-lookup"><span data-stu-id="97382-131">Based on what you learn from your analytics, make appropriate [updates to your knowledge base](../How-To/edit-knowledge-base.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="97382-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="97382-132">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="97382-133">Confidence score</span><span class="sxs-lookup"><span data-stu-id="97382-133">Confidence score</span></span>](./confidence-score.md)

## <a name="see-also"></a><span data-ttu-id="97382-134">See also</span><span class="sxs-lookup"><span data-stu-id="97382-134">See also</span></span> 

<span data-ttu-id="97382-135">[Knowledge base](./knowledge-base.md)
[QnA Maker overview](../Overview/overview.md)</span><span class="sxs-lookup"><span data-stu-id="97382-135">[Knowledge base](./knowledge-base.md)
[QnA Maker overview](../Overview/overview.md)</span></span>
