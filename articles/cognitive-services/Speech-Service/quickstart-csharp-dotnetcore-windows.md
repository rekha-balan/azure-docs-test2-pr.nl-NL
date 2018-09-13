---
title: 'Quickstart: Recognize speech in C# under .NET Core on Windows using the Cognitive Services Speech SDK'
titleSuffix: Microsoft Cognitive Services
description: Learn how to recognize speech in C# under .NET Core on Windows using the Cognitive Services Speech SDK
services: cognitive-services
author: wolfma61
ms.service: cognitive-services
ms.component: speech-service
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: wolfma
ms.openlocfilehash: a4435df33644bc330d1b0bcc69e60681f855f50c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966361"
---
# <a name="quickstart-recognize-speech-in-c-under-net-core-on-windows-using-the-speech-sdk"></a><span data-ttu-id="00afd-103">Quickstart: Recognize speech in C# under .NET Core on Windows using the Speech SDK</span><span class="sxs-lookup"><span data-stu-id="00afd-103">Quickstart: Recognize speech in C# under .NET Core on Windows using the Speech SDK</span></span>

[!INCLUDE [Selector](../../../includes/cognitive-services-speech-service-quickstart-selector.md)]

<span data-ttu-id="00afd-104">In this article, you create a C# console application for .NET Core on Windows using the Cognitive Services [Speech SDK](speech-sdk.md) to transcribe speech to text in real time from your PC's microphone.</span><span class="sxs-lookup"><span data-stu-id="00afd-104">In this article, you create a C# console application for .NET Core on Windows using the Cognitive Services [Speech SDK](speech-sdk.md) to transcribe speech to text in real time from your PC's microphone.</span></span> <span data-ttu-id="00afd-105">The application is built with the [Speech SDK NuGet package](https://aka.ms/csspeech/nuget) and Microsoft Visual Studio 2017 (any edition).</span><span class="sxs-lookup"><span data-stu-id="00afd-105">The application is built with the [Speech SDK NuGet package](https://aka.ms/csspeech/nuget) and Microsoft Visual Studio 2017 (any edition).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00afd-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="00afd-106">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="00afd-107">.NET Core is an open-source, cross-platform .NET platform implementing the [.NET Standard](https://docs.microsoft.com/dotnet/standard/net-standard) specification.</span><span class="sxs-lookup"><span data-stu-id="00afd-107">.NET Core is an open-source, cross-platform .NET platform implementing the [.NET Standard](https://docs.microsoft.com/dotnet/standard/net-standard) specification.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00afd-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="00afd-108">Prerequisites</span></span>

<span data-ttu-id="00afd-109">You need a Speech service subscription key to complete this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="00afd-109">You need a Speech service subscription key to complete this Quickstart.</span></span> <span data-ttu-id="00afd-110">You can get one for free.</span><span class="sxs-lookup"><span data-stu-id="00afd-110">You can get one for free.</span></span> <span data-ttu-id="00afd-111">See [Try the speech service for free](get-started.md) for details.</span><span class="sxs-lookup"><span data-stu-id="00afd-111">See [Try the speech service for free](get-started.md) for details.</span></span>


## <a name="create-visual-studio-project"></a><span data-ttu-id="00afd-112">Create Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="00afd-112">Create Visual Studio project</span></span>

1. <span data-ttu-id="00afd-113">Start Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="00afd-113">Start Visual Studio 2017.</span></span>

1. <span data-ttu-id="00afd-114">Make sure the **.NET cross-platform development** workload is available.</span><span class="sxs-lookup"><span data-stu-id="00afd-114">Make sure the **.NET cross-platform development** workload is available.</span></span> <span data-ttu-id="00afd-115">Choose **Tools** \> **Get Tools and Features** from the Visual Studio menu bar to open the Visual Studio installer.</span><span class="sxs-lookup"><span data-stu-id="00afd-115">Choose **Tools** \> **Get Tools and Features** from the Visual Studio menu bar to open the Visual Studio installer.</span></span> <span data-ttu-id="00afd-116">If this workload is already enabled, close the dialog.</span><span class="sxs-lookup"><span data-stu-id="00afd-116">If this workload is already enabled, close the dialog.</span></span>

    ![Enable .NET Core cross-platform development](media/sdk/vs-enable-net-core-workload.png)

    <span data-ttu-id="00afd-118">Otherwise, mark the checkbox next to **.NET cross-platform development,** then click the **Modify** button at the lower right corner of the dialog.</span><span class="sxs-lookup"><span data-stu-id="00afd-118">Otherwise, mark the checkbox next to **.NET cross-platform development,** then click the **Modify** button at the lower right corner of the dialog.</span></span> <span data-ttu-id="00afd-119">Installation of the new feature will take a moment.</span><span class="sxs-lookup"><span data-stu-id="00afd-119">Installation of the new feature will take a moment.</span></span>

