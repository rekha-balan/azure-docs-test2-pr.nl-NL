---
title: Emotion API C# tutorial | Microsoft Docs
description: Explore a basic Windows app that uses the Cognitive Services Emotion API to recognize the emotions expressed by faces in an image.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: emotion
ms.topic: article
ms.date: 01/23/2017
ms.author: anroth
ms.openlocfilehash: cf9d9a35f7d4acb6aa68aff300dfb2f0c4ac3b69
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540963"
---
# <a name="emotion-api-in-c35-tutorial"></a><span data-ttu-id="a7ab9-103">Emotion API in C&#35; Tutorial</span><span class="sxs-lookup"><span data-stu-id="a7ab9-103">Emotion API in C&#35; Tutorial</span></span>

<span data-ttu-id="a7ab9-104">Explore a basic Windows application that uses Emotion API to recognize the emotions expressed by the faces in an image.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-104">Explore a basic Windows application that uses Emotion API to recognize the emotions expressed by the faces in an image.</span></span> <span data-ttu-id="a7ab9-105">The below example lets you submit an image URL or a locally stored file.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-105">The below example lets you submit an image URL or a locally stored file.</span></span> <span data-ttu-id="a7ab9-106">You can use this open source example as a template for building your own app for Windows using the Emotion API and WPF (Windows Presentation Foundation), a part of .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-106">You can use this open source example as a template for building your own app for Windows using the Emotion API and WPF (Windows Presentation Foundation), a part of .NET Framework.</span></span>

