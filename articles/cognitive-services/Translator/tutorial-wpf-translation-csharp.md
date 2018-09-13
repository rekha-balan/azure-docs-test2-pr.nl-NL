---
title: 'Tutorial: Write a WPF application for Translator Text using C# | Microsoft Docs'
titleSuffix: Microsoft Cognitive Services
description: In this tutorial, you'll learn how to use the Translator Text API to translate text, get a localized list of supported languages, and more, by building a WPF application using C#.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: tutorial
ms.date: 07/20/2018
ms.author: nolachar
ms.openlocfilehash: 933e4ed3e4ea139e9edfa8dc1acf81502b04d188
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871499"
---
# <a name="tutorial-write-a-wpf-application-for-translator-text-using-c35"></a><span data-ttu-id="b575c-103">Tutorial: Write a WPF application for Translator Text using C&#35;</span><span class="sxs-lookup"><span data-stu-id="b575c-103">Tutorial: Write a WPF application for Translator Text using C&#35;</span></span>

<span data-ttu-id="b575c-104">In this tutorial, you'll build an interactive text translation tool using the Translator Text API (V3), a part of Microsoft Cognitive Services in Azure.</span><span class="sxs-lookup"><span data-stu-id="b575c-104">In this tutorial, you'll build an interactive text translation tool using the Translator Text API (V3), a part of Microsoft Cognitive Services in Azure.</span></span> <span data-ttu-id="b575c-105">You'll learn how to:</span><span class="sxs-lookup"><span data-stu-id="b575c-105">You'll learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b575c-106">Get a list of languages supported by the service</span><span class="sxs-lookup"><span data-stu-id="b575c-106">Get a list of languages supported by the service</span></span>
> * <span data-ttu-id="b575c-107">Perform a translation of user-entered text from one language to another</span><span class="sxs-lookup"><span data-stu-id="b575c-107">Perform a translation of user-entered text from one language to another</span></span>

<span data-ttu-id="b575c-108">This application also features integration with two other Microsoft Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="b575c-108">This application also features integration with two other Microsoft Cognitive Services.</span></span>

