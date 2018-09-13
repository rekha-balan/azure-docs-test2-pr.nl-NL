---
title: 'Quickstart: Generate a thumbnail - SDK, C# - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you generate a thumbnail from an image using the Computer Vision Windows C# client library in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 8153fe1b59bb63d3d720abc39e275ef90da4154b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856741"
---
# <a name="quickstart-generate-a-thumbnail---sdk-c35---computer-vision"></a><span data-ttu-id="a7005-103">Quickstart: Generate a thumbnail - SDK, C&#35; - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="a7005-103">Quickstart: Generate a thumbnail - SDK, C&#35; - Computer Vision</span></span>

<span data-ttu-id="a7005-104">In this quickstart, you generate a thumbnail from an image using the Computer Vision Windows client library.</span><span class="sxs-lookup"><span data-stu-id="a7005-104">In this quickstart, you generate a thumbnail from an image using the Computer Vision Windows client library.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7005-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a7005-105">Prerequisites</span></span>

* <span data-ttu-id="a7005-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="a7005-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>
* <span data-ttu-id="a7005-107">Any edition of [Visual Studio 2015 or 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a7005-107">Any edition of [Visual Studio 2015 or 2017](https://www.visualstudio.com/downloads/).</span></span>
* <span data-ttu-id="a7005-108">The [Microsoft.Azure.CognitiveServices.Vision.ComputerVision](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Vision.ComputerVision) client library NuGet package.</span><span class="sxs-lookup"><span data-stu-id="a7005-108">The [Microsoft.Azure.CognitiveServices.Vision.ComputerVision](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Vision.ComputerVision) client library NuGet package.</span></span> <span data-ttu-id="a7005-109">It isn't necessary to download the package.</span><span class="sxs-lookup"><span data-stu-id="a7005-109">It isn't necessary to download the package.</span></span> <span data-ttu-id="a7005-110">Installation instructions are provided below.</span><span class="sxs-lookup"><span data-stu-id="a7005-110">Installation instructions are provided below.</span></span>

## <a name="generatethumbnailasync-method"></a><span data-ttu-id="a7005-111">GenerateThumbnailAsync method</span><span class="sxs-lookup"><span data-stu-id="a7005-111">GenerateThumbnailAsync method</span></span>

<span data-ttu-id="a7005-112">The `GenerateThumbnailAsync` and `GenerateThumbnailInStreamAsync` methods wrap the [Get Thumbnail API](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb) for remote and local images, respectively.</span><span class="sxs-lookup"><span data-stu-id="a7005-112">The `GenerateThumbnailAsync` and `GenerateThumbnailInStreamAsync` methods wrap the [Get Thumbnail API](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb) for remote and local images, respectively.</span></span>  <span data-ttu-id="a7005-113">You can use these methods to generate a thumbnail of an image.</span><span class="sxs-lookup"><span data-stu-id="a7005-113">You can use these methods to generate a thumbnail of an image.</span></span> <span data-ttu-id="a7005-114">You specify the height and width, which can differ from the aspect ratio of the input image.</span><span class="sxs-lookup"><span data-stu-id="a7005-114">You specify the height and width, which can differ from the aspect ratio of the input image.</span></span> <span data-ttu-id="a7005-115">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span><span class="sxs-lookup"><span data-stu-id="a7005-115">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span></span>

<span data-ttu-id="a7005-116">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="a7005-116">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="a7005-117">Create a new Visual C# Console App in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a7005-117">Create a new Visual C# Console App in Visual Studio.</span></span>
1. <span data-ttu-id="a7005-118">Install the Computer Vision client library NuGet package.</span><span class="sxs-lookup"><span data-stu-id="a7005-118">Install the Computer Vision client library NuGet package.</span></span>
    1. <span data-ttu-id="a7005-119">On the menu, click **Tools**, select **NuGet Package Manager**, then **Manage NuGet Packages for Solution**.</span><span class="sxs-lookup"><span data-stu-id="a7005-119">On the menu, click **Tools**, select **NuGet Package Manager**, then **Manage NuGet Packages for Solution**.</span></span>
    1. <span data-ttu-id="a7005-120">Click the **Browse** tab, and in the **Search** box type "Microsoft.Azure.CognitiveServices.Vision.ComputerVision".</span><span class="sxs-lookup"><span data-stu-id="a7005-120">Click the **Browse** tab, and in the **Search** box type "Microsoft.Azure.CognitiveServices.Vision.ComputerVision".</span></span>
    1. <span data-ttu-id="a7005-121">Select **Microsoft.Azure.CognitiveServices.Vision.ComputerVision** when it displays, then click the checkbox next to your project name, and **Install**.</span><span class="sxs-lookup"><span data-stu-id="a7005-121">Select **Microsoft.Azure.CognitiveServices.Vision.ComputerVision** when it displays, then click the checkbox next to your project name, and **Install**.</span></span>
1. <span data-ttu-id="a7005-122">Replace `Program.cs` with the following code.</span><span class="sxs-lookup"><span data-stu-id="a7005-122">Replace `Program.cs` with the following code.</span></span>
1. <span data-ttu-id="a7005-123">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="a7005-123">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="a7005-124">Change `computerVision.AzureRegion = AzureRegions.Westcentralus` to the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="a7005-124">Change `computerVision.AzureRegion = AzureRegions.Westcentralus` to the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="a7005-125">Optionally, replace `<LocalImage>` with the path and file name of a local image (will be ignored if not set).</span><span class="sxs-lookup"><span data-stu-id="a7005-125">Optionally, replace `<LocalImage>` with the path and file name of a local image (will be ignored if not set).</span></span>
1. <span data-ttu-id="a7005-126">Optionally, set `remoteImageUrl` to a different image.</span><span class="sxs-lookup"><span data-stu-id="a7005-126">Optionally, set `remoteImageUrl` to a different image.</span></span>
1. <span data-ttu-id="a7005-127">Optionally, set `writeThumbnailToDisk` to `true` to save the thumbnail to disk.</span><span class="sxs-lookup"><span data-stu-id="a7005-127">Optionally, set `writeThumbnailToDisk` to `true` to save the thumbnail to disk.</span></span>
1. <span data-ttu-id="a7005-128">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a7005-128">Run the program.</span></span>

```csharp
using Microsoft.Azure.CognitiveServices.Vision.ComputerVision;
using Microsoft.Azure.CognitiveServices.Vision.ComputerVision.Models;

using System;
using System.IO;
using System.Threading.Tasks;

namespace ImageThumbnail
{
    class Program
    {
        private const bool writeThumbnailToDisk = false;

        // subscriptionKey = "0123456789abcdef0123456789ABCDEF"
        private const string subscriptionKey = "<SubscriptionKey>";

        // localImagePath = @"C:\Documents\LocalImage.jpg"
        private const string localImagePath = @"<LocalImage>";

        private const string remoteImageUrl =
            "https://upload.wikimedia.org/wikipedia/commons/9/94/Bloodhound_Puppy.jpg";

        private const int thumbnailWidth = 100;
        private const int thumbnailHeight = 100;

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

            Console.WriteLine("Images being analyzed ...\n");
            var t1 = GetRemoteThumbnailAsync(computerVision, remoteImageUrl);
            var t2 = GetLocalThumbnailAsnc(computerVision, localImagePath);

            Task.WhenAll(t1, t2).Wait(5000);
            Console.WriteLine("Press any key to exit");
            Console.ReadLine();
        }

        // Create a thumbnail from a remote image
        private static async Task GetRemoteThumbnailAsync(
            ComputerVisionAPI computerVision, string imageUrl)
        {
            if (!Uri.IsWellFormedUriString(imageUrl, UriKind.Absolute))
            {
                Console.WriteLine(
                    "\nInvalid remoteImageUrl:\n{0} \n", imageUrl);
                return;
            }

            Stream thumbnail = await computerVision.GenerateThumbnailAsync(
                thumbnailWidth, thumbnailHeight, imageUrl, true);

            string path = Environment.CurrentDirectory;
            string imageName = imageUrl.Substring(imageUrl.LastIndexOf('/') + 1);
            string thumbnailFilePath =
                path + "\\" + imageName.Insert(imageName.Length - 4, "_thumb");

            // Save the thumbnail to the current working directory,
            // using the original name with the suffix "_thumb".
            SaveThumbnail(thumbnail, thumbnailFilePath);
        }

        // Create a thumbnail from a local image
        private static async Task GetLocalThumbnailAsnc(
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
                Stream thumbnail = await computerVision.GenerateThumbnailInStreamAsync(
                    thumbnailWidth, thumbnailHeight, imageStream, true);

                string thumbnailFilePath =
                    localImagePath.Insert(localImagePath.Length - 4, "_thumb");

                // Save the thumbnail to the same folder as the original image,
                // using the original name with the suffix "_thumb".
                SaveThumbnail(thumbnail, thumbnailFilePath);
            }
        }

        // Save the thumbnail locally.
        // NOTE: This will overwrite an existing file of the same name.
        private static void SaveThumbnail(Stream thumbnail, string thumbnailFilePath)
        {
            if (writeThumbnailToDisk)
            {
                using (Stream file = File.Create(thumbnailFilePath))
                {
                    thumbnail.CopyTo(file);
                }
            }
            Console.WriteLine("Thumbnail {0} written to: {1}\n",
                writeThumbnailToDisk ? "" : "NOT", thumbnailFilePath);
        }
    }
}
```

## <a name="generatethumbnailasync-response"></a><span data-ttu-id="a7005-129">GenerateThumbnailAsync response</span><span class="sxs-lookup"><span data-stu-id="a7005-129">GenerateThumbnailAsync response</span></span>

<span data-ttu-id="a7005-130">A successful response saves the thumbnail for each image locally and displays the thumbnail's location, for example:</span><span class="sxs-lookup"><span data-stu-id="a7005-130">A successful response saves the thumbnail for each image locally and displays the thumbnail's location, for example:</span></span>

```cmd
Thumbnail written to: C:\Documents\LocalImage_thumb.jpg

Thumbnail written to: ...\bin\Debug\Bloodhound_Puppy_thumb.jpg
```

## <a name="next-steps"></a><span data-ttu-id="a7005-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="a7005-131">Next steps</span></span>

<span data-ttu-id="a7005-132">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="a7005-132">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a7005-133">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="a7005-133">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
