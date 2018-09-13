---
title: C# Quickstart for Azure Cognitive Services, Microsoft Translator Speech API | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Microsoft Translator Speech API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jaswel
ms.service: cognitive-services
ms.component: translator-speech
ms.topic: article
ms.date: 3/5/2018
ms.author: v-jaswel
ms.openlocfilehash: 23e1f74e0920a114b2f9717f46d1c5191c01dcb1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856100"
---
# <a name="quickstart-for-microsoft-translator-speech-api-with-c"></a><span data-ttu-id="8c693-103">Quickstart for Microsoft Translator Speech API with C#</span><span class="sxs-lookup"><span data-stu-id="8c693-103">Quickstart for Microsoft Translator Speech API with C#</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="8c693-104">This article shows you how to use the Microsoft Translator Speech API to translate words spoken in a .wav file.</span><span class="sxs-lookup"><span data-stu-id="8c693-104">This article shows you how to use the Microsoft Translator Speech API to translate words spoken in a .wav file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c693-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8c693-105">Prerequisites</span></span>

<span data-ttu-id="8c693-106">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span><span class="sxs-lookup"><span data-stu-id="8c693-106">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span></span> <span data-ttu-id="8c693-107">(The free Community Edition will work.)</span><span class="sxs-lookup"><span data-stu-id="8c693-107">(The free Community Edition will work.)</span></span>

<span data-ttu-id="8c693-108">You will need a .wav file named "speak.wav" in the same folder as the executable you compile from the code below.</span><span class="sxs-lookup"><span data-stu-id="8c693-108">You will need a .wav file named "speak.wav" in the same folder as the executable you compile from the code below.</span></span> <span data-ttu-id="8c693-109">This .wav file should be in standard PCM, 16bit, 16kHz, mono format.</span><span class="sxs-lookup"><span data-stu-id="8c693-109">This .wav file should be in standard PCM, 16bit, 16kHz, mono format.</span></span>

<span data-ttu-id="8c693-110">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft Translator Speech API**.</span><span class="sxs-lookup"><span data-stu-id="8c693-110">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft Translator Speech API**.</span></span> <span data-ttu-id="8c693-111">You will need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span><span class="sxs-lookup"><span data-stu-id="8c693-111">You will need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span></span>

## <a name="translate-speech"></a><span data-ttu-id="8c693-112">Translate speech</span><span class="sxs-lookup"><span data-stu-id="8c693-112">Translate speech</span></span>

<span data-ttu-id="8c693-113">The following code translates speech from one language to another.</span><span class="sxs-lookup"><span data-stu-id="8c693-113">The following code translates speech from one language to another.</span></span>

1. <span data-ttu-id="8c693-114">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="8c693-114">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="8c693-115">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8c693-115">Add the code provided below.</span></span>
3. <span data-ttu-id="8c693-116">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8c693-116">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="8c693-117">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8c693-117">Run the program.</span></span>

