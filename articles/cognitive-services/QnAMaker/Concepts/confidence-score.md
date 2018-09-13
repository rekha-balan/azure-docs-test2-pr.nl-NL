---
title: Confidence Score - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Explaining confidence score
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 04/21/2018
ms.author: saneppal
ms.openlocfilehash: c97bdb7e57275ebd1893bc28248c4ecc6b35c153
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871688"
---
# <a name="confidence-score"></a><span data-ttu-id="0d7d7-103">Confidence Score</span><span class="sxs-lookup"><span data-stu-id="0d7d7-103">Confidence Score</span></span>

<span data-ttu-id="0d7d7-104">A confidence score indicates the degree of match between the user question and the response returned.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-104">A confidence score indicates the degree of match between the user question and the response returned.</span></span>

<span data-ttu-id="0d7d7-105">When a user query is matched against knowledge base content, there can be more than one response returned.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-105">When a user query is matched against knowledge base content, there can be more than one response returned.</span></span> <span data-ttu-id="0d7d7-106">The responses are returned in a ranked order of decreasing confidence score.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-106">The responses are returned in a ranked order of decreasing confidence score.</span></span>

<span data-ttu-id="0d7d7-107">A confidence score is between 0 and 100.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-107">A confidence score is between 0 and 100.</span></span>

|<span data-ttu-id="0d7d7-108">Score value</span><span class="sxs-lookup"><span data-stu-id="0d7d7-108">Score value</span></span>|<span data-ttu-id="0d7d7-109">Confidence</span><span class="sxs-lookup"><span data-stu-id="0d7d7-109">Confidence</span></span>|
|--|--|
|<span data-ttu-id="0d7d7-110">100</span><span class="sxs-lookup"><span data-stu-id="0d7d7-110">100</span></span>|<span data-ttu-id="0d7d7-111">An exact match of user query and a KB question</span><span class="sxs-lookup"><span data-stu-id="0d7d7-111">An exact match of user query and a KB question</span></span>|
|<span data-ttu-id="0d7d7-112">90</span><span class="sxs-lookup"><span data-stu-id="0d7d7-112">90</span></span>|<span data-ttu-id="0d7d7-113">High confidence - most of the words match</span><span class="sxs-lookup"><span data-stu-id="0d7d7-113">High confidence - most of the words match</span></span>|
|<span data-ttu-id="0d7d7-114">40-60</span><span class="sxs-lookup"><span data-stu-id="0d7d7-114">40-60</span></span>|<span data-ttu-id="0d7d7-115">Fair confidence - important words match</span><span class="sxs-lookup"><span data-stu-id="0d7d7-115">Fair confidence - important words match</span></span>|
|<span data-ttu-id="0d7d7-116">10</span><span class="sxs-lookup"><span data-stu-id="0d7d7-116">10</span></span>|<span data-ttu-id="0d7d7-117">Low confidence - important words don't match</span><span class="sxs-lookup"><span data-stu-id="0d7d7-117">Low confidence - important words don't match</span></span>|
|<span data-ttu-id="0d7d7-118">0</span><span class="sxs-lookup"><span data-stu-id="0d7d7-118">0</span></span>|<span data-ttu-id="0d7d7-119">No word match</span><span class="sxs-lookup"><span data-stu-id="0d7d7-119">No word match</span></span>|


## <a name="similar-confidence-scores"></a><span data-ttu-id="0d7d7-120">Similar confidence scores</span><span class="sxs-lookup"><span data-stu-id="0d7d7-120">Similar confidence scores</span></span>
<span data-ttu-id="0d7d7-121">When multiple responses have a similar confidence score, it is likely that the query was too generic and therefore matched with equal likelihood with multiple answers.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-121">When multiple responses have a similar confidence score, it is likely that the query was too generic and therefore matched with equal likelihood with multiple answers.</span></span> <span data-ttu-id="0d7d7-122">Try to structure your QnAs better so that every QnA entity has a distinct intent.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-122">Try to structure your QnAs better so that every QnA entity has a distinct intent.</span></span>


