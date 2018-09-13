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
# <a name="quickstart-recognize-speech-in-c-under-net-core-on-windows-using-the-speech-sdk"></a>Quickstart: Recognize speech in C# under .NET Core on Windows using the Speech SDK

[!INCLUDE [Selector](../../../includes/cognitive-services-speech-service-quickstart-selector.md)]

In this article, you create a C# console application for .NET Core on Windows using the Cognitive Services [Speech SDK](speech-sdk.md) to transcribe speech to text in real time from your PC's microphone. The application is built with the [Speech SDK NuGet package](https://aka.ms/csspeech/nuget) and Microsoft Visual Studio 2017 (any edition).

## <a name="prerequisites"></a>Prerequisites

> [!NOTE]
> .NET Core is an open-source, cross-platform .NET platform implementing the [.NET Standard](https://docs.microsoft.com/dotnet/standard/net-standard) specification.

## <a name="prerequisites"></a>Prerequisites

You need a Speech service subscription key to complete this Quickstart. You can get one for free. See [Try the speech service for free](get-started.md) for details.


## <a name="create-visual-studio-project"></a>Create Visual Studio project

1. Start Visual Studio 2017.

1. Make sure the **.NET cross-platform development** workload is available. Choose **Tools** \> **Get Tools and Features** from the Visual Studio menu bar to open the Visual Studio installer. If this workload is already enabled, close the dialog.

    ![Enable .NET Core cross-platform development](media/sdk/vs-enable-net-core-workload.png)

    Otherwise, mark the checkbox next to **.NET cross-platform development,** then click the **Modify** button at the lower right corner of the dialog. Installation of the new feature will take a moment.

1. Create a new Visual C# .NET Core Console App. In the **New Project** dialog box, from the left pane, expand **Installed** \> **Visual C#** \> **.NET Core** and then select **Console App (.NET Core)**. For the project name, enter *helloworld*.

    ![Create Visual C# Console App (.NET Core)](media/sdk/qs-csharp-dotnetcore-windows-01-new-console-app.png "Create Visual C# Console App (.NET Core)")

1. Install and reference the [Speech SDK NuGet package](https://aka.ms/csspeech/nuget). In the Solution Explorer, right-click the solution and select **Manage NuGet Packages for Solution**.

    ![Right-click Manage NuGet Packages for Solution](media/sdk/qs-csharp-dotnetcore-windows-02-manage-nuget-packages.png "Manage NuGet Packages for Solution")

1. In the upper-right corner, in the **Package Source** field, select **Nuget.org**. Search for the `Microsoft.CognitiveServices.Speech` package and install it into the **helloworld** project.

    ![Install Microsoft.CognitiveServices.Speech NuGet Package](media/sdk/qs-csharp-dotnetcore-windows-03-nuget-install-0.5.0.png "Install Nuget package")

1. Accept the displayed license to begin installation of the NuGet package.

    ![Accept the license](media/sdk/qs-csharp-dotnetcore-windows-04-nuget-license.png "Accept the license")

AFter the package is installed, a confirmation appears in the Package Manager console.


## <a name="add-sample-code"></a>Add sample code

1. Open `Program.cs` and replace all the code in it with the following.

    [!code-csharp[Quickstart Code](~/samples-cognitive-services-speech-sdk/quickstart/csharp-dotnetcore-windows/helloworld/Program.cs#code)]

1. In the same file, replace the string `YourSubscriptionKey` with your subscription key.

1. Also replace the string `YourServiceRegion` with the [region](regions.md) associated with your subscription (for example, `westus` for the free trial subscription).

1. Save changes to the project.

## <a name="build-and-run-the-app"></a>Build and run the app

1. Build the application. From the menu bar, choose **Build** > **Build Solution**. The code should compile without errors.

    ![Successful build](media/sdk/qs-csharp-dotnetcore-windows-05-build.png "Successful build")

1. Start the application. From the menu bar, choose **Debug** > **Start Debugging**, or press **F5**.

    ![Start the app into debugging](media/sdk/qs-csharp-dotnetcore-windows-06-start-debugging.png "Start the app into debugging")

1. A console window appears, prompting you to say something. Speak an English phrase or sentence. Your speech is transmitted to the Speech service and transcribed to text, which appears in the same window.

    ![Console output after successful recognition](media/sdk/qs-csharp-dotnetcore-windows-07-console-output.png "Console output after successful recognition")

[!INCLUDE [Download this sample](../../../includes/cognitive-services-speech-service-speech-sdk-sample-download-h2.md)]
Look for this sample in the `quickstart/csharp-dotnetcore-windows` folder.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Recognize intents from speech by using the Speech SDK for C#](how-to-recognize-intents-from-speech-csharp.md)

## <a name="see-also"></a>See also

- [Translate speech](how-to-translate-speech-csharp.md)
- [Customize acoustic models](how-to-customize-acoustic-models.md)
- [Customize language models](how-to-customize-language-model.md)
