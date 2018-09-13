---
title: 'Quickstart: Analyze a remote image - REST, Go - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you analyze an image using Computer Vision with Go in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: d1d9487d614bc2df184227c4679ccf3ae553b9dc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965524"
---
# <a name="quickstart-analyze-a-remote-image---rest-go---computer-vision"></a><span data-ttu-id="c2a20-103">Quickstart: Analyze a remote image - REST, Go - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="c2a20-103">Quickstart: Analyze a remote image - REST, Go - Computer Vision</span></span>

<span data-ttu-id="c2a20-104">In this quickstart, you analyze an image to extract visual features using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="c2a20-104">In this quickstart, you analyze an image to extract visual features using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2a20-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c2a20-105">Prerequisites</span></span>

<span data-ttu-id="c2a20-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="c2a20-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="analyze-image-request"></a><span data-ttu-id="c2a20-107">Analyze Image request</span><span class="sxs-lookup"><span data-stu-id="c2a20-107">Analyze Image request</span></span>

<span data-ttu-id="c2a20-108">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span><span class="sxs-lookup"><span data-stu-id="c2a20-108">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span></span> <span data-ttu-id="c2a20-109">You can upload an image or specify an image URL and choose which features to return, including:</span><span class="sxs-lookup"><span data-stu-id="c2a20-109">You can upload an image or specify an image URL and choose which features to return, including:</span></span>

* <span data-ttu-id="c2a20-110">A detailed list of tags related to the image content.</span><span class="sxs-lookup"><span data-stu-id="c2a20-110">A detailed list of tags related to the image content.</span></span>
* <span data-ttu-id="c2a20-111">A description of image content in a complete sentence.</span><span class="sxs-lookup"><span data-stu-id="c2a20-111">A description of image content in a complete sentence.</span></span>
* <span data-ttu-id="c2a20-112">The coordinates, gender, and age of any faces contained in the image.</span><span class="sxs-lookup"><span data-stu-id="c2a20-112">The coordinates, gender, and age of any faces contained in the image.</span></span>
* <span data-ttu-id="c2a20-113">The ImageType (clip art or a line drawing).</span><span class="sxs-lookup"><span data-stu-id="c2a20-113">The ImageType (clip art or a line drawing).</span></span>
* <span data-ttu-id="c2a20-114">The dominant color, the accent color, or whether an image is black & white.</span><span class="sxs-lookup"><span data-stu-id="c2a20-114">The dominant color, the accent color, or whether an image is black & white.</span></span>
* <span data-ttu-id="c2a20-115">The category defined in this [taxonomy](../Category-Taxonomy.md).</span><span class="sxs-lookup"><span data-stu-id="c2a20-115">The category defined in this [taxonomy](../Category-Taxonomy.md).</span></span>
* <span data-ttu-id="c2a20-116">Does the image contain adult or sexually suggestive content?</span><span class="sxs-lookup"><span data-stu-id="c2a20-116">Does the image contain adult or sexually suggestive content?</span></span>

<span data-ttu-id="c2a20-117">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="c2a20-117">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="c2a20-118">Copy the following code into an editor.</span><span class="sxs-lookup"><span data-stu-id="c2a20-118">Copy the following code into an editor.</span></span>
1. <span data-ttu-id="c2a20-119">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="c2a20-119">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="c2a20-120">Change the `uriBase` value to the location where you got your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="c2a20-120">Change the `uriBase` value to the location where you got your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="c2a20-121">Optionally, change the `imageUrl` value to the image you want to analyze.</span><span class="sxs-lookup"><span data-stu-id="c2a20-121">Optionally, change the `imageUrl` value to the image you want to analyze.</span></span>
1. <span data-ttu-id="c2a20-122">Save the file with a `.go` extension.</span><span class="sxs-lookup"><span data-stu-id="c2a20-122">Save the file with a `.go` extension.</span></span>
1. <span data-ttu-id="c2a20-123">Open a command prompt on a computer with Go installed.</span><span class="sxs-lookup"><span data-stu-id="c2a20-123">Open a command prompt on a computer with Go installed.</span></span>
1. <span data-ttu-id="c2a20-124">Build the file, for example: `go build analyze-image.go`.</span><span class="sxs-lookup"><span data-stu-id="c2a20-124">Build the file, for example: `go build analyze-image.go`.</span></span>
1. <span data-ttu-id="c2a20-125">Run the file, for example: `analyze-image`.</span><span class="sxs-lookup"><span data-stu-id="c2a20-125">Run the file, for example: `analyze-image`.</span></span>

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
        "https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/analyze"
    const imageUrl =
        "http://upload.wikimedia.org/wikipedia/commons/3/3c/Shaki_waterfall.jpg"

    const params = "?visualFeatures=Description&details=Landmarks&language=en"
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

## <a name="analyze-image-response"></a><span data-ttu-id="c2a20-126">Analyze Image response</span><span class="sxs-lookup"><span data-stu-id="c2a20-126">Analyze Image response</span></span>

<span data-ttu-id="c2a20-127">A successful response is returned in JSON, for example:</span><span class="sxs-lookup"><span data-stu-id="c2a20-127">A successful response is returned in JSON, for example:</span></span>

```json
{
  "categories": [
    {
      "detail": {
        "landmarks": []
      },
      "name": "outdoor_water",
      "score": 0.9921875
    }
  ],
  "description": {
    "captions": [
      {
        "confidence": 0.916458423253597,
        "text": "a large waterfall over a rocky cliff"
      }
    ],
    "tags": [
      "nature",
      "water",
      "waterfall",
      "outdoor",
      "rock",
      "mountain",
      "rocky",
      "grass",
      "hill",
      "covered",
      "hillside",
      "standing",
      "side",
      "group",
      "walking",
      "white",
      "man",
      "large",
      "snow",
      "grazing",
      "forest",
      "slope",
      "herd",
      "river",
      "giraffe",
      "field"
    ]
  },
  "metadata": {
    "format": "Jpeg",
    "height": 959,
    "width": 1280
  },
  "requestId": "a92f89ab-51f8-4735-a58d-507da2213fc2"
}
```

## <a name="next-steps"></a><span data-ttu-id="c2a20-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="c2a20-128">Next steps</span></span>

<span data-ttu-id="c2a20-129">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="c2a20-129">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span> <span data-ttu-id="c2a20-130">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="c2a20-130">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c2a20-131">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="c2a20-131">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
