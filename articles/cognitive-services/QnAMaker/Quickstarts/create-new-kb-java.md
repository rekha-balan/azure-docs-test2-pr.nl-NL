---
title: Create a new knowledge base - quickstart Java - for Microsoft QnA Maker API (v4) - Azure Cognitive Services | Microsoft Docs
description: Create a knowledge base in Java to hold your FAQs or product manuals, so you can get started with QnA Maker.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.technology: qna-maker
ms.topic: quickstart
ms.date: 06/15/2018
ms.author: nolachar
ms.openlocfilehash: 3d637a4a046318a95eeeb532cbb7a9938cb1004d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856517"
---
# <a name="create-a-new-knowledge-base-in-java"></a><span data-ttu-id="3b696-103">Create a new knowledge base in Java</span><span class="sxs-lookup"><span data-stu-id="3b696-103">Create a new knowledge base in Java</span></span>

<span data-ttu-id="3b696-104">This quickstart walks you through creating a sample QnA Maker knowledge base, programmatically, that will appear in your Azure Dashboard of your Cognitive Services API account.</span><span class="sxs-lookup"><span data-stu-id="3b696-104">This quickstart walks you through creating a sample QnA Maker knowledge base, programmatically, that will appear in your Azure Dashboard of your Cognitive Services API account.</span></span>

<span data-ttu-id="3b696-105">Two sample FAQ URLs are given below (in 'kb.urls' of **getKB()**) that will provide content.</span><span class="sxs-lookup"><span data-stu-id="3b696-105">Two sample FAQ URLs are given below (in 'kb.urls' of **getKB()**) that will provide content.</span></span> <span data-ttu-id="3b696-106">QnA Maker automatically extracts questions and answers from semi-structured content, like FAQs, as explained more in this [data sources](../Concepts/data-sources-supported.md) document.</span><span class="sxs-lookup"><span data-stu-id="3b696-106">QnA Maker automatically extracts questions and answers from semi-structured content, like FAQs, as explained more in this [data sources](../Concepts/data-sources-supported.md) document.</span></span> <span data-ttu-id="3b696-107">You may also use your own FAQ URLs in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="3b696-107">You may also use your own FAQ URLs in this quickstart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b696-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3b696-108">Prerequisites</span></span>

<span data-ttu-id="3b696-109">You will need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span><span class="sxs-lookup"><span data-stu-id="3b696-109">You will need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span></span> <span data-ttu-id="3b696-110">You may use a Java IDE if you have a favorite, but a text editor will work okay.</span><span class="sxs-lookup"><span data-stu-id="3b696-110">You may use a Java IDE if you have a favorite, but a text editor will work okay.</span></span>

<span data-ttu-id="3b696-111">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **QnA Maker** chosen as your resource.</span><span class="sxs-lookup"><span data-stu-id="3b696-111">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **QnA Maker** chosen as your resource.</span></span> <span data-ttu-id="3b696-112">You'll need a paid subscription key from your new API account in your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span><span class="sxs-lookup"><span data-stu-id="3b696-112">You'll need a paid subscription key from your new API account in your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span></span> <span data-ttu-id="3b696-113">Either key will work for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="3b696-113">Either key will work for this quickstart.</span></span>

![Azure dashboard service key](../media/sub-key.png)

## <a name="create-knowledge-base"></a><span data-ttu-id="3b696-115">Create knowledge base</span><span class="sxs-lookup"><span data-stu-id="3b696-115">Create knowledge base</span></span>

<span data-ttu-id="3b696-116">The following code creates a new knowledge base, using the [Create](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff) method.</span><span class="sxs-lookup"><span data-stu-id="3b696-116">The following code creates a new knowledge base, using the [Create](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff) method.</span></span>

