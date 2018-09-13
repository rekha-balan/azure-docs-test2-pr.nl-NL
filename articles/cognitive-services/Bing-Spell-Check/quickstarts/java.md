---
title: Java Quickstart for Bing Spell Check API - Azure Cognitive Services | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Bing Spell Check API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jaswel
ms.service: cognitive-services
ms.component: bing-spell-check
ms.topic: quickstart
ms.date: 09/14/2017
ms.author: v-jaswel
ms.openlocfilehash: 2d4b4cb8904e973e8642c4d61c29b88ec4446bfb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870306"
---
# <a name="quickstart-for-bing-spell-check-api-with-java"></a><span data-ttu-id="7aa55-103">Quickstart for Bing Spell Check API with Java</span><span class="sxs-lookup"><span data-stu-id="7aa55-103">Quickstart for Bing Spell Check API with Java</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="7aa55-104">This article shows you how to use the [Bing Spell Check API](https://azure.microsoft.com/services/cognitive-services/spell-check/) with Java.</span><span class="sxs-lookup"><span data-stu-id="7aa55-104">This article shows you how to use the [Bing Spell Check API](https://azure.microsoft.com/services/cognitive-services/spell-check/) with Java.</span></span> <span data-ttu-id="7aa55-105">The Spell Check API returns a list of words it does not recognize along with suggested replacements.</span><span class="sxs-lookup"><span data-stu-id="7aa55-105">The Spell Check API returns a list of words it does not recognize along with suggested replacements.</span></span> <span data-ttu-id="7aa55-106">Typically, you would submit text to this API and then either make the suggested replacements in the text or show them to the user of your application so they can decide whether to make the replacements.</span><span class="sxs-lookup"><span data-stu-id="7aa55-106">Typically, you would submit text to this API and then either make the suggested replacements in the text or show them to the user of your application so they can decide whether to make the replacements.</span></span> <span data-ttu-id="7aa55-107">This article shows how to send a request that contains the text "Hollo, wrld!".</span><span class="sxs-lookup"><span data-stu-id="7aa55-107">This article shows how to send a request that contains the text "Hollo, wrld!".</span></span> <span data-ttu-id="7aa55-108">The suggested replacements will be "Hello" and "world."</span><span class="sxs-lookup"><span data-stu-id="7aa55-108">The suggested replacements will be "Hello" and "world."</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7aa55-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7aa55-109">Prerequisites</span></span>

<span data-ttu-id="7aa55-110">You will need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span><span class="sxs-lookup"><span data-stu-id="7aa55-110">You will need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span></span> <span data-ttu-id="7aa55-111">You may use a Java IDE if you have a favorite, but a text editor will suffice.</span><span class="sxs-lookup"><span data-stu-id="7aa55-111">You may use a Java IDE if you have a favorite, but a text editor will suffice.</span></span>

<span data-ttu-id="7aa55-112">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Spell Check API v7**.</span><span class="sxs-lookup"><span data-stu-id="7aa55-112">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Spell Check API v7**.</span></span> <span data-ttu-id="7aa55-113">The [free trial](https://azure.microsoft.com/try/cognitive-services/#lang) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="7aa55-113">The [free trial](https://azure.microsoft.com/try/cognitive-services/#lang) is sufficient for this quickstart.</span></span> <span data-ttu-id="7aa55-114">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="7aa55-114">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="get-spell-check-results"></a><span data-ttu-id="7aa55-115">Get Spell Check results</span><span class="sxs-lookup"><span data-stu-id="7aa55-115">Get Spell Check results</span></span>

1. <span data-ttu-id="7aa55-116">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="7aa55-116">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="7aa55-117">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="7aa55-117">Add the code provided below.</span></span>
3. <span data-ttu-id="7aa55-118">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="7aa55-118">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="7aa55-119">Run the program.</span><span class="sxs-lookup"><span data-stu-id="7aa55-119">Run the program.</span></span>

```java
import java.io.*;
import java.net.*;
import javax.net.ssl.HttpsURLConnection;

public class HelloWorld {

    static String host = "https://api.cognitive.microsoft.com";
    static String path = "/bing/v7.0/spellcheck";

    // NOTE: Replace this example key with a valid subscription key.
    static String key = "ENTER KEY HERE";

    static String mkt = "en-US";
    static String mode = "proof";
    static String text = "Hollo, wrld!";

    public static void check () throws Exception {
        String params = "?mkt=" + mkt + "&mode=" + mode;
        URL url = new URL(host + path + params);
        HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
        connection.setRequestMethod("POST");
        connection.setRequestProperty("Content-Type", "application/x-www-form-urlencoded");
        connection.setRequestProperty("Content-Length", "" + text.length() + 5);
        connection.setRequestProperty("Ocp-Apim-Subscription-Key", key);
        connection.setDoOutput(true);

        DataOutputStream wr = new DataOutputStream(connection.getOutputStream());
        wr.writeBytes("text=" + text);
        wr.flush();
        wr.close();

        BufferedReader in = new BufferedReader(
        new InputStreamReader(connection.getInputStream()));
        String line;
        while ((line = in.readLine()) != null) {
            System.out.println(line);
        }
        in.close();
    }

    public static void main(String[] args) {
        try {
            check ();
        }
        catch (Exception e) {
            System.out.println (e);
        }
    }
}
```

<span data-ttu-id="7aa55-120">**Response**</span><span class="sxs-lookup"><span data-stu-id="7aa55-120">**Response**</span></span>

<span data-ttu-id="7aa55-121">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="7aa55-121">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
   "_type": "SpellCheck",
   "flaggedTokens": [
      {
         "offset": 0,
         "token": "Hollo",
         "type": "UnknownToken",
         "suggestions": [
            {
               "suggestion": "Hello",
               "score": 0.9115257530801
            },
            {
               "suggestion": "Hollow",
               "score": 0.858039839213461
            },
            {
               "suggestion": "Hallo",
               "score": 0.597385084464481
            }
         ]
      },
      {
         "offset": 7,
         "token": "wrld",
         "type": "UnknownToken",
         "suggestions": [
            {
               "suggestion": "world",
               "score": 0.9115257530801
            }
         ]
      }
   ]
}
```

## <a name="next-steps"></a><span data-ttu-id="7aa55-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="7aa55-122">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7aa55-123">Bing Spell Check tutorial</span><span class="sxs-lookup"><span data-stu-id="7aa55-123">Bing Spell Check tutorial</span></span>](../tutorials/spellcheck.md)

## <a name="see-also"></a><span data-ttu-id="7aa55-124">See also</span><span class="sxs-lookup"><span data-stu-id="7aa55-124">See also</span></span>

- [<span data-ttu-id="7aa55-125">Bing Spell Check overview</span><span class="sxs-lookup"><span data-stu-id="7aa55-125">Bing Spell Check overview</span></span>](../proof-text.md)
- [<span data-ttu-id="7aa55-126">Bing Spell Check API v7 Reference</span><span class="sxs-lookup"><span data-stu-id="7aa55-126">Bing Spell Check API v7 Reference</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference)
