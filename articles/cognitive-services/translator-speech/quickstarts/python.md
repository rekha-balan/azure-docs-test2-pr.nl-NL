---
title: Python Quickstart for Azure Cognitive Services, Microsoft Translator Speech API | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Microsoft Translator Speech API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jaswel
ms.service: cognitive-services
ms.component: translator-speech
ms.topic: article
ms.date: 07/17/2018
ms.author: v-jaswel
ms.openlocfilehash: 3d9740e268cf48be771ccd6a69e63db3ade8e2a6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966596"
---
# <a name="quickstart-for-microsoft-translator-speech-api-with-python"></a><span data-ttu-id="d1211-103">Quickstart for Microsoft Translator Speech API with Python</span><span class="sxs-lookup"><span data-stu-id="d1211-103">Quickstart for Microsoft Translator Speech API with Python</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="d1211-104">This article shows you how to use the Microsoft Translator Speech API to translate words spoken in a .wav file.</span><span class="sxs-lookup"><span data-stu-id="d1211-104">This article shows you how to use the Microsoft Translator Speech API to translate words spoken in a .wav file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1211-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d1211-105">Prerequisites</span></span>

<span data-ttu-id="d1211-106">You will need [Python 3.x](https://www.python.org/downloads/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="d1211-106">You will need [Python 3.x](https://www.python.org/downloads/) to run this code.</span></span>

<span data-ttu-id="d1211-107">You will need to install the [websocket-client package](https://pypi.python.org/pypi/websocket-client) for Python.</span><span class="sxs-lookup"><span data-stu-id="d1211-107">You will need to install the [websocket-client package](https://pypi.python.org/pypi/websocket-client) for Python.</span></span>

<span data-ttu-id="d1211-108">You will need a .wav file named "speak.wav" in the same folder as the executable you compile from the code below.</span><span class="sxs-lookup"><span data-stu-id="d1211-108">You will need a .wav file named "speak.wav" in the same folder as the executable you compile from the code below.</span></span> <span data-ttu-id="d1211-109">This .wav file should be in standard PCM, 16bit, 16kHz, mono format.</span><span class="sxs-lookup"><span data-stu-id="d1211-109">This .wav file should be in standard PCM, 16bit, 16kHz, mono format.</span></span> 

<span data-ttu-id="d1211-110">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft Translator Speech API**.</span><span class="sxs-lookup"><span data-stu-id="d1211-110">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft Translator Speech API**.</span></span> <span data-ttu-id="d1211-111">You will need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span><span class="sxs-lookup"><span data-stu-id="d1211-111">You will need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span></span>

## <a name="translate-speech"></a><span data-ttu-id="d1211-112">Translate speech</span><span class="sxs-lookup"><span data-stu-id="d1211-112">Translate speech</span></span>

<span data-ttu-id="d1211-113">The following code translates speech from one language to another.</span><span class="sxs-lookup"><span data-stu-id="d1211-113">The following code translates speech from one language to another.</span></span>

1. <span data-ttu-id="d1211-114">Create a new Python project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="d1211-114">Create a new Python project in your favorite IDE.</span></span>
2. <span data-ttu-id="d1211-115">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="d1211-115">Add the code provided below.</span></span>
3. <span data-ttu-id="d1211-116">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="d1211-116">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="d1211-117">Run the program.</span><span class="sxs-lookup"><span data-stu-id="d1211-117">Run the program.</span></span>

```python
# -*- coding: utf-8 -*-

# To install this package, run:
#   pip install websocket-client
import websocket

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace the subscriptionKey string value with your valid subscription key.
key = 'ENTER KEY HERE'

host = 'wss://dev.microsofttranslator.com'
path = '/speech/translate';
params = '?api-version=1.0&from=en-US&to=it-IT&features=texttospeech&voice=it-IT-Elsa'
uri = host + path + params

input_file = 'speak.wav'
output_file = 'speak2.wav'

output = bytearray ()

def on_open (client):
    print ("Connected.")

# r = read. b = binary.
    with open (input_file, mode='rb') as file:
        data = file.read()

    print ("Sending audio.")
    client.send (data, websocket.ABNF.OPCODE_BINARY)
# Make sure the audio file is followed by silence.
# This lets the service know that the audio input is finished.
    print ("Sending silence.")
    client.send (bytearray (32000), websocket.ABNF.OPCODE_BINARY)

def on_data (client, message, message_type, is_last):
    global output
    if (websocket.ABNF.OPCODE_TEXT == message_type):
        print ("Received text data.")
        print (message)
# For some reason, we receive the data as type websocket.ABNF.OPCODE_CONT.
    elif (websocket.ABNF.OPCODE_BINARY == message_type or websocket.ABNF.OPCODE_CONT == message_type):
        print ("Received binary data.")
        print ("Is last? " + str(is_last))
        output = output + message
        if (True == is_last):
# w = write. b = binary.
            with open (output_file, mode='wb') as file:
                file.write (output)
                print ("Wrote data to output file.")
            client.close ()
    else:
        print ("Received data of type: " + str (message_type))

def on_error (client, error):
    print ("Connection error: " + str (error))

def on_close (client):
    print ("Connection closed.")

client = websocket.WebSocketApp(
    uri,
    header=[
        'Ocp-Apim-Subscription-Key: ' + key
    ],
    on_open=on_open,
    on_data=on_data,
    on_error=on_error,
    on_close=on_close
)

print ("Connecting...")
client.run_forever()
```

<span data-ttu-id="d1211-118">**Translate speech response**</span><span class="sxs-lookup"><span data-stu-id="d1211-118">**Translate speech response**</span></span>

<span data-ttu-id="d1211-119">A successful result is the creation of a file named "speak2.wav".</span><span class="sxs-lookup"><span data-stu-id="d1211-119">A successful result is the creation of a file named "speak2.wav".</span></span> <span data-ttu-id="d1211-120">The file contains the translation of the words spoken in "speak.wav".</span><span class="sxs-lookup"><span data-stu-id="d1211-120">The file contains the translation of the words spoken in "speak.wav".</span></span>

[<span data-ttu-id="d1211-121">Back to top</span><span class="sxs-lookup"><span data-stu-id="d1211-121">Back to top</span></span>](#HOLTop)

## <a name="next-steps"></a><span data-ttu-id="d1211-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="d1211-122">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d1211-123">Translator Speech tutorial</span><span class="sxs-lookup"><span data-stu-id="d1211-123">Translator Speech tutorial</span></span>](../tutorial-translator-speech-csharp.md)

## <a name="see-also"></a><span data-ttu-id="d1211-124">See also</span><span class="sxs-lookup"><span data-stu-id="d1211-124">See also</span></span> 

<span data-ttu-id="d1211-125">[Translator Speech overview](../overview.md)
[API Reference](https://docs.microsoft.com/azure/cognitive-services/translator-speech/reference)</span><span class="sxs-lookup"><span data-stu-id="d1211-125">[Translator Speech overview](../overview.md)
[API Reference](https://docs.microsoft.com/azure/cognitive-services/translator-speech/reference)</span></span>
