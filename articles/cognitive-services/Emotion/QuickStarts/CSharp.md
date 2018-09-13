---
title: Emotion API C# quick start | Microsoft Docs
description: Get information and a code sample to help you quickly get started using the Emotion API with C# in Cognitive Services.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: emotion
ms.topic: article
ms.date: 02/20/2017
ms.author: anroth
ms.openlocfilehash: 019c5a0396cbc064c4ddfba4dd8f5ea19d12ca2a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540906"
---
# <a name="emotion-api-c-quick-start"></a><span data-ttu-id="c9204-103">Emotion API C# Quick Start</span><span class="sxs-lookup"><span data-stu-id="c9204-103">Emotion API C# Quick Start</span></span>
<span data-ttu-id="c9204-104">This article provides information and a code sample to help you quickly get started using the [Emotion API Recognize method](https://dev.projectoxford.ai/docs/services/5639d931ca73072154c1ce89/operations/563b31ea778daf121cc3a5fa) with C# to recognize the emotions expressed by one or more people in an image.</span><span class="sxs-lookup"><span data-stu-id="c9204-104">This article provides information and a code sample to help you quickly get started using the [Emotion API Recognize method](https://dev.projectoxford.ai/docs/services/5639d931ca73072154c1ce89/operations/563b31ea778daf121cc3a5fa) with C# to recognize the emotions expressed by one or more people in an image.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c9204-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c9204-105">Prerequisites</span></span>
* <span data-ttu-id="c9204-106">Get the Microsoft Cognitive Emotion API Windows SDK [here](https://www.nuget.org/packages/Microsoft.ProjectOxford.Emotion/)</span><span class="sxs-lookup"><span data-stu-id="c9204-106">Get the Microsoft Cognitive Emotion API Windows SDK [here](https://www.nuget.org/packages/Microsoft.ProjectOxford.Emotion/)</span></span>
* <span data-ttu-id="c9204-107">Get your free Subscription Key [here](https://www.microsoft.com/cognitive-services/en-us/sign-up)</span><span class="sxs-lookup"><span data-stu-id="c9204-107">Get your free Subscription Key [here](https://www.microsoft.com/cognitive-services/en-us/sign-up)</span></span>

## <a name="emotion-recognition-c-example-request"></a><span data-ttu-id="c9204-108">Emotion Recognition C# Example Request</span><span class="sxs-lookup"><span data-stu-id="c9204-108">Emotion Recognition C# Example Request</span></span>

```c#
using System;
using System.IO;
using System.Net.Http.Headers;
using System.Net.Http;

namespace CSHttpClientSample
{
    static class Program
    {
        static void Main()
        {
            Console.Write("Enter the path to a JPEG image file:");
            string imageFilePath = Console.ReadLine();

            MakeRequest(imageFilePath);

            Console.WriteLine("\n\n\nWait for the result below, then hit ENTER to exit...\n\n\n");
            Console.ReadLine();
        }

        static byte[] GetImageAsByteArray(string imageFilePath)
        {
            FileStream fileStream = new FileStream(imageFilePath, FileMode.Open, FileAccess.Read);
            BinaryReader binaryReader = new BinaryReader(fileStream);
            return binaryReader.ReadBytes((int)fileStream.Length);
        }

        static async void MakeRequest(string imageFilePath)
        {
            var client = new HttpClient();

            // Request headers
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", "40d7576afa7e4f82b38315516d55cb5e");

            string uri = "https://westus.api.cognitive.microsoft.com/emotion/v1.0/recognize?";
            HttpResponseMessage response;
            string responseContent;

            // Request body. Try this sample with a locally stored JPEG image.
            byte[] byteData = GetImageAsByteArray(imageFilePath);

            using (var content = new ByteArrayContent(byteData))
            {
                // This example uses content type "application/octet-stream".
                // The other content types you can use are "application/json" and "multipart/form-data".
                content.Headers.ContentType = new MediaTypeHeaderValue("application/octet-stream");
                response = await client.PostAsync(uri, content);
                responseContent = response.Content.ReadAsStringAsync().Result;
            }

            //A peak at the JSON response.
            Console.WriteLine(responseContent);
        }
    }
}
```

## <a name="recognize-emotions-sample-response"></a><span data-ttu-id="c9204-109">Recognize Emotions Sample Response</span><span class="sxs-lookup"><span data-stu-id="c9204-109">Recognize Emotions Sample Response</span></span>
<span data-ttu-id="c9204-110">A successful call returns an array of face entries and their associated emotion scores, ranked by face rectangle size in descending order.</span><span class="sxs-lookup"><span data-stu-id="c9204-110">A successful call returns an array of face entries and their associated emotion scores, ranked by face rectangle size in descending order.</span></span> <span data-ttu-id="c9204-111">An empty response indicates that no faces were detected.</span><span class="sxs-lookup"><span data-stu-id="c9204-111">An empty response indicates that no faces were detected.</span></span> <span data-ttu-id="c9204-112">An emotion entry contains the following fields:</span><span class="sxs-lookup"><span data-stu-id="c9204-112">An emotion entry contains the following fields:</span></span>
* <span data-ttu-id="c9204-113">faceRectangle - Rectangle location of face in the image.</span><span class="sxs-lookup"><span data-stu-id="c9204-113">faceRectangle - Rectangle location of face in the image.</span></span>
* <span data-ttu-id="c9204-114">scores - Emotion scores for each face in the image.</span><span class="sxs-lookup"><span data-stu-id="c9204-114">scores - Emotion scores for each face in the image.</span></span> 

```json
application/json 
[
  {
    "faceRectangle": {
      "left": 68,
      "top": 97,
      "width": 64,
      "height": 97
    },
    "scores": {
      "anger": 0.00300731952,
      "contempt": 5.14648448E-08,
      "disgust": 9.180124E-06,
      "fear": 0.0001912825,
      "happiness": 0.9875571,
      "neutral": 0.0009861537,
      "sadness": 1.889955E-05,
      "surprise": 0.008229999
    }
  }
]
