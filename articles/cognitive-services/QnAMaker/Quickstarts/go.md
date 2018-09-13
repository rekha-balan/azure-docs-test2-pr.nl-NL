---
title: 'Quickstart: Go for QnA Maker API (V4)'
titleSuffix: Azure Cognitive Services
description: Get information and code samples to help you quickly get started using the Microsoft Translator Text API in Microsoft Cognitive Services on Azure.
services: cognitive-services
author: nitinme
manager: cgronlun
ms.service: cognitive-services
ms.technology: qna-maker
ms.topic: article
ms.date: 05/07/2018
ms.author: v-jaswel
ms.openlocfilehash: 5daf4d5e971e840db020e35d1997615723f8e06d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855655"
---
# <a name="quickstart-for-microsoft-qna-maker-api-with-go"></a><span data-ttu-id="1b14e-103">Quickstart for Microsoft QnA Maker API with Go</span><span class="sxs-lookup"><span data-stu-id="1b14e-103">Quickstart for Microsoft QnA Maker API with Go</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="1b14e-104">This article shows you how to use the [Microsoft QnA Maker API](../Overview/overview.md) with Go to do the following.</span><span class="sxs-lookup"><span data-stu-id="1b14e-104">This article shows you how to use the [Microsoft QnA Maker API](../Overview/overview.md) with Go to do the following.</span></span>

