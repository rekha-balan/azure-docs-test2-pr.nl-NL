---
title: Computer Vision quickstart summary | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In these quickstarts, you analyze an image, create a thumbnail, and extract printed and handwritten text using Computer Vision in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 94424de3f175e82cf8490bad98f4a775761979e4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966133"
---
# <a name="quickstart-summary"></a><span data-ttu-id="a6e2e-103">Quickstart: Summary</span><span class="sxs-lookup"><span data-stu-id="a6e2e-103">Quickstart: Summary</span></span>

<span data-ttu-id="a6e2e-104">These quickstarts provide information and code samples to help you quickly get started using the Computer Vision service.</span><span class="sxs-lookup"><span data-stu-id="a6e2e-104">These quickstarts provide information and code samples to help you quickly get started using the Computer Vision service.</span></span>

<span data-ttu-id="a6e2e-105">The samples make direct HTTP calls to the Computer Vision API.</span><span class="sxs-lookup"><span data-stu-id="a6e2e-105">The samples make direct HTTP calls to the Computer Vision API.</span></span> <span data-ttu-id="a6e2e-106">See the *SDK Quickstarts* section for samples using the Computer Vision client libraries, which provide convenience methods that wrap the HTTP calls.</span><span class="sxs-lookup"><span data-stu-id="a6e2e-106">See the *SDK Quickstarts* section for samples using the Computer Vision client libraries, which provide convenience methods that wrap the HTTP calls.</span></span>

<span data-ttu-id="a6e2e-107">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="a6e2e-107">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

<span data-ttu-id="a6e2e-108">You can use the Computer Vision service to accomplish the following tasks:</span><span class="sxs-lookup"><span data-stu-id="a6e2e-108">You can use the Computer Vision service to accomplish the following tasks:</span></span>

* <span data-ttu-id="a6e2e-109">Analyze a remote image</span><span class="sxs-lookup"><span data-stu-id="a6e2e-109">Analyze a remote image</span></span>
* <span data-ttu-id="a6e2e-110">Analyze a local image</span><span class="sxs-lookup"><span data-stu-id="a6e2e-110">Analyze a local image</span></span>
* <span data-ttu-id="a6e2e-111">Detect celebrities and landmarks (domain models)</span><span class="sxs-lookup"><span data-stu-id="a6e2e-111">Detect celebrities and landmarks (domain models)</span></span>
* <span data-ttu-id="a6e2e-112">Intelligently generate a thumbnail</span><span class="sxs-lookup"><span data-stu-id="a6e2e-112">Intelligently generate a thumbnail</span></span>
* <span data-ttu-id="a6e2e-113">Detect and extract printed text (OCR) from an image</span><span class="sxs-lookup"><span data-stu-id="a6e2e-113">Detect and extract printed text (OCR) from an image</span></span>
* <span data-ttu-id="a6e2e-114">Detect and extract handwritten text from an image</span><span class="sxs-lookup"><span data-stu-id="a6e2e-114">Detect and extract handwritten text from an image</span></span>

<span data-ttu-id="a6e2e-115">The code in each sample is similar.</span><span class="sxs-lookup"><span data-stu-id="a6e2e-115">The code in each sample is similar.</span></span> <span data-ttu-id="a6e2e-116">However, they highlight different Computer Vision features along with different techniques for exchanging data with the service, such as:</span><span class="sxs-lookup"><span data-stu-id="a6e2e-116">However, they highlight different Computer Vision features along with different techniques for exchanging data with the service, such as:</span></span>

* <span data-ttu-id="a6e2e-117">_Generate a thumbnail_ returns an image as a byte array in the body of the response.</span><span class="sxs-lookup"><span data-stu-id="a6e2e-117">_Generate a thumbnail_ returns an image as a byte array in the body of the response.</span></span>
* <span data-ttu-id="a6e2e-118">_Analyze a local image_ requires the image to be included in the request as a byte array.</span><span class="sxs-lookup"><span data-stu-id="a6e2e-118">_Analyze a local image_ requires the image to be included in the request as a byte array.</span></span>
* <span data-ttu-id="a6e2e-119">_Extract handwritten text_ requires two calls to retrieve the text.</span><span class="sxs-lookup"><span data-stu-id="a6e2e-119">_Extract handwritten text_ requires two calls to retrieve the text.</span></span>

