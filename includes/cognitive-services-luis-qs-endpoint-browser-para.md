---
title: include file
description: include file
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: luis
ms.topic: include
ms.custom: include file
ms.date: 08/16/2018
ms.author: diberry
ms.openlocfilehash: dae56e05f01e83f05e75fdf378c0c50679d18728
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45013027"
---
<span data-ttu-id="a9896-103">To understand what a LUIS prediction endpoint returns, view a prediction result in a web browser.</span><span class="sxs-lookup"><span data-stu-id="a9896-103">To understand what a LUIS prediction endpoint returns, view a prediction result in a web browser.</span></span> <span data-ttu-id="a9896-104">In order to query a public app, you need your own key and the app ID.</span><span class="sxs-lookup"><span data-stu-id="a9896-104">In order to query a public app, you need your own key and the app ID.</span></span> <span data-ttu-id="a9896-105">The public IoT app ID, `df67dcdb-c37d-46af-88e1-8b97951ca1c2`, is provided as part of the URL in step one.</span><span class="sxs-lookup"><span data-stu-id="a9896-105">The public IoT app ID, `df67dcdb-c37d-46af-88e1-8b97951ca1c2`, is provided as part of the URL in step one.</span></span>

<span data-ttu-id="a9896-106">The format of the URL for a **GET** endpoint request is:</span><span class="sxs-lookup"><span data-stu-id="a9896-106">The format of the URL for a **GET** endpoint request is:</span></span>

```JSON
https://<region>.api.cognitive.microsoft.com/luis/v2.0/apps/<appID>?subscription-key=<YOUR-KEY>&q=<user-utterance>
```

1. <span data-ttu-id="a9896-107">The endpoint of the public IoT app is in this format: `https://westus.api.cognitive.microsoft.com/luis/v2.0/apps/df67dcdb-c37d-46af-88e1-8b97951ca1c2?subscription-key=<YOUR_KEY>&q=turn on the bedroom light`</span><span class="sxs-lookup"><span data-stu-id="a9896-107">The endpoint of the public IoT app is in this format: `https://westus.api.cognitive.microsoft.com/luis/v2.0/apps/df67dcdb-c37d-46af-88e1-8b97951ca1c2?subscription-key=<YOUR_KEY>&q=turn on the bedroom light`</span></span>

    <span data-ttu-id="a9896-108">Copy the URL and substitute your key for the value of `<YOUR_KEY>`.</span><span class="sxs-lookup"><span data-stu-id="a9896-108">Copy the URL and substitute your key for the value of `<YOUR_KEY>`.</span></span>

2. <span data-ttu-id="a9896-109">Paste the URL into a browser window and press Enter.</span><span class="sxs-lookup"><span data-stu-id="a9896-109">Paste the URL into a browser window and press Enter.</span></span> <span data-ttu-id="a9896-110">The browser displays a JSON result that indicates that LUIS detects the `HomeAutomation.TurnOn` intent as the top intent and the `HomeAutomation.Room` entity with the value `bedroom`.</span><span class="sxs-lookup"><span data-stu-id="a9896-110">The browser displays a JSON result that indicates that LUIS detects the `HomeAutomation.TurnOn` intent as the top intent and the `HomeAutomation.Room` entity with the value `bedroom`.</span></span>

    ```JSON
    {
      "query": "turn on the bedroom light",
      "topScoringIntent": {
        "intent": "HomeAutomation.TurnOn",
        "score": 0.809439957
      },
      "entities": [
        {
          "entity": "bedroom",
          "type": "HomeAutomation.Room",
          "startIndex": 12,
          "endIndex": 18,
          "score": 0.8065475
        }
      ]
    }
    ```

3. <span data-ttu-id="a9896-111">Change the value of the `q=` parameter in the URL to `turn off the living room light`, and press Enter.</span><span class="sxs-lookup"><span data-stu-id="a9896-111">Change the value of the `q=` parameter in the URL to `turn off the living room light`, and press Enter.</span></span> <span data-ttu-id="a9896-112">The result now indicates that LUIS detected the `HomeAutomation.TurnOff` intent as the top intent and the `HomeAutomation.Room` entity with value `living room`.</span><span class="sxs-lookup"><span data-stu-id="a9896-112">The result now indicates that LUIS detected the `HomeAutomation.TurnOff` intent as the top intent and the `HomeAutomation.Room` entity with value `living room`.</span></span> 

    ```JSON
    {
      "query": "turn off the living room light",
      "topScoringIntent": {
        "intent": "HomeAutomation.TurnOff",
        "score": 0.984057844
      },
      "entities": [
        {
          "entity": "living room",
          "type": "HomeAutomation.Room",
          "startIndex": 13,
          "endIndex": 23,
          "score": 0.9619945
        }
      ]
    }
    ```
