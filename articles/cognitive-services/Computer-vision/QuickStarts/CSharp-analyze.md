---
title: 'Quickstart: Analyze a local image - REST, C# - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you analyze a local image using Computer Vision with C# in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: cf52c3f40b88e1ba705a9ddb5219501fb1ccfb35
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868593"
---
# <a name="quickstart-analyze-a-local-image---rest-c35---computer-vision"></a><span data-ttu-id="00eb2-103">Quickstart: Analyze a local image - REST, C&#35; - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="00eb2-103">Quickstart: Analyze a local image - REST, C&#35; - Computer Vision</span></span>

<span data-ttu-id="00eb2-104">In this quickstart, you analyze a local image to extract visual features using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="00eb2-104">In this quickstart, you analyze a local image to extract visual features using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00eb2-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="00eb2-105">Prerequisites</span></span>

<span data-ttu-id="00eb2-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="00eb2-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="analyze-image-request"></a><span data-ttu-id="00eb2-107">Analyze Image request</span><span class="sxs-lookup"><span data-stu-id="00eb2-107">Analyze Image request</span></span>

<span data-ttu-id="00eb2-108">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span><span class="sxs-lookup"><span data-stu-id="00eb2-108">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span></span> <span data-ttu-id="00eb2-109">You can upload an image or specify an image URL and choose which features to return, including:</span><span class="sxs-lookup"><span data-stu-id="00eb2-109">You can upload an image or specify an image URL and choose which features to return, including:</span></span>

* <span data-ttu-id="00eb2-110">A detailed list of tags related to the image content.</span><span class="sxs-lookup"><span data-stu-id="00eb2-110">A detailed list of tags related to the image content.</span></span>
* <span data-ttu-id="00eb2-111">A description of image content in a complete sentence.</span><span class="sxs-lookup"><span data-stu-id="00eb2-111">A description of image content in a complete sentence.</span></span>
* <span data-ttu-id="00eb2-112">The coordinates, gender, and age of any faces contained in the image.</span><span class="sxs-lookup"><span data-stu-id="00eb2-112">The coordinates, gender, and age of any faces contained in the image.</span></span>
* <span data-ttu-id="00eb2-113">The ImageType (clip art or a line drawing).</span><span class="sxs-lookup"><span data-stu-id="00eb2-113">The ImageType (clip art or a line drawing).</span></span>
* <span data-ttu-id="00eb2-114">The dominant color, the accent color, or whether an image is black & white.</span><span class="sxs-lookup"><span data-stu-id="00eb2-114">The dominant color, the accent color, or whether an image is black & white.</span></span>
* <span data-ttu-id="00eb2-115">The category defined in this [taxonomy](../Category-Taxonomy.md).</span><span class="sxs-lookup"><span data-stu-id="00eb2-115">The category defined in this [taxonomy](../Category-Taxonomy.md).</span></span>
* <span data-ttu-id="00eb2-116">Does the image contain adult or sexually suggestive content?</span><span class="sxs-lookup"><span data-stu-id="00eb2-116">Does the image contain adult or sexually suggestive content?</span></span>

<span data-ttu-id="00eb2-117">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="00eb2-117">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="00eb2-118">Create a new Visual C# Console App in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="00eb2-118">Create a new Visual C# Console App in Visual Studio.</span></span>
1. <span data-ttu-id="00eb2-119">Install the Newtonsoft.Json NuGet package.</span><span class="sxs-lookup"><span data-stu-id="00eb2-119">Install the Newtonsoft.Json NuGet package.</span></span>
    1. <span data-ttu-id="00eb2-120">On the menu, click **Tools**, select **NuGet Package Manager**, then **Manage NuGet Packages for Solution**.</span><span class="sxs-lookup"><span data-stu-id="00eb2-120">On the menu, click **Tools**, select **NuGet Package Manager**, then **Manage NuGet Packages for Solution**.</span></span>
    1. <span data-ttu-id="00eb2-121">Click the **Browse** tab, and in the **Search** box type "Newtonsoft.Json".</span><span class="sxs-lookup"><span data-stu-id="00eb2-121">Click the **Browse** tab, and in the **Search** box type "Newtonsoft.Json".</span></span>
    1. <span data-ttu-id="00eb2-122">Select **Newtonsoft.Json** when it displays, then click the checkbox next to your project name, and **Install**.</span><span class="sxs-lookup"><span data-stu-id="00eb2-122">Select **Newtonsoft.Json** when it displays, then click the checkbox next to your project name, and **Install**.</span></span>
1. <span data-ttu-id="00eb2-123">Replace `Program.cs` with the following code.</span><span class="sxs-lookup"><span data-stu-id="00eb2-123">Replace `Program.cs` with the following code.</span></span>
1. <span data-ttu-id="00eb2-124">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="00eb2-124">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="00eb2-125">Change the `uriBase` value to the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="00eb2-125">Change the `uriBase` value to the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="00eb2-126">Run the program.</span><span class="sxs-lookup"><span data-stu-id="00eb2-126">Run the program.</span></span>
1. <span data-ttu-id="00eb2-127">At the prompt, enter the path to a local image.</span><span class="sxs-lookup"><span data-stu-id="00eb2-127">At the prompt, enter the path to a local image.</span></span>

