---
title: Train your LUIS app
titleSuffix: Azure Cognitive Services
description: Training is the process of teaching your Language Understanding (LUIS) app to improve its natural language understanding. Train your LUIS app after updates to the model such as adding, editing, labeling, or deleting entities, intents, or utterances.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 09/06/2018
ms.author: diberry
ms.openlocfilehash: 42cff3dd8237598da5aa71ed1a4d6462c5b4c25d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856908"
---
# <a name="train-your-luis-app"></a><span data-ttu-id="3de8b-104">Train your LUIS app</span><span class="sxs-lookup"><span data-stu-id="3de8b-104">Train your LUIS app</span></span>

<span data-ttu-id="3de8b-105">Training is the process of teaching your Language Understanding (LUIS) app to improve its natural language understanding.</span><span class="sxs-lookup"><span data-stu-id="3de8b-105">Training is the process of teaching your Language Understanding (LUIS) app to improve its natural language understanding.</span></span> <span data-ttu-id="3de8b-106">Train your LUIS app after updates to the model such as adding, editing, labeling, or deleting entities, intents, or utterances.</span><span class="sxs-lookup"><span data-stu-id="3de8b-106">Train your LUIS app after updates to the model such as adding, editing, labeling, or deleting entities, intents, or utterances.</span></span> 

<!--
When you train a LUIS app by example, LUIS generalizes from the examples you have labeled, and it learns to recognize the relevant intents and entities. This teaches LUIS to improve classification accuracy in the future. -->

<span data-ttu-id="3de8b-107">Training and [testing](luis-concept-test.md) an app is an iterative process.</span><span class="sxs-lookup"><span data-stu-id="3de8b-107">Training and [testing](luis-concept-test.md) an app is an iterative process.</span></span> <span data-ttu-id="3de8b-108">After you train your LUIS app, you test it with sample utterances to see if the intents and entities are recognized correctly.</span><span class="sxs-lookup"><span data-stu-id="3de8b-108">After you train your LUIS app, you test it with sample utterances to see if the intents and entities are recognized correctly.</span></span> <span data-ttu-id="3de8b-109">If they're not, make updates to the LUIS app, train, and test again.</span><span class="sxs-lookup"><span data-stu-id="3de8b-109">If they're not, make updates to the LUIS app, train, and test again.</span></span> 

## <a name="train-your-app"></a><span data-ttu-id="3de8b-110">Train your app</span><span class="sxs-lookup"><span data-stu-id="3de8b-110">Train your app</span></span>
<span data-ttu-id="3de8b-111">To start the iterative process, you first need to train your LUIS app at least once.</span><span class="sxs-lookup"><span data-stu-id="3de8b-111">To start the iterative process, you first need to train your LUIS app at least once.</span></span> <span data-ttu-id="3de8b-112">Make sure every intent has at least one utterance before training.</span><span class="sxs-lookup"><span data-stu-id="3de8b-112">Make sure every intent has at least one utterance before training.</span></span>

1. <span data-ttu-id="3de8b-113">Access your app by selecting its name on the **My Apps** page.</span><span class="sxs-lookup"><span data-stu-id="3de8b-113">Access your app by selecting its name on the **My Apps** page.</span></span> 

2. <span data-ttu-id="3de8b-114">In your app, select **Train** in the top panel.</span><span class="sxs-lookup"><span data-stu-id="3de8b-114">In your app, select **Train** in the top panel.</span></span> 

3. <span data-ttu-id="3de8b-115">When training is complete, a green notification bar appears at the top of the browser.</span><span class="sxs-lookup"><span data-stu-id="3de8b-115">When training is complete, a green notification bar appears at the top of the browser.</span></span>

<!-- The following note refers to what might cause the error message "Training failed: FewLabels for model: <ModelName>" -->

>[!NOTE]
><span data-ttu-id="3de8b-116">If you have one or more intents in your app that do not contain example utterances, you cannot train your app.</span><span class="sxs-lookup"><span data-stu-id="3de8b-116">If you have one or more intents in your app that do not contain example utterances, you cannot train your app.</span></span> <span data-ttu-id="3de8b-117">Add utterances for all your intents.</span><span class="sxs-lookup"><span data-stu-id="3de8b-117">Add utterances for all your intents.</span></span> <span data-ttu-id="3de8b-118">For more information, see [Add example utterances](luis-how-to-add-example-utterances.md).</span><span class="sxs-lookup"><span data-stu-id="3de8b-118">For more information, see [Add example utterances](luis-how-to-add-example-utterances.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3de8b-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="3de8b-119">Next steps</span></span>

* [<span data-ttu-id="3de8b-120">Label suggested utterances with LUIS</span><span class="sxs-lookup"><span data-stu-id="3de8b-120">Label suggested utterances with LUIS</span></span>](luis-how-to-review-endoint-utt.md) 
* [<span data-ttu-id="3de8b-121">Use features to improve your LUIS app's performance</span><span class="sxs-lookup"><span data-stu-id="3de8b-121">Use features to improve your LUIS app's performance</span></span>](luis-how-to-add-features.md) 