## <span data-ttu-id="a7ab9-107"><a name="Prerequisites">Prerequisites</a></span><span class="sxs-lookup"><span data-stu-id="a7ab9-107"><a name="Prerequisites">Prerequisites</a></span></span>
#### <a name="platform-requirements"></a><span data-ttu-id="a7ab9-108">Platform requirements</span><span class="sxs-lookup"><span data-stu-id="a7ab9-108">Platform requirements</span></span>  
<span data-ttu-id="a7ab9-109">The below example has been developed for the .NET Framework using [Visual Studio 2015, Community Edition](https://www.visualstudio.com/products/visual-studio-community-vs).</span><span class="sxs-lookup"><span data-stu-id="a7ab9-109">The below example has been developed for the .NET Framework using [Visual Studio 2015, Community Edition](https://www.visualstudio.com/products/visual-studio-community-vs).</span></span>  

#### <a name="subscribe-to-emotion-api-and-get-a-subscription-key"></a><span data-ttu-id="a7ab9-110">Subscribe to Emotion API and get a subscription key</span><span class="sxs-lookup"><span data-stu-id="a7ab9-110">Subscribe to Emotion API and get a subscription key</span></span>  
<span data-ttu-id="a7ab9-111">Before creating the example, you must subscribe to Emotion API which is part of the Microsoft Cognitive Services (previously Project Oxford).</span><span class="sxs-lookup"><span data-stu-id="a7ab9-111">Before creating the example, you must subscribe to Emotion API which is part of the Microsoft Cognitive Services (previously Project Oxford).</span></span> <span data-ttu-id="a7ab9-112">See [Subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span><span class="sxs-lookup"><span data-stu-id="a7ab9-112">See [Subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span></span> <span data-ttu-id="a7ab9-113">Both the primary and secondary key can be used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-113">Both the primary and secondary key can be used in this tutorial.</span></span> <span data-ttu-id="a7ab9-114">Make sure to follow best practices for keeping your API key secret and secure.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-114">Make sure to follow best practices for keeping your API key secret and secure.</span></span>  

#### <a name="get-the-client-library-and-example"></a><span data-ttu-id="a7ab9-115">Get the client library and example</span><span class="sxs-lookup"><span data-stu-id="a7ab9-115">Get the client library and example</span></span>  
<span data-ttu-id="a7ab9-116">You may download the Emotion API client library via [SDK](https://www.github.com/microsoft/cognitive-emotion-windows).</span><span class="sxs-lookup"><span data-stu-id="a7ab9-116">You may download the Emotion API client library via [SDK](https://www.github.com/microsoft/cognitive-emotion-windows).</span></span> <span data-ttu-id="a7ab9-117">The downloaded zip file needs to be extracted to a folder of your choice, many users choose the Visual Studio 2015 folder.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-117">The downloaded zip file needs to be extracted to a folder of your choice, many users choose the Visual Studio 2015 folder.</span></span>
## <span data-ttu-id="a7ab9-118"><a name="Step1">Step 1: Open the example</a></span><span class="sxs-lookup"><span data-stu-id="a7ab9-118"><a name="Step1">Step 1: Open the example</a></span></span>
1.  <span data-ttu-id="a7ab9-119">Start Microsoft Visual Studio 2015 and click **File**, select **Open**, then **Project/Solution**.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-119">Start Microsoft Visual Studio 2015 and click **File**, select **Open**, then **Project/Solution**.</span></span>
2.  <span data-ttu-id="a7ab9-120">Browse to the folder where you saved the downloaded Emotion API files.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-120">Browse to the folder where you saved the downloaded Emotion API files.</span></span> <span data-ttu-id="a7ab9-121">Click on **Emotion**, then **Windows**, and then the **Sample-WPF** folder.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-121">Click on **Emotion**, then **Windows**, and then the **Sample-WPF** folder.</span></span>
3.  <span data-ttu-id="a7ab9-122">Double-click to open the Visual Studio 2015 Solution (.sln) file named **EmotionAPI-WPF-Samples.sln**.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-122">Double-click to open the Visual Studio 2015 Solution (.sln) file named **EmotionAPI-WPF-Samples.sln**.</span></span> <span data-ttu-id="a7ab9-123">This will open the solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-123">This will open the solution in Visual Studio.</span></span>

## <span data-ttu-id="a7ab9-124"><a name="Step2">Step 2: Build the example</a></span><span class="sxs-lookup"><span data-stu-id="a7ab9-124"><a name="Step2">Step 2: Build the example</a></span></span>
1. <span data-ttu-id="a7ab9-125">In **Solution Explorer**, right click **References** and select **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-125">In **Solution Explorer**, right click **References** and select **Manage NuGet Packages**.</span></span>

  ![Open Nuget Package Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Emotion/Images/EmotionNuget.png)

2.  <span data-ttu-id="a7ab9-127">The **NuGet Package Manager** window opens.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-127">The **NuGet Package Manager** window opens.</span></span> <span data-ttu-id="a7ab9-128">First select **Browse** in the upper left corner, then in the search box type “Newtonsoft.Json”, select the **Newtonsoft.Json** package and click **Install**.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-128">First select **Browse** in the upper left corner, then in the search box type “Newtonsoft.Json”, select the **Newtonsoft.Json** package and click **Install**.</span></span>  

  ![Browse to NuGet Package](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Emotion/Images/EmotionNugetBrowse.png)  

3.  <span data-ttu-id="a7ab9-130">Press Ctrl+Shift+B, or click **Build** on the ribbon menu, then select **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-130">Press Ctrl+Shift+B, or click **Build** on the ribbon menu, then select **Build Solution**.</span></span>

## <span data-ttu-id="a7ab9-131"><a name="Step3">Step 3: Run the example</a></span><span class="sxs-lookup"><span data-stu-id="a7ab9-131"><a name="Step3">Step 3: Run the example</a></span></span>
1.  <span data-ttu-id="a7ab9-132">After the build is complete, press **F5** or click **Start** on the ribbon menu to run the example.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-132">After the build is complete, press **F5** or click **Start** on the ribbon menu to run the example.</span></span>
2.  <span data-ttu-id="a7ab9-133">Locate the Emotion API window with the **text box** reading "**Paste your subscription key here to start**".</span><span class="sxs-lookup"><span data-stu-id="a7ab9-133">Locate the Emotion API window with the **text box** reading "**Paste your subscription key here to start**".</span></span> <span data-ttu-id="a7ab9-134">Paste your subscription key into the text box as shown in below screenshot.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-134">Paste your subscription key into the text box as shown in below screenshot.</span></span> <span data-ttu-id="a7ab9-135">You can choose to persist your subscription key on your PC or laptop by clicking the "Save Key" button.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-135">You can choose to persist your subscription key on your PC or laptop by clicking the "Save Key" button.</span></span> <span data-ttu-id="a7ab9-136">When you want to delete the subscription key from the system, click "Delete Key" to remove it from your PC or laptop.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-136">When you want to delete the subscription key from the system, click "Delete Key" to remove it from your PC or laptop.</span></span>
  
  ![Emotion Functionality Interface](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Emotion/Images/EmotionKey.png)

3.  <span data-ttu-id="a7ab9-138">Under "**Select Scenario**" click to use either of the two scenarios, “**Detect emotion using a stream**” or “**Detect emotion using a URL**”, then follow the instructions on the screen.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-138">Under "**Select Scenario**" click to use either of the two scenarios, “**Detect emotion using a stream**” or “**Detect emotion using a URL**”, then follow the instructions on the screen.</span></span> <span data-ttu-id="a7ab9-139">Microsoft receives the images you upload and may use them to improve Emotion API and related services.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-139">Microsoft receives the images you upload and may use them to improve Emotion API and related services.</span></span> <span data-ttu-id="a7ab9-140">By submitting an image, you confirm that you have followed our [Developer Code of Conduct](http://research.microsoft.com/en-us/UM/legal/ProjectOxford_CodeOfConduct.htm).</span><span class="sxs-lookup"><span data-stu-id="a7ab9-140">By submitting an image, you confirm that you have followed our [Developer Code of Conduct](http://research.microsoft.com/en-us/UM/legal/ProjectOxford_CodeOfConduct.htm).</span></span>
4.  <span data-ttu-id="a7ab9-141">There are example images to be used with this example application.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-141">There are example images to be used with this example application.</span></span> <span data-ttu-id="a7ab9-142">You can find these images on [the Face API Github repo](https://github.com/Microsoft/Cognitive-Face-Windows/tree/master/Data) under the **Data** folder.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-142">You can find these images on [the Face API Github repo](https://github.com/Microsoft/Cognitive-Face-Windows/tree/master/Data) under the **Data** folder.</span></span> <span data-ttu-id="a7ab9-143">Please note the use of these images is licensed under Fair Use agreement meaning they are OK to use for testing this example, but not for republishing.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-143">Please note the use of these images is licensed under Fair Use agreement meaning they are OK to use for testing this example, but not for republishing.</span></span>

## <span data-ttu-id="a7ab9-144"><a name="Review">Review and Learn</a></span><span class="sxs-lookup"><span data-stu-id="a7ab9-144"><a name="Review">Review and Learn</a></span></span>
<span data-ttu-id="a7ab9-145">Now that you have a running application, let us review how this example app integrates with Microsoft Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-145">Now that you have a running application, let us review how this example app integrates with Microsoft Cognitive Services.</span></span> <span data-ttu-id="a7ab9-146">This will make it easier to either continue building onto this app or develop your own app using Microsoft Emotion API.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-146">This will make it easier to either continue building onto this app or develop your own app using Microsoft Emotion API.</span></span> 

<span data-ttu-id="a7ab9-147">This example app makes use of the Emotion API Client Library, a thin C# client wrapper for the Microsoft Emotion API.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-147">This example app makes use of the Emotion API Client Library, a thin C# client wrapper for the Microsoft Emotion API.</span></span> <span data-ttu-id="a7ab9-148">When you built the example app as described above, you got the Client Library from a NuGet package.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-148">When you built the example app as described above, you got the Client Library from a NuGet package.</span></span> <span data-ttu-id="a7ab9-149">You can review the Client Library source code in the folder titled “[Client Library](https://github.com/Microsoft/Cognitive-Emotion-Windows/tree/master/ClientLibrary)” under **Emotion**, **Windows**, **Client Library**, which is part of the downloaded file repository mentioned above in [Prerequisites](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="a7ab9-149">You can review the Client Library source code in the folder titled “[Client Library](https://github.com/Microsoft/Cognitive-Emotion-Windows/tree/master/ClientLibrary)” under **Emotion**, **Windows**, **Client Library**, which is part of the downloaded file repository mentioned above in [Prerequisites](#Prerequisites).</span></span>
 
<span data-ttu-id="a7ab9-150">You can also find out how to use the Client Library code in **Solution Explorer**: Under **EmotionAPI-WPF_Samples**, expand **DetectEmotionUsingStreamPage.xaml** to locate **DetectEmotionUsingStreamPage.xaml.cs**, which is used for browsing to a locally stored file, or expand **DetectEmotionUsingURLPage.xaml** to find **DetectEmotionUsingURLPage.xaml.cs**, which is used when uploading an image URL.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-150">You can also find out how to use the Client Library code in **Solution Explorer**: Under **EmotionAPI-WPF_Samples**, expand **DetectEmotionUsingStreamPage.xaml** to locate **DetectEmotionUsingStreamPage.xaml.cs**, which is used for browsing to a locally stored file, or expand **DetectEmotionUsingURLPage.xaml** to find **DetectEmotionUsingURLPage.xaml.cs**, which is used when uploading an image URL.</span></span> <span data-ttu-id="a7ab9-151">Double-click the .xaml.cs files to have them open in new windows in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-151">Double-click the .xaml.cs files to have them open in new windows in Visual Studio.</span></span> 

<span data-ttu-id="a7ab9-152">Reviewing how the Emotion Client Library gets used in our example app, let's look at two code snippets from **DetectEmotionUsingStreamPage.xaml.cs** and **DetectEmotionUsingURLPage.xaml.cs**.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-152">Reviewing how the Emotion Client Library gets used in our example app, let's look at two code snippets from **DetectEmotionUsingStreamPage.xaml.cs** and **DetectEmotionUsingURLPage.xaml.cs**.</span></span> <span data-ttu-id="a7ab9-153">Each file contains code comments indicating “KEY SAMPLE CODE STARTS HERE” and “KEY SAMPLE CODE ENDS HERE” to help you locate the code snippets reproduced below.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-153">Each file contains code comments indicating “KEY SAMPLE CODE STARTS HERE” and “KEY SAMPLE CODE ENDS HERE” to help you locate the code snippets reproduced below.</span></span>

<span data-ttu-id="a7ab9-154">The Emotion API is able to work with either an image URL or binary image data (in form of an octet stream) as input.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-154">The Emotion API is able to work with either an image URL or binary image data (in form of an octet stream) as input.</span></span> <span data-ttu-id="a7ab9-155">The two options are reviewed below.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-155">The two options are reviewed below.</span></span> <span data-ttu-id="a7ab9-156">In both cases, you first find a using directive, which lets you use the Emotion Client Library.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-156">In both cases, you first find a using directive, which lets you use the Emotion Client Library.</span></span> 
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
#### <a name="detectemotionusingurlpagexamlcs"></a><span data-ttu-id="a7ab9-157">DetectEmotionUsingURLPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="a7ab9-157">DetectEmotionUsingURLPage.xaml.cs</span></span> 

<span data-ttu-id="a7ab9-158">This code snippet shows how to use the Client Library to submit your subscription key and a photo URL to the Emotion API service.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-158">This code snippet shows how to use the Client Library to submit your subscription key and a photo URL to the Emotion API service.</span></span> 

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
#### <a name="detectemotionusingstreampagexamlcs"></a><span data-ttu-id="a7ab9-159">DetectEmotionUsingStreamPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="a7ab9-159">DetectEmotionUsingStreamPage.xaml.cs</span></span> 

<span data-ttu-id="a7ab9-160">Shown below is how to submit your subscription key and a locally stored image to the Emotion API.</span><span class="sxs-lookup"><span data-stu-id="a7ab9-160">Shown below is how to submit your subscription key and a locally stored image to the Emotion API.</span></span> 


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



