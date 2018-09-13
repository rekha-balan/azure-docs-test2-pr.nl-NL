---
title: 'Quickstart: Analyze an image - SDK, C# - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you analyze an image using the Computer Vision Windows C# client library in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: ad0b6bfc1c576e54c819937d0af4ff6cc4b38b06
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864948"
---
# <a name="quickstart-analyze-an-image---sdk-c35---computer-vision"></a><span data-ttu-id="1fb4d-103">Quickstart: Analyze an image - SDK, C&#35; - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="1fb4d-103">Quickstart: Analyze an image - SDK, C&#35; - Computer Vision</span></span>

<span data-ttu-id="1fb4d-104">In this quickstart, you analyze both a local and a remote image to extract visual features using the Computer Vision Windows client library.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-104">In this quickstart, you analyze both a local and a remote image to extract visual features using the Computer Vision Windows client library.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fb4d-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1fb4d-105">Prerequisites</span></span>

* <span data-ttu-id="1fb4d-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="1fb4d-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>
* <span data-ttu-id="1fb4d-107">Any edition of [Visual Studio 2015 or 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1fb4d-107">Any edition of [Visual Studio 2015 or 2017](https://www.visualstudio.com/downloads/).</span></span>
* <span data-ttu-id="1fb4d-108">The [Microsoft.Azure.CognitiveServices.Vision.ComputerVision](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Vision.ComputerVision) client library NuGet package.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-108">The [Microsoft.Azure.CognitiveServices.Vision.ComputerVision](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Vision.ComputerVision) client library NuGet package.</span></span> <span data-ttu-id="1fb4d-109">It isn't necessary to download the package.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-109">It isn't necessary to download the package.</span></span> <span data-ttu-id="1fb4d-110">Installation instructions are provided below.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-110">Installation instructions are provided below.</span></span>

## <a name="analyzeimageasync-method"></a><span data-ttu-id="1fb4d-111">AnalyzeImageAsync method</span><span class="sxs-lookup"><span data-stu-id="1fb4d-111">AnalyzeImageAsync method</span></span>

<span data-ttu-id="1fb4d-112">The `AnalyzeImageAsync` and `AnalyzeImageInStreamAsync` methods wrap the [Analyze Image API](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa) for remote and local images, respectively.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-112">The `AnalyzeImageAsync` and `AnalyzeImageInStreamAsync` methods wrap the [Analyze Image API](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa) for remote and local images, respectively.</span></span> <span data-ttu-id="1fb4d-113">You can use these methods to extract visual features based on image content and choose which features to return, including:</span><span class="sxs-lookup"><span data-stu-id="1fb4d-113">You can use these methods to extract visual features based on image content and choose which features to return, including:</span></span>

* <span data-ttu-id="1fb4d-114">A detailed list of tags related to the image content.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-114">A detailed list of tags related to the image content.</span></span>
* <span data-ttu-id="1fb4d-115">A description of image content in a complete sentence.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-115">A description of image content in a complete sentence.</span></span>
* <span data-ttu-id="1fb4d-116">The coordinates, gender, and age of any faces contained in the image.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-116">The coordinates, gender, and age of any faces contained in the image.</span></span>
* <span data-ttu-id="1fb4d-117">The ImageType (clip art or a line drawing).</span><span class="sxs-lookup"><span data-stu-id="1fb4d-117">The ImageType (clip art or a line drawing).</span></span>
* <span data-ttu-id="1fb4d-118">The dominant color, the accent color, or whether an image is black & white.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-118">The dominant color, the accent color, or whether an image is black & white.</span></span>
* <span data-ttu-id="1fb4d-119">The category defined in this [taxonomy](../Category-Taxonomy.md).</span><span class="sxs-lookup"><span data-stu-id="1fb4d-119">The category defined in this [taxonomy](../Category-Taxonomy.md).</span></span>
* <span data-ttu-id="1fb4d-120">Does the image contain adult or sexually suggestive content?</span><span class="sxs-lookup"><span data-stu-id="1fb4d-120">Does the image contain adult or sexually suggestive content?</span></span>

<span data-ttu-id="1fb4d-121">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="1fb4d-121">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="1fb4d-122">Create a new Visual C# Console App in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-122">Create a new Visual C# Console App in Visual Studio.</span></span>
1. <span data-ttu-id="1fb4d-123">Install the Computer Vision client library NuGet package.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-123">Install the Computer Vision client library NuGet package.</span></span>
    1. <span data-ttu-id="1fb4d-124">On the menu, click **Tools**, select **NuGet Package Manager**, then **Manage NuGet Packages for Solution**.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-124">On the menu, click **Tools**, select **NuGet Package Manager**, then **Manage NuGet Packages for Solution**.</span></span>
    1. <span data-ttu-id="1fb4d-125">Click the **Browse** tab, and in the **Search** box type "Microsoft.Azure.CognitiveServices.Vision.ComputerVision".</span><span class="sxs-lookup"><span data-stu-id="1fb4d-125">Click the **Browse** tab, and in the **Search** box type "Microsoft.Azure.CognitiveServices.Vision.ComputerVision".</span></span>
    1. <span data-ttu-id="1fb4d-126">Select **Microsoft.Azure.CognitiveServices.Vision.ComputerVision** when it displays, then click the checkbox next to your project name, and **Install**.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-126">Select **Microsoft.Azure.CognitiveServices.Vision.ComputerVision** when it displays, then click the checkbox next to your project name, and **Install**.</span></span>
1. <span data-ttu-id="1fb4d-127">Replace `Program.cs` with the following code.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-127">Replace `Program.cs` with the following code.</span></span>
1. <span data-ttu-id="1fb4d-128">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-128">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="1fb4d-129">Change `computerVision.AzureRegion = AzureRegions.Westcentralus` to the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-129">Change `computerVision.AzureRegion = AzureRegions.Westcentralus` to the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="1fb4d-130">Replace `<LocalImage>` with the path and file name of a local image.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-130">Replace `<LocalImage>` with the path and file name of a local image.</span></span>
1. <span data-ttu-id="1fb4d-131">Optionally, set `remoteImageUrl` to a different image.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-131">Optionally, set `remoteImageUrl` to a different image.</span></span>
1. <span data-ttu-id="1fb4d-132">Run the program.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-132">Run the program.</span></span>

```csharp
using Microsoft.Azure.CognitiveServices.Vision.ComputerVision;
using Microsoft.Azure.CognitiveServices.Vision.ComputerVision.Models;

using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

namespace ImageAnalyze
{
    class Program
    {
        // subscriptionKey = "0123456789abcdef0123456789ABCDEF"
        private const string subscriptionKey = "<SubscriptionKey>";

        // localImagePath = @"C:\Documents\LocalImage.jpg"
        private const string localImagePath = @"<LocalImage>";

        private const string remoteImageUrl =
            "http://upload.wikimedia.org/wikipedia/commons/3/3c/Shaki_waterfall.jpg";

        // Specify the features to return
        private static readonly List<VisualFeatureTypes> features =
            new List<VisualFeatureTypes>()
        {
            VisualFeatureTypes.Categories, VisualFeatureTypes.Description,
            VisualFeatureTypes.Faces, VisualFeatureTypes.ImageType,
            VisualFeatureTypes.Tags
        };

        static void Main(string[] args)
        {
            ComputerVisionAPI computerVision = new ComputerVisionAPI(
                new ApiKeyServiceClientCredentials(subscriptionKey), 
                new System.Net.Http.DelegatingHandler[] { });

            // You must use the same region as you used to get your subscription
            // keys. For example, if you got your subscription keys from westus,
            // replace "Westcentralus" with "Westus".
            //
            // Free trial subscription keys are generated in the westcentralus
            // region. If you use a free trial subscription key, you shouldn't
            // need to change the region.

            // Specify the Azure region
            computerVision.AzureRegion = AzureRegions.Westcentralus;

            Console.WriteLine("Images being analyzed ...");
            var t1 = AnalyzeRemoteAsync(computerVision, remoteImageUrl);
            var t2 = AnalyzeLocalAsync(computerVision, localImagePath);

            Task.WhenAll(t1, t2).Wait(5000);
            Console.WriteLine("Press any key to exit");
            Console.ReadLine();
        }

        // Analyze a remote image
        private static async Task AnalyzeRemoteAsync(
            ComputerVisionAPI computerVision, string imageUrl)
        {
            if (!Uri.IsWellFormedUriString(imageUrl, UriKind.Absolute))
            {
                Console.WriteLine(
                    "\nInvalid remoteImageUrl:\n{0} \n", imageUrl);
                return;
            }

            ImageAnalysis analysis =
                await computerVision.AnalyzeImageAsync(imageUrl, features);
            DisplayResults(analysis, imageUrl);
        }

        // Analyze a local image
        private static async Task AnalyzeLocalAsync(
            ComputerVisionAPI computerVision, string imagePath)
        {
            if (!File.Exists(imagePath))
            {
                Console.WriteLine(
                    "\nUnable to open or read localImagePath:\n{0} \n", imagePath);
                return;
            }

            using (Stream imageStream = File.OpenRead(imagePath))
            {
                ImageAnalysis analysis = await computerVision.AnalyzeImageInStreamAsync(
                    imageStream, features);
                DisplayResults(analysis, imagePath);
            }
        }

        // Display the most relevant caption for the image
        private static void DisplayResults(ImageAnalysis analysis, string imageUri)
        {
            Console.WriteLine(imageUri);
            Console.WriteLine(analysis.Description.Captions[0].Text + "\n");
        }
    }
}
```

## <a name="analyzeimageasync-response"></a><span data-ttu-id="1fb4d-133">AnalyzeImageAsync response</span><span class="sxs-lookup"><span data-stu-id="1fb4d-133">AnalyzeImageAsync response</span></span>

<span data-ttu-id="1fb4d-134">A successful response displays the most relevant caption for each image.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-134">A successful response displays the most relevant caption for each image.</span></span>

<span data-ttu-id="1fb4d-135">See [API Quickstarts: Analyze a local image with C#](../QuickStarts/CSharp-analyze.md#analyze-image-response) for an example of raw JSON output.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-135">See [API Quickstarts: Analyze a local image with C#](../QuickStarts/CSharp-analyze.md#analyze-image-response) for an example of raw JSON output.</span></span>

```cmd
http://upload.wikimedia.org/wikipedia/commons/3/3c/Shaki_waterfall.jpg
a large waterfall over a rocky cliff
```

## <a name="next-steps"></a><span data-ttu-id="1fb4d-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="1fb4d-136">Next steps</span></span>

<span data-ttu-id="1fb4d-137">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="1fb4d-137">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1fb4d-138">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="1fb4d-138">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
