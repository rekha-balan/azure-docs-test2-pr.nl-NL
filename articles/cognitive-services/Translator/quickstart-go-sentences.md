---
title: Translator Text get sentence lengths with Go | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you find the lengths of sentences in text using the Translator Text API with Go in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/29/2018
ms.author: nolachar
ms.openlocfilehash: 441f7c9ced91899896b63f4925f1ec204a9f52fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968791"
---
# <a name="quickstart-get-sentence-lengths-with-go"></a><span data-ttu-id="fcf22-103">Quickstart: Get sentence lengths with Go</span><span class="sxs-lookup"><span data-stu-id="fcf22-103">Quickstart: Get sentence lengths with Go</span></span>

<span data-ttu-id="fcf22-104">In this quickstart, you find the lengths of sentences in text using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="fcf22-104">In this quickstart, you find the lengths of sentences in text using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcf22-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fcf22-105">Prerequisites</span></span>

<span data-ttu-id="fcf22-106">You'll need to install the [Go distribution](https://golang.org/doc/install) in order to run this code.</span><span class="sxs-lookup"><span data-stu-id="fcf22-106">You'll need to install the [Go distribution](https://golang.org/doc/install) in order to run this code.</span></span> <span data-ttu-id="fcf22-107">The sample code uses only **core** libraries, so there are no external dependencies.</span><span class="sxs-lookup"><span data-stu-id="fcf22-107">The sample code uses only **core** libraries, so there are no external dependencies.</span></span>

<span data-ttu-id="fcf22-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="fcf22-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="breaksentence-request"></a><span data-ttu-id="fcf22-109">BreakSentence request</span><span class="sxs-lookup"><span data-stu-id="fcf22-109">BreakSentence request</span></span>

<span data-ttu-id="fcf22-110">The following code breaks the source text into sentences using the [BreakSentence](./reference/v3-0-break-sentence.md) method.</span><span class="sxs-lookup"><span data-stu-id="fcf22-110">The following code breaks the source text into sentences using the [BreakSentence](./reference/v3-0-break-sentence.md) method.</span></span>

1. <span data-ttu-id="fcf22-111">Create a new Go project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="fcf22-111">Create a new Go project in your favorite code editor.</span></span>
2. <span data-ttu-id="fcf22-112">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="fcf22-112">Add the code provided below.</span></span>
3. <span data-ttu-id="fcf22-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="fcf22-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="fcf22-114">Save the file with a '.go' extension.</span><span class="sxs-lookup"><span data-stu-id="fcf22-114">Save the file with a '.go' extension.</span></span>
5. <span data-ttu-id="fcf22-115">Open a command prompt on a computer with Go installed.</span><span class="sxs-lookup"><span data-stu-id="fcf22-115">Open a command prompt on a computer with Go installed.</span></span>
6. <span data-ttu-id="fcf22-116">Build the file, for example: 'go build quickstart-sentences.go'.</span><span class="sxs-lookup"><span data-stu-id="fcf22-116">Build the file, for example: 'go build quickstart-sentences.go'.</span></span>
7. <span data-ttu-id="fcf22-117">Run the file, for example: 'quickstart-sentences'.</span><span class="sxs-lookup"><span data-stu-id="fcf22-117">Run the file, for example: 'quickstart-sentences'.</span></span>

```golang
package main

import (
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
    "strconv"
    "strings"
    "time"
)

func main() {
    // Replace the subscriptionKey string value with your valid subscription key
    const subscriptionKey = "<Subscription Key>"

    const uriBase = "https://api.cognitive.microsofttranslator.com"
    const uriPath = "/breaksentence?api-version=3.0"

    const uri = uriBase + uriPath

    const text = "How are you? I am fine. What did you do today?"

    r := strings.NewReader("[{\"Text\" : \"" + text + "\"}]")

    client := &http.Client{
        Timeout: time.Second * 2,
    }

    req, err := http.NewRequest("POST", uri, r)
    if err != nil {
        fmt.Printf("Error creating request: %v\n", err)
        return
    }

    req.Header.Add("Content-Type", "application/json")
    req.Header.Add("Content-Length", strconv.FormatInt(req.ContentLength, 10))
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
}
```

## <a name="breaksentence-response"></a><span data-ttu-id="fcf22-118">BreakSentence response</span><span class="sxs-lookup"><span data-stu-id="fcf22-118">BreakSentence response</span></span>

<span data-ttu-id="fcf22-119">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="fcf22-119">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "detectedLanguage": {
      "language": "en",
      "score": 1.0
    },
    "sentLen": [
      13,
      11,
      22
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="fcf22-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="fcf22-120">Next steps</span></span>

<span data-ttu-id="fcf22-121">Explore Go packages for Cognitive Services APIs from the [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="fcf22-121">Explore Go packages for Cognitive Services APIs from the [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fcf22-122">Explore Go packages on GitHub</span><span class="sxs-lookup"><span data-stu-id="fcf22-122">Explore Go packages on GitHub</span></span>](https://github.com/Azure/azure-sdk-for-go/tree/master/services/cognitiveservices)
