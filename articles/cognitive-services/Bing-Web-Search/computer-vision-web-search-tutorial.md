---
title: Visual Search mobile app tutorial
description: Open Source C# application implementing visual search using the Cognitive Services Computer Vision API, Bing Web Search API, and Xamarin.Forms cross-platform framework.
services: bing-web-search, computer-vision
author: Aristoddle
manager: bking
ms.service: cognitive-services
ms.devlang: csharp
ms.topic: article
ms.date: 06/22/2017
ms.author: t-jolan
ms.openlocfilehash: 54dabaeaad2e49ba7cc138636054bc3dfa4b8379
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870117"
---
# <a name="visual-search-mobile-app-tutorial"></a><span data-ttu-id="0009c-103">Visual Search mobile app tutorial</span><span class="sxs-lookup"><span data-stu-id="0009c-103">Visual Search mobile app tutorial</span></span>

## <a name="introduction"></a><span data-ttu-id="0009c-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="0009c-104">Introduction</span></span>  
<span data-ttu-id="0009c-105">This tutorial explores the [Computer Vision API](https://azure.microsoft.com/services/cognitive-services/computer-vision/) and [Bing Web Search API](https://azure.microsoft.com/services/cognitive-services/bing-web-search-api/) endpoints and shows how they can be used to build a basic visual search application with [Xamarin.Forms](https://developer.xamarin.com/guides/xamarin-forms/).</span><span class="sxs-lookup"><span data-stu-id="0009c-105">This tutorial explores the [Computer Vision API](https://azure.microsoft.com/services/cognitive-services/computer-vision/) and [Bing Web Search API](https://azure.microsoft.com/services/cognitive-services/bing-web-search-api/) endpoints and shows how they can be used to build a basic visual search application with [Xamarin.Forms](https://developer.xamarin.com/guides/xamarin-forms/).</span></span>  <span data-ttu-id="0009c-106">Overall, this tutorial covers the following topics:</span><span class="sxs-lookup"><span data-stu-id="0009c-106">Overall, this tutorial covers the following topics:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="0009c-107">Setting up Visual Studio to develop Xamarin.Forms applications</span><span class="sxs-lookup"><span data-stu-id="0009c-107">Setting up Visual Studio to develop Xamarin.Forms applications</span></span>
> * <span data-ttu-id="0009c-108">Using the [Xamarin Media Plugin](https://github.com/jamesmontemagno/MediaPlugin) to capture and import image data</span><span class="sxs-lookup"><span data-stu-id="0009c-108">Using the [Xamarin Media Plugin](https://github.com/jamesmontemagno/MediaPlugin) to capture and import image data</span></span>
> * <span data-ttu-id="0009c-109">Parsing text from an image using the Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="0009c-109">Parsing text from an image using the Computer Vision APIs</span></span>
> * <span data-ttu-id="0009c-110">Sending search requests to the Bing Web Search API</span><span class="sxs-lookup"><span data-stu-id="0009c-110">Sending search requests to the Bing Web Search API</span></span>
> * <span data-ttu-id="0009c-111">Parsing JSON responses from both APIs with [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) (with LINQ and model object deserialization)</span><span class="sxs-lookup"><span data-stu-id="0009c-111">Parsing JSON responses from both APIs with [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) (with LINQ and model object deserialization)</span></span>
> * <span data-ttu-id="0009c-112">Creating a cross-platform Xamarin.Forms user interface for visual search</span><span class="sxs-lookup"><span data-stu-id="0009c-112">Creating a cross-platform Xamarin.Forms user interface for visual search</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0009c-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0009c-113">Prerequisites</span></span>

<span data-ttu-id="0009c-114">This example was developed using Xamarin.Forms with [Visual Studio 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0009c-114">This example was developed using Xamarin.Forms with [Visual Studio 2017](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="0009c-115">The Community Edition of Visual Studio 2017 may be used.</span><span class="sxs-lookup"><span data-stu-id="0009c-115">The Community Edition of Visual Studio 2017 may be used.</span></span> <span data-ttu-id="0009c-116">For more information about using Xamarin with Visual Studio, see the [Xamarin documentation](https://developer.xamarin.com/guides/cross-platform/getting_started/).</span><span class="sxs-lookup"><span data-stu-id="0009c-116">For more information about using Xamarin with Visual Studio, see the [Xamarin documentation](https://developer.xamarin.com/guides/cross-platform/getting_started/).</span></span>

<span data-ttu-id="0009c-117">This sample makes use of the following NuGet Packages:</span><span class="sxs-lookup"><span data-stu-id="0009c-117">This sample makes use of the following NuGet Packages:</span></span>

> [!div class="checklist"]
> * [<span data-ttu-id="0009c-118">Xamarin Media Plugin</span><span class="sxs-lookup"><span data-stu-id="0009c-118">Xamarin Media Plugin</span></span>](https://github.com/jamesmontemagno/MediaPlugin)
> * [<span data-ttu-id="0009c-119">Json.NET</span><span class="sxs-lookup"><span data-stu-id="0009c-119">Json.NET</span></span>](https://github.com/JamesNK/Newtonsoft.Json)

<span data-ttu-id="0009c-120">The application uses the following Cognitive Services APIs:</span><span class="sxs-lookup"><span data-stu-id="0009c-120">The application uses the following Cognitive Services APIs:</span></span>

> [!div class="checklist"]
> * [<span data-ttu-id="0009c-121">Bing Web Search API</span><span class="sxs-lookup"><span data-stu-id="0009c-121">Bing Web Search API</span></span>](https://azure.microsoft.com/services/cognitive-services/bing-web-search-api/) 
> * [<span data-ttu-id="0009c-122">Computer Vision API</span><span class="sxs-lookup"><span data-stu-id="0009c-122">Computer Vision API</span></span>](https://azure.microsoft.com/services/cognitive-services/computer-vision/)

<span data-ttu-id="0009c-123">To obtain 30-day trial keys for these APIs, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="0009c-123">To obtain 30-day trial keys for these APIs, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/).</span></span> <span data-ttu-id="0009c-124">For more information about obtaining keys for commercial use, see [Pricing](https://azure.microsoft.com/pricing/calculator/).</span><span class="sxs-lookup"><span data-stu-id="0009c-124">For more information about obtaining keys for commercial use, see [Pricing](https://azure.microsoft.com/pricing/calculator/).</span></span>

## <a name="setup-for-development"></a><span data-ttu-id="0009c-125">Setup for development</span><span class="sxs-lookup"><span data-stu-id="0009c-125">Setup for development</span></span>  

### <a name="installing-xamarin-on-windows"></a><span data-ttu-id="0009c-126">Installing Xamarin on Windows</span><span class="sxs-lookup"><span data-stu-id="0009c-126">Installing Xamarin on Windows</span></span>
<span data-ttu-id="0009c-127">With any edition of Visual Studio 2017 installed, open the Visual Studio Installer, select the hamburger menu associated with your Visual Studio installation, and choose **Modify**.</span><span class="sxs-lookup"><span data-stu-id="0009c-127">With any edition of Visual Studio 2017 installed, open the Visual Studio Installer, select the hamburger menu associated with your Visual Studio installation, and choose **Modify**.</span></span>  

![Visual Studio installer](./media/computer-vision-web-search-tutorial/visual-studio-installer.png) 

<span data-ttu-id="0009c-129">Scroll down to Mobile & Gaming and enable **Mobile Development with .NET**, if it isn't already enabled.</span><span class="sxs-lookup"><span data-stu-id="0009c-129">Scroll down to Mobile & Gaming and enable **Mobile Development with .NET**, if it isn't already enabled.</span></span>

![Visual Studio installer with Xamarin.Forms selected](./media/computer-vision-web-search-tutorial/xamarin-forms-is-enabled.png)

<span data-ttu-id="0009c-131">Finally, click **Modify** in the bottom right corner of the window and wait for Xamarin to install.</span><span class="sxs-lookup"><span data-stu-id="0009c-131">Finally, click **Modify** in the bottom right corner of the window and wait for Xamarin to install.</span></span>

### <a name="installing-xamarin-on-macos"></a><span data-ttu-id="0009c-132">Installing Xamarin on macOS</span><span class="sxs-lookup"><span data-stu-id="0009c-132">Installing Xamarin on macOS</span></span>
<span data-ttu-id="0009c-133">Xamarin comes pre-packaged with Visual Studio for Mac.</span><span class="sxs-lookup"><span data-stu-id="0009c-133">Xamarin comes pre-packaged with Visual Studio for Mac.</span></span> <span data-ttu-id="0009c-134">No installation should be needed.</span><span class="sxs-lookup"><span data-stu-id="0009c-134">No installation should be needed.</span></span>

## <a name="building-and-running-the-app"></a><span data-ttu-id="0009c-135">Building and running the app</span><span class="sxs-lookup"><span data-stu-id="0009c-135">Building and running the app</span></span>

<span data-ttu-id="0009c-136">A Visual Studio solution file *(.sln)* for the Visual Search application can be downloaded from [Visual Search App with Cognitive Services](https://azure.microsoft.com/resources/samples/cognitive-services-xamarin-forms-computer-vision-search/).</span><span class="sxs-lookup"><span data-stu-id="0009c-136">A Visual Studio solution file *(.sln)* for the Visual Search application can be downloaded from [Visual Search App with Cognitive Services](https://azure.microsoft.com/resources/samples/cognitive-services-xamarin-forms-computer-vision-search/).</span></span> <span data-ttu-id="0009c-137">You can download the ZIP archive using a Web browser, clone it to your workstation from GitHub, or download it using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0009c-137">You can download the ZIP archive using a Web browser, clone it to your workstation from GitHub, or download it using Visual Studio.</span></span>

<span data-ttu-id="0009c-138">To start working with the sample, open `VisualSearchApp.sln` in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0009c-138">To start working with the sample, open `VisualSearchApp.sln` in Visual Studio.</span></span>  <span data-ttu-id="0009c-139">Initializing the required components may take a moment.</span><span class="sxs-lookup"><span data-stu-id="0009c-139">Initializing the required components may take a moment.</span></span>

<span data-ttu-id="0009c-140">The application requires two third-party libraries: **Json.NET** and the **Xamarin Media Plugin**.</span><span class="sxs-lookup"><span data-stu-id="0009c-140">The application requires two third-party libraries: **Json.NET** and the **Xamarin Media Plugin**.</span></span> <span data-ttu-id="0009c-141">You can install these libraries right in Visual Studio with the NuGet Package Manager.</span><span class="sxs-lookup"><span data-stu-id="0009c-141">You can install these libraries right in Visual Studio with the NuGet Package Manager.</span></span> <span data-ttu-id="0009c-142">Choose  **Tools > NuGet Package Manager > Manage NuGet Packages For Solution**, or right-click the solution in Solution Explorer and choose **Manage NuGet Packages** from the context menu.</span><span class="sxs-lookup"><span data-stu-id="0009c-142">Choose  **Tools > NuGet Package Manager > Manage NuGet Packages For Solution**, or right-click the solution in Solution Explorer and choose **Manage NuGet Packages** from the context menu.</span></span>

<span data-ttu-id="0009c-143">In the NuGet window, search for and install **Xamarin Media plugin** (Xam.Plugin.Media) version 2.6.2 and **Json.NET** (Newtonsoft.Json) 10.0.3.</span><span class="sxs-lookup"><span data-stu-id="0009c-143">In the NuGet window, search for and install **Xamarin Media plugin** (Xam.Plugin.Media) version 2.6.2 and **Json.NET** (Newtonsoft.Json) 10.0.3.</span></span> <span data-ttu-id="0009c-144">Be sure to select all projects when installing.</span><span class="sxs-lookup"><span data-stu-id="0009c-144">Be sure to select all projects when installing.</span></span>

<span data-ttu-id="0009c-145">To build the application for all available platforms, press **Ctrl + Shift + B**, or click **Build** on the ribbon menu and choose **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="0009c-145">To build the application for all available platforms, press **Ctrl + Shift + B**, or click **Build** on the ribbon menu and choose **Build Solution**.</span></span>  <span data-ttu-id="0009c-146">To compile and test code for iOS from a Windows system, see [this guide](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/) for help.</span><span class="sxs-lookup"><span data-stu-id="0009c-146">To compile and test code for iOS from a Windows system, see [this guide](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/) for help.</span></span>

<span data-ttu-id="0009c-147">Before running the application, you must select a target Configuration, Platform, and Project.</span><span class="sxs-lookup"><span data-stu-id="0009c-147">Before running the application, you must select a target Configuration, Platform, and Project.</span></span>  <span data-ttu-id="0009c-148">Xamarin.Forms applications compile to native code for Windows, Android, and iOS.</span><span class="sxs-lookup"><span data-stu-id="0009c-148">Xamarin.Forms applications compile to native code for Windows, Android, and iOS.</span></span> <span data-ttu-id="0009c-149">This tutorial includes screenshots of the Windows version of the sample, but all versions are functionally equivalent.</span><span class="sxs-lookup"><span data-stu-id="0009c-149">This tutorial includes screenshots of the Windows version of the sample, but all versions are functionally equivalent.</span></span> <span data-ttu-id="0009c-150">The deployment settings used in this guide are shown here.</span><span class="sxs-lookup"><span data-stu-id="0009c-150">The deployment settings used in this guide are shown here.</span></span>  

![Visual Studio configured to compile for an Android phone](./media/computer-vision-web-search-tutorial/configuration-selection.png)

<span data-ttu-id="0009c-152">Once the build process has succeeded and you have selected a target platform, click the **Start** button in the toolbar or press **F5**.</span><span class="sxs-lookup"><span data-stu-id="0009c-152">Once the build process has succeeded and you have selected a target platform, click the **Start** button in the toolbar or press **F5**.</span></span> <span data-ttu-id="0009c-153">Visual Studio deploys your solution to your target platform and launches it.</span><span class="sxs-lookup"><span data-stu-id="0009c-153">Visual Studio deploys your solution to your target platform and launches it.</span></span>

<span data-ttu-id="0009c-154">The Add Keys page appears.</span><span class="sxs-lookup"><span data-stu-id="0009c-154">The Add Keys page appears.</span></span> <span data-ttu-id="0009c-155">(This page is defined in `AddKeysPage.xaml`.)</span><span class="sxs-lookup"><span data-stu-id="0009c-155">(This page is defined in `AddKeysPage.xaml`.)</span></span>  

![Image of the Add Keys Page](./media/computer-vision-web-search-tutorial/add-keys-page.png)  

<span data-ttu-id="0009c-157">Here, paste in your Computer Vision and Bing Web Search API keys.</span><span class="sxs-lookup"><span data-stu-id="0009c-157">Here, paste in your Computer Vision and Bing Web Search API keys.</span></span> <span data-ttu-id="0009c-158">The Computer Vision API also requires you to choose the server where the endpoint is hosted.</span><span class="sxs-lookup"><span data-stu-id="0009c-158">The Computer Vision API also requires you to choose the server where the endpoint is hosted.</span></span>

> [!TIP]
> <span data-ttu-id="0009c-159">To skip this page, enter this information in the appropriate locations in `App.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="0009c-159">To skip this page, enter this information in the appropriate locations in `App.xaml.cs`.</span></span> 

<span data-ttu-id="0009c-160">The application validates your keys by performing a test query, then takes you to the OCR Select page (defined in `OcrSelectPage.xaml`).</span><span class="sxs-lookup"><span data-stu-id="0009c-160">The application validates your keys by performing a test query, then takes you to the OCR Select page (defined in `OcrSelectPage.xaml`).</span></span>
   
![Image of the OCR Select Page](./media/computer-vision-web-search-tutorial/ocr-select-page.png)  

<span data-ttu-id="0009c-162">At the top of this screen, you can choose whether the text you want to recognize is printed or handwritten.</span><span class="sxs-lookup"><span data-stu-id="0009c-162">At the top of this screen, you can choose whether the text you want to recognize is printed or handwritten.</span></span>

> [!TIP]
> <span data-ttu-id="0009c-163">Hold the item from which you're trying to recognize text as level as possible and make sure it is evenly lit with no reflections.</span><span class="sxs-lookup"><span data-stu-id="0009c-163">Hold the item from which you're trying to recognize text as level as possible and make sure it is evenly lit with no reflections.</span></span> <span data-ttu-id="0009c-164">We've found that handwritten OCR sometimes works better for script fonts or other "fancy" text.</span><span class="sxs-lookup"><span data-stu-id="0009c-164">We've found that handwritten OCR sometimes works better for script fonts or other "fancy" text.</span></span>

<span data-ttu-id="0009c-165">Next, click **Take Photo** or **Import Photo** to either take a photo using your device's camera, or choose a photo stored on your device.</span><span class="sxs-lookup"><span data-stu-id="0009c-165">Next, click **Take Photo** or **Import Photo** to either take a photo using your device's camera, or choose a photo stored on your device.</span></span>

<span data-ttu-id="0009c-166">After a photo is taken or chosen, the image is passed to the Computer Vision API.</span><span class="sxs-lookup"><span data-stu-id="0009c-166">After a photo is taken or chosen, the image is passed to the Computer Vision API.</span></span> <span data-ttu-id="0009c-167">The Words Found page (defined in `OcrResultsPage.xaml`) displays any words recognized in the image.</span><span class="sxs-lookup"><span data-stu-id="0009c-167">The Words Found page (defined in `OcrResultsPage.xaml`) displays any words recognized in the image.</span></span>

![Image of the OCR Results Page](./media/computer-vision-web-search-tutorial/ocr-results-page.png)  

> [!NOTE]
> <span data-ttu-id="0009c-169">The image we used for these results is in the source repository as  `SamplePhotos\TestImage.jpg`.</span><span class="sxs-lookup"><span data-stu-id="0009c-169">The image we used for these results is in the source repository as  `SamplePhotos\TestImage.jpg`.</span></span>

<span data-ttu-id="0009c-170">When you click an item on the Words Found page, the Web Results page (`WebResultsPage.xaml`) appears, showing you the top Bing results for that search.</span><span class="sxs-lookup"><span data-stu-id="0009c-170">When you click an item on the Words Found page, the Web Results page (`WebResultsPage.xaml`) appears, showing you the top Bing results for that search.</span></span>

![Image of the Web Results Page](./media/computer-vision-web-search-tutorial/web-results-page.png)  
<span data-ttu-id="0009c-172">Finally, choose an item on the Web Results page to open the link in an embedded WebView.</span><span class="sxs-lookup"><span data-stu-id="0009c-172">Finally, choose an item on the Web Results page to open the link in an embedded WebView.</span></span> <span data-ttu-id="0009c-173">(Or navigate back to choose a different result.)</span><span class="sxs-lookup"><span data-stu-id="0009c-173">(Or navigate back to choose a different result.)</span></span>

![Image of the Web View Page](./media/computer-vision-web-search-tutorial/web-view-page.png)  

<span data-ttu-id="0009c-175">You can interact with the page as you would in any Web browser, or navigate back to the Web Results page.</span><span class="sxs-lookup"><span data-stu-id="0009c-175">You can interact with the page as you would in any Web browser, or navigate back to the Web Results page.</span></span> 

## <a name="review-and-learn"></a><span data-ttu-id="0009c-176">Review and Learn</span><span class="sxs-lookup"><span data-stu-id="0009c-176">Review and Learn</span></span>

<span data-ttu-id="0009c-177">Now that you've taken the Visual Search app for a spin, let's explore exactly how we're using the two Microsoft Cognitive Services APIs.</span><span class="sxs-lookup"><span data-stu-id="0009c-177">Now that you've taken the Visual Search app for a spin, let's explore exactly how we're using the two Microsoft Cognitive Services APIs.</span></span>  <span data-ttu-id="0009c-178">Whether you're using this sample as a starting point for your own application or simply as a how-to for the APIs, it's valuable to walk through the application screen-by-screen to examine exactly how it works.</span><span class="sxs-lookup"><span data-stu-id="0009c-178">Whether you're using this sample as a starting point for your own application or simply as a how-to for the APIs, it's valuable to walk through the application screen-by-screen to examine exactly how it works.</span></span>

### <a name="add-keys-page"></a><span data-ttu-id="0009c-179">Add Keys Page</span><span class="sxs-lookup"><span data-stu-id="0009c-179">Add Keys Page</span></span>
<span data-ttu-id="0009c-180">The Add Keys page UI is defined in `AddKeysPage.xaml`, and its primary logic is defined in `AddKeysPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="0009c-180">The Add Keys page UI is defined in `AddKeysPage.xaml`, and its primary logic is defined in `AddKeysPage.xaml.cs`.</span></span> <span data-ttu-id="0009c-181">Since the keys are validated by making a test request, the time is ripe to establish how to use Cognitive Services endpoints in C#.</span><span class="sxs-lookup"><span data-stu-id="0009c-181">Since the keys are validated by making a test request, the time is ripe to establish how to use Cognitive Services endpoints in C#.</span></span>  

<span data-ttu-id="0009c-182">The basic structure of this interaction is:</span><span class="sxs-lookup"><span data-stu-id="0009c-182">The basic structure of this interaction is:</span></span> 

1. <span data-ttu-id="0009c-183">Instantiate *HttpResponseMessage* and *HttpClient* objects from *System.Net.Http*</span><span class="sxs-lookup"><span data-stu-id="0009c-183">Instantiate *HttpResponseMessage* and *HttpClient* objects from *System.Net.Http*</span></span>
2. <span data-ttu-id="0009c-184">Attach any desired headers (defined in each endpoint's API reference) to the *HttpClient* object</span><span class="sxs-lookup"><span data-stu-id="0009c-184">Attach any desired headers (defined in each endpoint's API reference) to the *HttpClient* object</span></span>
3. <span data-ttu-id="0009c-185">Send a GET or POST request with your data, adding any necessary parameters to your endpoint URI</span><span class="sxs-lookup"><span data-stu-id="0009c-185">Send a GET or POST request with your data, adding any necessary parameters to your endpoint URI</span></span>
4. <span data-ttu-id="0009c-186">Verify that the response was successful</span><span class="sxs-lookup"><span data-stu-id="0009c-186">Verify that the response was successful</span></span>
5. <span data-ttu-id="0009c-187">Pass the response on for further processing</span><span class="sxs-lookup"><span data-stu-id="0009c-187">Pass the response on for further processing</span></span>

<span data-ttu-id="0009c-188">The function that checks the validity of the Bing Search API key is `CheckBingSearchKey()`, shown here.</span><span class="sxs-lookup"><span data-stu-id="0009c-188">The function that checks the validity of the Bing Search API key is `CheckBingSearchKey()`, shown here.</span></span>

```csharp
async Task CheckBingSearchKey(object sender = null, EventArgs e = null)
{
    HttpResponseMessage response;
    HttpClient SearchApiClient = new HttpClient();

    SearchApiClient.DefaultRequestHeaders.Add(AppConstants.OcpApimSubscriptionKey, BingSearchKeyEntry.Text);

    try
    {
        response = await SearchApiClient.GetAsync(AppConstants.BingWebSearchApiUrl + "q=test");

        if (response.StatusCode != System.Net.HttpStatusCode.Unauthorized)
        {
            BingSearchKeyEntry.BackgroundColor = Color.Green;
            AppConstants.BingWebSearchApiKey = BingSearchKeyEntry.Text;
            bingSearchKeyWorks = true;
        }
        else
        {
            BingSearchKeyEntry.BackgroundColor = Color.Red;
            bingSearchKeyWorks = false;
        }
    }
    catch( Exception exception )
    {
        BingSearchKeyEntry.BackgroundColor = Color.Red;
        Console.WriteLine($"ERROR: {exception.Message}");
    }
}
```

<span data-ttu-id="0009c-189">A similar function, `CheckComputerVisionKey()`, is used to validate the Computer Vision key.</span><span class="sxs-lookup"><span data-stu-id="0009c-189">A similar function, `CheckComputerVisionKey()`, is used to validate the Computer Vision key.</span></span>

### <a name="ocr-select-page"></a><span data-ttu-id="0009c-190">OCR Select page</span><span class="sxs-lookup"><span data-stu-id="0009c-190">OCR Select page</span></span>

<span data-ttu-id="0009c-191">The OCR Select page (`OcrSelectPage.xaml`) has two important roles.</span><span class="sxs-lookup"><span data-stu-id="0009c-191">The OCR Select page (`OcrSelectPage.xaml`) has two important roles.</span></span> <span data-ttu-id="0009c-192">First, it determines what kind of OCR is performed on the target photo.</span><span class="sxs-lookup"><span data-stu-id="0009c-192">First, it determines what kind of OCR is performed on the target photo.</span></span> <span data-ttu-id="0009c-193">Second, it lets the user capture or open the image they wish to process.</span><span class="sxs-lookup"><span data-stu-id="0009c-193">Second, it lets the user capture or open the image they wish to process.</span></span>

<span data-ttu-id="0009c-194">The second task is traditionally cumbersome in a cross-platform application, because each platform requires different code.</span><span class="sxs-lookup"><span data-stu-id="0009c-194">The second task is traditionally cumbersome in a cross-platform application, because each platform requires different code.</span></span> <span data-ttu-id="0009c-195">The Xamarin Media Plugin handles it with just a few lines of code.</span><span class="sxs-lookup"><span data-stu-id="0009c-195">The Xamarin Media Plugin handles it with just a few lines of code.</span></span>

<span data-ttu-id="0009c-196">The following function incorporates an example of using the Xamarin Media Plugin for photo capture.</span><span class="sxs-lookup"><span data-stu-id="0009c-196">The following function incorporates an example of using the Xamarin Media Plugin for photo capture.</span></span>  <span data-ttu-id="0009c-197">In it, we:</span><span class="sxs-lookup"><span data-stu-id="0009c-197">In it, we:</span></span>

1. <span data-ttu-id="0009c-198">Ensure that a camera is available on the current device</span><span class="sxs-lookup"><span data-stu-id="0009c-198">Ensure that a camera is available on the current device</span></span>
2. <span data-ttu-id="0009c-199">Instantiate a `StoreCameraMediaOptions` object to specify where to save the captured image</span><span class="sxs-lookup"><span data-stu-id="0009c-199">Instantiate a `StoreCameraMediaOptions` object to specify where to save the captured image</span></span>
3. <span data-ttu-id="0009c-200">Capture an image and obtain a `MediaFile` object containing the image data</span><span class="sxs-lookup"><span data-stu-id="0009c-200">Capture an image and obtain a `MediaFile` object containing the image data</span></span>
4. <span data-ttu-id="0009c-201">Unpack the `MediaFile` into a byte array</span><span class="sxs-lookup"><span data-stu-id="0009c-201">Unpack the `MediaFile` into a byte array</span></span>
5. <span data-ttu-id="0009c-202">Return the byte array for further processing</span><span class="sxs-lookup"><span data-stu-id="0009c-202">Return the byte array for further processing</span></span>

<span data-ttu-id="0009c-203">Here's `TakePhoto()`, the function that uses the Xamarin Media Plugin for photo capture.</span><span class="sxs-lookup"><span data-stu-id="0009c-203">Here's `TakePhoto()`, the function that uses the Xamarin Media Plugin for photo capture.</span></span>  

```csharp
async Task<byte[]> TakePhoto()
{
    MediaFile photoMediaFile = null;
    byte[] photoByteArray = null;

    if (CrossMedia.Current.IsCameraAvailable)
    {
        var mediaOptions = new StoreCameraMediaOptions
        {
            PhotoSize = PhotoSize.Medium,
            AllowCropping = true,
            SaveToAlbum = true,
            Name = $"{DateTime.UtcNow}.jpg"
        };
        photoMediaFile = await CrossMedia.Current.TakePhotoAsync(mediaOptions);
        photoByteArray = MediaFileToByteArray(photoMediaFile);
    }
    else
    {
        await DisplayAlert("Error", "No camera found", "OK");
        Console.WriteLine($"ERROR: No camera found");
    }
    return photoByteArray;
}
```
<span data-ttu-id="0009c-204">The photo import utility works in a similar way.</span><span class="sxs-lookup"><span data-stu-id="0009c-204">The photo import utility works in a similar way.</span></span> <span data-ttu-id="0009c-205">Both pieces of functionality can be found in `OcrSelectPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="0009c-205">Both pieces of functionality can be found in `OcrSelectPage.xaml.cs`.</span></span> 
 
> [!NOTE]
> <span data-ttu-id="0009c-206">The Handwritten OCR endpoint can only handle photos that are smaller than 4 MB.</span><span class="sxs-lookup"><span data-stu-id="0009c-206">The Handwritten OCR endpoint can only handle photos that are smaller than 4 MB.</span></span> <span data-ttu-id="0009c-207">To avoid file size issues, we reduce the photo to 50% of its original size by setting the option `PhotoSize = PhotoSize.Medium` on the `StoreCameraMediaOptions` object.</span><span class="sxs-lookup"><span data-stu-id="0009c-207">To avoid file size issues, we reduce the photo to 50% of its original size by setting the option `PhotoSize = PhotoSize.Medium` on the `StoreCameraMediaOptions` object.</span></span>  <span data-ttu-id="0009c-208">If your device takes exceptionally high-quality photos and you are getting errors, you might try `PhotoSize = PhotoSize.Small` instead.</span><span class="sxs-lookup"><span data-stu-id="0009c-208">If your device takes exceptionally high-quality photos and you are getting errors, you might try `PhotoSize = PhotoSize.Small` instead.</span></span>

<span data-ttu-id="0009c-209">Here's the utility function used to convert a *MediaFile* into a byte array.</span><span class="sxs-lookup"><span data-stu-id="0009c-209">Here's the utility function used to convert a *MediaFile* into a byte array.</span></span>

```csharp
byte[] MediaFileToByteArray(MediaFile photoMediaFile)
{
    using (var memStream = new MemoryStream())
    {
        photoMediaFile.GetStream().CopyTo(memStream);
        return memStream.ToArray();
    }
}
```

### <a name="ocr-results-page"></a><span data-ttu-id="0009c-210">OCR Results page</span><span class="sxs-lookup"><span data-stu-id="0009c-210">OCR Results page</span></span>

<span data-ttu-id="0009c-211">The OCR Results page displays text extracted from the image using the  **Json.NET** [SelectToken method](http://www.newtonsoft.com/json/help/html/SelectToken.htm).</span><span class="sxs-lookup"><span data-stu-id="0009c-211">The OCR Results page displays text extracted from the image using the  **Json.NET** [SelectToken method](http://www.newtonsoft.com/json/help/html/SelectToken.htm).</span></span>  <span data-ttu-id="0009c-212">The two OCR endpoints work a little differently, so it's valuable to discuss both.</span><span class="sxs-lookup"><span data-stu-id="0009c-212">The two OCR endpoints work a little differently, so it's valuable to discuss both.</span></span>  

<span data-ttu-id="0009c-213">Because the Computer Vision API is only hosted in a few server locations, its endpoint must be constructed dynamically at runtime.</span><span class="sxs-lookup"><span data-stu-id="0009c-213">Because the Computer Vision API is only hosted in a few server locations, its endpoint must be constructed dynamically at runtime.</span></span> <span data-ttu-id="0009c-214">The function `SetOcrLocation` (part of the static *AppConstants* class found in `AppConstants.cs`) sets the location of the URI endpoint.</span><span class="sxs-lookup"><span data-stu-id="0009c-214">The function `SetOcrLocation` (part of the static *AppConstants* class found in `AppConstants.cs`) sets the location of the URI endpoint.</span></span> <span data-ttu-id="0009c-215">It corresponds to the user's selection on the Add Keys Page or uses the value set in `App.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="0009c-215">It corresponds to the user's selection on the Add Keys Page or uses the value set in `App.xaml.cs`.</span></span> 

```csharp
public static void SetOcrLocation(string location)
{
    ComputerVisionApiOcrUrl = $"https://{location}.api.cognitive.microsoft.com/vision/v1.0/ocr?language=en&detectOrientation=true";
    ComputerVisionApiHandwritingUrl = $"https://{location}.api.cognitive.microsoft.com/vision/v1.0/recognizeText?handwriting=true";
}
```

<span data-ttu-id="0009c-216">Let's take a closer look at these API requests.</span><span class="sxs-lookup"><span data-stu-id="0009c-216">Let's take a closer look at these API requests.</span></span> <span data-ttu-id="0009c-217">The Computer Vision OCR API is capable of parsing text from an undetermined language, but we tell it to search for English text to improve results.</span><span class="sxs-lookup"><span data-stu-id="0009c-217">The Computer Vision OCR API is capable of parsing text from an undetermined language, but we tell it to search for English text to improve results.</span></span> <span data-ttu-id="0009c-218">We also let the API detect text orientation for us.</span><span class="sxs-lookup"><span data-stu-id="0009c-218">We also let the API detect text orientation for us.</span></span> <span data-ttu-id="0009c-219">Using a fixed orientation might improve our parsing results, but orientation detection can be useful in a mobile application.</span><span class="sxs-lookup"><span data-stu-id="0009c-219">Using a fixed orientation might improve our parsing results, but orientation detection can be useful in a mobile application.</span></span>

<span data-ttu-id="0009c-220">You can learn more about the parameters available with this endpoint from the [Print Optical Character Recognition API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fc).</span><span class="sxs-lookup"><span data-stu-id="0009c-220">You can learn more about the parameters available with this endpoint from the [Print Optical Character Recognition API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fc).</span></span>  

<span data-ttu-id="0009c-221">The Handwritten OCR API is still in preview, and currently only works with English text.</span><span class="sxs-lookup"><span data-stu-id="0009c-221">The Handwritten OCR API is still in preview, and currently only works with English text.</span></span>  <span data-ttu-id="0009c-222">For this reason, its only parameter is currently a flag indicating whether or not to parse handwritten text at all.</span><span class="sxs-lookup"><span data-stu-id="0009c-222">For this reason, its only parameter is currently a flag indicating whether or not to parse handwritten text at all.</span></span> <span data-ttu-id="0009c-223">The handwritten OCR API can parse both machine printed and handwritten text, but `handwriting=false` yields better results on printed text.</span><span class="sxs-lookup"><span data-stu-id="0009c-223">The handwritten OCR API can parse both machine printed and handwritten text, but `handwriting=false` yields better results on printed text.</span></span> 

<span data-ttu-id="0009c-224">Since this application is in English, we could have used only Handwritten OCR for this sample, and set the `handwriting` flag according to what the user tells us to recognize.</span><span class="sxs-lookup"><span data-stu-id="0009c-224">Since this application is in English, we could have used only Handwritten OCR for this sample, and set the `handwriting` flag according to what the user tells us to recognize.</span></span>  <span data-ttu-id="0009c-225">We used both endpoints for illustrative purposes.</span><span class="sxs-lookup"><span data-stu-id="0009c-225">We used both endpoints for illustrative purposes.</span></span>  

<span data-ttu-id="0009c-226">You can learn more about the parameters available with this endpoint from the [Handwritten Optical Character Recognition API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/587f2c6a154055056008f200).</span><span class="sxs-lookup"><span data-stu-id="0009c-226">You can learn more about the parameters available with this endpoint from the [Handwritten Optical Character Recognition API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/587f2c6a154055056008f200).</span></span>

<span data-ttu-id="0009c-227">Now, let's look at the functions that call these APIs.</span><span class="sxs-lookup"><span data-stu-id="0009c-227">Now, let's look at the functions that call these APIs.</span></span>

<span data-ttu-id="0009c-228">`FetchPrintedWordList()` uses the Print OCR endpoint to parse printed text from images.</span><span class="sxs-lookup"><span data-stu-id="0009c-228">`FetchPrintedWordList()` uses the Print OCR endpoint to parse printed text from images.</span></span> <span data-ttu-id="0009c-229">The HTTP request follows a structure similar to the call that used in the Add Keys page to validate the key, but we need to send a photo.</span><span class="sxs-lookup"><span data-stu-id="0009c-229">The HTTP request follows a structure similar to the call that used in the Add Keys page to validate the key, but we need to send a photo.</span></span> <span data-ttu-id="0009c-230">A photo is too large to pass in a query string, so we must use an HTTP POST request instead of a GET request.</span><span class="sxs-lookup"><span data-stu-id="0009c-230">A photo is too large to pass in a query string, so we must use an HTTP POST request instead of a GET request.</span></span> <span data-ttu-id="0009c-231">We need to encode our photo (which exists in memory as a byte array) into a `ByteArrayContent` object and add a header to this object defining the type of data we're sending.</span><span class="sxs-lookup"><span data-stu-id="0009c-231">We need to encode our photo (which exists in memory as a byte array) into a `ByteArrayContent` object and add a header to this object defining the type of data we're sending.</span></span> 

<span data-ttu-id="0009c-232">You can read about the acceptable content types in the [Computer Vision API reference](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/587f2c6a154055056008f200).</span><span class="sxs-lookup"><span data-stu-id="0009c-232">You can read about the acceptable content types in the [Computer Vision API reference](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/587f2c6a154055056008f200).</span></span>  

```csharp
async Task<ObservableCollection<string>> FetchPrintedWordList()
{
    ObservableCollection<string> wordList = new ObservableCollection<string>();
    if (photo != null)
    {
        HttpResponseMessage response = null;
        using (var content = new ByteArrayContent(photo))
        {
            // The media type of the body sent to the API. 
            // "application/octet-stream" defines an image represented 
            // as a byte array
            content.Headers.ContentType = new MediaTypeHeaderValue("application/octet-stream");
            response = await visionApiClient.PostAsync(AppConstants.ComputerVisionApiOcrUrl, content);
        }

        string ResponseString = await response.Content.ReadAsStringAsync();
        JObject json = JObject.Parse(ResponseString);

        // Here, we pull down each "line" of text and then join it to 
        // make a string representing the entirety of each line.  
        // In the Handwritten endpoint, you are able to extract the 
        // "line" without any further processing.  If you would like 
        // to simply get a list of all extracted words,* you can do 
        // this with:
        // json.SelectTokens("$.regions[*].lines[*].words[*].text) 
        IEnumerable<JToken> lines = json.SelectTokens("$.regions[*].lines[*]");
        if (lines != null)
        {
            foreach (JToken line in lines)
            {
                IEnumerable<JToken> words = line.SelectTokens("$.words[*].text");
                if (words != null)
                {
                    wordList.Add(string.Join(" ", words.Select(x => x.ToString())));
                }
            }
        }
    }
    return wordList;
}
```
> [!TIP]
> <span data-ttu-id="0009c-233">Note how we're using the **Json.NET** [SelectToken method](http://www.newtonsoft.com/json/help/html/SelectToken.htm) to extract text from the response object.</span><span class="sxs-lookup"><span data-stu-id="0009c-233">Note how we're using the **Json.NET** [SelectToken method](http://www.newtonsoft.com/json/help/html/SelectToken.htm) to extract text from the response object.</span></span> <span data-ttu-id="0009c-234">`SelectToken` is ideal when we need only a specific part of the JSON response, which we can then pass on to the next function.</span><span class="sxs-lookup"><span data-stu-id="0009c-234">`SelectToken` is ideal when we need only a specific part of the JSON response, which we can then pass on to the next function.</span></span> <span data-ttu-id="0009c-235">In other parts of the code, we deserialize JSON responses into model objects defined in `ModelObjects.cs`.</span><span class="sxs-lookup"><span data-stu-id="0009c-235">In other parts of the code, we deserialize JSON responses into model objects defined in `ModelObjects.cs`.</span></span>

<span data-ttu-id="0009c-236">The primary difference between the Print OCR and Handwritten OCR request is that the Print OCR service returns the recognized text as part of the HTTP response, while the Handwritten OCR service requires an additional request to get the information.</span><span class="sxs-lookup"><span data-stu-id="0009c-236">The primary difference between the Print OCR and Handwritten OCR request is that the Print OCR service returns the recognized text as part of the HTTP response, while the Handwritten OCR service requires an additional request to get the information.</span></span> <span data-ttu-id="0009c-237">The initial Handwritten OCR request returns an HTTP 202 status, which signals only that processing has begun.</span><span class="sxs-lookup"><span data-stu-id="0009c-237">The initial Handwritten OCR request returns an HTTP 202 status, which signals only that processing has begun.</span></span> <span data-ttu-id="0009c-238">This response contains an endpoint that the client must check to obtain the completed response when it is available.</span><span class="sxs-lookup"><span data-stu-id="0009c-238">This response contains an endpoint that the client must check to obtain the completed response when it is available.</span></span> <span data-ttu-id="0009c-239">See `FetchHandwrittenWordList()` to see how it all works.</span><span class="sxs-lookup"><span data-stu-id="0009c-239">See `FetchHandwrittenWordList()` to see how it all works.</span></span>

```csharp
async Task<ObservableCollection<string>> FetchHandwrittenWordList()
{
    ObservableCollection<string> wordList = new ObservableCollection<string>();
    if (photo != null)
    {
        // Make the POST request to the handwriting recognition URL
        HttpResponseMessage response = null;
        using (var content = new ByteArrayContent(photo))
        {
            // The media type of the body sent to the API. 
            // "application/octet-stream" defines an image represented 
            // as a byte array
            content.Headers.ContentType = new MediaTypeHeaderValue("application/octet-stream");
            response = await visionApiClient.PostAsync(AppConstants.ComputerVisionApiHandwritingUrl, content);
        }

        // Fetch results
        IEnumerable<string> operationLocationValues;
        string statusUri = string.Empty;
        if (response.Headers.TryGetValues("Operation-Location", out operationLocationValues))
        {
            statusUri = operationLocationValues.FirstOrDefault();

            // Ping status URL, wait for processing to finish 
            JObject obj = await FetchResultFromStatusUri(statusUri);
            IEnumerable<JToken> strings = obj.SelectTokens("$.recognitionResult.lines[*].text");
            foreach (string s in strings)
            {
                wordList.Add((string)s);
            }
        }
    }
    return wordList;
}
```

<span data-ttu-id="0009c-240">`FetchResultFromStatusUri()` is the second part of the Handwriting OCR process.</span><span class="sxs-lookup"><span data-stu-id="0009c-240">`FetchResultFromStatusUri()` is the second part of the Handwriting OCR process.</span></span> <span data-ttu-id="0009c-241">It pings the URI extracted from the initial response's metadata either until a result is obtained or the function times out.  It's important that this function is called asynchronously on its own thread.</span><span class="sxs-lookup"><span data-stu-id="0009c-241">It pings the URI extracted from the initial response's metadata either until a result is obtained or the function times out.  It's important that this function is called asynchronously on its own thread.</span></span> <span data-ttu-id="0009c-242">Otherwise this method would lock up the user interface until processing was complete.</span><span class="sxs-lookup"><span data-stu-id="0009c-242">Otherwise this method would lock up the user interface until processing was complete.</span></span>

```csharp
// Takes in the url to check for handwritten text parsing results, and pings it per second until processing is finished
// Returns the JObject holding data for a successful parse
async Task<JObject> FetchResultFromStatusUri(string statusUri)
{
    JObject obj = null;
    int timeoutcounter = 0;
    HttpResponseMessage response = await visionApiClient.GetAsync(statusUri);
    string responseString = await response.Content.ReadAsStringAsync();
    obj = JObject.Parse(responseString);
    while ((!((string)obj.SelectToken("status")).Equals("Succeeded")) && (timeoutcounter++ < 60))
    {
        await Task.Delay(1000);
        response = await visionApiClient.GetAsync(statusUri);
        responseString = await response.Content.ReadAsStringAsync();
        obj = JObject.Parse(responseString);
    } 
    return obj;
}
```

### <a name="web-results-page"></a><span data-ttu-id="0009c-243">Web Results page</span><span class="sxs-lookup"><span data-stu-id="0009c-243">Web Results page</span></span>
<span data-ttu-id="0009c-244">After the user selects a search term displayed on the OCR Results page, we move along to the Web Results page.</span><span class="sxs-lookup"><span data-stu-id="0009c-244">After the user selects a search term displayed on the OCR Results page, we move along to the Web Results page.</span></span>  <span data-ttu-id="0009c-245">Here we construct a [Bing Web Search API](https://azure.microsoft.com/services/cognitive-services/bing-web-search-api/) request, send it to the service's endpoint, and deserialize the JSON response using the **Json.NET** [DeserializeObject](http://www.newtonsoft.com/json/help/html/DeserializeObject.htm) method.</span><span class="sxs-lookup"><span data-stu-id="0009c-245">Here we construct a [Bing Web Search API](https://azure.microsoft.com/services/cognitive-services/bing-web-search-api/) request, send it to the service's endpoint, and deserialize the JSON response using the **Json.NET** [DeserializeObject](http://www.newtonsoft.com/json/help/html/DeserializeObject.htm) method.</span></span>  

```csharp
async Task<WebResultsList> GetQueryResults()
{
    // URL-encode the query term
    var queryString = System.Net.WebUtility.UrlEncode(queryTerm);

    // Here we encode the URL that will be used for the GET request to 
    // find query results.  Its arguments are as follows:
    // 
    // - [count=20] This sets the number of webpage objects returned at 
    //   "$.webpages" in the JSON response.  Currently, the API asks for 
    //   20 webpages in the response
    //
    // - [mkt=en-US] This sets the market where the results come from.
    //   Currently, the API looks for english results based in the 
    //   United States.
    //
    // - [q=queryString] This sets the string queried using the Search 
    //   API.   
    //
    // - [responseFilter=Webpages] This filters the response to only 
    //   include Webpage results.  This tag can take a comma seperated 
    //   list of response types that you are looking for.  If left 
    //   blank, all responses (webPages, News, Videos, etc) are 
    //   returned.
    //
    // - [setLang=en] This sets the languge for user interface strings. 
    //   To learn more about UI strings, check the Web Search API 
    //   reference.
    //
    // - [API Reference] https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference
    string uri = AppConstants.BingWebSearchApiUrl + $"count=20&mkt=en-US&q={queryString}&responseFilter=Webpages&setLang=en";

    // Make the HTTP Request
    WebResultsList webResults = null;
    HttpResponseMessage httpResponseMessage = await searchApiClient.GetAsync(uri);
    var responseContentString = await httpResponseMessage.Content.ReadAsStringAsync();
    JObject json = JObject.Parse(responseContentString);
    JToken resultBlock = json.SelectToken("$.webPages");
    if (resultBlock != null)
    {
        webResults = JsonConvert.DeserializeObject<WebResultsList>(resultBlock.ToString());
    }
    return webResults;
}
```

<span data-ttu-id="0009c-246">The Bing Web Search API works best when you provide as much information as you can about what the user might want.</span><span class="sxs-lookup"><span data-stu-id="0009c-246">The Bing Web Search API works best when you provide as much information as you can about what the user might want.</span></span> <span data-ttu-id="0009c-247">In particular, you should almost always use the `mkt` and `setLang` paramaters (here set for US English) to identify your user's location and preferred language.</span><span class="sxs-lookup"><span data-stu-id="0009c-247">In particular, you should almost always use the `mkt` and `setLang` paramaters (here set for US English) to identify your user's location and preferred language.</span></span>

> [!NOTE]
> <span data-ttu-id="0009c-248">We kept our Bing Web Search query simple in order to make sure the source code was easy to understand.</span><span class="sxs-lookup"><span data-stu-id="0009c-248">We kept our Bing Web Search query simple in order to make sure the source code was easy to understand.</span></span>  <span data-ttu-id="0009c-249">In a real application, you should add the following headers to your HTTP request for improved results.</span><span class="sxs-lookup"><span data-stu-id="0009c-249">In a real application, you should add the following headers to your HTTP request for improved results.</span></span> 
> * <span data-ttu-id="0009c-250">User-Agent</span><span class="sxs-lookup"><span data-stu-id="0009c-250">User-Agent</span></span>  
> * <span data-ttu-id="0009c-251">X-MSEdge-ClientID</span><span class="sxs-lookup"><span data-stu-id="0009c-251">X-MSEdge-ClientID</span></span>  
> * <span data-ttu-id="0009c-252">X-Search-ClientIP</span><span class="sxs-lookup"><span data-stu-id="0009c-252">X-Search-ClientIP</span></span>  
> * <span data-ttu-id="0009c-253">X-Search-Location</span><span class="sxs-lookup"><span data-stu-id="0009c-253">X-Search-Location</span></span>  
>
> <span data-ttu-id="0009c-254">You can learn more about these header values in the [Bing Web Search API Reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#headers)</span><span class="sxs-lookup"><span data-stu-id="0009c-254">You can learn more about these header values in the [Bing Web Search API Reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#headers)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0009c-255">Next Steps</span><span class="sxs-lookup"><span data-stu-id="0009c-255">Next Steps</span></span>
<span data-ttu-id="0009c-256">Microsoft Cognitive Services provide many additional services that you could easily integrate into this application.</span><span class="sxs-lookup"><span data-stu-id="0009c-256">Microsoft Cognitive Services provide many additional services that you could easily integrate into this application.</span></span>  <span data-ttu-id="0009c-257">For example, you could:</span><span class="sxs-lookup"><span data-stu-id="0009c-257">For example, you could:</span></span>

* <span data-ttu-id="0009c-258">Add [Bing Entity Search](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) to augment your web search results</span><span class="sxs-lookup"><span data-stu-id="0009c-258">Add [Bing Entity Search](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) to augment your web search results</span></span>
* <span data-ttu-id="0009c-259">Swap in [Bing Custom Search](https://azure.microsoft.com/services/cognitive-services/bing-custom-search/) in place of Bing Web Search</span><span class="sxs-lookup"><span data-stu-id="0009c-259">Swap in [Bing Custom Search](https://azure.microsoft.com/services/cognitive-services/bing-custom-search/) in place of Bing Web Search</span></span>
* <span data-ttu-id="0009c-260">Use the [Bing Image Search](https://azure.microsoft.com/services/cognitive-services/bing-image-search-api/) image insights capability to learn more about your captured image and find similar images on the web</span><span class="sxs-lookup"><span data-stu-id="0009c-260">Use the [Bing Image Search](https://azure.microsoft.com/services/cognitive-services/bing-image-search-api/) image insights capability to learn more about your captured image and find similar images on the web</span></span>
* <span data-ttu-id="0009c-261">Employ [Bing Spell Check](https://azure.microsoft.com/services/cognitive-services/spell-check/) to further improve the quality of your parsed text</span><span class="sxs-lookup"><span data-stu-id="0009c-261">Employ [Bing Spell Check](https://azure.microsoft.com/services/cognitive-services/spell-check/) to further improve the quality of your parsed text</span></span>
* <span data-ttu-id="0009c-262">Integrate the [Microsoft Translator](https://azure.microsoft.com/services/cognitive-services/translator-text-api/) to see your extracted text in different languages</span><span class="sxs-lookup"><span data-stu-id="0009c-262">Integrate the [Microsoft Translator](https://azure.microsoft.com/services/cognitive-services/translator-text-api/) to see your extracted text in different languages</span></span>
* <span data-ttu-id="0009c-263">Mix and match the other services from the [Cognitive Services Portal](https://azure.microsoft.com/services/cognitive-services/); the sky's the limit!</span><span class="sxs-lookup"><span data-stu-id="0009c-263">Mix and match the other services from the [Cognitive Services Portal](https://azure.microsoft.com/services/cognitive-services/); the sky's the limit!</span></span>
