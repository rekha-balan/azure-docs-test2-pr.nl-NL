---
title: 'Quickstart: Recognize speech in C# under .NET Framework on Windows using the Cognitive Services Speech SDK'
titleSuffix: Microsoft Cognitive Services
description: Learn how to recognize speech in C# under .NET Framework on Windows using the Cognitive Services Speech SDK
services: cognitive-services
author: wolfma61
ms.service: cognitive-services
ms.component: speech-service
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: wolfma
ms.openlocfilehash: b29ec3ba846d363a222fe2ecb304a5a1dce67990
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967865"
---
# <a name="quickstart-recognize-speech-in-c-under-net-framework-on-windows-using-the-speech-sdk"></a><span data-ttu-id="39e65-103">Quickstart: Recognize speech in C# under .NET Framework on Windows using the Speech SDK</span><span class="sxs-lookup"><span data-stu-id="39e65-103">Quickstart: Recognize speech in C# under .NET Framework on Windows using the Speech SDK</span></span>

[!INCLUDE [Selector](../../../includes/cognitive-services-speech-service-quickstart-selector.md)]

<span data-ttu-id="39e65-104">In this article, you create a C# console application for .NET Framework on Windows using the [Speech SDK](speech-sdk.md) to transcribe speech to text in real time from your PC's microphone.</span><span class="sxs-lookup"><span data-stu-id="39e65-104">In this article, you create a C# console application for .NET Framework on Windows using the [Speech SDK](speech-sdk.md) to transcribe speech to text in real time from your PC's microphone.</span></span>
<span data-ttu-id="39e65-105">The application is built with the [Speech SDK NuGet package](https://aka.ms/csspeech/nuget) and Microsoft Visual Studio 2017 (any edition).</span><span class="sxs-lookup"><span data-stu-id="39e65-105">The application is built with the [Speech SDK NuGet package](https://aka.ms/csspeech/nuget) and Microsoft Visual Studio 2017 (any edition).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39e65-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="39e65-106">Prerequisites</span></span>

<span data-ttu-id="39e65-107">You need a Speech service subscription key to complete this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="39e65-107">You need a Speech service subscription key to complete this Quickstart.</span></span> <span data-ttu-id="39e65-108">You can get one for free.</span><span class="sxs-lookup"><span data-stu-id="39e65-108">You can get one for free.</span></span> <span data-ttu-id="39e65-109">See [Try the speech service for free](get-started.md) for details.</span><span class="sxs-lookup"><span data-stu-id="39e65-109">See [Try the speech service for free](get-started.md) for details.</span></span>

## <a name="create-visual-studio-project"></a><span data-ttu-id="39e65-110">Create Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="39e65-110">Create Visual Studio project</span></span>

1. <span data-ttu-id="39e65-111">Start Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="39e65-111">Start Visual Studio 2017.</span></span>
 
1. <span data-ttu-id="39e65-112">Make sure the **.NET desktop environment** workload is available.</span><span class="sxs-lookup"><span data-stu-id="39e65-112">Make sure the **.NET desktop environment** workload is available.</span></span> <span data-ttu-id="39e65-113">Choose **Tools** \> **Get Tools and Features** from the Visual Studio menu bar to open the Visual Studio installer.</span><span class="sxs-lookup"><span data-stu-id="39e65-113">Choose **Tools** \> **Get Tools and Features** from the Visual Studio menu bar to open the Visual Studio installer.</span></span> <span data-ttu-id="39e65-114">If this workload is already enabled, close the dialog.</span><span class="sxs-lookup"><span data-stu-id="39e65-114">If this workload is already enabled, close the dialog.</span></span> 

    <span data-ttu-id="39e65-115">Otherwise, mark the checkbox next to **.NET desktop development,** then click the **Modify** button at the lower right corner of the dialog.</span><span class="sxs-lookup"><span data-stu-id="39e65-115">Otherwise, mark the checkbox next to **.NET desktop development,** then click the **Modify** button at the lower right corner of the dialog.</span></span> <span data-ttu-id="39e65-116">Installation of the new feature will take a moment.</span><span class="sxs-lookup"><span data-stu-id="39e65-116">Installation of the new feature will take a moment.</span></span>

    ![Enable .NET desktop development](media/sdk/vs-enable-net-desktop-workload.png)

1. <span data-ttu-id="39e65-118">Create a new Visual C# Console App.</span><span class="sxs-lookup"><span data-stu-id="39e65-118">Create a new Visual C# Console App.</span></span> <span data-ttu-id="39e65-119">In the **New Project** dialog box, from the left pane, expand **Installed** \> **Visual C#** \> **Windows Desktop** and then choose **Console App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="39e65-119">In the **New Project** dialog box, from the left pane, expand **Installed** \> **Visual C#** \> **Windows Desktop** and then choose **Console App (.NET Framework)**.</span></span> <span data-ttu-id="39e65-120">For the project name, enter *helloworld*.</span><span class="sxs-lookup"><span data-stu-id="39e65-120">For the project name, enter *helloworld*.</span></span>

    <span data-ttu-id="39e65-121">![Create Visual C# Console App (.NET Framework)](media/sdk/qs-csharp-dotnet-windows-01-new-console-app.png "Create Visual C# Console App (.NET Framework)")</span><span class="sxs-lookup"><span data-stu-id="39e65-121">![Create Visual C# Console App (.NET Framework)](media/sdk/qs-csharp-dotnet-windows-01-new-console-app.png "Create Visual C# Console App (.NET Framework)")</span></span>

1. <span data-ttu-id="39e65-122">Install and reference the [Speech SDK NuGet package](https://aka.ms/csspeech/nuget).</span><span class="sxs-lookup"><span data-stu-id="39e65-122">Install and reference the [Speech SDK NuGet package](https://aka.ms/csspeech/nuget).</span></span> <span data-ttu-id="39e65-123">In the Solution Explorer, right-click the solution and select **Manage NuGet Packages for Solution**.</span><span class="sxs-lookup"><span data-stu-id="39e65-123">In the Solution Explorer, right-click the solution and select **Manage NuGet Packages for Solution**.</span></span>

    <span data-ttu-id="39e65-124">![Right-click Manage NuGet Packages for Solution](media/sdk/qs-csharp-dotnet-windows-02-manage-nuget-packages.png "Manage NuGet Packages for Solution")</span><span class="sxs-lookup"><span data-stu-id="39e65-124">![Right-click Manage NuGet Packages for Solution](media/sdk/qs-csharp-dotnet-windows-02-manage-nuget-packages.png "Manage NuGet Packages for Solution")</span></span>

1. <span data-ttu-id="39e65-125">In the upper-right corner, in the **Package Source** field, select **Nuget.org**. Search for the `Microsoft.CognitiveServices.Speech` package and install it into the **helloworld** project.</span><span class="sxs-lookup"><span data-stu-id="39e65-125">In the upper-right corner, in the **Package Source** field, select **Nuget.org**. Search for the `Microsoft.CognitiveServices.Speech` package and install it into the **helloworld** project.</span></span>

    <span data-ttu-id="39e65-126">![Install Microsoft.CognitiveServices.Speech NuGet Package](media/sdk/qs-csharp-dotnet-windows-03-nuget-install-0.5.0.png "Install Nuget package")</span><span class="sxs-lookup"><span data-stu-id="39e65-126">![Install Microsoft.CognitiveServices.Speech NuGet Package](media/sdk/qs-csharp-dotnet-windows-03-nuget-install-0.5.0.png "Install Nuget package")</span></span>

1. <span data-ttu-id="39e65-127">Accept the displayed license to begin installation of the NuGet package.</span><span class="sxs-lookup"><span data-stu-id="39e65-127">Accept the displayed license to begin installation of the NuGet package.</span></span>

    <span data-ttu-id="39e65-128">![Accept the license](media/sdk/qs-csharp-dotnet-windows-04-nuget-license.png "Accept the license")</span><span class="sxs-lookup"><span data-stu-id="39e65-128">![Accept the license](media/sdk/qs-csharp-dotnet-windows-04-nuget-license.png "Accept the license")</span></span>

    <span data-ttu-id="39e65-129">After the package is installed, a confirmation appears in the Package Manager console.</span><span class="sxs-lookup"><span data-stu-id="39e65-129">After the package is installed, a confirmation appears in the Package Manager console.</span></span>

1. <span data-ttu-id="39e65-130">Create a platform configuration matching your PC architecture via the Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="39e65-130">Create a platform configuration matching your PC architecture via the Configuration Manager.</span></span> <span data-ttu-id="39e65-131">Select **Build** > **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="39e65-131">Select **Build** > **Configuration Manager**.</span></span>

    <span data-ttu-id="39e65-132">![Launch the configuration manager](media/sdk/qs-csharp-dotnet-windows-05-cfg-manager-click.png "Launch the configuration manager")</span><span class="sxs-lookup"><span data-stu-id="39e65-132">![Launch the configuration manager](media/sdk/qs-csharp-dotnet-windows-05-cfg-manager-click.png "Launch the configuration manager")</span></span>

1. <span data-ttu-id="39e65-133">In the **Configuration Manager** dialog box, add a new platform.</span><span class="sxs-lookup"><span data-stu-id="39e65-133">In the **Configuration Manager** dialog box, add a new platform.</span></span> <span data-ttu-id="39e65-134">From the **Active solution platform** drop-down list, select **New**.</span><span class="sxs-lookup"><span data-stu-id="39e65-134">From the **Active solution platform** drop-down list, select **New**.</span></span>

    <span data-ttu-id="39e65-135">![Add a new platform under the configuration manager window](media/sdk/qs-csharp-dotnet-windows-06-cfg-manager-new.png "Add a new platform under the configuration manager window")</span><span class="sxs-lookup"><span data-stu-id="39e65-135">![Add a new platform under the configuration manager window](media/sdk/qs-csharp-dotnet-windows-06-cfg-manager-new.png "Add a new platform under the configuration manager window")</span></span>

1. <span data-ttu-id="39e65-136">If you are running 64-bit Windows, create a new platform configuration named `x64`.</span><span class="sxs-lookup"><span data-stu-id="39e65-136">If you are running 64-bit Windows, create a new platform configuration named `x64`.</span></span> <span data-ttu-id="39e65-137">If you are running 32-bit Windows, create a new platform configuration named `x86`.</span><span class="sxs-lookup"><span data-stu-id="39e65-137">If you are running 32-bit Windows, create a new platform configuration named `x86`.</span></span>

    <span data-ttu-id="39e65-138">![On 64-bit Windows, add a new platform named "x64"](media/sdk/qs-csharp-dotnet-windows-07-cfg-manager-add-x64.png "Add x64 platform")</span><span class="sxs-lookup"><span data-stu-id="39e65-138">![On 64-bit Windows, add a new platform named "x64"](media/sdk/qs-csharp-dotnet-windows-07-cfg-manager-add-x64.png "Add x64 platform")</span></span>


## <a name="add-sample-code"></a><span data-ttu-id="39e65-139">Add sample code</span><span class="sxs-lookup"><span data-stu-id="39e65-139">Add sample code</span></span>

1. <span data-ttu-id="39e65-140">Open `Program.cs` and replace all the code in it with the following.</span><span class="sxs-lookup"><span data-stu-id="39e65-140">Open `Program.cs` and replace all the code in it with the following.</span></span>

    [!code-csharp[Quickstart Code](~/samples-cognitive-services-speech-sdk/quickstart/csharp-dotnet-windows/helloworld/Program.cs#code)]

1. <span data-ttu-id="39e65-141">In the same file, replace the string `YourSubscriptionKey` with your Speech service subscription key.</span><span class="sxs-lookup"><span data-stu-id="39e65-141">In the same file, replace the string `YourSubscriptionKey` with your Speech service subscription key.</span></span>

1. <span data-ttu-id="39e65-142">Also replace the string `YourServiceRegion` with the [region](regions.md) associated with your subscription (for example, `westus` for the free trial subscription).</span><span class="sxs-lookup"><span data-stu-id="39e65-142">Also replace the string `YourServiceRegion` with the [region](regions.md) associated with your subscription (for example, `westus` for the free trial subscription).</span></span>

1. <span data-ttu-id="39e65-143">Save changes to the project.</span><span class="sxs-lookup"><span data-stu-id="39e65-143">Save changes to the project.</span></span>

## <a name="build-and-run-the-app"></a><span data-ttu-id="39e65-144">Build and run the app</span><span class="sxs-lookup"><span data-stu-id="39e65-144">Build and run the app</span></span>

1. <span data-ttu-id="39e65-145">Build the application.</span><span class="sxs-lookup"><span data-stu-id="39e65-145">Build the application.</span></span> <span data-ttu-id="39e65-146">From the menu bar, select **Build** > **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="39e65-146">From the menu bar, select **Build** > **Build Solution**.</span></span> <span data-ttu-id="39e65-147">The code should compile without errors now.</span><span class="sxs-lookup"><span data-stu-id="39e65-147">The code should compile without errors now.</span></span>

    <span data-ttu-id="39e65-148">![Successful build](media/sdk/qs-csharp-dotnet-windows-08-build.png "Successful build")</span><span class="sxs-lookup"><span data-stu-id="39e65-148">![Successful build](media/sdk/qs-csharp-dotnet-windows-08-build.png "Successful build")</span></span>

1. <span data-ttu-id="39e65-149">Start the application.</span><span class="sxs-lookup"><span data-stu-id="39e65-149">Start the application.</span></span> <span data-ttu-id="39e65-150">From the menu bar, select **Debug** > **Start Debugging**, or press **F5**.</span><span class="sxs-lookup"><span data-stu-id="39e65-150">From the menu bar, select **Debug** > **Start Debugging**, or press **F5**.</span></span>

    <span data-ttu-id="39e65-151">![Start the app into debugging](media/sdk/qs-csharp-dotnet-windows-09-start-debugging.png "Start the app into debugging")</span><span class="sxs-lookup"><span data-stu-id="39e65-151">![Start the app into debugging](media/sdk/qs-csharp-dotnet-windows-09-start-debugging.png "Start the app into debugging")</span></span>

1. <span data-ttu-id="39e65-152">A console window appears, prompting you to say something.</span><span class="sxs-lookup"><span data-stu-id="39e65-152">A console window appears, prompting you to say something.</span></span> <span data-ttu-id="39e65-153">Speak an English phrase or sentence.</span><span class="sxs-lookup"><span data-stu-id="39e65-153">Speak an English phrase or sentence.</span></span> <span data-ttu-id="39e65-154">Your speech is transmitted to the Speech service and transcribed to text, which appears in the same window.</span><span class="sxs-lookup"><span data-stu-id="39e65-154">Your speech is transmitted to the Speech service and transcribed to text, which appears in the same window.</span></span>

    <span data-ttu-id="39e65-155">![Console output after successful recognition](media/sdk/qs-csharp-dotnet-windows-10-console-output.png "Console output after successful recognition")</span><span class="sxs-lookup"><span data-stu-id="39e65-155">![Console output after successful recognition](media/sdk/qs-csharp-dotnet-windows-10-console-output.png "Console output after successful recognition")</span></span>

[!INCLUDE [Download this sample](../../../includes/cognitive-services-speech-service-speech-sdk-sample-download-h2.md)]
<span data-ttu-id="39e65-156">Look for this sample in the `quickstart/csharp-dotnet-windows` folder.</span><span class="sxs-lookup"><span data-stu-id="39e65-156">Look for this sample in the `quickstart/csharp-dotnet-windows` folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39e65-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="39e65-157">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="39e65-158">Recognize intents from speech by using the Speech SDK for C#</span><span class="sxs-lookup"><span data-stu-id="39e65-158">Recognize intents from speech by using the Speech SDK for C#</span></span>](how-to-recognize-intents-from-speech-csharp.md)

## <a name="see-also"></a><span data-ttu-id="39e65-159">See also</span><span class="sxs-lookup"><span data-stu-id="39e65-159">See also</span></span>

- [<span data-ttu-id="39e65-160">Translate speech</span><span class="sxs-lookup"><span data-stu-id="39e65-160">Translate speech</span></span>](how-to-translate-speech-csharp.md)
- [<span data-ttu-id="39e65-161">Customize acoustic models</span><span class="sxs-lookup"><span data-stu-id="39e65-161">Customize acoustic models</span></span>](how-to-customize-acoustic-models.md)
- [<span data-ttu-id="39e65-162">Customize language models</span><span class="sxs-lookup"><span data-stu-id="39e65-162">Customize language models</span></span>](how-to-customize-language-model.md)
