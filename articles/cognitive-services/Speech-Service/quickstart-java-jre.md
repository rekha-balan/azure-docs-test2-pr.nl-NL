---
title: 'Quickstart: Recognize speech in Java (Windows or Linux)'
titleSuffix: Microsoft Cognitive Services
description: Learn how to recognize speech in Java (Windows or Linux)
services: cognitive-services
author: fmegen
ms.service: cognitive-services
ms.technology: Speech
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: fmegen
ms.openlocfilehash: 6902e0a7246c172c5c02fab04228591a086252d0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865541"
---
# <a name="quickstart-recognize-speech-in-java-on-windows-or-linux-using-the-speech-sdk"></a><span data-ttu-id="e3922-103">Quickstart: Recognize speech in Java on Windows or Linux using the Speech SDK</span><span class="sxs-lookup"><span data-stu-id="e3922-103">Quickstart: Recognize speech in Java on Windows or Linux using the Speech SDK</span></span>

[!INCLUDE [Selector](../../../includes/cognitive-services-speech-service-quickstart-selector.md)]

<span data-ttu-id="e3922-104">In this article, you create a Java console application using the [Speech SDK](speech-sdk.md) to transcribe speech to text in real time from your PC's microphone.</span><span class="sxs-lookup"><span data-stu-id="e3922-104">In this article, you create a Java console application using the [Speech SDK](speech-sdk.md) to transcribe speech to text in real time from your PC's microphone.</span></span> <span data-ttu-id="e3922-105">The application is built with the Speech SDK Maven package and the Eclipse Java IDE (v4.8) on 64-bit Windows or Ubuntu Linux 16.04.</span><span class="sxs-lookup"><span data-stu-id="e3922-105">The application is built with the Speech SDK Maven package and the Eclipse Java IDE (v4.8) on 64-bit Windows or Ubuntu Linux 16.04.</span></span> <span data-ttu-id="e3922-106">It runs on a 64-bit Java 8 runtime environment (JRE).</span><span class="sxs-lookup"><span data-stu-id="e3922-106">It runs on a 64-bit Java 8 runtime environment (JRE).</span></span>

