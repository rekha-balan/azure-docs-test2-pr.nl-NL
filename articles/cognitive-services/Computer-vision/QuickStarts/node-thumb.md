---
title: 'Quickstart: Generate a thumbnail - REST, Node.js - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you generate a thumbnail from an image using Computer Vision with Node.js in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: ebc9c89969641ace679b3d6677efd67138424712
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866654"
---
# <a name="quickstart-generate-a-thumbnail---rest-nodejs---computer-vision"></a><span data-ttu-id="a33d7-103">Quickstart: Generate a thumbnail - REST, Node.js - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="a33d7-103">Quickstart: Generate a thumbnail - REST, Node.js - Computer Vision</span></span>

<span data-ttu-id="a33d7-104">In this quickstart, you generate a thumbnail from an image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="a33d7-104">In this quickstart, you generate a thumbnail from an image using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a33d7-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a33d7-105">Prerequisites</span></span>

<span data-ttu-id="a33d7-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="a33d7-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="get-thumbnail-request"></a><span data-ttu-id="a33d7-107">Get Thumbnail request</span><span class="sxs-lookup"><span data-stu-id="a33d7-107">Get Thumbnail request</span></span>

<span data-ttu-id="a33d7-108">With the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb), you can generate a thumbnail of an image.</span><span class="sxs-lookup"><span data-stu-id="a33d7-108">With the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb), you can generate a thumbnail of an image.</span></span> <span data-ttu-id="a33d7-109">You specify the height and width, which can differ from the aspect ratio of the input image.</span><span class="sxs-lookup"><span data-stu-id="a33d7-109">You specify the height and width, which can differ from the aspect ratio of the input image.</span></span> <span data-ttu-id="a33d7-110">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span><span class="sxs-lookup"><span data-stu-id="a33d7-110">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span></span>

<span data-ttu-id="a33d7-111">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="a33d7-111">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="a33d7-112">Copy the following code into an editor.</span><span class="sxs-lookup"><span data-stu-id="a33d7-112">Copy the following code into an editor.</span></span>
1. <span data-ttu-id="a33d7-113">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="a33d7-113">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="a33d7-114">Change the `uriBase` value to the location where you got your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="a33d7-114">Change the `uriBase` value to the location where you got your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="a33d7-115">Optionally, change the `imageUrl` value to the image you want to analyze.</span><span class="sxs-lookup"><span data-stu-id="a33d7-115">Optionally, change the `imageUrl` value to the image you want to analyze.</span></span>
1. <span data-ttu-id="a33d7-116">Save the file with an `.js` extension.</span><span class="sxs-lookup"><span data-stu-id="a33d7-116">Save the file with an `.js` extension.</span></span>
1. <span data-ttu-id="a33d7-117">Open the Node.js command prompt and run the file, for example: `node myfile.js`.</span><span class="sxs-lookup"><span data-stu-id="a33d7-117">Open the Node.js command prompt and run the file, for example: `node myfile.js`.</span></span>

<span data-ttu-id="a33d7-118">This sample uses the npm [request](https://www.npmjs.com/package/request) package.</span><span class="sxs-lookup"><span data-stu-id="a33d7-118">This sample uses the npm [request](https://www.npmjs.com/package/request) package.</span></span>

```nodejs
'use strict';

const request = require('request');

// Replace <Subscription Key> with your valid subscription key.
const subscriptionKey = '<Subscription Key>';

// You must use the same location in your REST call as you used to get your
// subscription keys. For example, if you got your subscription keys from
// westus, replace "westcentralus" in the URL below with "westus".
const uriBase =
    'https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail';

const imageUrl =
    'https://upload.wikimedia.org/wikipedia/commons/9/94/Bloodhound_Puppy.jpg';

// Request parameters.
const params = {
    'width': '100',
    'height': '100',
    'smartCropping': 'true'
};

const options = {
    uri: uriBase,
    qs: params,
    body: '{"url": ' + '"' + imageUrl + '"}',
    headers: {
        'Content-Type': 'application/json',
        'Ocp-Apim-Subscription-Key' : subscriptionKey
    }
};

request.post(options, (error, response, body) => {
  if (error) {
    console.log('Error: ', error);
    return;
  }
});
```

## <a name="get-thumbnail-response"></a><span data-ttu-id="a33d7-119">Get Thumbnail response</span><span class="sxs-lookup"><span data-stu-id="a33d7-119">Get Thumbnail response</span></span>

<span data-ttu-id="a33d7-120">A successful response contains the thumbnail image binary.</span><span class="sxs-lookup"><span data-stu-id="a33d7-120">A successful response contains the thumbnail image binary.</span></span> <span data-ttu-id="a33d7-121">If the request fails, the response contains an error code and a message to help determine what went wrong.</span><span class="sxs-lookup"><span data-stu-id="a33d7-121">If the request fails, the response contains an error code and a message to help determine what went wrong.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a33d7-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="a33d7-122">Next steps</span></span>

<span data-ttu-id="a33d7-123">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="a33d7-123">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span> <span data-ttu-id="a33d7-124">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="a33d7-124">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a33d7-125">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="a33d7-125">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
