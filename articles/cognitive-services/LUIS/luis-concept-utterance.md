---
title: Utterances in LUIS apps in Azure | Microsoft Docs
description: Add utterances in Language Understanding Intelligent Service (LUIS) apps.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 02/13/2018
ms.author: diberry
ms.openlocfilehash: 6f962d0aaf631051c841be29d2854a89bf58ac25
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870559"
---
# <a name="utterances-in-luis"></a>Utterances in LUIS

**Utterances** are input from the user that your app needs to interpret. To train LUIS to extract intents and entities from them, it's important to capture a variety of different inputs for each intent. Active learning, or the process of continuing to train on new utterances, is essential to machine-learned intelligence that LUIS provides.

Collect phrases that you think users will enter. Include utterances that mean the same thing but are constructed differently in word length and word placement. 

## <a name="how-to-choose-varied-utterances"></a>How to choose varied utterances
When you first get started by [adding example utterances](luis-how-to-add-example-utterances.md) to your LUIS model, here are some principles to keep in mind.

### <a name="utterances-arent-always-well-formed"></a>Utterances aren't always well formed
It may be a sentence, like "Book me a ticket to Paris", or a fragment of a sentence, like "Booking" or "Paris flight."  Users often make spelling mistakes. When planning your app, consider whether or not you spell-check user input before passing it to LUIS. The [Bing Spell Check API][BingSpellCheck] integrates with LUIS. You can associate your LUIS app with an external key for the Bing Spell Check API when you publish it. If you do not spell check user utterances, you should train LUIS on utterances that include typos and misspellings.

### <a name="use-the-representative-language-of-the-user"></a>Use the representative language of the user
When choosing utterances, be aware that what you think is a common term or phrase might not be to the typical user of your client application. They may not have domain experience. So be careful when using terms or phrases that a user would only say if they were an expert.

### <a name="choose-varied-terminology-as-well-as-phrasing"></a>Choose varied terminology as well as phrasing
You will find that even if you make efforts to create varied sentence patterns, you will still repeat some vocabulary.

Take these example utterances:
```
how do I get a computer?
Where do I get a computer?
I want to get a computer, how do I go about it?
When can I have a computer? 
```
The core term here, "computer", is not varied. They could say desktop computer, laptop, workstation, or even just machine. LUIS intelligently infers synonyms from context, but when you create utterances for training, it's still better to vary them.

## <a name="example-utterances-in-each-intent"></a>Example utterances in each intent
Each intent needs to have example utterances, at least 10 to 15. If you have an intent that does not have any example utterances, you will not be able to train LUIS. If you have an intent with one or very few example utterances, LUIS will not accurately predict the intent. 

## <a name="add-small-groups-of-10-15-utterances-for-each-authoring-iteration"></a>Add small groups of 10-15 utterances for each authoring iteration
In each iteration of the model, do not add a large quantity of utterances. Add utterances in quantities of tens. [Train](luis-how-to-train.md), [publish](luis-how-to-publish-app.md), and [test](luis-interactive-test.md) again.  

LUIS builds effective models with utterances that are selected carefully. Adding too many utterances is not valuable because it introduces confusion.  

It is better to start with a few utterances, then [review endpoint utterances](luis-how-to-review-endoint-utt.md) for correct intent prediction and entity extraction.

## <a name="ignoring-words-and-punctuation"></a>Ignoring words and punctuation
If you want to ignore specific words or punctuation in the example utterance, use a [pattern](luis-concept-patterns.md#pattern-syntax) with the _ignore_ syntax. 

## <a name="training-utterances"></a>Training utterances
Training is non-deterministic: the utterance prediction could vary slightly across versions or apps.

## <a name="testing-utterances"></a>Testing utterances 

Developers should start testing their LUIS application with real traffic by sending utterances to the endpoint. These utterances are used to improve the performance of the intents and entities with [Review utterances](luis-how-to-review-endoint-utt.md). Tests submitted with the LUIS website testing pane are not sent through the endpoint, and so do not contribute to active learning. 

## <a name="review-utterances"></a>Review utterances
After your model is trained, published, and receiving [endpoint](luis-glossary.md#endpoint) queries, [review the utterances](luis-how-to-review-endoint-utt.md) suggested by LUIS. LUIS selects endpoint utterances that have low scores for either the intent or entity. 

## <a name="best-practices"></a>Best practices
Review [best practices](luis-concept-best-practices.md) to learn more.

## <a name="next-steps"></a>Next steps
See [Add example utterances](luis-how-to-add-example-utterances.md) for information on training a LUIS app to understand user utterances.

[BingSpellCheck]: https://docs.microsoft.com/azure/cognitive-services/bing-spell-check/proof-text