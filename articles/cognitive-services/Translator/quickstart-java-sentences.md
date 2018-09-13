---
title: Translator Text get sentence lengths with Java | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you find the lengths of sentences in text using the Translator Text API with Java in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/21/2018
ms.author: nolachar
ms.openlocfilehash: 1e68f6b888aa670644ef1e05e5f4f3e26cf70b18
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969375"
---
# <a name="quickstart-get-sentence-lengths-with-java"></a><span data-ttu-id="9ac4f-103">Quickstart: Get sentence lengths with Java</span><span class="sxs-lookup"><span data-stu-id="9ac4f-103">Quickstart: Get sentence lengths with Java</span></span>

<span data-ttu-id="9ac4f-104">In this quickstart, you find the lengths of sentences in text using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-104">In this quickstart, you find the lengths of sentences in text using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ac4f-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9ac4f-105">Prerequisites</span></span>

<span data-ttu-id="9ac4f-106">You'll need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-106">You'll need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span></span> <span data-ttu-id="9ac4f-107">You can use a Java IDE if you have a favorite, but a text editor will also work.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-107">You can use a Java IDE if you have a favorite, but a text editor will also work.</span></span>

<span data-ttu-id="9ac4f-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="9ac4f-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="breaksentence-request"></a><span data-ttu-id="9ac4f-109">BreakSentence request</span><span class="sxs-lookup"><span data-stu-id="9ac4f-109">BreakSentence request</span></span>

<span data-ttu-id="9ac4f-110">The following code breaks the source text into sentences using the [BreakSentence](./reference/v3-0-break-sentence.md) method.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-110">The following code breaks the source text into sentences using the [BreakSentence](./reference/v3-0-break-sentence.md) method.</span></span>

1. <span data-ttu-id="9ac4f-111">Create a new Java project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-111">Create a new Java project in your favorite code editor.</span></span>
2. <span data-ttu-id="9ac4f-112">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-112">Add the code provided below.</span></span>
3. <span data-ttu-id="9ac4f-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="9ac4f-114">Run the program.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-114">Run the program.</span></span>

```java
import java.io.*;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

/*
 * Gson: https://github.com/google/gson
 * Maven info:
 *     groupId: com.google.code.gson
 *     artifactId: gson
 *     version: 2.8.1
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

/* NOTE: To compile and run this code:
1. Save this file as BreakSentences.java.
2. Run:
    javac BreakSentences.java -cp .;gson-2.8.1.jar -encoding UTF-8
3. Run:
    java -cp .;gson-2.8.1.jar BreakSentences
*/

public class BreakSentences {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the subscriptionKey string value with your valid subscription key.
    static String subscriptionKey = "ENTER KEY HERE";

    static String host = "https://api.cognitive.microsofttranslator.com";
    static String path = "/breaksentence?api-version=3.0";

    static String text = "How are you? I am fine. What did you do today?";

    public static class RequestBody {
        String Text;

        public RequestBody(String text) {
            this.Text = text;
        }
    }

    public static String Post (URL url, String content) throws Exception {
        HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
        connection.setRequestMethod("POST");
        connection.setRequestProperty("Content-Type", "application/json");
        connection.setRequestProperty("Content-Length", content.length() + "");
        connection.setRequestProperty("Ocp-Apim-Subscription-Key", subscriptionKey);
        connection.setRequestProperty("X-ClientTraceId", java.util.UUID.randomUUID().toString());
        connection.setDoOutput(true);

        DataOutputStream wr = new DataOutputStream(connection.getOutputStream());
        byte[] encoded_content = content.getBytes("UTF-8");
        wr.write(encoded_content, 0, encoded_content.length);
        wr.flush();
        wr.close();

        StringBuilder response = new StringBuilder ();
        BufferedReader in = new BufferedReader(new InputStreamReader(connection.getInputStream(), "UTF-8"));
        String line;
        while ((line = in.readLine()) != null) {
            response.append(line);
        }
        in.close();

        return response.toString();
    }

    public static String BreakSentences () throws Exception {
        URL url = new URL (host + path);

        List<RequestBody> objList = new ArrayList<RequestBody>();
        objList.add(new RequestBody(text));
        String content = new Gson().toJson(objList);

        return Post(url, content);
    }

    public static String prettify(String json_text) {
        JsonParser parser = new JsonParser();
        JsonElement json = parser.parse(json_text);
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

    public static void main(String[] args) {
        try {
            String response = BreakSentences ();
            System.out.println (prettify (response));
        }
        catch (Exception e) {
            System.out.println (e);
        }
    }
}
```

## <a name="breaksentence-response"></a><span data-ttu-id="9ac4f-115">BreakSentence response</span><span class="sxs-lookup"><span data-stu-id="9ac4f-115">BreakSentence response</span></span>

<span data-ttu-id="9ac4f-116">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="9ac4f-116">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "detectedLanguage": {
      "language": "en",
      "score": 1.0
    },
    "sentLen": [
      13,
      11,
      22
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="9ac4f-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="9ac4f-117">Next steps</span></span>

<span data-ttu-id="9ac4f-118">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="9ac4f-118">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9ac4f-119">Explore Java examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="9ac4f-119">Explore Java examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=java)
