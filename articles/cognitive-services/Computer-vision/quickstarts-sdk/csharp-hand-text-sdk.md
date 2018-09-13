---
title: 'Quickstart: Extract handwritten text - SDK, C# - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you extract handwritten text from an image using the Computer Vision Windows C# client library in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: f036bd1e42b5caf27259df1af1361a5919b2ad94
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866460"
---
# <a name="quickstart-extract-handwritten-text---sdk-c35---computer-vision"></a><span data-ttu-id="23413-103">Quickstart: Extract handwritten text - SDK, C&#35; - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="23413-103">Quickstart: Extract handwritten text - SDK, C&#35; - Computer Vision</span></span>

<span data-ttu-id="23413-104">In this quickstart, you extract handwritten text from an image using the Computer Vision Windows client library.</span><span class="sxs-lookup"><span data-stu-id="23413-104">In this quickstart, you extract handwritten text from an image using the Computer Vision Windows client library.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23413-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="23413-105">Prerequisites</span></span>

* <span data-ttu-id="23413-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="23413-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>
* <span data-ttu-id="23413-107">Any edition of [Visual Studio 2015 or 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="23413-107">Any edition of [Visual Studio 2015 or 2017](https://www.visualstudio.com/downloads/).</span></span>
* <span data-ttu-id="23413-108">The [Microsoft.Azure.CognitiveServices.Vision.ComputerVision](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Vision.ComputerVision) client library NuGet package.</span><span class="sxs-lookup"><span data-stu-id="23413-108">The [Microsoft.Azure.CognitiveServices.Vision.ComputerVision](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Vision.ComputerVision) client library NuGet package.</span></span> <span data-ttu-id="23413-109">It isn't necessary to download the package.</span><span class="sxs-lookup"><span data-stu-id="23413-109">It isn't necessary to download the package.</span></span> <span data-ttu-id="23413-110">Installation instructions are provided below.</span><span class="sxs-lookup"><span data-stu-id="23413-110">Installation instructions are provided below.</span></span>

## <a name="recognizetextasync-method"></a><span data-ttu-id="23413-111">RecognizeTextAsync method</span><span class="sxs-lookup"><span data-stu-id="23413-111">RecognizeTextAsync method</span></span>

<span data-ttu-id="23413-112">The `RecognizeTextAsync` and `RecognizeTextInStreamAsync` methods wrap the [Recognize Text API](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2c6a154055056008f200) for remote and local images, respectively.</span><span class="sxs-lookup"><span data-stu-id="23413-112">The `RecognizeTextAsync` and `RecognizeTextInStreamAsync` methods wrap the [Recognize Text API](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2c6a154055056008f200) for remote and local images, respectively.</span></span> <span data-ttu-id="23413-113">The `GetTextOperationResultAsync` method wraps the [Get Recognize Text Operation Results API](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2cf1154055056008f201).</span><span class="sxs-lookup"><span data-stu-id="23413-113">The `GetTextOperationResultAsync` method wraps the [Get Recognize Text Operation Results API](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2cf1154055056008f201).</span></span>  <span data-ttu-id="23413-114">You can use these methods to detect handwritten text in an image and extract recognized characters into a machine-usable character stream.</span><span class="sxs-lookup"><span data-stu-id="23413-114">You can use these methods to detect handwritten text in an image and extract recognized characters into a machine-usable character stream.</span></span>

<span data-ttu-id="23413-115">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="23413-115">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="23413-116">Create a new Visual C# Console App in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="23413-116">Create a new Visual C# Console App in Visual Studio.</span></span>
1. <span data-ttu-id="23413-117">Install the Computer Vision client library NuGet package.</span><span class="sxs-lookup"><span data-stu-id="23413-117">Install the Computer Vision client library NuGet package.</span></span>
    1. <span data-ttu-id="23413-118">On the menu, click **Tools**, select **NuGet Package Manager**, then **Manage NuGet Packages for Solution**.</span><span class="sxs-lookup"><span data-stu-id="23413-118">On the menu, click **Tools**, select **NuGet Package Manager**, then **Manage NuGet Packages for Solution**.</span></span>
    1. <span data-ttu-id="23413-119">Click the **Browse** tab, and in the **Search** box type "Microsoft.Azure.CognitiveServices.Vision.ComputerVision".</span><span class="sxs-lookup"><span data-stu-id="23413-119">Click the **Browse** tab, and in the **Search** box type "Microsoft.Azure.CognitiveServices.Vision.ComputerVision".</span></span>
    1. <span data-ttu-id="23413-120">Select **Microsoft.Azure.CognitiveServices.Vision.ComputerVision** when it displays, then click the checkbox next to your project name, and **Install**.</span><span class="sxs-lookup"><span data-stu-id="23413-120">Select **Microsoft.Azure.CognitiveServices.Vision.ComputerVision** when it displays, then click the checkbox next to your project name, and **Install**.</span></span>
1. <span data-ttu-id="23413-121">Replace `Program.cs` with the following code.</span><span class="sxs-lookup"><span data-stu-id="23413-121">Replace `Program.cs` with the following code.</span></span>
1. <span data-ttu-id="23413-122">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="23413-122">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="23413-123">Change `computerVision.AzureRegion = AzureRegions.Westcentralus` to the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="23413-123">Change `computerVision.AzureRegion = AzureRegions.Westcentralus` to the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="23413-124">Replace `<LocalImage>` with the path and file name of a local image.</span><span class="sxs-lookup"><span data-stu-id="23413-124">Replace `<LocalImage>` with the path and file name of a local image.</span></span>
1. <span data-ttu-id="23413-125">Optionally, set `remoteImageUrl` to a different image.</span><span class="sxs-lookup"><span data-stu-id="23413-125">Optionally, set `remoteImageUrl` to a different image.</span></span>
1. <span data-ttu-id="23413-126">Run the program.</span><span class="sxs-lookup"><span data-stu-id="23413-126">Run the program.</span></span>

```csharp
using Microsoft.Azure.CognitiveServices.Vision.ComputerVision;
using Microsoft.Azure.CognitiveServices.Vision.ComputerVision.Models;

using System;
using System.IO;
using System.Threading.Tasks;

namespace ImageHandText
{
    class Program
    {
        // subscriptionKey = "0123456789abcdef0123456789ABCDEF"
        private const string subscriptionKey = "<SubscriptionKey>";

        // localImagePath = @"C:\Documents\LocalImage.jpg"
        private const string localImagePath = @"<LocalImage>";

        private const string remoteImageUrl =
            "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/" +
            "Cursive_Writing_on_Notebook_paper.jpg/" +
            "800px-Cursive_Writing_on_Notebook_paper.jpg";

        private const int numberOfCharsInOperationId = 36;

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
            var t1 = ExtractRemoteHandTextAsync(computerVision, remoteImageUrl);
            var t2 = ExtractLocalHandTextAsync(computerVision, localImagePath);

            Task.WhenAll(t1, t2).Wait(5000);
            Console.WriteLine("Press any key to exit");
            Console.ReadLine();
        }

        // Recognize text from a remote image
        private static async Task ExtractRemoteHandTextAsync(
            ComputerVisionAPI computerVision, string imageUrl)
        {
            if (!Uri.IsWellFormedUriString(imageUrl, UriKind.Absolute))
            {
                Console.WriteLine(
                    "\nInvalid remoteImageUrl:\n{0} \n", imageUrl);
                return;
            }

            // Start the async process to recognize the text
            RecognizeTextHeaders textHeaders = await computerVision.RecognizeTextAsync(
                    imageUrl, TextRecognitionMode.Handwritten);

            await GetTextAsync(computerVision, textHeaders.OperationLocation);
        }

        // Recognize text from a local image
        private static async Task ExtractLocalHandTextAsync(
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
                // Start the async process to recognize the text
                RecognizeTextInStreamHeaders textHeaders =
                    await computerVision.RecognizeTextInStreamAsync(
                        imageStream, TextRecognitionMode.Handwritten);

                await GetTextAsync(computerVision, textHeaders.OperationLocation);
            }
        }

        // Retrieve the recognized text
        private static async Task GetTextAsync(
            ComputerVisionAPI computerVision, string operationLocation)
        {
            // Retrieve the URI where the recognized text will be
            // stored from the Operation-Location header
            string operationId = operationLocation.Substring(
                operationLocation.Length - numberOfCharsInOperationId);

            Console.WriteLine("\nCalling GetHandwritingRecognitionOperationResultAsync()");
            TextOperationResult result =
                await computerVision.GetTextOperationResultAsync(operationId);

            // Wait for the operation to complete
            int i = 0;
            int maxRetries = 10;
            while ((result.Status == TextOperationStatusCodes.Running ||
                    result.Status == TextOperationStatusCodes.NotStarted) && i++ < maxRetries)
            {
                Console.WriteLine(
                    "Server status: {0}, waiting {1} seconds...", result.Status, i);
                await Task.Delay(1000);

                result = await computerVision.GetTextOperationResultAsync(operationId);
            }

            // Display the results
            Console.WriteLine();
            var lines = result.RecognitionResult.Lines;
            foreach(Line line in lines)
            {
                Console.WriteLine(line.Text);
            }
            Console.WriteLine();
        }
    }
}
```

## <a name="recognizetextasync-response"></a><span data-ttu-id="23413-127">RecognizeTextAsync response</span><span class="sxs-lookup"><span data-stu-id="23413-127">RecognizeTextAsync response</span></span>

<span data-ttu-id="23413-128">A successful response displays the lines of recognized text for each image.</span><span class="sxs-lookup"><span data-stu-id="23413-128">A successful response displays the lines of recognized text for each image.</span></span>

<span data-ttu-id="23413-129">See [Quickstart: Extract handwritten text - REST, C#](../QuickStarts/CSharp-hand-text.md#examine-the-response) for an example of raw JSON output.</span><span class="sxs-lookup"><span data-stu-id="23413-129">See [Quickstart: Extract handwritten text - REST, C#](../QuickStarts/CSharp-hand-text.md#examine-the-response) for an example of raw JSON output.</span></span>

```cmd
Calling GetHandwritingRecognitionOperationResultAsync()

Calling GetHandwritingRecognitionOperationResultAsync()
Server status: Running, waiting 1 seconds...
Server status: Running, waiting 1 seconds...

dog
The quick brown fox jumps over the lazy
Pack my box with five dozen liquor jugs
```

## <a name="next-steps"></a><span data-ttu-id="23413-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="23413-130">Next steps</span></span>

<span data-ttu-id="23413-131">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="23413-131">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="23413-132">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="23413-132">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
