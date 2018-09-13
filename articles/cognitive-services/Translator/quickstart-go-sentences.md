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
# <a name="quickstart-get-sentence-lengths-with-go"></a>Quickstart: Get sentence lengths with Go

In this quickstart, you find the lengths of sentences in text using the Translator Text API.

## <a name="prerequisites"></a>Prerequisites

You'll need to install the [Go distribution](https://golang.org/doc/install) in order to run this code. The sample code uses only **core** libraries, so there are no external dependencies.

To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).

## <a name="breaksentence-request"></a>BreakSentence request

The following code breaks the source text into sentences using the [BreakSentence](./reference/v3-0-break-sentence.md) method.

1. Create a new Go project in your favorite code editor.
2. Add the code provided below.
3. Replace the `subscriptionKey` value with an access key valid for your subscription.
4. Save the file with a '.go' extension.
5. Open a command prompt on a computer with Go installed.
6. Build the file, for example: 'go build quickstart-sentences.go'.
7. Run the file, for example: 'quickstart-sentences'.

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

## <a name="breaksentence-response"></a>BreakSentence response

A successful response is returned in JSON as shown in the following example:

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

## <a name="next-steps"></a>Next steps

Explore Go packages for Cognitive Services APIs from the [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) on GitHub.

> [!div class="nextstepaction"]
> [Explore Go packages on GitHub](https://github.com/Azure/azure-sdk-for-go/tree/master/services/cognitiveservices)
