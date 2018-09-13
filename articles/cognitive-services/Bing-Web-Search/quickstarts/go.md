---
title: 'Quickstart: Use Go to call the Bing Web Search API'
description: In this quickstart, you will learn how to make your first call to the Bing Web Search API using Go and receive a JSON response.
services: cognitive-services
author: erhopf
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: quickstart
ms.date: 8/16/2018
ms.author: erhopf
ms.reviewer: nhoyadx@gmail.com, v-gedod, erhopf
ms.openlocfilehash: 3f5fc8461103b2f4ee04750ceba35e05eaa5515c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866672"
---
# <a name="quickstart-use-go-to-call-the-bing-web-search-api"></a><span data-ttu-id="e827c-103">Quickstart: Use Go to call the Bing Web Search API</span><span class="sxs-lookup"><span data-stu-id="e827c-103">Quickstart: Use Go to call the Bing Web Search API</span></span>  

<span data-ttu-id="e827c-104">Use this quickstart to make your first call to the Bing Web Search API and receive a JSON response in less than 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="e827c-104">Use this quickstart to make your first call to the Bing Web Search API and receive a JSON response in less than 10 minutes.</span></span>  

[!INCLUDE [bing-web-search-quickstart-signup](../../../../includes/bing-web-search-quickstart-signup.md)]  

## <a name="prerequisites"></a><span data-ttu-id="e827c-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e827c-105">Prerequisites</span></span>

<span data-ttu-id="e827c-106">Here are a few things that you'll need before running this quickstart:</span><span class="sxs-lookup"><span data-stu-id="e827c-106">Here are a few things that you'll need before running this quickstart:</span></span>

