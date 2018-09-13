---
title: Translator Speech Tutorial (C#) | Microsoft Docs
titleSuffix: Cognitive Services
description: Learn how to use the Translator speech service to translate text in real time.
services: cognitive-services
author: v-jerkin
manager: chriswendt1
ms.service: cognitive-services
ms.component: translator-speech
ms.devlang: csharp
ms.topic: article
ms.date: 3/5/2018
ms.author: v-jerkin
ms.openlocfilehash: 00e1abee404071a5d519762ccc0ae43486d4249e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857891"
---
# <a name="tutorial-microsoft-translator-wpf-application-in-c"></a><span data-ttu-id="fe4d7-103">Tutorial: Microsoft Translator WPF application in C#</span><span class="sxs-lookup"><span data-stu-id="fe4d7-103">Tutorial: Microsoft Translator WPF application in C#</span></span>

<span data-ttu-id="fe4d7-104">This tutorial is a tour of an interactive speech translation tool that uses the Microsoft Translator Speech translation service, a part of Microsoft Cognitive Services in Azure.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-104">This tutorial is a tour of an interactive speech translation tool that uses the Microsoft Translator Speech translation service, a part of Microsoft Cognitive Services in Azure.</span></span> <span data-ttu-id="fe4d7-105">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="fe4d7-105">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fe4d7-106">Request a list of the languages supported by the service</span><span class="sxs-lookup"><span data-stu-id="fe4d7-106">Request a list of the languages supported by the service</span></span>
> * <span data-ttu-id="fe4d7-107">Capture audio and transmit it to the service</span><span class="sxs-lookup"><span data-stu-id="fe4d7-107">Capture audio and transmit it to the service</span></span>
> * <span data-ttu-id="fe4d7-108">Receive and display translations of the speech as text</span><span class="sxs-lookup"><span data-stu-id="fe4d7-108">Receive and display translations of the speech as text</span></span>
> * <span data-ttu-id="fe4d7-109">Optionally play a spoken (text-to-speech) version of the translation</span><span class="sxs-lookup"><span data-stu-id="fe4d7-109">Optionally play a spoken (text-to-speech) version of the translation</span></span>

<span data-ttu-id="fe4d7-110">A Visual Studio solution file for this application is [available on GitHub](https://github.com/MicrosoftTranslator/SpeechTranslator).</span><span class="sxs-lookup"><span data-stu-id="fe4d7-110">A Visual Studio solution file for this application is [available on GitHub](https://github.com/MicrosoftTranslator/SpeechTranslator).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe4d7-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fe4d7-111">Prerequisites</span></span>

<span data-ttu-id="fe4d7-112">For this tutorial, you need any edition of Visual Studio 2017, including the Community Edition.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-112">For this tutorial, you need any edition of Visual Studio 2017, including the Community Edition.</span></span> 

<span data-ttu-id="fe4d7-113">The Visual Studio solution also builds an installer for the application.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-113">The Visual Studio solution also builds an installer for the application.</span></span> <span data-ttu-id="fe4d7-114">You need the [WiX Toolset](http://wixtoolset.org/) and the [WiX Toolset Visual Studio Extension](https://marketplace.visualstudio.com/items?itemName=RobMensching.WixToolsetVisualStudio2017Extension) to support this functionality.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-114">You need the [WiX Toolset](http://wixtoolset.org/) and the [WiX Toolset Visual Studio Extension](https://marketplace.visualstudio.com/items?itemName=RobMensching.WixToolsetVisualStudio2017Extension) to support this functionality.</span></span>

<span data-ttu-id="fe4d7-115">You also need a subscription key for the Translator Speech service, which you can obtain from the Microsoft Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-115">You also need a subscription key for the Translator Speech service, which you can obtain from the Microsoft Azure dashboard.</span></span> <span data-ttu-id="fe4d7-116">A free pricing tier is available that allows you to translate up to 10 hours of speech per month at no charge.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-116">A free pricing tier is available that allows you to translate up to 10 hours of speech per month at no charge.</span></span> <span data-ttu-id="fe4d7-117">This tier is sufficient for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-117">This tier is sufficient for this tutorial.</span></span>

<span data-ttu-id="fe4d7-118">The third-party [JSON.Net library](https://www.newtonsoft.com/json) (from Newtonsoft) is also required.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-118">The third-party [JSON.Net library](https://www.newtonsoft.com/json) (from Newtonsoft) is also required.</span></span> <span data-ttu-id="fe4d7-119">This assembly is automatically installed by NuGet if both Package Restore checkboxes are enabled in the Visual Studio options.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-119">This assembly is automatically installed by NuGet if both Package Restore checkboxes are enabled in the Visual Studio options.</span></span>

## <a name="trying-the-translation-app"></a><span data-ttu-id="fe4d7-120">Trying the translation app</span><span class="sxs-lookup"><span data-stu-id="fe4d7-120">Trying the translation app</span></span>

<span data-ttu-id="fe4d7-121">After opening the Microsoft Speech Translator solution (`SpeechTranslator.sln`) in Visual STudio, press F5 to build and launch the application.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-121">After opening the Microsoft Speech Translator solution (`SpeechTranslator.sln`) in Visual STudio, press F5 to build and launch the application.</span></span>  <span data-ttu-id="fe4d7-122">The program's main window appears.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-122">The program's main window appears.</span></span>

![[Speech Translator main window]](media/speech-translator-main-window.png)

<span data-ttu-id="fe4d7-124">On the first run, choose **Account Settings** from the **Settings** menu to open the window shown here.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-124">On the first run, choose **Account Settings** from the **Settings** menu to open the window shown here.</span></span>

![[Speech Translator main window]](media/speech-translator-settings-window.png)

<span data-ttu-id="fe4d7-126">Paste your Microsoft Translator Speech subscription key in this window, then click **Save.**</span><span class="sxs-lookup"><span data-stu-id="fe4d7-126">Paste your Microsoft Translator Speech subscription key in this window, then click **Save.**</span></span> <span data-ttu-id="fe4d7-127">Your key is saved between runs.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-127">Your key is saved between runs.</span></span>

<span data-ttu-id="fe4d7-128">Back in the main window, choose the audio input and output devices you want to use and the From and To languages.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-128">Back in the main window, choose the audio input and output devices you want to use and the From and To languages.</span></span> <span data-ttu-id="fe4d7-129">If you want to hear audio of the translation, make sure the **TTS** (text-to-speech) option is checked.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-129">If you want to hear audio of the translation, make sure the **TTS** (text-to-speech) option is checked.</span></span> <span data-ttu-id="fe4d7-130">If you want to see speculative partial translations as you speak, enable the **Partial Results** option.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-130">If you want to see speculative partial translations as you speak, enable the **Partial Results** option.</span></span>

<span data-ttu-id="fe4d7-131">Finally, click **Start** to begin translation.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-131">Finally, click **Start** to begin translation.</span></span> <span data-ttu-id="fe4d7-132">Say something you wish to have translated and watch the recognized text and the translation appear in the window.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-132">Say something you wish to have translated and watch the recognized text and the translation appear in the window.</span></span> <span data-ttu-id="fe4d7-133">If you enabled the TTS option, you also hear the translation.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-133">If you enabled the TTS option, you also hear the translation.</span></span>

## <a name="obtaining-supported-languages"></a><span data-ttu-id="fe4d7-134">Obtaining supported languages</span><span class="sxs-lookup"><span data-stu-id="fe4d7-134">Obtaining supported languages</span></span>

<span data-ttu-id="fe4d7-135">At this writing, the Microsoft Translator service supports more than five dozen languages for text translation.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-135">At this writing, the Microsoft Translator service supports more than five dozen languages for text translation.</span></span> <span data-ttu-id="fe4d7-136">A smaller number of languages are supported for speech translation.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-136">A smaller number of languages are supported for speech translation.</span></span> <span data-ttu-id="fe4d7-137">Such languages require support for both transcription (speech recognition) and, for text-to-speech output, synthesis.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-137">Such languages require support for both transcription (speech recognition) and, for text-to-speech output, synthesis.</span></span>

<span data-ttu-id="fe4d7-138">In other words, for speech translation, the source language must be one supported for transcription.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-138">In other words, for speech translation, the source language must be one supported for transcription.</span></span> <span data-ttu-id="fe4d7-139">The output language may be any of the languages supported for text translation, assuming you want a text result.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-139">The output language may be any of the languages supported for text translation, assuming you want a text result.</span></span> <span data-ttu-id="fe4d7-140">If you want speech output, you can only translate into a language supported for text-to-speech.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-140">If you want speech output, you can only translate into a language supported for text-to-speech.</span></span>

<span data-ttu-id="fe4d7-141">Microsoft may add support for new languages from time to time.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-141">Microsoft may add support for new languages from time to time.</span></span> <span data-ttu-id="fe4d7-142">For this reason, you should not hard-code any knowledge of supported languages in your application.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-142">For this reason, you should not hard-code any knowledge of supported languages in your application.</span></span> <span data-ttu-id="fe4d7-143">Instead, the Translator Speech API provides a Languages endpoint that allows you to retrieve the supported languages at runtime.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-143">Instead, the Translator Speech API provides a Languages endpoint that allows you to retrieve the supported languages at runtime.</span></span> <span data-ttu-id="fe4d7-144">You can choose to receive one or more lists of languages:</span><span class="sxs-lookup"><span data-stu-id="fe4d7-144">You can choose to receive one or more lists of languages:</span></span> 

| | |
|-|-|
|`speech`|<span data-ttu-id="fe4d7-145">The languages supported for speech transcription.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-145">The languages supported for speech transcription.</span></span> <span data-ttu-id="fe4d7-146">Can be source languages for speech translation.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-146">Can be source languages for speech translation.</span></span>|
|`text`|<span data-ttu-id="fe4d7-147">The languages supported for text-to-text translation.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-147">The languages supported for text-to-text translation.</span></span> <span data-ttu-id="fe4d7-148">Can be target languages for speech translation when text output is used.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-148">Can be target languages for speech translation when text output is used.</span></span>|
|`tts`|<span data-ttu-id="fe4d7-149">The voices supported for speech synthesis, each associated with a particular language.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-149">The voices supported for speech synthesis, each associated with a particular language.</span></span> <span data-ttu-id="fe4d7-150">Can be target languages for speech translation when text-to-speech is used.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-150">Can be target languages for speech translation when text-to-speech is used.</span></span> <span data-ttu-id="fe4d7-151">A given language may be supported by more than one voice.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-151">A given language may be supported by more than one voice.</span></span>|

<span data-ttu-id="fe4d7-152">The Languages endpoint does not require a subscription key, and its usage does not count against your quota.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-152">The Languages endpoint does not require a subscription key, and its usage does not count against your quota.</span></span> <span data-ttu-id="fe4d7-153">Its URI is `https://dev.microsofttranslator.com/languages` and it returns its results in JSON format.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-153">Its URI is `https://dev.microsofttranslator.com/languages` and it returns its results in JSON format.</span></span>

<span data-ttu-id="fe4d7-154">The method `UpdateLanguageSettingsAsync()` in `MainWindow.xaml.cs`, shown here, calls the Languages endpoint to get the list of supported languages.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-154">The method `UpdateLanguageSettingsAsync()` in `MainWindow.xaml.cs`, shown here, calls the Languages endpoint to get the list of supported languages.</span></span> 

```csharp
private async Task UpdateLanguageSettingsAsync()
{
    Uri baseUri = new Uri("https://" + baseUrl);
    string fullUriString = "/Languages?api-version=1.0&scope=text,speech,tts";
    if (MenuItem_Experimental.IsChecked) fullUriString += "&flight=experimental";            
    Uri fullUri = new Uri(baseUri, fullUriString);

    using (HttpClient client = new HttpClient()) //'client' is the var - using statement ensures the dispose method is used even after an exception.
    {
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, fullUri);

        // get language names for current UI culture:
        request.Headers.Add("Accept-Language", CultureInfo.CurrentUICulture.TwoLetterISOLanguageName);

        // add a client-side trace Id. In case of issues, one can contact support and provide this:
        //string traceId = "SpeechTranslator" + Guid.NewGuid().ToString();
        //request.Headers.Add("X-ClientTraceId", traceId);
        //Debug.Print("TraceId: {0}", traceId);

        client.Timeout = TimeSpan.FromMilliseconds(10000);
        HttpResponseMessage response = await client.SendAsync(request); //make the async call to the web using the client var and passing the built up URI
        response.EnsureSuccessStatusCode(); //causes exception if the return is false

        Debug.Print("Request Id returned: {0}", GetRequestId(response));

        //create dictionaries to hold the language specific data
        spokenLanguages = new Dictionary<string, string>();
        fromLanguages = new Dictionary<string, string>();
        textLanguages = new Dictionary<string, string>();
        isLTR = new Dictionary<string, bool>();
        voices = new Dictionary<string, List<TTsDetail>>();

        JObject jResponse = JObject.Parse(await response.Content.ReadAsStringAsync()); //get the json from the async call with the response var created above, parse it and put it in a var called jResponse - JObject is a newton class

        //Gather the set of TTS voices
        foreach (JProperty jTts in jResponse["tts"])
        {
            JObject ttsDetails = (JObject)jTts.Value;

            string code = jTts.Name;
            string language = ttsDetails["language"].ToString();
            string displayName = ttsDetails["displayName"].ToString();
            string gender = ttsDetails["gender"].ToString();

            if (!voices.ContainsKey(language)) //check dictionary for a specific key value
            {
                voices.Add(language, new List<TTsDetail>()); //add to the dictionary the locale key and a ttsDetail object
            }

            voices[language].Add(new TTsDetail() { Code = code, DisplayName = string.Format("{0} ({1})", displayName, gender) });
        }

        // Gather the set of speech translation languages
        foreach (JProperty jSpeech in jResponse["speech"])
        {
            JObject languageDetails = (JObject)jSpeech.Value;
            string code = jSpeech.Name;
            string simplecode = languageDetails["language"].ToString();
            string displayName = languageDetails["name"].ToString();
            spokenLanguages.Add(code, displayName);
            fromLanguages.Add(code,simplecode);
        }

        spokenLanguages = spokenLanguages.OrderBy(x => x.Value).ToDictionary(x => x.Key, x => x.Value);
        FromLanguage.Items.Clear();
        foreach (var language in spokenLanguages)
        {
            FromLanguage.Items.Add(new ComboBoxItem() { Content = language.Value, Tag = language.Key});
        }

        // Gather the set of text translation languages
        foreach (JProperty jText in jResponse["text"])
        {
            JObject languageDetails = (JObject)jText.Value;
            string code = jText.Name;
            string displayName = languageDetails["name"].ToString();
            textLanguages.Add(code, displayName);

            string direction = languageDetails["dir"].ToString().ToLowerInvariant();
            bool LTR = true;
            if (direction.ToLowerInvariant() == "rtl") LTR = false;
            isLTR.Add(code, LTR);
        }

        textLanguages = textLanguages.OrderBy(x => x.Value).ToDictionary(x => x.Key, x => x.Value);
        ToLanguage.Items.Clear();
        foreach (var language in textLanguages)
        {
            ToLanguage.Items.Add(new ComboBoxItem() { Content = language.Value, Tag = language.Key });
        }

        if (Properties.Settings.Default.FromLanguageIndex >= 0) FromLanguage.SelectedIndex = Properties.Settings.Default.FromLanguageIndex;
        else
        {
            for(int i=0; i < FromLanguage.Items.Count; ++i)
            {
                ComboBoxItem item = (ComboBoxItem)FromLanguage.Items[i];
                if(CultureInfo.CurrentUICulture.Name.Equals((string)item.Tag, StringComparison.OrdinalIgnoreCase))
                {
                    FromLanguage.SelectedIndex = i;
                }
            }
        }
        if (Properties.Settings.Default.ToLanguageIndex >= 0) ToLanguage.SelectedIndex = Properties.Settings.Default.ToLanguageIndex;
        else
        {
            Random rnd = new Random(DateTime.Now.Millisecond);
            ToLanguage.SelectedIndex = (rnd.Next() % textLanguages.Count);
        }
    }
}
```

<span data-ttu-id="fe4d7-155">This method first constructs an HTTP request to the Languages endpoint, requesting all three lists of languages (`text`, `speech`, and `tts`).</span><span class="sxs-lookup"><span data-stu-id="fe4d7-155">This method first constructs an HTTP request to the Languages endpoint, requesting all three lists of languages (`text`, `speech`, and `tts`).</span></span>

<span data-ttu-id="fe4d7-156">The Languages endpoint uses the request's `Accept-Languages` header to determine the language in which the names of the languages are represented.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-156">The Languages endpoint uses the request's `Accept-Languages` header to determine the language in which the names of the languages are represented.</span></span> <span data-ttu-id="fe4d7-157">For example, the language known to English speakers as "German" is called "Deutsch" in German and "Alemán" in Spanish, and the list of languages reflects these differences.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-157">For example, the language known to English speakers as "German" is called "Deutsch" in German and "Alemán" in Spanish, and the list of languages reflects these differences.</span></span> <span data-ttu-id="fe4d7-158">The system's default language is used for this header.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-158">The system's default language is used for this header.</span></span>

<span data-ttu-id="fe4d7-159">After the request has been sent and the JSON response received, the response is parsed into internal data structures.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-159">After the request has been sent and the JSON response received, the response is parsed into internal data structures.</span></span> <span data-ttu-id="fe4d7-160">These structures are then used to construct the From Language and To Language menus.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-160">These structures are then used to construct the From Language and To Language menus.</span></span> 

<span data-ttu-id="fe4d7-161">Since the voices available depend on the To Language chosen by the user, it isn't possible to set up the Voice menu yet.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-161">Since the voices available depend on the To Language chosen by the user, it isn't possible to set up the Voice menu yet.</span></span> <span data-ttu-id="fe4d7-162">Instead, the available voices for each language are stored for later use.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-162">Instead, the available voices for each language are stored for later use.</span></span> <span data-ttu-id="fe4d7-163">The `ToLanguage_SelectionChanged` handler (in the same source file) later updates the Voice menu by calling `UpdateVoiceComboBox()`  when the user chooses a To Language.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-163">The `ToLanguage_SelectionChanged` handler (in the same source file) later updates the Voice menu by calling `UpdateVoiceComboBox()`  when the user chooses a To Language.</span></span> 

<span data-ttu-id="fe4d7-164">Just for fun, a To Language is randomly selected if the user has not run the application before.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-164">Just for fun, a To Language is randomly selected if the user has not run the application before.</span></span> <span data-ttu-id="fe4d7-165">(The menu settings are stored between sessions.)</span><span class="sxs-lookup"><span data-stu-id="fe4d7-165">(The menu settings are stored between sessions.)</span></span>

## <a name="authenticating-requests"></a><span data-ttu-id="fe4d7-166">Authenticating requests</span><span class="sxs-lookup"><span data-stu-id="fe4d7-166">Authenticating requests</span></span>

<span data-ttu-id="fe4d7-167">To authenticate to the Microsoft Translator Speech service you need to send your Azure subscription key in the header as the value for `Ocp-Apim-Subscription-Key` in the connection request.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-167">To authenticate to the Microsoft Translator Speech service you need to send your Azure subscription key in the header as the value for `Ocp-Apim-Subscription-Key` in the connection request.</span></span>

## <a name="translation-overview"></a><span data-ttu-id="fe4d7-168">Translation overview</span><span class="sxs-lookup"><span data-stu-id="fe4d7-168">Translation overview</span></span>

<span data-ttu-id="fe4d7-169">The Translate API (WebSockets endpoint `wss://dev.microsofttranslator.com/speech/translate`) accepts audio to be translated in monophonic, 16 kHz, 16-bit signed WAVE format.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-169">The Translate API (WebSockets endpoint `wss://dev.microsofttranslator.com/speech/translate`) accepts audio to be translated in monophonic, 16 kHz, 16-bit signed WAVE format.</span></span> <span data-ttu-id="fe4d7-170">The service returns one or more JSON responses containing both the recognized and translated text.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-170">The service returns one or more JSON responses containing both the recognized and translated text.</span></span> <span data-ttu-id="fe4d7-171">If text-to-speech has been requested, an audio file is sent.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-171">If text-to-speech has been requested, an audio file is sent.</span></span>

<span data-ttu-id="fe4d7-172">The user chooses the audio source using the Microphone/File Input menu.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-172">The user chooses the audio source using the Microphone/File Input menu.</span></span> <span data-ttu-id="fe4d7-173">The audio may come from an audio device (such as a microphone) or from a `.WAV` file.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-173">The audio may come from an audio device (such as a microphone) or from a `.WAV` file.</span></span>

<span data-ttu-id="fe4d7-174">The method `StartListening_Click` is invoked when the user clicks the Start button.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-174">The method `StartListening_Click` is invoked when the user clicks the Start button.</span></span> <span data-ttu-id="fe4d7-175">This event handler, in turn, calls `Connect()` to begin the process of sending audio to the service API endpoint.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-175">This event handler, in turn, calls `Connect()` to begin the process of sending audio to the service API endpoint.</span></span> <span data-ttu-id="fe4d7-176">The `Connect()` method performs the following tasks:</span><span class="sxs-lookup"><span data-stu-id="fe4d7-176">The `Connect()` method performs the following tasks:</span></span>


> [!div class="checklist"]
> * <span data-ttu-id="fe4d7-177">Getting user settings from the main window and validate them</span><span class="sxs-lookup"><span data-stu-id="fe4d7-177">Getting user settings from the main window and validate them</span></span>
> * <span data-ttu-id="fe4d7-178">Initializing the audio input and output streams</span><span class="sxs-lookup"><span data-stu-id="fe4d7-178">Initializing the audio input and output streams</span></span>
> * <span data-ttu-id="fe4d7-179">Calling `ConnectAsync()` to handle the rest of the work</span><span class="sxs-lookup"><span data-stu-id="fe4d7-179">Calling `ConnectAsync()` to handle the rest of the work</span></span>

<span data-ttu-id="fe4d7-180">`ConnectAsync()`, in turn, handles the following chores:</span><span class="sxs-lookup"><span data-stu-id="fe4d7-180">`ConnectAsync()`, in turn, handles the following chores:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fe4d7-181">Authenticating with Azure Subscription key in header `Ocp-Apim-Subscription-Key`</span><span class="sxs-lookup"><span data-stu-id="fe4d7-181">Authenticating with Azure Subscription key in header `Ocp-Apim-Subscription-Key`</span></span>
> * <span data-ttu-id="fe4d7-182">Creating a `SpeechClient` instance (found in `SpeechClient.cs`) to communicate with the service</span><span class="sxs-lookup"><span data-stu-id="fe4d7-182">Creating a `SpeechClient` instance (found in `SpeechClient.cs`) to communicate with the service</span></span>
> * <span data-ttu-id="fe4d7-183">Initializing `TextMessageDecoder` and `BinaryMessageDecoder` instances (see `SpeechResponseDecoder.cs`) to handle responses</span><span class="sxs-lookup"><span data-stu-id="fe4d7-183">Initializing `TextMessageDecoder` and `BinaryMessageDecoder` instances (see `SpeechResponseDecoder.cs`) to handle responses</span></span>
> * <span data-ttu-id="fe4d7-184">Sending the audio via the `SpeechClient` instance to the Translator Speech service</span><span class="sxs-lookup"><span data-stu-id="fe4d7-184">Sending the audio via the `SpeechClient` instance to the Translator Speech service</span></span>
> * <span data-ttu-id="fe4d7-185">Receiving and processing the results of the translation</span><span class="sxs-lookup"><span data-stu-id="fe4d7-185">Receiving and processing the results of the translation</span></span>

<span data-ttu-id="fe4d7-186">The responsibilities of `SpeechClient` are fewer:</span><span class="sxs-lookup"><span data-stu-id="fe4d7-186">The responsibilities of `SpeechClient` are fewer:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fe4d7-187">Establishing a WebSocket connection to the Translator Speech service</span><span class="sxs-lookup"><span data-stu-id="fe4d7-187">Establishing a WebSocket connection to the Translator Speech service</span></span>
> * <span data-ttu-id="fe4d7-188">Sending audio data and receiving responses via the socket</span><span class="sxs-lookup"><span data-stu-id="fe4d7-188">Sending audio data and receiving responses via the socket</span></span>

## <a name="a-closer-look"></a><span data-ttu-id="fe4d7-189">A closer look</span><span class="sxs-lookup"><span data-stu-id="fe4d7-189">A closer look</span></span>

<span data-ttu-id="fe4d7-190">It should be clearer now how parts of the application work together to perform the translation request.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-190">It should be clearer now how parts of the application work together to perform the translation request.</span></span> <span data-ttu-id="fe4d7-191">Let's take a look at some code, focusing on the relevant parts.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-191">Let's take a look at some code, focusing on the relevant parts.</span></span>

<span data-ttu-id="fe4d7-192">Here's a partial version of `Connect()` that shows setting up the audio streams:</span><span class="sxs-lookup"><span data-stu-id="fe4d7-192">Here's a partial version of `Connect()` that shows setting up the audio streams:</span></span>

```csharp
private void Connect()
{
    if (this.currentState != UiState.ReadyToConnect) return;

    Stopwatch watch = Stopwatch.StartNew();
    UpdateUiState(UiState.Connecting);

    // Omitted: code to validate UI settings

    string tag = ((ComboBoxItem)Mic.SelectedItem).Tag as string;
    string audioFileInputPath = null;
    if (tag == "File")
    {
        audioFileInputPath = this.AudioFileInput.Text;
        foreach (string currFile in audioFileInputPath.Split('|'))
        {
            if (!File.Exists(currFile))
            {
                SetMessage(String.Format($"Invalid audio source: selected file {currFile} does not exist."), "", MessageKind.Error);
                UpdateUiState(UiState.ReadyToConnect);
                return;
            }
        }
    }
    bool shouldSuspendInputAudioDuringTTS = this.CutInputAudioCheckBox.IsChecked.HasValue ? this.CutInputAudioCheckBox.IsChecked.Value : false;

    correlationId = Guid.NewGuid().ToString("D").Split('-')[0].ToUpperInvariant();

    // Setup speech translation client options
    SpeechClientOptions options;

    string voicename = "";
    if (this.Voice.SelectedItem != null)
    {
        voicename = ((ComboBoxItem)this.Voice.SelectedItem).Tag.ToString();
    }
    options = new SpeechTranslateClientOptions()
    {
        TranslateFrom = ((ComboBoxItem)this.FromLanguage.SelectedItem).Tag.ToString(),
        TranslateTo = ((ComboBoxItem)this.ToLanguage.SelectedItem).Tag.ToString(),
        Voice = voicename,
    };
    
    options.Hostname = baseUrl;
    options.AuthHeaderKey = "Authorization";
    options.AuthHeaderValue = ""; // set later in ConnectAsync.
    options.ClientAppId = new Guid("EA66703D-90A8-436B-9BD6-7A2707A2AD99");
    options.CorrelationId = this.correlationId;
    options.Features = GetFeatures().ToString().Replace(" ", "");
    options.Profanity = ((SpeechClient.ProfanityFilter)Enum.Parse(typeof(SpeechClient.ProfanityFilter), GetProfanityLevel(), true)).ToString();
    options.Experimental = MenuItem_Experimental.IsChecked;

    // Setup player and recorder but don't start them yet.
    WaveFormat waveFormat = new WaveFormat(16000, 16, 1);

    // WaveProvider for incoming TTS
    // We use a rather large BufferDuration because we need to be able to hold an entire utterance.
    // TTS audio is received in bursts (faster than real-time).
    textToSpeechBytes = 0;
    playerTextToSpeechWaveProvider = new BufferedWaveProvider(waveFormat);
    playerTextToSpeechWaveProvider.BufferDuration = TimeSpan.FromMinutes(5);

    ISampleProvider sampleProvider = null;
    if (audioFileInputPath != null)
    {
        // Setup mixing of audio from input file and from TTS
        playerAudioInputWaveProvider = new BufferedWaveProvider(waveFormat);
        var srce1 = new Pcm16BitToSampleProvider(playerTextToSpeechWaveProvider);
        var srce2 = new Pcm16BitToSampleProvider(playerAudioInputWaveProvider);
        var mixer = new MixingSampleProvider(srce1.WaveFormat);
        mixer.AddMixerInput(srce1);
        mixer.AddMixerInput(srce2);
        sampleProvider = mixer;
    }
    else
    {
        recorder = new WaveIn();
        recorder.DeviceNumber = (int)((ComboBoxItem)Mic.SelectedItem).Tag;
        recorder.WaveFormat = waveFormat;
        recorder.DataAvailable += OnRecorderDataAvailable;
        sampleProvider = playerTextToSpeechWaveProvider.ToSampleProvider();
    }

    if (!batchMode)
    {
        player = new WaveOut();
        player.DeviceNumber = (int)((ComboBoxItem)Speaker.SelectedItem).Tag;
        player.Init(sampleProvider);
    }

    this.audioBytesSent = 0;

    string logAudioFileName = null;
    if (LogSentAudio.IsChecked|| LogReceivedAudio.IsChecked)
    {
        string logAudioPath = System.IO.Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.ApplicationData), Properties.Settings.Default.OutputDirectory);
        try
        {
            Directory.CreateDirectory(logAudioPath);
        }
        catch
        {
            this.AddItemToLog(string.Format("Could not create folder {0}", logAudioPath));
        }

        if (LogSentAudio.IsChecked)
        {
            logAudioFileName = System.IO.Path.Combine(logAudioPath, string.Format("audiosent_{0}.wav", this.correlationId));
        }

        if (LogReceivedAudio.IsChecked)
        {
            string fmt = System.IO.Path.Combine(logAudioPath, string.Format("audiotts_{0}_{{0}}.wav", this.correlationId));
            this.audioReceived = new BinaryMessageDecoder(fmt);
        }
    }
}
```

<span data-ttu-id="fe4d7-193">A substantial portion of `Connect()` involves the creation of a `SpeechClientOptions` instance (see `SpeechClientOptions.cs`) to hold the options for translation.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-193">A substantial portion of `Connect()` involves the creation of a `SpeechClientOptions` instance (see `SpeechClientOptions.cs`) to hold the options for translation.</span></span> <span data-ttu-id="fe4d7-194">Options include the information needed to connect to the service (such as authentication key and hostname) and the features used for the translation.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-194">Options include the information needed to connect to the service (such as authentication key and hostname) and the features used for the translation.</span></span> <span data-ttu-id="fe4d7-195">The fields here map to the header fields and HTTP parameters exposed by [the Translator Speech API](https://docs.microsoft.com/azure/cognitive-services/translator-speech/reference).</span><span class="sxs-lookup"><span data-stu-id="fe4d7-195">The fields here map to the header fields and HTTP parameters exposed by [the Translator Speech API](https://docs.microsoft.com/azure/cognitive-services/translator-speech/reference).</span></span>

<span data-ttu-id="fe4d7-196">`Connect()` also creates and initializes the audio input device (variable `sampleProvider`) that serves as the source of the speech to be translated.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-196">`Connect()` also creates and initializes the audio input device (variable `sampleProvider`) that serves as the source of the speech to be translated.</span></span> <span data-ttu-id="fe4d7-197">This device is either a hardware input device such as a microphone, or a file containing WAVE audio data.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-197">This device is either a hardware input device such as a microphone, or a file containing WAVE audio data.</span></span>

<span data-ttu-id="fe4d7-198">Here's the `ConnectAsync()` method that instantiates the `speechClient` class and hooks up anonymous functions to handle text and binary responses from the service.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-198">Here's the `ConnectAsync()` method that instantiates the `speechClient` class and hooks up anonymous functions to handle text and binary responses from the service.</span></span>

```csharp
private async Task ConnectAsync(SpeechClientOptions options, bool suspendInputAudioDuringTTS)
{
    await ADMAuthenticate(options);
    
    TextMessageDecoder textDecoder;
    
    s2smtClient = new SpeechClient((SpeechTranslateClientOptions)options, CancellationToken.None);
    
    s2smtClient.OnBinaryData += (c, a) => { AddSamplesToPlay(a, suspendInputAudioDuringTTS); };
    s2smtClient.OnEndOfBinaryData += (c, a) => { AddSamplesToPlay(a, suspendInputAudioDuringTTS); };
    s2smtClient.OnTextData += (c, a) => { textDecoder.AppendData(a); lastReceivedPacketTick = DateTime.Now.Ticks; };
    s2smtClient.OnEndOfTextData += (c, a) =>
    {
        textDecoder.AppendData(a);
        lastReceivedPacketTick = DateTime.Now.Ticks;
        textDecoder
            .Decode()
            .ContinueWith(t =>
            {
                if (t.IsFaulted)
                {
                    Log(t.Exception, "E: Failed to decode incoming text message.");
                }
                else
                {
                    object msg = t.Result;
                    if (msg.GetType() == typeof(FinalResultMessage))
                    {
                        // omitted: code to process final binary result
                    }
                    if (msg.GetType() == typeof(PartialResultMessage))
                    {
                        // omitted: code to process partial binary result
                    }
                }
            });
    };
    s2smtClient.Failed += (c, ex) =>
    {
        Log(ex, "E: SpeechTranslation client reported an error.");
    };
    s2smtClient.Disconnected += (c, ea) =>
    {
        SafeInvoke(() =>
        {
            // We only care to react to server disconnect when our state is Connected. 
            if (currentState == UiState.Connected)
            {
                Log("E: Connection has been lost.");
                Log($"E: Errors (if any): \n{string.Join("\n", s2smtClient.Errors)}");
                Disconnect();
            }
        });
    };
    await s2smtClient.Connect();
}
```

<span data-ttu-id="fe4d7-199">After authenticating, the method creates the `SpeechClient` instance.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-199">After authenticating, the method creates the `SpeechClient` instance.</span></span> <span data-ttu-id="fe4d7-200">The `SpeechClient` class (in `SpeechClient.cs`) invokes event handlers upon receipt binary and text data.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-200">The `SpeechClient` class (in `SpeechClient.cs`) invokes event handlers upon receipt binary and text data.</span></span> <span data-ttu-id="fe4d7-201">Additional handlers are invoked when the connection fails or disconnects.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-201">Additional handlers are invoked when the connection fails or disconnects.</span></span>

<span data-ttu-id="fe4d7-202">Binary data is audio (text-to-speech output) sent by the service when TTS is enabled.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-202">Binary data is audio (text-to-speech output) sent by the service when TTS is enabled.</span></span> <span data-ttu-id="fe4d7-203">Text data is either a partial or a full translation of the spoken text.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-203">Text data is either a partial or a full translation of the spoken text.</span></span> <span data-ttu-id="fe4d7-204">So after instantiating, the method hooks up functions to handle these messages: audio by storing it for later playback, and text by displaying it in the window.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-204">So after instantiating, the method hooks up functions to handle these messages: audio by storing it for later playback, and text by displaying it in the window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe4d7-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="fe4d7-205">Next steps</span></span>

<span data-ttu-id="fe4d7-206">This code sample is a feature-rich application demonstrating the use of the Translator Speech API.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-206">This code sample is a feature-rich application demonstrating the use of the Translator Speech API.</span></span> <span data-ttu-id="fe4d7-207">As such, there are a fair number of moving parts to understand.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-207">As such, there are a fair number of moving parts to understand.</span></span> <span data-ttu-id="fe4d7-208">You've walked through the most important bits.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-208">You've walked through the most important bits.</span></span> <span data-ttu-id="fe4d7-209">For the rest, it can be instructive to set a few breakpoints in Visual Studio and walk through the translation process.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-209">For the rest, it can be instructive to set a few breakpoints in Visual Studio and walk through the translation process.</span></span> <span data-ttu-id="fe4d7-210">When you understand the sample application, you're equipped to use the Translator Speech service in your own applications.</span><span class="sxs-lookup"><span data-stu-id="fe4d7-210">When you understand the sample application, you're equipped to use the Translator Speech service in your own applications.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fe4d7-211">Microsoft Translator Speech API reference</span><span class="sxs-lookup"><span data-stu-id="fe4d7-211">Microsoft Translator Speech API reference</span></span>](https://docs.microsoft.com/azure/cognitive-services/translator-speech/reference)
