---
title: 'Quickstart: Generate a thumbnail - REST, C# - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you generate a thumbnail from an image using Computer Vision with C# in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 8436d626f0472c488bd4edb7906204ebacc08eae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857501"
---
# <a name="quickstart-generate-a-thumbnail---rest-c35---computer-vision"></a><span data-ttu-id="f6b26-103">Quickstart: Generate a thumbnail - REST, C&#35; - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="f6b26-103">Quickstart: Generate a thumbnail - REST, C&#35; - Computer Vision</span></span>

<span data-ttu-id="f6b26-104">In this quickstart, you generate a thumbnail from an image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="f6b26-104">In this quickstart, you generate a thumbnail from an image using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6b26-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f6b26-105">Prerequisites</span></span>

<span data-ttu-id="f6b26-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="f6b26-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="get-thumbnail-request"></a><span data-ttu-id="f6b26-107">Get Thumbnail request</span><span class="sxs-lookup"><span data-stu-id="f6b26-107">Get Thumbnail request</span></span>

<span data-ttu-id="f6b26-108">With the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb), you can generate a thumbnail of an image.</span><span class="sxs-lookup"><span data-stu-id="f6b26-108">With the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb), you can generate a thumbnail of an image.</span></span> <span data-ttu-id="f6b26-109">You specify the height and width, which can differ from the aspect ratio of the input image.</span><span class="sxs-lookup"><span data-stu-id="f6b26-109">You specify the height and width, which can differ from the aspect ratio of the input image.</span></span> <span data-ttu-id="f6b26-110">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span><span class="sxs-lookup"><span data-stu-id="f6b26-110">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span></span>

<span data-ttu-id="f6b26-111">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="f6b26-111">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="f6b26-112">Create a new Visual C# Console App in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f6b26-112">Create a new Visual C# Console App in Visual Studio.</span></span>
1. <span data-ttu-id="f6b26-113">Install the Newtonsoft.Json NuGet package.</span><span class="sxs-lookup"><span data-stu-id="f6b26-113">Install the Newtonsoft.Json NuGet package.</span></span>
    1. <span data-ttu-id="f6b26-114">On the menu, click **Tools**, select **NuGet Package Manager**, then **Manage NuGet Packages for Solution**.</span><span class="sxs-lookup"><span data-stu-id="f6b26-114">On the menu, click **Tools**, select **NuGet Package Manager**, then **Manage NuGet Packages for Solution**.</span></span>
    1. <span data-ttu-id="f6b26-115">Click the **Browse** tab, and in the **Search** box type "Newtonsoft.Json".</span><span class="sxs-lookup"><span data-stu-id="f6b26-115">Click the **Browse** tab, and in the **Search** box type "Newtonsoft.Json".</span></span>
    1. <span data-ttu-id="f6b26-116">Select **Newtonsoft.Json** when it displays, then click the checkbox next to your project name, and **Install**.</span><span class="sxs-lookup"><span data-stu-id="f6b26-116">Select **Newtonsoft.Json** when it displays, then click the checkbox next to your project name, and **Install**.</span></span>
1. <span data-ttu-id="f6b26-117">Replace `Program.cs` with the following code.</span><span class="sxs-lookup"><span data-stu-id="f6b26-117">Replace `Program.cs` with the following code.</span></span>
1. <span data-ttu-id="f6b26-118">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="f6b26-118">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="f6b26-119">Change the `uriBase` value to the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="f6b26-119">Change the `uriBase` value to the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="f6b26-120">Run the program.</span><span class="sxs-lookup"><span data-stu-id="f6b26-120">Run the program.</span></span>
1. <span data-ttu-id="f6b26-121">At the prompt, enter the path to a local image.</span><span class="sxs-lookup"><span data-stu-id="f6b26-121">At the prompt, enter the path to a local image.</span></span>

