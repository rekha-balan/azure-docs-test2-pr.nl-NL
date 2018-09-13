---
title: Review endpoint utterances to use active learning in Language Understanding (LUIS) - Azure| Microsoft Docs
description: Use the active learning feature named 'Review endpoint utterances' to improve performance predictions faster.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 06/08/2018
ms.author: diberry
ms.openlocfilehash: 05b3404d318359c6966df44bfab9baff3ded980f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865575"
---
# <a name="enable-active-learning-by-reviewing-endpoint-utterances"></a><span data-ttu-id="4aa0c-103">Enable active learning by reviewing endpoint utterances</span><span class="sxs-lookup"><span data-stu-id="4aa0c-103">Enable active learning by reviewing endpoint utterances</span></span>
<span data-ttu-id="4aa0c-104">Active learning is one of three strategies to improve prediction accuracy and the easiest to implement.</span><span class="sxs-lookup"><span data-stu-id="4aa0c-104">Active learning is one of three strategies to improve prediction accuracy and the easiest to implement.</span></span> 

## <a name="what-is-active-learning"></a><span data-ttu-id="4aa0c-105">What is active learning</span><span class="sxs-lookup"><span data-stu-id="4aa0c-105">What is active learning</span></span>
<span data-ttu-id="4aa0c-106">Active learning is a two-step process.</span><span class="sxs-lookup"><span data-stu-id="4aa0c-106">Active learning is a two-step process.</span></span> <span data-ttu-id="4aa0c-107">First, LUIS selects utterances it receives at the app's endpoint that need validation.</span><span class="sxs-lookup"><span data-stu-id="4aa0c-107">First, LUIS selects utterances it receives at the app's endpoint that need validation.</span></span> <span data-ttu-id="4aa0c-108">The second step is performed by the app owner or collaborator to validate the selected utterances for [review](luis-how-to-review-endoint-utt.md), including the correct intent and any entities within the intent.</span><span class="sxs-lookup"><span data-stu-id="4aa0c-108">The second step is performed by the app owner or collaborator to validate the selected utterances for [review](luis-how-to-review-endoint-utt.md), including the correct intent and any entities within the intent.</span></span> <span data-ttu-id="4aa0c-109">After reviewing the utterances, train and publish the app again.</span><span class="sxs-lookup"><span data-stu-id="4aa0c-109">After reviewing the utterances, train and publish the app again.</span></span> 

## <a name="which-utterances-are-on-the-review-list"></a><span data-ttu-id="4aa0c-110">Which utterances are on the review list</span><span class="sxs-lookup"><span data-stu-id="4aa0c-110">Which utterances are on the review list</span></span>
<span data-ttu-id="4aa0c-111">LUIS adds utterances to the review list when the top firing intent has a low score or the top two intents' scores are too close.</span><span class="sxs-lookup"><span data-stu-id="4aa0c-111">LUIS adds utterances to the review list when the top firing intent has a low score or the top two intents' scores are too close.</span></span> 

## <a name="single-pool-for-utterances-per-app"></a><span data-ttu-id="4aa0c-112">Single pool for utterances per app</span><span class="sxs-lookup"><span data-stu-id="4aa0c-112">Single pool for utterances per app</span></span>
<span data-ttu-id="4aa0c-113">The **Review endpoint utterances** list doesn't change based on the version.</span><span class="sxs-lookup"><span data-stu-id="4aa0c-113">The **Review endpoint utterances** list doesn't change based on the version.</span></span> <span data-ttu-id="4aa0c-114">There is a single pool of utterances to review, regardless of which version the utterance you are actively editing or which version of the app was published at the endpoint.</span><span class="sxs-lookup"><span data-stu-id="4aa0c-114">There is a single pool of utterances to review, regardless of which version the utterance you are actively editing or which version of the app was published at the endpoint.</span></span> 

## <a name="where-are-the-utterances-from"></a><span data-ttu-id="4aa0c-115">Where are the utterances from</span><span class="sxs-lookup"><span data-stu-id="4aa0c-115">Where are the utterances from</span></span>
<span data-ttu-id="4aa0c-116">Endpoint utterances are taken from end-user queries on the application’s HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="4aa0c-116">Endpoint utterances are taken from end-user queries on the application’s HTTP endpoint.</span></span> <span data-ttu-id="4aa0c-117">If your app is not published or has not received hits yet, you do not have any utterances to review.</span><span class="sxs-lookup"><span data-stu-id="4aa0c-117">If your app is not published or has not received hits yet, you do not have any utterances to review.</span></span> <span data-ttu-id="4aa0c-118">If no endpoint hits are received for a specific intent or entity, you do not have utterances to review that contain them.</span><span class="sxs-lookup"><span data-stu-id="4aa0c-118">If no endpoint hits are received for a specific intent or entity, you do not have utterances to review that contain them.</span></span> 

## <a name="schedule-review-periodically"></a><span data-ttu-id="4aa0c-119">Schedule review periodically</span><span class="sxs-lookup"><span data-stu-id="4aa0c-119">Schedule review periodically</span></span>
<span data-ttu-id="4aa0c-120">Reviewing suggested utterances doesn't need to be done every day but should be part of your regular maintenance of LUIS.</span><span class="sxs-lookup"><span data-stu-id="4aa0c-120">Reviewing suggested utterances doesn't need to be done every day but should be part of your regular maintenance of LUIS.</span></span> 

## <a name="delete-review-items-programmatically"></a><span data-ttu-id="4aa0c-121">Delete review items programmatically</span><span class="sxs-lookup"><span data-stu-id="4aa0c-121">Delete review items programmatically</span></span>
<span data-ttu-id="4aa0c-122">If your app is large, you may choose to review some utterances and delete the rest from the list programmatically.</span><span class="sxs-lookup"><span data-stu-id="4aa0c-122">If your app is large, you may choose to review some utterances and delete the rest from the list programmatically.</span></span> <span data-ttu-id="4aa0c-123">This is done by first [getting](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c0a) the list and then [deleting](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/58b6f32139e2bb139ce823c9) the utterances by ID.</span><span class="sxs-lookup"><span data-stu-id="4aa0c-123">This is done by first [getting](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c0a) the list and then [deleting](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/58b6f32139e2bb139ce823c9) the utterances by ID.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4aa0c-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="4aa0c-124">Next steps</span></span>

* <span data-ttu-id="4aa0c-125">Learn how to [review](luis-how-to-review-endoint-utt.md) endpoint utterances</span><span class="sxs-lookup"><span data-stu-id="4aa0c-125">Learn how to [review](luis-how-to-review-endoint-utt.md) endpoint utterances</span></span>
