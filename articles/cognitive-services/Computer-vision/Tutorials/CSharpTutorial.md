---
title: Computer Vision API C# tutorial | Microsoft Docs
description: Explore a basic Windows app that uses the Computer Vision API in Microsoft Cognitive Services. Perform OCR, create thumbnails, and work with visual features in an image.
services: cognitive-services
author: KellyDF
manager: corncar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: article
ms.date: 05/22/2017
ms.author: kefre
ms.openlocfilehash: f2aeb1734f8858ed8b80e5cdf48ef7e558703919
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809262"
---
# <a name="computer-vision-api-c35-tutorial"></a><span data-ttu-id="dd2da-104">Computer Vision API C&#35; Tutorial</span><span class="sxs-lookup"><span data-stu-id="dd2da-104">Computer Vision API C&#35; Tutorial</span></span>

<span data-ttu-id="dd2da-105">Explore a basic Windows application that uses Computer Vision API to perform optical character recognition (OCR), create smart-cropped thumbnails, plus detect, categorize, tag and describe visual features, including faces, in an image.</span><span class="sxs-lookup"><span data-stu-id="dd2da-105">Explore a basic Windows application that uses Computer Vision API to perform optical character recognition (OCR), create smart-cropped thumbnails, plus detect, categorize, tag and describe visual features, including faces, in an image.</span></span> <span data-ttu-id="dd2da-106">The below example lets you submit an image URL or a locally stored file.</span><span class="sxs-lookup"><span data-stu-id="dd2da-106">The below example lets you submit an image URL or a locally stored file.</span></span> <span data-ttu-id="dd2da-107">You can use this open source example as a template for building your own app for Windows using the Vision API and WPF (Windows Presentation Foundation), a part of .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="dd2da-107">You can use this open source example as a template for building your own app for Windows using the Vision API and WPF (Windows Presentation Foundation), a part of .NET Framework.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="dd2da-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dd2da-108">Prerequisites</span></span>

#### <a name="platform-requirements"></a><span data-ttu-id="dd2da-109">Platform requirements</span><span class="sxs-lookup"><span data-stu-id="dd2da-109">Platform requirements</span></span>