* [<span data-ttu-id="e827c-107">Go binaries</span><span class="sxs-lookup"><span data-stu-id="e827c-107">Go binaries</span></span>](https://golang.org/dl/)
* <span data-ttu-id="e827c-108">A subscription key</span><span class="sxs-lookup"><span data-stu-id="e827c-108">A subscription key</span></span>

<span data-ttu-id="e827c-109">This quickstart only requires **core** libraries, there are no external dependencies.</span><span class="sxs-lookup"><span data-stu-id="e827c-109">This quickstart only requires **core** libraries, there are no external dependencies.</span></span>  

## <a name="create-a-project-and-import-core-libraries"></a><span data-ttu-id="e827c-110">Create a project and import core libraries</span><span class="sxs-lookup"><span data-stu-id="e827c-110">Create a project and import core libraries</span></span>

<span data-ttu-id="e827c-111">Create a new Go project in your favorite IDE or editor.</span><span class="sxs-lookup"><span data-stu-id="e827c-111">Create a new Go project in your favorite IDE or editor.</span></span> <span data-ttu-id="e827c-112">Then import `net/http` for requests, `ioutil` to read the response, `time` and `encoding/json` to handle the JSON, and `fmt` to print the output.</span><span class="sxs-lookup"><span data-stu-id="e827c-112">Then import `net/http` for requests, `ioutil` to read the response, `time` and `encoding/json` to handle the JSON, and `fmt` to print the output.</span></span>

```go
package main
import (
    "fmt"
    "net/http"
    "io/ioutil"
    "time"
    "encoding/json"
)
```

## <a name="create-a-struct-to-format-the-search-results"></a><span data-ttu-id="e827c-113">Create a struct to format the search results</span><span class="sxs-lookup"><span data-stu-id="e827c-113">Create a struct to format the search results</span></span>

<span data-ttu-id="e827c-114">The `BingAnswer` struct formats the data provided in the response.</span><span class="sxs-lookup"><span data-stu-id="e827c-114">The `BingAnswer` struct formats the data provided in the response.</span></span>

```go
// This struct formats the answers provided by the Bing Web Search API.
type BingAnswer struct {
        Type         string `json:"_type"`
        QueryContext struct {
                OriginalQuery string `json:"originalQuery"`
        } `json:"queryContext"`
        WebPages struct {
                WebSearchURL          string `json:"webSearchUrl"`
                TotalEstimatedMatches int    `json:"totalEstimatedMatches"`
                Value                 []struct {
                        ID               string    `json:"id"`
                        Name             string    `json:"name"`
                        URL              string    `json:"url"`
                        IsFamilyFriendly bool      `json:"isFamilyFriendly"`
                        DisplayURL       string    `json:"displayUrl"`
                        Snippet          string    `json:"snippet"`
                        DateLastCrawled  time.Time `json:"dateLastCrawled"`
                        SearchTags       []struct {
                                Name    string `json:"name"`
                                Content string `json:"content"`
                        } `json:"searchTags,omitempty"`
                        About []struct {
                                Name string `json:"name"`
                        } `json:"about,omitempty"`
                } `json:"value"`
        } `json:"webPages"`
        RelatedSearches struct {
                ID    string `json:"id"`
                Value []struct {
                        Text         string `json:"text"`
                        DisplayText  string `json:"displayText"`
                        WebSearchURL string `json:"webSearchUrl"`
                } `json:"value"`
        } `json:"relatedSearches"`
        RankingResponse struct {
                Mainline struct {
                        Items []struct {
                                AnswerType  string `json:"answerType"`
                                ResultIndex int    `json:"resultIndex"`
                                Value       struct {
                                        ID string `json:"id"`
                                } `json:"value"`
                        } `json:"items"`
                } `json:"mainline"`
                Sidebar struct {
                        Items []struct {
                                AnswerType string `json:"answerType"`
                                Value      struct {
                                        ID string `json:"id"`
                                } `json:"value"`
                        } `json:"items"`
                } `json:"sidebar"`
        } `json:"rankingResponse"`
}
```

## <a name="declare-the-main-function-and-define-variables"></a><span data-ttu-id="e827c-115">Declare the main function and define variables</span><span class="sxs-lookup"><span data-stu-id="e827c-115">Declare the main function and define variables</span></span>  

<span data-ttu-id="e827c-116">This code declares the main function and sets required variables.</span><span class="sxs-lookup"><span data-stu-id="e827c-116">This code declares the main function and sets required variables.</span></span> <span data-ttu-id="e827c-117">Confirm that the endpoint is correct and replace the `token` value with a valid subscription key from your Azure account.</span><span class="sxs-lookup"><span data-stu-id="e827c-117">Confirm that the endpoint is correct and replace the `token` value with a valid subscription key from your Azure account.</span></span> <span data-ttu-id="e827c-118">Feel free to customize the search query by replacing the value for `searchTerm`.</span><span class="sxs-lookup"><span data-stu-id="e827c-118">Feel free to customize the search query by replacing the value for `searchTerm`.</span></span>

```go
// Declare the main function. This is required for all Go programs.
func main() {
// Verify the endpoint URI and replace the token string with a valid subscription key.  
    const endpoint = "https://api.cognitive.microsoft.com/bing/v7.0/search"
    token := "YOUR-ACCESS-KEY"
    searchTerm := "Microsoft Cognitive Services"

// The remaining code in this quickstart goes in the main function.

}
```

## <a name="construct-a-request"></a><span data-ttu-id="e827c-119">Construct a request</span><span class="sxs-lookup"><span data-stu-id="e827c-119">Construct a request</span></span>

<span data-ttu-id="e827c-120">This code declares the HTTP request, inserts the header and payload, and instantiates the client.</span><span class="sxs-lookup"><span data-stu-id="e827c-120">This code declares the HTTP request, inserts the header and payload, and instantiates the client.</span></span>

```go
// Declare a new GET request.
req, err := http.NewRequest("GET", endpoint, nil)
if err != nil {
    panic(err)
}

// Add the payload to the request.  
param := req.URL.Query()
param.Add("q", searchTerm)
req.URL.RawQuery = param.Encode()

// Insert the request header.  
req.Header.Add("Ocp-Apim-Subscription-Key", token)

// Instantiate a client.  
client := new(http.Client)
```

## <a name="make-a-request"></a><span data-ttu-id="e827c-121">Make a request</span><span class="sxs-lookup"><span data-stu-id="e827c-121">Make a request</span></span>

<span data-ttu-id="e827c-122">Use this code to call the Bing Web Search API and close the connection after a response is returned.</span><span class="sxs-lookup"><span data-stu-id="e827c-122">Use this code to call the Bing Web Search API and close the connection after a response is returned.</span></span>

```go
// Send the request to Bing.  
resp, err := client.Do(req)
if err != nil {
    panic(err)
}

// Close the connection.
defer resp.Body.Close()
body, err := ioutil.ReadAll(resp.Body)
if err != nil {
    panic(err)
}
```

## <a name="handle-the-response"></a><span data-ttu-id="e827c-123">Handle the response</span><span class="sxs-lookup"><span data-stu-id="e827c-123">Handle the response</span></span>

<span data-ttu-id="e827c-124">Remember the struct we created earlier?</span><span class="sxs-lookup"><span data-stu-id="e827c-124">Remember the struct we created earlier?</span></span> <span data-ttu-id="e827c-125">We're going to use it to format the response and print the search results.</span><span class="sxs-lookup"><span data-stu-id="e827c-125">We're going to use it to format the response and print the search results.</span></span>

```go
// Create a new answer.  
ans := new(BingAnswer)
err = json.Unmarshal(body, &ans)
if err != nil {
    fmt.Println(err)
}
// Iterate over search results and print the result name and URL.
for _, result := range ans.WebPages.Value {
    fmt.Println(result.Name, "||", result.URL)
}
```

## <a name="put-it-all-together"></a><span data-ttu-id="e827c-126">Put it all together</span><span class="sxs-lookup"><span data-stu-id="e827c-126">Put it all together</span></span>

<span data-ttu-id="e827c-127">The last step is to validate your code and run it!</span><span class="sxs-lookup"><span data-stu-id="e827c-127">The last step is to validate your code and run it!</span></span> <span data-ttu-id="e827c-128">If you'd like to compare your code with ours, here's the complete program:</span><span class="sxs-lookup"><span data-stu-id="e827c-128">If you'd like to compare your code with ours, here's the complete program:</span></span>

```go
package main
import (
    "fmt"
    "net/http"
    "io/ioutil"
    "time"
    "encoding/json"
)

// The is the struct for the data returned by Bing.
type BingAnswer struct {
        Type         string `json:"_type"`
        QueryContext struct {
                OriginalQuery string `json:"originalQuery"`
        } `json:"queryContext"`
        WebPages struct {
                WebSearchURL          string `json:"webSearchUrl"`
                TotalEstimatedMatches int    `json:"totalEstimatedMatches"`
                Value                 []struct {
                        ID               string    `json:"id"`
                        Name             string    `json:"name"`
                        URL              string    `json:"url"`
                        IsFamilyFriendly bool      `json:"isFamilyFriendly"`
                        DisplayURL       string    `json:"displayUrl"`
                        Snippet          string    `json:"snippet"`
                        DateLastCrawled  time.Time `json:"dateLastCrawled"`
                        SearchTags       []struct {
                                Name    string `json:"name"`
                                Content string `json:"content"`
                        } `json:"searchTags,omitempty"`
                        About []struct {
                                Name string `json:"name"`
                        } `json:"about,omitempty"`
                } `json:"value"`
        } `json:"webPages"`
        RelatedSearches struct {
                ID    string `json:"id"`
                Value []struct {
                        Text         string `json:"text"`
                        DisplayText  string `json:"displayText"`
                        WebSearchURL string `json:"webSearchUrl"`
                } `json:"value"`
        } `json:"relatedSearches"`
        RankingResponse struct {
                Mainline struct {
                        Items []struct {
                                AnswerType  string `json:"answerType"`
                                ResultIndex int    `json:"resultIndex"`
                                Value       struct {
                                        ID string `json:"id"`
                                } `json:"value"`
                        } `json:"items"`
                } `json:"mainline"`
                Sidebar struct {
                        Items []struct {
                                AnswerType string `json:"answerType"`
                                Value      struct {
                                        ID string `json:"id"`
                                } `json:"value"`
                        } `json:"items"`
                } `json:"sidebar"`
        } `json:"rankingResponse"`
}

// Verify the endpoint URI and replace the token string with a valid subscription key.  
func main() {
    const endpoint = "https://api.cognitive.microsoft.com/bing/v7.0/search"
    token := "YOUR-ACCESS-KEY"
    searchTerm := "Microsoft Cognitive Services"

    // Declare a new GET request.
    req, err := http.NewRequest("GET", endpoint, nil)
    if err != nil {
        panic(err)
    }

    // Add the payload to the request.  
    param := req.URL.Query()
    param.Add("q", searchTerm)
    req.URL.RawQuery = param.Encode()

    // Insert the request header.  
    req.Header.Add("Ocp-Apim-Subscription-Key", token)

    // Create a new client.  
    client := new(http.Client)

    // Send the request to Bing.  
    resp, err := client.Do(req)
    if err != nil {
        panic(err)
    }

    // Close the response.
    defer resp.Body.Close()
    body, err := ioutil.ReadAll(resp.Body)
    if err != nil {
        panic(err)
    }

    // Create a new answer.  
    ans := new(BingAnswer)
    err = json.Unmarshal(body, &ans)
    if err != nil {
         fmt.Println(err)
    }

    // Iterate over search results and print the result name and URL.
    for _, result := range ans.WebPages.Value {
         fmt.Println(result.Name, "||", result.URL)
    }

}
```

## <a name="sample-response"></a><span data-ttu-id="e827c-129">Sample response</span><span class="sxs-lookup"><span data-stu-id="e827c-129">Sample response</span></span>  

<span data-ttu-id="e827c-130">Responses from the Bing Web Search API are returned as JSON.</span><span class="sxs-lookup"><span data-stu-id="e827c-130">Responses from the Bing Web Search API are returned as JSON.</span></span> <span data-ttu-id="e827c-131">This sample response has been formatted using the `BingAnswer` struct and displays the `result.Name` and `result.URL`.</span><span class="sxs-lookup"><span data-stu-id="e827c-131">This sample response has been formatted using the `BingAnswer` struct and displays the `result.Name` and `result.URL`.</span></span>

```go
Microsoft Cognitive Services || https://www.microsoft.com/cognitive-services
Cognitive Services | Microsoft Azure || https://azure.microsoft.com/services/cognitive-services/
Cognitive Service Try experience | Microsoft Azure || https://azure.microsoft.com/en-us/try/cognitive-services/
What is Microsoft Cognitive Services? | Microsoft Docs || https://docs.microsoft.com/en-us/azure/cognitive-services/Welcome
Microsoft Cognitive Toolkit || https://www.microsoft.com/en-us/cognitive-toolkit/
Microsoft Customers || https://customers.microsoft.com/en-us/search?sq=%22Microsoft%20Cognitive%20Services%22&ff=&p=0&so=story_publish_date%20desc
Microsoft Enterprise Services - Microsoft Enterprise || https://enterprise.microsoft.com/en-us/services/
Microsoft Cognitive Services || https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236
Cognitive Services - msdn.microsoft.com || https://msdn.microsoft.com/en-us/magazine/mt742868.aspx  
```

## <a name="next-steps"></a><span data-ttu-id="e827c-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="e827c-132">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e827c-133">Bing Web search single-page app tutorial</span><span class="sxs-lookup"><span data-stu-id="e827c-133">Bing Web search single-page app tutorial</span></span>](../tutorial-bing-web-search-single-page-app.md)

[!INCLUDE [bing-web-search-quickstart-see-also](../../../../includes/bing-web-search-quickstart-see-also.md)]