```csharp
using Newtonsoft.Json.Linq;
using System;
using System.IO;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Threading.Tasks;

namespace CSHttpClientSample
{
    static class Program
    {
        // Replace <Subscription Key> with your valid subscription key.
        const string subscriptionKey = "<Subscription Key>";

        // You must use the same region in your REST call as you used to
        // get your subscription keys. For example, if you got your
        // subscription keys from westus, replace "westcentralus" in the URL
        // below with "westus".
        //
        // Free trial subscription keys are generated in the westcentralus region.
        // If you use a free trial subscription key, you shouldn't need to change
        // this region.
        const string uriBase =
            "https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/analyze";

        static void Main()
        {
            // Get the path and filename to process from the user.
            Console.WriteLine("Analyze an image:");
            Console.Write("Enter the path to the image you wish to analyze: ");
            string imageFilePath = Console.ReadLine();

            if (File.Exists(imageFilePath))
            {
                // Make the REST API call.
                Console.WriteLine("\nWait a moment for the results to appear.\n");
                MakeAnalysisRequest(imageFilePath).Wait();
            }
            else
            {
                Console.WriteLine("\nInvalid file path");
            }
            Console.WriteLine("\nPress Enter to exit...");
            Console.ReadLine();
        }

        /// <summary>
        /// Gets the analysis of the specified image file by using
        /// the Computer Vision REST API.
        /// </summary>
        /// <param name="imageFilePath">The image file to analyze.</param>
        static async Task MakeAnalysisRequest(string imageFilePath)
        {
            try
            {
                HttpClient client = new HttpClient();

                // Request headers.
                client.DefaultRequestHeaders.Add(
                    "Ocp-Apim-Subscription-Key", subscriptionKey);

                // Request parameters. A third optional parameter is "details".
                string requestParameters =
                    "visualFeatures=Categories,Description,Color";

                // Assemble the URI for the REST API Call.
                string uri = uriBase + "?" + requestParameters;

                HttpResponseMessage response;

                // Request body. Posts a locally stored JPEG image.
                byte[] byteData = GetImageAsByteArray(imageFilePath);

                using (ByteArrayContent content = new ByteArrayContent(byteData))
                {
                    // This example uses content type "application/octet-stream".
                    // The other content types you can use are "application/json"
                    // and "multipart/form-data".
                    content.Headers.ContentType =
                        new MediaTypeHeaderValue("application/octet-stream");

                    // Make the REST API call.
                    response = await client.PostAsync(uri, content);
                }

                // Get the JSON response.
                string contentString = await response.Content.ReadAsStringAsync();

                // Display the JSON response.
                Console.WriteLine("\nResponse:\n\n{0}\n",
                    JToken.Parse(contentString).ToString());
            }
            catch (Exception e)
            {
                Console.WriteLine("\n" + e.Message);
            }
        }

        /// <summary>
        /// Returns the contents of the specified file as a byte array.
        /// </summary>
        /// <param name="imageFilePath">The image file to read.</param>
        /// <returns>The byte array of the image data.</returns>
        static byte[] GetImageAsByteArray(string imageFilePath)
        {
            using (FileStream fileStream =
                new FileStream(imageFilePath, FileMode.Open, FileAccess.Read))
            {
                BinaryReader binaryReader = new BinaryReader(fileStream);
                return binaryReader.ReadBytes((int)fileStream.Length);
            }
        }
    }
}
```

## <a name="analyze-image-response"></a><span data-ttu-id="00eb2-128">Analyze Image response</span><span class="sxs-lookup"><span data-stu-id="00eb2-128">Analyze Image response</span></span>

<span data-ttu-id="00eb2-129">A successful response is returned in JSON, for example:</span><span class="sxs-lookup"><span data-stu-id="00eb2-129">A successful response is returned in JSON, for example:</span></span>

```json
{
   "categories": [
      {
         "name": "abstract_",
         "score": 0.00390625
      },
      {
         "name": "others_",
         "score": 0.0234375
      },
      {
         "name": "outdoor_",
         "score": 0.00390625
      }
   ],
   "description": {
      "tags": [
         "road",
         "building",
         "outdoor",
         "street",
         "night",
         "black",
         "city",
         "white",
         "light",
         "sitting",
         "riding",
         "man",
         "side",
         "empty",
         "rain",
         "corner",
         "traffic",
         "lit",
         "hydrant",
         "stop",
         "board",
         "parked",
         "bus",
         "tall"
      ],
      "captions": [
         {
            "text": "a close up of an empty city street at night",
            "confidence": 0.7965622853462756
         }
      ]
   },
   "requestId": "dddf1ac9-7e66-4c47-bdef-222f3fe5aa23",
   "metadata": {
      "width": 3733,
      "height": 1986,
      "format": "Jpeg"
   },
   "color": {
      "dominantColorForeground": "Black",
      "dominantColorBackground": "Black",
      "dominantColors": [
         "Black",
         "Grey"
      ],
      "accentColor": "666666",
      "isBWImg": true
   }
}
```

## <a name="next-steps"></a><span data-ttu-id="00eb2-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="00eb2-130">Next steps</span></span>

<span data-ttu-id="00eb2-131">Explore a basic Windows application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span><span class="sxs-lookup"><span data-stu-id="00eb2-131">Explore a basic Windows application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span></span> <span data-ttu-id="00eb2-132">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="00eb2-132">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="00eb2-133">Use Computer Vision with C#</span><span class="sxs-lookup"><span data-stu-id="00eb2-133">Use Computer Vision with C#</span></span>](../Tutorials/CSharpTutorial.md)
