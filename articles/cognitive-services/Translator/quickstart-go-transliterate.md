---
title: Translator Text convert text script with Go | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you convert text in one language from one script to another using the Translator Text API with Go in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/29/2018
ms.author: nolachar
ms.openlocfilehash: f01fe38ef0605ad399edc03b52dc5b8ecc75275b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871213"
---
# <a name="quickstart-transliterate-text-with-go"></a><span data-ttu-id="2eb1d-103">Quickstart: Transliterate text with Go</span><span class="sxs-lookup"><span data-stu-id="2eb1d-103">Quickstart: Transliterate text with Go</span></span>

<span data-ttu-id="2eb1d-104">In this quickstart, you convert text in one language from one script to another using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="2eb1d-104">In this quickstart, you convert text in one language from one script to another using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2eb1d-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2eb1d-105">Prerequisites</span></span>

<span data-ttu-id="2eb1d-106">You'll need to install the [Go distribution](https://golang.org/doc/install) in order to run this code.</span><span class="sxs-lookup"><span data-stu-id="2eb1d-106">You'll need to install the [Go distribution](https://golang.org/doc/install) in order to run this code.</span></span> <span data-ttu-id="2eb1d-107">The sample code uses only **core** libraries, so there are no external dependencies.</span><span class="sxs-lookup"><span data-stu-id="2eb1d-107">The sample code uses only **core** libraries, so there are no external dependencies.</span></span>

<span data-ttu-id="2eb1d-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="2eb1d-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="transliterate-request"></a><span data-ttu-id="2eb1d-109">Transliterate request</span><span class="sxs-lookup"><span data-stu-id="2eb1d-109">Transliterate request</span></span>

<span data-ttu-id="2eb1d-110">The following converts text in one language from one script to another script using the [Transliterate](./reference/v3-0-transliterate.md) method.</span><span class="sxs-lookup"><span data-stu-id="2eb1d-110">The following converts text in one language from one script to another script using the [Transliterate](./reference/v3-0-transliterate.md) method.</span></span>

1. <span data-ttu-id="2eb1d-111">Create a new Go project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="2eb1d-111">Create a new Go project in your favorite code editor.</span></span>
2. <span data-ttu-id="2eb1d-112">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="2eb1d-112">Add the code provided below.</span></span>
3. <span data-ttu-id="2eb1d-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="2eb1d-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="2eb1d-114">Save the file with a '.go' extension.</span><span class="sxs-lookup"><span data-stu-id="2eb1d-114">Save the file with a '.go' extension.</span></span>
5. <span data-ttu-id="2eb1d-115">Open a command prompt on a computer with Go installed.</span><span class="sxs-lookup"><span data-stu-id="2eb1d-115">Open a command prompt on a computer with Go installed.</span></span>
6. <span data-ttu-id="2eb1d-116">Build the file, for example: 'go build quickstart-transliterate.go'.</span><span class="sxs-lookup"><span data-stu-id="2eb1d-116">Build the file, for example: 'go build quickstart-transliterate.go'.</span></span>
7. <span data-ttu-id="2eb1d-117">Run the file, for example: 'quickstart-transliterate'.</span><span class="sxs-lookup"><span data-stu-id="2eb1d-117">Run the file, for example: 'quickstart-transliterate'.</span></span>

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
    const uriPath = "/transliterate?api-version=3.0"

    // Transliterate text in Japanese from Japanese script (i.e. Hiragana/Katakana/Kanji) to Latin script
    const params = "&language=ja&fromScript=jpan&toScript=latn"

    const uri = uriBase + uriPath + params

    // Transliterate "good afternoon".
    const text = "こんにちは"

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

## <a name="transliterate-response"></a><span data-ttu-id="2eb1d-118">Transliterate response</span><span class="sxs-lookup"><span data-stu-id="2eb1d-118">Transliterate response</span></span>

<span data-ttu-id="2eb1d-119">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="2eb1d-119">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "script": "latn",
    "text": "konnnichiha"
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="2eb1d-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="2eb1d-120">Next steps</span></span>

<span data-ttu-id="2eb1d-121">Explore Go packages for Cognitive Services APIs from the [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="2eb1d-121">Explore Go packages for Cognitive Services APIs from the [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2eb1d-122">Explore Go packages on GitHub</span><span class="sxs-lookup"><span data-stu-id="2eb1d-122">Explore Go packages on GitHub</span></span>](https://github.com/Azure/azure-sdk-for-go/tree/master/services/cognitiveservices)
