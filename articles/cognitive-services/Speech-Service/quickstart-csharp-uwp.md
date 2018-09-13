---
title: 'Quickstart: Recognize speech in C# in a UWP app using the Cognitive Services Speech SDK'
titleSuffix: Microsoft Cognitive Services
description: Learn how to recognize speech in a UWP app using the Cognitive Services Speech SDK
services: cognitive-services
author: wolfma61
ms.service: cognitive-services
ms.component: speech-service
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: wolfma
ms.openlocfilehash: 0e733c199eab13fb62cc06160ce014de3f434f36
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864660"
---
# <a name="quickstart-recognize-speech-in-a-uwp-app-using-the-speech-sdk"></a><span data-ttu-id="89f9c-103">Quickstart: Recognize speech in a UWP app using the Speech SDK</span><span class="sxs-lookup"><span data-stu-id="89f9c-103">Quickstart: Recognize speech in a UWP app using the Speech SDK</span></span>

[!INCLUDE [Selector](../../../includes/cognitive-services-speech-service-quickstart-selector.md)]

<span data-ttu-id="89f9c-104">In this article, you create a C# Universal Windows Platform (UWP) application using the Cognitive Services [Speech SDK](speech-sdk.md) to transcribe speech to text in real time from your device's microphone.</span><span class="sxs-lookup"><span data-stu-id="89f9c-104">In this article, you create a C# Universal Windows Platform (UWP) application using the Cognitive Services [Speech SDK](speech-sdk.md) to transcribe speech to text in real time from your device's microphone.</span></span> <span data-ttu-id="89f9c-105">The application is built with the [Speech SDK NuGet Package](https://aka.ms/csspeech/nuget) and Microsoft Visual Studio 2017 (any edition).</span><span class="sxs-lookup"><span data-stu-id="89f9c-105">The application is built with the [Speech SDK NuGet Package](https://aka.ms/csspeech/nuget) and Microsoft Visual Studio 2017 (any edition).</span></span>

> [!NOTE]
> <span data-ttu-id="89f9c-106">The Universal Windows Platform lets you develop apps that run on any device that supports Windows 10, including PCs, Xbox, Surface Hub, and other devices.</span><span class="sxs-lookup"><span data-stu-id="89f9c-106">The Universal Windows Platform lets you develop apps that run on any device that supports Windows 10, including PCs, Xbox, Surface Hub, and other devices.</span></span> <span data-ttu-id="89f9c-107">Apps using the Speech SDK do not yet pass the Windows App Certification Kit (WACK).</span><span class="sxs-lookup"><span data-stu-id="89f9c-107">Apps using the Speech SDK do not yet pass the Windows App Certification Kit (WACK).</span></span> <span data-ttu-id="89f9c-108">It is possible to sideload your app, but it may not currently be submitted to the Windows Store.</span><span class="sxs-lookup"><span data-stu-id="89f9c-108">It is possible to sideload your app, but it may not currently be submitted to the Windows Store.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89f9c-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="89f9c-109">Prerequisites</span></span>

<span data-ttu-id="89f9c-110">You need a Speech service subscription key to complete this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="89f9c-110">You need a Speech service subscription key to complete this Quickstart.</span></span> <span data-ttu-id="89f9c-111">You can get one for free.</span><span class="sxs-lookup"><span data-stu-id="89f9c-111">You can get one for free.</span></span> <span data-ttu-id="89f9c-112">See [Try the speech service for free](get-started.md) for details.</span><span class="sxs-lookup"><span data-stu-id="89f9c-112">See [Try the speech service for free](get-started.md) for details.</span></span>

## <a name="create-visual-studio-project"></a><span data-ttu-id="89f9c-113">Create Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="89f9c-113">Create Visual Studio project</span></span>

1. <span data-ttu-id="89f9c-114">Start Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="89f9c-114">Start Visual Studio 2017.</span></span>

