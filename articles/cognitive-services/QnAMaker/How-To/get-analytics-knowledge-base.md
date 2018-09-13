---
title: How to get analytics on your knowledge base - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: How to get analytics on your knowledge base
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 05/07/2018
ms.author: saneppal
ms.openlocfilehash: 1588d0c5a8eaf4e161b5319c9f33a772dc56b247
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868900"
---
# <a name="get-analytics-on-your-knowledge-base"></a><span data-ttu-id="c8b5d-103">Get analytics on your knowledge base</span><span class="sxs-lookup"><span data-stu-id="c8b5d-103">Get analytics on your knowledge base</span></span>

<span data-ttu-id="c8b5d-104">QnA Maker stores all chat logs and other telemetry, if you have enabled App Insights during the [creation of your QnA Maker service](./set-up-qnamaker-service-azure.md).</span><span class="sxs-lookup"><span data-stu-id="c8b5d-104">QnA Maker stores all chat logs and other telemetry, if you have enabled App Insights during the [creation of your QnA Maker service](./set-up-qnamaker-service-azure.md).</span></span> <span data-ttu-id="c8b5d-105">Run the sample queries to get your chat logs from App Insights.</span><span class="sxs-lookup"><span data-stu-id="c8b5d-105">Run the sample queries to get your chat logs from App Insights.</span></span>

1. <span data-ttu-id="c8b5d-106">Go to your App Insights resource.</span><span class="sxs-lookup"><span data-stu-id="c8b5d-106">Go to your App Insights resource.</span></span>

    ![Select your application insights resource](../media/qnamaker-how-to-analytics-kb/resources-created.png)

2. <span data-ttu-id="c8b5d-108">Select **Analytics**.</span><span class="sxs-lookup"><span data-stu-id="c8b5d-108">Select **Analytics**.</span></span> <span data-ttu-id="c8b5d-109">A new window opens where you can query QnA Maker telemetry.</span><span class="sxs-lookup"><span data-stu-id="c8b5d-109">A new window opens where you can query QnA Maker telemetry.</span></span>

    ![Select Analytics](../media/qnamaker-how-to-analytics-kb/analytics.png)

3. <span data-ttu-id="c8b5d-111">Paste in the following query and run it.</span><span class="sxs-lookup"><span data-stu-id="c8b5d-111">Paste in the following query and run it.</span></span>

    ```query
        requests
        | where url endswith "generateAnswer"
        | project timestamp, id, name, resultCode, duration
        | parse name with *"/knowledgebases/"KbId"/generateAnswer"
        | join kind= inner (
        traces | extend id = operation_ParentId
        ) on id
        | extend question = tostring(customDimensions['Question'])
        | extend answer = tostring(customDimensions['Answer'])
        | project KbId, timestamp, resultCode, duration, question, answer
    ```

    <span data-ttu-id="c8b5d-112">Select **Run** to run the query.</span><span class="sxs-lookup"><span data-stu-id="c8b5d-112">Select **Run** to run the query.</span></span>

    ![Run query](../media/qnamaker-how-to-analytics-kb/run-query.png)

## <a name="run-queries-for-other-analytics-on-your-qna-maker-knowledge-base"></a><span data-ttu-id="c8b5d-114">Run queries for other analytics on your QnA Maker knowledge base</span><span class="sxs-lookup"><span data-stu-id="c8b5d-114">Run queries for other analytics on your QnA Maker knowledge base</span></span>

### <a name="total-90-day-traffic"></a><span data-ttu-id="c8b5d-115">Total 90-day traffic</span><span class="sxs-lookup"><span data-stu-id="c8b5d-115">Total 90-day traffic</span></span>

```query
    //Total Traffic
    requests
    | where url endswith "generateAnswer" and name startswith "POST"
    | parse name with *"/knowledgebases/"KbId"/generateAnswer" 
    | summarize ChatCount=count() by bin(timestamp, 1d), KbId
``` 

### <a name="total-question-traffic-in-a-given-time-period"></a><span data-ttu-id="c8b5d-116">Total question traffic in a given time period</span><span class="sxs-lookup"><span data-stu-id="c8b5d-116">Total question traffic in a given time period</span></span>

```query
    //Total Question Traffic in a given time period
    let startDate = todatetime('2018-02-18');
    let endDate = todatetime('2018-03-12');
    requests
    | where timestamp <= endDate and timestamp >=startDate
    | where url endswith "generateAnswer" and name startswith "POST" 
    | parse name with *"/knowledgebases/"KbId"/generateAnswer" 
    | summarize ChatCount=count() by KbId
```

### <a name="user-traffic"></a><span data-ttu-id="c8b5d-117">User traffic</span><span class="sxs-lookup"><span data-stu-id="c8b5d-117">User traffic</span></span>

```query
    //User Traffic
    requests
    | where url endswith "generateAnswer"
    | project timestamp, id, name, resultCode, duration
    | parse name with *"/knowledgebases/"KbId"/generateAnswer"
    | join kind= inner (
    traces | extend id = operation_ParentId 
    ) on id
    | extend UserId = tostring(customDimensions['UserId'])
    | summarize ChatCount=count() by bin(timestamp, 1d), UserId, KbId
```

### <a name="latency-distribution-of-questions"></a><span data-ttu-id="c8b5d-118">Latency distribution of questions</span><span class="sxs-lookup"><span data-stu-id="c8b5d-118">Latency distribution of questions</span></span>

```query
    //Latency distribution of questions
    requests
    | where url endswith "generateAnswer" and name startswith "POST"
    | parse name with *"/knowledgebases/"KbId"/generateAnswer" 
    | project timestamp, id, name, resultCode, performanceBucket, KbId
    | summarize count() by performanceBucket, KbId
```

## <a name="next-steps"></a><span data-ttu-id="c8b5d-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="c8b5d-119">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c8b5d-120">Manage keys</span><span class="sxs-lookup"><span data-stu-id="c8b5d-120">Manage keys</span></span>](./key-management.md)