|||
|-|-|
|[<span data-ttu-id="b575c-109">Text Analytics</span><span class="sxs-lookup"><span data-stu-id="b575c-109">Text Analytics</span></span>](https://azure.microsoft.com/services/cognitive-services/text-analytics/)|<span data-ttu-id="b575c-110">Used to optionally automatically detect the source language of the text to be translated</span><span class="sxs-lookup"><span data-stu-id="b575c-110">Used to optionally automatically detect the source language of the text to be translated</span></span>|
|[<span data-ttu-id="b575c-111">Bing Spell Check</span><span class="sxs-lookup"><span data-stu-id="b575c-111">Bing Spell Check</span></span>](https://azure.microsoft.com/services/cognitive-services/spell-check/)|<span data-ttu-id="b575c-112">For English source text, used to correct misspellings so translation is more accurate</span><span class="sxs-lookup"><span data-stu-id="b575c-112">For English source text, used to correct misspellings so translation is more accurate</span></span>

![[The tutorial program running]](media/translator-text-csharp-session.png)

## <a name="prerequisites"></a><span data-ttu-id="b575c-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b575c-114">Prerequisites</span></span>

<span data-ttu-id="b575c-115">You'll need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span><span class="sxs-lookup"><span data-stu-id="b575c-115">You'll need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span></span> <span data-ttu-id="b575c-116">(The free Community Edition will work.)</span><span class="sxs-lookup"><span data-stu-id="b575c-116">(The free Community Edition will work.)</span></span>

<span data-ttu-id="b575c-117">You also need subscription keys for the three Azure services used in the program.</span><span class="sxs-lookup"><span data-stu-id="b575c-117">You also need subscription keys for the three Azure services used in the program.</span></span> <span data-ttu-id="b575c-118">You can get a key for the Translator Text service from the Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="b575c-118">You can get a key for the Translator Text service from the Azure dashboard.</span></span> <span data-ttu-id="b575c-119">A free pricing tier is available that allows you to translate up to two million characters per month at no charge.</span><span class="sxs-lookup"><span data-stu-id="b575c-119">A free pricing tier is available that allows you to translate up to two million characters per month at no charge.</span></span>

<span data-ttu-id="b575c-120">Both the Text Analytics and Bing Spell Check services offer free trials, which you can sign up for on [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="b575c-120">Both the Text Analytics and Bing Spell Check services offer free trials, which you can sign up for on [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/).</span></span> <span data-ttu-id="b575c-121">You may also create a subscription for either service via the Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="b575c-121">You may also create a subscription for either service via the Azure dashboard.</span></span> <span data-ttu-id="b575c-122">Text Analytics has a free tier.</span><span class="sxs-lookup"><span data-stu-id="b575c-122">Text Analytics has a free tier.</span></span>

<span data-ttu-id="b575c-123">Source code for this tutorial is available below.</span><span class="sxs-lookup"><span data-stu-id="b575c-123">Source code for this tutorial is available below.</span></span> <span data-ttu-id="b575c-124">Your subscription keys must be copied into the source code as the variables `TEXT_TRANSLATION_API_SUBSCRIPTION_KEY`, and so on, in `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="b575c-124">Your subscription keys must be copied into the source code as the variables `TEXT_TRANSLATION_API_SUBSCRIPTION_KEY`, and so on, in `MainWindow.xaml.cs`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b575c-125">The Text Analytics service is available in multiple regions.</span><span class="sxs-lookup"><span data-stu-id="b575c-125">The Text Analytics service is available in multiple regions.</span></span> <span data-ttu-id="b575c-126">The URI in this tutorial source code is in the `westus` region, which is the region used for free trials.</span><span class="sxs-lookup"><span data-stu-id="b575c-126">The URI in this tutorial source code is in the `westus` region, which is the region used for free trials.</span></span> <span data-ttu-id="b575c-127">If you have a subscription in another region, update this URI accordingly.</span><span class="sxs-lookup"><span data-stu-id="b575c-127">If you have a subscription in another region, update this URI accordingly.</span></span>

## <a name="source-code"></a><span data-ttu-id="b575c-128">Source code</span><span class="sxs-lookup"><span data-stu-id="b575c-128">Source code</span></span>

<span data-ttu-id="b575c-129">This is the source code for the Microsoft Translator text API.</span><span class="sxs-lookup"><span data-stu-id="b575c-129">This is the source code for the Microsoft Translator text API.</span></span> <span data-ttu-id="b575c-130">To run the app, copy the source code into the appropriate file in a new WPF project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b575c-130">To run the app, copy the source code into the appropriate file in a new WPF project in Visual Studio.</span></span>

### <a name="mainwindowxamlcs"></a><span data-ttu-id="b575c-131">MainWindow.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="b575c-131">MainWindow.xaml.cs</span></span>

<span data-ttu-id="b575c-132">This is the code-behind file that provides the application's functionality.</span><span class="sxs-lookup"><span data-stu-id="b575c-132">This is the code-behind file that provides the application's functionality.</span></span>

```csharp
using System;
using System.Windows;
using System.Net;
using System.Net.Http;
using System.IO;
using System.Collections.Generic;
using System.Linq;
using System.Text;

// NOTE: Add assembly references to System.Runtime.Serialization, System.Web, and System.Web.Extensions.

// NOTE: Install the Newtonsoft.Json NuGet package.
using Newtonsoft.Json;

namespace MSTranslatorTextDemo
{
    /// <summary>
    /// This WPF application demonstrates the use of the Microsoft Translator Text API to translate a brief text string from
    /// one language to another. The languages are selected from a drop-down menu. The text of the translation is displayed.
    /// The source language may optionally be automatically detected. English text is spell-checked.
    /// </summary>
    public partial class MainWindow : Window
    {
        // Translator text subscription key from Microsoft Azure dashboard
        const string TEXT_TRANSLATION_API_SUBSCRIPTION_KEY = "ENTER KEY HERE";
        const string TEXT_ANALYTICS_API_SUBSCRIPTION_KEY = "ENTER KEY HERE";
        const string BING_SPELL_CHECK_API_SUBSCRIPTION_KEY = "ENTER KEY HERE";

        public static readonly string TEXT_TRANSLATION_API_ENDPOINT = "https://api.cognitive.microsofttranslator.com/{0}?api-version=3.0";
        const string TEXT_ANALYTICS_API_ENDPOINT = "https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/";
        const string BING_SPELL_CHECK_API_ENDPOINT = "https://api.cognitive.microsoft.com/bing/v7.0/spellcheck/";

        private string[] languageCodes;     // array of language codes

        // Dictionary to map language code from friendly name (sorted case-insensitively on language name)
        private SortedDictionary<string, string> languageCodesAndTitles =
            new SortedDictionary<string, string>(Comparer<string>.Create((a, b) => string.Compare(a, b, true)));

        public MainWindow()
        {
            // at least show an error dialog if there's an unexpected error
            AppDomain.CurrentDomain.UnhandledException += new UnhandledExceptionEventHandler(HandleExceptions);

            if (TEXT_TRANSLATION_API_SUBSCRIPTION_KEY.Length != 32
                || TEXT_ANALYTICS_API_SUBSCRIPTION_KEY.Length != 32
                || BING_SPELL_CHECK_API_SUBSCRIPTION_KEY.Length != 32)
            {
                MessageBox.Show("One or more invalid API subscription keys.\n\n" +
                    "Put your keys in the *_API_SUBSCRIPTION_KEY variables in MainWindow.xaml.cs.",
                    "Invalid Subscription Key(s)", MessageBoxButton.OK, MessageBoxImage.Error);
                System.Windows.Application.Current.Shutdown();
            }
            else
            {
                InitializeComponent();          // start the GUI
                GetLanguagesForTranslate();     // get codes and friendly names of languages that can be translated
                PopulateLanguageMenus();        // fill the drop-down language lists
            }
        }

        // Global exception handler to display error message and exit
        private static void HandleExceptions(object sender, UnhandledExceptionEventArgs args)
        {
            Exception e = (Exception)args.ExceptionObject;
            MessageBox.Show("Caught " + e.Message, "Error", MessageBoxButton.OK, MessageBoxImage.Error);
            System.Windows.Application.Current.Shutdown();
        }

        // ***** POPULATE LANGUAGE MENUS
        private void PopulateLanguageMenus()
        {
            // Add option to automatically detect the source language
            FromLanguageComboBox.Items.Add("Detect");

            int count = languageCodesAndTitles.Count;
            foreach (string menuItem in languageCodesAndTitles.Keys)
            {
                FromLanguageComboBox.Items.Add(menuItem);
                ToLanguageComboBox.Items.Add(menuItem);
            }

            // set default languages
            FromLanguageComboBox.SelectedItem = "Detect";
            ToLanguageComboBox.SelectedItem = "English";
        }

        // ***** DETECT LANGUAGE OF TEXT TO BE TRANSLATED
        private string DetectLanguage(string text)
        {
            string uri = TEXT_ANALYTICS_API_ENDPOINT + "languages?numberOfLanguagesToDetect=1";

            // create request to Text Analytics API
            HttpWebRequest detectLanguageWebRequest = (HttpWebRequest)WebRequest.Create(uri);
            detectLanguageWebRequest.Headers.Add("Ocp-Apim-Subscription-Key", TEXT_ANALYTICS_API_SUBSCRIPTION_KEY);
            detectLanguageWebRequest.Method = "POST";

            // create and send body of request
            var serializer = new System.Web.Script.Serialization.JavaScriptSerializer();
            string jsonText = serializer.Serialize(text);

            string body = "{ \"documents\": [ { \"id\": \"0\", \"text\": " + jsonText + "} ] }";
            byte[] data = Encoding.UTF8.GetBytes(body);
            detectLanguageWebRequest.ContentLength = data.Length;

            using (var requestStream = detectLanguageWebRequest.GetRequestStream())
                requestStream.Write(data, 0, data.Length);

            HttpWebResponse response = (HttpWebResponse)detectLanguageWebRequest.GetResponse();

            // read and parse JSON response
            var responseStream = response.GetResponseStream();
            var jsonString = new StreamReader(responseStream, Encoding.GetEncoding("utf-8")).ReadToEnd();
            dynamic jsonResponse = serializer.DeserializeObject(jsonString);

            // fish out the detected language code
            var languageInfo = jsonResponse["documents"][0]["detectedLanguages"][0];
            if (languageInfo["score"] > (decimal)0.5)
                return languageInfo["iso6391Name"];
            else
                return "";
        }

        // ***** CORRECT SPELLING OF TEXT TO BE TRANSLATED
        private string CorrectSpelling(string text)
        {
            string uri = BING_SPELL_CHECK_API_ENDPOINT + "?mode=spell&mkt=en-US";

            // create request to Bing Spell Check API
            HttpWebRequest spellCheckWebRequest = (HttpWebRequest)WebRequest.Create(uri);
            spellCheckWebRequest.Headers.Add("Ocp-Apim-Subscription-Key", BING_SPELL_CHECK_API_SUBSCRIPTION_KEY);
            spellCheckWebRequest.Method = "POST";
            spellCheckWebRequest.ContentType = "application/x-www-form-urlencoded"; // doesn't work without this

            // create and send body of request
            string body = "text=" + System.Web.HttpUtility.UrlEncode(text);
            byte[] data = Encoding.UTF8.GetBytes(body);
            spellCheckWebRequest.ContentLength = data.Length;
            using (var requestStream = spellCheckWebRequest.GetRequestStream())
                requestStream.Write(data, 0, data.Length);
            HttpWebResponse response = (HttpWebResponse)spellCheckWebRequest.GetResponse();

            // read and parse JSON response and get spelling corrections
            var serializer = new System.Web.Script.Serialization.JavaScriptSerializer();
            var responseStream = response.GetResponseStream();
            var jsonString = new StreamReader(responseStream, Encoding.GetEncoding("utf-8")).ReadToEnd();
            dynamic jsonResponse = serializer.DeserializeObject(jsonString);
            var flaggedTokens = jsonResponse["flaggedTokens"];

            // construct sorted dictionary of corrections in reverse order in string (right to left)
            // so that making a correction can't affect later indexes
            var corrections = new SortedDictionary<int, string[]>(Comparer<int>.Create((a, b) => b.CompareTo(a)));
            for (int i = 0; i < flaggedTokens.Length; i++)
            {
                var correction = flaggedTokens[i];
                var suggestion = correction["suggestions"][0];  // consider only first suggestion
                if (suggestion["score"] > (decimal)0.7)         // take it only if highly confident
                    corrections[(int)correction["offset"]] = new string[]   // dict key   = offset
                        { correction["token"], suggestion["suggestion"] };  // dict value = {error, correction}
            }

            // apply the corrections in order from right to left
            foreach (int i in corrections.Keys)
            {
                var oldtext = corrections[i][0];
                var newtext = corrections[i][1];

                // apply capitalization from original text to correction - all caps or initial caps
                if (text.Substring(i, oldtext.Length).All(char.IsUpper)) newtext = newtext.ToUpper();
                else if (char.IsUpper(text[i])) newtext = newtext[0].ToString().ToUpper() + newtext.Substring(1);

                text = text.Substring(0, i) + newtext + text.Substring(i + oldtext.Length);
            }

            return text;
        }

        // ***** GET TRANSLATABLE LANGUAGE CODES
        private void GetLanguagesForTranslate()
        {
            // send request to get supported language codes
            string uri = String.Format(TEXT_TRANSLATION_API_ENDPOINT, "languages") + "&scope=translation";
            WebRequest WebRequest = WebRequest.Create(uri);
            WebRequest.Headers.Add("Ocp-Apim-Subscription-Key", TEXT_TRANSLATION_API_SUBSCRIPTION_KEY);
            WebRequest.Headers.Add("Accept-Language", "en");
            WebResponse response = null;
            // read and parse the JSON response
            response = WebRequest.GetResponse();
            using (var reader = new StreamReader(response.GetResponseStream(), UnicodeEncoding.UTF8))
            {
                var result = JsonConvert.DeserializeObject<Dictionary<string, Dictionary<string, Dictionary<string, string>>>>(reader.ReadToEnd());
                var languages = result["translation"];

                languageCodes = languages.Keys.ToArray();
                foreach (var kv in languages)
                {
                    languageCodesAndTitles.Add(kv.Value["name"], kv.Key);
                }
            }
        }

        // ***** PERFORM TRANSLATION ON BUTTON CLICK
        private async void TranslateButton_Click(object sender, EventArgs e)
        {
            string textToTranslate = TextToTranslate.Text.Trim();

            string fromLanguage = FromLanguageComboBox.SelectedValue.ToString();
            string fromLanguageCode;

            // auto-detect source language if requested
            if (fromLanguage == "Detect")
            {
                fromLanguageCode = DetectLanguage(textToTranslate);
                if (!languageCodes.Contains(fromLanguageCode))
                {
                    MessageBox.Show("The source language could not be detected automatically " +
                        "or is not supported for translation.", "Language detection failed",
                        MessageBoxButton.OK, MessageBoxImage.Error);
                    return;
                }
            }
            else
                fromLanguageCode = languageCodesAndTitles[fromLanguage];

            string toLanguageCode = languageCodesAndTitles[ToLanguageComboBox.SelectedValue.ToString()];

            // spell-check the source text if the source language is English
            if (fromLanguageCode == "en")
            {
                if (textToTranslate.StartsWith("-"))    // don't spell check in this case
                    textToTranslate = textToTranslate.Substring(1);
                else
                {
                    textToTranslate = CorrectSpelling(textToTranslate);
                    TextToTranslate.Text = textToTranslate;     // put corrected text into input field
                }
            }

            // handle null operations: no text or same source/target languages
            if (textToTranslate == "" || fromLanguageCode == toLanguageCode)
            {
                TranslatedTextLabel.Content = textToTranslate;
                return;
            }

            // send HTTP request to perform the translation
            string endpoint = string.Format(TEXT_TRANSLATION_API_ENDPOINT, "translate");
            string uri = string.Format(endpoint + "&from={0}&to={1}", fromLanguageCode, toLanguageCode);

            System.Object[] body = new System.Object[] { new { Text = textToTranslate } };
            var requestBody = JsonConvert.SerializeObject(body);

            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Post;
                request.RequestUri = new Uri(uri);
                request.Content = new StringContent(requestBody, Encoding.UTF8, "application/json");
                request.Headers.Add("Ocp-Apim-Subscription-Key", TEXT_TRANSLATION_API_SUBSCRIPTION_KEY);
                request.Headers.Add("X-ClientTraceId", Guid.NewGuid().ToString());

                var response = await client.SendAsync(request);
                var responseBody = await response.Content.ReadAsStringAsync();

                var result = JsonConvert.DeserializeObject<List<Dictionary<string, List<Dictionary<string, string>>>>>(responseBody);
                var translations = result[0]["translations"];
                var translation = translations[0]["text"];

                // Update the translation field
                TranslatedTextLabel.Content = translation;
            }
        }
    }
}
```

### <a name="mainwindowxaml"></a><span data-ttu-id="b575c-133">MainWindow.xaml</span><span class="sxs-lookup"><span data-stu-id="b575c-133">MainWindow.xaml</span></span>

<span data-ttu-id="b575c-134">This file defines the user interface for the application, a WPF form.</span><span class="sxs-lookup"><span data-stu-id="b575c-134">This file defines the user interface for the application, a WPF form.</span></span> <span data-ttu-id="b575c-135">If you want to design your own version of the form, you don't need this XAML.</span><span class="sxs-lookup"><span data-stu-id="b575c-135">If you want to design your own version of the form, you don't need this XAML.</span></span>

```xml
<Window x:Class="MSTranslatorTextDemo.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:MSTranslatorTextDemo"
        mc:Ignorable="d"
        Title="Microsoft Translator" Height="400" Width="700" BorderThickness="0">
    <Grid>
        <Label x:Name="label" Content="Microsoft Translator" HorizontalAlignment="Left" Margin="39,6,0,0" VerticalAlignment="Top" Height="49" FontSize="26.667"/>
        <TextBox x:Name="TextToTranslate" HorizontalAlignment="Left" Height="23" Margin="42,160,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="600" FontSize="14" TabIndex="3"/>
        <Label x:Name="EnterTextLabel" Content="Text to translate:" HorizontalAlignment="Left" Margin="40,129,0,0" VerticalAlignment="Top" FontSize="14"/>
        <Label x:Name="toLabel" Content="Translate to:" HorizontalAlignment="Left" Margin="304,58,0,0" VerticalAlignment="Top" FontSize="14"/>

        <Button x:Name="TranslateButton" Content="Translate" HorizontalAlignment="Left" Margin="39,206,0,0" VerticalAlignment="Top" Width="114" Height="31" Click="TranslateButton_Click" FontSize="14" TabIndex="4" IsDefault="True"/>
        <ComboBox x:Name="ToLanguageComboBox"
                HorizontalAlignment="Left"
                Margin="306,88,0,0"
                VerticalAlignment="Top"
                Width="175" FontSize="14" TabIndex="2">

        </ComboBox>
        <Label x:Name="fromLabel" Content="Translate from:" HorizontalAlignment="Left" Margin="40,58,0,0" VerticalAlignment="Top" FontSize="14"/>
        <ComboBox x:Name="FromLanguageComboBox"
            HorizontalAlignment="Left"
            Margin="42,88,0,0"
            VerticalAlignment="Top"
            Width="175" FontSize="14" TabIndex="1"/>
        <Label x:Name="TranslatedTextLabel" Content="Translation appears here" HorizontalAlignment="Left" Margin="39,255,0,0" VerticalAlignment="Top" Width="620" FontSize="14" Height="85" BorderThickness="0"/>
    </Grid>
</Window>
```

## <a name="service-endpoints"></a><span data-ttu-id="b575c-136">Service endpoints</span><span class="sxs-lookup"><span data-stu-id="b575c-136">Service endpoints</span></span>

<span data-ttu-id="b575c-137">The Microsoft Translator service has a number of endpoints that provide various pieces of translation functionality.</span><span class="sxs-lookup"><span data-stu-id="b575c-137">The Microsoft Translator service has a number of endpoints that provide various pieces of translation functionality.</span></span> <span data-ttu-id="b575c-138">The ones used in this tutorial are:</span><span class="sxs-lookup"><span data-stu-id="b575c-138">The ones used in this tutorial are:</span></span>

|||
|-|-|
|`Languages`|<span data-ttu-id="b575c-139">Returns the set of languages currently supported by other operations of the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="b575c-139">Returns the set of languages currently supported by other operations of the Translator Text API.</span></span>|
|`Translate`|<span data-ttu-id="b575c-140">Given source text, a source language code, and a target language code, returns a translation of the source text to the target language.</span><span class="sxs-lookup"><span data-stu-id="b575c-140">Given source text, a source language code, and a target language code, returns a translation of the source text to the target language.</span></span>|

## <a name="the-translation-app"></a><span data-ttu-id="b575c-141">The translation app</span><span class="sxs-lookup"><span data-stu-id="b575c-141">The translation app</span></span>

<span data-ttu-id="b575c-142">The translator application's user interface is built using Windows Presentation Foundation (WPF).</span><span class="sxs-lookup"><span data-stu-id="b575c-142">The translator application's user interface is built using Windows Presentation Foundation (WPF).</span></span> <span data-ttu-id="b575c-143">Create a new WPF project in Visual Studio by following these steps.</span><span class="sxs-lookup"><span data-stu-id="b575c-143">Create a new WPF project in Visual Studio by following these steps.</span></span>

* <span data-ttu-id="b575c-144">From the **File** menu, choose **New > Project**.</span><span class="sxs-lookup"><span data-stu-id="b575c-144">From the **File** menu, choose **New > Project**.</span></span>
* <span data-ttu-id="b575c-145">In the New Project window, open **Installed > Templates > Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="b575c-145">In the New Project window, open **Installed > Templates > Visual C#**.</span></span> <span data-ttu-id="b575c-146">A list of the available project templates appears in the center of the dialog.</span><span class="sxs-lookup"><span data-stu-id="b575c-146">A list of the available project templates appears in the center of the dialog.</span></span>
* <span data-ttu-id="b575c-147">Make sure **.NET Framework 4.5.2** is chosen in the drop-down menu above the project template list.</span><span class="sxs-lookup"><span data-stu-id="b575c-147">Make sure **.NET Framework 4.5.2** is chosen in the drop-down menu above the project template list.</span></span>
* <span data-ttu-id="b575c-148">Click **WPF App (.NET Framework)** in the project template list.</span><span class="sxs-lookup"><span data-stu-id="b575c-148">Click **WPF App (.NET Framework)** in the project template list.</span></span>
* <span data-ttu-id="b575c-149">Using the fields at the bottom of the dialog, name the new project and the solution that contains it.</span><span class="sxs-lookup"><span data-stu-id="b575c-149">Using the fields at the bottom of the dialog, name the new project and the solution that contains it.</span></span>
* <span data-ttu-id="b575c-150">Click **OK** to create the new project and the solution.</span><span class="sxs-lookup"><span data-stu-id="b575c-150">Click **OK** to create the new project and the solution.</span></span>

![[Creating a new WPF app in Visual Studio]](media/translator-text-csharp-new-project.png)

<span data-ttu-id="b575c-152">Add references to the following .NET framework assemblies to your project.</span><span class="sxs-lookup"><span data-stu-id="b575c-152">Add references to the following .NET framework assemblies to your project.</span></span>

* <span data-ttu-id="b575c-153">System.Runtime.Serialization</span><span class="sxs-lookup"><span data-stu-id="b575c-153">System.Runtime.Serialization</span></span>
* <span data-ttu-id="b575c-154">System.Web</span><span class="sxs-lookup"><span data-stu-id="b575c-154">System.Web</span></span>
* <span data-ttu-id="b575c-155">System.Web.Extensions</span><span class="sxs-lookup"><span data-stu-id="b575c-155">System.Web.Extensions</span></span>

<span data-ttu-id="b575c-156">Also, install the NuGet package `Newtonsoft.Json` into your project.</span><span class="sxs-lookup"><span data-stu-id="b575c-156">Also, install the NuGet package `Newtonsoft.Json` into your project.</span></span>

<span data-ttu-id="b575c-157">Now find the `MainWindow.xaml` file in the Solution Explorer and open it.</span><span class="sxs-lookup"><span data-stu-id="b575c-157">Now find the `MainWindow.xaml` file in the Solution Explorer and open it.</span></span> <span data-ttu-id="b575c-158">It's blank initially.</span><span class="sxs-lookup"><span data-stu-id="b575c-158">It's blank initially.</span></span> <span data-ttu-id="b575c-159">Here's what the finished user interface should look like, annotated with the names of the controls in blue.</span><span class="sxs-lookup"><span data-stu-id="b575c-159">Here's what the finished user interface should look like, annotated with the names of the controls in blue.</span></span> <span data-ttu-id="b575c-160">Use the same names for the controls in your user interface, since they also appear in the code.</span><span class="sxs-lookup"><span data-stu-id="b575c-160">Use the same names for the controls in your user interface, since they also appear in the code.</span></span>

![[Annotated view of main window in Visual Studio designer]](media/translator-text-csharp-xaml.png)

> [!NOTE]
> <span data-ttu-id="b575c-162">The source code for this tutorial includes the XAML source for this form.</span><span class="sxs-lookup"><span data-stu-id="b575c-162">The source code for this tutorial includes the XAML source for this form.</span></span> <span data-ttu-id="b575c-163">You may paste it to your project instead of building the form in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b575c-163">You may paste it to your project instead of building the form in Visual Studio.</span></span>

* <span data-ttu-id="b575c-164">`FromLanguageComboBox` *(ComboBox)* - Displays a list of the languages supported by Microsoft Translator for text translation.</span><span class="sxs-lookup"><span data-stu-id="b575c-164">`FromLanguageComboBox` *(ComboBox)* - Displays a list of the languages supported by Microsoft Translator for text translation.</span></span> <span data-ttu-id="b575c-165">The user selects the language they are translating from.</span><span class="sxs-lookup"><span data-stu-id="b575c-165">The user selects the language they are translating from.</span></span>
* <span data-ttu-id="b575c-166">`ToLanguageComboBox` *(ComboBox)* - Displays the same list of languages as `FromComboBox`, but is used to select the language the user is translating to.</span><span class="sxs-lookup"><span data-stu-id="b575c-166">`ToLanguageComboBox` *(ComboBox)* - Displays the same list of languages as `FromComboBox`, but is used to select the language the user is translating to.</span></span>
* <span data-ttu-id="b575c-167">`TextToTranslate` *(TextBox)* - The user enters the text to be translated here.</span><span class="sxs-lookup"><span data-stu-id="b575c-167">`TextToTranslate` *(TextBox)* - The user enters the text to be translated here.</span></span>
* <span data-ttu-id="b575c-168">`TranslateButton` *(Button)* - The user clicks this button (or presses Enter) to translate the text.</span><span class="sxs-lookup"><span data-stu-id="b575c-168">`TranslateButton` *(Button)* - The user clicks this button (or presses Enter) to translate the text.</span></span>
* <span data-ttu-id="b575c-169">`TranslatedTextLabel` *(Label)* - The translation for the user's text appears here.</span><span class="sxs-lookup"><span data-stu-id="b575c-169">`TranslatedTextLabel` *(Label)* - The translation for the user's text appears here.</span></span>

<span data-ttu-id="b575c-170">If you're making your own version of this form, it isn't necessary to make it *exactly* like the one used here.</span><span class="sxs-lookup"><span data-stu-id="b575c-170">If you're making your own version of this form, it isn't necessary to make it *exactly* like the one used here.</span></span> <span data-ttu-id="b575c-171">But make sure the language drop-downs are wide enough to avoid cutting off a language name.</span><span class="sxs-lookup"><span data-stu-id="b575c-171">But make sure the language drop-downs are wide enough to avoid cutting off a language name.</span></span>

## <a name="the-mainwindow-class"></a><span data-ttu-id="b575c-172">The MainWindow class</span><span class="sxs-lookup"><span data-stu-id="b575c-172">The MainWindow class</span></span>

<span data-ttu-id="b575c-173">The code-behind file `MainWindow.xaml.cs` is where the code goes that makes the program do what it does.</span><span class="sxs-lookup"><span data-stu-id="b575c-173">The code-behind file `MainWindow.xaml.cs` is where the code goes that makes the program do what it does.</span></span> <span data-ttu-id="b575c-174">The work happens at two times:</span><span class="sxs-lookup"><span data-stu-id="b575c-174">The work happens at two times:</span></span>

* <span data-ttu-id="b575c-175">When the program starts and `MainWindow` is instantiated, it retrieves the language list using Translator's  and  APIs and populates the drop-down menus with them.</span><span class="sxs-lookup"><span data-stu-id="b575c-175">When the program starts and `MainWindow` is instantiated, it retrieves the language list using Translator's  and  APIs and populates the drop-down menus with them.</span></span> <span data-ttu-id="b575c-176">This task is done once, at the beginning of each session.</span><span class="sxs-lookup"><span data-stu-id="b575c-176">This task is done once, at the beginning of each session.</span></span>

* <span data-ttu-id="b575c-177">When the user clicks the **Translate** button, the user's language selections are retrieved and the text they entered, and then the `Translate` API is called to perform the translation.</span><span class="sxs-lookup"><span data-stu-id="b575c-177">When the user clicks the **Translate** button, the user's language selections are retrieved and the text they entered, and then the `Translate` API is called to perform the translation.</span></span> <span data-ttu-id="b575c-178">Other functions might also be called to determine the language of the text and to correct its spelling before translation.</span><span class="sxs-lookup"><span data-stu-id="b575c-178">Other functions might also be called to determine the language of the text and to correct its spelling before translation.</span></span>

<span data-ttu-id="b575c-179">Take a look at the beginning of the class:</span><span class="sxs-lookup"><span data-stu-id="b575c-179">Take a look at the beginning of the class:</span></span>

```csharp
public partial class MainWindow : Window
{
    // Translator text subscription key from Microsoft Azure dashboard
    const string TEXT_TRANSLATION_API_SUBSCRIPTION_KEY = "ENTER KEY HERE";
    const string TEXT_ANALYTICS_API_SUBSCRIPTION_KEY = "ENTER KEY HERE";
    const string BING_SPELL_CHECK_API_SUBSCRIPTION_KEY = "ENTER KEY HERE";

    public static readonly string TEXT_TRANSLATION_API_ENDPOINT = "https://api.cognitive.microsofttranslator.com/{0}?api-version=3.0";
    const string TEXT_ANALYTICS_API_ENDPOINT = "https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/";
    const string BING_SPELL_CHECK_API_ENDPOINT = "https://api.cognitive.microsoft.com/bing/v7.0/spellcheck/";

    private string[] languageCodes;     // array of language codes

    // Dictionary to map language code from friendly name (sorted case-insensitively on language name)
    private SortedDictionary<string, string> languageCodesAndTitles =
        new SortedDictionary<string, string>(Comparer<string>.Create((a, b) => string.Compare(a, b, true)));

    public MainWindow()
    {
        // at least show an error dialog if there's an unexpected error
        AppDomain.CurrentDomain.UnhandledException += new UnhandledExceptionEventHandler(HandleExceptions);

        if (TEXT_TRANSLATION_API_SUBSCRIPTION_KEY.Length != 32
            || TEXT_ANALYTICS_API_SUBSCRIPTION_KEY.Length != 32
            || BING_SPELL_CHECK_API_SUBSCRIPTION_KEY.Length != 32)
        {
            MessageBox.Show("One or more invalid API subscription keys.\n\n" +
                "Put your keys in the *_API_SUBSCRIPTION_KEY variables in MainWindow.xaml.cs.",
                "Invalid Subscription Key(s)", MessageBoxButton.OK, MessageBoxImage.Error);
            System.Windows.Application.Current.Shutdown();
        }
        else
        {
            InitializeComponent();          // start the GUI
            GetLanguagesForTranslate();     // get codes and friendly names of languages that can be translated
            PopulateLanguageMenus();        // fill the drop-down language lists
        }
    }
// more to come
}
```

<span data-ttu-id="b575c-180">Two member variables declared here hold information about our languages:</span><span class="sxs-lookup"><span data-stu-id="b575c-180">Two member variables declared here hold information about our languages:</span></span>

|||
|-|-|
|`languageCodes`<br><span data-ttu-id="b575c-181">array of string</span><span class="sxs-lookup"><span data-stu-id="b575c-181">array of string</span></span>|<span data-ttu-id="b575c-182">Caches the language codes.</span><span class="sxs-lookup"><span data-stu-id="b575c-182">Caches the language codes.</span></span> <span data-ttu-id="b575c-183">The Translator service uses short codes, such as `en` for English, to identify languages.</span><span class="sxs-lookup"><span data-stu-id="b575c-183">The Translator service uses short codes, such as `en` for English, to identify languages.</span></span>|
|`languageCodesAndTitles`<br><span data-ttu-id="b575c-184">SortedDictionary</span><span class="sxs-lookup"><span data-stu-id="b575c-184">SortedDictionary</span></span>|<span data-ttu-id="b575c-185">Maps the "friendly" names in the user interface back to the short codes used in the API.</span><span class="sxs-lookup"><span data-stu-id="b575c-185">Maps the "friendly" names in the user interface back to the short codes used in the API.</span></span> <span data-ttu-id="b575c-186">Kept sorted alphabetically without regard for case.</span><span class="sxs-lookup"><span data-stu-id="b575c-186">Kept sorted alphabetically without regard for case.</span></span>|

<span data-ttu-id="b575c-187">The first code executed by the application is the `MainWindow` constructor.</span><span class="sxs-lookup"><span data-stu-id="b575c-187">The first code executed by the application is the `MainWindow` constructor.</span></span> <span data-ttu-id="b575c-188">First, set up the method `HandleExceptions` as the global error handler.</span><span class="sxs-lookup"><span data-stu-id="b575c-188">First, set up the method `HandleExceptions` as the global error handler.</span></span> <span data-ttu-id="b575c-189">This way, there is at least an error alert if an exception isn't handled.</span><span class="sxs-lookup"><span data-stu-id="b575c-189">This way, there is at least an error alert if an exception isn't handled.</span></span>

<span data-ttu-id="b575c-190">Next, check to make sure the API subscription keys are all exactly 32 characters long.</span><span class="sxs-lookup"><span data-stu-id="b575c-190">Next, check to make sure the API subscription keys are all exactly 32 characters long.</span></span> <span data-ttu-id="b575c-191">If they aren't, the most likely reason is that *someone* hasn't pasted in their API keys.</span><span class="sxs-lookup"><span data-stu-id="b575c-191">If they aren't, the most likely reason is that *someone* hasn't pasted in their API keys.</span></span> <span data-ttu-id="b575c-192">In this case, display an error message and bail out. (Passing this test doesn't mean the keys are valid, of course.)</span><span class="sxs-lookup"><span data-stu-id="b575c-192">In this case, display an error message and bail out. (Passing this test doesn't mean the keys are valid, of course.)</span></span>

<span data-ttu-id="b575c-193">If there are keys that are at least the right length, the `InitializeComponent()` call gets the user interface rolling by locating, loading, and instantiating the XAML description of the main application window.</span><span class="sxs-lookup"><span data-stu-id="b575c-193">If there are keys that are at least the right length, the `InitializeComponent()` call gets the user interface rolling by locating, loading, and instantiating the XAML description of the main application window.</span></span>

<span data-ttu-id="b575c-194">Finally, set up the language drop-down menus.</span><span class="sxs-lookup"><span data-stu-id="b575c-194">Finally, set up the language drop-down menus.</span></span> <span data-ttu-id="b575c-195">This task requires three separate method calls, which are covered in detail in the following sections.</span><span class="sxs-lookup"><span data-stu-id="b575c-195">This task requires three separate method calls, which are covered in detail in the following sections.</span></span>

## <a name="get-supported-languages"></a><span data-ttu-id="b575c-196">Get supported languages</span><span class="sxs-lookup"><span data-stu-id="b575c-196">Get supported languages</span></span>

<span data-ttu-id="b575c-197">The Microsoft Translator service supports a total of 61 languages at this writing, and more may be added from time to time.</span><span class="sxs-lookup"><span data-stu-id="b575c-197">The Microsoft Translator service supports a total of 61 languages at this writing, and more may be added from time to time.</span></span> <span data-ttu-id="b575c-198">So it's best not to hard-code the supported languages in your program.</span><span class="sxs-lookup"><span data-stu-id="b575c-198">So it's best not to hard-code the supported languages in your program.</span></span> <span data-ttu-id="b575c-199">Instead, ask the Translator service what languages it supports.</span><span class="sxs-lookup"><span data-stu-id="b575c-199">Instead, ask the Translator service what languages it supports.</span></span> <span data-ttu-id="b575c-200">Any supported language can be translated to any other supported language.</span><span class="sxs-lookup"><span data-stu-id="b575c-200">Any supported language can be translated to any other supported language.</span></span>

<span data-ttu-id="b575c-201">Call the `Languages` API to get the list of supported languages.</span><span class="sxs-lookup"><span data-stu-id="b575c-201">Call the `Languages` API to get the list of supported languages.</span></span>

<span data-ttu-id="b575c-202">The `Languages` API takes an optional GET query parameter, *scope*.</span><span class="sxs-lookup"><span data-stu-id="b575c-202">The `Languages` API takes an optional GET query parameter, *scope*.</span></span> <span data-ttu-id="b575c-203">*scope* can have one of three values: `translation`, `transliteration`, and `dictionary`.</span><span class="sxs-lookup"><span data-stu-id="b575c-203">*scope* can have one of three values: `translation`, `transliteration`, and `dictionary`.</span></span> <span data-ttu-id="b575c-204">This code uses the value `translation`.</span><span class="sxs-lookup"><span data-stu-id="b575c-204">This code uses the value `translation`.</span></span>

<span data-ttu-id="b575c-205">The `Languages` API also takes an optional HTTP header, `Accept-Language`.</span><span class="sxs-lookup"><span data-stu-id="b575c-205">The `Languages` API also takes an optional HTTP header, `Accept-Language`.</span></span> <span data-ttu-id="b575c-206">The value of this header determines the language in which the names of the supported languages are returned.</span><span class="sxs-lookup"><span data-stu-id="b575c-206">The value of this header determines the language in which the names of the supported languages are returned.</span></span> <span data-ttu-id="b575c-207">The value should be a well-formed BCP 47 language tag.</span><span class="sxs-lookup"><span data-stu-id="b575c-207">The value should be a well-formed BCP 47 language tag.</span></span> <span data-ttu-id="b575c-208">This code uses the value `en` to get the language names in English.</span><span class="sxs-lookup"><span data-stu-id="b575c-208">This code uses the value `en` to get the language names in English.</span></span>

<span data-ttu-id="b575c-209">The `Languages` API returns a JSON response that looks like the following.</span><span class="sxs-lookup"><span data-stu-id="b575c-209">The `Languages` API returns a JSON response that looks like the following.</span></span>

```json
{
  "translation": {
    "af": {
      "name": "Afrikaans",
      "nativeName": "Afrikaans",
      "dir": "ltr"
    },
    "ar": {
      "name": "Arabic",
      "nativeName": "العربية",
      "dir": "rtl"
    },
...
}
```

<span data-ttu-id="b575c-210">So that language codes (for example, `af`) and language names (for example, `Afrikaans`) can be extracted, this code uses the NewtonSoft.Json method [JsonConvert.DeserializeObject](https://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_JsonConvert_DeserializeObject__1.htm).</span><span class="sxs-lookup"><span data-stu-id="b575c-210">So that language codes (for example, `af`) and language names (for example, `Afrikaans`) can be extracted, this code uses the NewtonSoft.Json method [JsonConvert.DeserializeObject](https://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_JsonConvert_DeserializeObject__1.htm).</span></span>

<span data-ttu-id="b575c-211">With this background knowledge, create the following method to retrieve the language codes and their names.</span><span class="sxs-lookup"><span data-stu-id="b575c-211">With this background knowledge, create the following method to retrieve the language codes and their names.</span></span>

```csharp
private void GetLanguagesForTranslate()
{
    // send request to get supported language codes
    string uri = String.Format(TEXT_TRANSLATION_API_ENDPOINT, "languages") + "&scope=translation";
    WebRequest WebRequest = WebRequest.Create(uri);
    WebRequest.Headers.Add("Ocp-Apim-Subscription-Key", TEXT_TRANSLATION_API_SUBSCRIPTION_KEY);
    WebRequest.Headers.Add("Accept-Language", "en");
    WebResponse response = null;
    // read and parse the JSON response
    response = WebRequest.GetResponse();
    using (var reader = new StreamReader(response.GetResponseStream(), UnicodeEncoding.UTF8))
    {
        var result = JsonConvert.DeserializeObject<Dictionary<string, Dictionary<string, Dictionary<string, string>>>>(reader.ReadToEnd());
        var languages = result["translation"];

        languageCodes = languages.Keys.ToArray();
        foreach (var kv in languages)
        {
            languageCodesAndTitles.Add(kv.Value["name"], kv.Key);
        }
    }
}
```

<span data-ttu-id="b575c-212">`GetLanguagesForTranslate()` first creates the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="b575c-212">`GetLanguagesForTranslate()` first creates the HTTP request.</span></span> <span data-ttu-id="b575c-213">The `scope=translation` query string parameter requests only those languages supported for text translation.</span><span class="sxs-lookup"><span data-stu-id="b575c-213">The `scope=translation` query string parameter requests only those languages supported for text translation.</span></span> <span data-ttu-id="b575c-214">The Text Translation API subscription key is added to the request headers.</span><span class="sxs-lookup"><span data-stu-id="b575c-214">The Text Translation API subscription key is added to the request headers.</span></span> <span data-ttu-id="b575c-215">The `Accept-Language` header with the value `en` is added so that the supported languages are returned in English.</span><span class="sxs-lookup"><span data-stu-id="b575c-215">The `Accept-Language` header with the value `en` is added so that the supported languages are returned in English.</span></span>

<span data-ttu-id="b575c-216">After the request completes, the JSON response is parsed and converted to a Dictionary, and then the language codes are added to the `languageCodes` member variable.</span><span class="sxs-lookup"><span data-stu-id="b575c-216">After the request completes, the JSON response is parsed and converted to a Dictionary, and then the language codes are added to the `languageCodes` member variable.</span></span> <span data-ttu-id="b575c-217">The key/value pairs that contain the language codes and the friendly language names are looped through and added to the `languageCodesAndTitles` member variable.</span><span class="sxs-lookup"><span data-stu-id="b575c-217">The key/value pairs that contain the language codes and the friendly language names are looped through and added to the `languageCodesAndTitles` member variable.</span></span> <span data-ttu-id="b575c-218">(The drop-down menus in the form display the friendly names, but the codes are needed to request the translation.)</span><span class="sxs-lookup"><span data-stu-id="b575c-218">(The drop-down menus in the form display the friendly names, but the codes are needed to request the translation.)</span></span>

## <a name="populate-the-language-menus"></a><span data-ttu-id="b575c-219">Populate the language menus</span><span class="sxs-lookup"><span data-stu-id="b575c-219">Populate the language menus</span></span>

<span data-ttu-id="b575c-220">Most of the user interface is defined in XAML, so you don't need to do much to set it up besides call `InitializeComponent()`.</span><span class="sxs-lookup"><span data-stu-id="b575c-220">Most of the user interface is defined in XAML, so you don't need to do much to set it up besides call `InitializeComponent()`.</span></span> <span data-ttu-id="b575c-221">The only other thing you need to do is add the friendly language names to the **Translate from** and **Translate to** drop-downs, which is done in `PopulateLanguageMenus()`.</span><span class="sxs-lookup"><span data-stu-id="b575c-221">The only other thing you need to do is add the friendly language names to the **Translate from** and **Translate to** drop-downs, which is done in `PopulateLanguageMenus()`.</span></span>

```csharp
private void PopulateLanguageMenus()
{
    // Add option to automatically detect the source language
    FromLanguageComboBox.Items.Add("Detect");

    int count = languageCodesAndTitles.Count;
    foreach (string menuItem in languageCodesAndTitles.Keys)
    {
        FromLanguageComboBox.Items.Add(menuItem);
        ToLanguageComboBox.Items.Add(menuItem);
    }

    // set default languages
    FromLanguageComboBox.SelectedItem = "Detect";
    ToLanguageComboBox.SelectedItem = "English";
}
```

<span data-ttu-id="b575c-222">Populating the menus is a straightforward matter of iterating over the `languageCodesAndTitles` dictionary and adding each key, which is the "friendly" name, to both menus.</span><span class="sxs-lookup"><span data-stu-id="b575c-222">Populating the menus is a straightforward matter of iterating over the `languageCodesAndTitles` dictionary and adding each key, which is the "friendly" name, to both menus.</span></span> <span data-ttu-id="b575c-223">After populating the menus, the default "to" and "from" languages are set to **Detect** (to auto-detect the language) and **English**.</span><span class="sxs-lookup"><span data-stu-id="b575c-223">After populating the menus, the default "to" and "from" languages are set to **Detect** (to auto-detect the language) and **English**.</span></span>

> [!TIP]
> <span data-ttu-id="b575c-224">Without a default selection for the menus, the user can click **Translate** without first choosing a "to" or "from" language.</span><span class="sxs-lookup"><span data-stu-id="b575c-224">Without a default selection for the menus, the user can click **Translate** without first choosing a "to" or "from" language.</span></span> <span data-ttu-id="b575c-225">The defaults eliminate the need to deal with this problem.</span><span class="sxs-lookup"><span data-stu-id="b575c-225">The defaults eliminate the need to deal with this problem.</span></span>

<span data-ttu-id="b575c-226">Now that `MainWindow` has been initialized and the user interface created, the code waits until the user clicks the **Translate**  button.</span><span class="sxs-lookup"><span data-stu-id="b575c-226">Now that `MainWindow` has been initialized and the user interface created, the code waits until the user clicks the **Translate**  button.</span></span>

## <a name="perform-translation"></a><span data-ttu-id="b575c-227">Perform translation</span><span class="sxs-lookup"><span data-stu-id="b575c-227">Perform translation</span></span>

<span data-ttu-id="b575c-228">When the user clicks **Translate**, WPF invokes the `TranslateButton_Click()` event handler, shown here.</span><span class="sxs-lookup"><span data-stu-id="b575c-228">When the user clicks **Translate**, WPF invokes the `TranslateButton_Click()` event handler, shown here.</span></span>

```csharp
private async void TranslateButton_Click(object sender, EventArgs e)
{
    string textToTranslate = TextToTranslate.Text.Trim();

    string fromLanguage = FromLanguageComboBox.SelectedValue.ToString();
    string fromLanguageCode;

    // auto-detect source language if requested
    if (fromLanguage == "Detect")
    {
        fromLanguageCode = DetectLanguage(textToTranslate);
        if (!languageCodes.Contains(fromLanguageCode))
        {
            MessageBox.Show("The source language could not be detected automatically " +
                "or is not supported for translation.", "Language detection failed",
                MessageBoxButton.OK, MessageBoxImage.Error);
            return;
        }
    }
    else
        fromLanguageCode = languageCodesAndTitles[fromLanguage];

    string toLanguageCode = languageCodesAndTitles[ToLanguageComboBox.SelectedValue.ToString()];

    // spell-check the source text if the source language is English
    if (fromLanguageCode == "en")
    {
        if (textToTranslate.StartsWith("-"))    // don't spell check in this case
            textToTranslate = textToTranslate.Substring(1);
        else
        {
            textToTranslate = CorrectSpelling(textToTranslate);
            TextToTranslate.Text = textToTranslate;     // put corrected text into input field
        }
    }

    // handle null operations: no text or same source/target languages
    if (textToTranslate == "" || fromLanguageCode == toLanguageCode)
    {
        TranslatedTextLabel.Content = textToTranslate;
        return;
    }

    // send HTTP request to perform the translation
    string endpoint = string.Format(TEXT_TRANSLATION_API_ENDPOINT, "translate");
    string uri = string.Format(endpoint + "&from={0}&to={1}", fromLanguageCode, toLanguageCode);

    System.Object[] body = new System.Object[] { new { Text = textToTranslate } };
    var requestBody = JsonConvert.SerializeObject(body);

    using (var client = new HttpClient())
    using (var request = new HttpRequestMessage())
    {
        request.Method = HttpMethod.Post;
        request.RequestUri = new Uri(uri);
        request.Content = new StringContent(requestBody, Encoding.UTF8, "application/json");
        request.Headers.Add("Ocp-Apim-Subscription-Key", TEXT_TRANSLATION_API_SUBSCRIPTION_KEY);
        request.Headers.Add("X-ClientTraceId", Guid.NewGuid().ToString());

        var response = await client.SendAsync(request);
        var responseBody = await response.Content.ReadAsStringAsync();

        var result = JsonConvert.DeserializeObject<List<Dictionary<string, List<Dictionary<string, string>>>>>(responseBody);
        var translations = result[0]["translations"];
        var translation = translations[0]["text"];

        // Update the translation field
        TranslatedTextLabel.Content = translation;
    }
}
```

<span data-ttu-id="b575c-229">The first step is to retrieve the "to" and "from" languages, along with the text the user has entered, from the form.</span><span class="sxs-lookup"><span data-stu-id="b575c-229">The first step is to retrieve the "to" and "from" languages, along with the text the user has entered, from the form.</span></span>

<span data-ttu-id="b575c-230">If the source language is set to **Detect**, make a call to `DetectLanguage()` to determine the language of the text.</span><span class="sxs-lookup"><span data-stu-id="b575c-230">If the source language is set to **Detect**, make a call to `DetectLanguage()` to determine the language of the text.</span></span> <span data-ttu-id="b575c-231">The text might be in a language that the Translator APIs don't support (many more languages can be detected than can be translated), or the Text Analytics API might not be able to detect it.</span><span class="sxs-lookup"><span data-stu-id="b575c-231">The text might be in a language that the Translator APIs don't support (many more languages can be detected than can be translated), or the Text Analytics API might not be able to detect it.</span></span> <span data-ttu-id="b575c-232">In that case, display a message to inform the user and return without translating.</span><span class="sxs-lookup"><span data-stu-id="b575c-232">In that case, display a message to inform the user and return without translating.</span></span>

<span data-ttu-id="b575c-233">If the source language is English (whether specified or detected), check the spelling of the text with `CorrectSpelling()` and apply any corrections.</span><span class="sxs-lookup"><span data-stu-id="b575c-233">If the source language is English (whether specified or detected), check the spelling of the text with `CorrectSpelling()` and apply any corrections.</span></span> <span data-ttu-id="b575c-234">The corrected text is stuffed back into the input field so the user knows the correction was made.</span><span class="sxs-lookup"><span data-stu-id="b575c-234">The corrected text is stuffed back into the input field so the user knows the correction was made.</span></span> <span data-ttu-id="b575c-235">(The user may precede the text being translated with a hyphen to suppress spelling correction.)</span><span class="sxs-lookup"><span data-stu-id="b575c-235">(The user may precede the text being translated with a hyphen to suppress spelling correction.)</span></span>

<span data-ttu-id="b575c-236">If the user has not entered any text, or if the "to" and "from" languages are the same, no translation is necessary and the request can be avoided.</span><span class="sxs-lookup"><span data-stu-id="b575c-236">If the user has not entered any text, or if the "to" and "from" languages are the same, no translation is necessary and the request can be avoided.</span></span>

<span data-ttu-id="b575c-237">The code to perform the translation request should look familiar: build the URI, create a request, send it, and parse the response.</span><span class="sxs-lookup"><span data-stu-id="b575c-237">The code to perform the translation request should look familiar: build the URI, create a request, send it, and parse the response.</span></span> <span data-ttu-id="b575c-238">To display the text, send it to the `TranslatedTextLabel` control.</span><span class="sxs-lookup"><span data-stu-id="b575c-238">To display the text, send it to the `TranslatedTextLabel` control.</span></span>

<span data-ttu-id="b575c-239">Next, pass text to the `Translate` API in a serialized JSON array in the body of a POST request.</span><span class="sxs-lookup"><span data-stu-id="b575c-239">Next, pass text to the `Translate` API in a serialized JSON array in the body of a POST request.</span></span> <span data-ttu-id="b575c-240">The JSON array can contain multiple pieces of text to translate, but just one is required here.</span><span class="sxs-lookup"><span data-stu-id="b575c-240">The JSON array can contain multiple pieces of text to translate, but just one is required here.</span></span>

<span data-ttu-id="b575c-241">The HTTP header named `X-ClientTraceId` is optional.</span><span class="sxs-lookup"><span data-stu-id="b575c-241">The HTTP header named `X-ClientTraceId` is optional.</span></span> <span data-ttu-id="b575c-242">The value should be a GUID.</span><span class="sxs-lookup"><span data-stu-id="b575c-242">The value should be a GUID.</span></span> <span data-ttu-id="b575c-243">The client-supplied trace ID is useful to trace requests when things don't work as expected.</span><span class="sxs-lookup"><span data-stu-id="b575c-243">The client-supplied trace ID is useful to trace requests when things don't work as expected.</span></span> <span data-ttu-id="b575c-244">However, to be useful, the value of X-ClientTraceID must be recorded by the client.</span><span class="sxs-lookup"><span data-stu-id="b575c-244">However, to be useful, the value of X-ClientTraceID must be recorded by the client.</span></span> <span data-ttu-id="b575c-245">A client trace ID and the date of requests can help Microsoft diagnose issues that may occur.</span><span class="sxs-lookup"><span data-stu-id="b575c-245">A client trace ID and the date of requests can help Microsoft diagnose issues that may occur.</span></span>

> [!NOTE]
> <span data-ttu-id="b575c-246">This tutorial focuses on the Microsoft Translator service, so the `DetectLanguage()` and `CorrectSpelling()` methods aren't covered in detail.</span><span class="sxs-lookup"><span data-stu-id="b575c-246">This tutorial focuses on the Microsoft Translator service, so the `DetectLanguage()` and `CorrectSpelling()` methods aren't covered in detail.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b575c-247">Next steps</span><span class="sxs-lookup"><span data-stu-id="b575c-247">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b575c-248">Microsoft Translator Text API reference</span><span class="sxs-lookup"><span data-stu-id="b575c-248">Microsoft Translator Text API reference</span></span>](https://docs.microsoft.com/azure/cognitive-services/Translator/reference/v3-0-reference)
