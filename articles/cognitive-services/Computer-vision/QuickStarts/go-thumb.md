---
title: 'Quickstart: Generate a thumbnail - REST, Go - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you generate a thumbnail from an image using Computer Vision with Go in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 4b9e8fb97b5d389e9113a549152eceaa49b60811
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866922"
---
# <a name="quickstart-generate-a-thumbnail---rest-go---computer-vision"></a><span data-ttu-id="09006-103">Quickstart: Generate a thumbnail - REST, Go - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="09006-103">Quickstart: Generate a thumbnail - REST, Go - Computer Vision</span></span>

<span data-ttu-id="09006-104">In this quickstart, you generate a thumbnail from an image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="09006-104">In this quickstart, you generate a thumbnail from an image using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09006-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="09006-105">Prerequisites</span></span>

<span data-ttu-id="09006-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="09006-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="get-thumbnail-request"></a><span data-ttu-id="09006-107">Get Thumbnail request</span><span class="sxs-lookup"><span data-stu-id="09006-107">Get Thumbnail request</span></span>

<span data-ttu-id="09006-108">With the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb), you can generate a thumbnail of an image.</span><span class="sxs-lookup"><span data-stu-id="09006-108">With the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb), you can generate a thumbnail of an image.</span></span> <span data-ttu-id="09006-109">You specify the height and width, which can differ from the aspect ratio of the input image.</span><span class="sxs-lookup"><span data-stu-id="09006-109">You specify the height and width, which can differ from the aspect ratio of the input image.</span></span> <span data-ttu-id="09006-110">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span><span class="sxs-lookup"><span data-stu-id="09006-110">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span></span>

<span data-ttu-id="09006-111">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="09006-111">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="09006-112">Copy the following code into an editor.</span><span class="sxs-lookup"><span data-stu-id="09006-112">Copy the following code into an editor.</span></span>
1. <span data-ttu-id="09006-113">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="09006-113">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="09006-114">Change the `uriBase` value to the location where you got your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="09006-114">Change the `uriBase` value to the location where you got your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="09006-115">Optionally, change the `imageUrl` value to the image you want to analyze.</span><span class="sxs-lookup"><span data-stu-id="09006-115">Optionally, change the `imageUrl` value to the image you want to analyze.</span></span>
1. <span data-ttu-id="09006-116">Save the file with a `.go` extension.</span><span class="sxs-lookup"><span data-stu-id="09006-116">Save the file with a `.go` extension.</span></span>
1. <span data-ttu-id="09006-117">Open a command prompt on a computer with Go installed.</span><span class="sxs-lookup"><span data-stu-id="09006-117">Open a command prompt on a computer with Go installed.</span></span>
1. <span data-ttu-id="09006-118">Build the file, for example: `go build get-thumbnail.go`.</span><span class="sxs-lookup"><span data-stu-id="09006-118">Build the file, for example: `go build get-thumbnail.go`.</span></span>
1. <span data-ttu-id="09006-119">Run the file, for example: `get-thumbnail`.</span><span class="sxs-lookup"><span data-stu-id="09006-119">Run the file, for example: `get-thumbnail`.</span></span>

```go
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
    // For example, subscriptionKey = "0123456789abcdef0123456789ABCDEF"
    const subscriptionKey = "<Subscription Key>"

    // You must use the same location in your REST call as you used to get your
    // subscription keys. For example, if you got your subscription keys from
    // westus, replace "westcentralus" in the URL below with "westus".
    const uriBase =
        "https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail"
    const imageUrl =
        "https://upload.wikimedia.org/wikipedia/commons/9/94/Bloodhound_Puppy.jpg"

    const params = "?width=100&height=100&smartCropping=true"
    const uri = uriBase + params
    const imageUrlEnc = "{\"url\":\"" + imageUrl + "\"}"

    reader := strings.NewReader(imageUrlEnc)

    // Create the Http client
    client := &http.Client{
        Timeout: time.Second * 2,
    }

    // Create the Post request, passing the image URL in the request body
    req, err := http.NewRequest("POST", uri, reader)
    if err != nil {
        panic(err)
    }

    // Add headers
    req.Header.Add("Content-Type", "application/json")
    req.Header.Add("Ocp-Apim-Subscription-Key", subscriptionKey)

    // Send the request and retrieve the response
    resp, err := client.Do(req)
    if err != nil {
        panic(err)
    }

    defer resp.Body.Close()

    // Read the response body.
    // Note, data is a byte array
    data, err := ioutil.ReadAll(resp.Body)
    if err != nil {
        panic(err)
    }

    // Parse the Json data
    var f interface{}
    json.Unmarshal(data, &f)

    // Format and display the Json result
    jsonFormatted, _ := json.MarshalIndent(f, "", "  ")
    fmt.Println(string(jsonFormatted))
}
```

## <a name="get-thumbnail-response"></a><span data-ttu-id="09006-120">Get Thumbnail response</span><span class="sxs-lookup"><span data-stu-id="09006-120">Get Thumbnail response</span></span>

<span data-ttu-id="09006-121">A successful response contains the thumbnail image binary.</span><span class="sxs-lookup"><span data-stu-id="09006-121">A successful response contains the thumbnail image binary.</span></span> <span data-ttu-id="09006-122">If the request fails, the response contains an error code and a message to help determine what went wrong.</span><span class="sxs-lookup"><span data-stu-id="09006-122">If the request fails, the response contains an error code and a message to help determine what went wrong.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09006-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="09006-123">Next steps</span></span>

<span data-ttu-id="09006-124">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="09006-124">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span> <span data-ttu-id="09006-125">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="09006-125">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="09006-126">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="09006-126">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