## <a name="summary"></a><span data-ttu-id="a6e2e-120">Summary</span><span class="sxs-lookup"><span data-stu-id="a6e2e-120">Summary</span></span>

| <span data-ttu-id="a6e2e-121">Quickstart</span><span class="sxs-lookup"><span data-stu-id="a6e2e-121">Quickstart</span></span>               | <span data-ttu-id="a6e2e-122">Request Parameters</span><span class="sxs-lookup"><span data-stu-id="a6e2e-122">Request Parameters</span></span>                          | <span data-ttu-id="a6e2e-123">Response</span><span class="sxs-lookup"><span data-stu-id="a6e2e-123">Response</span></span>          |
| ------------------------ | ------------------------------------------- | ----------------  |
| <span data-ttu-id="a6e2e-124">Analyze a remote image</span><span class="sxs-lookup"><span data-stu-id="a6e2e-124">Analyze a remote image</span></span>   | <span data-ttu-id="a6e2e-125">visualFeatures=Categories,Description,Color</span><span class="sxs-lookup"><span data-stu-id="a6e2e-125">visualFeatures=Categories,Description,Color</span></span> | <span data-ttu-id="a6e2e-126">JSON string</span><span class="sxs-lookup"><span data-stu-id="a6e2e-126">JSON string</span></span>       |
| <span data-ttu-id="a6e2e-127">Analyze a local image</span><span class="sxs-lookup"><span data-stu-id="a6e2e-127">Analyze a local image</span></span>    | <span data-ttu-id="a6e2e-128">data=image_data (byte array)</span><span class="sxs-lookup"><span data-stu-id="a6e2e-128">data=image_data (byte array)</span></span>                | <span data-ttu-id="a6e2e-129">JSON string</span><span class="sxs-lookup"><span data-stu-id="a6e2e-129">JSON string</span></span>       |
| <span data-ttu-id="a6e2e-130">Detect celebrities</span><span class="sxs-lookup"><span data-stu-id="a6e2e-130">Detect celebrities</span></span>       | <span data-ttu-id="a6e2e-131">model=celebrities</span><span class="sxs-lookup"><span data-stu-id="a6e2e-131">model=celebrities</span></span>                           | <span data-ttu-id="a6e2e-132">JSON string</span><span class="sxs-lookup"><span data-stu-id="a6e2e-132">JSON string</span></span>       |
| <span data-ttu-id="a6e2e-133">Generate a thumbnail</span><span class="sxs-lookup"><span data-stu-id="a6e2e-133">Generate a thumbnail</span></span>     | <span data-ttu-id="a6e2e-134">width=200&height=150&smartCropping=true</span><span class="sxs-lookup"><span data-stu-id="a6e2e-134">width=200&height=150&smartCropping=true</span></span>     | <span data-ttu-id="a6e2e-135">byte array</span><span class="sxs-lookup"><span data-stu-id="a6e2e-135">byte array</span></span>        |
| <span data-ttu-id="a6e2e-136">Extract printed text</span><span class="sxs-lookup"><span data-stu-id="a6e2e-136">Extract printed text</span></span>     | <span data-ttu-id="a6e2e-137">language=unk&detectOrientation=true</span><span class="sxs-lookup"><span data-stu-id="a6e2e-137">language=unk&detectOrientation=true</span></span>         | <span data-ttu-id="a6e2e-138">JSON string</span><span class="sxs-lookup"><span data-stu-id="a6e2e-138">JSON string</span></span>       |
| <span data-ttu-id="a6e2e-139">Extract handwritten text</span><span class="sxs-lookup"><span data-stu-id="a6e2e-139">Extract handwritten text</span></span> | <span data-ttu-id="a6e2e-140">handwriting=true</span><span class="sxs-lookup"><span data-stu-id="a6e2e-140">handwriting=true</span></span>                            | <span data-ttu-id="a6e2e-141">URL, JSON string</span><span class="sxs-lookup"><span data-stu-id="a6e2e-141">URL, JSON string</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="a6e2e-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6e2e-142">Next steps</span></span>

<span data-ttu-id="a6e2e-143">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="a6e2e-143">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a6e2e-144">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="a6e2e-144">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