1. <span data-ttu-id="3b696-117">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="3b696-117">Create a new Java project in your favorite IDE.</span></span>
1. <span data-ttu-id="3b696-118">Add the [Google GSON library](https://github.com/google/gson) to your Java project, either by manually [creating](https://stackoverflow.com/questions/5258159/how-to-make-an-executable-jar-file) & importing the .jar file or adding a dependency to your preferred project management tool, such as Maven.</span><span class="sxs-lookup"><span data-stu-id="3b696-118">Add the [Google GSON library](https://github.com/google/gson) to your Java project, either by manually [creating](https://stackoverflow.com/questions/5258159/how-to-make-an-executable-jar-file) & importing the .jar file or adding a dependency to your preferred project management tool, such as Maven.</span></span>
1. <span data-ttu-id="3b696-119">Copy/paste the code provided below.</span><span class="sxs-lookup"><span data-stu-id="3b696-119">Copy/paste the code provided below.</span></span>
1. <span data-ttu-id="3b696-120">Replace the `subscriptionKey` value with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="3b696-120">Replace the `subscriptionKey` value with your valid subscription key.</span></span>
1. <span data-ttu-id="3b696-121">Run the program.</span><span class="sxs-lookup"><span data-stu-id="3b696-121">Run the program.</span></span>

```java
import java.io.*;
import java.lang.reflect.Type;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

/**
 * Gson: https://github.com/google/gson
 * Maven info:
 *    <dependency>
 *      <groupId>com.google.code.gson</groupId>
 *      <artifactId>gson</artifactId>
 *      <version>2.8.5</version>
 *    </dependency>
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import com.google.gson.reflect.TypeToken;

/** NOTE: To compile and run this code without an IDE:
 * 1. Save this file as CreateKB.java
 * 2. Run *:
 *    javac CreateKB.java -cp .;<GSON> -encoding UTF-8
 * 3. Run *:
 *    java -cp .;<GSON> CreateKB
 * *replace <GSON> with the name of the current Google GSON library .jar file,
 * for example: gson-2.8.5.jar
*/

public class CreateKB {

    // **********************************************
    // *** Update or verify the following values. ***
    // **********************************************

    // Replace this with a valid subscription key.
    static String subscriptionKey = "ADD YOUR SUBSCRIPTION KEY HERE";

    // Components used to create HTTP request URIs for QnA Maker operations.
    static String host = "https://westus.api.cognitive.microsoft.com";
    static String service = "/qnamaker/v4.0";
    static String method = "/knowledgebases/create";

    // Serializing classes into JSON for our request to the server.
    // For the JSON request schema, see <a href="https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff">QnA Maker V4.0</a>
    public static class KB {
        String name;
        Question[] qnaList;
        String[] urls;
        File[] files;
    }

    public static class Question {
        Integer id;
        String answer;
        String source;
        String[] questions;
        Metadata[] metadata;
    }

    public static class Metadata {
        String name;
        String value;
    }

    public static class File {
        String fileName;
        String fileUri;
    }

    // This class has the HTTP response headers and body that is returned
    // by the HTTP request.
    public static class Response {
        Map<String, List<String>> Headers;
        String Response;

        /**
         * Constructor that specifies header and body response
         * @param headers List of headers
         * @param response Response returned from your HTTP request
         */
        public Response(Map<String, List<String>> headers, String response) {
            this.Headers = headers;
            this.Response = response;
        }
    }

    /**
     * Formats and indents JSON for display.
     * @param json_text The JSON string to format and indent.
     * @return The formatted, indented JSON string.
     */
    public static String PrettyPrint (String json_text) {
        JsonParser parser = new JsonParser();
        JsonElement json = parser.parse(json_text);
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

    /**
     * Sends an HTTP GET request.
     * @param url The URL of the HTTP request.
     * @return The object that represents the HTTP response.
     */
    public static Response Get (URL url) throws Exception{
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
        return new Response (connection.getHeaderFields(), response.toString());
    }

    /**
     * Builds and sends an HTTP POST request.
     * @param url The URL of the HTTP request.
     * @param content The contents of your POST.
     * @return The object that represents the HTTP response.
     */
    public static Response Post (URL url, String content) throws Exception{
        HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
        connection.setRequestMethod("POST");
        connection.setRequestProperty("Content-Type", "application/json");
        connection.setRequestProperty("Content-Length", content.length() + "");
        connection.setRequestProperty("Ocp-Apim-Subscription-Key", subscriptionKey);
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
        return new Response (connection.getHeaderFields(), response.toString());
    }

    /**
      * Sends the request to create the knowledge base.
      * @param kb Your knowledge base object.
      * @return Sends POST request.
      * @throws Exception If POST request fails.
      */
    public static Response CreateKB (KB kb) throws Exception {
        URL url = new URL (host + service + method);
        System.out.println ("Calling " + url.toString() + ".");
        String content = new Gson().toJson(kb);
        return Post(url, content);
    }

    /**
     * Checks the status of the request to create the knowledge base.
     * @param operation The operation ID.
     * @return The specific URL being called.
     * @throws Exception If the GET request fails.
     */
    public static Response GetStatus (String operation) throws Exception {
        URL url = new URL (host + service + operation);
        System.out.println ("Calling " + url.toString() + ".");
        return Get(url);
    }

    /**
     * Sends a sample request to create a knowledge base. To understand
     * this 'kb' object, refer to the <a href="https://docs.microsoft.com/en-us/azure/cognitive-services/QnAMaker/concepts/knowledge-base">Knowledge base</a> concept page.
     * @return A new knowledge base.
     */
    public static KB GetKB () {
        KB kb = new KB ();
        kb.name = "Example Knowledge Base";

        Question q = new Question();
        q.id = 0;
        q.answer = "You can use our REST APIs to manage your Knowledge Base. See here for details: https://westus.dev.cognitive.microsoft.com/docs/services/58994a073d9e04097c7ba6fe/operations/58994a073d9e041ad42d9baa";
        q.source = "Custom Editorial";
        q.questions = new String[]{"How do I programmatically update my Knowledge Base?"};

        Metadata md = new Metadata();
        md.name = "category";
        md.value = "api";
        q.metadata = new Metadata[]{md};

        kb.qnaList = new Question[]{q};
        kb.urls = new String[]{"https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs",     "https://docs.microsoft.com/en-us/bot-framework/resources-bot-framework-faq"};

        return kb;
    }

    public static void main(String[] args) {
        try {
            // Send the request to create the knowledge base.
            Response response = CreateKB (GetKB ());
            String operation = response.Headers.get("Location").get(0);
            System.out.println (PrettyPrint (response.Response));
            // Loop until the request is completed.
            Boolean done = false;
            while (!done) {
                // Check on the status of the request.
                response = GetStatus (operation);
                System.out.println (PrettyPrint (response.Response));
                Type type = new TypeToken<Map<String, String>>(){}.getType();
                Map<String, String> fields = new Gson().fromJson(response.Response, type);
                String state = fields.get ("operationState");
                // If the request is still running, the server tells us how
                // long to wait before checking the status again.
                if (state.equals("Running") || state.equals("NotStarted")) {
                    String wait = response.Headers.get ("Retry-After").get(0);
                    System.out.println ("Waiting " + wait + " seconds...");
                    Thread.sleep (Integer.parseInt(wait) * 1000);
                }
                else {
                    done = true;
                }
            }
        } catch (Exception e) {
            System.out.println (e.getCause().getMessage());
        }
    }
}
```

## <a name="understanding-what-qna-maker-returns"></a><span data-ttu-id="3b696-122">Understanding what QnA Maker returns</span><span class="sxs-lookup"><span data-stu-id="3b696-122">Understanding what QnA Maker returns</span></span>

<span data-ttu-id="3b696-123">A successful response is returned in JSON, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="3b696-123">A successful response is returned in JSON, as shown in the following example.</span></span> <span data-ttu-id="3b696-124">Your results may differ slightly.</span><span class="sxs-lookup"><span data-stu-id="3b696-124">Your results may differ slightly.</span></span> <span data-ttu-id="3b696-125">If the final call returns a "Succeeded" state, your knowledge base was created successfully.</span><span class="sxs-lookup"><span data-stu-id="3b696-125">If the final call returns a "Succeeded" state, your knowledge base was created successfully.</span></span> <span data-ttu-id="3b696-126">To troubleshoot refer to the [Get Operation Details](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/operations_getoperationdetails) of the QnA Maker API.</span><span class="sxs-lookup"><span data-stu-id="3b696-126">To troubleshoot refer to the [Get Operation Details](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/operations_getoperationdetails) of the QnA Maker API.</span></span>

```json
Calling https://westus.api.cognitive.microsoft.com/qnamaker/v4.0/knowledgebases/create.
{
  "operationState": "NotStarted",
  "createdTimestamp": "2018-04-13T01:52:30Z",
  "lastActionTimestamp": "2018-04-13T01:52:30Z",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "e88b5b23-e9ab-47fe-87dd-3affc2fb10f3"
}
Calling https://westus.api.cognitive.microsoft.com/qnamaker/v4.0/operations/d9d40918-01bd-49f4-88b4-129fbc434c94.
{
  "operationState": "Running",
  "createdTimestamp": "2018-04-13T01:52:30Z",
  "lastActionTimestamp": "2018-04-13T01:52:30Z",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "e88b5b23-e9ab-47fe-87dd-3affc2fb10f3"
}
Waiting 30 seconds...
Calling https://westus.api.cognitive.microsoft.com/qnamaker/v4.0/operations/d9d40918-01bd-49f4-88b4-129fbc434c94.
{
  "operationState": "Succeeded",
  "createdTimestamp": "2018-04-13T01:52:30Z",
  "lastActionTimestamp": "2018-04-13T01:52:46Z",
  "resourceLocation": "/knowledgebases/b0288f33-27b9-4258-a304-8b9f63427dad",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "e88b5b23-e9ab-47fe-87dd-3affc2fb10f3"
}
Press any key to continue.
```
   
## <a name="next-steps"></a><span data-ttu-id="3b696-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="3b696-127">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3b696-128">QnA Maker (V4) REST API Reference</span><span class="sxs-lookup"><span data-stu-id="3b696-128">QnA Maker (V4) REST API Reference</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff)