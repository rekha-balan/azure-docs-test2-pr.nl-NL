---
title: Translator Text get supported languages with Go | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API with Go in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/29/2018
ms.author: nolachar
ms.openlocfilehash: 91ba39f072d97a87250a2d6284df8571905c1b0f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868627"
---
# <a name="quickstart-get-supported-languages-with-go"></a><span data-ttu-id="f0b28-103">Quickstart: Get supported languages with Go</span><span class="sxs-lookup"><span data-stu-id="f0b28-103">Quickstart: Get supported languages with Go</span></span>

<span data-ttu-id="f0b28-104">In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="f0b28-104">In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0b28-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f0b28-105">Prerequisites</span></span>

<span data-ttu-id="f0b28-106">You'll need to install the [Go distribution](https://golang.org/doc/install) in order to run this code.</span><span class="sxs-lookup"><span data-stu-id="f0b28-106">You'll need to install the [Go distribution](https://golang.org/doc/install) in order to run this code.</span></span> <span data-ttu-id="f0b28-107">The sample code uses only **core** libraries, so there are no external dependencies.</span><span class="sxs-lookup"><span data-stu-id="f0b28-107">The sample code uses only **core** libraries, so there are no external dependencies.</span></span>

<span data-ttu-id="f0b28-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="f0b28-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="languages-request"></a><span data-ttu-id="f0b28-109">Languages request</span><span class="sxs-lookup"><span data-stu-id="f0b28-109">Languages request</span></span>

<span data-ttu-id="f0b28-110">The following code gets a list of supported languages for translation, transliteration, and dictionary lookup and examples, using the [Languages](./reference/v3-0-languages.md) method.</span><span class="sxs-lookup"><span data-stu-id="f0b28-110">The following code gets a list of supported languages for translation, transliteration, and dictionary lookup and examples, using the [Languages](./reference/v3-0-languages.md) method.</span></span>

1. <span data-ttu-id="f0b28-111">Create a new Go project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="f0b28-111">Create a new Go project in your favorite code editor.</span></span>
2. <span data-ttu-id="f0b28-112">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="f0b28-112">Add the code provided below.</span></span>
3. <span data-ttu-id="f0b28-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="f0b28-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="f0b28-114">Save the file with a '.go' extension.</span><span class="sxs-lookup"><span data-stu-id="f0b28-114">Save the file with a '.go' extension.</span></span>
5. <span data-ttu-id="f0b28-115">Open a command prompt on a computer with Go installed.</span><span class="sxs-lookup"><span data-stu-id="f0b28-115">Open a command prompt on a computer with Go installed.</span></span>
6. <span data-ttu-id="f0b28-116">Build the file, for example: 'go build quickstart-languages.go'.</span><span class="sxs-lookup"><span data-stu-id="f0b28-116">Build the file, for example: 'go build quickstart-languages.go'.</span></span>
7. <span data-ttu-id="f0b28-117">Run the file, for example: 'quickstart-languages'.</span><span class="sxs-lookup"><span data-stu-id="f0b28-117">Run the file, for example: 'quickstart-languages'.</span></span>

```golang
package main

import (
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
    "time"
)

func main() {
    // Replace the subscriptionKey string value with your valid subscription key
    const subscriptionKey = "<Subscription Key>"

    const uriBase = "https://api.cognitive.microsofttranslator.com"
    const uriPath = "/languages?api-version=3.0"

    const uri = uriBase + uriPath

    client := &http.Client{
        Timeout: time.Second * 2,
    }

    req, err := http.NewRequest("GET", uri, nil)
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
}
```

## <a name="languages-response"></a><span data-ttu-id="f0b28-118">Languages response</span><span class="sxs-lookup"><span data-stu-id="f0b28-118">Languages response</span></span>

<span data-ttu-id="f0b28-119">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f0b28-119">A successful response is returned in JSON as shown in the following example:</span></span>

```json
{
  "dictionary": {
    "af": {
      "name": "Afrikaans",
      "nativeName": "Afrikaans",
      "dir": "ltr",
      "translations": [
        {
          "name": "English",
          "nativeName": "English",
          "dir": "ltr",
          "code": "en"
        }
      ]
    },
    "ar": {
      "name": "Arabic",
      "nativeName": "العربية",
      "dir": "rtl",
      "translations": [
        {
          "name": "English",
          "nativeName": "English",
          "dir": "ltr",
          "code": "en"
        }
      ]
    },
...
  },
  "translation": {
    "af": {
      "name": "Afrikaans",
      "nativeName": "Afrikaans",
      "dir": "ltr"
    },
    "ar": {
      "name": "Arabic",
      "nativeName": "العربية",
      "dir": "rtl"
    },
...
  },
  "transliteration": {
    "ar": {
      "name": "Arabic",
      "nativeName": "العربية",
      "scripts": [
        {
          "code": "Arab",
          "name": "Arabic",
          "nativeName": "العربية",
          "dir": "rtl",
          "toScripts": [
            {
              "code": "Latn",
              "name": "Latin",
              "nativeName": "اللاتينية",
              "dir": "ltr"
            }
          ]
        },
        {
          "code": "Latn",
          "name": "Latin",
          "nativeName": "اللاتينية",
          "dir": "ltr",
          "toScripts": [
            {
              "code": "Arab",
              "name": "Arabic",
              "nativeName": "العربية",
              "dir": "rtl"
            }
          ]
        }
      ]
    },
...
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="f0b28-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="f0b28-120">Next steps</span></span>

<span data-ttu-id="f0b28-121">Explore Go packages for Cognitive Services APIs from the [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="f0b28-121">Explore Go packages for Cognitive Services APIs from the [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f0b28-122">Explore Go packages on GitHub</span><span class="sxs-lookup"><span data-stu-id="f0b28-122">Explore Go packages on GitHub</span></span>](https://github.com/Azure/azure-sdk-for-go/tree/master/services/cognitiveservices)
