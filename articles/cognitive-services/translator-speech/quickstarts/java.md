---
title: Java Quickstart for Azure Cognitive Services, Microsoft Translator Speech API | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Microsoft Translator Speech API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jaswel
ms.service: cognitive-services
ms.component: translator-speech
ms.topic: article
ms.date: 3/5/2018
ms.author: v-jaswel
ms.openlocfilehash: 8b8019a037d2ef2dabb8a0a5e7e0797400fae9a8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865036"
---
# <a name="quickstart-for-microsoft-translator-speech-api-with-java"></a><span data-ttu-id="0e942-103">Quickstart for Microsoft Translator Speech API with Java</span><span class="sxs-lookup"><span data-stu-id="0e942-103">Quickstart for Microsoft Translator Speech API with Java</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="0e942-104">This article shows you how to use the Microsoft Translator Speech API to translate words spoken in a .wav file.</span><span class="sxs-lookup"><span data-stu-id="0e942-104">This article shows you how to use the Microsoft Translator Speech API to translate words spoken in a .wav file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e942-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0e942-105">Prerequisites</span></span>

<span data-ttu-id="0e942-106">You will need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span><span class="sxs-lookup"><span data-stu-id="0e942-106">You will need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span></span> <span data-ttu-id="0e942-107">You may use a Java IDE if you have a favorite, but a text editor will suffice.</span><span class="sxs-lookup"><span data-stu-id="0e942-107">You may use a Java IDE if you have a favorite, but a text editor will suffice.</span></span>

