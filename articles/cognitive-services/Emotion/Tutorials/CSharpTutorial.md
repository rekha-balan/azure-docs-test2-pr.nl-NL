---
title: Emotion API C# tutorial | Microsoft Docs
description: Explore a basic Windows app that uses the Cognitive Services Emotion API to recognize the emotions expressed by faces in an image.
services: cognitive-services
author: anrothMSFT
manager: corncar
ms.service: cognitive-services
ms.component: emotion-api
ms.topic: article
ms.date: 01/23/2017
ms.author: anroth
ms.openlocfilehash: f015e5720f65d0951a77de76ce8882a6dcdc1c3b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819317"
---
# <a name="emotion-api-in-c35-tutorial"></a><span data-ttu-id="dfde1-103">Emotion API in C&#35; Tutorial</span><span class="sxs-lookup"><span data-stu-id="dfde1-103">Emotion API in C&#35; Tutorial</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dfde1-104">Video API Preview will end on October 30th, 2017.</span><span class="sxs-lookup"><span data-stu-id="dfde1-104">Video API Preview will end on October 30th, 2017.</span></span> <span data-ttu-id="dfde1-105">Try the new [Video Indexer API Preview](https://azure.microsoft.com/services/cognitive-services/video-indexer/) to easily extract insights from videos and to enhance content discovery experiences, such as search results, by detecting spoken words, faces, characters, and emotions.</span><span class="sxs-lookup"><span data-stu-id="dfde1-105">Try the new [Video Indexer API Preview](https://azure.microsoft.com/services/cognitive-services/video-indexer/) to easily extract insights from videos and to enhance content discovery experiences, such as search results, by detecting spoken words, faces, characters, and emotions.</span></span> <span data-ttu-id="dfde1-106">[Learn more](https://docs.microsoft.com/azure/cognitive-services/video-indexer/video-indexer-overview).</span><span class="sxs-lookup"><span data-stu-id="dfde1-106">[Learn more](https://docs.microsoft.com/azure/cognitive-services/video-indexer/video-indexer-overview).</span></span>

<span data-ttu-id="dfde1-107">Explore a basic Windows application that uses Emotion API to recognize the emotions expressed by the faces in an image.</span><span class="sxs-lookup"><span data-stu-id="dfde1-107">Explore a basic Windows application that uses Emotion API to recognize the emotions expressed by the faces in an image.</span></span> <span data-ttu-id="dfde1-108">The below example lets you submit an image URL or a locally stored file.</span><span class="sxs-lookup"><span data-stu-id="dfde1-108">The below example lets you submit an image URL or a locally stored file.</span></span> <span data-ttu-id="dfde1-109">You can use this open source example as a template for building your own app for Windows using the Emotion API and WPF (Windows Presentation Foundation), a part of .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="dfde1-109">You can use this open source example as a template for building your own app for Windows using the Emotion API and WPF (Windows Presentation Foundation), a part of .NET Framework.</span></span>