> [!NOTE]
> <span data-ttu-id="e3922-107">For the Speech Devices SDK and the Roobo device, see [Speech Devices SDK](speech-devices-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="e3922-107">For the Speech Devices SDK and the Roobo device, see [Speech Devices SDK](speech-devices-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3922-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e3922-108">Prerequisites</span></span>

<span data-ttu-id="e3922-109">You need a Speech service subscription key to complete this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="e3922-109">You need a Speech service subscription key to complete this Quickstart.</span></span> <span data-ttu-id="e3922-110">You can get one for free.</span><span class="sxs-lookup"><span data-stu-id="e3922-110">You can get one for free.</span></span> <span data-ttu-id="e3922-111">See [Try the speech service for free](get-started.md) for details.</span><span class="sxs-lookup"><span data-stu-id="e3922-111">See [Try the speech service for free](get-started.md) for details.</span></span>


## <a name="create-and-configure-project"></a><span data-ttu-id="e3922-112">Create and configure project</span><span class="sxs-lookup"><span data-stu-id="e3922-112">Create and configure project</span></span>

<span data-ttu-id="e3922-113">If you are using Ubuntu 16.04, before starting Eclipse, run the following commands ta make sure that required packages are installed.</span><span class="sxs-lookup"><span data-stu-id="e3922-113">If you are using Ubuntu 16.04, before starting Eclipse, run the following commands ta make sure that required packages are installed.</span></span>

  ```sh
  sudo apt-get update
  sudo apt-get install build-essential libssl1.0.0 libcurl3 libasound2 wget
  ```

1. <span data-ttu-id="e3922-114">Start Eclipse.</span><span class="sxs-lookup"><span data-stu-id="e3922-114">Start Eclipse.</span></span>

1. <span data-ttu-id="e3922-115">In the Eclipse Launcher, enter the name of a new workspace directory into the **Workspace** field.</span><span class="sxs-lookup"><span data-stu-id="e3922-115">In the Eclipse Launcher, enter the name of a new workspace directory into the **Workspace** field.</span></span> <span data-ttu-id="e3922-116">Then click **Launch**.</span><span class="sxs-lookup"><span data-stu-id="e3922-116">Then click **Launch**.</span></span>

   ![Create Eclipse workspace](media/sdk/qs-java-jre-01-create-new-eclipse-workspace.png)

1. <span data-ttu-id="e3922-118">In a moment, the main window of the Eclipse IDE appears.</span><span class="sxs-lookup"><span data-stu-id="e3922-118">In a moment, the main window of the Eclipse IDE appears.</span></span> <span data-ttu-id="e3922-119">Close the Welcome screen if one is present.</span><span class="sxs-lookup"><span data-stu-id="e3922-119">Close the Welcome screen if one is present.</span></span>

1. <span data-ttu-id="e3922-120">Create a new project by choosing **File** \> **New** \> **Project** from the Eclipse menu bar.</span><span class="sxs-lookup"><span data-stu-id="e3922-120">Create a new project by choosing **File** \> **New** \> **Project** from the Eclipse menu bar.</span></span>

1. <span data-ttu-id="e3922-121">The **New Project** dialog appears.</span><span class="sxs-lookup"><span data-stu-id="e3922-121">The **New Project** dialog appears.</span></span> <span data-ttu-id="e3922-122">In this window, select **Java Project**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e3922-122">In this window, select **Java Project**, and click **Next**.</span></span>

   ![Select a wizard](media/sdk/qs-java-jre-02-select-wizard.png)

1. <span data-ttu-id="e3922-124">The New Java Project wizard starts.</span><span class="sxs-lookup"><span data-stu-id="e3922-124">The New Java Project wizard starts.</span></span> <span data-ttu-id="e3922-125">Enter **quickstart** as a project name and choose **JavaSE-1.8** as the execution environment.</span><span class="sxs-lookup"><span data-stu-id="e3922-125">Enter **quickstart** as a project name and choose **JavaSE-1.8** as the execution environment.</span></span> <span data-ttu-id="e3922-126">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="e3922-126">Click **Finish**.</span></span>

   ![New Java Project wizard](media/sdk/qs-java-jre-03-create-java-project.png)

1. <span data-ttu-id="e3922-128">If the **Open Associated Perspective?** window appears, click **Open Perspective**.</span><span class="sxs-lookup"><span data-stu-id="e3922-128">If the **Open Associated Perspective?** window appears, click **Open Perspective**.</span></span>

1. <span data-ttu-id="e3922-129">In the **Package explorer**, right-click the **quickstart** project and choose **Configure** \> **Convert to Maven Project** from the context menu.</span><span class="sxs-lookup"><span data-stu-id="e3922-129">In the **Package explorer**, right-click the **quickstart** project and choose **Configure** \> **Convert to Maven Project** from the context menu.</span></span>

   ![Convert to Maven project](media/sdk/qs-java-jre-04-convert-to-maven-project.png)

1. <span data-ttu-id="e3922-131">The **Create New Maven POM** window appears.</span><span class="sxs-lookup"><span data-stu-id="e3922-131">The **Create New Maven POM** window appears.</span></span> <span data-ttu-id="e3922-132">Enter **com.microsoft.cognitiveservices.speech.samples** as **Group Id** and **quickstart** as **Artifact Id**. Then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="e3922-132">Enter **com.microsoft.cognitiveservices.speech.samples** as **Group Id** and **quickstart** as **Artifact Id**. Then click **Finish**.</span></span>

   ![Configure Maven POM](media/sdk/qs-java-jre-05-configure-maven-pom.png)

1. <span data-ttu-id="e3922-134">Open the **pom.xml** file and edit it.</span><span class="sxs-lookup"><span data-stu-id="e3922-134">Open the **pom.xml** file and edit it.</span></span>

  * <span data-ttu-id="e3922-135">At the end of the file, before the closing tag `</project>`, create a repositories section with a reference to the Maven repository for the Speech SDK, as shown here.</span><span class="sxs-lookup"><span data-stu-id="e3922-135">At the end of the file, before the closing tag `</project>`, create a repositories section with a reference to the Maven repository for the Speech SDK, as shown here.</span></span>

    [!code-xml[POM Repositories](~/samples-cognitive-services-speech-sdk/quickstart/java-jre/pom.xml#repositories)]

  * <span data-ttu-id="e3922-136">Also, add a dependencies section with the Speech SDK version 0.6.0.</span><span class="sxs-lookup"><span data-stu-id="e3922-136">Also, add a dependencies section with the Speech SDK version 0.6.0.</span></span>

    [!code-xml[POM Dependencies](~/samples-cognitive-services-speech-sdk/quickstart/java-jre/pom.xml#dependencies)]

  * <span data-ttu-id="e3922-137">Save the changes.</span><span class="sxs-lookup"><span data-stu-id="e3922-137">Save the changes.</span></span>

## <a name="add-sample-code"></a><span data-ttu-id="e3922-138">Add sample code</span><span class="sxs-lookup"><span data-stu-id="e3922-138">Add sample code</span></span>

1. <span data-ttu-id="e3922-139">Select **File** \> **New** \> **Class** to add a new empty class to your Java project.</span><span class="sxs-lookup"><span data-stu-id="e3922-139">Select **File** \> **New** \> **Class** to add a new empty class to your Java project.</span></span>

1. <span data-ttu-id="e3922-140">In the window **New Java Class** enter **speechsdk.quickstart** into the **Package** field, and **Main** into the **Name** field.</span><span class="sxs-lookup"><span data-stu-id="e3922-140">In the window **New Java Class** enter **speechsdk.quickstart** into the **Package** field, and **Main** into the **Name** field.</span></span>

   ![Creating a Main class](media/sdk/qs-java-jre-06-create-main-java.png)

1. <span data-ttu-id="e3922-142">Replace all code in `Main.java` with the following snippet:</span><span class="sxs-lookup"><span data-stu-id="e3922-142">Replace all code in `Main.java` with the following snippet:</span></span>

   [!code-java[Quickstart Code](~/samples-cognitive-services-speech-sdk/quickstart/java-jre/src/speechsdk/quickstart/Main.java#code)]

1. <span data-ttu-id="e3922-143">Replace the string `YourSubscriptionKey` with your subscription key.</span><span class="sxs-lookup"><span data-stu-id="e3922-143">Replace the string `YourSubscriptionKey` with your subscription key.</span></span>

1. <span data-ttu-id="e3922-144">Replace the string `YourServiceRegion` with the [region](regions.md) associated with your subscription (for example, `westus` for the free trial subscription).</span><span class="sxs-lookup"><span data-stu-id="e3922-144">Replace the string `YourServiceRegion` with the [region](regions.md) associated with your subscription (for example, `westus` for the free trial subscription).</span></span>

1. <span data-ttu-id="e3922-145">Save changes to the project.</span><span class="sxs-lookup"><span data-stu-id="e3922-145">Save changes to the project.</span></span>

## <a name="build-and-run-the-app"></a><span data-ttu-id="e3922-146">Build and run the app</span><span class="sxs-lookup"><span data-stu-id="e3922-146">Build and run the app</span></span>

<span data-ttu-id="e3922-147">Press F11, or select **Run** \> **Debug**.</span><span class="sxs-lookup"><span data-stu-id="e3922-147">Press F11, or select **Run** \> **Debug**.</span></span>
<span data-ttu-id="e3922-148">The next 15 seconds of speech input from your microphone will be recognized and logged in the console window.</span><span class="sxs-lookup"><span data-stu-id="e3922-148">The next 15 seconds of speech input from your microphone will be recognized and logged in the console window.</span></span>

![Console output after successful recognition](media/sdk/qs-java-jre-07-console-output.png)

[!INCLUDE [Download this sample](../../../includes/cognitive-services-speech-service-speech-sdk-sample-download-h2.md)]
<span data-ttu-id="e3922-150">Look for this sample in the `quickstart/java-jre` folder.</span><span class="sxs-lookup"><span data-stu-id="e3922-150">Look for this sample in the `quickstart/java-jre` folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3922-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="e3922-151">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e3922-152">Recognize intents from speech by using the Speech SDK for C#</span><span class="sxs-lookup"><span data-stu-id="e3922-152">Recognize intents from speech by using the Speech SDK for C#</span></span>](how-to-recognize-intents-from-speech-csharp.md)

## <a name="see-also"></a><span data-ttu-id="e3922-153">See also</span><span class="sxs-lookup"><span data-stu-id="e3922-153">See also</span></span>

- [<span data-ttu-id="e3922-154">Translate speech</span><span class="sxs-lookup"><span data-stu-id="e3922-154">Translate speech</span></span>](how-to-translate-speech-csharp.md)
- [<span data-ttu-id="e3922-155">Customize acoustic models</span><span class="sxs-lookup"><span data-stu-id="e3922-155">Customize acoustic models</span></span>](how-to-customize-acoustic-models.md)
- [<span data-ttu-id="e3922-156">Customize language models</span><span class="sxs-lookup"><span data-stu-id="e3922-156">Customize language models</span></span>](how-to-customize-language-model.md)
