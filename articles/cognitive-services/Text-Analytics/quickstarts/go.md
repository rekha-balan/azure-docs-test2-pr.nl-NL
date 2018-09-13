---
title: 'Quickstart: Using Go to call the Text Analytics API | Microsoft Docs'
titleSuffix: Azure Cognitive Services
description: Get information and code samples to help you quickly get started using the Text Analytics API in Microsoft Cognitive Services on Azure.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: text-analytics
ms.topic: quickstart
ms.date: 08/30/2018
ms.author: nolachar
ms.openlocfilehash: 210aec071be35fdd60582f6e13a2b245ca5e9a56
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867303"
---
# <a name="quickstart-using-go-to-call-the-text-analytics-cognitive-service"></a><span data-ttu-id="a7bb8-103">Quickstart: Using Go to call the Text Analytics Cognitive Service</span><span class="sxs-lookup"><span data-stu-id="a7bb8-103">Quickstart: Using Go to call the Text Analytics Cognitive Service</span></span>
<a name="HOLTop"></a>

<span data-ttu-id="a7bb8-104">This article shows you how to [detect language](#Detect), [analyze sentiment](#SentimentAnalysis), [extract key phrases](#KeyPhraseExtraction), and [identify linked entities](#Entities) using the [Text Analytics APIs](//go.microsoft.com/fwlink/?LinkID=759711) with Go.</span><span class="sxs-lookup"><span data-stu-id="a7bb8-104">This article shows you how to [detect language](#Detect), [analyze sentiment](#SentimentAnalysis), [extract key phrases](#KeyPhraseExtraction), and [identify linked entities](#Entities) using the [Text Analytics APIs](//go.microsoft.com/fwlink/?LinkID=759711) with Go.</span></span>

<span data-ttu-id="a7bb8-105">Refer to the [API definitions](//go.microsoft.com/fwlink/?LinkID=759346) for technical documentation for the APIs.</span><span class="sxs-lookup"><span data-stu-id="a7bb8-105">Refer to the [API definitions](//go.microsoft.com/fwlink/?LinkID=759346) for technical documentation for the APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7bb8-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a7bb8-106">Prerequisites</span></span>

<span data-ttu-id="a7bb8-107">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Text Analytics API**.</span><span class="sxs-lookup"><span data-stu-id="a7bb8-107">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Text Analytics API**.</span></span> <span data-ttu-id="a7bb8-108">You can use the **free tier for 5,000 transactions/month** to complete this quickstart.</span><span class="sxs-lookup"><span data-stu-id="a7bb8-108">You can use the **free tier for 5,000 transactions/month** to complete this quickstart.</span></span>

<span data-ttu-id="a7bb8-109">You must also have the [endpoint and access key](../How-tos/text-analytics-how-to-access-key.md) that was generated for you during sign-up.</span><span class="sxs-lookup"><span data-stu-id="a7bb8-109">You must also have the [endpoint and access key](../How-tos/text-analytics-how-to-access-key.md) that was generated for you during sign-up.</span></span>

<a name="Detect"></a>

## <a name="detect-language-request"></a><span data-ttu-id="a7bb8-110">Detect language request</span><span class="sxs-lookup"><span data-stu-id="a7bb8-110">Detect language request</span></span>

<span data-ttu-id="a7bb8-111">The Language Detection API detects the language of a text document, using the [Detect Language method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7).</span><span class="sxs-lookup"><span data-stu-id="a7bb8-111">The Language Detection API detects the language of a text document, using the [Detect Language method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7).</span></span>

1. <span data-ttu-id="a7bb8-112">Create a new Go project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="a7bb8-112">Create a new Go project in your favorite code editor.</span></span>
1. <span data-ttu-id="a7bb8-113">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="a7bb8-113">Add the code provided below.</span></span>
1. <span data-ttu-id="a7bb8-114">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="a7bb8-114">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
1. <span data-ttu-id="a7bb8-115">Replace the location in `uriBase` (currently `westcentralus`) to the region you signed up for.</span><span class="sxs-lookup"><span data-stu-id="a7bb8-115">Replace the location in `uriBase` (currently `westcentralus`) to the region you signed up for.</span></span>
1. <span data-ttu-id="a7bb8-116">Save the file with a '.go' extension.</span><span class="sxs-lookup"><span data-stu-id="a7bb8-116">Save the file with a '.go' extension.</span></span>
1. <span data-ttu-id="a7bb8-117">Open a command prompt on a computer with Go installed.</span><span class="sxs-lookup"><span data-stu-id="a7bb8-117">Open a command prompt on a computer with Go installed.</span></span>
1. <span data-ttu-id="a7bb8-118">Build the file, for example: 'go build quickstart.go'.</span><span class="sxs-lookup"><span data-stu-id="a7bb8-118">Build the file, for example: 'go build quickstart.go'.</span></span>
1. <span data-ttu-id="a7bb8-119">Run the file, for example: 'quickstart'.</span><span class="sxs-lookup"><span data-stu-id="a7bb8-119">Run the file, for example: 'quickstart'.</span></span>

```golang
package main

import (
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
    "strings"
    "time"
)

func main() {
    // Replace the subscriptionKey string value with your valid subscription key
    const subscriptionKey = "ENTER KEY HERE"

    /*
    Replace or verify the region.

    You must use the same region in your REST API call as you used to obtain your access keys.
    For example, if you obtained your access keys from the westus region, replace 
    "westcentralus" in the URI below with "westus".

    NOTE: Free trial access keys are generated in the westcentralus region, so if you are using
    a free trial access key, you should not need to change this region.
    */
    const uriBase = "https://westcentralus.api.cognitive.microsoft.com"
    const uriPath = "/text/analytics/v2.0/"

    // Detect language.
    fmt.Println("===== DETECT LANGUAGE ======")

    uri := uriBase + uriPath + "languages"

    data := []map[string]string{
        {"id": "1", "text": "This is a document written in English."},
        {"id": "2", "text": "Este es un document escrito en Español."},
        {"id": "3", "text": "这是一个用中文写的文件"},
    }

    documents, err := json.Marshal(&data)
    if err != nil {
        fmt.Printf("Error marshaling data: %v\n", err)
        return
    }

    r := strings.NewReader("{\"documents\": " + string(documents) + "}")

    client := &http.Client{
        Timeout: time.Second * 2,
    }

    req, err := http.NewRequest("POST", uri, r)
    if err != nil {
        fmt.Printf("Error creating request: %v\n", err)
        return
    }

    req.Header.Add("Content-Type", "application/json")
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)

    resp, err := client.Do(req)
    if err != nil {
        fmt.Printf("Error on request: %v\n", err)
        return
    }
    defer resp.Body.Close()

    body, err := ioutil.ReadAll(resp.Body)
    if err != nil {
        fmt.Printf("Error reading response body: %v\n", err)
        return
    }

    var f interface{}
    json.Unmarshal(body, &f)

    jsonFormatted, err := json.MarshalIndent(f, "", "  ")
    if err != nil {
        fmt.Printf("Error producing JSON: %v\n", err)
        return
    }
    fmt.Println(string(jsonFormatted))
```

## <a name="detect-language-response"></a><span data-ttu-id="a7bb8-120">Detect language response</span><span class="sxs-lookup"><span data-stu-id="a7bb8-120">Detect language response</span></span>

<span data-ttu-id="a7bb8-121">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a7bb8-121">A successful response is returned in JSON, as shown in the following example:</span></span>

```json

{
   "documents": [
      {
         "id": "1",
         "detectedLanguages": [
            {
               "name": "English",
               "iso6391Name": "en",
               "score": 1.0
            }
         ]
      },
      {
         "id": "2",
         "detectedLanguages": [
            {
               "name": "Spanish",
               "iso6391Name": "es",
               "score": 1.0
            }
         ]
      },
      {
         "id": "3",
         "detectedLanguages": [
            {
               "name": "Chinese_Simplified",
               "iso6391Name": "zh_chs",
               "score": 1.0
            }
         ]
      }
   ],
   "errors": [

   ]
}
```

<a name="SentimentAnalysis"></a>

## <a name="analyze-sentiment-request"></a><span data-ttu-id="a7bb8-122">Analyze sentiment request</span><span class="sxs-lookup"><span data-stu-id="a7bb8-122">Analyze sentiment request</span></span>

<span data-ttu-id="a7bb8-123">The Sentiment Analysis API detects the sentiment of a set of text records, using the [Sentiment method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9).</span><span class="sxs-lookup"><span data-stu-id="a7bb8-123">The Sentiment Analysis API detects the sentiment of a set of text records, using the [Sentiment method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9).</span></span> <span data-ttu-id="a7bb8-124">The following example scores two documents, one in English and another in Spanish.</span><span class="sxs-lookup"><span data-stu-id="a7bb8-124">The following example scores two documents, one in English and another in Spanish.</span></span>

<span data-ttu-id="a7bb8-125">Add the following code to the code from the [previous section](#Detect).</span><span class="sxs-lookup"><span data-stu-id="a7bb8-125">Add the following code to the code from the [previous section](#Detect).</span></span>

```golang
    // Detect sentiment.
    fmt.Println("===== DETECT SENTIMENT ======")

    uri = uriBase + uriPath + "sentiment"

    data = []map[string]string{
        {"id": "1", "language": "en", "text": "I really enjoy the new XBox One S. It has a clean look, it has 4K/HDR resolution and it is affordable."},
        {"id": "2", "language": "es", "text": "Este ha sido un dia terrible, llegué tarde al trabajo debido a un accidente automobilistico."},
    }

    documents, err = json.Marshal(&data)
    if err != nil {
        fmt.Printf("Error marshaling data: %v\n", err)
        return
    }

    r = strings.NewReader("{\"documents\": " + string(documents) + "}")

    client = &http.Client{
        Timeout: time.Second * 2,
    }

    req, err = http.NewRequest("POST", uri, r)
    if err != nil {
        fmt.Printf("Error creating request: %v\n", err)
        return
    }

    req.Header.Add("Content-Type", "application/json")
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)

    resp, err = client.Do(req)
    if err != nil {
        fmt.Printf("Error on request: %v\n", err)
        return
    }
    defer resp.Body.Close()

    body, err = ioutil.ReadAll(resp.Body)
    if err != nil {
        fmt.Printf("Error reading response body: %v\n", err)
        return
    }

    json.Unmarshal(body, &f)

    jsonFormatted, err = json.MarshalIndent(f, "", "  ")
    if err != nil {
        fmt.Printf("Error producing JSON: %v\n", err)
        return
    }
    fmt.Println(string(jsonFormatted))
```

## <a name="analyze-sentiment-response"></a><span data-ttu-id="a7bb8-126">Analyze sentiment response</span><span class="sxs-lookup"><span data-stu-id="a7bb8-126">Analyze sentiment response</span></span>

<span data-ttu-id="a7bb8-127">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a7bb8-127">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
   "documents": [
      {
         "score": 0.99984133243560791,
         "id": "1"
      },
      {
         "score": 0.024017512798309326,
         "id": "2"
      },
   ],
   "errors": [   ]
}
```

<a name="KeyPhraseExtraction"></a>

## <a name="extract-key-phrases-request"></a><span data-ttu-id="a7bb8-128">Extract key phrases request</span><span class="sxs-lookup"><span data-stu-id="a7bb8-128">Extract key phrases request</span></span>

<span data-ttu-id="a7bb8-129">The Key Phrase Extraction API extracts key-phrases from a text document, using the [Key Phrases method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6).</span><span class="sxs-lookup"><span data-stu-id="a7bb8-129">The Key Phrase Extraction API extracts key-phrases from a text document, using the [Key Phrases method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6).</span></span> <span data-ttu-id="a7bb8-130">The following example extracts key phrases for both English and Spanish documents.</span><span class="sxs-lookup"><span data-stu-id="a7bb8-130">The following example extracts key phrases for both English and Spanish documents.</span></span>

<span data-ttu-id="a7bb8-131">Add the following code to the code from the [previous section](#SentimentAnalysis).</span><span class="sxs-lookup"><span data-stu-id="a7bb8-131">Add the following code to the code from the [previous section](#SentimentAnalysis).</span></span>

```golang
    // Extract key phrases.
    fmt.Println("===== EXTRACT KEY PHRASES ======")

    uri = uriBase + uriPath + "keyPhrases"

    data = []map[string]string{
        {"id": "1", "language": "en", "text": "I really enjoy the new XBox One S. It has a clean look, it has 4K/HDR resolution and it is affordable."},
        {"id": "2", "language": "es", "text": "Si usted quiere comunicarse con Carlos, usted debe de llamarlo a su telefono movil. Carlos es muy responsable, pero necesita recibir una notificacion si hay algun problema."},
        {"id": "3", "language": "en", "text": "The Grand Hotel is a new hotel in the center of Seattle. It earned 5 stars in my review, and has the classiest decor I've ever seen."},
    }

    documents, err = json.Marshal(&data)
    if err != nil {
        fmt.Printf("Error marshaling data: %v\n", err)
        return
    }

    r = strings.NewReader("{\"documents\": " + string(documents) + "}")

    client = &http.Client{
        Timeout: time.Second * 2,
    }

    req, err = http.NewRequest("POST", uri, r)
    if err != nil {
        fmt.Printf("Error creating request: %v\n", err)
        return
    }

    req.Header.Add("Content-Type", "application/json")
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)

    resp, err = client.Do(req)
    if err != nil {
        fmt.Printf("Error on request: %v\n", err)
        return
    }
    defer resp.Body.Close()

    body, err = ioutil.ReadAll(resp.Body)
    if err != nil {
        fmt.Printf("Error reading response body: %v\n", err)
        return
    }

    json.Unmarshal(body, &f)

    jsonFormatted, err = json.MarshalIndent(f, "", "  ")
    if err != nil {
        fmt.Printf("Error producing JSON: %v\n", err)
        return
    }
    fmt.Println(string(jsonFormatted))
```

## <a name="extract-key-phrases-response"></a><span data-ttu-id="a7bb8-132">Extract key phrases response</span><span class="sxs-lookup"><span data-stu-id="a7bb8-132">Extract key phrases response</span></span>

<span data-ttu-id="a7bb8-133">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a7bb8-133">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
   "documents": [
      {
         "keyPhrases": [
            "HDR resolution",
            "new XBox",
            "clean look"
         ],
         "id": "1"
      },
      {
         "keyPhrases": [
            "Carlos",
            "notificacion",
            "algun problema",
            "telefono movil"
         ],
         "id": "2"
      },
      {
         "keyPhrases": [
            "new hotel",
            "Grand Hotel",
            "review",
            "center of Seattle",
            "classiest decor",
            "stars"
         ],
         "id": "3"
      }
   ],
   "errors": [  ]
}
```

<a name="Entities"></a>

## <a name="identify-linked-entities-request"></a><span data-ttu-id="a7bb8-134">Identify linked entities request</span><span class="sxs-lookup"><span data-stu-id="a7bb8-134">Identify linked entities request</span></span>

<span data-ttu-id="a7bb8-135">The Entity Linking API identifies well-known entities in a text document, using the [Entity Linking method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634).</span><span class="sxs-lookup"><span data-stu-id="a7bb8-135">The Entity Linking API identifies well-known entities in a text document, using the [Entity Linking method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634).</span></span> <span data-ttu-id="a7bb8-136">The following example identifies entities for English documents.</span><span class="sxs-lookup"><span data-stu-id="a7bb8-136">The following example identifies entities for English documents.</span></span>

<span data-ttu-id="a7bb8-137">Add the following code to the code from the [previous section](#KeyPhraseExtraction).</span><span class="sxs-lookup"><span data-stu-id="a7bb8-137">Add the following code to the code from the [previous section](#KeyPhraseExtraction).</span></span>

```golang
    // Detect linked entities.
    fmt.Println("===== DETECT LINKED ENTITIES ======")

    uri = uriBase + uriPath + "entities"

    data = []map[string]string{
        {"id": "1", "language": "en", "text": "I really enjoy the new XBox One S. It has a clean look, it has 4K/HDR resolution and it is affordable."},
        {"id": "2", "language": "en", "text": "The Seattle Seahawks won the Super Bowl in 2014."},
    }

    documents, err = json.Marshal(&data)
    if err != nil {
        fmt.Printf("Error marshaling data: %v\n", err)
        return
    }

    r = strings.NewReader("{\"documents\": " + string(documents) + "}")

    client = &http.Client{
        Timeout: time.Second * 2,
    }

    req, err = http.NewRequest("POST", uri, r)
    if err != nil {
        fmt.Printf("Error creating request: %v\n", err)
        return
    }

    req.Header.Add("Content-Type", "application/json")
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)

    resp, err = client.Do(req)
    if err != nil {
        fmt.Printf("Error on request: %v\n", err)
        return
    }
    defer resp.Body.Close()

    body, err = ioutil.ReadAll(resp.Body)
    if err != nil {
        fmt.Printf("Error reading response body: %v\n", err)
        return
    }

    json.Unmarshal(body, &f)

    jsonFormatted, err = json.MarshalIndent(f, "", "  ")
    if err != nil {
        fmt.Printf("Error producing JSON: %v\n", err)
        return
    }
    fmt.Println(string(jsonFormatted))
}
```

## <a name="identify-linked-entities-response"></a><span data-ttu-id="a7bb8-138">Identify linked entities response</span><span class="sxs-lookup"><span data-stu-id="a7bb8-138">Identify linked entities response</span></span>

<span data-ttu-id="a7bb8-139">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a7bb8-139">A successful response is returned in JSON, as shown in the following example:</span></span>

```json
{
    "documents": [
        {
            "id": "1",
            "entities": [
                {
                    "name": "Xbox One",
                    "matches": [
                        {
                            "text": "XBox One",
                            "offset": 23,
                            "length": 8
                        }
                    ],
                    "wikipediaLanguage": "en",
                    "wikipediaId": "Xbox One",
                    "wikipediaUrl": "https://en.wikipedia.org/wiki/Xbox_One",
                    "bingId": "446bb4df-4999-4243-84c0-74e0f6c60e75"
                },
                {
                    "name": "4K resolution",
                    "matches": [
                        {
                            "text": "4K",
                            "offset": 63,
                            "length": 2
                        }
                    ],
                    "wikipediaLanguage": "en",
                    "wikipediaId": "4K resolution",
                    "wikipediaUrl": "https://en.wikipedia.org/wiki/4K_resolution",
                    "bingId": "1d4d689e-9cbf-b9eb-6ecf-f3296aaa96d8"
                }
            ]
        },
        {
            "id": "2",
            "entities": [
                {
                    "name": "Seattle Seahawks",
                    "matches": [
                        {
                            "text": "Seattle Seahawks",
                            "offset": 4,
                            "length": 16
                        }
                    ],
                    "wikipediaLanguage": "en",
                    "wikipediaId": "Seattle Seahawks",
                    "wikipediaUrl": "https://en.wikipedia.org/wiki/Seattle_Seahawks",
                    "bingId": "1bf844db-8225-f90c-a78e-1787fb8af0ce"
                },
                {
                    "name": "Super Bowl",
                    "matches": [
                        {
                            "text": "Super Bowl",
                            "offset": 29,
                            "length": 10
                        }
                    ],
                    "wikipediaLanguage": "en",
                    "wikipediaId": "Super Bowl",
                    "wikipediaUrl": "https://en.wikipedia.org/wiki/Super_Bowl",
                    "bingId": "ce1fece8-34c4-6249-a1aa-2e779294760e"
                }
            ]
        }
    ],
    "errors": []
}
```

## <a name="next-steps"></a><span data-ttu-id="a7bb8-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="a7bb8-140">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a7bb8-141">Text Analytics With Power BI</span><span class="sxs-lookup"><span data-stu-id="a7bb8-141">Text Analytics With Power BI</span></span>](../tutorials/tutorial-power-bi-key-phrases.md)

## <a name="see-also"></a><span data-ttu-id="a7bb8-142">See also</span><span class="sxs-lookup"><span data-stu-id="a7bb8-142">See also</span></span>

 [<span data-ttu-id="a7bb8-143">Text Analytics overview</span><span class="sxs-lookup"><span data-stu-id="a7bb8-143">Text Analytics overview</span></span>](../overview.md)  
 [<span data-ttu-id="a7bb8-144">Frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="a7bb8-144">Frequently asked questions (FAQ)</span></span>](../text-analytics-resource-faq.md)