1. <span data-ttu-id="89f9c-115">Make sure the **Universal Windows Platform development** workload is available.</span><span class="sxs-lookup"><span data-stu-id="89f9c-115">Make sure the **Universal Windows Platform development** workload is available.</span></span> <span data-ttu-id="89f9c-116">Choose **Tools** \> **Get Tools and Features** from the Visual Studio menu bar to open the Visual Studio installer.</span><span class="sxs-lookup"><span data-stu-id="89f9c-116">Choose **Tools** \> **Get Tools and Features** from the Visual Studio menu bar to open the Visual Studio installer.</span></span> <span data-ttu-id="89f9c-117">If this workload is already enabled, close the dialog.</span><span class="sxs-lookup"><span data-stu-id="89f9c-117">If this workload is already enabled, close the dialog.</span></span> 

    ![Enable Universal Windows Platform development](media/sdk/vs-enable-uwp-workload.png)

    <span data-ttu-id="89f9c-119">Otherwise, mark the checkbox next to **.NET cross-platform development,** then click the **Modify** button at the lower right corner of the dialog.</span><span class="sxs-lookup"><span data-stu-id="89f9c-119">Otherwise, mark the checkbox next to **.NET cross-platform development,** then click the **Modify** button at the lower right corner of the dialog.</span></span> <span data-ttu-id="89f9c-120">Installation of the new feature takes a moment.</span><span class="sxs-lookup"><span data-stu-id="89f9c-120">Installation of the new feature takes a moment.</span></span>

1. <span data-ttu-id="89f9c-121">Create a blank Visual C# Universal Windows app.</span><span class="sxs-lookup"><span data-stu-id="89f9c-121">Create a blank Visual C# Universal Windows app.</span></span> <span data-ttu-id="89f9c-122">First, choose **File** \> **New** \> **Project** from the menu.</span><span class="sxs-lookup"><span data-stu-id="89f9c-122">First, choose **File** \> **New** \> **Project** from the menu.</span></span> <span data-ttu-id="89f9c-123">In the **New Project** dialog, expand **Installed** \> **Visual C#** \> **Windows Universal** in the left pane, then select **Blank App (Universal Windows)**.</span><span class="sxs-lookup"><span data-stu-id="89f9c-123">In the **New Project** dialog, expand **Installed** \> **Visual C#** \> **Windows Universal** in the left pane, then select **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="89f9c-124">For the project name, enter *helloworld*.</span><span class="sxs-lookup"><span data-stu-id="89f9c-124">For the project name, enter *helloworld*.</span></span>

    ![](media/sdk/qs-csharp-uwp-01-new-blank-app.png)

1. <span data-ttu-id="89f9c-125">The Speed SDK requires that your application be built for the Windows 10 Fall Creators Update or later.</span><span class="sxs-lookup"><span data-stu-id="89f9c-125">The Speed SDK requires that your application be built for the Windows 10 Fall Creators Update or later.</span></span> <span data-ttu-id="89f9c-126">In the **New Universal Windows Platform Project** window that pops up, choose **Windows 10 Fall Creators Update (10.0; Build 16299)** as **Minimum version**, and this or any later version as **Target version**, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="89f9c-126">In the **New Universal Windows Platform Project** window that pops up, choose **Windows 10 Fall Creators Update (10.0; Build 16299)** as **Minimum version**, and this or any later version as **Target version**, then click **OK**.</span></span>

    ![](media/sdk/qs-csharp-uwp-02-new-uwp-project.png)

1. <span data-ttu-id="89f9c-127">If you're running 64-bit Windows, you may switch your build platform to `x64` using the drop-down menu in the Visual Studio toolbar.</span><span class="sxs-lookup"><span data-stu-id="89f9c-127">If you're running 64-bit Windows, you may switch your build platform to `x64` using the drop-down menu in the Visual Studio toolbar.</span></span> <span data-ttu-id="89f9c-128">(64-bit Windows can run 32-bit applications, so you may leave it set to `x86` if you prefer.)</span><span class="sxs-lookup"><span data-stu-id="89f9c-128">(64-bit Windows can run 32-bit applications, so you may leave it set to `x86` if you prefer.)</span></span>

   ![Switch the build platform to x64](media/sdk/qs-csharp-uwp-03-switch-to-x64.png)

   > [!NOTE]
   > <span data-ttu-id="89f9c-130">The Speech SDK supports Intel-compatible processors only.</span><span class="sxs-lookup"><span data-stu-id="89f9c-130">The Speech SDK supports Intel-compatible processors only.</span></span> <span data-ttu-id="89f9c-131">ARM is currently not supported.</span><span class="sxs-lookup"><span data-stu-id="89f9c-131">ARM is currently not supported.</span></span>

