---
title: Translator Text find alternate translations with Go | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you find alternate translations and examples of terms in context using the Translator Text API with Go in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/29/2018
ms.author: nolachar
ms.openlocfilehash: a076418dbf969a61107c28f191457fc336a8b907
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969254"
---
# <a name="quickstart-find-alternate-translations-and-usage-with-go"></a><span data-ttu-id="37dd5-103">Quickstart: Find alternate translations and usage with Go</span><span class="sxs-lookup"><span data-stu-id="37dd5-103">Quickstart: Find alternate translations and usage with Go</span></span>

<span data-ttu-id="37dd5-104">In this quickstart, you find details of possible alternate translations for a term, and also usage examples of those alternate translations, using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="37dd5-104">In this quickstart, you find details of possible alternate translations for a term, and also usage examples of those alternate translations, using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37dd5-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="37dd5-105">Prerequisites</span></span>

<span data-ttu-id="37dd5-106">You'll need to install the [Go distribution](https://golang.org/doc/install) in order to run this code.</span><span class="sxs-lookup"><span data-stu-id="37dd5-106">You'll need to install the [Go distribution](https://golang.org/doc/install) in order to run this code.</span></span> <span data-ttu-id="37dd5-107">The sample code uses only **core** libraries, so there are no external dependencies.</span><span class="sxs-lookup"><span data-stu-id="37dd5-107">The sample code uses only **core** libraries, so there are no external dependencies.</span></span>

<span data-ttu-id="37dd5-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="37dd5-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="dictionary-lookup-request"></a><span data-ttu-id="37dd5-109">Dictionary Lookup request</span><span class="sxs-lookup"><span data-stu-id="37dd5-109">Dictionary Lookup request</span></span>

<span data-ttu-id="37dd5-110">The following gets alternate translations for a word using the [Dictionary Lookup](./reference/v3-0-dictionary-lookup.md) method.</span><span class="sxs-lookup"><span data-stu-id="37dd5-110">The following gets alternate translations for a word using the [Dictionary Lookup](./reference/v3-0-dictionary-lookup.md) method.</span></span>

1. <span data-ttu-id="37dd5-111">Create a new Go project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="37dd5-111">Create a new Go project in your favorite code editor.</span></span>
2. <span data-ttu-id="37dd5-112">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="37dd5-112">Add the code provided below.</span></span>
3. <span data-ttu-id="37dd5-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="37dd5-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="37dd5-114">Save the file with a '.go' extension.</span><span class="sxs-lookup"><span data-stu-id="37dd5-114">Save the file with a '.go' extension.</span></span>
5. <span data-ttu-id="37dd5-115">Open a command prompt on a computer with Go installed.</span><span class="sxs-lookup"><span data-stu-id="37dd5-115">Open a command prompt on a computer with Go installed.</span></span>
6. <span data-ttu-id="37dd5-116">Build the file, for example: 'go build quickstart-lookup.go'.</span><span class="sxs-lookup"><span data-stu-id="37dd5-116">Build the file, for example: 'go build quickstart-lookup.go'.</span></span>
7. <span data-ttu-id="37dd5-117">Run the file, for example: 'quickstart-lookup'.</span><span class="sxs-lookup"><span data-stu-id="37dd5-117">Run the file, for example: 'quickstart-lookup'.</span></span>

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
    const uriPath = "/dictionary/lookup?api-version=3.0"

    // From English to French
    const params = "&from=en&to=fr"

    const uri = uriBase + uriPath + params

    const text = "great"

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

## <a name="dictionary-lookup-response"></a><span data-ttu-id="37dd5-118">Dictionary Lookup response</span><span class="sxs-lookup"><span data-stu-id="37dd5-118">Dictionary Lookup response</span></span>

<span data-ttu-id="37dd5-119">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="37dd5-119">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "normalizedSource": "great",
    "displaySource": "great",
    "translations": [
      {
        "normalizedTarget": "grand",
        "displayTarget": "grand",
        "posTag": "ADJ",
        "confidence": 0.2783,
        "prefixWord": "",
        "backTranslations": [
          {
            "normalizedText": "great",
            "displayText": "great",
            "numExamples": 15,
            "frequencyCount": 34358
          },
          {
            "normalizedText": "big",
            "displayText": "big",
            "numExamples": 15,
            "frequencyCount": 21770
          },
...
        ]
      },
      {
        "normalizedTarget": "super",
        "displayTarget": "super",
        "posTag": "ADJ",
        "confidence": 0.1514,
        "prefixWord": "",
        "backTranslations": [
          {
            "normalizedText": "super",
            "displayText": "super",
            "numExamples": 15,
            "frequencyCount": 12023
          },
          {
            "normalizedText": "great",
            "displayText": "great",
            "numExamples": 15,
            "frequencyCount": 10931
          },
...
        ]
      },
...
    ]
  }
]
```

## <a name="dictionary-examples-request"></a><span data-ttu-id="37dd5-120">Dictionary Examples request</span><span class="sxs-lookup"><span data-stu-id="37dd5-120">Dictionary Examples request</span></span>

<span data-ttu-id="37dd5-121">The following gets contextual examples of how to use a term in the dictionary using the [Dictionary Examples](./reference/v3-0-dictionary-examples.md) method.</span><span class="sxs-lookup"><span data-stu-id="37dd5-121">The following gets contextual examples of how to use a term in the dictionary using the [Dictionary Examples](./reference/v3-0-dictionary-examples.md) method.</span></span>

1. <span data-ttu-id="37dd5-122">Create a new Go project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="37dd5-122">Create a new Go project in your favorite code editor.</span></span>
2. <span data-ttu-id="37dd5-123">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="37dd5-123">Add the code provided below.</span></span>
3. <span data-ttu-id="37dd5-124">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="37dd5-124">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="37dd5-125">Save the file with a '.go' extension.</span><span class="sxs-lookup"><span data-stu-id="37dd5-125">Save the file with a '.go' extension.</span></span>
5. <span data-ttu-id="37dd5-126">Open a command prompt on a computer with Go installed.</span><span class="sxs-lookup"><span data-stu-id="37dd5-126">Open a command prompt on a computer with Go installed.</span></span>
6. <span data-ttu-id="37dd5-127">Build the file, for example: 'go build quickstart-examples.go'.</span><span class="sxs-lookup"><span data-stu-id="37dd5-127">Build the file, for example: 'go build quickstart-examples.go'.</span></span>
7. <span data-ttu-id="37dd5-128">Run the file, for example: 'quickstart-examples'.</span><span class="sxs-lookup"><span data-stu-id="37dd5-128">Run the file, for example: 'quickstart-examples'.</span></span>

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
    const uriPath = "/dictionary/examples?api-version=3.0"

    // From English to French
    const params = "&from=en&to=fr"

    const uri = uriBase + uriPath + params

    const text = "great"
    const translation = "formidable"

    r := strings.NewReader("[{\"Text\" : \"" + text + "\", \"Translation\" : \"" + translation + "\"}]")

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

## <a name="dictionary-examples-response"></a><span data-ttu-id="37dd5-129">Dictionary Examples response</span><span class="sxs-lookup"><span data-stu-id="37dd5-129">Dictionary Examples response</span></span>

<span data-ttu-id="37dd5-130">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="37dd5-130">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "normalizedSource": "great",
    "normalizedTarget": "formidable",
    "examples": [
      {
        "sourcePrefix": "You have a ",
        "sourceTerm": "great",
        "sourceSuffix": " expression there.",
        "targetPrefix": "Vous avez une expression ",
        "targetTerm": "formidable",
        "targetSuffix": "."
      },
      {
        "sourcePrefix": "You played a ",
        "sourceTerm": "great",
        "sourceSuffix": " game today.",
        "targetPrefix": "Vous avez été ",
        "targetTerm": "formidable",
        "targetSuffix": "."
      },
...
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="37dd5-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="37dd5-131">Next steps</span></span>

<span data-ttu-id="37dd5-132">Explore Go packages for Cognitive Services APIs from the [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="37dd5-132">Explore Go packages for Cognitive Services APIs from the [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="37dd5-133">Explore Go packages on GitHub</span><span class="sxs-lookup"><span data-stu-id="37dd5-133">Explore Go packages on GitHub</span></span>](https://github.com/Azure/azure-sdk-for-go/tree/master/services/cognitiveservices)