1. <span data-ttu-id="00afd-120">Create a new Visual C# .NET Core Console App.</span><span class="sxs-lookup"><span data-stu-id="00afd-120">Create a new Visual C# .NET Core Console App.</span></span> <span data-ttu-id="00afd-121">In the **New Project** dialog box, from the left pane, expand **Installed** \> **Visual C#** \> **.NET Core** and then select **Console App (.NET Core)**.</span><span class="sxs-lookup"><span data-stu-id="00afd-121">In the **New Project** dialog box, from the left pane, expand **Installed** \> **Visual C#** \> **.NET Core** and then select **Console App (.NET Core)**.</span></span> <span data-ttu-id="00afd-122">For the project name, enter *helloworld*.</span><span class="sxs-lookup"><span data-stu-id="00afd-122">For the project name, enter *helloworld*.</span></span>

    <span data-ttu-id="00afd-123">![Create Visual C# Console App (.NET Core)](media/sdk/qs-csharp-dotnetcore-windows-01-new-console-app.png "Create Visual C# Console App (.NET Core)")</span><span class="sxs-lookup"><span data-stu-id="00afd-123">![Create Visual C# Console App (.NET Core)](media/sdk/qs-csharp-dotnetcore-windows-01-new-console-app.png "Create Visual C# Console App (.NET Core)")</span></span>

1. <span data-ttu-id="00afd-124">Install and reference the [Speech SDK NuGet package](https://aka.ms/csspeech/nuget).</span><span class="sxs-lookup"><span data-stu-id="00afd-124">Install and reference the [Speech SDK NuGet package](https://aka.ms/csspeech/nuget).</span></span> <span data-ttu-id="00afd-125">In the Solution Explorer, right-click the solution and select **Manage NuGet Packages for Solution**.</span><span class="sxs-lookup"><span data-stu-id="00afd-125">In the Solution Explorer, right-click the solution and select **Manage NuGet Packages for Solution**.</span></span>

    <span data-ttu-id="00afd-126">![Right-click Manage NuGet Packages for Solution](media/sdk/qs-csharp-dotnetcore-windows-02-manage-nuget-packages.png "Manage NuGet Packages for Solution")</span><span class="sxs-lookup"><span data-stu-id="00afd-126">![Right-click Manage NuGet Packages for Solution](media/sdk/qs-csharp-dotnetcore-windows-02-manage-nuget-packages.png "Manage NuGet Packages for Solution")</span></span>

1. <span data-ttu-id="00afd-127">In the upper-right corner, in the **Package Source** field, select **Nuget.org**. Search for the `Microsoft.CognitiveServices.Speech` package and install it into the **helloworld** project.</span><span class="sxs-lookup"><span data-stu-id="00afd-127">In the upper-right corner, in the **Package Source** field, select **Nuget.org**. Search for the `Microsoft.CognitiveServices.Speech` package and install it into the **helloworld** project.</span></span>

    <span data-ttu-id="00afd-128">![Install Microsoft.CognitiveServices.Speech NuGet Package](media/sdk/qs-csharp-dotnetcore-windows-03-nuget-install-0.5.0.png "Install Nuget package")</span><span class="sxs-lookup"><span data-stu-id="00afd-128">![Install Microsoft.CognitiveServices.Speech NuGet Package](media/sdk/qs-csharp-dotnetcore-windows-03-nuget-install-0.5.0.png "Install Nuget package")</span></span>

1. <span data-ttu-id="00afd-129">Accept the displayed license to begin installation of the NuGet package.</span><span class="sxs-lookup"><span data-stu-id="00afd-129">Accept the displayed license to begin installation of the NuGet package.</span></span>

    <span data-ttu-id="00afd-130">![Accept the license](media/sdk/qs-csharp-dotnetcore-windows-04-nuget-license.png "Accept the license")</span><span class="sxs-lookup"><span data-stu-id="00afd-130">![Accept the license](media/sdk/qs-csharp-dotnetcore-windows-04-nuget-license.png "Accept the license")</span></span>

<span data-ttu-id="00afd-131">AFter the package is installed, a confirmation appears in the Package Manager console.</span><span class="sxs-lookup"><span data-stu-id="00afd-131">AFter the package is installed, a confirmation appears in the Package Manager console.</span></span>


## <a name="add-sample-code"></a><span data-ttu-id="00afd-132">Add sample code</span><span class="sxs-lookup"><span data-stu-id="00afd-132">Add sample code</span></span>

1. <span data-ttu-id="00afd-133">Open `Program.cs` and replace all the code in it with the following.</span><span class="sxs-lookup"><span data-stu-id="00afd-133">Open `Program.cs` and replace all the code in it with the following.</span></span>

    [!code-csharp[Quickstart Code](~/samples-cognitive-services-speech-sdk/quickstart/csharp-dotnetcore-windows/helloworld/Program.cs#code)]

1. <span data-ttu-id="00afd-134">In the same file, replace the string `YourSubscriptionKey` with your subscription key.</span><span class="sxs-lookup"><span data-stu-id="00afd-134">In the same file, replace the string `YourSubscriptionKey` with your subscription key.</span></span>

1. <span data-ttu-id="00afd-135">Also replace the string `YourServiceRegion` with the [region](regions.md) associated with your subscription (for example, `westus` for the free trial subscription).</span><span class="sxs-lookup"><span data-stu-id="00afd-135">Also replace the string `YourServiceRegion` with the [region](regions.md) associated with your subscription (for example, `westus` for the free trial subscription).</span></span>

1. <span data-ttu-id="00afd-136">Save changes to the project.</span><span class="sxs-lookup"><span data-stu-id="00afd-136">Save changes to the project.</span></span>

## <a name="build-and-run-the-app"></a><span data-ttu-id="00afd-137">Build and run the app</span><span class="sxs-lookup"><span data-stu-id="00afd-137">Build and run the app</span></span>

1. <span data-ttu-id="00afd-138">Build the application.</span><span class="sxs-lookup"><span data-stu-id="00afd-138">Build the application.</span></span> <span data-ttu-id="00afd-139">From the menu bar, choose **Build** > **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="00afd-139">From the menu bar, choose **Build** > **Build Solution**.</span></span> <span data-ttu-id="00afd-140">The code should compile without errors.</span><span class="sxs-lookup"><span data-stu-id="00afd-140">The code should compile without errors.</span></span>

    <span data-ttu-id="00afd-141">![Successful build](media/sdk/qs-csharp-dotnetcore-windows-05-build.png "Successful build")</span><span class="sxs-lookup"><span data-stu-id="00afd-141">![Successful build](media/sdk/qs-csharp-dotnetcore-windows-05-build.png "Successful build")</span></span>

1. <span data-ttu-id="00afd-142">Start the application.</span><span class="sxs-lookup"><span data-stu-id="00afd-142">Start the application.</span></span> <span data-ttu-id="00afd-143">From the menu bar, choose **Debug** > **Start Debugging**, or press **F5**.</span><span class="sxs-lookup"><span data-stu-id="00afd-143">From the menu bar, choose **Debug** > **Start Debugging**, or press **F5**.</span></span>

    <span data-ttu-id="00afd-144">![Start the app into debugging](media/sdk/qs-csharp-dotnetcore-windows-06-start-debugging.png "Start the app into debugging")</span><span class="sxs-lookup"><span data-stu-id="00afd-144">![Start the app into debugging](media/sdk/qs-csharp-dotnetcore-windows-06-start-debugging.png "Start the app into debugging")</span></span>

1. <span data-ttu-id="00afd-145">A console window appears, prompting you to say something.</span><span class="sxs-lookup"><span data-stu-id="00afd-145">A console window appears, prompting you to say something.</span></span> <span data-ttu-id="00afd-146">Speak an English phrase or sentence.</span><span class="sxs-lookup"><span data-stu-id="00afd-146">Speak an English phrase or sentence.</span></span> <span data-ttu-id="00afd-147">Your speech is transmitted to the Speech service and transcribed to text, which appears in the same window.</span><span class="sxs-lookup"><span data-stu-id="00afd-147">Your speech is transmitted to the Speech service and transcribed to text, which appears in the same window.</span></span>

    <span data-ttu-id="00afd-148">![Console output after successful recognition](media/sdk/qs-csharp-dotnetcore-windows-07-console-output.png "Console output after successful recognition")</span><span class="sxs-lookup"><span data-stu-id="00afd-148">![Console output after successful recognition](media/sdk/qs-csharp-dotnetcore-windows-07-console-output.png "Console output after successful recognition")</span></span>

[!INCLUDE [Download this sample](../../../includes/cognitive-services-speech-service-speech-sdk-sample-download-h2.md)]
<span data-ttu-id="00afd-149">Look for this sample in the `quickstart/csharp-dotnetcore-windows` folder.</span><span class="sxs-lookup"><span data-stu-id="00afd-149">Look for this sample in the `quickstart/csharp-dotnetcore-windows` folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00afd-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="00afd-150">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="00afd-151">Recognize intents from speech by using the Speech SDK for C#</span><span class="sxs-lookup"><span data-stu-id="00afd-151">Recognize intents from speech by using the Speech SDK for C#</span></span>](how-to-recognize-intents-from-speech-csharp.md)

## <a name="see-also"></a><span data-ttu-id="00afd-152">See also</span><span class="sxs-lookup"><span data-stu-id="00afd-152">See also</span></span>

- [<span data-ttu-id="00afd-153">Translate speech</span><span class="sxs-lookup"><span data-stu-id="00afd-153">Translate speech</span></span>](how-to-translate-speech-csharp.md)
- [<span data-ttu-id="00afd-154">Customize acoustic models</span><span class="sxs-lookup"><span data-stu-id="00afd-154">Customize acoustic models</span></span>](how-to-customize-acoustic-models.md)
- [<span data-ttu-id="00afd-155">Customize language models</span><span class="sxs-lookup"><span data-stu-id="00afd-155">Customize language models</span></span>](how-to-customize-language-model.md)