## <span data-ttu-id="dfde1-110"><a name="Prerequisites">Prerequisites</a></span><span class="sxs-lookup"><span data-stu-id="dfde1-110"><a name="Prerequisites">Prerequisites</a></span></span>
#### <a name="platform-requirements"></a><span data-ttu-id="dfde1-111">Platform requirements</span><span class="sxs-lookup"><span data-stu-id="dfde1-111">Platform requirements</span></span>  
<span data-ttu-id="dfde1-112">The below example has been developed for the .NET Framework using [Visual Studio 2015, Community Edition](https://www.visualstudio.com/products/visual-studio-community-vs).</span><span class="sxs-lookup"><span data-stu-id="dfde1-112">The below example has been developed for the .NET Framework using [Visual Studio 2015, Community Edition](https://www.visualstudio.com/products/visual-studio-community-vs).</span></span>  

#### <a name="subscribe-to-emotion-api-and-get-a-subscription-key"></a><span data-ttu-id="dfde1-113">Subscribe to Emotion API and get a subscription key</span><span class="sxs-lookup"><span data-stu-id="dfde1-113">Subscribe to Emotion API and get a subscription key</span></span>  
<span data-ttu-id="dfde1-114">Before creating the example, you must subscribe to Emotion API which is part of the Microsoft Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="dfde1-114">Before creating the example, you must subscribe to Emotion API which is part of the Microsoft Cognitive Services.</span></span> <span data-ttu-id="dfde1-115">See [Subscriptions](https://azure.microsoft.com/try/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="dfde1-115">See [Subscriptions](https://azure.microsoft.com/try/cognitive-services/).</span></span> <span data-ttu-id="dfde1-116">Both the primary and secondary key can be used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="dfde1-116">Both the primary and secondary key can be used in this tutorial.</span></span> <span data-ttu-id="dfde1-117">Make sure to follow best practices for keeping your API key secret and secure.</span><span class="sxs-lookup"><span data-stu-id="dfde1-117">Make sure to follow best practices for keeping your API key secret and secure.</span></span>  

#### <a name="get-the-client-library-and-example"></a><span data-ttu-id="dfde1-118">Get the client library and example</span><span class="sxs-lookup"><span data-stu-id="dfde1-118">Get the client library and example</span></span>  
<span data-ttu-id="dfde1-119">You may download the Emotion API client library via [SDK](https://www.github.com/microsoft/cognitive-emotion-windows).</span><span class="sxs-lookup"><span data-stu-id="dfde1-119">You may download the Emotion API client library via [SDK](https://www.github.com/microsoft/cognitive-emotion-windows).</span></span> <span data-ttu-id="dfde1-120">The downloaded zip file needs to be extracted to a folder of your choice, many users choose the Visual Studio 2015 folder.</span><span class="sxs-lookup"><span data-stu-id="dfde1-120">The downloaded zip file needs to be extracted to a folder of your choice, many users choose the Visual Studio 2015 folder.</span></span>
## <span data-ttu-id="dfde1-121"><a name="Step1">Step 1: Open the example</a></span><span class="sxs-lookup"><span data-stu-id="dfde1-121"><a name="Step1">Step 1: Open the example</a></span></span>
1.  <span data-ttu-id="dfde1-122">Start Microsoft Visual Studio 2015 and click **File**, select **Open**, then **Project/Solution**.</span><span class="sxs-lookup"><span data-stu-id="dfde1-122">Start Microsoft Visual Studio 2015 and click **File**, select **Open**, then **Project/Solution**.</span></span>
2.  <span data-ttu-id="dfde1-123">Browse to the folder where you saved the downloaded Emotion API files.</span><span class="sxs-lookup"><span data-stu-id="dfde1-123">Browse to the folder where you saved the downloaded Emotion API files.</span></span> <span data-ttu-id="dfde1-124">Click on **Emotion**, then **Windows**, and then the **Sample-WPF** folder.</span><span class="sxs-lookup"><span data-stu-id="dfde1-124">Click on **Emotion**, then **Windows**, and then the **Sample-WPF** folder.</span></span>
3.  <span data-ttu-id="dfde1-125">Double-click to open the Visual Studio 2015 Solution (.sln) file named **EmotionAPI-WPF-Samples.sln**.</span><span class="sxs-lookup"><span data-stu-id="dfde1-125">Double-click to open the Visual Studio 2015 Solution (.sln) file named **EmotionAPI-WPF-Samples.sln**.</span></span> <span data-ttu-id="dfde1-126">This will open the solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dfde1-126">This will open the solution in Visual Studio.</span></span>

## <span data-ttu-id="dfde1-127"><a name="Step2">Step 2: Build the example</a></span><span class="sxs-lookup"><span data-stu-id="dfde1-127"><a name="Step2">Step 2: Build the example</a></span></span>
1. <span data-ttu-id="dfde1-128">In **Solution Explorer**, right click **References** and select **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="dfde1-128">In **Solution Explorer**, right click **References** and select **Manage NuGet Packages**.</span></span>

  ![Open Nuget Package Manager](../Images/EmotionNuget.png)

2.  <span data-ttu-id="dfde1-130">The **NuGet Package Manager** window opens.</span><span class="sxs-lookup"><span data-stu-id="dfde1-130">The **NuGet Package Manager** window opens.</span></span> <span data-ttu-id="dfde1-131">First select **Browse** in the upper left corner, then in the search box type “Newtonsoft.Json”, select the **Newtonsoft.Json** package and click **Install**.</span><span class="sxs-lookup"><span data-stu-id="dfde1-131">First select **Browse** in the upper left corner, then in the search box type “Newtonsoft.Json”, select the **Newtonsoft.Json** package and click **Install**.</span></span>  

  ![Browse to NuGet Package](../Images/EmotionNugetBrowse.png)  

3.  <span data-ttu-id="dfde1-133">Press Ctrl+Shift+B, or click **Build** on the ribbon menu, then select **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="dfde1-133">Press Ctrl+Shift+B, or click **Build** on the ribbon menu, then select **Build Solution**.</span></span>

## <span data-ttu-id="dfde1-134"><a name="Step3">Step 3: Run the example</a></span><span class="sxs-lookup"><span data-stu-id="dfde1-134"><a name="Step3">Step 3: Run the example</a></span></span>
1.  <span data-ttu-id="dfde1-135">After the build is complete, press **F5** or click **Start** on the ribbon menu to run the example.</span><span class="sxs-lookup"><span data-stu-id="dfde1-135">After the build is complete, press **F5** or click **Start** on the ribbon menu to run the example.</span></span>
2.  <span data-ttu-id="dfde1-136">Locate the Emotion API window with the **text box** reading "**Paste your subscription key here to start**".</span><span class="sxs-lookup"><span data-stu-id="dfde1-136">Locate the Emotion API window with the **text box** reading "**Paste your subscription key here to start**".</span></span> <span data-ttu-id="dfde1-137">Paste your subscription key into the text box as shown in below screenshot.</span><span class="sxs-lookup"><span data-stu-id="dfde1-137">Paste your subscription key into the text box as shown in below screenshot.</span></span> <span data-ttu-id="dfde1-138">You can choose to persist your subscription key on your PC or laptop by clicking the "Save Key" button.</span><span class="sxs-lookup"><span data-stu-id="dfde1-138">You can choose to persist your subscription key on your PC or laptop by clicking the "Save Key" button.</span></span> <span data-ttu-id="dfde1-139">When you want to delete the subscription key from the system, click "Delete Key" to remove it from your PC or laptop.</span><span class="sxs-lookup"><span data-stu-id="dfde1-139">When you want to delete the subscription key from the system, click "Delete Key" to remove it from your PC or laptop.</span></span>
  
  ![Emotion Functionality Interface](../Images/EmotionKey.png)

3.  <span data-ttu-id="dfde1-141">Under "**Select Scenario**" click to use either of the two scenarios, “**Detect emotion using a stream**” or “**Detect emotion using a URL**”, then follow the instructions on the screen.</span><span class="sxs-lookup"><span data-stu-id="dfde1-141">Under "**Select Scenario**" click to use either of the two scenarios, “**Detect emotion using a stream**” or “**Detect emotion using a URL**”, then follow the instructions on the screen.</span></span> <span data-ttu-id="dfde1-142">Microsoft receives the images you upload and may use them to improve Emotion API and related services.</span><span class="sxs-lookup"><span data-stu-id="dfde1-142">Microsoft receives the images you upload and may use them to improve Emotion API and related services.</span></span> <span data-ttu-id="dfde1-143">By submitting an image, you confirm that you have followed our [Developer Code of Conduct](https://azure.microsoft.com/support/legal/developer-code-of-conduct/).</span><span class="sxs-lookup"><span data-stu-id="dfde1-143">By submitting an image, you confirm that you have followed our [Developer Code of Conduct](https://azure.microsoft.com/support/legal/developer-code-of-conduct/).</span></span>
4.  <span data-ttu-id="dfde1-144">There are example images to be used with this example application.</span><span class="sxs-lookup"><span data-stu-id="dfde1-144">There are example images to be used with this example application.</span></span> <span data-ttu-id="dfde1-145">You can find these images on [the Face API Github repo](https://github.com/Microsoft/Cognitive-Face-Windows/tree/master/Data) under the **Data** folder.</span><span class="sxs-lookup"><span data-stu-id="dfde1-145">You can find these images on [the Face API Github repo](https://github.com/Microsoft/Cognitive-Face-Windows/tree/master/Data) under the **Data** folder.</span></span> <span data-ttu-id="dfde1-146">Please note the use of these images is licensed under Fair Use agreement meaning they are OK to use for testing this example, but not for republishing.</span><span class="sxs-lookup"><span data-stu-id="dfde1-146">Please note the use of these images is licensed under Fair Use agreement meaning they are OK to use for testing this example, but not for republishing.</span></span>

## <span data-ttu-id="dfde1-147"><a name="Review">Review and Learn</a></span><span class="sxs-lookup"><span data-stu-id="dfde1-147"><a name="Review">Review and Learn</a></span></span>
<span data-ttu-id="dfde1-148">Now that you have a running application, let us review how this example app integrates with Microsoft Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="dfde1-148">Now that you have a running application, let us review how this example app integrates with Microsoft Cognitive Services.</span></span> <span data-ttu-id="dfde1-149">This will make it easier to either continue building onto this app or develop your own app using Microsoft Emotion API.</span><span class="sxs-lookup"><span data-stu-id="dfde1-149">This will make it easier to either continue building onto this app or develop your own app using Microsoft Emotion API.</span></span> 

<span data-ttu-id="dfde1-150">This example app makes use of the Emotion API Client Library, a thin C# client wrapper for the Microsoft Emotion API.</span><span class="sxs-lookup"><span data-stu-id="dfde1-150">This example app makes use of the Emotion API Client Library, a thin C# client wrapper for the Microsoft Emotion API.</span></span> <span data-ttu-id="dfde1-151">When you built the example app as described above, you got the Client Library from a NuGet package.</span><span class="sxs-lookup"><span data-stu-id="dfde1-151">When you built the example app as described above, you got the Client Library from a NuGet package.</span></span> <span data-ttu-id="dfde1-152">You can review the Client Library source code in the folder titled “[Client Library](https://github.com/Microsoft/Cognitive-Emotion-Windows/tree/master/ClientLibrary)” under **Emotion**, **Windows**, **Client Library**, which is part of the downloaded file repository mentioned above in [Prerequisites](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="dfde1-152">You can review the Client Library source code in the folder titled “[Client Library](https://github.com/Microsoft/Cognitive-Emotion-Windows/tree/master/ClientLibrary)” under **Emotion**, **Windows**, **Client Library**, which is part of the downloaded file repository mentioned above in [Prerequisites](#Prerequisites).</span></span>
 
<span data-ttu-id="dfde1-153">You can also find out how to use the Client Library code in **Solution Explorer**: Under **EmotionAPI-WPF_Samples**, expand **DetectEmotionUsingStreamPage.xaml** to locate **DetectEmotionUsingStreamPage.xaml.cs**, which is used for browsing to a locally stored file, or expand **DetectEmotionUsingURLPage.xaml** to find **DetectEmotionUsingURLPage.xaml.cs**, which is used when uploading an image URL.</span><span class="sxs-lookup"><span data-stu-id="dfde1-153">You can also find out how to use the Client Library code in **Solution Explorer**: Under **EmotionAPI-WPF_Samples**, expand **DetectEmotionUsingStreamPage.xaml** to locate **DetectEmotionUsingStreamPage.xaml.cs**, which is used for browsing to a locally stored file, or expand **DetectEmotionUsingURLPage.xaml** to find **DetectEmotionUsingURLPage.xaml.cs**, which is used when uploading an image URL.</span></span> <span data-ttu-id="dfde1-154">Double-click the .xaml.cs files to have them open in new windows in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dfde1-154">Double-click the .xaml.cs files to have them open in new windows in Visual Studio.</span></span> 

<span data-ttu-id="dfde1-155">Reviewing how the Emotion Client Library gets used in our example app, let's look at two code snippets from **DetectEmotionUsingStreamPage.xaml.cs** and **DetectEmotionUsingURLPage.xaml.cs**.</span><span class="sxs-lookup"><span data-stu-id="dfde1-155">Reviewing how the Emotion Client Library gets used in our example app, let's look at two code snippets from **DetectEmotionUsingStreamPage.xaml.cs** and **DetectEmotionUsingURLPage.xaml.cs**.</span></span> <span data-ttu-id="dfde1-156">Each file contains code comments indicating “KEY SAMPLE CODE STARTS HERE” and “KEY SAMPLE CODE ENDS HERE” to help you locate the code snippets reproduced below.</span><span class="sxs-lookup"><span data-stu-id="dfde1-156">Each file contains code comments indicating “KEY SAMPLE CODE STARTS HERE” and “KEY SAMPLE CODE ENDS HERE” to help you locate the code snippets reproduced below.</span></span>

<span data-ttu-id="dfde1-157">The Emotion API is able to work with either an image URL or binary image data (in form of an octet stream) as input.</span><span class="sxs-lookup"><span data-stu-id="dfde1-157">The Emotion API is able to work with either an image URL or binary image data (in form of an octet stream) as input.</span></span> <span data-ttu-id="dfde1-158">The two options are reviewed below.</span><span class="sxs-lookup"><span data-stu-id="dfde1-158">The two options are reviewed below.</span></span> <span data-ttu-id="dfde1-159">In both cases, you first find a using directive, which lets you use the Emotion Client Library.</span><span class="sxs-lookup"><span data-stu-id="dfde1-159">In both cases, you first find a using directive, which lets you use the Emotion Client Library.</span></span> 
```csharp

            // ----------------------------------------------------------------------- 
            // KEY SAMPLE CODE STARTS HERE 
            // Use the following namespace for EmotionServiceClient 
            // ----------------------------------------------------------------------- 
            using Microsoft.ProjectOxford.Emotion; 
            using Microsoft.ProjectOxford.Emotion.Contract; 
            // ----------------------------------------------------------------------- 
            // KEY SAMPLE CODE ENDS HERE 
            // ----------------------------------------------------------------------- 
```
#### <a name="detectemotionusingurlpagexamlcs"></a><span data-ttu-id="dfde1-160">DetectEmotionUsingURLPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="dfde1-160">DetectEmotionUsingURLPage.xaml.cs</span></span> 

<span data-ttu-id="dfde1-161">This code snippet shows how to use the Client Library to submit your subscription key and a photo URL to the Emotion API service.</span><span class="sxs-lookup"><span data-stu-id="dfde1-161">This code snippet shows how to use the Client Library to submit your subscription key and a photo URL to the Emotion API service.</span></span> 

```csharp

            // -----------------------------------------------------------------------
            // KEY SAMPLE CODE STARTS HERE
            // -----------------------------------------------------------------------

            window.Log("EmotionServiceClient is created");

            //
            // Create Project Oxford Emotion API Service client
            //
            EmotionServiceClient emotionServiceClient = new EmotionServiceClient(subscriptionKey);

            window.Log("Calling EmotionServiceClient.RecognizeAsync()...");
            try
            {
                //
                // Detect the emotions in the URL
                //
                Emotion[] emotionResult = await emotionServiceClient.RecognizeAsync(url);
                return emotionResult;
            }
            catch (Exception exception)
            {
                window.Log("Detection failed. Please make sure that you have the right subscription key and proper URL to detect.");
                window.Log(exception.ToString());
                return null;
            }
            // -----------------------------------------------------------------------
            // KEY SAMPLE CODE ENDS HERE
            // -----------------------------------------------------------------------
```
#### <a name="detectemotionusingstreampagexamlcs"></a><span data-ttu-id="dfde1-162">DetectEmotionUsingStreamPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="dfde1-162">DetectEmotionUsingStreamPage.xaml.cs</span></span> 

<span data-ttu-id="dfde1-163">Shown below is how to submit your subscription key and a locally stored image to the Emotion API.</span><span class="sxs-lookup"><span data-stu-id="dfde1-163">Shown below is how to submit your subscription key and a locally stored image to the Emotion API.</span></span> 


```csharp


            // -----------------------------------------------------------------------
            // KEY SAMPLE CODE STARTS HERE
            // -----------------------------------------------------------------------

            //
            // Create Project Oxford Emotion API Service client
            //
            EmotionServiceClient emotionServiceClient = new EmotionServiceClient(subscriptionKey);

            window.Log("Calling EmotionServiceClient.RecognizeAsync()...");
            try
            {
                Emotion[] emotionResult;
                using (Stream imageFileStream = File.OpenRead(imageFilePath))
                {
                    //
                    // Detect the emotions in the URL
                    //
                    emotionResult = await emotionServiceClient.RecognizeAsync(imageFileStream);
                    return emotionResult;
                }
            }
            catch (Exception exception)
            {
                window.Log(exception.ToString());
                return null;
            }
            // -----------------------------------------------------------------------
            // KEY SAMPLE CODE ENDS HERE
            // -----------------------------------------------------------------------
```
<!--
## <a name="Related">Related Topics</a>
[Emotion API Overview](.)
-->
