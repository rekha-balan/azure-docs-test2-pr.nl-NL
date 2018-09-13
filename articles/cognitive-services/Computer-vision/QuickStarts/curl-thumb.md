---
title: 'Quickstart: Generate a thumbnail - REST, cURL - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you generate a thumbnail from an image using Computer Vision with cURL in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: ecb973c35a05ca8c246bb10d6fda892b07ab805e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868119"
---
# <a name="quickstart-generate-a-thumbnail---rest-curl---computer-vision"></a><span data-ttu-id="b89b4-103">Quickstart: Generate a thumbnail - REST, cURL - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="b89b4-103">Quickstart: Generate a thumbnail - REST, cURL - Computer Vision</span></span>

<span data-ttu-id="b89b4-104">In this quickstart, you generate a thumbnail from an image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="b89b4-104">In this quickstart, you generate a thumbnail from an image using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b89b4-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b89b4-105">Prerequisites</span></span>

<span data-ttu-id="b89b4-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="b89b4-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="get-thumbnail-request"></a><span data-ttu-id="b89b4-107">Get Thumbnail request</span><span class="sxs-lookup"><span data-stu-id="b89b4-107">Get Thumbnail request</span></span>

<span data-ttu-id="b89b4-108">With the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb), you can generate a thumbnail of an image.</span><span class="sxs-lookup"><span data-stu-id="b89b4-108">With the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb), you can generate a thumbnail of an image.</span></span> <span data-ttu-id="b89b4-109">You specify the height and width, which can differ from the aspect ratio of the input image.</span><span class="sxs-lookup"><span data-stu-id="b89b4-109">You specify the height and width, which can differ from the aspect ratio of the input image.</span></span> <span data-ttu-id="b89b4-110">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span><span class="sxs-lookup"><span data-stu-id="b89b4-110">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span></span>

<span data-ttu-id="b89b4-111">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="b89b4-111">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="b89b4-112">Copy the following code into an editor.</span><span class="sxs-lookup"><span data-stu-id="b89b4-112">Copy the following code into an editor.</span></span>
1. <span data-ttu-id="b89b4-113">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="b89b4-113">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="b89b4-114">Replace `<File>` with the path and filename to save the thumbnail.</span><span class="sxs-lookup"><span data-stu-id="b89b4-114">Replace `<File>` with the path and filename to save the thumbnail.</span></span>
1. <span data-ttu-id="b89b4-115">Change the Request URL (`https://westcentralus.api.cognitive.microsoft.com/vision/v2.0`) to use the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="b89b4-115">Change the Request URL (`https://westcentralus.api.cognitive.microsoft.com/vision/v2.0`) to use the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="b89b4-116">Optionally, change the image (`{\"url\":\"...`) to analyze.</span><span class="sxs-lookup"><span data-stu-id="b89b4-116">Optionally, change the image (`{\"url\":\"...`) to analyze.</span></span>
1. <span data-ttu-id="b89b4-117">Open a command window on a computer with cURL installed.</span><span class="sxs-lookup"><span data-stu-id="b89b4-117">Open a command window on a computer with cURL installed.</span></span>
1. <span data-ttu-id="b89b4-118">Paste the code in the window and run the command.</span><span class="sxs-lookup"><span data-stu-id="b89b4-118">Paste the code in the window and run the command.</span></span>

>[!NOTE]
><span data-ttu-id="b89b4-119">You must use the same location in your REST call as you used to obtain your subscription keys.</span><span class="sxs-lookup"><span data-stu-id="b89b4-119">You must use the same location in your REST call as you used to obtain your subscription keys.</span></span> <span data-ttu-id="b89b4-120">For example, if you obtained your subscription keys from westus, replace "westcentralus" in the URL below with "westus".</span><span class="sxs-lookup"><span data-stu-id="b89b4-120">For example, if you obtained your subscription keys from westus, replace "westcentralus" in the URL below with "westus".</span></span>

```json
curl -H "Ocp-Apim-Subscription-Key: <Subscription Key>" -o <File> -H "Content-Type: application/json" "https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail?width=100&height=100&smartCropping=true" -d "{\"url\":\"https://upload.wikimedia.org/wikipedia/commons/thumb/5/56/Shorkie_Poo_Puppy.jpg/1280px-Shorkie_Poo_Puppy.jpg\"}"
```

## <a name="get-thumbnail-response"></a><span data-ttu-id="b89b4-121">Get Thumbnail response</span><span class="sxs-lookup"><span data-stu-id="b89b4-121">Get Thumbnail response</span></span>

<span data-ttu-id="b89b4-122">A successful response writes the thumbnail image to `<File>`.</span><span class="sxs-lookup"><span data-stu-id="b89b4-122">A successful response writes the thumbnail image to `<File>`.</span></span> <span data-ttu-id="b89b4-123">If the request fails, the response contains an error code and a message to help determine what went wrong.</span><span class="sxs-lookup"><span data-stu-id="b89b4-123">If the request fails, the response contains an error code and a message to help determine what went wrong.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b89b4-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="b89b4-124">Next steps</span></span>

<span data-ttu-id="b89b4-125">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="b89b4-125">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span> <span data-ttu-id="b89b4-126">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="b89b4-126">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b89b4-127">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="b89b4-127">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
