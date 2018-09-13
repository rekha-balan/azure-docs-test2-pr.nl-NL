---
title: 'Quickstart: Recognize speech in Java on Android using the Cognitive Services Speech SDK'
titleSuffix: Microsoft Cognitive Services
description: Learn how to recognize speech in Java on Android using the Cognitive Services Speech SDK
services: cognitive-services
author: fmegen
ms.service: cognitive-services
ms.technology: Speech
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: fmegen
ms.openlocfilehash: f899ad33228565650e2c6e7766ac7d2d1636bd09
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856115"
---
# <a name="quickstart-recognize-speech-in-java-on-android-using-the-speech-sdk"></a><span data-ttu-id="5ce8a-103">Quickstart: Recognize speech in Java on Android using the Speech SDK</span><span class="sxs-lookup"><span data-stu-id="5ce8a-103">Quickstart: Recognize speech in Java on Android using the Speech SDK</span></span>

[!INCLUDE [Selector](../../../includes/cognitive-services-speech-service-quickstart-selector.md)]

<span data-ttu-id="5ce8a-104">In this article, you create a Java application for Android 6.0 Marshmallow (API 23) or later using the Cognitive Services [Speech SDK](speech-sdk.md) to transcribe speech to text in real time from your device's microphone.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-104">In this article, you create a Java application for Android 6.0 Marshmallow (API 23) or later using the Cognitive Services [Speech SDK](speech-sdk.md) to transcribe speech to text in real time from your device's microphone.</span></span> <span data-ttu-id="5ce8a-105">The application is built with the Speech SDK Maven package and [Android Studio](https://developer.android.com/studio/) 3.1 running on a PC.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-105">The application is built with the Speech SDK Maven package and [Android Studio](https://developer.android.com/studio/) 3.1 running on a PC.</span></span> <span data-ttu-id="5ce8a-106">The Speech SDK libraries are currently compatible with Android devices having 64-bit ARM processors.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-106">The Speech SDK libraries are currently compatible with Android devices having 64-bit ARM processors.</span></span>

> [!NOTE]
> <span data-ttu-id="5ce8a-107">For the Speech Devices SDK and the Roobo device, see [Speech Devices SDK](speech-devices-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="5ce8a-107">For the Speech Devices SDK and the Roobo device, see [Speech Devices SDK](speech-devices-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ce8a-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5ce8a-108">Prerequisites</span></span>

<span data-ttu-id="5ce8a-109">You need a Speech service subscription key to complete this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-109">You need a Speech service subscription key to complete this Quickstart.</span></span> <span data-ttu-id="5ce8a-110">You can get one for free.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-110">You can get one for free.</span></span> <span data-ttu-id="5ce8a-111">See [Try the speech service for free](get-started.md) for details.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-111">See [Try the speech service for free](get-started.md) for details.</span></span>

## <a name="create-and-configure-project"></a><span data-ttu-id="5ce8a-112">Create and configure project</span><span class="sxs-lookup"><span data-stu-id="5ce8a-112">Create and configure project</span></span>

1. <span data-ttu-id="5ce8a-113">Launch Android Studio and choose **Start a new Android Studio project** in the Welcome window.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-113">Launch Android Studio and choose **Start a new Android Studio project** in the Welcome window.</span></span>

    ![](media/sdk/qs-java-android-01-start-new-android-studio-project.png)

1. <span data-ttu-id="5ce8a-114">The **Create New Project** wizard appears.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-114">The **Create New Project** wizard appears.</span></span> <span data-ttu-id="5ce8a-115">FIn the **Create Android Project** screen, enter **Quickstart** as **application name**, **samples.speech.cognitiveservices.microsoft.com** as **company domain**, and choose a project directory.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-115">FIn the **Create Android Project** screen, enter **Quickstart** as **application name**, **samples.speech.cognitiveservices.microsoft.com** as **company domain**, and choose a project directory.</span></span> <span data-ttu-id="5ce8a-116">Leave the C++ and Kotlin checkboxes unchecked, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-116">Leave the C++ and Kotlin checkboxes unchecked, and click **Next**.</span></span>

   ![](media/sdk/qs-java-android-02-create-android-project.png)

1. <span data-ttu-id="5ce8a-117">In the **Target Android Devices** screen, mark only **Phone and Tablet**, choose **API 23: Android 6.0 (Marshmallow)** from the drop-down below it, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-117">In the **Target Android Devices** screen, mark only **Phone and Tablet**, choose **API 23: Android 6.0 (Marshmallow)** from the drop-down below it, and click **Next**.</span></span>

   ![](media/sdk/qs-java-android-03-target-android-devices.png)

1. <span data-ttu-id="5ce8a-118">In the **Add an Activity to Mobile** screen, select **Empty Activity**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-118">In the **Add an Activity to Mobile** screen, select **Empty Activity**, and click **Next**.</span></span>

   ![](media/sdk/qs-java-android-04-add-an-activity-to-mobile.png)

1. <span data-ttu-id="5ce8a-119">In the **Configure Activity** screen, use **MainActivity** as the Activity Name and **activity\_main** as the Layout Name.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-119">In the **Configure Activity** screen, use **MainActivity** as the Activity Name and **activity\_main** as the Layout Name.</span></span> <span data-ttu-id="5ce8a-120">Mark both checkboxes and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-120">Mark both checkboxes and click **Finish**.</span></span>

   ![](media/sdk/qs-java-android-05-configure-activity.png)

<span data-ttu-id="5ce8a-121">Android Studio takes a moment to prepare your new Android project.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-121">Android Studio takes a moment to prepare your new Android project.</span></span> <span data-ttu-id="5ce8a-122">Next, configure the project to know about the Speech SDK and to use Java 8.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-122">Next, configure the project to know about the Speech SDK and to use Java 8.</span></span>

[!INCLUDE [License Notice](../../../includes/cognitive-services-speech-service-license-notice.md)]

<span data-ttu-id="5ce8a-123">The Speech SDK for Android is packaged as an [AAR (Android Library)](https://developer.android.com/studio/projects/android-library), which includes the necessary libraries and the Android permissions needed to use it.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-123">The Speech SDK for Android is packaged as an [AAR (Android Library)](https://developer.android.com/studio/projects/android-library), which includes the necessary libraries and the Android permissions needed to use it.</span></span> <span data-ttu-id="5ce8a-124">It is hosted in a Maven repository and so is automatically downloaded by Android Studio for use in your application.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-124">It is hosted in a Maven repository and so is automatically downloaded by Android Studio for use in your application.</span></span>

<span data-ttu-id="5ce8a-125">To set up your project to use the Speech SDK, open the Project Structure window by choosing **File** \> **Project Structure** from the Android Studio menu bar.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-125">To set up your project to use the Speech SDK, open the Project Structure window by choosing **File** \> **Project Structure** from the Android Studio menu bar.</span></span>
<span data-ttu-id="5ce8a-126">In the Project Structure window, make the following changes.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-126">In the Project Structure window, make the following changes.</span></span> 

1. <span data-ttu-id="5ce8a-127">Select **Project** in the list on the left side of the window and edit the **Default Library Repository** settings by appending a comma and our Maven repository URL enclosed in single quotes.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-127">Select **Project** in the list on the left side of the window and edit the **Default Library Repository** settings by appending a comma and our Maven repository URL enclosed in single quotes.</span></span> <span data-ttu-id="5ce8a-128">'https://csspeechstorage.blob.core.windows.net/maven/'</span><span class="sxs-lookup"><span data-stu-id="5ce8a-128">'https://csspeechstorage.blob.core.windows.net/maven/'</span></span>

   ![](media/sdk/qs-java-android-06-add-maven-repository.png)

1. <span data-ttu-id="5ce8a-129">Still in the same screen, on the left side, select **App**, then click the **Dependencies** tab at the top of the window.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-129">Still in the same screen, on the left side, select **App**, then click the **Dependencies** tab at the top of the window.</span></span> <span data-ttu-id="5ce8a-130">Click the green Plus sign in the right upper corner and choose **Library dependency** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-130">Click the green Plus sign in the right upper corner and choose **Library dependency** from the drop-down menu.</span></span>

   ![](media/sdk/qs-java-android-07-add-module-dependency.png)

1. <span data-ttu-id="5ce8a-131">In the window that appears, enter the name and version of the Speech SDK for Android in the expected format, `com.microsoft.cognitiveservices.speech:client-sdk:0.6.0`, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-131">In the window that appears, enter the name and version of the Speech SDK for Android in the expected format, `com.microsoft.cognitiveservices.speech:client-sdk:0.6.0`, then click **OK**.</span></span> <span data-ttu-id="5ce8a-132">The Speech SDK is added to the list of dependencies now, as shown here.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-132">The Speech SDK is added to the list of dependencies now, as shown here.</span></span>

   ![](media/sdk/qs-java-android-08-dependency-added.png)

1. <span data-ttu-id="5ce8a-133">Click the **Properties** tab. Select **1.8** both for **Source Compatibility** and **Target Compatibility**.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-133">Click the **Properties** tab. Select **1.8** both for **Source Compatibility** and **Target Compatibility**.</span></span>

   ![](media/sdk/qs-java-android-09-dependency-added.png)

1. <span data-ttu-id="5ce8a-134">Finally, click **OK** to close the Project Structure window and apply your changes to the project.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-134">Finally, click **OK** to close the Project Structure window and apply your changes to the project.</span></span>

## <a name="create-user-interface"></a><span data-ttu-id="5ce8a-135">Create user interface</span><span class="sxs-lookup"><span data-stu-id="5ce8a-135">Create user interface</span></span>

<span data-ttu-id="5ce8a-136">We will create a basic user interface for the application.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-136">We will create a basic user interface for the application.</span></span> <span data-ttu-id="5ce8a-137">Edit the layout for your main activity, `activity_main.xml`.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-137">Edit the layout for your main activity, `activity_main.xml`.</span></span> <span data-ttu-id="5ce8a-138">Initially, the layout includes a title bar with your application's name and a TextView containing the text "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="5ce8a-138">Initially, the layout includes a title bar with your application's name and a TextView containing the text "Hello World!"</span></span>

* <span data-ttu-id="5ce8a-139">Click the TextView element.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-139">Click the TextView element.</span></span> <span data-ttu-id="5ce8a-140">Change its ID attribute in the upper-right corner to `hello`.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-140">Change its ID attribute in the upper-right corner to `hello`.</span></span>

* <span data-ttu-id="5ce8a-141">From the Palette in the upper left of the `activity_main.xml` window, drag a Button into the empty space above the text.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-141">From the Palette in the upper left of the `activity_main.xml` window, drag a Button into the empty space above the text.</span></span>

* <span data-ttu-id="5ce8a-142">In the button's attributes on the right, in the value for the `onClick` attribute, enter `onSpeechButtonClicked`.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-142">In the button's attributes on the right, in the value for the `onClick` attribute, enter `onSpeechButtonClicked`.</span></span> <span data-ttu-id="5ce8a-143">We'll write a method with this name to handle the button event.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-143">We'll write a method with this name to handle the button event.</span></span>  <span data-ttu-id="5ce8a-144">Change its ID attribute in the upper-right corner to `button`.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-144">Change its ID attribute in the upper-right corner to `button`.</span></span>

* <span data-ttu-id="5ce8a-145">Use the magic wand icon at the top of the designer if to infer layout constraints.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-145">Use the magic wand icon at the top of the designer if to infer layout constraints.</span></span>

  ![](media/sdk/qs-java-android-10-infer-layout-constraints.png)

<span data-ttu-id="5ce8a-146">The text and graphical representation of your UI should now look like this.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-146">The text and graphical representation of your UI should now look like this.</span></span>

<table>
<tr>
<td valign="top">
![](media/sdk/qs-java-android-11-gui.png)
</td>
<td valign="top">
<span data-ttu-id="5ce8a-147">[!code-xml[](~/samples-cognitive-services-speech-sdk/quickstart/java-android/app/src/main/res/layout/activity_main.xml)]</span><span class="sxs-lookup"><span data-stu-id="5ce8a-147">[!code-xml[](~/samples-cognitive-services-speech-sdk/quickstart/java-android/app/src/main/res/layout/activity_main.xml)]</span></span>
</td>
</tr>
</table>

## <a name="add-sample-code"></a><span data-ttu-id="5ce8a-148">Add sample code</span><span class="sxs-lookup"><span data-stu-id="5ce8a-148">Add sample code</span></span>

1. <span data-ttu-id="5ce8a-149">Open the source file `MainActivity.java`.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-149">Open the source file `MainActivity.java`.</span></span> <span data-ttu-id="5ce8a-150">Replace all the code following the `package` statement with the following.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-150">Replace all the code following the `package` statement with the following.</span></span>

   [!code-java[](~/samples-cognitive-services-speech-sdk/quickstart/java-android/app/src/main/java/com/microsoft/cognitiveservices/speech/samples/quickstart/MainActivity.java#code)]

   * <span data-ttu-id="5ce8a-151">The `onCreate` method includes code that requests microphone and Internet permissions and initializes the native platform binding.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-151">The `onCreate` method includes code that requests microphone and Internet permissions and initializes the native platform binding.</span></span> <span data-ttu-id="5ce8a-152">Configuring the native platform bindings is only required once, that is, it should be done early during application initialization.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-152">Configuring the native platform bindings is only required once, that is, it should be done early during application initialization.</span></span>
   
   * <span data-ttu-id="5ce8a-153">The method `onSpeechButtonClicked` is, as noted earlier, the button click handler.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-153">The method `onSpeechButtonClicked` is, as noted earlier, the button click handler.</span></span> <span data-ttu-id="5ce8a-154">A button press triggers speech-to-text transcription.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-154">A button press triggers speech-to-text transcription.</span></span>

1. <span data-ttu-id="5ce8a-155">In the same file, replace the string `YourSubscriptionKey` with your subscription key.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-155">In the same file, replace the string `YourSubscriptionKey` with your subscription key.</span></span>

1. <span data-ttu-id="5ce8a-156">Also replace the string `YourServiceRegion` with the [region](regions.md) associated with your subscription (for example, `westus` for the free trial subscription).</span><span class="sxs-lookup"><span data-stu-id="5ce8a-156">Also replace the string `YourServiceRegion` with the [region](regions.md) associated with your subscription (for example, `westus` for the free trial subscription).</span></span>

## <a name="build-and-run-the-app"></a><span data-ttu-id="5ce8a-157">Build and run the app</span><span class="sxs-lookup"><span data-stu-id="5ce8a-157">Build and run the app</span></span>

1. <span data-ttu-id="5ce8a-158">Connect your Android device to your development PC.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-158">Connect your Android device to your development PC.</span></span> <span data-ttu-id="5ce8a-159">Make sure you have enabled [development mode and USB debugging](https://developer.android.com/studio/debug/dev-options) on the device.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-159">Make sure you have enabled [development mode and USB debugging](https://developer.android.com/studio/debug/dev-options) on the device.</span></span>

1. <span data-ttu-id="5ce8a-160">To build the application, press Ctrl+F9, or choose **Build** \> **Make Project** from the menu bar.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-160">To build the application, press Ctrl+F9, or choose **Build** \> **Make Project** from the menu bar.</span></span>

1. <span data-ttu-id="5ce8a-161">To launch the application, press Shift+F10, or choose **Run** \> **Run 'app'**.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-161">To launch the application, press Shift+F10, or choose **Run** \> **Run 'app'**.</span></span>

1. <span data-ttu-id="5ce8a-162">In the deployment target window that appears, choose your Android device.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-162">In the deployment target window that appears, choose your Android device.</span></span>

   ![Launch the app into debugging](media/sdk/qs-java-android-12-deploy.png)

<span data-ttu-id="5ce8a-164">Press the button in the application to begin a speech recognition section.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-164">Press the button in the application to begin a speech recognition section.</span></span> <span data-ttu-id="5ce8a-165">The next 15 seconds of English speech will be sent to the Speech service and transcribed.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-165">The next 15 seconds of English speech will be sent to the Speech service and transcribed.</span></span> <span data-ttu-id="5ce8a-166">The result appears in the Android application and in the logcat window in Android Studio.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-166">The result appears in the Android application and in the logcat window in Android Studio.</span></span>

![UI after successful recognition](media/sdk/qs-java-android-13-gui-on-device.png)

[!INCLUDE [Download this sample](../../../includes/cognitive-services-speech-service-speech-sdk-sample-download-h2.md)]
<span data-ttu-id="5ce8a-168">Look for this sample in the `quickstart/java-android` folder.</span><span class="sxs-lookup"><span data-stu-id="5ce8a-168">Look for this sample in the `quickstart/java-android` folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ce8a-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="5ce8a-169">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5ce8a-170">Recognize intents from speech by using the Speech SDK for C#</span><span class="sxs-lookup"><span data-stu-id="5ce8a-170">Recognize intents from speech by using the Speech SDK for C#</span></span>](how-to-recognize-intents-from-speech-csharp.md)

## <a name="see-also"></a><span data-ttu-id="5ce8a-171">See also</span><span class="sxs-lookup"><span data-stu-id="5ce8a-171">See also</span></span>

- [<span data-ttu-id="5ce8a-172">Translate speech</span><span class="sxs-lookup"><span data-stu-id="5ce8a-172">Translate speech</span></span>](how-to-translate-speech-csharp.md)
- [<span data-ttu-id="5ce8a-173">Customize acoustic models</span><span class="sxs-lookup"><span data-stu-id="5ce8a-173">Customize acoustic models</span></span>](how-to-customize-acoustic-models.md)
- [<span data-ttu-id="5ce8a-174">Customize language models</span><span class="sxs-lookup"><span data-stu-id="5ce8a-174">Customize language models</span></span>](how-to-customize-language-model.md)
