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
# <a name="enable-active-learning-by-reviewing-endpoint-utterances"></a>Enable active learning by reviewing endpoint utterances
Active learning is one of three strategies to improve prediction accuracy and the easiest to implement. 

## <a name="what-is-active-learning"></a>What is active learning
Active learning is a two-step process. First, LUIS selects utterances it receives at the app's endpoint that need validation. The second step is performed by the app owner or collaborator to validate the selected utterances for [review](luis-how-to-review-endoint-utt.md), including the correct intent and any entities within the intent. After reviewing the utterances, train and publish the app again. 

## <a name="which-utterances-are-on-the-review-list"></a>Which utterances are on the review list
LUIS adds utterances to the review list when the top firing intent has a low score or the top two intents' scores are too close. 

## <a name="single-pool-for-utterances-per-app"></a>Single pool for utterances per app
The **Review endpoint utterances** list doesn't change based on the version. There is a single pool of utterances to review, regardless of which version the utterance you are actively editing or which version of the app was published at the endpoint. 

## <a name="where-are-the-utterances-from"></a>Where are the utterances from
Endpoint utterances are taken from end-user queries on the application’s HTTP endpoint. If your app is not published or has not received hits yet, you do not have any utterances to review. If no endpoint hits are received for a specific intent or entity, you do not have utterances to review that contain them. 

## <a name="schedule-review-periodically"></a>Schedule review periodically
Reviewing suggested utterances doesn't need to be done every day but should be part of your regular maintenance of LUIS. 

## <a name="delete-review-items-programmatically"></a>Delete review items programmatically
If your app is large, you may choose to review some utterances and delete the rest from the list programmatically. This is done by first [getting](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c0a) the list and then [deleting](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/58b6f32139e2bb139ce823c9) the utterances by ID.

## <a name="next-steps"></a>Next steps

* Learn how to [review](luis-how-to-review-endoint-utt.md) endpoint utterances
