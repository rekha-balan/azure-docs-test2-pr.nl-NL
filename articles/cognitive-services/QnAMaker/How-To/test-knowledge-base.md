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
# <a name="test-your-knowledge-base"></a>Test your knowledge base

Testing your QnA Maker knowledge base is an important part of an iterative process to improve the accuracy of the responses being returned. You can test the knowledge base through an enhanced chat interface that also allows you make edits.

## <a name="test-answer-matching"></a>Test answer matching

1.  Access your knowledge base by selecting its name on the **My knowledge bases** page.
2.  To access the Test slide-out panel, select **Test** in your application's top panel.

    ![Access Test](../media/qnamaker-how-to-test-kb/access-test.png)

3.  Enter a query in the text box and select Enter.

4.  The best-matched answer from the knowledge base is returned as the response.

## <a name="clear-test-panel"></a>Clear test panel

To clear all the entered test queries and their results from the test console, select **Start over** at the upper-left corner of the Test panel.

## <a name="close-test-panel"></a>Close test panel

To close the Test panel, select the **Test** button again. While the Test panel is open, you cannot edit the Knowledge Base contents.

## <a name="inspect-score"></a>Inspect score

You inspect details of the test result in the Inspect panel.

1.  With the Test slide-out panel open, select **Inspect** for more details on that response.

    ![Inspect responses](../media/qnamaker-how-to-test-kb/inspect.png)

2.  The Inspection panel appears. The panel includes the top scoring intent as well as any identified entities. The panel shows the result of the selected utterance.

## <a name="correct-the-top-scoring-answer"></a>Correct the top scoring answer

If the top scoring answer is incorrect, select the correct answer from the list and select **Save and Train**.

![Access Test](../media/qnamaker-how-to-test-kb/choose-answer.png)

## <a name="add-alternate-questions"></a>Add alternate questions

You can add alternate forms of a question to a given answer. Type the alternate answers in the text box and click enter to add them. Select **Save and Train** to store the updates.

![Access Test](../media/qnamaker-how-to-test-kb/add-alternate-question.png)

## <a name="add-a-new-answer"></a>Add a new answer

You can add a new answer if any of the existing answers that were matched are incorrect or the answer does not exist in the knowledge base (no good match found in the KB). Enter the new answer to current question in the text box and press enter to add it. 

Select **Save and Train** to persist this answer. A new question-answer pair has now been added to your knowledge base.

![Access Test](../media/qnamaker-how-to-test-kb/add-answer.png)

> [!NOTE]
> All edits to your knowledge base only get saved when you press the **Save and Train** button.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Publish a knowledge base](./publish-knowledge-base.md)
