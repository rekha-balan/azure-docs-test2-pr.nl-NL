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
# <a name="moderate-images-from-the-api-console"></a>Moderate images from the API console

Use the [Image Moderation API](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66c) in Azure Content Moderator to initiate scan-and-review moderation workflows for image content. The moderation job scans your content for profanity, and compares it against custom and shared blacklists.

## <a name="use-the-api-console"></a>Use the API console
Before you can test-drive the API in the online console, you need your subscription key. This is located on the **Settings** tab, in the **Ocp-Apim-Subscription-Key** box. For more information, see [Overview](overview.md).

1.  Go to [Image Moderation API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66c).

  The **Image - Evaluate** image moderation page opens.

2. For **Open API testing console**, select the region that most closely describes your location. 

  ![Try Image - Evaluate page region selection](images/test-drive-region.png)
  
  The **Image - Evaluate** API console opens.

3. In the **Ocp-Apim-Subscription-Key** box, enter your subscription key.

  ![Try Image - Evaluate console subscription key](images/try-image-api-1.PNG)

4. In the **Request body** box, use the default sample image, or specify an image to scan. You can submit the image itself as binary bit data, or specify a publicly accessible URL for an image. 

  For this example, use the path provided in the **Request body** box, and then select **Send**. 

   ![Try Image - Evaluate console Request body](images/try-image-api-2.PNG)

  This is the image at that URL:

  ![Try Image - Evaluate console sample image](images/sample-image.jpg) 

5. Select **Send**.

6. The API returns a probability score for each classification. It also returns a determination of whether the image meets the conditions (**true** or **false**). 

  ![Try Image - Evaluate console probability score and condition determination](images/try-image-api-3.PNG)

## <a name="face-detection"></a>Face detection

You can use the Image Moderation API to locate faces in an image. This option can be useful when you have privacy concerns and want to prevent a specific face from being posted on your platform. 

1.  In the [Image Moderation API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66c), in the left menu, under **Image**, select **Find Faces**. 

  The **Image - Find Faces** page opens.

2.  For **Open API testing console**, select the region that most closely describes your location. 

  ![Try Image - Find Faces page region selection](images/test-drive-region.png)

  The **Image - Find Faces** API console opens.

3. Specify an image to scan. You can submit the image itself as binary bit data, or specify a publicly accessible URL to an image. This example links to an image that's used in a CNN story.

  ![Try Image - Find Faces sample image](images/try-image-api-face-image.jpg)

  ![Try Image - Find Faces sample request](images/try-image-api-face-request.png)

4. Select **Send**. In this example, the API finds two faces, and returns their coordinates in the image.

   ![Try Image - Find Faces  sample Response content box](images/try-image-api-face-response.png)

## <a name="text-detection-via-ocr-capability"></a>Text detection via OCR capability

You can use the Content Moderator OCR capability to detect text in images.

1. In the [Image Moderation API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66c), in the left menu, under **Image**, select **OCR**. 

  The **Image - OCR** page opens.

2. For **Open API testing console**, select the region that most closely describes your location. 

  ![Image - OCR page region selection](images/test-drive-region.png)

  The **Image - OCR** API console opens.

3. In the **Ocp-Apim-Subscription-Key** box, enter your subscription key.

4. In the **Request body** box, use the default sample image. This is the same image that's used in the preceding section.

5. Select **Send**. The extracted text is displayed in JSON:

  ![Image - OCR sample Response content box](images/try-image-api-ocr.PNG)

## <a name="next-steps"></a>Next steps

Use the REST API in your code or start with the [image moderation .NET quickstart](image-moderation-quickstart-dotnet.md) to integrate with your application.
