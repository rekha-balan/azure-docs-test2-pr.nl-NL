---
title: Use metadata in your knowledge base along with the GenerateAnswer API | Microsoft Docs
description: Using metadata with GenerateAnswer API
services: cognitive-services
author: pchoudhari
manager: rsrikan
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 05/18/2018
ms.author: pchoudh
ms.openlocfilehash: e1b7c82e6998705bdc7e1c1a5d279bda7793667a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856640"
---
# <a name="using-metadata-and-the-generateanswer-api"></a><span data-ttu-id="cb3bd-103">Using metadata and the GenerateAnswer API</span><span class="sxs-lookup"><span data-stu-id="cb3bd-103">Using metadata and the GenerateAnswer API</span></span>

<span data-ttu-id="cb3bd-104">QnA Maker lets you add metadata, in the form of key/value pairs, to your question/answer sets.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-104">QnA Maker lets you add metadata, in the form of key/value pairs, to your question/answer sets.</span></span> <span data-ttu-id="cb3bd-105">This information can be used to filter results to user queries and to store additional information that can be used in follow-up conversations.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-105">This information can be used to filter results to user queries and to store additional information that can be used in follow-up conversations.</span></span> <span data-ttu-id="cb3bd-106">For more information, see [Knowledge base](../Concepts/knowledge-base.md).</span><span class="sxs-lookup"><span data-stu-id="cb3bd-106">For more information, see [Knowledge base](../Concepts/knowledge-base.md).</span></span>

## <a name="qna-entity"></a><span data-ttu-id="cb3bd-107">QnA Entity</span><span class="sxs-lookup"><span data-stu-id="cb3bd-107">QnA Entity</span></span>

<span data-ttu-id="cb3bd-108">First it's important to understand how QnA Maker stores the question/answer data.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-108">First it's important to understand how QnA Maker stores the question/answer data.</span></span> <span data-ttu-id="cb3bd-109">The following illustration shows a QnA entity:</span><span class="sxs-lookup"><span data-stu-id="cb3bd-109">The following illustration shows a QnA entity:</span></span>

![QnA Entity](../media/qnamaker-how-to-metadata-usage/qna-entity.png)

<span data-ttu-id="cb3bd-111">Each QnA entity has a unique and persistent ID.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-111">Each QnA entity has a unique and persistent ID.</span></span> <span data-ttu-id="cb3bd-112">The ID can be used to make updates to a particular QnA entity.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-112">The ID can be used to make updates to a particular QnA entity.</span></span>

## <a name="generateanswer-api"></a><span data-ttu-id="cb3bd-113">GenerateAnswer API</span><span class="sxs-lookup"><span data-stu-id="cb3bd-113">GenerateAnswer API</span></span>

<span data-ttu-id="cb3bd-114">You use the GenerateAnswer API in your Bot or application to query your knowledge base with a user question to get the best match from the question/answer sets.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-114">You use the GenerateAnswer API in your Bot or application to query your knowledge base with a user question to get the best match from the question/answer sets.</span></span>

### <a name="generateanswer-endpoint"></a><span data-ttu-id="cb3bd-115">GenerateAnswer endpoint</span><span class="sxs-lookup"><span data-stu-id="cb3bd-115">GenerateAnswer endpoint</span></span>

