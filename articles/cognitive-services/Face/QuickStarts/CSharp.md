---
title: Face API C# quick start | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Face API with C# in Cognitive Services.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: face
ms.topic: article
ms.date: 03/21/2017
ms.author: anroth
ms.openlocfilehash: 2939fde83ee4f5cc79c5eef3703c92829c749c1a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556487"
---
# <a name="face-api-c-quick-starts"></a><span data-ttu-id="03ad5-103">Face API C# Quick Starts</span><span class="sxs-lookup"><span data-stu-id="03ad5-103">Face API C# Quick Starts</span></span>
<span data-ttu-id="03ad5-104">This article provides information and code samples to help you quickly get started using the Face API with C# to accomplish the following tasks:</span><span class="sxs-lookup"><span data-stu-id="03ad5-104">This article provides information and code samples to help you quickly get started using the Face API with C# to accomplish the following tasks:</span></span> 
* [<span data-ttu-id="03ad5-105">Detect Faces in Images</span><span class="sxs-lookup"><span data-stu-id="03ad5-105">Detect Faces in Images</span></span>](#Detect) 
* [<span data-ttu-id="03ad5-106">Create a Person Group</span><span class="sxs-lookup"><span data-stu-id="03ad5-106">Create a Person Group</span></span>](#Create)

## <a name="prerequisites"></a><span data-ttu-id="03ad5-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="03ad5-107">Prerequisites</span></span>
* <span data-ttu-id="03ad5-108">Get the Microsoft Face API Windows SDK [here](https://github.com/Microsoft/Cognitive-face-windows)</span><span class="sxs-lookup"><span data-stu-id="03ad5-108">Get the Microsoft Face API Windows SDK [here](https://github.com/Microsoft/Cognitive-face-windows)</span></span>
* <span data-ttu-id="03ad5-109">Learn more about obtaining free Subscription Keys [here](../../Computer-vision/Vision-API-How-to-Topics/HowToSubscribe.md)</span><span class="sxs-lookup"><span data-stu-id="03ad5-109">Learn more about obtaining free Subscription Keys [here](../../Computer-vision/Vision-API-How-to-Topics/HowToSubscribe.md)</span></span>

## <span data-ttu-id="03ad5-110">Detect Faces in Images With Face API Using C# <a name="Detect"> </a></span><span class="sxs-lookup"><span data-stu-id="03ad5-110">Detect Faces in Images With Face API Using C# <a name="Detect"> </a></span></span>
<span data-ttu-id="03ad5-111">Use the [Face - Detect method](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) to detect faces in an image and return face attributes including:</span><span class="sxs-lookup"><span data-stu-id="03ad5-111">Use the [Face - Detect method](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) to detect faces in an image and return face attributes including:</span></span>
* <span data-ttu-id="03ad5-112">Face ID: Unique ID used in a number of Face API scenarios.</span><span class="sxs-lookup"><span data-stu-id="03ad5-112">Face ID: Unique ID used in a number of Face API scenarios.</span></span> 
* <span data-ttu-id="03ad5-113">Face Rectangle: The left, top, width, and height indicating the location of the face in the image.</span><span class="sxs-lookup"><span data-stu-id="03ad5-113">Face Rectangle: The left, top, width, and height indicating the location of the face in the image.</span></span>
* <span data-ttu-id="03ad5-114">Landmarks: An array of 27-point face landmarks pointing to the important positions of face components.</span><span class="sxs-lookup"><span data-stu-id="03ad5-114">Landmarks: An array of 27-point face landmarks pointing to the important positions of face components.</span></span>
* <span data-ttu-id="03ad5-115">Facial attributes including age, gender, smile intensity, head pose, and facial hair.</span><span class="sxs-lookup"><span data-stu-id="03ad5-115">Facial attributes including age, gender, smile intensity, head pose, and facial hair.</span></span> 

#### <a name="face-detect-c-example-request"></a><span data-ttu-id="03ad5-116">Face Detect C# Example Request</span><span class="sxs-lookup"><span data-stu-id="03ad5-116">Face Detect C# Example Request</span></span>
<span data-ttu-id="03ad5-117">The sample is written in C# using the Face API client library.</span><span class="sxs-lookup"><span data-stu-id="03ad5-117">The sample is written in C# using the Face API client library.</span></span> 
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
            Console.Write("Enter the path to the JPEG image with faces to identify:");
            string imageFilePath = Console.ReadLine();

            MakeDetectRequest(imageFilePath);

            Console.WriteLine("\n\n\nWait for the result below, then hit ENTER to exit...\n\n\n");
            Console.ReadLine();
        }

        static byte[] GetImageAsByteArray(string imageFilePath)
        {
            FileStream fileStream = new FileStream(imageFilePath, FileMode.Open, FileAccess.Read);
            BinaryReader binaryReader = new BinaryReader(fileStream);
            return binaryReader.ReadBytes((int)fileStream.Length);
        }

        static async void MakeDetectRequest(string imageFilePath)
        {
            var client = new HttpClient();

            // Request headers - replace this example key with your valid key.
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", "6726adbabb494773a28a7a5a21d5974a");

            // Request parameters and URI string.
            string queryString = "returnFaceId=true&returnFaceLandmarks=false&returnFaceAttributes=age,gender";
            string uri = "https://westus.api.cognitive.microsoft.com/face/v1.0/detect?" + queryString;

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
#### <a name="face---detect-response"></a><span data-ttu-id="03ad5-118">Face - Detect Response</span><span class="sxs-lookup"><span data-stu-id="03ad5-118">Face - Detect Response</span></span>
<span data-ttu-id="03ad5-119">A successful response will be returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="03ad5-119">A successful response will be returned in JSON.</span></span> <span data-ttu-id="03ad5-120">Following is an example of a successful response:</span><span class="sxs-lookup"><span data-stu-id="03ad5-120">Following is an example of a successful response:</span></span> 

```json
[
    {
        "faceId": "c5c24a82-6845-4031-9d5d-978df9175426",
        "faceRectangle": {
            "width": 78,
            "height": 78,
            "left": 394,
            "top": 54
        },
        "faceLandmarks": {
            "pupilLeft": {
                "x": 412.7,
                "y": 78.4 
            },
            "pupilRight": {
                "x": 446.8,
                "y": 74.2 
            },
            "noseTip": {
                "x": 437.7,
                "y": 92.4 
            },
            "mouthLeft": {
                "x": 417.8,
                "y": 114.4 
            },
            "mouthRight": {
                "x": 451.3,
                "y": 109.3 
            },
            "eyebrowLeftOuter": {
                "x": 397.9,
                "y": 78.5 
            },
            "eyebrowLeftInner": {
                "x": 425.4,
                "y": 70.5 
            },
            "eyeLeftOuter": {
                "x": 406.7,
                "y": 80.6 
            },
            "eyeLeftTop": {
                "x": 412.2,
                "y": 76.2 
            },
            "eyeLeftBottom": {
                "x": 413.0,
                "y": 80.1 
            },
            "eyeLeftInner": {
                "x": 418.9,
                "y": 78.0 
            },
            "eyebrowRightInner": {
                "x": 4.8,
                "y": 69.7 
            },
            "eyebrowRightOuter": {
                "x": 5.5,
                "y": 68.5 
            },
            "eyeRightInner": {
                "x": 441.5,
                "y": 75.0 
            },
            "eyeRightTop": {
                "x": 446.4,
                "y": 71.7 
            },
            "eyeRightBottom": {
                "x": 447.0,
                "y": 75.3 
            },
            "eyeRightOuter": {
                "x": 451.7,
                "y": 73.4 
            },
            "noseRootLeft": {
                "x": 428.0,
                "y": 77.1 
            },
            "noseRootRight": {
                "x": 435.8,
                "y": 75.6 
            },
            "noseLeftAlarTop": {
                "x": 428.3,
                "y": 89.7 
            },
            "noseRightAlarTop": {
                "x": 442.2,
                "y": 87.0 
            },
            "noseLeftAlarOutTip": {
                "x": 424.3,
                "y": 96.4 
            },
            "noseRightAlarOutTip": {
                "x": 446.6,
                "y": 92.5 
            },
            "upperLipTop": {
                "x": 437.6,
                "y": 105.9 
            },
            "upperLipBottom": {
                "x": 437.6,
                "y": 108.2 
            },
            "underLipTop": {
                "x": 436.8,
                "y": 111.4 
            },
            "underLipBottom": {
                "x": 437.3,
                "y": 114.5 
            }
        },
        "faceAttributes": {
            "age": 71.0,
            "gender": "male",
            "smile": 0.88,
            "facialHair": {
                "mustache": 0.8,
                "beard": 0.1,
                "sideburns": 0.02
            },
            "glasses": "sunglasses",
            "headPose": {
                "roll": 2.1,
                "yaw": 3,
                "pitch": 0
            }
        }
    }
]
```
## <span data-ttu-id="03ad5-121">Create a Person Group With Face API Using C# <a name="Create"> </a></span><span class="sxs-lookup"><span data-stu-id="03ad5-121">Create a Person Group With Face API Using C# <a name="Create"> </a></span></span>
<span data-ttu-id="03ad5-122">Use the [Person Group - Create a Person Group method](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244) to create a new person group with specified personGroupId, name, and user-provided userData.</span><span class="sxs-lookup"><span data-stu-id="03ad5-122">Use the [Person Group - Create a Person Group method](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244) to create a new person group with specified personGroupId, name, and user-provided userData.</span></span>

#### <a name="person-group---create-a-person-group-c-example-request"></a><span data-ttu-id="03ad5-123">Person Group - Create a Person Group C# Example Request</span><span class="sxs-lookup"><span data-stu-id="03ad5-123">Person Group - Create a Person Group C# Example Request</span></span>
```C#
using System;
using System.Net.Http.Headers;
using System.Net.Http;

namespace CSHttpClientSample
{
    static class Program
    {
        static void Main()
        {
            Console.WriteLine("Enter an ID for the group you wish to create:");
            Console.WriteLine("(Use numbers, lower case letters, '-' and '_'. The maximum length of the personGroupId is 64.)");

            string personGroupId = Console.ReadLine();
            MakeCreateGroupRequest(personGroupId);

            Console.WriteLine("\n\n\nWait for the result below, then hit ENTER to exit...\n\n\n");
            Console.ReadLine();
        }


        static async void MakeCreateGroupRequest(string personGroupId)
        {
            var client = new HttpClient();

            // Request headers - replace this example key with your valid key.
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", "6726adbabb494773a28a7a5a21d5974a");

            // Request URI string.
            string uri = "https://westus.api.cognitive.microsoft.com/face/v1.0/persongroups/" + personGroupId;

            // Here "name" is for display and doesn't have to be unique. Also, "userData" is optional.
            string json = "{\"name\":\"My Group\", \"userData\":\"Some data related to my group.\"}";
            HttpContent content = new StringContent(json);
            content.Headers.ContentType = new MediaTypeHeaderValue("application/json");

            HttpResponseMessage response = await client.PutAsync(uri, content);

            // If the group was created successfully, you'll see "OK".
            // Otherwise, if a group with the same personGroupId has been created before, you'll see "Conflict".
            Console.WriteLine("Response status: " + response.StatusCode);
        }
    }
}
```