- [<span data-ttu-id="1b14e-105">Create a new knowledge base.</span><span class="sxs-lookup"><span data-stu-id="1b14e-105">Create a new knowledge base.</span></span>](#Create)
- [<span data-ttu-id="1b14e-106">Update an existing knowledge base.</span><span class="sxs-lookup"><span data-stu-id="1b14e-106">Update an existing knowledge base.</span></span>](#Update)
- [<span data-ttu-id="1b14e-107">Get the status of a request to create or update a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="1b14e-107">Get the status of a request to create or update a knowledge base.</span></span>](#Status)
- [<span data-ttu-id="1b14e-108">Publish an existing knowledge base.</span><span class="sxs-lookup"><span data-stu-id="1b14e-108">Publish an existing knowledge base.</span></span>](#Publish)
- [<span data-ttu-id="1b14e-109">Replace the contents of an existing knowledge base.</span><span class="sxs-lookup"><span data-stu-id="1b14e-109">Replace the contents of an existing knowledge base.</span></span>](#Replace)
- [<span data-ttu-id="1b14e-110">Download the contents of a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="1b14e-110">Download the contents of a knowledge base.</span></span>](#GetQnA)
- [<span data-ttu-id="1b14e-111">Get answers to a question using a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="1b14e-111">Get answers to a question using a knowledge base.</span></span>](#GetAnswers)
- [<span data-ttu-id="1b14e-112">Get information about a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="1b14e-112">Get information about a knowledge base.</span></span>](#GetKB)
- [<span data-ttu-id="1b14e-113">Get information about all knowledge bases belonging to the specified user.</span><span class="sxs-lookup"><span data-stu-id="1b14e-113">Get information about all knowledge bases belonging to the specified user.</span></span>](#GetKBsByUser)
- [<span data-ttu-id="1b14e-114">Delete a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="1b14e-114">Delete a knowledge base.</span></span>](#Delete)
- [<span data-ttu-id="1b14e-115">Get the current endpoint keys.</span><span class="sxs-lookup"><span data-stu-id="1b14e-115">Get the current endpoint keys.</span></span>](#GetKeys)
- [<span data-ttu-id="1b14e-116">Re-generate the current endpoint keys.</span><span class="sxs-lookup"><span data-stu-id="1b14e-116">Re-generate the current endpoint keys.</span></span>](#PutKeys)
- [<span data-ttu-id="1b14e-117">Get the current set of word alterations.</span><span class="sxs-lookup"><span data-stu-id="1b14e-117">Get the current set of word alterations.</span></span>](#GetAlterations)
- [<span data-ttu-id="1b14e-118">Replace the current set of word alterations.</span><span class="sxs-lookup"><span data-stu-id="1b14e-118">Replace the current set of word alterations.</span></span>](#PutAlterations)

## <a name="prerequisites"></a><span data-ttu-id="1b14e-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1b14e-119">Prerequisites</span></span>

<span data-ttu-id="1b14e-120">You will need [Go 1.10.1](https://golang.org/dl/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="1b14e-120">You will need [Go 1.10.1](https://golang.org/dl/) to run this code.</span></span>

<span data-ttu-id="1b14e-121">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft QnA Maker API**.</span><span class="sxs-lookup"><span data-stu-id="1b14e-121">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft QnA Maker API**.</span></span> <span data-ttu-id="1b14e-122">You will need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span><span class="sxs-lookup"><span data-stu-id="1b14e-122">You will need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span></span>

<a name="Create"></a>

## <a name="create-knowledge-base"></a><span data-ttu-id="1b14e-123">Create knowledge base</span><span class="sxs-lookup"><span data-stu-id="1b14e-123">Create knowledge base</span></span>

<span data-ttu-id="1b14e-124">The following code creates a new knowledge base, using the [Create](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff) method.</span><span class="sxs-lookup"><span data-stu-id="1b14e-124">The following code creates a new knowledge base, using the [Create](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff) method.</span></span>

1. <span data-ttu-id="1b14e-125">Create a new Go project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="1b14e-125">Create a new Go project in your favorite IDE.</span></span>
2. <span data-ttu-id="1b14e-126">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="1b14e-126">Add the code provided below.</span></span>
3. <span data-ttu-id="1b14e-127">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="1b14e-127">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="1b14e-128">Run the program.</span><span class="sxs-lookup"><span data-stu-id="1b14e-128">Run the program.</span></span>

```go
package main

import (
    "bytes"
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
    "strconv"
    "time"
)

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
var subscriptionKey string = "ENTER KEY HERE"

var host string = "https://westus.api.cognitive.microsoft.com"
var service string = "/qnamaker/v4.0"
var method string = "/knowledgebases/create"

type Response struct {
    Headers map[string][]string
    Body    string
}

func pretty_print(content string) string {
    var obj map[string]interface{}
    json.Unmarshal([]byte(content), &obj)
    result, _ := json.MarshalIndent(obj, "", "  ")
    return string(result)
}

func post(uri string, content string) Response {
    req, _ := http.NewRequest("POST", uri, bytes.NewBuffer([]byte(content)))
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)
    req.Header.Add("Content-Type", "application/json")
    req.Header.Add("Content-Length", strconv.Itoa(len(content)))
    client := &http.Client{}
    response, err := client.Do(req)
    if err != nil {
        panic(err)
    }

    defer response.Body.Close()
    body, _ := ioutil.ReadAll(response.Body)

    return Response {response.Header, string(body)}
}

func get(uri string) Response {
    req, _ := http.NewRequest("GET", uri, nil)
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)
    client := &http.Client{}
    response, err := client.Do(req)
    if err != nil {
        panic(err)
    }

    defer response.Body.Close()
    body, _ := ioutil.ReadAll(response.Body)

    return Response {response.Header, string(body)}
}

var req string = `{
  "name": "QnA Maker FAQ",
  "qnaList": [
    {
      "id": 0,
      "answer": "You can use our REST APIs to manage your Knowledge Base. See here for details: https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600",
      "source": "Custom Editorial",
      "questions": [
        "How do I programmatically update my Knowledge Base?"
      ],
      "metadata": [
        {
          "name": "category",
          "value": "api"
        }
      ]
    }
  ],
  "urls": [
    "https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs",
    "https://docs.microsoft.com/en-us/bot-framework/resources-bot-framework-faq"
  ],
  "files": []
}`;

func create_kb(uri string, req string) (string, string) {
    fmt.Println("Calling " + uri + ".")
    result := post(uri, req)
    return result.Headers["Location"][0], result.Body
}

func check_status(uri string) (string, string) {
    fmt.Println("Calling " + uri + ".")
    result := get(uri)
    if retry, success := result.Headers["Retry-After"]; success {
        return retry[0], result.Body
    } else {
// If the response headers did not include a Retry-After value, default to 30 seconds.
        return "30", result.Body
    }
}

func main() {
    var uri = host + service + method
    operation, body := create_kb(uri, req)
    fmt.Printf(body + "\n")
    var done bool = false
    for done == false {
        uri := host + service + operation
        wait, status := check_status(uri)
        fmt.Println(status)
        var status_obj map[string]interface{}
        json.Unmarshal([]byte(status), &status_obj)
        state := status_obj["operationState"]
// If the operation isn't finished, wait and query again.
        if state == "Running" || state == "NotStarted" {
            fmt.Printf ("Waiting " + wait + " seconds...")
            sec, _ := strconv.Atoi(wait)
            time.Sleep (time.Duration(sec) * time.Second)
        } else {
            done = true
        }
    }
}
```

<span data-ttu-id="1b14e-129">**Create knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="1b14e-129">**Create knowledge base response**</span></span>

<span data-ttu-id="1b14e-130">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1b14e-130">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "operationState": "NotStarted",
  "createdTimestamp": "2018-04-13T01:52:30Z",
  "lastActionTimestamp": "2018-04-13T01:52:30Z",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "e88b5b23-e9ab-47fe-87dd-3affc2fb10f3"
}
...
{
  "operationState": "Running",
  "createdTimestamp": "2018-04-13T01:52:30Z",
  "lastActionTimestamp": "2018-04-13T01:52:30Z",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "e88b5b23-e9ab-47fe-87dd-3affc2fb10f3"
}
...
{
  "operationState": "Succeeded",
  "createdTimestamp": "2018-04-13T01:52:30Z",
  "lastActionTimestamp": "2018-04-13T01:52:46Z",
  "resourceLocation": "/knowledgebases/b0288f33-27b9-4258-a304-8b9f63427dad",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "e88b5b23-e9ab-47fe-87dd-3affc2fb10f3"
}
```

[<span data-ttu-id="1b14e-131">Back to top</span><span class="sxs-lookup"><span data-stu-id="1b14e-131">Back to top</span></span>](#HOLTop)

<a name="Update"></a>

## <a name="update-knowledge-base"></a><span data-ttu-id="1b14e-132">Update knowledge base</span><span class="sxs-lookup"><span data-stu-id="1b14e-132">Update knowledge base</span></span>

<span data-ttu-id="1b14e-133">The following code updates an existing knowledge base, using the [Update](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) method.</span><span class="sxs-lookup"><span data-stu-id="1b14e-133">The following code updates an existing knowledge base, using the [Update](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) method.</span></span>

1. <span data-ttu-id="1b14e-134">Create a new Go project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="1b14e-134">Create a new Go project in your favorite IDE.</span></span>
2. <span data-ttu-id="1b14e-135">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="1b14e-135">Add the code provided below.</span></span>
3. <span data-ttu-id="1b14e-136">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="1b14e-136">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="1b14e-137">Run the program.</span><span class="sxs-lookup"><span data-stu-id="1b14e-137">Run the program.</span></span>

```go
package main

import (
    "bytes"
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
    "strconv"
    "time"
)

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
var subscriptionKey string = "ENTER KEY HERE"

// NOTE: Replace this with a valid knowledge base ID.
var kb string = "ENTER ID HERE";

var host string = "https://westus.api.cognitive.microsoft.com"
var service string = "/qnamaker/v4.0"
var method string = "/knowledgebases/"

type Response struct {
    Headers map[string][]string
    Body    string
}

func pretty_print(content string) string {
    var obj map[string]interface{}
    json.Unmarshal([]byte(content), &obj)
    result, _ := json.MarshalIndent(obj, "", "  ")
    return string(result)
}

func patch(uri string, content string) Response {
    req, _ := http.NewRequest("PATCH", uri, bytes.NewBuffer([]byte(content)))
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)
    req.Header.Add("Content-Type", "application/json")
    req.Header.Add("Content-Length", strconv.Itoa(len(content)))
    client := &http.Client{}
    response, err := client.Do(req)
    if err != nil {
        panic(err)
    }

    defer response.Body.Close()
    body, _ := ioutil.ReadAll(response.Body)

    return Response {response.Header, string(body)}
}

func get(uri string) Response {
    req, _ := http.NewRequest("GET", uri, nil)
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)
    client := &http.Client{}
    response, err := client.Do(req)
    if err != nil {
        panic(err)
    }

    defer response.Body.Close()
    body, _ := ioutil.ReadAll(response.Body)

    return Response {response.Header, string(body)}
}

var req string = `{
  'add': {
    'qnaList': [
      {
        'id': 1,
        'answer': 'You can change the default message if you use the QnAMakerDialog. See this for details: https://docs.botframework.com/en-us/azure-bot-service/templates/qnamaker/#navtitle',
        'source': 'Custom Editorial',
        'questions': [
          'How can I change the default message from QnA Maker?'
        ],
        'metadata': []
      }
    ],
    'urls': [
      'https://docs.microsoft.com/en-us/azure/cognitive-services/Emotion/FAQ'
    ]
  },
  'update' : {
    'name' : 'New KB Name'
  },
  'delete': {
    'ids': [
      0
    ]
  }
}`;

func update_kb (uri string, req string) (string, string) {
    fmt.Println("Calling " + uri + ".")
    result := patch(uri, req)
    return result.Headers["Location"][0], result.Body
}

func check_status(uri string) (string, string) {
    fmt.Println("Calling " + uri + ".")
    result := get(uri)
    if retry, success := result.Headers["Retry-After"]; success {
        return retry[0], result.Body
    } else {
// If the response headers did not include a Retry-After value, default to 30 seconds.
        return "30", result.Body
    }
}

func main() {
    var uri = host + service + method + kb
    operation, body := update_kb (uri, req)
    fmt.Printf(body + "\n")
    var done bool = false
    for done == false {
        uri := host + service + operation
        wait, status := check_status(uri)
        fmt.Println(status)
        var status_obj map[string]interface{}
        json.Unmarshal([]byte(status), &status_obj)
        state := status_obj["operationState"]
// If the operation isn't finished, wait and query again.
        if state == "Running" || state == "NotStarted" {
            fmt.Printf ("Waiting " + wait + " seconds...")
            sec, _ := strconv.Atoi(wait)
            time.Sleep (time.Duration(sec) * time.Second)
        } else {
            done = true
        }
    }
}
```

<span data-ttu-id="1b14e-138">**Update knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="1b14e-138">**Update knowledge base response**</span></span>

<span data-ttu-id="1b14e-139">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1b14e-139">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "operationState": "NotStarted",
  "createdTimestamp": "2018-04-13T01:49:48Z",
  "lastActionTimestamp": "2018-04-13T01:49:48Z",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "5156f64e-e31d-4638-ad7c-a2bdd7f41658"
}
...
{
  "operationState": "Succeeded",
  "createdTimestamp": "2018-04-13T01:49:48Z",
  "lastActionTimestamp": "2018-04-13T01:49:50Z",
  "resourceLocation": "/knowledgebases/140a46f3-b248-4f1b-9349-614bfd6e5563",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "5156f64e-e31d-4638-ad7c-a2bdd7f41658"
}
Press any key to continue.
```

[<span data-ttu-id="1b14e-140">Back to top</span><span class="sxs-lookup"><span data-stu-id="1b14e-140">Back to top</span></span>](#HOLTop)

<a name="Status"></a>

## <a name="get-request-status"></a><span data-ttu-id="1b14e-141">Get request status</span><span class="sxs-lookup"><span data-stu-id="1b14e-141">Get request status</span></span>

<span data-ttu-id="1b14e-142">You can call the [Operation](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/operations_getoperationdetails) method to check the status of a request to create or update a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="1b14e-142">You can call the [Operation](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/operations_getoperationdetails) method to check the status of a request to create or update a knowledge base.</span></span> <span data-ttu-id="1b14e-143">To see how this method is used, please see the sample code for the [Create](#Create) or [Update](#Update) method.</span><span class="sxs-lookup"><span data-stu-id="1b14e-143">To see how this method is used, please see the sample code for the [Create](#Create) or [Update](#Update) method.</span></span>

[<span data-ttu-id="1b14e-144">Back to top</span><span class="sxs-lookup"><span data-stu-id="1b14e-144">Back to top</span></span>](#HOLTop)

<a name="Publish"></a>

## <a name="publish-knowledge-base"></a><span data-ttu-id="1b14e-145">Publish knowledge base</span><span class="sxs-lookup"><span data-stu-id="1b14e-145">Publish knowledge base</span></span>

<span data-ttu-id="1b14e-146">The following code publishes an existing knowledge base, using the [Publish](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fe) method.</span><span class="sxs-lookup"><span data-stu-id="1b14e-146">The following code publishes an existing knowledge base, using the [Publish](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fe) method.</span></span>

1. <span data-ttu-id="1b14e-147">Create a new Go project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="1b14e-147">Create a new Go project in your favorite IDE.</span></span>
2. <span data-ttu-id="1b14e-148">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="1b14e-148">Add the code provided below.</span></span>
3. <span data-ttu-id="1b14e-149">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="1b14e-149">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="1b14e-150">Run the program.</span><span class="sxs-lookup"><span data-stu-id="1b14e-150">Run the program.</span></span>

```go
package main

import (
    "bytes"
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
    "strconv"
)

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
var subscriptionKey string = "ENTER KEY HERE"

// NOTE: Replace this with a valid knowledge base ID.
var kb string = "ENTER ID HERE";

var host string = "https://westus.api.cognitive.microsoft.com"
var service string = "/qnamaker/v4.0"
var method string = "/knowledgebases/"

func pretty_print(content string) string {
    var obj map[string]interface{}
    json.Unmarshal([]byte(content), &obj)
    result, _ := json.MarshalIndent(obj, "", "  ")
    return string(result)
}

func post(uri string, content string) string {
    req, _ := http.NewRequest("POST", uri, bytes.NewBuffer([]byte(content)))
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)
    req.Header.Add("Content-Type", "application/json")
    req.Header.Add("Content-Length", strconv.Itoa(len(content)))
    client := &http.Client{}
    response, err := client.Do(req)
    if err != nil {
        panic(err)
    }

    defer response.Body.Close()
    body, _ := ioutil.ReadAll(response.Body)

    if(response.StatusCode == 204) {
        return "{'result' : 'Success.'}"
    } else {
        return string(body)
    }
}

func publish(uri string, req string) string {
    fmt.Println("Calling " + uri + ".")
    return post(uri, req)
}

func main() {
    var uri = host + service + method + kb
    body := publish(uri, "")
    fmt.Printf(body + "\n")

}
```

<span data-ttu-id="1b14e-151">**Publish knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="1b14e-151">**Publish knowledge base response**</span></span>

<span data-ttu-id="1b14e-152">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1b14e-152">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "result": "Success."
}
```

[<span data-ttu-id="1b14e-153">Back to top</span><span class="sxs-lookup"><span data-stu-id="1b14e-153">Back to top</span></span>](#HOLTop)

<a name="Replace"></a>

## <a name="replace-knowledge-base"></a><span data-ttu-id="1b14e-154">Replace knowledge base</span><span class="sxs-lookup"><span data-stu-id="1b14e-154">Replace knowledge base</span></span>

<span data-ttu-id="1b14e-155">The following code replaces the contents of the specified knowledge base, using the [Replace](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_publish) method.</span><span class="sxs-lookup"><span data-stu-id="1b14e-155">The following code replaces the contents of the specified knowledge base, using the [Replace](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_publish) method.</span></span>

1. <span data-ttu-id="1b14e-156">Create a new Go project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="1b14e-156">Create a new Go project in your favorite IDE.</span></span>
2. <span data-ttu-id="1b14e-157">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="1b14e-157">Add the code provided below.</span></span>
3. <span data-ttu-id="1b14e-158">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="1b14e-158">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="1b14e-159">Run the program.</span><span class="sxs-lookup"><span data-stu-id="1b14e-159">Run the program.</span></span>

```go
package main

import (
    "bytes"
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
    "strconv"
)

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
var subscriptionKey string = "ENTER KEY HERE"

// NOTE: Replace this with a valid knowledge base ID.
var kb string = "ENTER ID HERE";

var host string = "https://westus.api.cognitive.microsoft.com"
var service string = "/qnamaker/v4.0"
var method string = "/knowledgebases/"

func pretty_print(content string) string {
    var obj map[string]interface{}
    json.Unmarshal([]byte(content), &obj)
    result, _ := json.MarshalIndent(obj, "", "  ")
    return string(result)
}

func put(uri string, content string) string {
    req, _ := http.NewRequest("PUT", uri, bytes.NewBuffer([]byte(content)))
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)
    req.Header.Add("Content-Type", "application/json")
    req.Header.Add("Content-Length", strconv.Itoa(len(content)))
    client := &http.Client{}
    response, err := client.Do(req)
    if err != nil {
        panic(err)
    }

    defer response.Body.Close()
    body, _ := ioutil.ReadAll(response.Body)

    if(response.StatusCode == 204) {
        return "{'result' : 'Success.'}"
    } else {
        return string(body)
    }
}

var req string = `{
  'qnaList': [
    {
      'id': 0,
      'answer': 'You can use our REST APIs to manage your Knowledge Base. See here for details: https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600',
      'source': 'Custom Editorial',
      'questions': [
        'How do I programmatically update my Knowledge Base?'
      ],
      'metadata': [
        {
          'name': 'category',
          'value': 'api'
        }
      ]
    }
  ]
}`;

func replace_kb (uri string, req string) (string) {
    fmt.Println("Calling " + uri + ".")
    return put(uri, req)
}

func main() {
    var uri = host + service + method + kb
    body := replace_kb (uri, req)
    fmt.Printf(body + "\n")
}
```

<span data-ttu-id="1b14e-160">**Replace knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="1b14e-160">**Replace knowledge base response**</span></span>

<span data-ttu-id="1b14e-161">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1b14e-161">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
    "result": "Success."
}
```

[<span data-ttu-id="1b14e-162">Back to top</span><span class="sxs-lookup"><span data-stu-id="1b14e-162">Back to top</span></span>](#HOLTop)

<a name="GetQnA"></a>

## <a name="download-the-contents-of-a-knowledge-base"></a><span data-ttu-id="1b14e-163">Download the contents of a knowledge base</span><span class="sxs-lookup"><span data-stu-id="1b14e-163">Download the contents of a knowledge base</span></span>

<span data-ttu-id="1b14e-164">The following code downloads the contents of the specified knowledge base, using the [Download knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_download) method.</span><span class="sxs-lookup"><span data-stu-id="1b14e-164">The following code downloads the contents of the specified knowledge base, using the [Download knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_download) method.</span></span>

1. <span data-ttu-id="1b14e-165">Create a new Go project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="1b14e-165">Create a new Go project in your favorite IDE.</span></span>
2. <span data-ttu-id="1b14e-166">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="1b14e-166">Add the code provided below.</span></span>
3. <span data-ttu-id="1b14e-167">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="1b14e-167">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="1b14e-168">Run the program.</span><span class="sxs-lookup"><span data-stu-id="1b14e-168">Run the program.</span></span>

```go
package main

import (
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
)

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
var subscriptionKey string = "ENTER KEY HERE"

// NOTE: Replace this with a valid knowledge base ID.
var kb string = "ENTER ID HERE";

// NOTE: Replace this with "test" or "prod".
var env string = "test";

var host string = "https://westus.api.cognitive.microsoft.com"
var service string = "/qnamaker/v4.0"
var method string = "/knowledgebases/%s/%s/qna"

func pretty_print(content string) string {
    var obj map[string]interface{}
    json.Unmarshal([]byte(content), &obj)
    result, _ := json.MarshalIndent(obj, "", "  ")
    return string(result)
}

func get(uri string) string {
    req, _ := http.NewRequest("GET", uri, nil)
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)
    client := &http.Client{}
    response, err := client.Do(req)
    if err != nil {
        panic(err)
    }

    defer response.Body.Close()
    body, _ := ioutil.ReadAll(response.Body)
    return string(body)
}

func getQnA(uri string) string {
    fmt.Println("Calling " + uri + ".")
    return get(uri)
}

func main() {
    var method_with_id = fmt.Sprintf(method, kb, env)
    var uri = host + service + method_with_id
    body := getQnA(uri)
    fmt.Printf(body + "\n")
}
```

<span data-ttu-id="1b14e-169">**Download knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="1b14e-169">**Download knowledge base response**</span></span>

<span data-ttu-id="1b14e-170">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1b14e-170">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "qnaDocuments": [
    {
      "id": 1,
      "answer": "You can use our REST APIs to manage your Knowledge Base. See here for details: https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600",
      "source": "Custom Editorial",
      "questions": [
        "How do I programmatically update my Knowledge Base?"
      ],
      "metadata": [
        {
          "name": "category",
          "value": "api"
        }
      ]
    },
    {
      "id": 2,
      "answer": "QnA Maker provides an FAQ data source that you can query from your bot or application. Although developers will find this useful, content owners will especially benefit from this tool. QnA Maker is a completely no-code way of managing the content that powers your bot or application.",
      "source": "https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs",
      "questions": [
        "Who is the target audience for the QnA Maker tool?"
      ],
      "metadata": []
    },
...
  ]
}
```

[<span data-ttu-id="1b14e-171">Back to top</span><span class="sxs-lookup"><span data-stu-id="1b14e-171">Back to top</span></span>](#HOLTop)

<a name="GetAnswers"></a>

## <a name="get-answers-to-a-question-by-using-a-knowledge-base"></a><span data-ttu-id="1b14e-172">Get answers to a question by using a knowledge base</span><span class="sxs-lookup"><span data-stu-id="1b14e-172">Get answers to a question by using a knowledge base</span></span>

<span data-ttu-id="1b14e-173">The following code gets answers to a question using the specified knowledge base, using the **Generate answers** method.</span><span class="sxs-lookup"><span data-stu-id="1b14e-173">The following code gets answers to a question using the specified knowledge base, using the **Generate answers** method.</span></span>

1. <span data-ttu-id="1b14e-174">Create a new Go project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="1b14e-174">Create a new Go project in your favorite IDE.</span></span>
1. <span data-ttu-id="1b14e-175">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="1b14e-175">Add the code provided below.</span></span>
1. <span data-ttu-id="1b14e-176">Replace the `host` value with the Website name for your QnA Maker subscription.</span><span class="sxs-lookup"><span data-stu-id="1b14e-176">Replace the `host` value with the Website name for your QnA Maker subscription.</span></span> <span data-ttu-id="1b14e-177">For more information see [Create a QnA Maker service](../How-To/set-up-qnamaker-service-azure.md).</span><span class="sxs-lookup"><span data-stu-id="1b14e-177">For more information see [Create a QnA Maker service](../How-To/set-up-qnamaker-service-azure.md).</span></span>
1. <span data-ttu-id="1b14e-178">Replace the `endpoint_key` value with a valid endpoint key for your subscription.</span><span class="sxs-lookup"><span data-stu-id="1b14e-178">Replace the `endpoint_key` value with a valid endpoint key for your subscription.</span></span> <span data-ttu-id="1b14e-179">Note this is not the same as your subscription key.</span><span class="sxs-lookup"><span data-stu-id="1b14e-179">Note this is not the same as your subscription key.</span></span> <span data-ttu-id="1b14e-180">You can get your endpoint keys using the [Get endpoint keys](#GetKeys) method.</span><span class="sxs-lookup"><span data-stu-id="1b14e-180">You can get your endpoint keys using the [Get endpoint keys](#GetKeys) method.</span></span>
1. <span data-ttu-id="1b14e-181">Replace the `kb` value with the ID of the knowledge base you want to query for answers.</span><span class="sxs-lookup"><span data-stu-id="1b14e-181">Replace the `kb` value with the ID of the knowledge base you want to query for answers.</span></span> <span data-ttu-id="1b14e-182">Note this knowledge base must already have been published using the [Publish](#Publish) method.</span><span class="sxs-lookup"><span data-stu-id="1b14e-182">Note this knowledge base must already have been published using the [Publish](#Publish) method.</span></span>
1. <span data-ttu-id="1b14e-183">Run the program.</span><span class="sxs-lookup"><span data-stu-id="1b14e-183">Run the program.</span></span>

```go
package main

import (
    "bytes"
    "fmt"
    "io/ioutil"
    "net/http"
    "strconv"
)

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// NOTE: Replace this with a valid host name.
var host string = "ENTER HOST HERE";

// NOTE: Replace this with a valid endpoint key.
// This is not your subscription key.
// To get your endpoint keys, call the GET /endpointkeys method.
var endpoint_key string = "ENTER KEY HERE";

// NOTE: Replace this with a valid knowledge base ID.
// Make sure you have published the knowledge base with the
// POST /knowledgebases/{knowledge base ID} method.
var kb string = "ENTER KB ID HERE";

var method string = "/qnamaker/knowledgebases/" + kb + "/generateanswer"

func post(uri string, content string) string {
    req, _ := http.NewRequest("POST", uri, bytes.NewBuffer([]byte(content)))
    req.Header.Add("Authorization", "EndpointKey " + endpoint_key)
    req.Header.Add("Content-Type", "application/json")
    req.Header.Add("Content-Length", strconv.Itoa(len(content)))
    client := &http.Client{}
    response, err := client.Do(req)
    if err != nil {
        panic(err)
    }

    defer response.Body.Close()
    body, _ := ioutil.ReadAll(response.Body)

    return string(body)
}

var req string = `{
    'question': 'Is the QnA Maker Service free?',
    'top': 3
}`;

func get_answers(uri string, req string) string {
    fmt.Println("Calling " + uri + ".")
    return post(uri, req)
}

func main() {
    var uri = host + method
    body := get_answers(uri, req)
    fmt.Printf(body + "\n")
}
```

<span data-ttu-id="1b14e-184">**Get answers response**</span><span class="sxs-lookup"><span data-stu-id="1b14e-184">**Get answers response**</span></span>

<span data-ttu-id="1b14e-185">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1b14e-185">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "answers": [
    {
      "questions": [
        "Can I use BitLocker with the Volume Shadow Copy Service?"
      ],
      "answer": "Yes. However, shadow copies made prior to enabling BitLocker will be automatically deleted when BitLocker is enabled on software-encrypted drives. If you are using a hardware encrypted drive, the shadow copies are retained.",
      "score": 17.3,
      "id": 62,
      "source": "https://docs.microsoft.com/en-us/windows/security/information-protection/bitlocker/bitlocker-frequently-asked-questions",
      "metadata": []
    },
...
  ]
}
```

[<span data-ttu-id="1b14e-186">Back to top</span><span class="sxs-lookup"><span data-stu-id="1b14e-186">Back to top</span></span>](#HOLTop)

<a name="GetKB"></a>

## <a name="get-information-about-a-knowledge-base"></a><span data-ttu-id="1b14e-187">Get information about a knowledge base</span><span class="sxs-lookup"><span data-stu-id="1b14e-187">Get information about a knowledge base</span></span>

<span data-ttu-id="1b14e-188">The following code gets information about the specified knowledge base, using the [Get knowledge base details](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasedetails) method.</span><span class="sxs-lookup"><span data-stu-id="1b14e-188">The following code gets information about the specified knowledge base, using the [Get knowledge base details](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasedetails) method.</span></span>

1. <span data-ttu-id="1b14e-189">Create a new Go project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="1b14e-189">Create a new Go project in your favorite IDE.</span></span>
2. <span data-ttu-id="1b14e-190">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="1b14e-190">Add the code provided below.</span></span>
3. <span data-ttu-id="1b14e-191">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="1b14e-191">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="1b14e-192">Run the program.</span><span class="sxs-lookup"><span data-stu-id="1b14e-192">Run the program.</span></span>

```go
package main

import (
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
)

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
var subscriptionKey string = "ENTER KEY HERE"

// NOTE: Replace this with a valid knowledge base ID.
var kb string = "ENTER ID HERE";

var host string = "https://westus.api.cognitive.microsoft.com"
var service string = "/qnamaker/v4.0"
var method string = "/knowledgebases/"

func pretty_print(content string) string {
    var obj map[string]interface{}
    json.Unmarshal([]byte(content), &obj)
    result, _ := json.MarshalIndent(obj, "", "  ")
    return string(result)
}

func get(uri string) string {
    req, _ := http.NewRequest("GET", uri, nil)
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)
    client := &http.Client{}
    response, err := client.Do(req)
    if err != nil {
        panic(err)
    }

    defer response.Body.Close()
    body, _ := ioutil.ReadAll(response.Body)
    return string(body)
}

func getKB(uri string) string {
    fmt.Println("Calling " + uri + ".")
    return get(uri)
}

func main() {
    var uri = host + service + method + kb
    body := getKB(uri)
    fmt.Printf(body + "\n")
}
```

<span data-ttu-id="1b14e-193">**Get knowledge base details response**</span><span class="sxs-lookup"><span data-stu-id="1b14e-193">**Get knowledge base details response**</span></span>

<span data-ttu-id="1b14e-194">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1b14e-194">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "id": "140a46f3-b248-4f1b-9349-614bfd6e5563",
  "hostName": "https://qna-docs.azurewebsites.net",
  "lastAccessedTimestamp": "2018-04-12T22:58:01Z",
  "lastChangedTimestamp": "2018-04-12T22:58:01Z",
  "name": "QnA Maker FAQ",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "urls": [
    "https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs",
    "https://docs.microsoft.com/en-us/bot-framework/resources-bot-framework-faq"
  ],
  "sources": [
    "Custom Editorial"
  ]
}
```

[<span data-ttu-id="1b14e-195">Back to top</span><span class="sxs-lookup"><span data-stu-id="1b14e-195">Back to top</span></span>](#HOLTop)

<a name="GetKBsByUser"></a>

## <a name="get-all-knowledge-bases-for-a-user"></a><span data-ttu-id="1b14e-196">Get all knowledge bases for a user</span><span class="sxs-lookup"><span data-stu-id="1b14e-196">Get all knowledge bases for a user</span></span>

<span data-ttu-id="1b14e-197">The following code gets information about all knowledge bases for a specified user, using the [Get knowledge bases for user](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasesforuser) method.</span><span class="sxs-lookup"><span data-stu-id="1b14e-197">The following code gets information about all knowledge bases for a specified user, using the [Get knowledge bases for user](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasesforuser) method.</span></span>

1. <span data-ttu-id="1b14e-198">Create a new Go project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="1b14e-198">Create a new Go project in your favorite IDE.</span></span>
2. <span data-ttu-id="1b14e-199">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="1b14e-199">Add the code provided below.</span></span>
3. <span data-ttu-id="1b14e-200">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="1b14e-200">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="1b14e-201">Run the program.</span><span class="sxs-lookup"><span data-stu-id="1b14e-201">Run the program.</span></span>

```go
package main

import (
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
)

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
var subscriptionKey string = "ENTER KEY HERE"

var host string = "https://westus.api.cognitive.microsoft.com"
var service string = "/qnamaker/v4.0"
var method string = "/knowledgebases/"

func pretty_print(content string) string {
    var obj map[string]interface{}
    json.Unmarshal([]byte(content), &obj)
    result, _ := json.MarshalIndent(obj, "", "  ")
    return string(result)
}

func get(uri string) string {
    req, _ := http.NewRequest("GET", uri, nil)
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)
    client := &http.Client{}
    response, err := client.Do(req)
    if err != nil {
        panic(err)
    }

    defer response.Body.Close()
    body, _ := ioutil.ReadAll(response.Body)
    return string(body)
}

func getKBs(uri string) string {
    fmt.Println("Calling " + uri + ".")
    return get(uri)
}

func main() {
    var uri = host + service + method
    body := getKBs(uri)
    fmt.Printf(body + "\n")
}
```

<span data-ttu-id="1b14e-202">**Get knowledge bases for user response**</span><span class="sxs-lookup"><span data-stu-id="1b14e-202">**Get knowledge bases for user response**</span></span>

<span data-ttu-id="1b14e-203">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1b14e-203">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "knowledgebases": [
    {
      "id": "081c32a7-bd05-4982-9d74-07ac736df0ac",
      "hostName": "https://qna-docs.azurewebsites.net",
      "lastAccessedTimestamp": "2018-04-12T11:51:58Z",
      "lastChangedTimestamp": "2018-04-12T11:51:58Z",
      "name": "QnA Maker FAQ",
      "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
      "urls": [],
      "sources": []
    },
    {
      "id": "140a46f3-b248-4f1b-9349-614bfd6e5563",
      "hostName": "https://qna-docs.azurewebsites.net",
      "lastAccessedTimestamp": "2018-04-12T22:58:01Z",
      "lastChangedTimestamp": "2018-04-12T22:58:01Z",
      "name": "QnA Maker FAQ",
      "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
      "urls": [
        "https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs",
        "https://docs.microsoft.com/en-us/bot-framework/resources-bot-framework-faq"
      ],
      "sources": [
        "Custom Editorial"
      ]
    },
...
  ]
}
Press any key to continue.
```

[<span data-ttu-id="1b14e-204">Back to top</span><span class="sxs-lookup"><span data-stu-id="1b14e-204">Back to top</span></span>](#HOLTop)

<a name="Delete"></a>

## <a name="delete-a-knowledge-base"></a><span data-ttu-id="1b14e-205">Delete a knowledge base</span><span class="sxs-lookup"><span data-stu-id="1b14e-205">Delete a knowledge base</span></span>

<span data-ttu-id="1b14e-206">The following code deletes the specified knowledge base, using the [Delete knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_delete) method.</span><span class="sxs-lookup"><span data-stu-id="1b14e-206">The following code deletes the specified knowledge base, using the [Delete knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_delete) method.</span></span>

1. <span data-ttu-id="1b14e-207">Create a new Go project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="1b14e-207">Create a new Go project in your favorite IDE.</span></span>
2. <span data-ttu-id="1b14e-208">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="1b14e-208">Add the code provided below.</span></span>
3. <span data-ttu-id="1b14e-209">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="1b14e-209">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="1b14e-210">Run the program.</span><span class="sxs-lookup"><span data-stu-id="1b14e-210">Run the program.</span></span>

```go
package main

import (
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
)

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
var subscriptionKey string = "ENTER KEY HERE"

// NOTE: Replace this with a valid knowledge base ID.
var kb string = "ENTER ID HERE";

var host string = "https://westus.api.cognitive.microsoft.com"
var service string = "/qnamaker/v4.0"
var method string = "/knowledgebases/"

func pretty_print(content string) string {
    var obj map[string]interface{}
    json.Unmarshal([]byte(content), &obj)
    result, _ := json.MarshalIndent(obj, "", "  ")
    return string(result)
}

func delete(uri string) string {
    req, _ := http.NewRequest("DELETE", uri, nil)
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)
    client := &http.Client{}
    response, err := client.Do(req)
    if err != nil {
        panic(err)
    }

    defer response.Body.Close()
    body, _ := ioutil.ReadAll(response.Body)

    if(response.StatusCode == 204) {
        return "{'result' : 'Success.'}"
    } else {
        return string(body)
    }
}

func deleteKB(uri string) string {
    fmt.Println("Calling " + uri + ".")
    return delete(uri)
}

func main() {
    var uri = host + service + method + kb
    body := deleteKB(uri)
    fmt.Printf(body + "\n")

}
```

<span data-ttu-id="1b14e-211">**Delete knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="1b14e-211">**Delete knowledge base response**</span></span>

<span data-ttu-id="1b14e-212">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1b14e-212">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "result": "Success."
}
```

[<span data-ttu-id="1b14e-213">Back to top</span><span class="sxs-lookup"><span data-stu-id="1b14e-213">Back to top</span></span>](#HOLTop)

<a name="GetKeys"></a>

## <a name="get-endpoint-keys"></a><span data-ttu-id="1b14e-214">Get endpoint keys</span><span class="sxs-lookup"><span data-stu-id="1b14e-214">Get endpoint keys</span></span>

<span data-ttu-id="1b14e-215">The following code gets the current endpoint keys, using the [Get endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_getendpointkeys) method.</span><span class="sxs-lookup"><span data-stu-id="1b14e-215">The following code gets the current endpoint keys, using the [Get endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_getendpointkeys) method.</span></span>

1. <span data-ttu-id="1b14e-216">Create a new Go project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="1b14e-216">Create a new Go project in your favorite IDE.</span></span>
2. <span data-ttu-id="1b14e-217">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="1b14e-217">Add the code provided below.</span></span>
3. <span data-ttu-id="1b14e-218">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="1b14e-218">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="1b14e-219">Run the program.</span><span class="sxs-lookup"><span data-stu-id="1b14e-219">Run the program.</span></span>

```go
package main

import (
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
)

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
var subscriptionKey string = "ENTER KEY HERE"

var host string = "https://westus.api.cognitive.microsoft.com"
var service string = "/qnamaker/v4.0"
var method string = "/endpointkeys/"

func pretty_print(content string) string {
    var obj map[string]interface{}
    json.Unmarshal([]byte(content), &obj)
    result, _ := json.MarshalIndent(obj, "", "  ")
    return string(result)
}

func get(uri string) string {
    req, _ := http.NewRequest("GET", uri, nil)
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)
    client := &http.Client{}
    response, err := client.Do(req)
    if err != nil {
        panic(err)
    }

    defer response.Body.Close()
    body, _ := ioutil.ReadAll(response.Body)
    return string(body)
}

func getEndpointKeys(uri string) string {
    fmt.Println("Calling " + uri + ".")
    return get(uri)
}

func main() {
    var uri = host + service + method
    body := getEndpointKeys(uri)
    fmt.Printf(body + "\n")
}
```

<span data-ttu-id="1b14e-220">**Get endpoint keys response**</span><span class="sxs-lookup"><span data-stu-id="1b14e-220">**Get endpoint keys response**</span></span>

<span data-ttu-id="1b14e-221">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1b14e-221">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "primaryEndpointKey": "ac110bdc-34b7-4b1c-b9cd-b05f9a6001f3",
  "secondaryEndpointKey": "1b4ed14e-614f-444a-9f3d-9347f45a9206"
}
```

[<span data-ttu-id="1b14e-222">Back to top</span><span class="sxs-lookup"><span data-stu-id="1b14e-222">Back to top</span></span>](#HOLTop)

<a name="PutKeys"></a>

## <a name="refresh-endpoint-keys"></a><span data-ttu-id="1b14e-223">Refresh endpoint keys</span><span class="sxs-lookup"><span data-stu-id="1b14e-223">Refresh endpoint keys</span></span>

<span data-ttu-id="1b14e-224">The following code regenerates the current endpoint keys, using the [Refresh endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_refreshendpointkeys) method.</span><span class="sxs-lookup"><span data-stu-id="1b14e-224">The following code regenerates the current endpoint keys, using the [Refresh endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_refreshendpointkeys) method.</span></span>

1. <span data-ttu-id="1b14e-225">Create a new Go project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="1b14e-225">Create a new Go project in your favorite IDE.</span></span>
2. <span data-ttu-id="1b14e-226">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="1b14e-226">Add the code provided below.</span></span>
3. <span data-ttu-id="1b14e-227">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="1b14e-227">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="1b14e-228">Run the program.</span><span class="sxs-lookup"><span data-stu-id="1b14e-228">Run the program.</span></span>

```go
package main

import (
    "bytes"
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
    "strconv"
)

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
var subscriptionKey string = "ENTER KEY HERE"

// NOTE: Replace this with "PrimaryKey" or "SecondaryKey."
var key_type string = "PrimaryKey";

var host string = "https://westus.api.cognitive.microsoft.com"
var service string = "/qnamaker/v4.0"
var method string = "/endpointkeys/"

func pretty_print(content string) string {
    var obj map[string]interface{}
    json.Unmarshal([]byte(content), &obj)
    result, _ := json.MarshalIndent(obj, "", "  ")
    return string(result)
}

func patch(uri string, content string) string {
    req, _ := http.NewRequest("PATCH", uri, bytes.NewBuffer([]byte(content)))
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)
    req.Header.Add("Content-Type", "application/json")
    req.Header.Add("Content-Length", strconv.Itoa(len(content)))
    client := &http.Client{}
    response, err := client.Do(req)
    if err != nil {
        panic(err)
    }

    defer response.Body.Close()
    body, _ := ioutil.ReadAll(response.Body)

    return string(body)
}

func refresh (uri string, req string) string {
    fmt.Println("Calling " + uri + ".")
    return patch(uri, req)
}

func main() {
    var uri = host + service + method + key_type
    body := refresh (uri, "")
    fmt.Printf(body + "\n")
}
```

<span data-ttu-id="1b14e-229">**Refresh endpoint keys response**</span><span class="sxs-lookup"><span data-stu-id="1b14e-229">**Refresh endpoint keys response**</span></span>

<span data-ttu-id="1b14e-230">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1b14e-230">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "primaryEndpointKey": "ac110bdc-34b7-4b1c-b9cd-b05f9a6001f3",
  "secondaryEndpointKey": "1b4ed14e-614f-444a-9f3d-9347f45a9206"
}
```

[<span data-ttu-id="1b14e-231">Back to top</span><span class="sxs-lookup"><span data-stu-id="1b14e-231">Back to top</span></span>](#HOLTop)

<a name="GetAlterations"></a>

## <a name="get-word-alterations"></a><span data-ttu-id="1b14e-232">Get word alterations</span><span class="sxs-lookup"><span data-stu-id="1b14e-232">Get word alterations</span></span>

<span data-ttu-id="1b14e-233">The following code gets the current word alterations, using the [Download alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fc) method.</span><span class="sxs-lookup"><span data-stu-id="1b14e-233">The following code gets the current word alterations, using the [Download alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fc) method.</span></span>

1. <span data-ttu-id="1b14e-234">Create a new Go project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="1b14e-234">Create a new Go project in your favorite IDE.</span></span>
2. <span data-ttu-id="1b14e-235">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="1b14e-235">Add the code provided below.</span></span>
3. <span data-ttu-id="1b14e-236">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="1b14e-236">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="1b14e-237">Run the program.</span><span class="sxs-lookup"><span data-stu-id="1b14e-237">Run the program.</span></span>

```go
package main

import (
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
)

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
var subscriptionKey string = "ENTER KEY HERE"

var host string = "https://westus.api.cognitive.microsoft.com"
var service string = "/qnamaker/v4.0"
var method string = "/alterations/"

func pretty_print(content string) string {
    var obj map[string]interface{}
    json.Unmarshal([]byte(content), &obj)
    result, _ := json.MarshalIndent(obj, "", "  ")
    return string(result)
}

func get(uri string) string {
    req, _ := http.NewRequest("GET", uri, nil)
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)
    client := &http.Client{}
    response, err := client.Do(req)
    if err != nil {
        panic(err)
    }

    defer response.Body.Close()
    body, _ := ioutil.ReadAll(response.Body)
    return string(body)
}

func getAlterations(uri string) string {
    fmt.Println("Calling " + uri + ".")
    return get(uri)
}

func main() {
    var uri = host + service + method
    body := getAlterations(uri)
    fmt.Printf(body + "\n")
}
```

<span data-ttu-id="1b14e-238">**Get word alterations response**</span><span class="sxs-lookup"><span data-stu-id="1b14e-238">**Get word alterations response**</span></span>

<span data-ttu-id="1b14e-239">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1b14e-239">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "wordAlterations": [
    {
      "alterations": [
        "botframework",
        "bot frame work"
      ]
    }
  ]
}
```

[<span data-ttu-id="1b14e-240">Back to top</span><span class="sxs-lookup"><span data-stu-id="1b14e-240">Back to top</span></span>](#HOLTop)

<a name="PutAlterations"></a>

## <a name="replace-word-alterations"></a><span data-ttu-id="1b14e-241">Replace word alterations</span><span class="sxs-lookup"><span data-stu-id="1b14e-241">Replace word alterations</span></span>

<span data-ttu-id="1b14e-242">The following code replaces the current word alterations, using the [Replace alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fd) method.</span><span class="sxs-lookup"><span data-stu-id="1b14e-242">The following code replaces the current word alterations, using the [Replace alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fd) method.</span></span>

1. <span data-ttu-id="1b14e-243">Create a new Go project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="1b14e-243">Create a new Go project in your favorite IDE.</span></span>
2. <span data-ttu-id="1b14e-244">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="1b14e-244">Add the code provided below.</span></span>
3. <span data-ttu-id="1b14e-245">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="1b14e-245">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="1b14e-246">Run the program.</span><span class="sxs-lookup"><span data-stu-id="1b14e-246">Run the program.</span></span>

```go
package main

import (
    "bytes"
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
    "strconv"
)

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
var subscriptionKey string = "ENTER KEY HERE"

var host string = "https://westus.api.cognitive.microsoft.com"
var service string = "/qnamaker/v4.0"
var method string = "/alterations/"

func pretty_print(content string) string {
    var obj map[string]interface{}
    json.Unmarshal([]byte(content), &obj)
    result, _ := json.MarshalIndent(obj, "", "  ")
    return string(result)
}

func put(uri string, content string) string {
    req, _ := http.NewRequest("PUT", uri, bytes.NewBuffer([]byte(content)))
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)
    req.Header.Add("Content-Type", "application/json")
    req.Header.Add("Content-Length", strconv.Itoa(len(content)))
    client := &http.Client{}
    response, err := client.Do(req)
    if err != nil {
        panic(err)
    }

    defer response.Body.Close()
    body, _ := ioutil.ReadAll(response.Body)

    if(response.StatusCode == 204) {
        return "{'result' : 'Success.'}"
    } else {
        return string(body)
    }
}

var req string = `{
  'wordAlterations': [
    {
      'alterations': [
        'botframework',
        'bot frame work'
      ]
    }
  ]
}`;

func putAlterations (uri string, req string) (string) {
    fmt.Println("Calling " + uri + ".")
    return put(uri, req)
}

func main() {
    var uri = host + service + method
    body := putAlterations (uri, req)
    fmt.Printf(body + "\n")
}
```

<span data-ttu-id="1b14e-247">**Replace word alterations response**</span><span class="sxs-lookup"><span data-stu-id="1b14e-247">**Replace word alterations response**</span></span>

<span data-ttu-id="1b14e-248">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1b14e-248">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "result": "Success."
}
```

[<span data-ttu-id="1b14e-249">Back to top</span><span class="sxs-lookup"><span data-stu-id="1b14e-249">Back to top</span></span>](#HOLTop)

## <a name="next-steps"></a><span data-ttu-id="1b14e-250">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b14e-250">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b14e-251">QnA Maker (V4) REST API Reference</span><span class="sxs-lookup"><span data-stu-id="1b14e-251">QnA Maker (V4) REST API Reference</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff)

## <a name="see-also"></a><span data-ttu-id="1b14e-252">See also</span><span class="sxs-lookup"><span data-stu-id="1b14e-252">See also</span></span> 

[<span data-ttu-id="1b14e-253">QnA Maker overview</span><span class="sxs-lookup"><span data-stu-id="1b14e-253">QnA Maker overview</span></span>](../Overview/overview.md)