<span data-ttu-id="cb3bd-116">Once you publish your knowledge base, either from the [QnA Maker portal](https://www.qnamaker.ai), or using the [API](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff), you can get the details of your GenerateAnswer endpoint.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-116">Once you publish your knowledge base, either from the [QnA Maker portal](https://www.qnamaker.ai), or using the [API](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff), you can get the details of your GenerateAnswer endpoint.</span></span>

<span data-ttu-id="cb3bd-117">To get your endpoint details:</span><span class="sxs-lookup"><span data-stu-id="cb3bd-117">To get your endpoint details:</span></span>
1. <span data-ttu-id="cb3bd-118">Log in to [https://www.qnamaker.ai](https://www.qnamaker.ai).</span><span class="sxs-lookup"><span data-stu-id="cb3bd-118">Log in to [https://www.qnamaker.ai](https://www.qnamaker.ai).</span></span>
2. <span data-ttu-id="cb3bd-119">In **My knowledge bases**, click on **View Code** for your knowledge base.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-119">In **My knowledge bases**, click on **View Code** for your knowledge base.</span></span>
<span data-ttu-id="cb3bd-120">![my knowledge bases](../media/qnamaker-how-to-metadata-usage/my-knowledge-bases.png)</span><span class="sxs-lookup"><span data-stu-id="cb3bd-120">![my knowledge bases](../media/qnamaker-how-to-metadata-usage/my-knowledge-bases.png)</span></span>
3. <span data-ttu-id="cb3bd-121">Get your GenerateAnswer endpoint details.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-121">Get your GenerateAnswer endpoint details.</span></span>

![endpoint details](../media/qnamaker-how-to-metadata-usage/view-code.png)

<span data-ttu-id="cb3bd-123">You can also get your endpoint details from the **Settings** tab of your knowledge base.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-123">You can also get your endpoint details from the **Settings** tab of your knowledge base.</span></span>

### <a name="generateanswer-request"></a><span data-ttu-id="cb3bd-124">GenerateAnswer request</span><span class="sxs-lookup"><span data-stu-id="cb3bd-124">GenerateAnswer request</span></span>

<span data-ttu-id="cb3bd-125">You call GenerateAnswer with an HTTP POST request.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-125">You call GenerateAnswer with an HTTP POST request.</span></span> <span data-ttu-id="cb3bd-126">For sample code that shows how to call GenerateAnswer, see the [quickstarts](../quickstarts/csharp.md).</span><span class="sxs-lookup"><span data-stu-id="cb3bd-126">For sample code that shows how to call GenerateAnswer, see the [quickstarts](../quickstarts/csharp.md).</span></span>

- <span data-ttu-id="cb3bd-127">**Request URL**: https://{QnA Maker endpoint}/knowledgebases/{knowledge base ID}/generateAnswer</span><span class="sxs-lookup"><span data-stu-id="cb3bd-127">**Request URL**: https://{QnA Maker endpoint}/knowledgebases/{knowledge base ID}/generateAnswer</span></span>

- <span data-ttu-id="cb3bd-128">**Request parameters**:</span><span class="sxs-lookup"><span data-stu-id="cb3bd-128">**Request parameters**:</span></span> 
    - <span data-ttu-id="cb3bd-129">**Knowledge base ID** (string): The GUID for your knowledge base.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-129">**Knowledge base ID** (string): The GUID for your knowledge base.</span></span>
    - <span data-ttu-id="cb3bd-130">**QnAMaker endpoint** (string): The hostname of the endpoint deployed in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-130">**QnAMaker endpoint** (string): The hostname of the endpoint deployed in your Azure subscription.</span></span>
- <span data-ttu-id="cb3bd-131">**Request headers**</span><span class="sxs-lookup"><span data-stu-id="cb3bd-131">**Request headers**</span></span>
    - <span data-ttu-id="cb3bd-132">**Content-Type** (string): The media type of the body sent to the API.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-132">**Content-Type** (string): The media type of the body sent to the API.</span></span>
    - <span data-ttu-id="cb3bd-133">**Authorization** (string): Your endpoint key (EndpointKey xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx).</span><span class="sxs-lookup"><span data-stu-id="cb3bd-133">**Authorization** (string): Your endpoint key (EndpointKey xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx).</span></span>
- <span data-ttu-id="cb3bd-134">**Request body**</span><span class="sxs-lookup"><span data-stu-id="cb3bd-134">**Request body**</span></span>
    - <span data-ttu-id="cb3bd-135">**question** (string): A user question to be queried against your knowledge base.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-135">**question** (string): A user question to be queried against your knowledge base.</span></span>
    - <span data-ttu-id="cb3bd-136">**top** (optional, integer): The number of ranked results to include in the output.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-136">**top** (optional, integer): The number of ranked results to include in the output.</span></span> <span data-ttu-id="cb3bd-137">The default value is 1.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-137">The default value is 1.</span></span>
    - <span data-ttu-id="cb3bd-138">**userId** (optional, string): A unique ID to identify the user.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-138">**userId** (optional, string): A unique ID to identify the user.</span></span> <span data-ttu-id="cb3bd-139">This ID will be recorded in the chat logs.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-139">This ID will be recorded in the chat logs.</span></span>
    - <span data-ttu-id="cb3bd-140">**strictFilters** (optional, string): If specified, tells QnA Maker to return only answers that have the specified metadata.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-140">**strictFilters** (optional, string): If specified, tells QnA Maker to return only answers that have the specified metadata.</span></span> <span data-ttu-id="cb3bd-141">For more information, see below.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-141">For more information, see below.</span></span>
    ```json
    {
        "question": "qna maker and luis",
        "top": 6,
        "strictFilters": [
        {
            "name": "category",
            "value": "api"
        }],
        "userId": "sd53lsY="
    }
    ```

### <a name="generateanswer-response"></a><span data-ttu-id="cb3bd-142">GenerateAnswer Response</span><span class="sxs-lookup"><span data-stu-id="cb3bd-142">GenerateAnswer Response</span></span>

- <span data-ttu-id="cb3bd-143">**Response 200** - A successful call returns the result of the question.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-143">**Response 200** - A successful call returns the result of the question.</span></span> <span data-ttu-id="cb3bd-144">The response contains the following fields:</span><span class="sxs-lookup"><span data-stu-id="cb3bd-144">The response contains the following fields:</span></span>
    - <span data-ttu-id="cb3bd-145">**answers** - A list of answers for the user query, sorted in decreasing order of ranking score.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-145">**answers** - A list of answers for the user query, sorted in decreasing order of ranking score.</span></span>
        - <span data-ttu-id="cb3bd-146">**score**: A ranking score between 0 and 100.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-146">**score**: A ranking score between 0 and 100.</span></span>
        - <span data-ttu-id="cb3bd-147">**questions**: The questions provided by the user.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-147">**questions**: The questions provided by the user.</span></span>
        - <span data-ttu-id="cb3bd-148">**answer**: The answer to the question.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-148">**answer**: The answer to the question.</span></span>
        - <span data-ttu-id="cb3bd-149">**source**: The name of the source from which the answer was extracted or saved in the knowledge base.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-149">**source**: The name of the source from which the answer was extracted or saved in the knowledge base.</span></span>
        - <span data-ttu-id="cb3bd-150">**metadata**: The metadata associated with the answer.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-150">**metadata**: The metadata associated with the answer.</span></span>
            - <span data-ttu-id="cb3bd-151">name: Metadata name.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-151">name: Metadata name.</span></span> <span data-ttu-id="cb3bd-152">(string, max Length: 100, required)</span><span class="sxs-lookup"><span data-stu-id="cb3bd-152">(string, max Length: 100, required)</span></span>
            - <span data-ttu-id="cb3bd-153">value: Metadata value.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-153">value: Metadata value.</span></span> <span data-ttu-id="cb3bd-154">(string, max Length: 100, required)</span><span class="sxs-lookup"><span data-stu-id="cb3bd-154">(string, max Length: 100, required)</span></span>
        - <span data-ttu-id="cb3bd-155">**Id**: A unique ID assigned to the answer.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-155">**Id**: A unique ID assigned to the answer.</span></span>
    ```json
    {
        "answers": [
            {
                "score": 28.54820341616869,
                "Id": 20,
                "answer": "There is no direct integration of LUIS with QnA Maker. But, in your bot code, you can use LUIS and QnA Maker together. [View a sample bot](https://github.com/Microsoft/BotBuilder-CognitiveServices/tree/master/Node/samples/QnAMaker/QnAWithLUIS)",
                "source": "Custom Editorial",
                "questions": [
                    "How can I integrate LUIS with QnA Maker?"
                ],
                "metadata": [
                    {
                        "name": "category",
                        "value": "api"
                    }
                ]
            }
        ]
    }
    ```

## <a name="metadata-example"></a><span data-ttu-id="cb3bd-156">Metadata example</span><span class="sxs-lookup"><span data-stu-id="cb3bd-156">Metadata example</span></span>

<span data-ttu-id="cb3bd-157">Consider the below FAQ data for restaurants in Hyderabad.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-157">Consider the below FAQ data for restaurants in Hyderabad.</span></span> <span data-ttu-id="cb3bd-158">Add metadata to your knowledge base by clicking on the gear icon.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-158">Add metadata to your knowledge base by clicking on the gear icon.</span></span>

![add metadata](../media/qnamaker-how-to-metadata-usage/add-metadata.png)

### <a name="filter-results-with-strictfilters"></a><span data-ttu-id="cb3bd-160">Filter results with strictFilters</span><span class="sxs-lookup"><span data-stu-id="cb3bd-160">Filter results with strictFilters</span></span>

<span data-ttu-id="cb3bd-161">Consider the user question "When does this hotel close?"</span><span class="sxs-lookup"><span data-stu-id="cb3bd-161">Consider the user question "When does this hotel close?"</span></span> <span data-ttu-id="cb3bd-162">where the intent is implied for the restaurant "Paradise."</span><span class="sxs-lookup"><span data-stu-id="cb3bd-162">where the intent is implied for the restaurant "Paradise."</span></span>

<span data-ttu-id="cb3bd-163">Since results are required only for the restaurant "Paradise", you can set a filter in the GenerateAnswer call on the metadata "Restaurant Name", as follows.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-163">Since results are required only for the restaurant "Paradise", you can set a filter in the GenerateAnswer call on the metadata "Restaurant Name", as follows.</span></span>

```json
{
    "question": "When does this hotel close?",
    "top": 1,
    "strictFilters": [
      {
        "name": "restaurant",
        "value": "paradise"
      }]
}
```

### <a name="keep-context"></a><span data-ttu-id="cb3bd-164">Keep context</span><span class="sxs-lookup"><span data-stu-id="cb3bd-164">Keep context</span></span>
<span data-ttu-id="cb3bd-165">The response to the GenerateAnswer contains the corresponding metadata information of the matched question/answer set, as follows.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-165">The response to the GenerateAnswer contains the corresponding metadata information of the matched question/answer set, as follows.</span></span>

```json
{
    "answers": [
        {
            "questions": [
                "What is the closing time?"
            ],
            "answer": "10.30 PM",
            "score": 100,
            "id": 1,
            "source": "Editorial",
            "metadata": [
                {
                    "name": "restaurant",
                    "value": "paradise"
                },
                {
                    "name": "location",
                    "value": "secunderabad"
                }
            ]
        }
    ]
}
```

<span data-ttu-id="cb3bd-166">This information can be used to record the context of the previous conversation for use in later conversations.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-166">This information can be used to record the context of the previous conversation for use in later conversations.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="cb3bd-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="cb3bd-167">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cb3bd-168">Create a knowledge base</span><span class="sxs-lookup"><span data-stu-id="cb3bd-168">Create a knowledge base</span></span>](./create-knowledge-base.md)