## <a name="improving-confidence-scores"></a><span data-ttu-id="0d7d7-123">Improving confidence scores</span><span class="sxs-lookup"><span data-stu-id="0d7d7-123">Improving confidence scores</span></span>
<span data-ttu-id="0d7d7-124">To improve the confidence score of a particular response to a user query, you can add the user query to the knowledge base as an alternate question on that response.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-124">To improve the confidence score of a particular response to a user query, you can add the user query to the knowledge base as an alternate question on that response.</span></span>
   
## <a name="confidence-score-differences"></a><span data-ttu-id="0d7d7-125">Confidence score differences</span><span class="sxs-lookup"><span data-stu-id="0d7d7-125">Confidence score differences</span></span>
<span data-ttu-id="0d7d7-126">The confidence score of an answer may change negligibly between the test and published version of the knowledge base even if the content is the same.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-126">The confidence score of an answer may change negligibly between the test and published version of the knowledge base even if the content is the same.</span></span> <span data-ttu-id="0d7d7-127">This is because the content of the test and the published knowledge base are located in different Azure Search indexes.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-127">This is because the content of the test and the published knowledge base are located in different Azure Search indexes.</span></span>

<span data-ttu-id="0d7d7-128">See here how the [publish](../How-To/publish-knowledge-base.md) operation works.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-128">See here how the [publish](../How-To/publish-knowledge-base.md) operation works.</span></span>


## <a name="no-match-found"></a><span data-ttu-id="0d7d7-129">No match found</span><span class="sxs-lookup"><span data-stu-id="0d7d7-129">No match found</span></span>
<span data-ttu-id="0d7d7-130">When no good match is found by the ranker, the confidence score of 0.0 or "None" is returned and the default response is "No good match found in the KB".</span><span class="sxs-lookup"><span data-stu-id="0d7d7-130">When no good match is found by the ranker, the confidence score of 0.0 or "None" is returned and the default response is "No good match found in the KB".</span></span> <span data-ttu-id="0d7d7-131">You can override this default response in the bot or application code calling the endpoint.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-131">You can override this default response in the bot or application code calling the endpoint.</span></span> <span data-ttu-id="0d7d7-132">Alternately, you can also set the override response in Azure and this changes the default for all knowledge bases deployed in a particular QnA Maker service.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-132">Alternately, you can also set the override response in Azure and this changes the default for all knowledge bases deployed in a particular QnA Maker service.</span></span>

1. <span data-ttu-id="0d7d7-133">Go to the [Azure portal](http://portal.azure.com) and navigate to the resource group that represents the QnA Maker service you created.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-133">Go to the [Azure portal](http://portal.azure.com) and navigate to the resource group that represents the QnA Maker service you created.</span></span>

2. <span data-ttu-id="0d7d7-134">Click to open the **App Service**.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-134">Click to open the **App Service**.</span></span>

    ![Access App service](../media/qnamaker-concepts-confidencescore/set-default-response.png)

3. <span data-ttu-id="0d7d7-136">Click on **Application Settings** and edit the **DefaultAnswer** field to the desired default response.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-136">Click on **Application Settings** and edit the **DefaultAnswer** field to the desired default response.</span></span> <span data-ttu-id="0d7d7-137">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="0d7d7-137">Click **Save**.</span></span>

    ![Change default response](../media/qnamaker-concepts-confidencescore/change-response.png)

4. <span data-ttu-id="0d7d7-139">Restart your App service</span><span class="sxs-lookup"><span data-stu-id="0d7d7-139">Restart your App service</span></span>

    ![QnA Maker appservice restart](../media/qnamaker-faq/qnamaker-appservice-restart.png)


## <a name="next-steps"></a><span data-ttu-id="0d7d7-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="0d7d7-141">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0d7d7-142">Data sources supported</span><span class="sxs-lookup"><span data-stu-id="0d7d7-142">Data sources supported</span></span>](./data-sources-supported.md)

## <a name="see-also"></a><span data-ttu-id="0d7d7-143">See also</span><span class="sxs-lookup"><span data-stu-id="0d7d7-143">See also</span></span> 

[<span data-ttu-id="0d7d7-144">QnA Maker overview</span><span class="sxs-lookup"><span data-stu-id="0d7d7-144">QnA Maker overview</span></span>](../Overview/overview.md)
