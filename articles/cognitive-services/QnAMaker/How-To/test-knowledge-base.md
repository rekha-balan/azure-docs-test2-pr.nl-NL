---
title: How to test a knowledge base - QnA Maker - Azure Cognitive Services | Microsoft Docs
description: Test your knowledge base before publishing it.
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 05/07/2018
ms.author: saneppal
ms.openlocfilehash: cffb63666edab25e1b3b0739d0e0f2f828600f3a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868842"
---
# <a name="test-your-knowledge-base"></a><span data-ttu-id="ff8e9-103">Test your knowledge base</span><span class="sxs-lookup"><span data-stu-id="ff8e9-103">Test your knowledge base</span></span>

<span data-ttu-id="ff8e9-104">Testing your QnA Maker knowledge base is an important part of an iterative process to improve the accuracy of the responses being returned.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-104">Testing your QnA Maker knowledge base is an important part of an iterative process to improve the accuracy of the responses being returned.</span></span> <span data-ttu-id="ff8e9-105">You can test the knowledge base through an enhanced chat interface that also allows you make edits.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-105">You can test the knowledge base through an enhanced chat interface that also allows you make edits.</span></span>

## <a name="test-answer-matching"></a><span data-ttu-id="ff8e9-106">Test answer matching</span><span class="sxs-lookup"><span data-stu-id="ff8e9-106">Test answer matching</span></span>

1.  <span data-ttu-id="ff8e9-107">Access your knowledge base by selecting its name on the **My knowledge bases** page.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-107">Access your knowledge base by selecting its name on the **My knowledge bases** page.</span></span>
2.  <span data-ttu-id="ff8e9-108">To access the Test slide-out panel, select **Test** in your application's top panel.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-108">To access the Test slide-out panel, select **Test** in your application's top panel.</span></span>

    ![Access Test](../media/qnamaker-how-to-test-kb/access-test.png)

3.  <span data-ttu-id="ff8e9-110">Enter a query in the text box and select Enter.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-110">Enter a query in the text box and select Enter.</span></span>

4.  <span data-ttu-id="ff8e9-111">The best-matched answer from the knowledge base is returned as the response.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-111">The best-matched answer from the knowledge base is returned as the response.</span></span>

## <a name="clear-test-panel"></a><span data-ttu-id="ff8e9-112">Clear test panel</span><span class="sxs-lookup"><span data-stu-id="ff8e9-112">Clear test panel</span></span>

<span data-ttu-id="ff8e9-113">To clear all the entered test queries and their results from the test console, select **Start over** at the upper-left corner of the Test panel.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-113">To clear all the entered test queries and their results from the test console, select **Start over** at the upper-left corner of the Test panel.</span></span>

## <a name="close-test-panel"></a><span data-ttu-id="ff8e9-114">Close test panel</span><span class="sxs-lookup"><span data-stu-id="ff8e9-114">Close test panel</span></span>

<span data-ttu-id="ff8e9-115">To close the Test panel, select the **Test** button again.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-115">To close the Test panel, select the **Test** button again.</span></span> <span data-ttu-id="ff8e9-116">While the Test panel is open, you cannot edit the Knowledge Base contents.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-116">While the Test panel is open, you cannot edit the Knowledge Base contents.</span></span>

## <a name="inspect-score"></a><span data-ttu-id="ff8e9-117">Inspect score</span><span class="sxs-lookup"><span data-stu-id="ff8e9-117">Inspect score</span></span>

<span data-ttu-id="ff8e9-118">You inspect details of the test result in the Inspect panel.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-118">You inspect details of the test result in the Inspect panel.</span></span>

1.  <span data-ttu-id="ff8e9-119">With the Test slide-out panel open, select **Inspect** for more details on that response.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-119">With the Test slide-out panel open, select **Inspect** for more details on that response.</span></span>

    ![Inspect responses](../media/qnamaker-how-to-test-kb/inspect.png)

2.  <span data-ttu-id="ff8e9-121">The Inspection panel appears.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-121">The Inspection panel appears.</span></span> <span data-ttu-id="ff8e9-122">The panel includes the top scoring intent as well as any identified entities.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-122">The panel includes the top scoring intent as well as any identified entities.</span></span> <span data-ttu-id="ff8e9-123">The panel shows the result of the selected utterance.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-123">The panel shows the result of the selected utterance.</span></span>

## <a name="correct-the-top-scoring-answer"></a><span data-ttu-id="ff8e9-124">Correct the top scoring answer</span><span class="sxs-lookup"><span data-stu-id="ff8e9-124">Correct the top scoring answer</span></span>

<span data-ttu-id="ff8e9-125">If the top scoring answer is incorrect, select the correct answer from the list and select **Save and Train**.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-125">If the top scoring answer is incorrect, select the correct answer from the list and select **Save and Train**.</span></span>

![Access Test](../media/qnamaker-how-to-test-kb/choose-answer.png)

## <a name="add-alternate-questions"></a><span data-ttu-id="ff8e9-127">Add alternate questions</span><span class="sxs-lookup"><span data-stu-id="ff8e9-127">Add alternate questions</span></span>

<span data-ttu-id="ff8e9-128">You can add alternate forms of a question to a given answer.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-128">You can add alternate forms of a question to a given answer.</span></span> <span data-ttu-id="ff8e9-129">Type the alternate answers in the text box and click enter to add them.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-129">Type the alternate answers in the text box and click enter to add them.</span></span> <span data-ttu-id="ff8e9-130">Select **Save and Train** to store the updates.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-130">Select **Save and Train** to store the updates.</span></span>

![Access Test](../media/qnamaker-how-to-test-kb/add-alternate-question.png)

## <a name="add-a-new-answer"></a><span data-ttu-id="ff8e9-132">Add a new answer</span><span class="sxs-lookup"><span data-stu-id="ff8e9-132">Add a new answer</span></span>

<span data-ttu-id="ff8e9-133">You can add a new answer if any of the existing answers that were matched are incorrect or the answer does not exist in the knowledge base (no good match found in the KB).</span><span class="sxs-lookup"><span data-stu-id="ff8e9-133">You can add a new answer if any of the existing answers that were matched are incorrect or the answer does not exist in the knowledge base (no good match found in the KB).</span></span> <span data-ttu-id="ff8e9-134">Enter the new answer to current question in the text box and press enter to add it.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-134">Enter the new answer to current question in the text box and press enter to add it.</span></span> 

<span data-ttu-id="ff8e9-135">Select **Save and Train** to persist this answer.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-135">Select **Save and Train** to persist this answer.</span></span> <span data-ttu-id="ff8e9-136">A new question-answer pair has now been added to your knowledge base.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-136">A new question-answer pair has now been added to your knowledge base.</span></span>

![Access Test](../media/qnamaker-how-to-test-kb/add-answer.png)

> [!NOTE]
> <span data-ttu-id="ff8e9-138">All edits to your knowledge base only get saved when you press the **Save and Train** button.</span><span class="sxs-lookup"><span data-stu-id="ff8e9-138">All edits to your knowledge base only get saved when you press the **Save and Train** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff8e9-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff8e9-139">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ff8e9-140">Publish a knowledge base</span><span class="sxs-lookup"><span data-stu-id="ff8e9-140">Publish a knowledge base</span></span>](./publish-knowledge-base.md)