<span data-ttu-id="dd2da-110">The below example has been developed for the .NET Framework using [Visual Studio 2015, Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="dd2da-110">The below example has been developed for the .NET Framework using [Visual Studio 2015, Community Edition](https://www.visualstudio.com/downloads/).</span></span>

#### <a name="subscribe-to-computer-vision-api-and-get-a-subscription-key"></a><span data-ttu-id="dd2da-111">Subscribe to Computer Vision API and get a subscription key</span><span class="sxs-lookup"><span data-stu-id="dd2da-111">Subscribe to Computer Vision API and get a subscription key</span></span> 

<span data-ttu-id="dd2da-112">Before creating the example, you must subscribe to Computer Vision API which is part of the Microsoft Cognitive Services (formerly Project Oxford).</span><span class="sxs-lookup"><span data-stu-id="dd2da-112">Before creating the example, you must subscribe to Computer Vision API which is part of the Microsoft Cognitive Services (formerly Project Oxford).</span></span> <span data-ttu-id="dd2da-113">For subscription and key management details, see [Subscriptions](https://azure.microsoft.com/try/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="dd2da-113">For subscription and key management details, see [Subscriptions](https://azure.microsoft.com/try/cognitive-services/).</span></span> <span data-ttu-id="dd2da-114">Both the primary and secondary key can be used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="dd2da-114">Both the primary and secondary key can be used in this tutorial.</span></span> 

> [!NOTE]
> <span data-ttu-id="dd2da-115">The tutorial is designed to use subscription keys in the **westcentralus** region.</span><span class="sxs-lookup"><span data-stu-id="dd2da-115">The tutorial is designed to use subscription keys in the **westcentralus** region.</span></span> <span data-ttu-id="dd2da-116">The subscription keys generated in the Computer Vision free trail use the **westcentralus** region, so they work correctly.</span><span class="sxs-lookup"><span data-stu-id="dd2da-116">The subscription keys generated in the Computer Vision free trail use the **westcentralus** region, so they work correctly.</span></span> <span data-ttu-id="dd2da-117">If you generated your subscription keys using your Azure account through [https://azure.microsoft.com/](https://azure.microsoft.com/), you must specify the **westcentralus** region.</span><span class="sxs-lookup"><span data-stu-id="dd2da-117">If you generated your subscription keys using your Azure account through [https://azure.microsoft.com/](https://azure.microsoft.com/), you must specify the **westcentralus** region.</span></span> <span data-ttu-id="dd2da-118">Keys generated outside the **westcentralus** region will not work.</span><span class="sxs-lookup"><span data-stu-id="dd2da-118">Keys generated outside the **westcentralus** region will not work.</span></span>

#### <a name="get-the-client-library-and-example"></a><span data-ttu-id="dd2da-119">Get the client library and example</span><span class="sxs-lookup"><span data-stu-id="dd2da-119">Get the client library and example</span></span>

<span data-ttu-id="dd2da-120">You may clone the Computer Vision API client library and example application to your computer via [SDK](https://www.github.com/microsoft/cognitive-vision-windows).</span><span class="sxs-lookup"><span data-stu-id="dd2da-120">You may clone the Computer Vision API client library and example application to your computer via [SDK](https://www.github.com/microsoft/cognitive-vision-windows).</span></span> <span data-ttu-id="dd2da-121">Don't download it as a ZIP.</span><span class="sxs-lookup"><span data-stu-id="dd2da-121">Don't download it as a ZIP.</span></span>

### <span data-ttu-id="dd2da-122"><a name="Step1">Step 1: Install the example</a></span><span class="sxs-lookup"><span data-stu-id="dd2da-122"><a name="Step1">Step 1: Install the example</a></span></span>

<span data-ttu-id="dd2da-123">In your GitHub Desktop, open Sample-WPF\VisionAPI-WPF-Samples.sln.</span><span class="sxs-lookup"><span data-stu-id="dd2da-123">In your GitHub Desktop, open Sample-WPF\VisionAPI-WPF-Samples.sln.</span></span>

### <span data-ttu-id="dd2da-124"><a name="Step2">Step 2: Build the example</a></span><span class="sxs-lookup"><span data-stu-id="dd2da-124"><a name="Step2">Step 2: Build the example</a></span></span>

* <span data-ttu-id="dd2da-125">Press Ctrl+Shift+B, or click Build on the ribbon menu, then select Build Solution.</span><span class="sxs-lookup"><span data-stu-id="dd2da-125">Press Ctrl+Shift+B, or click Build on the ribbon menu, then select Build Solution.</span></span>

### <span data-ttu-id="dd2da-126"><a name="Step3">Step 3: Run the example</a></span><span class="sxs-lookup"><span data-stu-id="dd2da-126"><a name="Step3">Step 3: Run the example</a></span></span>

1. <span data-ttu-id="dd2da-127">After the build is complete, press **F5** or click **Start** on the ribbon menu to run the example.</span><span class="sxs-lookup"><span data-stu-id="dd2da-127">After the build is complete, press **F5** or click **Start** on the ribbon menu to run the example.</span></span>
2. <span data-ttu-id="dd2da-128">Locate the Computer Vision API user interface window with the text edit box reading "Paste your subscription key here to start".</span><span class="sxs-lookup"><span data-stu-id="dd2da-128">Locate the Computer Vision API user interface window with the text edit box reading "Paste your subscription key here to start".</span></span>
<span data-ttu-id="dd2da-129">You can choose to persist your subscription key on your PC or laptop by clicking the "Save Key" button.</span><span class="sxs-lookup"><span data-stu-id="dd2da-129">You can choose to persist your subscription key on your PC or laptop by clicking the "Save Key" button.</span></span> <span data-ttu-id="dd2da-130">When you want to delete the subscription key from the system, click "Delete Key" to remove it from your PC or laptop.</span><span class="sxs-lookup"><span data-stu-id="dd2da-130">When you want to delete the subscription key from the system, click "Delete Key" to remove it from your PC or laptop.</span></span>

    ![Vision Subscription Key](../Images/Vision_UI_Subscription.PNG)

3. <span data-ttu-id="dd2da-132">Under "Select Scenario" click to use one of the six scenarios, then follow the instructions on the screen.</span><span class="sxs-lookup"><span data-stu-id="dd2da-132">Under "Select Scenario" click to use one of the six scenarios, then follow the instructions on the screen.</span></span> <span data-ttu-id="dd2da-133">Microsoft receives the images you upload and may use them to improve Computer Vision API and related services.</span><span class="sxs-lookup"><span data-stu-id="dd2da-133">Microsoft receives the images you upload and may use them to improve Computer Vision API and related services.</span></span> <span data-ttu-id="dd2da-134">By submitting an image, you confirm that you have followed our [Developer Code of Conduct](https://azure.microsoft.com/support/legal/developer-code-of-conduct/).</span><span class="sxs-lookup"><span data-stu-id="dd2da-134">By submitting an image, you confirm that you have followed our [Developer Code of Conduct](https://azure.microsoft.com/support/legal/developer-code-of-conduct/).</span></span>

    ![Analyze Image Interface](../Images/Analyze_Image_Example.PNG)

4. <span data-ttu-id="dd2da-136">There are example images to be used with this example application.</span><span class="sxs-lookup"><span data-stu-id="dd2da-136">There are example images to be used with this example application.</span></span> <span data-ttu-id="dd2da-137">You can find these images on the Face API Windows Github repo, in the [Data folder](https://github.com/Microsoft/Cognitive-Face-Windows/tree/master/Data).</span><span class="sxs-lookup"><span data-stu-id="dd2da-137">You can find these images on the Face API Windows Github repo, in the [Data folder](https://github.com/Microsoft/Cognitive-Face-Windows/tree/master/Data).</span></span> <span data-ttu-id="dd2da-138">Please note the use of these images is licensed under agreement [LICENSE-IMAGE](https://github.com/Microsoft/Cognitive-Face-Windows/blob/master/LICENSE-IMAGE.md).</span><span class="sxs-lookup"><span data-stu-id="dd2da-138">Please note the use of these images is licensed under agreement [LICENSE-IMAGE](https://github.com/Microsoft/Cognitive-Face-Windows/blob/master/LICENSE-IMAGE.md).</span></span>

### <span data-ttu-id="dd2da-139"><a name="Review">Review and Learn</a></span><span class="sxs-lookup"><span data-stu-id="dd2da-139"><a name="Review">Review and Learn</a></span></span>

<span data-ttu-id="dd2da-140">Now that you have a running application, let us review how this example app integrates with Cognitive Services technology.</span><span class="sxs-lookup"><span data-stu-id="dd2da-140">Now that you have a running application, let us review how this example app integrates with Cognitive Services technology.</span></span> <span data-ttu-id="dd2da-141">This will make it easier to either continue building onto this app or develop your own app using Microsoft Computer Vision API.</span><span class="sxs-lookup"><span data-stu-id="dd2da-141">This will make it easier to either continue building onto this app or develop your own app using Microsoft Computer Vision API.</span></span>

<span data-ttu-id="dd2da-142">This example app makes use of the Computer Vision API Client Library, a thin C# client wrapper for the Microsoft Computer Vision API.</span><span class="sxs-lookup"><span data-stu-id="dd2da-142">This example app makes use of the Computer Vision API Client Library, a thin C# client wrapper for the Microsoft Computer Vision API.</span></span> <span data-ttu-id="dd2da-143">When you built the example app as described above, you got the Client Library from a NuGet package.</span><span class="sxs-lookup"><span data-stu-id="dd2da-143">When you built the example app as described above, you got the Client Library from a NuGet package.</span></span> <span data-ttu-id="dd2da-144">You can review the Client Library source code in the folder titled “**Client Library**” under **Vision**, **Windows**, **Client Library**, which is part of the downloaded file repository mentioned above in Prerequisites.</span><span class="sxs-lookup"><span data-stu-id="dd2da-144">You can review the Client Library source code in the folder titled “**Client Library**” under **Vision**, **Windows**, **Client Library**, which is part of the downloaded file repository mentioned above in Prerequisites.</span></span>

<span data-ttu-id="dd2da-145">You can also find out how to use the Client Library code in Solution Explorer: Under **VisionAPI-WPF_Samples**, expand **AnalyzePage.xaml** to locate **AnalyzePage.xaml.cs**, which is used for submitting an image to the image analysis endpoint.</span><span class="sxs-lookup"><span data-stu-id="dd2da-145">You can also find out how to use the Client Library code in Solution Explorer: Under **VisionAPI-WPF_Samples**, expand **AnalyzePage.xaml** to locate **AnalyzePage.xaml.cs**, which is used for submitting an image to the image analysis endpoint.</span></span> <span data-ttu-id="dd2da-146">Double-click the .xaml.cs files to have them open in new windows in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dd2da-146">Double-click the .xaml.cs files to have them open in new windows in Visual Studio.</span></span>

<span data-ttu-id="dd2da-147">Reviewing how the Vision Client Library gets used in our example app, let's look at two code snippets from **AnalyzePage.xaml.cs**.</span><span class="sxs-lookup"><span data-stu-id="dd2da-147">Reviewing how the Vision Client Library gets used in our example app, let's look at two code snippets from **AnalyzePage.xaml.cs**.</span></span> <span data-ttu-id="dd2da-148">The file contains code comments indicating “KEY SAMPLE CODE STARTS HERE” and “KEY SAMPLE CODE ENDS HERE” to help you locate the code snippets reproduced below.</span><span class="sxs-lookup"><span data-stu-id="dd2da-148">The file contains code comments indicating “KEY SAMPLE CODE STARTS HERE” and “KEY SAMPLE CODE ENDS HERE” to help you locate the code snippets reproduced below.</span></span>

<span data-ttu-id="dd2da-149">The analyze endpoint is able to work with either an image URL or binary image data (in form of an octet stream) as input.</span><span class="sxs-lookup"><span data-stu-id="dd2da-149">The analyze endpoint is able to work with either an image URL or binary image data (in form of an octet stream) as input.</span></span> <span data-ttu-id="dd2da-150">First, you find a using directive, which lets you use the Vision Client Library.</span><span class="sxs-lookup"><span data-stu-id="dd2da-150">First, you find a using directive, which lets you use the Vision Client Library.</span></span>

```
                // ----------------------------------------------------------------------
                // KEY SAMPLE CODE STARTS HERE
                // Use the following namespace for VisionServiceClient 
                // ---------------------------------------------------------------------- 
                using Microsoft.ProjectOxford.Vision; 
                using Microsoft.ProjectOxford.Vision.Contract; 
                // ----------------------------------------------------------------------
                // KEY SAMPLE CODE ENDS HERE 
                // ----------------------------------------------------------------------

```
<span data-ttu-id="dd2da-151">**UploadAndAnalyzeImage(…)** This code snippet shows how to use the Client Library to submit your subscription key and a locally stored image to the analyze endpoint of the Computer Vision API service.</span><span class="sxs-lookup"><span data-stu-id="dd2da-151">**UploadAndAnalyzeImage(…)** This code snippet shows how to use the Client Library to submit your subscription key and a locally stored image to the analyze endpoint of the Computer Vision API service.</span></span>

```
    private async Task<AnalysisResult> UploadAndAnalyzeImage(string imageFilePath)
    {
        // -----------------------------------------------------------------------
        // KEY SAMPLE CODE STARTS HERE
        // -----------------------------------------------------------------------  
        //
        // Create Project Oxford Computer Vision API Service client
        //
        VisionServiceClient VisionServiceClient = new VisionServiceClient(SubscriptionKey);
        Log("VisionServiceClient is created");
    
        using (Stream imageFileStream = File.OpenRead(imageFilePath))
        {
            //
            // Analyze the image for all visual features
            //
            Log("Calling VisionServiceClient.AnalyzeImageAsync()...");
         VisualFeature[] visualFeatures = new VisualFeature[] { VisualFeature.Adult, VisualFeature.Categories, VisualFeature.Color, VisualFeature.Description, VisualFeature.Faces, VisualFeature.ImageType, VisualFeature.Tags };
            AnalysisResult analysisResult = await VisionServiceClient.AnalyzeImageAsync(imageFileStream, visualFeatures);
            return analysisResult;
        }
    
        // -----------------------------------------------------------------------
        // KEY SAMPLE CODE ENDS HERE
        // -----------------------------------------------------------------------
        }
```
<span data-ttu-id="dd2da-152">**AnalyzeUrl(…)** This code snippet shows how to use the Client Library to submit your subscription key and a photo URL to the analyze endpoint of the Computer Vision API service.</span><span class="sxs-lookup"><span data-stu-id="dd2da-152">**AnalyzeUrl(…)** This code snippet shows how to use the Client Library to submit your subscription key and a photo URL to the analyze endpoint of the Computer Vision API service.</span></span>

```
    private async Task<AnalysisResult> AnalyzeUrl(string imageUrl)
    {
        // -----------------------------------------------------------------------
        // KEY SAMPLE CODE STARTS HERE
        // -----------------------------------------------------------------------
    
        //
        // Create Project Oxford Computer Vision API Service client
        //
     VisionServiceClient VisionServiceClient = new VisionServiceClient(SubscriptionKey);
        Log("VisionServiceClient is created");
    
        //
        // Analyze the url for all visual features
        //
        Log("Calling VisionServiceClient.AnalyzeImageAsync()...");
        VisualFeature[] visualFeatures = new VisualFeature[] { VisualFeature.Adult, VisualFeature.Categories, VisualFeature.Color, VisualFeature.Description, VisualFeature.Faces, VisualFeature.ImageType, VisualFeature.Tags };
        AnalysisResult analysisResult = await VisionServiceClient.AnalyzeImageAsync(imageUrl, visualFeatures);
     return analysisResult;
    }
        // -----------------------------------------------------------------------
        // KEY SAMPLE CODE ENDS HERE
        // -----------------------------------------------------------------------
```
<span data-ttu-id="dd2da-153">**Other pages and endpoints** How to interact with the other endpoints exposed by the Computer Vision API service can be seen by looking at the other pages in the sample; for instance, the OCR endpoint is shown as part of the code contained in OCRPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="dd2da-153">**Other pages and endpoints** How to interact with the other endpoints exposed by the Computer Vision API service can be seen by looking at the other pages in the sample; for instance, the OCR endpoint is shown as part of the code contained in OCRPage.xaml.cs</span></span> 

### <span data-ttu-id="dd2da-154"><a name="Related">Related Topics</a></span><span class="sxs-lookup"><span data-stu-id="dd2da-154"><a name="Related">Related Topics</a></span></span>
 * [<span data-ttu-id="dd2da-155">Get started with Face API</span><span class="sxs-lookup"><span data-stu-id="dd2da-155">Get started with Face API</span></span>](../../Face/Tutorials/FaceAPIinCSharpTutorial.md)
 
 


