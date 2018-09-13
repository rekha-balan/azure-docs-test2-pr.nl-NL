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
# <a name="quickstart-recognize-speech-in-java-on-android-using-the-speech-sdk"></a>Quickstart: Recognize speech in Java on Android using the Speech SDK

[!INCLUDE [Selector](../../../includes/cognitive-services-speech-service-quickstart-selector.md)]

In this article, you create a Java application for Android 6.0 Marshmallow (API 23) or later using the Cognitive Services [Speech SDK](speech-sdk.md) to transcribe speech to text in real time from your device's microphone. The application is built with the Speech SDK Maven package and [Android Studio](https://developer.android.com/studio/) 3.1 running on a PC. The Speech SDK libraries are currently compatible with Android devices having 64-bit ARM processors.

> [!NOTE]
> For the Speech Devices SDK and the Roobo device, see [Speech Devices SDK](speech-devices-sdk.md).

## <a name="prerequisites"></a>Prerequisites

You need a Speech service subscription key to complete this Quickstart. You can get one for free. See [Try the speech service for free](get-started.md) for details.

## <a name="create-and-configure-project"></a>Create and configure project

1. Launch Android Studio and choose **Start a new Android Studio project** in the Welcome window.

    ![](media/sdk/qs-java-android-01-start-new-android-studio-project.png)

1. The **Create New Project** wizard appears. FIn the **Create Android Project** screen, enter **Quickstart** as **application name**, **samples.speech.cognitiveservices.microsoft.com** as **company domain**, and choose a project directory. Leave the C++ and Kotlin checkboxes unchecked, and click **Next**.

   ![](media/sdk/qs-java-android-02-create-android-project.png)

1. In the **Target Android Devices** screen, mark only **Phone and Tablet**, choose **API 23: Android 6.0 (Marshmallow)** from the drop-down below it, and click **Next**.

   ![](media/sdk/qs-java-android-03-target-android-devices.png)

1. In the **Add an Activity to Mobile** screen, select **Empty Activity**, and click **Next**.

   ![](media/sdk/qs-java-android-04-add-an-activity-to-mobile.png)

1. In the **Configure Activity** screen, use **MainActivity** as the Activity Name and **activity\_main** as the Layout Name. Mark both checkboxes and click **Finish**.

   ![](media/sdk/qs-java-android-05-configure-activity.png)

Android Studio takes a moment to prepare your new Android project. Next, configure the project to know about the Speech SDK and to use Java 8.

[!INCLUDE [License Notice](../../../includes/cognitive-services-speech-service-license-notice.md)]

The Speech SDK for Android is packaged as an [AAR (Android Library)](https://developer.android.com/studio/projects/android-library), which includes the necessary libraries and the Android permissions needed to use it. It is hosted in a Maven repository and so is automatically downloaded by Android Studio for use in your application.

To set up your project to use the Speech SDK, open the Project Structure window by choosing **File** \> **Project Structure** from the Android Studio menu bar.
In the Project Structure window, make the following changes. 

1. Select **Project** in the list on the left side of the window and edit the **Default Library Repository** settings by appending a comma and our Maven repository URL enclosed in single quotes. 'https://csspeechstorage.blob.core.windows.net/maven/'

   ![](media/sdk/qs-java-android-06-add-maven-repository.png)

1. Still in the same screen, on the left side, select **App**, then click the **Dependencies** tab at the top of the window. Click the green Plus sign in the right upper corner and choose **Library dependency** from the drop-down menu.

   ![](media/sdk/qs-java-android-07-add-module-dependency.png)

1. In the window that appears, enter the name and version of the Speech SDK for Android in the expected format, `com.microsoft.cognitiveservices.speech:client-sdk:0.6.0`, then click **OK**. The Speech SDK is added to the list of dependencies now, as shown here.

   ![](media/sdk/qs-java-android-08-dependency-added.png)

1. Click the **Properties** tab. Select **1.8** both for **Source Compatibility** and **Target Compatibility**.

   ![](media/sdk/qs-java-android-09-dependency-added.png)

1. Finally, click **OK** to close the Project Structure window and apply your changes to the project.

## <a name="create-user-interface"></a>Create user interface

We will create a basic user interface for the application. Edit the layout for your main activity, `activity_main.xml`. Initially, the layout includes a title bar with your application's name and a TextView containing the text "Hello World!"

* Click the TextView element. Change its ID attribute in the upper-right corner to `hello`.

* From the Palette in the upper left of the `activity_main.xml` window, drag a Button into the empty space above the text.

* In the button's attributes on the right, in the value for the `onClick` attribute, enter `onSpeechButtonClicked`. We'll write a method with this name to handle the button event.  Change its ID attribute in the upper-right corner to `button`.

* Use the magic wand icon at the top of the designer if to infer layout constraints.

  ![](media/sdk/qs-java-android-10-infer-layout-constraints.png)

The text and graphical representation of your UI should now look like this.

<table>
<tr>
<td valign="top">
![](media/sdk/qs-java-android-11-gui.png)
</td>
<td valign="top">
[!code-xml[](~/samples-cognitive-services-speech-sdk/quickstart/java-android/app/src/main/res/layout/activity_main.xml)]
</td>
</tr>
</table>

## <a name="add-sample-code"></a>Add sample code

1. Open the source file `MainActivity.java`. Replace all the code following the `package` statement with the following.

   [!code-java[](~/samples-cognitive-services-speech-sdk/quickstart/java-android/app/src/main/java/com/microsoft/cognitiveservices/speech/samples/quickstart/MainActivity.java#code)]

   * The `onCreate` method includes code that requests microphone and Internet permissions and initializes the native platform binding. Configuring the native platform bindings is only required once, that is, it should be done early during application initialization.
   
   * The method `onSpeechButtonClicked` is, as noted earlier, the button click handler. A button press triggers speech-to-text transcription.

1. In the same file, replace the string `YourSubscriptionKey` with your subscription key.

1. Also replace the string `YourServiceRegion` with the [region](regions.md) associated with your subscription (for example, `westus` for the free trial subscription).

## <a name="build-and-run-the-app"></a>Build and run the app

1. Connect your Android device to your development PC. Make sure you have enabled [development mode and USB debugging](https://developer.android.com/studio/debug/dev-options) on the device.

1. To build the application, press Ctrl+F9, or choose **Build** \> **Make Project** from the menu bar.

1. To launch the application, press Shift+F10, or choose **Run** \> **Run 'app'**.

1. In the deployment target window that appears, choose your Android device.

   ![Launch the app into debugging](media/sdk/qs-java-android-12-deploy.png)

Press the button in the application to begin a speech recognition section. The next 15 seconds of English speech will be sent to the Speech service and transcribed. The result appears in the Android application and in the logcat window in Android Studio.

![UI after successful recognition](media/sdk/qs-java-android-13-gui-on-device.png)

[!INCLUDE [Download this sample](../../../includes/cognitive-services-speech-service-speech-sdk-sample-download-h2.md)]
Look for this sample in the `quickstart/java-android` folder.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Recognize intents from speech by using the Speech SDK for C#](how-to-recognize-intents-from-speech-csharp.md)

## <a name="see-also"></a>See also

- [Translate speech](how-to-translate-speech-csharp.md)
- [Customize acoustic models](how-to-customize-acoustic-models.md)
- [Customize language models](how-to-customize-language-model.md)
