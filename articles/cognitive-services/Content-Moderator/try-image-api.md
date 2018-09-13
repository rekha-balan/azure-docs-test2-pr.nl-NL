---
title: Moderate images with Azure Content Moderator | Microsoft Docs
description: Test-drive image moderation in the Content Moderator API console.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 08/05/2017
ms.author: sajagtap
ms.openlocfilehash: fec54826c70ae10e56c68406f629c56639985295
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871139"
---
# <a name="moderate-images-from-the-api-console"></a><span data-ttu-id="92387-103">Moderate images from the API console</span><span class="sxs-lookup"><span data-stu-id="92387-103">Moderate images from the API console</span></span>

<span data-ttu-id="92387-104">Use the [Image Moderation API](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66c) in Azure Content Moderator to initiate scan-and-review moderation workflows for image content.</span><span class="sxs-lookup"><span data-stu-id="92387-104">Use the [Image Moderation API](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66c) in Azure Content Moderator to initiate scan-and-review moderation workflows for image content.</span></span> <span data-ttu-id="92387-105">The moderation job scans your content for profanity, and compares it against custom and shared blacklists.</span><span class="sxs-lookup"><span data-stu-id="92387-105">The moderation job scans your content for profanity, and compares it against custom and shared blacklists.</span></span>

## <a name="use-the-api-console"></a><span data-ttu-id="92387-106">Use the API console</span><span class="sxs-lookup"><span data-stu-id="92387-106">Use the API console</span></span>
<span data-ttu-id="92387-107">Before you can test-drive the API in the online console, you need your subscription key.</span><span class="sxs-lookup"><span data-stu-id="92387-107">Before you can test-drive the API in the online console, you need your subscription key.</span></span> <span data-ttu-id="92387-108">This is located on the **Settings** tab, in the **Ocp-Apim-Subscription-Key** box.</span><span class="sxs-lookup"><span data-stu-id="92387-108">This is located on the **Settings** tab, in the **Ocp-Apim-Subscription-Key** box.</span></span> <span data-ttu-id="92387-109">For more information, see [Overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="92387-109">For more information, see [Overview](overview.md).</span></span>

1.  <span data-ttu-id="92387-110">Go to [Image Moderation API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66c).</span><span class="sxs-lookup"><span data-stu-id="92387-110">Go to [Image Moderation API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66c).</span></span>

  <span data-ttu-id="92387-111">The **Image - Evaluate** image moderation page opens.</span><span class="sxs-lookup"><span data-stu-id="92387-111">The **Image - Evaluate** image moderation page opens.</span></span>

2. <span data-ttu-id="92387-112">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="92387-112">For **Open API testing console**, select the region that most closely describes your location.</span></span> 

  ![Try Image - Evaluate page region selection](images/test-drive-region.png)
  
  <span data-ttu-id="92387-114">The **Image - Evaluate** API console opens.</span><span class="sxs-lookup"><span data-stu-id="92387-114">The **Image - Evaluate** API console opens.</span></span>

3. <span data-ttu-id="92387-115">In the **Ocp-Apim-Subscription-Key** box, enter your subscription key.</span><span class="sxs-lookup"><span data-stu-id="92387-115">In the **Ocp-Apim-Subscription-Key** box, enter your subscription key.</span></span>

  ![Try Image - Evaluate console subscription key](images/try-image-api-1.PNG)

4. <span data-ttu-id="92387-117">In the **Request body** box, use the default sample image, or specify an image to scan.</span><span class="sxs-lookup"><span data-stu-id="92387-117">In the **Request body** box, use the default sample image, or specify an image to scan.</span></span> <span data-ttu-id="92387-118">You can submit the image itself as binary bit data, or specify a publicly accessible URL for an image.</span><span class="sxs-lookup"><span data-stu-id="92387-118">You can submit the image itself as binary bit data, or specify a publicly accessible URL for an image.</span></span> 

  <span data-ttu-id="92387-119">For this example, use the path provided in the **Request body** box, and then select **Send**.</span><span class="sxs-lookup"><span data-stu-id="92387-119">For this example, use the path provided in the **Request body** box, and then select **Send**.</span></span> 

   ![Try Image - Evaluate console Request body](images/try-image-api-2.PNG)

  <span data-ttu-id="92387-121">This is the image at that URL:</span><span class="sxs-lookup"><span data-stu-id="92387-121">This is the image at that URL:</span></span>

  ![Try Image - Evaluate console sample image](images/sample-image.jpg) 

5. <span data-ttu-id="92387-123">Select **Send**.</span><span class="sxs-lookup"><span data-stu-id="92387-123">Select **Send**.</span></span>

6. <span data-ttu-id="92387-124">The API returns a probability score for each classification.</span><span class="sxs-lookup"><span data-stu-id="92387-124">The API returns a probability score for each classification.</span></span> <span data-ttu-id="92387-125">It also returns a determination of whether the image meets the conditions (**true** or **false**).</span><span class="sxs-lookup"><span data-stu-id="92387-125">It also returns a determination of whether the image meets the conditions (**true** or **false**).</span></span> 

  ![Try Image - Evaluate console probability score and condition determination](images/try-image-api-3.PNG)

## <a name="face-detection"></a><span data-ttu-id="92387-127">Face detection</span><span class="sxs-lookup"><span data-stu-id="92387-127">Face detection</span></span>

<span data-ttu-id="92387-128">You can use the Image Moderation API to locate faces in an image.</span><span class="sxs-lookup"><span data-stu-id="92387-128">You can use the Image Moderation API to locate faces in an image.</span></span> <span data-ttu-id="92387-129">This option can be useful when you have privacy concerns and want to prevent a specific face from being posted on your platform.</span><span class="sxs-lookup"><span data-stu-id="92387-129">This option can be useful when you have privacy concerns and want to prevent a specific face from being posted on your platform.</span></span> 

1.  <span data-ttu-id="92387-130">In the [Image Moderation API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66c), in the left menu, under **Image**, select **Find Faces**.</span><span class="sxs-lookup"><span data-stu-id="92387-130">In the [Image Moderation API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66c), in the left menu, under **Image**, select **Find Faces**.</span></span> 

  <span data-ttu-id="92387-131">The **Image - Find Faces** page opens.</span><span class="sxs-lookup"><span data-stu-id="92387-131">The **Image - Find Faces** page opens.</span></span>

2.  <span data-ttu-id="92387-132">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="92387-132">For **Open API testing console**, select the region that most closely describes your location.</span></span> 

  ![Try Image - Find Faces page region selection](images/test-drive-region.png)

  <span data-ttu-id="92387-134">The **Image - Find Faces** API console opens.</span><span class="sxs-lookup"><span data-stu-id="92387-134">The **Image - Find Faces** API console opens.</span></span>

3. <span data-ttu-id="92387-135">Specify an image to scan.</span><span class="sxs-lookup"><span data-stu-id="92387-135">Specify an image to scan.</span></span> <span data-ttu-id="92387-136">You can submit the image itself as binary bit data, or specify a publicly accessible URL to an image.</span><span class="sxs-lookup"><span data-stu-id="92387-136">You can submit the image itself as binary bit data, or specify a publicly accessible URL to an image.</span></span> <span data-ttu-id="92387-137">This example links to an image that's used in a CNN story.</span><span class="sxs-lookup"><span data-stu-id="92387-137">This example links to an image that's used in a CNN story.</span></span>

  ![Try Image - Find Faces sample image](images/try-image-api-face-image.jpg)

  ![Try Image - Find Faces sample request](images/try-image-api-face-request.png)

4. <span data-ttu-id="92387-140">Select **Send**.</span><span class="sxs-lookup"><span data-stu-id="92387-140">Select **Send**.</span></span> <span data-ttu-id="92387-141">In this example, the API finds two faces, and returns their coordinates in the image.</span><span class="sxs-lookup"><span data-stu-id="92387-141">In this example, the API finds two faces, and returns their coordinates in the image.</span></span>

   ![Try Image - Find Faces  sample Response content box](images/try-image-api-face-response.png)

## <a name="text-detection-via-ocr-capability"></a><span data-ttu-id="92387-143">Text detection via OCR capability</span><span class="sxs-lookup"><span data-stu-id="92387-143">Text detection via OCR capability</span></span>

<span data-ttu-id="92387-144">You can use the Content Moderator OCR capability to detect text in images.</span><span class="sxs-lookup"><span data-stu-id="92387-144">You can use the Content Moderator OCR capability to detect text in images.</span></span>

1. <span data-ttu-id="92387-145">In the [Image Moderation API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66c), in the left menu, under **Image**, select **OCR**.</span><span class="sxs-lookup"><span data-stu-id="92387-145">In the [Image Moderation API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66c), in the left menu, under **Image**, select **OCR**.</span></span> 

  <span data-ttu-id="92387-146">The **Image - OCR** page opens.</span><span class="sxs-lookup"><span data-stu-id="92387-146">The **Image - OCR** page opens.</span></span>

2. <span data-ttu-id="92387-147">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="92387-147">For **Open API testing console**, select the region that most closely describes your location.</span></span> 

  ![Image - OCR page region selection](images/test-drive-region.png)

  <span data-ttu-id="92387-149">The **Image - OCR** API console opens.</span><span class="sxs-lookup"><span data-stu-id="92387-149">The **Image - OCR** API console opens.</span></span>

3. <span data-ttu-id="92387-150">In the **Ocp-Apim-Subscription-Key** box, enter your subscription key.</span><span class="sxs-lookup"><span data-stu-id="92387-150">In the **Ocp-Apim-Subscription-Key** box, enter your subscription key.</span></span>

4. <span data-ttu-id="92387-151">In the **Request body** box, use the default sample image.</span><span class="sxs-lookup"><span data-stu-id="92387-151">In the **Request body** box, use the default sample image.</span></span> <span data-ttu-id="92387-152">This is the same image that's used in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="92387-152">This is the same image that's used in the preceding section.</span></span>

5. <span data-ttu-id="92387-153">Select **Send**.</span><span class="sxs-lookup"><span data-stu-id="92387-153">Select **Send**.</span></span> <span data-ttu-id="92387-154">The extracted text is displayed in JSON:</span><span class="sxs-lookup"><span data-stu-id="92387-154">The extracted text is displayed in JSON:</span></span>

  ![Image - OCR sample Response content box](images/try-image-api-ocr.PNG)

## <a name="next-steps"></a><span data-ttu-id="92387-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="92387-156">Next steps</span></span>

<span data-ttu-id="92387-157">Use the REST API in your code or start with the [image moderation .NET quickstart](image-moderation-quickstart-dotnet.md) to integrate with your application.</span><span class="sxs-lookup"><span data-stu-id="92387-157">Use the REST API in your code or start with the [image moderation .NET quickstart](image-moderation-quickstart-dotnet.md) to integrate with your application.</span></span>
