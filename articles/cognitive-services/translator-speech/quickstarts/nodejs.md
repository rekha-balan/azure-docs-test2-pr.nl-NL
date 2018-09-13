---
title: Node.js Quickstart for Azure Cognitive Services, Microsoft Translator Speech API | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Microsoft Translator Speech API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jaswel
ms.service: cognitive-services
ms.component: translator-speech
ms.topic: article
ms.date: 3/5/2018
ms.author: v-jaswel
ms.openlocfilehash: 7fbf435305da0c290fc3e8cf9b0370e83a8b516f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857644"
---
# <a name="quickstart-for-microsoft-translator-speech-api-with-nodejs"></a><span data-ttu-id="42dcd-103">Quickstart for Microsoft Translator Speech API with Node.js</span><span class="sxs-lookup"><span data-stu-id="42dcd-103">Quickstart for Microsoft Translator Speech API with Node.js</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="42dcd-104">This article shows you how to use the Microsoft Translator Speech API to translate words spoken in a .wav file.</span><span class="sxs-lookup"><span data-stu-id="42dcd-104">This article shows you how to use the Microsoft Translator Speech API to translate words spoken in a .wav file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42dcd-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="42dcd-105">Prerequisites</span></span>

<span data-ttu-id="42dcd-106">You need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="42dcd-106">You need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span></span>

