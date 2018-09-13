---
title: Get started with Bing Speech Recognition in C# for .Net Windows | Microsoft Docs
description: Develop basic Windows applications that use the Bing Speech Recognition API to convert spoken audio to text.
services: cognitive-services
author: priyaravi20
manager: yanbo
ms.service: cognitive-services
ms.technology: speech
ms.topic: article
ms.date: 02/17/2017
ms.author: prrajan
ms.openlocfilehash: 6ebb5908e9f8f1b732a337ae243356eba854dff4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550223"
---
# <a name="getting-started-with-bing-speech-recognition-in-c35-for-net-windows"></a>Getting Started with Bing Speech Recognition in C&#35; for .Net Windows

Develop a basic Windows application that uses Bing Speech Recognition API to convert spoken audio to text by sending audio to Microsoft’s servers in the cloud. Using the Client Library allows for real-time streaming, which means that at the same time your client application sends audio to the service, it simultaneously and asynchronously receives partial recognition results back. This page describes use of the Client Library, which currently supports speech in seven languages, the example below defaults to American English, “en-US”. For client library API reference, see [Microsoft Bing Speech SDK](https://cdn.rawgit.com/Microsoft/Cognitive-Speech-STT-Windows/master/docs/SpeechSDK/index.html).

<a name="Prerequisites"></a>
## <a name="prerequisites"></a>Prerequisites
#### <a name="platform-requirements"></a>Platform Requirements
The below example has been developed for Windows 8+ and .NET Framework 4.5+ using [Visual Studio 2015, Community Edition](https://www.visualstudio.com/products/visual-studio-community-vs).
#### <a name="get-the-client-library-and-example"></a>Get the Client Library and Example
You may download the Speech API client library and example through [SDK](https://github.com/microsoft/cognitive-speech-stt-windows). The downloaded zip file needs to be extracted to a folder of your choice, many users choose the Visual Studio 2015 folder.
#### <a name="subscribe-to-speech-api-and-get-a-free-trial-subscription-key"></a>Subscribe to Speech API and Get a Free Trial Subscription Key
Before creating the example, you must subscribe to Speech API which is part of Microsoft Cognitive Services (previously Project Oxford). For subscription and key management details, see [Subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up). Both the primary and secondary key can be used in this tutorial.

<a name="Step1"></a>
## <a name="step-1-install-the-example-application"></a>Step 1: Install the Example Application
1.  Start Microsoft Visual Studio 2015 and click **File**, select **Open**, then **Project/Solution**.
2.  Browse to the folder where you saved the downloaded Speech API files. Click on **Speech**, then **Windows**, and then the **Sample-WPF** folder.
3.  Double-click to open the Visual Studio 2015 Solution (.sln) file named **SpeechToText-WPF-Samples.sln**. This will open the solution in Visual Studio.

<a name="Step2"></a>
## <a name="step-2-build-the-example-application"></a>Step 2: Build the Example Application
1.  Press Ctrl+Shift+B, or click **Build** on the ribbon menu, then select **Build Solution**.

<a name="Step3"></a>
## <a name="step-3-run-the-example-application"></a>Step 3: Run the Example Application
1.  After the build is complete, press **F5** or click **Start** on the ribbon menu to run the example.
2.  Locate the **Project Oxford Speech to Text** window with the **text edit box** reading **"Paste your subscription key here to start"**. Paste your subscription key into the text box as shown in below screenshot. You may choose to persist your subscription key on your PC or laptop by clicking the **Save Key** button. When you want to delete the subscription key from the system, click **Delete Key** to remove it from your PC or laptop.

  ![Speech Recognition paste in key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Speech/Images/SpeechRecog_paste_key.PNG)

3.  Under **Speech Recognition Source** choose one of the six speech sources, which fall into two main input categories.
  *  Using your computer’s microphone, or an attached microphone, to capture speech.
  *  Playing an audio file.

Each category has three recognition modes.
 * **ShortPhrase Mode**: An utterance up to 15 seconds long. As data is sent to the server, the client will receive multiple partial results and one final multiple N-best choice result.
 * **LongDictation Mode**: An utterance up to 2 minutes long. As data is sent to the server, the client will receive multiple partial results and multiple final results, based on where the server indicates sentence pauses.
 * **Intent Detection**: The server returns additional structured information about the speech input. To use Intent you will need to first train a model. See details [here](https://www.luis.ai/).

There are example audio files to be used with this example application. You find the files in the repository you downloaded with this example under **SpeechToText**, in the **Windows** folder, under **samples**, in the **SpeechRecognitionServiceExample** folder. These example audio files will run automatically if no other files are chosen when selecting the **Use wav file for Shortphrase mode** or **Use wav file for Longdictation mode** as your speech input. Currently only wav audio format is supported.

![Speech to Text Interface](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Speech/Images/HelloJones.PNG)

<a name="Review"></a>
## <a name="review-and-learn"></a>Review and Learn

### <a name="events"></a>Events
#### <a name="partial-results-event"></a>Partial Results Event:
This event gets called every time the Speech Recognition Server has an idea of what the speaker might be saying – even before he or she has finished speaking (if you are using the Microphone Client) or have finished transferring data (if you are using the Data Client).
#### <a name="intent-event"></a>Intent Event:
Called on WithIntent clients (only in ShortPhrase mode) after the final reco result has been parsed into structured JSON intent.
#### <a name="result-event"></a>Result Event:
When you have finished speaking (in ShortPhrase mode), this event is called. You will be provided with n-best choices for the result. In LongDictation mode, the handler associated with this event will be called multiple times, based on where the server thinks sentence pauses are.

Eventhandlers are already pointed out in the code in form of code comments.

 **Return Format** |  Description |
 ------|------
 **LexicalForm** |  This form is optimal for use by applications that need raw, unprocessed speech recognition results.
 **DisplayText**  |  The recognized phrase with inverse text normalization, capitalization, punctuation and profanity masking applied. Profanity is masked with asterisks after the initial character, e.g. "d***". This form is optimal for use by applications that display the speech recognition results to a user.
**Inverse Text Normalization (ITN) has been applied**  |  An example of ITN is converting result text from "go to fourth street" to "go to 4th st". This form is optimal for use by applications that display the speech recognition results to a user.
**InverseTextNormalizationResult**  | Inverse text normalization (ITN) converts phrases like "one two three four" to a normalized form such as "1234". Another example is converting result text from "go to fourth street" to "go to 4th st". This form is optimal for use by applications that interpret the speech recognition results as commands or perform queries based on the recognized text.
**MaskedInverseTextNormalizationResult**  |  The recognized phrase with inverse text normalization and profanity masking applied, but no capitalization or punctuation. Profanity is masked with asterisks after the initial character, e.g. "d***". This form is optimal for use by applications that display the speech recognition results to a user. Inverse Text Normalization (ITN) has also been applied. An example of ITN is converting result text from "go to fourth street" to "go to 4th st". This form is optimal for use by applications that use the unmasked ITN results but also need to display the command or query to the user.

<a name="RelatedTopics"></a>
## <a name="related-topics"></a>Related Topics
* [Get started with Bing Speech Recognition and/or intent in Java on Android](GetStartedJavaAndroid.md)
* [Get started with Bing Speech Recognition and/or intent in Objective C on iOS](Get-Started-ObjectiveC-iOS.md)
* [Get started with Bing Speech API in JavaScript](GetStartedJS.md)
* [Get started with Bing Speech API in cURL](GetStarted-cURL.md)


