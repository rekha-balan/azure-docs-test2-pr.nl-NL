---
title: Translator Text convert text script with Java | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you convert text in one language from one script to another using the Translator Text API with Java in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/21/2018
ms.author: nolachar
ms.openlocfilehash: 6f7353ba0a51bdeec2450d7435f3b738687db766
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856657"
---
# <a name="quickstart-transliterate-text-with-java"></a><span data-ttu-id="21aa4-103">Quickstart: Transliterate text with Java</span><span class="sxs-lookup"><span data-stu-id="21aa4-103">Quickstart: Transliterate text with Java</span></span>

<span data-ttu-id="21aa4-104">In this quickstart, you convert text in one language from one script to another using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="21aa4-104">In this quickstart, you convert text in one language from one script to another using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21aa4-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="21aa4-105">Prerequisites</span></span>

<span data-ttu-id="21aa4-106">You'll need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span><span class="sxs-lookup"><span data-stu-id="21aa4-106">You'll need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span></span> <span data-ttu-id="21aa4-107">You can use a Java IDE if you have a favorite, but a text editor will also work.</span><span class="sxs-lookup"><span data-stu-id="21aa4-107">You can use a Java IDE if you have a favorite, but a text editor will also work.</span></span>

<span data-ttu-id="21aa4-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="21aa4-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="transliterate-request"></a><span data-ttu-id="21aa4-109">Transliterate request</span><span class="sxs-lookup"><span data-stu-id="21aa4-109">Transliterate request</span></span>

<span data-ttu-id="21aa4-110">The following converts text in one language from one script to another script using the [Transliterate](./reference/v3-0-transliterate.md) method.</span><span class="sxs-lookup"><span data-stu-id="21aa4-110">The following converts text in one language from one script to another script using the [Transliterate](./reference/v3-0-transliterate.md) method.</span></span>

1. <span data-ttu-id="21aa4-111">Create a new Java project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="21aa4-111">Create a new Java project in your favorite code editor.</span></span>
2. <span data-ttu-id="21aa4-112">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="21aa4-112">Add the code provided below.</span></span>
3. <span data-ttu-id="21aa4-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="21aa4-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="21aa4-114">Run the program.</span><span class="sxs-lookup"><span data-stu-id="21aa4-114">Run the program.</span></span>

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
1. Save this file as Transliterate.java.
2. Run:
    javac Transliterate.java -cp .;gson-2.8.1.jar -encoding UTF-8
3. Run:
    java -cp .;gson-2.8.1.jar Transliterate
*/

public class Transliterate {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the subscriptionKey string value with your valid subscription key.
    static String subscriptionKey = "ENTER KEY HERE";

    static String host = "https://api.cognitive.microsofttranslator.com";
    static String path = "/transliterate?api-version=3.0";

    // Transliterate text in Japanese from Japanese script (i.e. Hiragana/Katakana/Kanji) to Latin script.
    static String params = "&language=ja&fromScript=jpan&toScript=latn";

    // Transliterate "good afternoon".
    static String text = "こんにちは";

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

    public static String Transliterate () throws Exception {
        URL url = new URL (host + path + params);

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
            String response = Transliterate ();
            System.out.println (prettify (response));
        }
        catch (Exception e) {
            System.out.println (e);
        }
    }
}
```

## <a name="transliterate-response"></a><span data-ttu-id="21aa4-115">Transliterate response</span><span class="sxs-lookup"><span data-stu-id="21aa4-115">Transliterate response</span></span>

<span data-ttu-id="21aa4-116">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="21aa4-116">A successful response is returned in JSON as shown in the following example:</span></span>

```json
[
  {
    "text": "konnnichiha",
    "script": "latn"
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="21aa4-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="21aa4-117">Next steps</span></span>

<span data-ttu-id="21aa4-118">Explore the sample code for this quickstart and others, including translation and language identification, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="21aa4-118">Explore the sample code for this quickstart and others, including translation and language identification, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="21aa4-119">Explore Java examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="21aa4-119">Explore Java examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=java)
