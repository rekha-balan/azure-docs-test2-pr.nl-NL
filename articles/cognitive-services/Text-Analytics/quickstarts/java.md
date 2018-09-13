---
title: 'Quickstart: Using Java to call the Text Analytics API | Microsoft Docs'
titleSuffix: Azure Cognitive Services
description: Get information and code samples to help you quickly get started using the Text Analytics API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: ashmaka
ms.service: cognitive-services
ms.component: text-analytics
ms.topic: article
ms.date: 05/02/2018
ms.author: ashmaka
ms.openlocfilehash: 9c08536c8bf5fc4d27c896c7eed00999d14b8872
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968366"
---
# <a name="quickstart-using-java-to-call-the-text-analytics-cognitive-service"></a><span data-ttu-id="57dd9-103">Quickstart: Using Java to call the Text Analytics Cognitive Service</span><span class="sxs-lookup"><span data-stu-id="57dd9-103">Quickstart: Using Java to call the Text Analytics Cognitive Service</span></span>
<a name="HOLTop"></a>

<span data-ttu-id="57dd9-104">This article shows you how to [detect language](#Detect), [analyze sentiment](#SentimentAnalysis), [extract key phrases](#KeyPhraseExtraction), and [identify linked entities](#Entities) using the [Text Analytics APIs](//go.microsoft.com/fwlink/?LinkID=759711) with Java.</span><span class="sxs-lookup"><span data-stu-id="57dd9-104">This article shows you how to [detect language](#Detect), [analyze sentiment](#SentimentAnalysis), [extract key phrases](#KeyPhraseExtraction), and [identify linked entities](#Entities) using the [Text Analytics APIs](//go.microsoft.com/fwlink/?LinkID=759711) with Java.</span></span>

<span data-ttu-id="57dd9-105">Refer to the [API definitions](//go.microsoft.com/fwlink/?LinkID=759346) for technical documentation for the APIs.</span><span class="sxs-lookup"><span data-stu-id="57dd9-105">Refer to the [API definitions](//go.microsoft.com/fwlink/?LinkID=759346) for technical documentation for the APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57dd9-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="57dd9-106">Prerequisites</span></span>

<span data-ttu-id="57dd9-107">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Text Analytics API**.</span><span class="sxs-lookup"><span data-stu-id="57dd9-107">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Text Analytics API**.</span></span> <span data-ttu-id="57dd9-108">You can use the **free tier for 5,000 transactions/month** to complete this quickstart.</span><span class="sxs-lookup"><span data-stu-id="57dd9-108">You can use the **free tier for 5,000 transactions/month** to complete this quickstart.</span></span>
<span data-ttu-id="57dd9-109">You must also have the [endpoint and access key](../How-tos/text-analytics-how-to-access-key.md) that was generated for you during sign up.</span><span class="sxs-lookup"><span data-stu-id="57dd9-109">You must also have the [endpoint and access key](../How-tos/text-analytics-how-to-access-key.md) that was generated for you during sign up.</span></span> 

<a name="Detect"></a>

## <a name="detect-language"></a><span data-ttu-id="57dd9-110">Detect language</span><span class="sxs-lookup"><span data-stu-id="57dd9-110">Detect language</span></span>

<span data-ttu-id="57dd9-111">The Language Detection API detects the language of a text document, using the [Detect Language method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7).</span><span class="sxs-lookup"><span data-stu-id="57dd9-111">The Language Detection API detects the language of a text document, using the [Detect Language method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7).</span></span>

1. <span data-ttu-id="57dd9-112">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="57dd9-112">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="57dd9-113">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="57dd9-113">Add the code provided below.</span></span>
3. <span data-ttu-id="57dd9-114">Replace the `accessKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="57dd9-114">Replace the `accessKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="57dd9-115">Replace the location in `host` (currently `westus`) to the region you signed up for.</span><span class="sxs-lookup"><span data-stu-id="57dd9-115">Replace the location in `host` (currently `westus`) to the region you signed up for.</span></span>
5. <span data-ttu-id="57dd9-116">Run the program.</span><span class="sxs-lookup"><span data-stu-id="57dd9-116">Run the program.</span></span>

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
 *
 * Once you have compiled or downloaded gson-2.8.1.jar, assuming you have placed it in the
 * same folder as this file (DetectLanguage.java), you can compile and run this program at
 * the command line as follows.
 *
 * javac DetectLanguage.java -classpath .;gson-2.8.1.jar -encoding UTF-8
 * java -cp .;gson-2.8.1.jar DetectLanguage
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

class Document {
    public String id, text;

    public Document(String id, String text){
        this.id = id;
        this.text = text;
    }
}

class Documents {
    public List<Document> documents;

    public Documents() {
        this.documents = new ArrayList<Document>();
    }
    public void add(String id, String text) {
        this.documents.add (new Document (id, text));
    }
}

public class DetectLanguage {

// ***********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the accessKey string value with your valid access key.
    static String accessKey = "enter key here";

// Replace or verify the region.

// You must use the same region in your REST API call as you used to obtain your access keys.
// For example, if you obtained your access keys from the westus region, replace 
// "westcentralus" in the URI below with "westus".

// NOTE: Free trial access keys are generated in the westcentralus region, so if you are using
// a free trial access key, you should not need to change this region.
    static String host = "https://westus.api.cognitive.microsoft.com";

    static String path = "/text/analytics/v2.0/languages";
    
    public static String GetLanguage (Documents documents) throws Exception {
        String text = new Gson().toJson(documents);
        byte[] encoded_text = text.getBytes("UTF-8");

        URL url = new URL(host+path);
        HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
        connection.setRequestMethod("POST");
        connection.setRequestProperty("Content-Type", "text/json");
        connection.setRequestProperty("Ocp-Apim-Subscription-Key", accessKey);
        connection.setDoOutput(true);

        DataOutputStream wr = new DataOutputStream(connection.getOutputStream());
        wr.write(encoded_text, 0, encoded_text.length);
        wr.flush();
        wr.close();

        StringBuilder response = new StringBuilder ();
        BufferedReader in = new BufferedReader(
        new InputStreamReader(connection.getInputStream()));
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

    public static void main (String[] args) {
        try {
            Documents documents = new Documents ();
            documents.add ("1", "This is a document written in English.");
            documents.add ("2", "Este es un document escrito en Español.");
            documents.add ("3", "这是一个用中文写的文件");

            String response = GetLanguage (documents);
            System.out.println (prettify (response));
        }
        catch (Exception e) {
            System.out.println (e);
        }
    }
}
```

<span data-ttu-id="57dd9-117">**Language detection response**</span><span class="sxs-lookup"><span data-stu-id="57dd9-117">**Language detection response**</span></span>

<span data-ttu-id="57dd9-118">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="57dd9-118">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json

{
   "documents": [
      {
         "id": "1",
         "detectedLanguages": [
            {
               "name": "English",
               "iso6391Name": "en",
               "score": 1.0
            }
         ]
      },
      {
         "id": "2",
         "detectedLanguages": [
            {
               "name": "Spanish",
               "iso6391Name": "es",
               "score": 1.0
            }
         ]
      },
      {
         "id": "3",
         "detectedLanguages": [
            {
               "name": "Chinese_Simplified",
               "iso6391Name": "zh_chs",
               "score": 1.0
            }
         ]
      }
   ],
   "errors": [

   ]
}
```
<a name="SentimentAnalysis"></a>

## <a name="analyze-sentiment"></a><span data-ttu-id="57dd9-119">Analyze sentiment</span><span class="sxs-lookup"><span data-stu-id="57dd9-119">Analyze sentiment</span></span>

<span data-ttu-id="57dd9-120">The Sentiment Analysis API detexts the sentiment of a set of text records, using the [Sentiment method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9).</span><span class="sxs-lookup"><span data-stu-id="57dd9-120">The Sentiment Analysis API detexts the sentiment of a set of text records, using the [Sentiment method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9).</span></span> <span data-ttu-id="57dd9-121">The following example scores two documents, one in English and another in Spanish.</span><span class="sxs-lookup"><span data-stu-id="57dd9-121">The following example scores two documents, one in English and another in Spanish.</span></span>

1. <span data-ttu-id="57dd9-122">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="57dd9-122">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="57dd9-123">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="57dd9-123">Add the code provided below.</span></span>
3. <span data-ttu-id="57dd9-124">Replace the `accessKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="57dd9-124">Replace the `accessKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="57dd9-125">Replace the location in `uriBase` (currently `westus`) to the region you signed up for.</span><span class="sxs-lookup"><span data-stu-id="57dd9-125">Replace the location in `uriBase` (currently `westus`) to the region you signed up for.</span></span>
5. <span data-ttu-id="57dd9-126">Run the program.</span><span class="sxs-lookup"><span data-stu-id="57dd9-126">Run the program.</span></span>

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
 *
 * Once you have compiled or downloaded gson-2.8.1.jar, assuming you have placed it in the
 * same folder as this file (GetSentiment.java), you can compile and run this program at
 * the command line as follows.
 *
 * javac GetSentiment.java -classpath .;gson-2.8.1.jar -encoding UTF-8
 * java -cp .;gson-2.8.1.jar GetSentiment
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

class Document {
    public String id, language, text;

    public Document(String id, String language, String text){
        this.id = id;
        this.language = language;
        this.text = text;
    }
}

class Documents {
    public List<Document> documents;

    public Documents() {
        this.documents = new ArrayList<Document>();
    }
    public void add(String id, String language, String text) {
        this.documents.add (new Document (id, language, text));
    }
}

public class GetSentiment {

// ***********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the accessKey string value with your valid access key.
    static String accessKey = "enter key here";

// Replace or verify the region.

// You must use the same region in your REST API call as you used to obtain your access keys.
// For example, if you obtained your access keys from the westus region, replace 
// "westcentralus" in the URI below with "westus".

// NOTE: Free trial access keys are generated in the westcentralus region, so if you are using
// a free trial access key, you should not need to change this region.
    static String host = "https://westus.api.cognitive.microsoft.com";

    static String path = "/text/analytics/v2.0/sentiment";
    
    public static String GetSentiment (Documents documents) throws Exception {
        String text = new Gson().toJson(documents);
        byte[] encoded_text = text.getBytes("UTF-8");

        URL url = new URL(host+path);
        HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
        connection.setRequestMethod("POST");
        connection.setRequestProperty("Content-Type", "text/json");
        connection.setRequestProperty("Ocp-Apim-Subscription-Key", accessKey);
        connection.setDoOutput(true);

        DataOutputStream wr = new DataOutputStream(connection.getOutputStream());
        wr.write(encoded_text, 0, encoded_text.length);
        wr.flush();
        wr.close();

        StringBuilder response = new StringBuilder ();
        BufferedReader in = new BufferedReader(
        new InputStreamReader(connection.getInputStream()));
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

    public static void main (String[] args) {
        try {
            Documents documents = new Documents ();
            documents.add ("1", "en", "I really enjoy the new XBox One S. It has a clean look, it has 4K/HDR resolution and it is affordable.");
            documents.add ("2", "es", "Este ha sido un dia terrible, llegué tarde al trabajo debido a un accidente automobilistico.");

            String response = GetSentiment (documents);
            System.out.println (prettify (response));
        }
        catch (Exception e) {
            System.out.println (e);
        }
    }
}
```
<span data-ttu-id="57dd9-127">**Sentiment analysis response**</span><span class="sxs-lookup"><span data-stu-id="57dd9-127">**Sentiment analysis response**</span></span>

<span data-ttu-id="57dd9-128">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="57dd9-128">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
   "documents": [
      {
         "score": 0.99984133243560791,
         "id": "1"
      },
      {
         "score": 0.024017512798309326,
         "id": "2"
      },
   ],
   "errors": [   ]
}
```

<a name="KeyPhraseExtraction"></a>

## <a name="extract-key-phrases"></a><span data-ttu-id="57dd9-129">Extract key phrases</span><span class="sxs-lookup"><span data-stu-id="57dd9-129">Extract key phrases</span></span>

<span data-ttu-id="57dd9-130">The Key Phrase Extraction API extracts key-phrases from a text document, using the [Key Phrases method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6).</span><span class="sxs-lookup"><span data-stu-id="57dd9-130">The Key Phrase Extraction API extracts key-phrases from a text document, using the [Key Phrases method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6).</span></span> <span data-ttu-id="57dd9-131">The following example extracts Key phrases for both English and Spanish documents.</span><span class="sxs-lookup"><span data-stu-id="57dd9-131">The following example extracts Key phrases for both English and Spanish documents.</span></span>

1. <span data-ttu-id="57dd9-132">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="57dd9-132">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="57dd9-133">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="57dd9-133">Add the code provided below.</span></span>
3. <span data-ttu-id="57dd9-134">Replace the `accessKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="57dd9-134">Replace the `accessKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="57dd9-135">Replace the location in `uriBase` (currently `westus`) to the region you signed up for.</span><span class="sxs-lookup"><span data-stu-id="57dd9-135">Replace the location in `uriBase` (currently `westus`) to the region you signed up for.</span></span>
5. <span data-ttu-id="57dd9-136">Run the program.</span><span class="sxs-lookup"><span data-stu-id="57dd9-136">Run the program.</span></span>

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
 *
 * Once you have compiled or downloaded gson-2.8.1.jar, assuming you have placed it in the
 * same folder as this file (GetKeyPhrases.java), you can compile and run this program at
 * the command line as follows.
 *
 * javac GetKeyPhrases.java -classpath .;gson-2.8.1.jar -encoding UTF-8
 * java -cp .;gson-2.8.1.jar GetKeyPhrases
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

class Document {
    public String id, language, text;

    public Document(String id, String language, String text){
        this.id = id;
        this.language = language;
        this.text = text;
    }
}

class Documents {
    public List<Document> documents;

    public Documents() {
        this.documents = new ArrayList<Document>();
    }
    public void add(String id, String language, String text) {
        this.documents.add (new Document (id, language, text));
    }
}

public class GetKeyPhrases {

// ***********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the accessKey string value with your valid access key.
    static String accessKey = "enter key here";

// Replace or verify the region.

// You must use the same region in your REST API call as you used to obtain your access keys.
// For example, if you obtained your access keys from the westus region, replace 
// "westcentralus" in the URI below with "westus".

// NOTE: Free trial access keys are generated in the westcentralus region, so if you are using
// a free trial access key, you should not need to change this region.
    static String host = "https://westus.api.cognitive.microsoft.com";

    static String path = "/text/analytics/v2.0/keyPhrases";
    
    public static String GetKeyPhrases (Documents documents) throws Exception {
        String text = new Gson().toJson(documents);
        byte[] encoded_text = text.getBytes("UTF-8");

        URL url = new URL(host+path);
        HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
        connection.setRequestMethod("POST");
        connection.setRequestProperty("Content-Type", "text/json");
        connection.setRequestProperty("Ocp-Apim-Subscription-Key", accessKey);
        connection.setDoOutput(true);

        DataOutputStream wr = new DataOutputStream(connection.getOutputStream());
        wr.write(encoded_text, 0, encoded_text.length);
        wr.flush();
        wr.close();

        StringBuilder response = new StringBuilder ();
        BufferedReader in = new BufferedReader(
        new InputStreamReader(connection.getInputStream()));
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

    public static void main (String[] args) {
        try {
            Documents documents = new Documents ();
            documents.add ("1", "en", "I really enjoy the new XBox One S. It has a clean look, it has 4K/HDR resolution and it is affordable.");
            documents.add ("2", "es", "Si usted quiere comunicarse con Carlos, usted debe de llamarlo a su telefono movil. Carlos es muy responsable, pero necesita recibir una notificacion si hay algun problema.");
            documents.add ("3", "en", "The Grand Hotel is a new hotel in the center of Seattle. It earned 5 stars in my review, and has the classiest decor I've ever seen.");

            String response = GetKeyPhrases (documents);
            System.out.println (prettify (response));
        }
        catch (Exception e) {
            System.out.println (e);
        }
    }
}
```
<span data-ttu-id="57dd9-137">**Key phrase extraction response**</span><span class="sxs-lookup"><span data-stu-id="57dd9-137">**Key phrase extraction response**</span></span>

<span data-ttu-id="57dd9-138">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="57dd9-138">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
   "documents": [
      {
         "keyPhrases": [
            "HDR resolution",
            "new XBox",
            "clean look"
         ],
         "id": "1"
      },
      {
         "keyPhrases": [
            "Carlos",
            "notificacion",
            "algun problema",
            "telefono movil"
         ],
         "id": "2"
      },
      {
         "keyPhrases": [
            "new hotel",
            "Grand Hotel",
            "review",
            "center of Seattle",
            "classiest decor",
            "stars"
         ],
         "id": "3"
      }
   ],
   "errors": [  ]
}
```
<a name="Entities"></a>

## <a name="identify-linked-entities"></a><span data-ttu-id="57dd9-139">Identify linked entities</span><span class="sxs-lookup"><span data-stu-id="57dd9-139">Identify linked entities</span></span>

<span data-ttu-id="57dd9-140">The Entity Linking API identifies well-known entities in a text document, using the [Entity Linking method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634).</span><span class="sxs-lookup"><span data-stu-id="57dd9-140">The Entity Linking API identifies well-known entities in a text document, using the [Entity Linking method](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634).</span></span> <span data-ttu-id="57dd9-141">The following example identifies entities for English documents.</span><span class="sxs-lookup"><span data-stu-id="57dd9-141">The following example identifies entities for English documents.</span></span>

1. <span data-ttu-id="57dd9-142">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="57dd9-142">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="57dd9-143">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="57dd9-143">Add the code provided below.</span></span>
3. <span data-ttu-id="57dd9-144">Replace the `accessKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="57dd9-144">Replace the `accessKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="57dd9-145">Replace the location in `uriBase` (currently `westus`) to the region you signed up for.</span><span class="sxs-lookup"><span data-stu-id="57dd9-145">Replace the location in `uriBase` (currently `westus`) to the region you signed up for.</span></span>
5. <span data-ttu-id="57dd9-146">Run the program.</span><span class="sxs-lookup"><span data-stu-id="57dd9-146">Run the program.</span></span>

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
 *
 * Once you have compiled or downloaded gson-2.8.1.jar, assuming you have placed it in the
 * same folder as this file (GetEntities.java), you can compile and run this program at
 * the command line as follows.
 *
 * javac GetEntities.java -classpath .;gson-2.8.1.jar -encoding UTF-8
 * java -cp .;gson-2.8.1.jar GetEntities
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

class Document {
    public String id, language, text;

    public Document(String id, String language, String text){
        this.id = id;
        this.language = language;
        this.text = text;
    }
}

class Documents {
    public List<Document> documents;

    public Documents() {
        this.documents = new ArrayList<Document>();
    }
    public void add(String id, String language, String text) {
        this.documents.add (new Document (id, language, text));
    }
}

public class GetEntities {

// ***********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the accessKey string value with your valid access key.
    static String accessKey = "enter key here";

// Replace or verify the region.

// You must use the same region in your REST API call as you used to obtain your access keys.
// For example, if you obtained your access keys from the westus region, replace 
// "westcentralus" in the URI below with "westus".

// NOTE: Free trial access keys are generated in the westcentralus region, so if you are using
// a free trial access key, you should not need to change this region.
    static String host = "https://westus.api.cognitive.microsoft.com";

    static String path = "/text/analytics/v2.0/entities";
    
    public static String GetEntities (Documents documents) throws Exception {
        String text = new Gson().toJson(documents);
        byte[] encoded_text = text.getBytes("UTF-8");

        URL url = new URL(host+path);
        HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
        connection.setRequestMethod("POST");
        connection.setRequestProperty("Content-Type", "text/json");
        connection.setRequestProperty("Ocp-Apim-Subscription-Key", accessKey);
        connection.setDoOutput(true);

        DataOutputStream wr = new DataOutputStream(connection.getOutputStream());
        wr.write(encoded_text, 0, encoded_text.length);
        wr.flush();
        wr.close();

        StringBuilder response = new StringBuilder ();
        BufferedReader in = new BufferedReader(
        new InputStreamReader(connection.getInputStream()));
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

    public static void main (String[] args) {
        try {
            Documents documents = new Documents ();
            documents.add ("1", "en", "I really enjoy the new XBox One S. It has a clean look, it has 4K/HDR resolution and it is affordable.");
            documents.add ("2", "en", "The Seattle Seahawks won the Super Bowl in 2014.");

            String response = GetEntities (documents);
            System.out.println (prettify (response));
        }
        catch (Exception e) {
            System.out.println (e);
        }
    }
}
```
<span data-ttu-id="57dd9-147">**Entity linking response**</span><span class="sxs-lookup"><span data-stu-id="57dd9-147">**Entity linking response**</span></span>

<span data-ttu-id="57dd9-148">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="57dd9-148">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
    "documents": [
        {
            "id": "1",
            "entities": [
                {
                    "name": "Xbox One",
                    "matches": [
                        {
                            "text": "XBox One",
                            "offset": 23,
                            "length": 8
                        }
                    ],
                    "wikipediaLanguage": "en",
                    "wikipediaId": "Xbox One",
                    "wikipediaUrl": "https://en.wikipedia.org/wiki/Xbox_One",
                    "bingId": "446bb4df-4999-4243-84c0-74e0f6c60e75"
                },
                {
                    "name": "Ultra-high-definition television",
                    "matches": [
                        {
                            "text": "4K",
                            "offset": 63,
                            "length": 2
                        }
                    ],
                    "wikipediaLanguage": "en",
                    "wikipediaId": "Ultra-high-definition television",
                    "wikipediaUrl": "https://en.wikipedia.org/wiki/Ultra-high-definition_television",
                    "bingId": "7ee02026-b6ec-878b-f4de-f0bc7b0ab8c4"
                }
            ]
        },
        {
            "id": "2",
            "entities": [
                {
                    "name": "2013 Seattle Seahawks season",
                    "matches": [
                        {
                            "text": "Seattle Seahawks",
                            "offset": 4,
                            "length": 16
                        }
                    ],
                    "wikipediaLanguage": "en",
                    "wikipediaId": "2013 Seattle Seahawks season",
                    "wikipediaUrl": "https://en.wikipedia.org/wiki/2013_Seattle_Seahawks_season",
                    "bingId": "eb637865-4722-4eca-be9e-0ac0c376d361"
                }
            ]
        }
    ],
    "errors": []
}
```

## <a name="next-steps"></a><span data-ttu-id="57dd9-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="57dd9-149">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="57dd9-150">Text Analytics With Power BI</span><span class="sxs-lookup"><span data-stu-id="57dd9-150">Text Analytics With Power BI</span></span>](../tutorials/tutorial-power-bi-key-phrases.md)

## <a name="see-also"></a><span data-ttu-id="57dd9-151">See also</span><span class="sxs-lookup"><span data-stu-id="57dd9-151">See also</span></span> 

 [<span data-ttu-id="57dd9-152">Text Analytics overview</span><span class="sxs-lookup"><span data-stu-id="57dd9-152">Text Analytics overview</span></span>](../overview.md)  
 [<span data-ttu-id="57dd9-153">Frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="57dd9-153">Frequently asked questions (FAQ)</span></span>](../text-analytics-resource-faq.md)