<span data-ttu-id="0e942-108">You will need the following files.</span><span class="sxs-lookup"><span data-stu-id="0e942-108">You will need the following files.</span></span>
- [<span data-ttu-id="0e942-109">javax.websocket-api-1.1.jar (or newer)</span><span class="sxs-lookup"><span data-stu-id="0e942-109">javax.websocket-api-1.1.jar (or newer)</span></span>](https://mvnrepository.com/artifact/javax.websocket/javax.websocket-api)
- [<span data-ttu-id="0e942-110">jetty-http-9.4.11.v20180605.jar (or newer)</span><span class="sxs-lookup"><span data-stu-id="0e942-110">jetty-http-9.4.11.v20180605.jar (or newer)</span></span>](https://mvnrepository.com/artifact/org.eclipse.jetty/jetty-http)
- [<span data-ttu-id="0e942-111">jetty-io-9.4.11.v20180605.jar (or newer)</span><span class="sxs-lookup"><span data-stu-id="0e942-111">jetty-io-9.4.11.v20180605.jar (or newer)</span></span>](https://mvnrepository.com/artifact/org.eclipse.jetty/jetty-io)
- [<span data-ttu-id="0e942-112">jetty-util-9.4.11.v20180605.jar (or newer)</span><span class="sxs-lookup"><span data-stu-id="0e942-112">jetty-util-9.4.11.v20180605.jar (or newer)</span></span>](https://mvnrepository.com/artifact/org.eclipse.jetty/jetty-util)
- [<span data-ttu-id="0e942-113">websocket-api-9.4.11.v20180605.jar (or newer)</span><span class="sxs-lookup"><span data-stu-id="0e942-113">websocket-api-9.4.11.v20180605.jar (or newer)</span></span>](https://mvnrepository.com/artifact/org.eclipse.jetty.websocket/websocket-api)
- [<span data-ttu-id="0e942-114">websocket-client-9.4.11.v20180605.jar (or newer)</span><span class="sxs-lookup"><span data-stu-id="0e942-114">websocket-client-9.4.11.v20180605.jar (or newer)</span></span>](https://mvnrepository.com/artifact/org.eclipse.jetty.websocket/websocket-client)
- [<span data-ttu-id="0e942-115">websocket-common-9.4.11.v20180605.jar (or newer)</span><span class="sxs-lookup"><span data-stu-id="0e942-115">websocket-common-9.4.11.v20180605.jar (or newer)</span></span>](https://mvnrepository.com/artifact/org.eclipse.jetty.websocket/websocket-common)
- [<span data-ttu-id="0e942-116">javax-websocket-client-impl-9.4.11.v20180605.jar (or newer)</span><span class="sxs-lookup"><span data-stu-id="0e942-116">javax-websocket-client-impl-9.4.11.v20180605.jar (or newer)</span></span>](https://mvnrepository.com/artifact/org.eclipse.jetty.websocket/javax-websocket-client-impl)
- [<span data-ttu-id="0e942-117">jetty-client-9.4.11.v20180605.jar (or newer)</span><span class="sxs-lookup"><span data-stu-id="0e942-117">jetty-client-9.4.11.v20180605.jar (or newer)</span></span>](https://mvnrepository.com/artifact/org.eclipse.jetty/jetty-client)

<span data-ttu-id="0e942-118">You will need a .wav file named "speak.wav" in the same folder as the executable you compile from the code below.</span><span class="sxs-lookup"><span data-stu-id="0e942-118">You will need a .wav file named "speak.wav" in the same folder as the executable you compile from the code below.</span></span> <span data-ttu-id="0e942-119">This .wav file should be in standard PCM, 16bit, 16kHz, mono format.</span><span class="sxs-lookup"><span data-stu-id="0e942-119">This .wav file should be in standard PCM, 16bit, 16kHz, mono format.</span></span> <span data-ttu-id="0e942-120">You can obtain such a .wav file from the [Text to Speech API](https://docs.microsoft.com/en-us/azure/cognitive-services/speech-service/rest-apis#text-to-speech).</span><span class="sxs-lookup"><span data-stu-id="0e942-120">You can obtain such a .wav file from the [Text to Speech API](https://docs.microsoft.com/en-us/azure/cognitive-services/speech-service/rest-apis#text-to-speech).</span></span>

<span data-ttu-id="0e942-121">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft Translator Speech API**.</span><span class="sxs-lookup"><span data-stu-id="0e942-121">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft Translator Speech API**.</span></span> <span data-ttu-id="0e942-122">You will need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span><span class="sxs-lookup"><span data-stu-id="0e942-122">You will need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span></span>

## <a name="translate-speech"></a><span data-ttu-id="0e942-123">Translate speech</span><span class="sxs-lookup"><span data-stu-id="0e942-123">Translate speech</span></span>

<span data-ttu-id="0e942-124">The following code translates speech from one language to another.</span><span class="sxs-lookup"><span data-stu-id="0e942-124">The following code translates speech from one language to another.</span></span>

1. <span data-ttu-id="0e942-125">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="0e942-125">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="0e942-126">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="0e942-126">Add the code provided below.</span></span>
3. <span data-ttu-id="0e942-127">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="0e942-127">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="0e942-128">Run the program.</span><span class="sxs-lookup"><span data-stu-id="0e942-128">Run the program.</span></span>

<span data-ttu-id="0e942-129">Config.java:</span><span class="sxs-lookup"><span data-stu-id="0e942-129">Config.java:</span></span>

```java
import java.util.*;

import javax.websocket.ClientEndpointConfig;

public class Config extends ClientEndpointConfig.Configurator {
    // **********************************************
    // *** Update or verify the following values. ***
    // **********************************************

    // Replace the subscriptionKey string value with your valid subscription key.
    static String key = "ENTER KEY HERE";

    @Override
    public void beforeRequest (Map<String,List<String>> headers) {
        headers.put("Ocp-Apim-Subscription-Key", Arrays.asList (key));
    }
}
```

<span data-ttu-id="0e942-130">Client.java:</span><span class="sxs-lookup"><span data-stu-id="0e942-130">Client.java:</span></span>

```java
import java.io.*;
import java.net.*;
import java.util.*;

import javax.websocket.ClientEndpoint;
import javax.websocket.CloseReason;
import javax.websocket.ContainerProvider;
import javax.websocket.OnClose;
import javax.websocket.OnError;
import javax.websocket.OnMessage;
import javax.websocket.OnOpen;
import javax.websocket.Session;
import javax.websocket.WebSocketContainer;

import org.eclipse.jetty.client.*;
import org.eclipse.jetty.http.*;
import org.eclipse.jetty.io.*;
import org.eclipse.jetty.util.*;
import org.eclipse.jetty.websocket.api.*;
import org.eclipse.jetty.websocket.client.io.*;
import org.eclipse.jetty.websocket.common.scopes.*;

/* Useful reference links:
    https://docs.oracle.com/javaee/7/api/javax/websocket/Session.html
    https://docs.oracle.com/javaee/7/api/javax/websocket/RemoteEndpoint.Basic.html
    https://docs.oracle.com/javaee/7/api/javax/websocket/OnMessage.html
    http://www.oracle.com/technetwork/articles/java/jsr356-1937161.html
*/

@ClientEndpoint(configurator = Config.class)
public class Client {
    static String host = "wss://dev.microsofttranslator.com";
    static String path = "/speech/translate";
    static String params = "?api-version=1.0&from=en-US&to=it-IT&features=texttospeech&voice=it-IT-Elsa";
    static String uri = host + path + params;

    static String input_path = "speak.wav";
    static String output_path = "speak2.wav";

    Session session = null;

    @OnOpen
    public void onOpen(Session session) {
        this.session = session;
        System.out.println ("Connected.");
        SendAudio ();
    }

    @OnMessage
    public void onTextMessage(String message, Session session){
        System.out.println ("Text message received.");
        System.out.println (message);
    }

/*
Use the following signature to receive the message in parts:
    public void onBinaryMessage(byte[] buffer, boolean last, Session session)
Use the following signature to receive the entire message:
    public void onBinaryMessage(byte[] buffer, Session session)
See:
    https://docs.oracle.com/javaee/7/api/javax/websocket/OnMessage.html
*/
    @OnMessage
    public void onBinaryMessage(byte[] buffer, Session session) {
        try {
            System.out.println ("Binary message received.");
            FileOutputStream stream = new FileOutputStream(output_path);
            stream.write(buffer);
            stream.close();
            System.out.println ("Message contents written to file.");
            Close ();
        } catch (Exception e) {
            e.printStackTrace ();
        }
    }

    @OnError
    public void onError(Session session, Throwable e) {
        System.out.println ("Error message received: " + e.getMessage ());
    }

    @OnClose
    public void myOnClose (CloseReason reason) {
        System.out.println ("Close message received: " + reason.getReasonPhrase());
    }

    public void SendAudio() {
        try {
            File file = new File(input_path);
            FileInputStream stream = new FileInputStream (file);
            byte buffer[] = new byte[(int)file.length()];
            stream.read(buffer);
            stream.close();
            sendMessage (buffer);
        } catch (Exception e) {
            e.printStackTrace ();
        }
    }

    public void sendMessage(byte[] message) {
        try {
            System.out.println ("Sending audio.");
            OutputStream stream = this.session.getBasicRemote().getSendStream();
            stream.write (message);
/* Make sure the audio file is followed by silence.
 * This lets the service know that the audio file is finished.
 * At 32 bytes per millisecond, this is 10 seconds of silence. */
            System.out.println ("Sending silence.");
            byte silence[] = new byte[320000];
            stream.write (silence);
            stream.flush();
        } catch (Exception e) {
            e.printStackTrace ();
        }
    }

    public void Connect () throws Exception {
        try {
            System.out.println("Connecting.");
            WebSocketContainer container = ContainerProvider.getWebSocketContainer();
/* The response message might exceed the default max message size of 65536. */
            container.setDefaultMaxBinaryMessageBufferSize(131072);
/* Some code samples show container.connectToServer as returning a Session, but this seems to be false. */
            container.connectToServer(this, new URI(uri));
        } catch (Exception e) {
            e.printStackTrace ();
        }
    }

    public void Close () throws Exception {
        try {
            System.out.println("Closing connection.");
            this.session.close ();
        } catch (Exception e) {
            e.printStackTrace ();
        }
    }
}
```

<span data-ttu-id="0e942-131">Speak.java:</span><span class="sxs-lookup"><span data-stu-id="0e942-131">Speak.java:</span></span>

```java
/*
Download javax.websocket-api-1.1.jar (or newer) from:
    http://central.maven.org/maven2/javax/websocket/javax.websocket-api/1.1/
Download jetty-http-9.4.11.v20180605.jar (or newer) from:
    https://mvnrepository.com/artifact/org.eclipse.jetty/jetty-http
Download jetty-io-9.4.11.v20180605.jar (or newer) from:
    https://mvnrepository.com/artifact/org.eclipse.jetty/jetty-io
Download jetty-util-9.4.11.v20180605.jar (or newer) from:
    https://mvnrepository.com/artifact/org.eclipse.jetty/jetty-util
Download websocket-api-9.4.11.v20180605.jar (or newer) from:
    https://mvnrepository.com/artifact/org.eclipse.jetty.websocket/websocket-api
Download websocket-client-9.4.11.v20180605.jar (or newer) from:
    https://mvnrepository.com/artifact/org.eclipse.jetty.websocket/websocket-client
Download websocket-common-9.4.11.v20180605.jar (or newer) from:
    https://mvnrepository.com/artifact/org.eclipse.jetty.websocket/websocket-common
Download javax-websocket-client-impl-9.4.11.v20180605.jar (or newer) from:
    https://mvnrepository.com/artifact/org.eclipse.jetty.websocket/javax-websocket-client-impl
Download jetty-client-9.4.11.v20180605.jar (or newer) from:
    https://mvnrepository.com/artifact/org.eclipse.jetty/jetty-client

Compile and run with:
    javac Config.java -cp .;javax.websocket-api-1.1.jar
    javac Client.java -cp .;javax.websocket-api-1.1.jar;javax-websocket-client-impl-9.4.11.v20180605.jar;websocket-common-9.4.11.v20180605.jar;jetty-util-9.4.11.v20180605.jar;jetty-io-9.4.11.v20180605.jar;websocket-api-9.4.11.v20180605.jar;websocket-client-9.4.11.v20180605.jar;jetty-client-9.4.11.v20180605.jar;jetty-http-9.4.11.v20180605.jar
    javac Speak.java -cp .;javax.websocket-api-1.1.jar;javax-websocket-client-impl-9.4.11.v20180605.jar;websocket-common-9.4.11.v20180605.jar;jetty-util-9.4.11.v20180605.jar;jetty-io-9.4.11.v20180605.jar;websocket-api-9.4.11.v20180605.jar;websocket-client-9.4.11.v20180605.jar;jetty-client-9.4.11.v20180605.jar;jetty-http-9.4.11.v20180605.jar
    java -cp .;javax.websocket-api-1.1.jar;javax-websocket-client-impl-9.4.11.v20180605.jar;websocket-common-9.4.11.v20180605.jar;jetty-util-9.4.11.v20180605.jar;jetty-io-9.4.11.v20180605.jar;websocket-api-9.4.11.v20180605.jar;websocket-client-9.4.11.v20180605.jar;jetty-client-9.4.11.v20180605.jar;jetty-http-9.4.11.v20180605.jar Speak
*/

import java.lang.Thread;

public class Speak {
    public static void main(String[] args) {
        try {
            Client client = new Client ();
            client.Connect ();
            // Wait for the reply.
            Thread.sleep (5000);
            System.out.println ("Press Enter to exit the application at any time.");
            System.in.read();
        }
        catch (Exception e) {
            System.out.println (e);
        }
    }
}
```

<span data-ttu-id="0e942-132">**Translate speech response**</span><span class="sxs-lookup"><span data-stu-id="0e942-132">**Translate speech response**</span></span>

<span data-ttu-id="0e942-133">A successful result is the creation of a file named "speak2.wav".</span><span class="sxs-lookup"><span data-stu-id="0e942-133">A successful result is the creation of a file named "speak2.wav".</span></span> <span data-ttu-id="0e942-134">The file contains the translation of the words spoken in "speak.wav".</span><span class="sxs-lookup"><span data-stu-id="0e942-134">The file contains the translation of the words spoken in "speak.wav".</span></span>

[<span data-ttu-id="0e942-135">Back to top</span><span class="sxs-lookup"><span data-stu-id="0e942-135">Back to top</span></span>](#HOLTop)

## <a name="next-steps"></a><span data-ttu-id="0e942-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="0e942-136">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0e942-137">Translator Speech tutorial</span><span class="sxs-lookup"><span data-stu-id="0e942-137">Translator Speech tutorial</span></span>](../tutorial-translator-speech-csharp.md)

## <a name="see-also"></a><span data-ttu-id="0e942-138">See also</span><span class="sxs-lookup"><span data-stu-id="0e942-138">See also</span></span> 

<span data-ttu-id="0e942-139">[Translator Speech overview](../overview.md)
[API Reference](https://docs.microsoft.com/azure/cognitive-services/translator-speech/reference)</span><span class="sxs-lookup"><span data-stu-id="0e942-139">[Translator Speech overview](../overview.md)
[API Reference](https://docs.microsoft.com/azure/cognitive-services/translator-speech/reference)</span></span>
