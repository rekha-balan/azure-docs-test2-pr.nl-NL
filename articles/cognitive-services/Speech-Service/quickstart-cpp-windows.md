---
title: 'Quickstart: Recognize speech in C++ on Windows using the Cognitive Services Speech SDK'
titleSuffix: Microsoft Cognitive Services
description: Learn how to recognize speech in C++ on Windows Desktop using the Cognitive Services Speech SDK
services: cognitive-services
author: wolfma61
ms.service: cognitive-services
ms.technology: Speech
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: wolfma
ms.openlocfilehash: 921e2881be95050c9424c284fd9adfa16af1de78
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866025"
---
# <a name="quickstart-recognize-speech-in-c-on-windows-using-the-speech-sdk"></a><span data-ttu-id="bec56-103">Quickstart: Recognize speech in C++ on Windows using the Speech SDK</span><span class="sxs-lookup"><span data-stu-id="bec56-103">Quickstart: Recognize speech in C++ on Windows using the Speech SDK</span></span>

[!INCLUDE [Selector](../../../includes/cognitive-services-speech-service-quickstart-selector.md)]

<span data-ttu-id="bec56-104">In this article, you create a C++ console application for Windows using the Cognitive Services [Speech SDK](speech-sdk.md) to transcribe speech to text in real time from your PC's microphone.</span><span class="sxs-lookup"><span data-stu-id="bec56-104">In this article, you create a C++ console application for Windows using the Cognitive Services [Speech SDK](speech-sdk.md) to transcribe speech to text in real time from your PC's microphone.</span></span> <span data-ttu-id="bec56-105">The application is built with the [Speech SDK NuGet package](https://aka.ms/csspeech/nuget) and Microsoft Visual Studio 2017 (any edition).</span><span class="sxs-lookup"><span data-stu-id="bec56-105">The application is built with the [Speech SDK NuGet package](https://aka.ms/csspeech/nuget) and Microsoft Visual Studio 2017 (any edition).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bec56-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bec56-106">Prerequisites</span></span>

<span data-ttu-id="bec56-107">You need a Speech service subscription key to complete this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="bec56-107">You need a Speech service subscription key to complete this Quickstart.</span></span> <span data-ttu-id="bec56-108">You can get one for free.</span><span class="sxs-lookup"><span data-stu-id="bec56-108">You can get one for free.</span></span> <span data-ttu-id="bec56-109">See [Try the speech service for free](get-started.md) for details.</span><span class="sxs-lookup"><span data-stu-id="bec56-109">See [Try the speech service for free](get-started.md) for details.</span></span>

## <a name="create-visual-studio-project"></a><span data-ttu-id="bec56-110">Create Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="bec56-110">Create Visual Studio project</span></span>

1. <span data-ttu-id="bec56-111">Start Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="bec56-111">Start Visual Studio 2017.</span></span>

1. <span data-ttu-id="bec56-112">Make sure the **Desktop development with C++** workload is available.</span><span class="sxs-lookup"><span data-stu-id="bec56-112">Make sure the **Desktop development with C++** workload is available.</span></span> <span data-ttu-id="bec56-113">Choose **Tools** \> **Get Tools and Features** from the Visual Studio menu bar to open the Visual Studio installer.</span><span class="sxs-lookup"><span data-stu-id="bec56-113">Choose **Tools** \> **Get Tools and Features** from the Visual Studio menu bar to open the Visual Studio installer.</span></span> <span data-ttu-id="bec56-114">If this workload is already enabled, skip to the next step.</span><span class="sxs-lookup"><span data-stu-id="bec56-114">If this workload is already enabled, skip to the next step.</span></span> 

    ![Enable Desktop development with C++ workload](media/sdk/vs-enable-cpp-workload.png)

    <span data-ttu-id="bec56-116">Otherwise, mark the checkbox next to **Desktop development with C++,**</span><span class="sxs-lookup"><span data-stu-id="bec56-116">Otherwise, mark the checkbox next to **Desktop development with C++,**</span></span> 

1. <span data-ttu-id="bec56-117">Make sure the **NuGet package manager** component is available.</span><span class="sxs-lookup"><span data-stu-id="bec56-117">Make sure the **NuGet package manager** component is available.</span></span> <span data-ttu-id="bec56-118">Switch to the Individual Components tab of the Visual Studio installer dialog and mark the **NuGet package manager** checkbox if it is not already enabled.</span><span class="sxs-lookup"><span data-stu-id="bec56-118">Switch to the Individual Components tab of the Visual Studio installer dialog and mark the **NuGet package manager** checkbox if it is not already enabled.</span></span>

      ![<span data-ttu-id="bec56-119">Enable NuGet package manager in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bec56-119">Enable NuGet package manager in Visual Studio</span></span> ](media/sdk/vs-enable-nuget-package-manager.png)

1. <span data-ttu-id="bec56-120">If you needed to enable either the C++ workload or NuGet, click the **Modify** button at the lower right corner of the dialog.</span><span class="sxs-lookup"><span data-stu-id="bec56-120">If you needed to enable either the C++ workload or NuGet, click the **Modify** button at the lower right corner of the dialog.</span></span> <span data-ttu-id="bec56-121">Installation of the new features takes a moment.</span><span class="sxs-lookup"><span data-stu-id="bec56-121">Installation of the new features takes a moment.</span></span> <span data-ttu-id="bec56-122">If both features were already enabled, close the dialog instead.</span><span class="sxs-lookup"><span data-stu-id="bec56-122">If both features were already enabled, close the dialog instead.</span></span>

1. <span data-ttu-id="bec56-123">Create a new Visual C++ Windows Desktop Windows console Application.</span><span class="sxs-lookup"><span data-stu-id="bec56-123">Create a new Visual C++ Windows Desktop Windows console Application.</span></span> <span data-ttu-id="bec56-124">First, choose **File** \> **New** \> **Project** from the menu.</span><span class="sxs-lookup"><span data-stu-id="bec56-124">First, choose **File** \> **New** \> **Project** from the menu.</span></span> <span data-ttu-id="bec56-125">In the **New Project** dialog, expand **Installed** \> **Visual C++** \> **Windows Desktop** in the left pane, then select **Windows Console Application**.</span><span class="sxs-lookup"><span data-stu-id="bec56-125">In the **New Project** dialog, expand **Installed** \> **Visual C++** \> **Windows Desktop** in the left pane, then select **Windows Console Application**.</span></span> <span data-ttu-id="bec56-126">For the project name, enter *helloworld*.</span><span class="sxs-lookup"><span data-stu-id="bec56-126">For the project name, enter *helloworld*.</span></span>

    ![Create Visual C++ Windows Desktop Windows Console Application](media/sdk/qs-cpp-windows-01-new-console-app.png)

1. <span data-ttu-id="bec56-128">If you're running 64-bit Windows, you may switch your build platform to `x64` using the drop-down menu in the Visual Studio toolbar.</span><span class="sxs-lookup"><span data-stu-id="bec56-128">If you're running 64-bit Windows, you may switch your build platform to `x64` using the drop-down menu in the Visual Studio toolbar.</span></span> <span data-ttu-id="bec56-129">(64-bit versions of Windows can run 32-bit applications, so this is not a requirement.)</span><span class="sxs-lookup"><span data-stu-id="bec56-129">(64-bit versions of Windows can run 32-bit applications, so this is not a requirement.)</span></span>

    ![Switch the build platform to x64](media/sdk/qs-cpp-windows-02-switch-to-x64.png)

1. <span data-ttu-id="bec56-131">In Solution Explorer, right-click the solution and choose **Manage NuGet Packages for Solution**.</span><span class="sxs-lookup"><span data-stu-id="bec56-131">In Solution Explorer, right-click the solution and choose **Manage NuGet Packages for Solution**.</span></span>

    ![Right-click Manage NuGet Packages for Solution](media/sdk/qs-cpp-windows-03-manage-nuget-packages.png)

1. <span data-ttu-id="bec56-133">In the upper-right corner, in the **Package Source** field, select **Nuget.org**. Search for the `Microsoft.CognitiveServices.Speech` package and install it into the **helloworld** project.</span><span class="sxs-lookup"><span data-stu-id="bec56-133">In the upper-right corner, in the **Package Source** field, select **Nuget.org**. Search for the `Microsoft.CognitiveServices.Speech` package and install it into the **helloworld** project.</span></span>

    ![Install Microsoft.CognitiveServices.Speech NuGet Package](media/sdk/qs-cpp-windows-04-nuget-install-0.5.0.png)

1. <span data-ttu-id="bec56-135">Accept the displayed license to begin installation of the NuGet package.</span><span class="sxs-lookup"><span data-stu-id="bec56-135">Accept the displayed license to begin installation of the NuGet package.</span></span>

    ![Accept the license](media/sdk/qs-cpp-windows-05-nuget-license.png)

<span data-ttu-id="bec56-137">After the package is installed, a confirmation appears in the Package Manager console.</span><span class="sxs-lookup"><span data-stu-id="bec56-137">After the package is installed, a confirmation appears in the Package Manager console.</span></span>

## <a name="add-sample-code"></a><span data-ttu-id="bec56-138">Add sample code</span><span class="sxs-lookup"><span data-stu-id="bec56-138">Add sample code</span></span>

1. <span data-ttu-id="bec56-139">Open the source file *helloworld.cpp*.</span><span class="sxs-lookup"><span data-stu-id="bec56-139">Open the source file *helloworld.cpp*.</span></span> <span data-ttu-id="bec56-140">Replace all the code in it with the following.</span><span class="sxs-lookup"><span data-stu-id="bec56-140">Replace all the code in it with the following.</span></span>

   [!code-cpp[Quickstart Code](~/samples-cognitive-services-speech-sdk/quickstart/cpp-windows/helloworld/helloworld.cpp#code)]

1. <span data-ttu-id="bec56-141">In the same file, replace the string `YourSubscriptionKey` with your subscription key.</span><span class="sxs-lookup"><span data-stu-id="bec56-141">In the same file, replace the string `YourSubscriptionKey` with your subscription key.</span></span>

1. <span data-ttu-id="bec56-142">Also replace the string `YourServiceRegion` with the [region](regions.md) associated with your subscription (for example, `westus` for the free trial subscription).</span><span class="sxs-lookup"><span data-stu-id="bec56-142">Also replace the string `YourServiceRegion` with the [region](regions.md) associated with your subscription (for example, `westus` for the free trial subscription).</span></span>

1. <span data-ttu-id="bec56-143">Save changes to the project.</span><span class="sxs-lookup"><span data-stu-id="bec56-143">Save changes to the project.</span></span>

## <a name="build-and-run-the-app"></a><span data-ttu-id="bec56-144">Build and run the app</span><span class="sxs-lookup"><span data-stu-id="bec56-144">Build and run the app</span></span>

1. <span data-ttu-id="bec56-145">Build the application.</span><span class="sxs-lookup"><span data-stu-id="bec56-145">Build the application.</span></span> <span data-ttu-id="bec56-146">From the menu bar, choose **Build** > **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="bec56-146">From the menu bar, choose **Build** > **Build Solution**.</span></span> <span data-ttu-id="bec56-147">The code should compile without errors.</span><span class="sxs-lookup"><span data-stu-id="bec56-147">The code should compile without errors.</span></span>

   ![Successful build](media/sdk/qs-cpp-windows-06-build.png)

1. <span data-ttu-id="bec56-149">Start the application.</span><span class="sxs-lookup"><span data-stu-id="bec56-149">Start the application.</span></span> <span data-ttu-id="bec56-150">From the menu bar, choose **Debug** > **Start Debugging**, or press **F5**.</span><span class="sxs-lookup"><span data-stu-id="bec56-150">From the menu bar, choose **Debug** > **Start Debugging**, or press **F5**.</span></span>

   ![Launch the app into debugging](media/sdk/qs-cpp-windows-07-start-debugging.png)

1. <span data-ttu-id="bec56-152">A console window appears, prompting you to say something.</span><span class="sxs-lookup"><span data-stu-id="bec56-152">A console window appears, prompting you to say something.</span></span> <span data-ttu-id="bec56-153">Speak an English phrase or sentence.</span><span class="sxs-lookup"><span data-stu-id="bec56-153">Speak an English phrase or sentence.</span></span> <span data-ttu-id="bec56-154">Your speech is transmitted to the Speech service and transcribed to text, which appears in the same window.</span><span class="sxs-lookup"><span data-stu-id="bec56-154">Your speech is transmitted to the Speech service and transcribed to text, which appears in the same window.</span></span>

   ![Console output after successful recognition](media/sdk/qs-cpp-windows-08-console-output-release.png)

[!INCLUDE [Download this sample](../../../includes/cognitive-services-speech-service-speech-sdk-sample-download-h2.md)]
<span data-ttu-id="bec56-156">Look for this sample in the `quickstart/cpp-windows` folder.</span><span class="sxs-lookup"><span data-stu-id="bec56-156">Look for this sample in the `quickstart/cpp-windows` folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bec56-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="bec56-157">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bec56-158">Recognize intents from speech by using the Speech SDK for C#</span><span class="sxs-lookup"><span data-stu-id="bec56-158">Recognize intents from speech by using the Speech SDK for C#</span></span>](how-to-recognize-intents-from-speech-csharp.md)

## <a name="see-also"></a><span data-ttu-id="bec56-159">See also</span><span class="sxs-lookup"><span data-stu-id="bec56-159">See also</span></span>

- [<span data-ttu-id="bec56-160">Translate speech</span><span class="sxs-lookup"><span data-stu-id="bec56-160">Translate speech</span></span>](how-to-translate-speech-csharp.md)
- [<span data-ttu-id="bec56-161">Customize acoustic models</span><span class="sxs-lookup"><span data-stu-id="bec56-161">Customize acoustic models</span></span>](how-to-customize-acoustic-models.md)
- [<span data-ttu-id="bec56-162">Customize language models</span><span class="sxs-lookup"><span data-stu-id="bec56-162">Customize language models</span></span>](how-to-customize-language-model.md)