```csharp
using System;
using System.IO;
using System.Net.WebSockets;
using System.Text;
using System.Threading;
using System.Threading.Tasks;

namespace TranslateSpeechQuickStart
{
    class Program
    {
        static string host = "wss://dev.microsofttranslator.com";
        static string path = "/speech/translate";

        // NOTE: Replace this example key with a valid subscription key.
        static string key = "ENTER KEY HERE";

        async static Task Send (ClientWebSocket client, string input_path)
        {
            var audio = File.ReadAllBytes(input_path);
            var audio_out_buffer = new ArraySegment<byte>(audio);
            Console.WriteLine("Sending audio.");
            await client.SendAsync(audio_out_buffer, WebSocketMessageType.Binary, true, CancellationToken.None);

            /* Make sure the audio file is followed by silence.
             * This lets the service know that the audio input is finished. */
            var silence = new byte[3200000];
            var silence_buffer = new ArraySegment<byte>(silence);
            await client.SendAsync(silence_buffer, WebSocketMessageType.Binary, true, CancellationToken.None);

            Console.WriteLine("Done sending.");
            await client.CloseAsync(WebSocketCloseStatus.NormalClosure, "", CancellationToken.None);
        }

        async static Task Receive(ClientWebSocket client, string output_path)
        {
            var inbuf = new byte[102400];
            var segment = new ArraySegment<byte>(inbuf);
            var stream = new FileStream(output_path, FileMode.Create);

            Console.WriteLine("Awaiting response.");
            while (client.State == WebSocketState.Open)
            {
                var result = await client.ReceiveAsync(segment, CancellationToken.None);
                switch (result.MessageType)
                {
                    case WebSocketMessageType.Close:
                        Console.WriteLine("Received close message. Status: " + result.CloseStatus + ". Description: " + result.CloseStatusDescription);
                        await client.CloseAsync(WebSocketCloseStatus.NormalClosure, string.Empty, CancellationToken.None);
                        break;
                    case WebSocketMessageType.Text:
                        Console.WriteLine("Received text.");
                        Console.WriteLine(Encoding.UTF8.GetString(inbuf).TrimEnd('\0'));
                        break;
                    case WebSocketMessageType.Binary:
                        Console.WriteLine("Received binary data: " + result.Count + " bytes.");
                        stream.Write(inbuf, 0, result.Count);
                        break;
                }
            }

            stream.Close();
            stream.Dispose();
        }

        async static void TranslateSpeech()
        {
            var client = new ClientWebSocket();
            client.Options.SetRequestHeader ("Ocp-Apim-Subscription-Key", key);

            string from = "en-US";
            string to = "it-IT";
            string features = "texttospeech";
            string voice = "it-IT-Elsa";
            string api = "1.0";

            string input_path = "speak.wav";
            string output_path = "speak2.wav";

            string uri = host + path +
                "?from=" + from +
                "&to=" + to +
                "&api-version=" + api +
                "&features=" + features +
                "&voice=" + voice;

            Console.WriteLine("uri: " + uri);
            Console.WriteLine("Opening connection.");
            await client.ConnectAsync(new Uri(uri), CancellationToken.None);
            Console.WriteLine("Connection open.");
            Task.WhenAll(Send(client, input_path), Receive(client, output_path)).Wait();
        }

        static void Main()
        {
            TranslateSpeech();
            Console.ReadLine();
        }

    }
}
```

<span data-ttu-id="8c693-118">**Translate speech response**</span><span class="sxs-lookup"><span data-stu-id="8c693-118">**Translate speech response**</span></span>

<span data-ttu-id="8c693-119">A successful result is the creation of a file named "speak2.wav".</span><span class="sxs-lookup"><span data-stu-id="8c693-119">A successful result is the creation of a file named "speak2.wav".</span></span> <span data-ttu-id="8c693-120">The file contains the translation of the words spoken in "speak.wav".</span><span class="sxs-lookup"><span data-stu-id="8c693-120">The file contains the translation of the words spoken in "speak.wav".</span></span>

[<span data-ttu-id="8c693-121">Back to top</span><span class="sxs-lookup"><span data-stu-id="8c693-121">Back to top</span></span>](#HOLTop)

## <a name="next-steps"></a><span data-ttu-id="8c693-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="8c693-122">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8c693-123">Translator Speech tutorial</span><span class="sxs-lookup"><span data-stu-id="8c693-123">Translator Speech tutorial</span></span>](../tutorial-translator-speech-csharp.md)

## <a name="see-also"></a><span data-ttu-id="8c693-124">See also</span><span class="sxs-lookup"><span data-stu-id="8c693-124">See also</span></span> 

<span data-ttu-id="8c693-125">[Translator Speech overview](../overview.md)
[API Reference](https://docs.microsoft.com/azure/cognitive-services/translator-speech/reference)</span><span class="sxs-lookup"><span data-stu-id="8c693-125">[Translator Speech overview](../overview.md)
[API Reference](https://docs.microsoft.com/azure/cognitive-services/translator-speech/reference)</span></span>
