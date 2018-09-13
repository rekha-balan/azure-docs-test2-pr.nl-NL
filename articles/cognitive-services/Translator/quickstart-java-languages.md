---
title: Translator Text get supported languages with Java | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API with Java in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/21/2018
ms.author: nolachar
ms.openlocfilehash: af8b50d6600354601c8516c20a079028cefe2b16
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965928"
---
# <a name="quickstart-get-supported-languages-with-java"></a><span data-ttu-id="8d75a-103">Quickstart: Get supported languages with Java</span><span class="sxs-lookup"><span data-stu-id="8d75a-103">Quickstart: Get supported languages with Java</span></span>

<span data-ttu-id="8d75a-104">In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="8d75a-104">In this quickstart, you get a list of languages supported for translation, transliteration, and dictionary lookup and examples using the Translator Text API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d75a-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8d75a-105">Prerequisites</span></span>

<span data-ttu-id="8d75a-106">You'll need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span><span class="sxs-lookup"><span data-stu-id="8d75a-106">You'll need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span></span> <span data-ttu-id="8d75a-107">You can use a Java IDE if you have a favorite, but a text editor will also work.</span><span class="sxs-lookup"><span data-stu-id="8d75a-107">You can use a Java IDE if you have a favorite, but a text editor will also work.</span></span>

<span data-ttu-id="8d75a-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span><span class="sxs-lookup"><span data-stu-id="8d75a-108">To use the Translator Text API, you also need a subscription key; see [How to sign up for the Translator Text API](translator-text-how-to-signup.md).</span></span>

## <a name="languages-request"></a><span data-ttu-id="8d75a-109">Languages request</span><span class="sxs-lookup"><span data-stu-id="8d75a-109">Languages request</span></span>

<span data-ttu-id="8d75a-110">The following code gets a list of supported languages for translation, transliteration, and dictionary lookup and examples, using the [Languages](./reference/v3-0-languages.md) method.</span><span class="sxs-lookup"><span data-stu-id="8d75a-110">The following code gets a list of supported languages for translation, transliteration, and dictionary lookup and examples, using the [Languages](./reference/v3-0-languages.md) method.</span></span>

1. <span data-ttu-id="8d75a-111">Create a new Java project in your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="8d75a-111">Create a new Java project in your favorite code editor.</span></span>
2. <span data-ttu-id="8d75a-112">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8d75a-112">Add the code provided below.</span></span>
3. <span data-ttu-id="8d75a-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8d75a-113">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="8d75a-114">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8d75a-114">Run the program.</span></span>

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
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

/* NOTE: To compile and run this code:
1. Save this file as Languages.java.
2. Run:
    javac Languages.java -cp .;gson-2.8.1.jar -encoding UTF-8
3. Run:
    java -cp .;gson-2.8.1.jar Languages
*/

public class Languages {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the subscriptionKey string value with your valid subscription key.
    static String subscriptionKey = "ENTER KEY HERE";

    static String host = "https://api.cognitive.microsofttranslator.com";
    static String path = "/languages?api-version=3.0";

    static String output_path = "output.txt";

    public static String GetLanguages () throws Exception {
        URL url = new URL (host + path);

        HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
        connection.setRequestMethod("GET");
        connection.setRequestProperty("Ocp-Apim-Subscription-Key", subscriptionKey);
        connection.setDoOutput(true);

        StringBuilder response = new StringBuilder ();
        BufferedReader in = new BufferedReader(new InputStreamReader(connection.getInputStream(), "UTF-8"));

        String line;
        while ((line = in.readLine()) != null) {
            response.append(line);
        }
        in.close();

        return response.toString();
    }

    public static String prettify(String json_text) {
        JsonParser parser = new JsonParser();
        JsonObject json = parser.parse(json_text).getAsJsonObject();
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

    public static void WriteToFile (String data) throws Exception {
        String json = prettify (data);
        Writer outputStream = new BufferedWriter(new OutputStreamWriter(new FileOutputStream(output_path), "UTF-8"));
        outputStream.write(json);
        outputStream.close();
    }

    public static void main(String[] args) {
        try {
            String response = GetLanguages ();
            WriteToFile (response);
        }
        catch (Exception e) {
            System.out.println (e);
        }
    }
}
```

## <a name="languages-response"></a><span data-ttu-id="8d75a-115">Languages response</span><span class="sxs-lookup"><span data-stu-id="8d75a-115">Languages response</span></span>

<span data-ttu-id="8d75a-116">A successful response is returned in JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8d75a-116">A successful response is returned in JSON as shown in the following example:</span></span>

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
  },
  "transliteration": {
    "ar": {
      "name": "Arabic",
      "nativeName": "العربية",
      "scripts": [
        {
          "code": "Arab",
          "name": "Arabic",
          "nativeName": "العربية",
          "dir": "rtl",
          "toScripts": [
            {
              "code": "Latn",
              "name": "Latin",
              "nativeName": "اللاتينية",
              "dir": "ltr"
            }
          ]
        },
        {
          "code": "Latn",
          "name": "Latin",
          "nativeName": "اللاتينية",
          "dir": "ltr",
          "toScripts": [
            {
              "code": "Arab",
              "name": "Arabic",
              "nativeName": "العربية",
              "dir": "rtl"
            }
          ]
        }
      ]
    },
...
  },
  "dictionary": {
    "af": {
      "name": "Afrikaans",
      "nativeName": "Afrikaans",
      "dir": "ltr",
      "translations": [
        {
          "name": "English",
          "nativeName": "English",
          "dir": "ltr",
          "code": "en"
        }
      ]
    },
    "ar": {
      "name": "Arabic",
      "nativeName": "العربية",
      "dir": "rtl",
      "translations": [
        {
          "name": "English",
          "nativeName": "English",
          "dir": "ltr",
          "code": "en"
        }
      ]
    },
...
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="8d75a-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="8d75a-117">Next steps</span></span>

<span data-ttu-id="8d75a-118">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span><span class="sxs-lookup"><span data-stu-id="8d75a-118">Explore the sample code for this quickstart and others, including translation and transliteration, as well as other sample Translator Text projects on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8d75a-119">Explore Java examples on GitHub</span><span class="sxs-lookup"><span data-stu-id="8d75a-119">Explore Java examples on GitHub</span></span>](https://aka.ms/TranslatorGitHub?type=&language=java)