<span data-ttu-id="f6b26-122">The thumbnail is saved to the same folder as the local image, using the original name with the suffix "_thumb".</span><span class="sxs-lookup"><span data-stu-id="f6b26-122">The thumbnail is saved to the same folder as the local image, using the original name with the suffix "_thumb".</span></span>

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
            "https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail";

        static void Main()
        {
            // Get the path and filename to process from the user.
            Console.WriteLine("Thumbnail:");
            Console.Write(
                "Enter the path to the image you wish to use to create a thumbnail image: ");
            string imageFilePath = Console.ReadLine();

            if (File.Exists(imageFilePath))
            {
                // Make the REST API call.
                Console.WriteLine("\nWait a moment for the results to appear.\n");
                MakeThumbNailRequest(imageFilePath).Wait();
            }
            else
            {
                Console.WriteLine("\nInvalid file path");
            }
            Console.WriteLine("\nPress Enter to exit...");
            Console.ReadLine();
        }

        /// <summary>
        /// Gets a thumbnail image from the specified image file by using
        /// the Computer Vision REST API.
        /// </summary>
        /// <param name="imageFilePath">The image file to use to create the thumbnail image.</param>
        static async Task MakeThumbNailRequest(string imageFilePath)
        {
            try
            {
                HttpClient client = new HttpClient();

                // Request headers.
                client.DefaultRequestHeaders.Add(
                    "Ocp-Apim-Subscription-Key", subscriptionKey);

                // Request parameters.
                string requestParameters = "width=200&height=150&smartCropping=true";

                // Assemble the URI for the REST API Call.
                string uri = uriBase + "?" + requestParameters;

                HttpResponseMessage response;

                // Request body.
                // Posts a locally stored JPEG image.
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

                if (response.IsSuccessStatusCode)
                {
                    // Display the response data.
                    Console.WriteLine("\nResponse:\n{0}", response);

                    // Get the image data.
                    byte[] thumbnailImageData =
                        await response.Content.ReadAsByteArrayAsync();

                    // Save the thumbnail to the same folder as the original image,
                    // using the original name with the suffix "_thumb".
                    // Note: This will overwrite an existing file of the same name.
                    string thumbnailFilePath =
                        imageFilePath.Insert(imageFilePath.Length - 4, "_thumb");
                    File.WriteAllBytes(thumbnailFilePath, thumbnailImageData);
                    Console.WriteLine("\nThumbnail written to: {0}", thumbnailFilePath);
                }
                else
                {
                    // Display the JSON error data.
                    string errorString = await response.Content.ReadAsStringAsync();
                    Console.WriteLine("\n\nResponse:\n{0}\n",
                        JToken.Parse(errorString).ToString());
                }
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

## <a name="get-thumbnail-response"></a><span data-ttu-id="f6b26-123">Get Thumbnail response</span><span class="sxs-lookup"><span data-stu-id="f6b26-123">Get Thumbnail response</span></span>

<span data-ttu-id="f6b26-124">A successful response contains the thumbnail image binary.</span><span class="sxs-lookup"><span data-stu-id="f6b26-124">A successful response contains the thumbnail image binary.</span></span> <span data-ttu-id="f6b26-125">If the request fails, the response contains an error code and a message to help determine what went wrong.</span><span class="sxs-lookup"><span data-stu-id="f6b26-125">If the request fails, the response contains an error code and a message to help determine what went wrong.</span></span>

```text
Response:

StatusCode: 200, ReasonPhrase: 'OK', Version: 1.1, Content: System.Net.Http.StreamContent, Headers:
{
  Pragma: no-cache
  apim-request-id: 131eb5b4-5807-466d-9656-4c1ef0a64c9b
  Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
  x-content-type-options: nosniff
  Cache-Control: no-cache
  Date: Tue, 06 Jun 2017 20:54:07 GMT
  X-AspNet-Version: 4.0.30319
  X-Powered-By: ASP.NET
  Content-Length: 5800
  Content-Type: image/jpeg
  Expires: -1
}
```

## <a name="next-steps"></a><span data-ttu-id="f6b26-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="f6b26-126">Next steps</span></span>

<span data-ttu-id="f6b26-127">Explore a basic Windows application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span><span class="sxs-lookup"><span data-stu-id="f6b26-127">Explore a basic Windows application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span></span> <span data-ttu-id="f6b26-128">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="f6b26-128">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6b26-129">Computer Vision API C&#35; Tutorial</span><span class="sxs-lookup"><span data-stu-id="f6b26-129">Computer Vision API C&#35; Tutorial</span></span>](../Tutorials/CSharpTutorial.md)