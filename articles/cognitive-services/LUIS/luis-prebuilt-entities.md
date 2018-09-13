---
title: Prebuilt entities for Language Understanding (LUIS)
titleSuffix: Azure Cognitive Services
description: LUIS includes a set of prebuilt entities for recognizing common types of information, like dates, times, numbers, measurements and currency. Prebuilt entity support varies by the culture of your LUIS app.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 09/06/2018
ms.author: diberry
ms.openlocfilehash: f62c078a023d9ee7ca535cb5e02623df7a568e8a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870118"
---
# <a name="prebuilt-entities-to-recognize-common-data-types"></a><span data-ttu-id="de57d-104">Prebuilt entities to recognize common data types</span><span class="sxs-lookup"><span data-stu-id="de57d-104">Prebuilt entities to recognize common data types</span></span>

<span data-ttu-id="de57d-105">LUIS includes a set of prebuilt entities for recognizing common types of information, like dates, times, numbers, measurements, and currency.</span><span class="sxs-lookup"><span data-stu-id="de57d-105">LUIS includes a set of prebuilt entities for recognizing common types of information, like dates, times, numbers, measurements, and currency.</span></span> <span data-ttu-id="de57d-106">Prebuilt entity support varies by the culture of your LUIS app.</span><span class="sxs-lookup"><span data-stu-id="de57d-106">Prebuilt entity support varies by the culture of your LUIS app.</span></span> <span data-ttu-id="de57d-107">For a full list of the prebuilt entities that LUIS supports, including support by culture, see the [prebuilt entity reference](./luis-reference-prebuilt-entities.md).</span><span class="sxs-lookup"><span data-stu-id="de57d-107">For a full list of the prebuilt entities that LUIS supports, including support by culture, see the [prebuilt entity reference](./luis-reference-prebuilt-entities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="de57d-108">**builtin.datetime** is deprecated.</span><span class="sxs-lookup"><span data-stu-id="de57d-108">**builtin.datetime** is deprecated.</span></span> <span data-ttu-id="de57d-109">It is replaced by [**builtin.datetimeV2**](luis-reference-prebuilt-datetimev2.md), which provides recognition of date and time ranges, as well as improved recognition of ambiguous dates and times.</span><span class="sxs-lookup"><span data-stu-id="de57d-109">It is replaced by [**builtin.datetimeV2**](luis-reference-prebuilt-datetimev2.md), which provides recognition of date and time ranges, as well as improved recognition of ambiguous dates and times.</span></span>

## <a name="add-a-prebuilt-entity"></a><span data-ttu-id="de57d-110">Add a prebuilt entity</span><span class="sxs-lookup"><span data-stu-id="de57d-110">Add a prebuilt entity</span></span>

1. <span data-ttu-id="de57d-111">Open your app by clicking its name on **My Apps** page, and then click **Entities** in the left side.</span><span class="sxs-lookup"><span data-stu-id="de57d-111">Open your app by clicking its name on **My Apps** page, and then click **Entities** in the left side.</span></span> 
2. <span data-ttu-id="de57d-112">On the **Entities** page, click **Manage prebuilt entities**.</span><span class="sxs-lookup"><span data-stu-id="de57d-112">On the **Entities** page, click **Manage prebuilt entities**.</span></span>

3. <span data-ttu-id="de57d-113">In **Add prebuilt entities** dialog box, click the prebuilt entity you want to add (for example, "datetimeV2").</span><span class="sxs-lookup"><span data-stu-id="de57d-113">In **Add prebuilt entities** dialog box, click the prebuilt entity you want to add (for example, "datetimeV2").</span></span> <span data-ttu-id="de57d-114">Then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="de57d-114">Then click **Save**.</span></span>

    ![Add prebuilt entity dialog box](./media/luis-use-prebuilt-entity/add-prebuilt-entity-dialog.png)

## <a name="use-a-prebuilt-number-entity"></a><span data-ttu-id="de57d-116">Use a prebuilt number entity</span><span class="sxs-lookup"><span data-stu-id="de57d-116">Use a prebuilt number entity</span></span>
<span data-ttu-id="de57d-117">When a prebuilt entity is included in your application, its predictions are included in your published application.</span><span class="sxs-lookup"><span data-stu-id="de57d-117">When a prebuilt entity is included in your application, its predictions are included in your published application.</span></span> <span data-ttu-id="de57d-118">The behavior of prebuilt entities is pre-trained and **cannot** be modified.</span><span class="sxs-lookup"><span data-stu-id="de57d-118">The behavior of prebuilt entities is pre-trained and **cannot** be modified.</span></span> <span data-ttu-id="de57d-119">Follow these steps to see how a prebuilt entity works:</span><span class="sxs-lookup"><span data-stu-id="de57d-119">Follow these steps to see how a prebuilt entity works:</span></span>

1. <span data-ttu-id="de57d-120">Add a **number** entity to your app, then [Train](luis-interactive-test.md) and [publish](luis-how-to-publish-app.md) the app.</span><span class="sxs-lookup"><span data-stu-id="de57d-120">Add a **number** entity to your app, then [Train](luis-interactive-test.md) and [publish](luis-how-to-publish-app.md) the app.</span></span>
2. <span data-ttu-id="de57d-121">Click on the endpoint URL in the **Publish App** page to open the LUIS endpoint in a web browser.</span><span class="sxs-lookup"><span data-stu-id="de57d-121">Click on the endpoint URL in the **Publish App** page to open the LUIS endpoint in a web browser.</span></span> 
3. <span data-ttu-id="de57d-122">Append an utterance to the URL that contains a numerical expression.</span><span class="sxs-lookup"><span data-stu-id="de57d-122">Append an utterance to the URL that contains a numerical expression.</span></span> <span data-ttu-id="de57d-123">For example, you can type in `buy two plane ticktets`, and see that LUIS identifies `two` as a `builtin.number` entity, and identifies `2` as its value in the `resolution` field.</span><span class="sxs-lookup"><span data-stu-id="de57d-123">For example, you can type in `buy two plane ticktets`, and see that LUIS identifies `two` as a `builtin.number` entity, and identifies `2` as its value in the `resolution` field.</span></span> <span data-ttu-id="de57d-124">The `resolution` field helps you resolve numbers and dates to a canonical form that's easier for your client application to use.</span><span class="sxs-lookup"><span data-stu-id="de57d-124">The `resolution` field helps you resolve numbers and dates to a canonical form that's easier for your client application to use.</span></span> 

    ![utterance in browser containing a number entity](./media/luis-use-prebuilt-entity/browser-query.png)

<span data-ttu-id="de57d-126">LUIS can intelligently recognize numbers that aren't in non-standard form.</span><span class="sxs-lookup"><span data-stu-id="de57d-126">LUIS can intelligently recognize numbers that aren't in non-standard form.</span></span> <span data-ttu-id="de57d-127">Try out different numerical expressions in your utterances and see what LUIS returns.</span><span class="sxs-lookup"><span data-stu-id="de57d-127">Try out different numerical expressions in your utterances and see what LUIS returns.</span></span>

<span data-ttu-id="de57d-128">The following example shows a JSON response from LUIS, that includes the resolution of the value 24, for the utterance "two dozen".</span><span class="sxs-lookup"><span data-stu-id="de57d-128">The following example shows a JSON response from LUIS, that includes the resolution of the value 24, for the utterance "two dozen".</span></span>

```json
{
  "query": "order two dozen tickets for group travel",
  "topScoringIntent": {
    "intent": "BookFlight",
    "score": 0.905443209
  },
  "entities": [
    {
      "entity": "two dozen",
      "type": "builtin.number",
      "startIndex": 6,
      "endIndex": 14,
      "resolution": {
        "value": "24"
      }
    }
  ]
}
```
## <a name="use-a-prebuilt-datetimev2-entity"></a><span data-ttu-id="de57d-129">Use a prebuilt datetimeV2 entity</span><span class="sxs-lookup"><span data-stu-id="de57d-129">Use a prebuilt datetimeV2 entity</span></span>
<span data-ttu-id="de57d-130">The **datetimeV2** prebuilt entity recognizes dates, times, date ranges, and time durations.</span><span class="sxs-lookup"><span data-stu-id="de57d-130">The **datetimeV2** prebuilt entity recognizes dates, times, date ranges, and time durations.</span></span> <span data-ttu-id="de57d-131">Follow these steps to see how the `datetimeV2` prebuilt entity works:</span><span class="sxs-lookup"><span data-stu-id="de57d-131">Follow these steps to see how the `datetimeV2` prebuilt entity works:</span></span>

1. <span data-ttu-id="de57d-132">Add a **datetimeV2** entity to your app, then [Train](luis-interactive-test.md) and [publish](luis-how-to-publish-app.md) the app.</span><span class="sxs-lookup"><span data-stu-id="de57d-132">Add a **datetimeV2** entity to your app, then [Train](luis-interactive-test.md) and [publish](luis-how-to-publish-app.md) the app.</span></span>
2. <span data-ttu-id="de57d-133">Click on the endpoint URL in the **Publish App** page to open the LUIS endpoint in a web browser.</span><span class="sxs-lookup"><span data-stu-id="de57d-133">Click on the endpoint URL in the **Publish App** page to open the LUIS endpoint in a web browser.</span></span> 
3. <span data-ttu-id="de57d-134">Append an utterance to the URL that contains a date range.</span><span class="sxs-lookup"><span data-stu-id="de57d-134">Append an utterance to the URL that contains a date range.</span></span> <span data-ttu-id="de57d-135">For example, you can type in `book a flight tomorrow`, and see that LUIS identifies `tomorrow` as a `builtin.datetimeV2.date` entity, and identifies tomorrow's date as its value in the `resolution` field.</span><span class="sxs-lookup"><span data-stu-id="de57d-135">For example, you can type in `book a flight tomorrow`, and see that LUIS identifies `tomorrow` as a `builtin.datetimeV2.date` entity, and identifies tomorrow's date as its value in the `resolution` field.</span></span> 

<span data-ttu-id="de57d-136">The following example shows what the JSON response from LUIS might look like if today's date were October 31st, 2017.</span><span class="sxs-lookup"><span data-stu-id="de57d-136">The following example shows what the JSON response from LUIS might look like if today's date were October 31st, 2017.</span></span>

```json
{
  "query": "book a flight tomorrow",
  "topScoringIntent": {
    "intent": "BookFlight",
    "score": 0.9063408
  },
  "entities": [
    {
      "entity": "tomorrow",
      "type": "builtin.datetimeV2.date",
      "startIndex": 14,
      "endIndex": 21,
      "resolution": {
        "values": [
          {
            "timex": "2017-11-01",
            "type": "date",
            "value": "2017-11-01"
          }
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="de57d-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="de57d-137">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="de57d-138">Prebuilt entity reference</span><span class="sxs-lookup"><span data-stu-id="de57d-138">Prebuilt entity reference</span></span>](./luis-reference-prebuilt-entities.md)