<span data-ttu-id="42dcd-107">You need to install the [Websocket package](https://www.npmjs.com/package/websocket) for Node.js.</span><span class="sxs-lookup"><span data-stu-id="42dcd-107">You need to install the [Websocket package](https://www.npmjs.com/package/websocket) for Node.js.</span></span>

<span data-ttu-id="42dcd-108">You need a .wav file named "speak.wav" in the same folder as the executable you compile from the code below.</span><span class="sxs-lookup"><span data-stu-id="42dcd-108">You need a .wav file named "speak.wav" in the same folder as the executable you compile from the code below.</span></span> <span data-ttu-id="42dcd-109">This .wav file should be in standard PCM, 16 bit, 16 kHz, mono format.</span><span class="sxs-lookup"><span data-stu-id="42dcd-109">This .wav file should be in standard PCM, 16 bit, 16 kHz, mono format.</span></span> <span data-ttu-id="42dcd-110">You can obtain such a .wav file from the [Text to Speech API](https://docs.microsoft.com/en-us/azure/cognitive-services/speech-service/rest-apis#text-to-speech).</span><span class="sxs-lookup"><span data-stu-id="42dcd-110">You can obtain such a .wav file from the [Text to Speech API](https://docs.microsoft.com/en-us/azure/cognitive-services/speech-service/rest-apis#text-to-speech).</span></span>

<span data-ttu-id="42dcd-111">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft Translator Speech API**.</span><span class="sxs-lookup"><span data-stu-id="42dcd-111">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft Translator Speech API**.</span></span> <span data-ttu-id="42dcd-112">You need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span><span class="sxs-lookup"><span data-stu-id="42dcd-112">You need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span></span>

## <a name="translate-speech"></a><span data-ttu-id="42dcd-113">Translate speech</span><span class="sxs-lookup"><span data-stu-id="42dcd-113">Translate speech</span></span>

<span data-ttu-id="42dcd-114">The following code translates speech from one language to another.</span><span class="sxs-lookup"><span data-stu-id="42dcd-114">The following code translates speech from one language to another.</span></span>

1. <span data-ttu-id="42dcd-115">Create a new Node.js project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="42dcd-115">Create a new Node.js project in your favorite IDE.</span></span>
2. <span data-ttu-id="42dcd-116">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="42dcd-116">Add the code provided below.</span></span>
3. <span data-ttu-id="42dcd-117">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="42dcd-117">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="42dcd-118">Run the program.</span><span class="sxs-lookup"><span data-stu-id="42dcd-118">Run the program.</span></span>

```nodejs
/* To install this dependency, run:
npm install websocket
*/
var wsClient = require('websocket').client;
var fs = require('fs');
/* To install this dependency, run:
npm install stream-buffers
*/
var streamBuffers = require('stream-buffers');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the subscriptionKey string value with your valid subscription key.
let key = 'ENTER KEY HERE';

let host = 'wss://dev.microsofttranslator.com';
let path = '/speech/translate';
let params = '?api-version=1.0&from=en-US&to=it-IT&features=texttospeech&voice=it-IT-Elsa';
let uri = host + path + params;

/* The input .wav file is in PCM 16bit, 16kHz, mono format.
You can obtain such a .wav file using the Text to Speech API. See:
https://docs.microsoft.com/en-us/azure/cognitive-services/speech-service/rest-apis#text-to-speech
*/
let input_path = 'speak.wav';

let output_path = 'speak2.wav';

function receive(message) {
    console.log ("Received message of type: " + message.type + ".");

    if (message.type == 'utf8') {
        var result = JSON.parse(message.utf8Data)
        console.log("Response type: " + result.type + ".");
        console.log("Recognized input as: " + result.recognition);
        console.log("Translation: " + result.translation);
    }
    else if (message.type == 'binary') {
/* This is needed to make sure message.binaryData is defined. See:
https://stackoverflow.com/questions/17546953/cant-access-object-property-even-though-it-exists-returns-undefined
*/
        let binary_data = JSON.parse (JSON.stringify (message.binaryData));

        if (binary_data.type == 'Buffer') {
/* Put the binary data in a Buffer - do not write it directly to the file. */
            let buffer = new Buffer(binary_data.data, 'binary');
/* Write the contents of the Buffer to the file. */
            fs.writeFile (output_path, buffer, 'binary', function (error) {
/* fs.writeFile calls the error-handling function even if there is no error, in which case error === null. See:
https://stackoverflow.com/questions/44473868/node-js-fs-writefile-err-returns-null
*/
                if (error !== null) {
                    console.log ("Error: " + error);
                }
            });
        }
    }
}

function send(connection, filename) {
    
    var myReadableStreamBuffer = new streamBuffers.ReadableStreamBuffer({
        frequency: 100,
        chunkSize: 32000
    });

/* Make sure the audio file is followed by silence.
This lets the service know that the audio file is finished.
At 32 bytes per millisecond, this is 100 seconds of silence. */
    myReadableStreamBuffer.put(fs.readFileSync(filename));
    myReadableStreamBuffer.put(new Buffer(3200000));
    myReadableStreamBuffer.stop();

    myReadableStreamBuffer.on('data', function (data) {
        connection.sendBytes(data);
    });

    myReadableStreamBuffer.on('end', function () {
        console.log('Closing connection.');
        connection.close(1000);
    });
}

function connect() {
    var ws = new wsClient();

    ws.on('connectFailed', function (error) {
        console.log('Connection error: ' + error.toString());
    });
                            
    ws.on('connect', function (connection) {
        console.log('Connected.');

        connection.on('message', receive);
        
        connection.on('close', function (reasonCode, description) {
            console.log('Connection closed: ' + reasonCode);
        });

        connection.on('error', function (error) {
            console.log('Connection error: ' + error.toString());
        });
        
        send(connection, input_path);
    });

    ws.connect(uri, null, null, { 'Ocp-Apim-Subscription-Key' : key });
}

connect();
```

<span data-ttu-id="42dcd-119">**Translate speech response**</span><span class="sxs-lookup"><span data-stu-id="42dcd-119">**Translate speech response**</span></span>

<span data-ttu-id="42dcd-120">A successful result is the creation of a file named "speak2.wav".</span><span class="sxs-lookup"><span data-stu-id="42dcd-120">A successful result is the creation of a file named "speak2.wav".</span></span> <span data-ttu-id="42dcd-121">The file contains the translation of the words spoken in "speak.wav".</span><span class="sxs-lookup"><span data-stu-id="42dcd-121">The file contains the translation of the words spoken in "speak.wav".</span></span>

[<span data-ttu-id="42dcd-122">Back to top</span><span class="sxs-lookup"><span data-stu-id="42dcd-122">Back to top</span></span>](#HOLTop)

## <a name="next-steps"></a><span data-ttu-id="42dcd-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="42dcd-123">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="42dcd-124">Translator Speech tutorial</span><span class="sxs-lookup"><span data-stu-id="42dcd-124">Translator Speech tutorial</span></span>](../tutorial-translator-speech-csharp.md)

## <a name="see-also"></a><span data-ttu-id="42dcd-125">See also</span><span class="sxs-lookup"><span data-stu-id="42dcd-125">See also</span></span> 

<span data-ttu-id="42dcd-126">[Translator Speech overview](../overview.md)
[API Reference](https://docs.microsoft.com/azure/cognitive-services/translator-speech/reference)</span><span class="sxs-lookup"><span data-stu-id="42dcd-126">[Translator Speech overview](../overview.md)
[API Reference](https://docs.microsoft.com/azure/cognitive-services/translator-speech/reference)</span></span>
