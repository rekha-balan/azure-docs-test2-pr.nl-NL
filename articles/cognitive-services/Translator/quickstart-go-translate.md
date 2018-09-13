---
title: Translator Text translate text with Go | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you translate text from one language to another using the Translator Text API with Go in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/29/2018
ms.author: nolachar
ms.openlocfilehash: 72d4a3bc7563d6427335f1536f787eab6d7a0de4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966320"
---
# <a name="quickstart-translate-text-with-go"></a><span data-ttu-id="13251-103">Quickstart: Translate text with Go</span><span class="sxs-lookup"><span data-stu-id="13251-103">Quickstart: Translate text with Go</span></span>

<span data-ttu-id="13251-104">In this quickstart, you translate text from one language to another using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="13251-104">In this quickstart, you translate text from one language to another using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13251-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="13251-105">Prerequisites</span></span>

<span data-ttu-id="13251-106">You'll need to install the [Go distribution](https://golang.org/doc/install) in order to run this code.</span><span class="sxs-lookup"><span data-stu-id="13251-106">You'll need to install the [Go distribution](https://golang.org/doc/install) in order to run this code.</span></span> <span data-ttu-id="13251-107">The sample code uses only **core** libraries, so there are no external dependencies.</span><span class="sxs-lookup"><span data-stu-id="13251-107">The sample code uses only **core** libraries, so there are no external dependencies.</span></span>

<span data-ttu-id="13251-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="13251-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="translate-request"></a><span data-ttu-id="13251-109">Translate request</span><span class="sxs-lookup"><span data-stu-id="13251-109">Translate request</span></span>

<span data-ttu-id="13251-110">The following code translates source text from one language to another using the [Translate](./reference/v3-0-translate.md) method.</span><span class="sxs-lookup"><span data-stu-id="13251-110">The following code translates source text from one language to another using the [Translate](./reference/v3-0-translate.md) method.</span></span>

1. <span data-ttu-id="13251-111">Create a new Go project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="13251-111">Create a new Go project in your favorite code editor.</span></span>
2. <span data-ttu-id="13251-112">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="13251-112">Add the code provided below.</span></span>
3. <span data-ttu-id="13251-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="13251-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="13251-114">Save the file with a '.go' extension.</span><span class="sxs-lookup"><span data-stu-id="13251-114">Save the file with a '.go' extension.</span></span>
5. <span data-ttu-id="13251-115">Open a command prompt on a computer with Go installed.</span><span class="sxs-lookup"><span data-stu-id="13251-115">Open a command prompt on a computer with Go installed.</span></span>
6. <span data-ttu-id="13251-116">Build the file, for example: 'go build quickstart-translate.go'.</span><span class="sxs-lookup"><span data-stu-id="13251-116">Build the file, for example: 'go build quickstart-translate.go'.</span></span>
7. <span data-ttu-id="13251-117">Run the file, for example: 'quickstart-translate'.</span><span class="sxs-lookup"><span data-stu-id="13251-117">Run the file, for example: 'quickstart-translate'.</span></span>

```golang
package translate

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
    const uriPath = "/translate?api-version=3.0"

    // Translate to German and Italian
    const params = "&to=de&to=it"

    const uri = uriBase + uriPath + params

    const text = "Hello, world!"

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

## <a name="translate-response"></a><span data-ttu-id="13251-118">Translate response</span><span class="sxs-lookup"><span data-stu-id="13251-118">Translate response</span></span>

<span data-ttu-id="13251-119">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="13251-119">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "detectedLanguage": {
      "language": "en",
      "score": 1.0
    },
    "translations": [
      {
        "text": "Hallo Welt!",
        "to": "de"
      },
      {
        "text": "Salve, mondo!",
        "to": "it"
      }
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="13251-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="13251-120">Next steps</span></span>

<span data-ttu-id="13251-121">Explore Go packages for Cognitive Services APIs from the [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="13251-121">Explore Go packages for Cognitive Services APIs from the [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="13251-122">Explore Go packages on GitHub</span><span class="sxs-lookup"><span data-stu-id="13251-122">Explore Go packages on GitHub</span></span>](https://github.com/Azure/azure-sdk-for-go/tree/master/services/cognitiveservices)