1. <span data-ttu-id="89f9c-132">Install and reference the [Speech SDK NuGet package](https://aka.ms/csspeech/nuget).</span><span class="sxs-lookup"><span data-stu-id="89f9c-132">Install and reference the [Speech SDK NuGet package](https://aka.ms/csspeech/nuget).</span></span> <span data-ttu-id="89f9c-133">In the Solution Explorer, right-click the solution and select **Manage NuGet Packages for Solution**.</span><span class="sxs-lookup"><span data-stu-id="89f9c-133">In the Solution Explorer, right-click the solution and select **Manage NuGet Packages for Solution**.</span></span>

    ![Right-click Manage NuGet Packages for Solution](media/sdk/qs-csharp-uwp-04-manage-nuget-packages.png)

1. <span data-ttu-id="89f9c-135">In the upper-right corner, in the **Package Source** field, select **Nuget.org**. Search for the `Microsoft.CognitiveServices.Speech` package and install it into the **helloworld** project.</span><span class="sxs-lookup"><span data-stu-id="89f9c-135">In the upper-right corner, in the **Package Source** field, select **Nuget.org**. Search for the `Microsoft.CognitiveServices.Speech` package and install it into the **helloworld** project.</span></span>

    <span data-ttu-id="89f9c-136">![Install Microsoft.CognitiveServices.Speech NuGet Package](media/sdk/qs-csharp-uwp-05-nuget-install-0.5.0.png "Install Nuget package")</span><span class="sxs-lookup"><span data-stu-id="89f9c-136">![Install Microsoft.CognitiveServices.Speech NuGet Package](media/sdk/qs-csharp-uwp-05-nuget-install-0.5.0.png "Install Nuget package")</span></span>

1. <span data-ttu-id="89f9c-137">Accept the displayed license to begin installation of the NuGet package.</span><span class="sxs-lookup"><span data-stu-id="89f9c-137">Accept the displayed license to begin installation of the NuGet package.</span></span>

    <span data-ttu-id="89f9c-138">![Accept the license](media/sdk/qs-csharp-uwp-06-nuget-license.png "Accept the license")</span><span class="sxs-lookup"><span data-stu-id="89f9c-138">![Accept the license](media/sdk/qs-csharp-uwp-06-nuget-license.png "Accept the license")</span></span>

    <span data-ttu-id="89f9c-139">After the package is installed, a confirmation appears in the Package Manager console.</span><span class="sxs-lookup"><span data-stu-id="89f9c-139">After the package is installed, a confirmation appears in the Package Manager console.</span></span>

1. <span data-ttu-id="89f9c-140">Since the application uses the microphone for speech input, add the **Microphone** capability to the project.</span><span class="sxs-lookup"><span data-stu-id="89f9c-140">Since the application uses the microphone for speech input, add the **Microphone** capability to the project.</span></span>

   <span data-ttu-id="89f9c-141">In Solution Explorer, double-click **Package.appxmanifest** to edit your application manifest.</span><span class="sxs-lookup"><span data-stu-id="89f9c-141">In Solution Explorer, double-click **Package.appxmanifest** to edit your application manifest.</span></span>
   <span data-ttu-id="89f9c-142">Then switch to the **Capabilities** tab, mark the checkbox for the **Microphone** capability, and save your changes.</span><span class="sxs-lookup"><span data-stu-id="89f9c-142">Then switch to the **Capabilities** tab, mark the checkbox for the **Microphone** capability, and save your changes.</span></span>

   ![](media/sdk/qs-csharp-uwp-07-capabilities.png)


## <a name="add-sample-code"></a><span data-ttu-id="89f9c-143">Add sample code</span><span class="sxs-lookup"><span data-stu-id="89f9c-143">Add sample code</span></span>

1. <span data-ttu-id="89f9c-144">The application's user interface is defined using XAML.</span><span class="sxs-lookup"><span data-stu-id="89f9c-144">The application's user interface is defined using XAML.</span></span> <span data-ttu-id="89f9c-145">Open `MainPage.xaml` in the Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="89f9c-145">Open `MainPage.xaml` in the Solution Explorer.</span></span> <span data-ttu-id="89f9c-146">In the designer's XAML view, insert the following XAML snippet into the Grid tag (between `<Grid>` and `</Grid>`).</span><span class="sxs-lookup"><span data-stu-id="89f9c-146">In the designer's XAML view, insert the following XAML snippet into the Grid tag (between `<Grid>` and `</Grid>`).</span></span>

   [!code-xml[UI elements](~/samples-cognitive-services-speech-sdk/quickstart/csharp-uwp/helloworld/MainPage.xaml#StackPanel)]

1. <span data-ttu-id="89f9c-147">Open the code-behind source file `MainPage.xaml.cs` (find it grouped under `MainPage.xaml`).</span><span class="sxs-lookup"><span data-stu-id="89f9c-147">Open the code-behind source file `MainPage.xaml.cs` (find it grouped under `MainPage.xaml`).</span></span> <span data-ttu-id="89f9c-148">Replace all the code in it with the following.</span><span class="sxs-lookup"><span data-stu-id="89f9c-148">Replace all the code in it with the following.</span></span>

   [!code-csharp[Quickstart Code](~/samples-cognitive-services-speech-sdk/quickstart/csharp-uwp/helloworld/MainPage.xaml.cs#code)]

1. <span data-ttu-id="89f9c-149">In the `SpeechRecognitionFromMicrophone_ButtonClicked` handler in this file, replace the string `YourSubscriptionKey` with your subscription key.</span><span class="sxs-lookup"><span data-stu-id="89f9c-149">In the `SpeechRecognitionFromMicrophone_ButtonClicked` handler in this file, replace the string `YourSubscriptionKey` with your subscription key.</span></span>

1. <span data-ttu-id="89f9c-150">In the `SpeechRecognitionFromMicrophone_ButtonClicked` handler, replace the string `YourServiceRegion` with the [region](regions.md) associated with your subscription (for example, `westus` for the free trial subscription).</span><span class="sxs-lookup"><span data-stu-id="89f9c-150">In the `SpeechRecognitionFromMicrophone_ButtonClicked` handler, replace the string `YourServiceRegion` with the [region](regions.md) associated with your subscription (for example, `westus` for the free trial subscription).</span></span>

1. <span data-ttu-id="89f9c-151">Save all changes to the project.</span><span class="sxs-lookup"><span data-stu-id="89f9c-151">Save all changes to the project.</span></span>

## <a name="build-and-run-the-app"></a><span data-ttu-id="89f9c-152">Build and run the app</span><span class="sxs-lookup"><span data-stu-id="89f9c-152">Build and run the app</span></span>

1. <span data-ttu-id="89f9c-153">Build the application.</span><span class="sxs-lookup"><span data-stu-id="89f9c-153">Build the application.</span></span> <span data-ttu-id="89f9c-154">From the menu bar, select **Build** > **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="89f9c-154">From the menu bar, select **Build** > **Build Solution**.</span></span> <span data-ttu-id="89f9c-155">The code should compile without errors now.</span><span class="sxs-lookup"><span data-stu-id="89f9c-155">The code should compile without errors now.</span></span>

    <span data-ttu-id="89f9c-156">![Successful build](media/sdk/qs-csharp-uwp-08-build.png "Successful build")</span><span class="sxs-lookup"><span data-stu-id="89f9c-156">![Successful build](media/sdk/qs-csharp-uwp-08-build.png "Successful build")</span></span>

1. <span data-ttu-id="89f9c-157">Start the application.</span><span class="sxs-lookup"><span data-stu-id="89f9c-157">Start the application.</span></span> <span data-ttu-id="89f9c-158">From the menu bar, select **Debug** > **Start Debugging**, or press **F5**.</span><span class="sxs-lookup"><span data-stu-id="89f9c-158">From the menu bar, select **Debug** > **Start Debugging**, or press **F5**.</span></span>

    <span data-ttu-id="89f9c-159">![Start the app into debugging](media/sdk/qs-csharp-uwp-09-start-debugging.png "Start the app into debugging")</span><span class="sxs-lookup"><span data-stu-id="89f9c-159">![Start the app into debugging](media/sdk/qs-csharp-uwp-09-start-debugging.png "Start the app into debugging")</span></span>

1. <span data-ttu-id="89f9c-160">A GUI window pops up.</span><span class="sxs-lookup"><span data-stu-id="89f9c-160">A GUI window pops up.</span></span> <span data-ttu-id="89f9c-161">First click the **Enable Microphone** button and acknowledge the permission request that pops up.</span><span class="sxs-lookup"><span data-stu-id="89f9c-161">First click the **Enable Microphone** button and acknowledge the permission request that pops up.</span></span>

    <span data-ttu-id="89f9c-162">![Start the app into debugging](media/sdk/qs-csharp-uwp-10-access-prompt.png "Start the app into debugging")</span><span class="sxs-lookup"><span data-stu-id="89f9c-162">![Start the app into debugging](media/sdk/qs-csharp-uwp-10-access-prompt.png "Start the app into debugging")</span></span>

1. <span data-ttu-id="89f9c-163">Click the **Speech recognition with microphone input** and speak an English phrase or sentence into your device's microphone.</span><span class="sxs-lookup"><span data-stu-id="89f9c-163">Click the **Speech recognition with microphone input** and speak an English phrase or sentence into your device's microphone.</span></span> <span data-ttu-id="89f9c-164">Your speech is transmitted to the Speech service and transcribed to text, which appears in the window.</span><span class="sxs-lookup"><span data-stu-id="89f9c-164">Your speech is transmitted to the Speech service and transcribed to text, which appears in the window.</span></span>

    ![](media/sdk/qs-csharp-uwp-11-ui-result.png)

[!INCLUDE [Download this sample](../../../includes/cognitive-services-speech-service-speech-sdk-sample-download-h2.md)]
<span data-ttu-id="89f9c-165">Look for this sample in the `quickstart/csharp-uwp` folder.</span><span class="sxs-lookup"><span data-stu-id="89f9c-165">Look for this sample in the `quickstart/csharp-uwp` folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89f9c-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="89f9c-166">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="89f9c-167">Recognize intents from speech by using the Speech SDK for C#</span><span class="sxs-lookup"><span data-stu-id="89f9c-167">Recognize intents from speech by using the Speech SDK for C#</span></span>](how-to-recognize-intents-from-speech-csharp.md)

## <a name="see-also"></a><span data-ttu-id="89f9c-168">See also</span><span class="sxs-lookup"><span data-stu-id="89f9c-168">See also</span></span>

- [<span data-ttu-id="89f9c-169">Translate speech</span><span class="sxs-lookup"><span data-stu-id="89f9c-169">Translate speech</span></span>](how-to-translate-speech-csharp.md)
- [<span data-ttu-id="89f9c-170">Customize acoustic models</span><span class="sxs-lookup"><span data-stu-id="89f9c-170">Customize acoustic models</span></span>](how-to-customize-acoustic-models.md)
- [<span data-ttu-id="89f9c-171">Customize language models</span><span class="sxs-lookup"><span data-stu-id="89f9c-171">Customize language models</span></span>](how-to-customize-language-model.md)
