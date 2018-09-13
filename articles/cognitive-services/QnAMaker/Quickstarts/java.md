---
title: 'Quickstart: Java for QnA Maker API (v4)'
titleSuffix: Azure Cognitive Services
description: Get information and code samples to help you quickly get started using the Microsoft Translator Text API in Microsoft Cognitive Services on Azure.
services: cognitive-services
author: nitinme
manager: cgronlun
ms.service: cognitive-services
ms.technology: qna-maker
ms.topic: article
ms.date: 05/07/2018
ms.author: v-jaswel
ms.openlocfilehash: b436cbc1efde2e28b388e6bfc1843af1808ea993
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867064"
---
# <a name="quickstart-for-microsoft-qna-maker-api-with-java"></a><span data-ttu-id="f4cdd-103">Quickstart for Microsoft QnA Maker API with Java</span><span class="sxs-lookup"><span data-stu-id="f4cdd-103">Quickstart for Microsoft QnA Maker API with Java</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="f4cdd-104">This article shows you how to use the [Microsoft QnA Maker API](../Overview/overview.md) with Java to do the following.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-104">This article shows you how to use the [Microsoft QnA Maker API](../Overview/overview.md) with Java to do the following.</span></span>

- [<span data-ttu-id="f4cdd-105">Create a new knowledge base.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-105">Create a new knowledge base.</span></span>](#Create)
- [<span data-ttu-id="f4cdd-106">Update an existing knowledge base.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-106">Update an existing knowledge base.</span></span>](#Update)
- [<span data-ttu-id="f4cdd-107">Get the status of a request to create or update a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-107">Get the status of a request to create or update a knowledge base.</span></span>](#Status)
- [<span data-ttu-id="f4cdd-108">Publish an existing knowledge base.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-108">Publish an existing knowledge base.</span></span>](#Publish)
- [<span data-ttu-id="f4cdd-109">Replace the contents of an existing knowledge base.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-109">Replace the contents of an existing knowledge base.</span></span>](#Replace)
- [<span data-ttu-id="f4cdd-110">Download the contents of a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-110">Download the contents of a knowledge base.</span></span>](#GetQnA)
- [<span data-ttu-id="f4cdd-111">Get answers to a question using a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-111">Get answers to a question using a knowledge base.</span></span>](#GetAnswers)
- [<span data-ttu-id="f4cdd-112">Get information about a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-112">Get information about a knowledge base.</span></span>](#GetKB)
- [<span data-ttu-id="f4cdd-113">Get information about all knowledge bases belonging to the specified user.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-113">Get information about all knowledge bases belonging to the specified user.</span></span>](#GetKBsByUser)
- [<span data-ttu-id="f4cdd-114">Delete a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-114">Delete a knowledge base.</span></span>](#Delete)
- [<span data-ttu-id="f4cdd-115">Get the current endpoint keys.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-115">Get the current endpoint keys.</span></span>](#GetKeys)
- [<span data-ttu-id="f4cdd-116">Re-generate the current endpoint keys.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-116">Re-generate the current endpoint keys.</span></span>](#PutKeys)
- [<span data-ttu-id="f4cdd-117">Get the current set of word alterations.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-117">Get the current set of word alterations.</span></span>](#GetAlterations)
- [<span data-ttu-id="f4cdd-118">Replace the current set of word alterations.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-118">Replace the current set of word alterations.</span></span>](#PutAlterations)

## <a name="prerequisites"></a><span data-ttu-id="f4cdd-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f4cdd-119">Prerequisites</span></span>

<span data-ttu-id="f4cdd-120">You will need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-120">You will need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span></span> <span data-ttu-id="f4cdd-121">You may use a Java IDE if you have a favorite, but a text editor will suffice.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-121">You may use a Java IDE if you have a favorite, but a text editor will suffice.</span></span>

<span data-ttu-id="f4cdd-122">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft QnA Maker API**.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-122">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Microsoft QnA Maker API**.</span></span> <span data-ttu-id="f4cdd-123">You will need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span><span class="sxs-lookup"><span data-stu-id="f4cdd-123">You will need a paid subscription key from your [Azure dashboard](https://portal.azure.com/#create/Microsoft.CognitiveServices).</span></span>

<a name="Create"></a>

## <a name="create-knowledge-base"></a><span data-ttu-id="f4cdd-124">Create knowledge base</span><span class="sxs-lookup"><span data-stu-id="f4cdd-124">Create knowledge base</span></span>

<span data-ttu-id="f4cdd-125">The following code creates a new knowledge base, using the [Create](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff) method.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-125">The following code creates a new knowledge base, using the [Create](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff) method.</span></span>

1. <span data-ttu-id="f4cdd-126">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-126">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="f4cdd-127">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-127">Add the code provided below.</span></span>
3. <span data-ttu-id="f4cdd-128">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-128">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="f4cdd-129">Run the program.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-129">Run the program.</span></span>

```java
import java.io.*;
import java.lang.reflect.Type;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

/*
 * Gson: https://github.com/google/gson
 * Maven info:
 *    <dependency>
 *      <groupId>com.google.code.gson</groupId>
 *      <artifactId>gson</artifactId>
 *      <version>2.8.1</version>
 *    </dependency>
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import com.google.gson.reflect.TypeToken;

/* NOTE: To compile and run this code:
1. Save this file as CreateKB.java.
2. Run:
    javac CreateKB.java -cp .;gson-2.8.1.jar -encoding UTF-8
3. Run:
    java -cp .;gson-2.8.1.jar CreateKB
*/

public class CreateKB {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
    static String subscriptionKey = "ENTER KEY HERE";

    static String host = "https://westus.api.cognitive.microsoft.com";
    static String service = "/qnamaker/v4.0";
    static String method = "/knowledgebases/create";

// We'll serialize these classes into JSON for our request to the server.
// For the JSON request schema, see:
// https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff
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

// This class contains the headers and body of the HTTP response.
    public static class Response {
        Map<String, List<String>> Headers;
        String Response;

        public Response(Map<String, List<String>> headers, String response) {
            this.Headers = headers;
            this.Response = response;
        }
    }

    public static String PrettyPrint (String json_text) {
        JsonParser parser = new JsonParser();
        JsonElement json = parser.parse(json_text);
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

// Send an HTTP GET request.
    public static Response Get (URL url) throws Exception {
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

// Send an HTTP POST request.
    public static Response Post (URL url, String content) throws Exception {
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

// Sends the request to create the knowledge base.
    public static Response CreateKB (KB kb) throws Exception {
        URL url = new URL (host + service + method);
        System.out.println ("Calling " + url.toString() + ".");
        String content = new Gson().toJson(kb);
        return Post(url, content);
    }

// Checks the status of the request to create the knowledge base.
    public static Response GetStatus (String operation) throws Exception {
        URL url = new URL (host + service + operation);
        System.out.println ("Calling " + url.toString() + ".");
        return Get(url);
    }

// Returns a sample request to create a knowledge base.
    public static KB GetKB () {
        KB kb = new KB ();
        kb.name = "Example Knowledge Base";

        Question q = new Question();
        q.id = 0;
        q.answer = "You can use our REST APIs to manage your Knowledge Base. See here for details: https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600";
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
            while (true != done) {
// Check on the status of the request.
                response = GetStatus (operation);
                System.out.println (PrettyPrint (response.Response));
                Type type = new TypeToken<Map<String, String>>(){}.getType();
                Map<String, String> fields = new Gson().fromJson(response.Response, type);
                String state = fields.get ("operationState");
// If the request is still running, the server tells us how long to wait before checking the status again.
                if (state.equals("Running") || state.equals("NotStarted")) {
                    String wait = response.Headers.get ("Retry-After").get(0);
                    System.out.println ("Waiting " + wait + " seconds...");
                    Thread.sleep (Integer.parseInt(wait) * 1000);
                }
                else {
                    done = true;
                }
            }
        }
        catch (Exception e) {
            System.out.println (e.getCause().getMessage());
        }
    }
}
```

<span data-ttu-id="f4cdd-130">**Create knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="f4cdd-130">**Create knowledge base response**</span></span>

<span data-ttu-id="f4cdd-131">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f4cdd-131">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "operationState": "NotStarted",
  "createdTimestamp": "2018-04-13T01:52:30Z",
  "lastActionTimestamp": "2018-04-13T01:52:30Z",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "e88b5b23-e9ab-47fe-87dd-3affc2fb10f3"
}
...
{
  "operationState": "Running",
  "createdTimestamp": "2018-04-13T01:52:30Z",
  "lastActionTimestamp": "2018-04-13T01:52:30Z",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "e88b5b23-e9ab-47fe-87dd-3affc2fb10f3"
}
...
{
  "operationState": "Succeeded",
  "createdTimestamp": "2018-04-13T01:52:30Z",
  "lastActionTimestamp": "2018-04-13T01:52:46Z",
  "resourceLocation": "/knowledgebases/b0288f33-27b9-4258-a304-8b9f63427dad",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "e88b5b23-e9ab-47fe-87dd-3affc2fb10f3"
}
```

[<span data-ttu-id="f4cdd-132">Back to top</span><span class="sxs-lookup"><span data-stu-id="f4cdd-132">Back to top</span></span>](#HOLTop)

<a name="Update"></a>

## <a name="update-knowledge-base"></a><span data-ttu-id="f4cdd-133">Update knowledge base</span><span class="sxs-lookup"><span data-stu-id="f4cdd-133">Update knowledge base</span></span>

<span data-ttu-id="f4cdd-134">The following code updates an existing knowledge base, using the [Update](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) method.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-134">The following code updates an existing knowledge base, using the [Update](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) method.</span></span>

1. <span data-ttu-id="f4cdd-135">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-135">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="f4cdd-136">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-136">Add the code provided below.</span></span>
3. <span data-ttu-id="f4cdd-137">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-137">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="f4cdd-138">Run the program.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-138">Run the program.</span></span>

```java
import java.io.*;
import java.lang.reflect.Type;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

/*
 * Gson: https://github.com/google/gson
 * Maven info:
 *    <dependency>
 *      <groupId>com.google.code.gson</groupId>
 *      <artifactId>gson</artifactId>
 *      <version>2.8.1</version>
 *    </dependency>
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import com.google.gson.reflect.TypeToken;

// Java does not natively support HTTP PATCH requests, so Apache HttpClient is required.
/*
 * HttpClient: http://hc.apache.org/downloads.cgi
 * Maven info:
 *    <dependency>
 *      <groupId>org.apache.httpcomponents</groupId>
 *      <artifactId>httpclient</artifactId>
 *      <version>4.5.5</version>
 *    </dependency>
 */
import org.apache.commons.logging.LogFactory;
import org.apache.http.client.methods.HttpPatch;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.entity.ByteArrayEntity;
import org.apache.http.Header;
import org.apache.http.HttpEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;

/* NOTE: To compile and run this code:
1. Save this file as UpdateKB.java.
2. Run:
    javac UpdateKB.java -cp .;gson-2.8.1.jar;httpclient-4.5.5.jar;httpcore-4.4.9.jar;commons-logging-1.2.jar -encoding UTF-8
3. Run:
    java -cp .;gson-2.8.1.jar;httpclient-4.5.5.jar;httpcore-4.4.9.jar;commons-logging-1.2.jar UpdateKB
*/

public class UpdateKB {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
    static String subscriptionKey = "ENTER KEY HERE";

// Replace this with a valid knowledge base ID.
    static String kb = "ENTER ID HERE";

    static String host = "https://westus.api.cognitive.microsoft.com";
    static String service = "/qnamaker/v4.0";
    static String method = "/knowledgebases/";

// We'll serialize these classes into JSON for our request to the server.
// For the JSON request schema, see:
// https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600
    public static class Request {
        Add add;
        Delete delete;
        Update update;
    }

    public static class Add {
        Question[] qnaList;
        String[] urls;
        File[] files;
    }

    public static class Delete {
        Integer[] ids;
    }

    public static class Update {
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

// This class contains the headers and body of the HTTP response.
    public static class Response {
        Map<String, List<String>> Headers;
        String Response;

        public Response(Map<String, List<String>> headers, String response) {
            this.Headers = headers;
            this.Response = response;
        }
    }

    public static String PrettyPrint (String json_text) {
        JsonParser parser = new JsonParser();
        JsonElement json = parser.parse(json_text);
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

// Send an HTTP GET request.
    public static Response Get (URL url) throws Exception {
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

// Send an HTTP PATCH request. We use Apache HttpClient to do this, as HttpsURLConnection does not support PATCH.
    public static Response Patch (URL url, String content) throws Exception {
        HttpPatch patch = new HttpPatch(url.toString());
        // HttpPatch implements HttpMessage, which includes addHeader. See:
        // https://hc.apache.org/httpcomponents-client-ga/httpclient/apidocs/org/apache/http/client/methods/HttpPatch.html
        // http://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/HttpMessage.html
        patch.addHeader("Content-Type", "application/json");
        // Note: Adding the Content-Length header causes the exception:
        // "Content-Length header already present."
        patch.addHeader("Ocp-Apim-Subscription-Key", subscriptionKey);
        // HttpPatch implements HttpEntityEnclosingRequest, which includes setEntity. See:
        // http://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/HttpEntityEnclosingRequest.html
        HttpEntity entity = new ByteArrayEntity(content.getBytes("UTF-8"));
        patch.setEntity(entity);

        CloseableHttpClient httpClient = HttpClients.createDefault();
        CloseableHttpResponse response = httpClient.execute(patch);

        // CloseableHttpResponse implements HttpMessage, which includes getAllHeaders. See:
        // https://hc.apache.org/httpcomponents-client-ga/httpclient/apidocs/org/apache/http/client/methods/CloseableHttpResponse.html
        // Header implements NameValuePair. See:
        // http://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/Header.html
        // http://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/NameValuePair.html
        Map<String, List<String>> headers = new HashMap<String, List<String>>();
        for (Header header : response.getAllHeaders()) {
            List<String> list = new ArrayList<String>() {
                {
                    add(header.getValue());
                }
            };
            headers.put(header.getName(), list);
        }

        // CloseableHttpResponse implements HttpResponse, which includes getEntity. See:
        // http://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/HttpResponse.html
        // HttpEntity implements getContent, which returns an InputStream. See:
        // http://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/HttpEntity.html
        StringBuilder output = new StringBuilder ();
        BufferedReader reader = new BufferedReader(new InputStreamReader(response.getEntity().getContent(), "UTF-8"));
        String line;
        while ((line = reader.readLine()) != null) {
            output.append(line);
        }
        reader.close();

        return new Response (headers, output.toString());
    }

// Sends the request to update the knowledge base.
    public static Response UpdateKB (String kb, Request req) throws Exception {
        URL url = new URL(host + service + method + kb);
        System.out.println ("Calling " + url.toString() + ".");
        String content = new Gson().toJson(req);
        return Patch(url, content);
    }

// Checks on the status of the request to update the knowledge base.
    public static Response GetStatus (String operation) throws Exception {
        URL url = new URL (host + service + operation);
        System.out.println ("Calling " + url.toString() + ".");
        return Get(url);
    }

// Returns a sample request to update a knowledge base.
    public static Request GetRequest () {
        Request req = new Request ();

        Question q = new Question();
        q.id = 0;
        q.answer = "You can use our REST APIs to manage your Knowledge Base. See here for details: https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600";
        q.source = "Custom Editorial";
        q.questions = new String[]{"How do I programmatically update my Knowledge Base?"};

        Metadata md = new Metadata();
        md.name = "category";
        md.value = "api";
        q.metadata = new Metadata[]{md};

        req.add = new Add ();
        req.add.qnaList = new Question[]{q};
        req.add.urls = new String[]{"https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs",     "https://docs.microsoft.com/en-us/bot-framework/resources-bot-framework-faq"};

        return req;
    }

    public static void main(String[] args) {
        try {
// Send the request to update the knowledge base.
            Response response = UpdateKB (kb, GetRequest ());
            String operation = response.Headers.get("Location").get(0);
            System.out.println (PrettyPrint (response.Response));
// Loop until the request is completed.
            Boolean done = false;
            while (true != done) {
// Check on the status of the request.
                response = GetStatus (operation);
                System.out.println (PrettyPrint (response.Response));
                Type type = new TypeToken<Map<String, String>>(){}.getType();
                Map<String, String> fields = new Gson().fromJson(response.Response, type);
                String state = fields.get ("operationState");
// If the request is still running, the server tells us how long to wait before checking the status again.
                if (state.equals("Running") || state.equals("NotStarted")) {
                    String wait = response.Headers.get ("Retry-After").get(0);
                    System.out.println ("Waiting " + wait + " seconds...");
                    Thread.sleep (Integer.parseInt(wait) * 1000);
                }
                else {
                    done = true;
                }
            }
        }
        catch (Exception e) {
            System.out.println (e.getCause().getMessage());
        }
    }
}
```

<span data-ttu-id="f4cdd-139">**Update knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="f4cdd-139">**Update knowledge base response**</span></span>

<span data-ttu-id="f4cdd-140">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f4cdd-140">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "operationState": "NotStarted",
  "createdTimestamp": "2018-04-13T01:49:48Z",
  "lastActionTimestamp": "2018-04-13T01:49:48Z",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "5156f64e-e31d-4638-ad7c-a2bdd7f41658"
}
...
{
  "operationState": "Succeeded",
  "createdTimestamp": "2018-04-13T01:49:48Z",
  "lastActionTimestamp": "2018-04-13T01:49:50Z",
  "resourceLocation": "/knowledgebases/140a46f3-b248-4f1b-9349-614bfd6e5563",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "5156f64e-e31d-4638-ad7c-a2bdd7f41658"
}
Press any key to continue.
```

[<span data-ttu-id="f4cdd-141">Back to top</span><span class="sxs-lookup"><span data-stu-id="f4cdd-141">Back to top</span></span>](#HOLTop)

<a name="Status"></a>

## <a name="get-request-status"></a><span data-ttu-id="f4cdd-142">Get request status</span><span class="sxs-lookup"><span data-stu-id="f4cdd-142">Get request status</span></span>

<span data-ttu-id="f4cdd-143">You can call the [Operation](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/operations_getoperationdetails) method to check the status of a request to create or update a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-143">You can call the [Operation](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/operations_getoperationdetails) method to check the status of a request to create or update a knowledge base.</span></span> <span data-ttu-id="f4cdd-144">To see how this method is used, please see the sample code for the [Create](#Create) or [Update](#Update) method.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-144">To see how this method is used, please see the sample code for the [Create](#Create) or [Update](#Update) method.</span></span>

[<span data-ttu-id="f4cdd-145">Back to top</span><span class="sxs-lookup"><span data-stu-id="f4cdd-145">Back to top</span></span>](#HOLTop)

<a name="Publish"></a>

## <a name="publish-knowledge-base"></a><span data-ttu-id="f4cdd-146">Publish knowledge base</span><span class="sxs-lookup"><span data-stu-id="f4cdd-146">Publish knowledge base</span></span>

<span data-ttu-id="f4cdd-147">The following code publishes an existing knowledge base, using the [Publish](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fe) method.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-147">The following code publishes an existing knowledge base, using the [Publish](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fe) method.</span></span>

1. <span data-ttu-id="f4cdd-148">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-148">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="f4cdd-149">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-149">Add the code provided below.</span></span>
3. <span data-ttu-id="f4cdd-150">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-150">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="f4cdd-151">Run the program.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-151">Run the program.</span></span>

```java
import java.io.*;
import java.lang.reflect.Type;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

/*
 * Gson: https://github.com/google/gson
 * Maven info:
 *    <dependency>
 *      <groupId>com.google.code.gson</groupId>
 *      <artifactId>gson</artifactId>
 *      <version>2.8.1</version>
 *    </dependency>
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import com.google.gson.reflect.TypeToken;

/* NOTE: To compile and run this code:
1. Save this file as PublishKB.java.
2. Run:
    javac PublishKB.java -cp .;gson-2.8.1.jar -encoding UTF-8
3. Run:
    java -cp .;gson-2.8.1.jar PublishKB
*/

public class PublishKB {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
    static String subscriptionKey = "ENTER KEY HERE";

// Replace this with a valid knowledge base ID.
    static String kb = "ENTER ID HERE";

    static String host = "https://westus.api.cognitive.microsoft.com";
    static String service = "/qnamaker/v4.0";
    static String method = "/knowledgebases/";

    public static String PrettyPrint (String json_text) {
        JsonParser parser = new JsonParser();
        JsonElement json = parser.parse(json_text);
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

// Send an HTTP POST request.
    public static String Post (URL url, String content) throws Exception {
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

        if (connection.getResponseCode() == 204)
        {
            return "{'result' : 'Success.'}";
        }
        else {
            StringBuilder response = new StringBuilder ();
            BufferedReader in = new BufferedReader(new InputStreamReader(connection.getErrorStream(), "UTF-8"));

            String line;
            while ((line = in.readLine()) != null) {
                response.append(line);
            }
            in.close();

            return response.toString();
        }
    }

// Sends the request to publish the knowledge base.
    public static String PublishKB (String kb) throws Exception {
        URL url = new URL(host + service + method + kb);
        System.out.println ("Calling " + url.toString() + ".");
        return Post(url, "");
    }

    public static void main(String[] args) {
        try {
            String response = PublishKB (kb);
            System.out.println (PrettyPrint (response));
        }
        catch (Exception e) {
            System.out.println (e.getCause().getMessage());
        }
    }
}
```

<span data-ttu-id="f4cdd-152">**Publish knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="f4cdd-152">**Publish knowledge base response**</span></span>

<span data-ttu-id="f4cdd-153">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f4cdd-153">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "result": "Success."
}
```

[<span data-ttu-id="f4cdd-154">Back to top</span><span class="sxs-lookup"><span data-stu-id="f4cdd-154">Back to top</span></span>](#HOLTop)

<a name="Replace"></a>

## <a name="replace-knowledge-base"></a><span data-ttu-id="f4cdd-155">Replace knowledge base</span><span class="sxs-lookup"><span data-stu-id="f4cdd-155">Replace knowledge base</span></span>

<span data-ttu-id="f4cdd-156">The following code replaces the contents of the specified knowledge base, using the [Replace](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_publish) method.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-156">The following code replaces the contents of the specified knowledge base, using the [Replace](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_publish) method.</span></span>

1. <span data-ttu-id="f4cdd-157">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-157">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="f4cdd-158">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-158">Add the code provided below.</span></span>
3. <span data-ttu-id="f4cdd-159">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-159">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="f4cdd-160">Run the program.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-160">Run the program.</span></span>

```java
import java.io.*;
import java.lang.reflect.Type;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

/*
 * Gson: https://github.com/google/gson
 * Maven info:
 *    <dependency>
 *      <groupId>com.google.code.gson</groupId>
 *      <artifactId>gson</artifactId>
 *      <version>2.8.1</version>
 *    </dependency>
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import com.google.gson.reflect.TypeToken;

/* NOTE: To compile and run this code:
1. Save this file as ReplaceKB.java.
2. Run:
    javac ReplaceKB.java -cp .;gson-2.8.1.jar -encoding UTF-8
3. Run:
    java -cp .;gson-2.8.1.jar ReplaceKB
*/

public class ReplaceKB {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
    static String subscriptionKey = "ENTER KEY HERE";

// Replace this with a valid knowledge base ID.
    static String kb = "ENTER ID HERE";

    static String host = "https://westus.api.cognitive.microsoft.com";
    static String service = "/qnamaker/v4.0";
    static String method = "/knowledgebases/";

// We'll serialize these classes into JSON for our request to the server.
// For the JSON request schema, see:
// https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_publish
    public static class Request {
        Question[] qnaList;
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

    public static String PrettyPrint (String json_text) {
        JsonParser parser = new JsonParser();
        JsonElement json = parser.parse(json_text);
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

// Send an HTTP PUT request.
    public static String Put (URL url, String content) throws Exception {
        HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
        connection.setRequestMethod("PUT");
        connection.setRequestProperty("Content-Type", "application/json");
        connection.setRequestProperty("Content-Length", content.length() + "");
        connection.setRequestProperty("Ocp-Apim-Subscription-Key", subscriptionKey);
        connection.setDoOutput(true);

        DataOutputStream wr = new DataOutputStream(connection.getOutputStream());
        byte[] encoded_content = content.getBytes("UTF-8");
        wr.write(encoded_content, 0, encoded_content.length);
        wr.flush();
        wr.close();

        if (connection.getResponseCode() == 204)
        {
            return "{'result' : 'Success.'}";
        }
        else {
            StringBuilder response = new StringBuilder ();
            BufferedReader in = new BufferedReader(new InputStreamReader(connection.getErrorStream(), "UTF-8"));

            String line;
            while ((line = in.readLine()) != null) {
                response.append(line);
            }
            in.close();

            return response.toString();
        }
    }

// Sends the request to replace the knowledge base.
    public static String ReplaceKB (String kb, Request req) throws Exception {
        URL url = new URL(host + service + method + kb);
        System.out.println ("Calling " + url.toString() + ".");
        String content = new Gson().toJson(req);
        return Put(url, content);
    }

// Returns a sample request to replace a knowledge base.
    public static Request GetRequest () {
        Request req = new Request ();

        Question q = new Question();
        q.id = 0;
        q.answer = "You can use our REST APIs to manage your Knowledge Base. See here for details: https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600";
        q.source = "Custom Editorial";
        q.questions = new String[]{"How do I programmatically update my Knowledge Base?"};

        Metadata md = new Metadata();
        md.name = "category";
        md.value = "api";
        q.metadata = new Metadata[]{md};

        req.qnaList = new Question[]{q};

        return req;
    }

    public static void main(String[] args) {
        try {
            String response = ReplaceKB (kb, GetRequest ());
            System.out.println (PrettyPrint (response));
        }
        catch (Exception e) {
            System.out.println (e.getCause().getMessage());
        }
    }
}
```

<span data-ttu-id="f4cdd-161">**Replace knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="f4cdd-161">**Replace knowledge base response**</span></span>

<span data-ttu-id="f4cdd-162">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f4cdd-162">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
    "result": "Success."
}
```

[<span data-ttu-id="f4cdd-163">Back to top</span><span class="sxs-lookup"><span data-stu-id="f4cdd-163">Back to top</span></span>](#HOLTop)

<a name="GetQnA"></a>

## <a name="download-the-contents-of-a-knowledge-base"></a><span data-ttu-id="f4cdd-164">Download the contents of a knowledge base</span><span class="sxs-lookup"><span data-stu-id="f4cdd-164">Download the contents of a knowledge base</span></span>

<span data-ttu-id="f4cdd-165">The following code downloads the contents of the specified knowledge base, using the [Download knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_download) method.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-165">The following code downloads the contents of the specified knowledge base, using the [Download knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_download) method.</span></span>

1. <span data-ttu-id="f4cdd-166">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-166">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="f4cdd-167">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-167">Add the code provided below.</span></span>
3. <span data-ttu-id="f4cdd-168">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-168">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="f4cdd-169">Run the program.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-169">Run the program.</span></span>

```java
import java.io.*;
import java.lang.reflect.Type;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

/*
 * Gson: https://github.com/google/gson
 * Maven info:
 *    <dependency>
 *      <groupId>com.google.code.gson</groupId>
 *      <artifactId>gson</artifactId>
 *      <version>2.8.1</version>
 *    </dependency>
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import com.google.gson.reflect.TypeToken;

/* NOTE: To compile and run this code:
1. Save this file as GetQnA.java.
2. Run:
    javac GetQnA.java -cp .;gson-2.8.1.jar -encoding UTF-8
3. Run:
    java -cp .;gson-2.8.1.jar GetQnA
*/

public class GetQnA {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
    static String subscriptionKey = "ENTER KEY HERE";

// Replace this with a valid knowledge base ID.
    static String kb = "ENTER ID HERE";

// Replace this with "test" or "prod".
    static String env = "test";

    static String host = "https://westus.api.cognitive.microsoft.com";
    static String service = "/qnamaker/v4.0";
    static String method = "/knowledgebases/%s/%s/qna/";

    public static String PrettyPrint (String json_text) {
        JsonParser parser = new JsonParser();
        JsonElement json = parser.parse(json_text);
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

// Send an HTTP GET request.
    public static String Get (URL url) throws Exception {
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

// Sends the request to download the knowledge base.
    public static String GetQnA (String kb) throws Exception {
        String method_with_id = String.format (method, kb, env);
        URL url = new URL (host + service + method_with_id);
        System.out.println ("Calling " + url.toString() + ".");
        return Get(url);
    }

    public static void main(String[] args) {
        try {
            String response = GetQnA (kb);
            System.out.println (PrettyPrint (response));
        }
        catch (Exception e) {
            System.out.println (e.getCause().getMessage());
        }
    }
}
```

<span data-ttu-id="f4cdd-170">**Download knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="f4cdd-170">**Download knowledge base response**</span></span>

<span data-ttu-id="f4cdd-171">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f4cdd-171">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "qnaDocuments": [
    {
      "id": 1,
      "answer": "You can use our REST APIs to manage your Knowledge Base. See here for details: https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600",
      "source": "Custom Editorial",
      "questions": [
        "How do I programmatically update my Knowledge Base?"
      ],
      "metadata": [
        {
          "name": "category",
          "value": "api"
        }
      ]
    },
    {
      "id": 2,
      "answer": "QnA Maker provides an FAQ data source that you can query from your bot or application. Although developers will find this useful, content owners will especially benefit from this tool. QnA Maker is a completely no-code way of managing the content that powers your bot or application.",
      "source": "https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs",
      "questions": [
        "Who is the target audience for the QnA Maker tool?"
      ],
      "metadata": []
    },
...
  ]
}
```

[<span data-ttu-id="f4cdd-172">Back to top</span><span class="sxs-lookup"><span data-stu-id="f4cdd-172">Back to top</span></span>](#HOLTop)

<a name="GetAnswers"></a>

## <a name="get-answers-to-a-question-by-using-a-knowledge-base"></a><span data-ttu-id="f4cdd-173">Get answers to a question by using a knowledge base</span><span class="sxs-lookup"><span data-stu-id="f4cdd-173">Get answers to a question by using a knowledge base</span></span>

<span data-ttu-id="f4cdd-174">The following code gets answers to a question using the specified knowledge base, using the **Generate answers** method.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-174">The following code gets answers to a question using the specified knowledge base, using the **Generate answers** method.</span></span>

1. <span data-ttu-id="f4cdd-175">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-175">Create a new Java project in your favorite IDE.</span></span>
1. <span data-ttu-id="f4cdd-176">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-176">Add the code provided below.</span></span>
1. <span data-ttu-id="f4cdd-177">Replace the `host` value with the Website name for your QnA Maker subscription.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-177">Replace the `host` value with the Website name for your QnA Maker subscription.</span></span> <span data-ttu-id="f4cdd-178">For more information see [Create a QnA Maker service](../How-To/set-up-qnamaker-service-azure.md).</span><span class="sxs-lookup"><span data-stu-id="f4cdd-178">For more information see [Create a QnA Maker service](../How-To/set-up-qnamaker-service-azure.md).</span></span>
1. <span data-ttu-id="f4cdd-179">Replace the `endpoint_key` value with a valid endpoint key for your subscription.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-179">Replace the `endpoint_key` value with a valid endpoint key for your subscription.</span></span> <span data-ttu-id="f4cdd-180">Note this is not the same as your subscription key.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-180">Note this is not the same as your subscription key.</span></span> <span data-ttu-id="f4cdd-181">You can get your endpoint keys using the [Get endpoint keys](#GetKeys) method.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-181">You can get your endpoint keys using the [Get endpoint keys](#GetKeys) method.</span></span>
1. <span data-ttu-id="f4cdd-182">Replace the `kb` value with the ID of the knowledge base you want to query for answers.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-182">Replace the `kb` value with the ID of the knowledge base you want to query for answers.</span></span> <span data-ttu-id="f4cdd-183">Note this knowledge base must already have been published using the [Publish](#Publish) method.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-183">Note this knowledge base must already have been published using the [Publish](#Publish) method.</span></span>
1. <span data-ttu-id="f4cdd-184">Run the program.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-184">Run the program.</span></span>

```java
import java.io.*;
import java.lang.reflect.Type;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

/*
 * Gson: https://github.com/google/gson
 * Maven info:
 *    <dependency>
 *      <groupId>com.google.code.gson</groupId>
 *      <artifactId>gson</artifactId>
 *      <version>2.8.1</version>
 *    </dependency>
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import com.google.gson.reflect.TypeToken;

/* NOTE: To compile and run this code:
1. Save this file as GetAnswers.java.
2. Run:
    javac GetAnswers.java -cp .;gson-2.8.1.jar -encoding UTF-8
3. Run:
    java -cp .;gson-2.8.1.jar GetAnswers
*/

public class GetAnswers {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

    // NOTE: Replace this with a valid host name.
    static String host = "ENTER HOST HERE";

    // NOTE: Replace this with a valid endpoint key.
    // This is not your subscription key.
    // To get your endpoint keys, call the GET /endpointkeys method.
    static String endpoint_key = "ENTER KEY HERE";

    // NOTE: Replace this with a valid knowledge base ID.
    // Make sure you have published the knowledge base with the
    // POST /knowledgebases/{knowledge base ID} method.
    static String kb = "ENTER KB ID HERE";

    static String method = "/qnamaker/knowledgebases/" + kb + "/generateAnswer";

    static String question = "{ 'question' : 'Is the QnA Maker Service free?', 'top' : 3 }";

    public static String PrettyPrint (String json_text) {
        JsonParser parser = new JsonParser();
        JsonElement json = parser.parse(json_text);
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

// Send an HTTP POST request.
    public static String Post (URL url, String content) throws Exception {
        HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
        connection.setRequestMethod("POST");
        connection.setRequestProperty("Content-Type", "application/json");
        connection.setRequestProperty("Content-Length", content.length() + "");
        connection.setRequestProperty("Authorization", "EndpointKey " + endpoint_key);
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

    public static String GetAnswers (String kb, String question) throws Exception {
        URL url = new URL(host + method);
        System.out.println ("Calling " + url.toString() + ".");
        return Post(url, question);
    }

    public static void main(String[] args) {
        try {
            String response = GetAnswers (kb, question);
            System.out.println (PrettyPrint(response));
        }
        catch (Exception e) {
            System.out.println (e);
        }
    }
}
```

<span data-ttu-id="f4cdd-185">**Get answers response**</span><span class="sxs-lookup"><span data-stu-id="f4cdd-185">**Get answers response**</span></span>

<span data-ttu-id="f4cdd-186">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f4cdd-186">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "answers": [
    {
      "questions": [
        "Can I use BitLocker with the Volume Shadow Copy Service?"
      ],
      "answer": "Yes. However, shadow copies made prior to enabling BitLocker will be automatically deleted when BitLocker is enabled on software-encrypted drives. If you are using a hardware encrypted drive, the shadow copies are retained.",
      "score": 17.3,
      "id": 62,
      "source": "https://docs.microsoft.com/en-us/windows/security/information-protection/bitlocker/bitlocker-frequently-asked-questions",
      "metadata": []
    },
...
  ]
}
```

[<span data-ttu-id="f4cdd-187">Back to top</span><span class="sxs-lookup"><span data-stu-id="f4cdd-187">Back to top</span></span>](#HOLTop)

<a name="GetKB"></a>

## <a name="get-information-about-a-knowledge-base"></a><span data-ttu-id="f4cdd-188">Get information about a knowledge base</span><span class="sxs-lookup"><span data-stu-id="f4cdd-188">Get information about a knowledge base</span></span>

<span data-ttu-id="f4cdd-189">The following code gets information about the specified knowledge base, using the [Get knowledge base details](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasedetails) method.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-189">The following code gets information about the specified knowledge base, using the [Get knowledge base details](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasedetails) method.</span></span>

1. <span data-ttu-id="f4cdd-190">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-190">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="f4cdd-191">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-191">Add the code provided below.</span></span>
3. <span data-ttu-id="f4cdd-192">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-192">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="f4cdd-193">Run the program.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-193">Run the program.</span></span>

```java
import java.io.*;
import java.lang.reflect.Type;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

/*
 * Gson: https://github.com/google/gson
 * Maven info:
 *    <dependency>
 *      <groupId>com.google.code.gson</groupId>
 *      <artifactId>gson</artifactId>
 *      <version>2.8.1</version>
 *    </dependency>
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import com.google.gson.reflect.TypeToken;

/* NOTE: To compile and run this code:
1. Save this file as GetKB.java.
2. Run:
    javac GetKB.java -cp .;gson-2.8.1.jar -encoding UTF-8
3. Run:
    java -cp .;gson-2.8.1.jar GetKB
*/

public class GetKB {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
    static String subscriptionKey = "ENTER KEY HERE";

// Replace this with a valid knowledge base ID.
    static String kb = "ENTER ID HERE";

    static String host = "https://westus.api.cognitive.microsoft.com";
    static String service = "/qnamaker/v4.0";
    static String method = "/knowledgebases/";

    public static String PrettyPrint (String json_text) {
        JsonParser parser = new JsonParser();
        JsonElement json = parser.parse(json_text);
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

// Send an HTTP GET request.
    public static String Get (URL url) throws Exception {
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

// Sends the request to get the knowledge base information.
    public static String GetKB (String kb) throws Exception {
        URL url = new URL (host + service + method + kb);
        System.out.println ("Calling " + url.toString() + ".");
        return Get(url);
    }

    public static void main(String[] args) {
        try {
            String response = GetKB (kb);
            System.out.println (PrettyPrint (response));
        }
        catch (Exception e) {
            System.out.println (e.getCause().getMessage());
        }
    }
}
```

<span data-ttu-id="f4cdd-194">**Get knowledge base details response**</span><span class="sxs-lookup"><span data-stu-id="f4cdd-194">**Get knowledge base details response**</span></span>

<span data-ttu-id="f4cdd-195">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f4cdd-195">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "id": "140a46f3-b248-4f1b-9349-614bfd6e5563",
  "hostName": "https://qna-docs.azurewebsites.net",
  "lastAccessedTimestamp": "2018-04-12T22:58:01Z",
  "lastChangedTimestamp": "2018-04-12T22:58:01Z",
  "name": "QnA Maker FAQ",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "urls": [
    "https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs",
    "https://docs.microsoft.com/en-us/bot-framework/resources-bot-framework-faq"
  ],
  "sources": [
    "Custom Editorial"
  ]
}
```

[<span data-ttu-id="f4cdd-196">Back to top</span><span class="sxs-lookup"><span data-stu-id="f4cdd-196">Back to top</span></span>](#HOLTop)

<a name="GetKBsByUser"></a>

## <a name="get-all-knowledge-bases-for-a-user"></a><span data-ttu-id="f4cdd-197">Get all knowledge bases for a user</span><span class="sxs-lookup"><span data-stu-id="f4cdd-197">Get all knowledge bases for a user</span></span>

<span data-ttu-id="f4cdd-198">The following code gets information about all knowledge bases for a specified user, using the [Get knowledge bases for user](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasesforuser) method.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-198">The following code gets information about all knowledge bases for a specified user, using the [Get knowledge bases for user](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_getknowledgebasesforuser) method.</span></span>

1. <span data-ttu-id="f4cdd-199">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-199">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="f4cdd-200">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-200">Add the code provided below.</span></span>
3. <span data-ttu-id="f4cdd-201">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-201">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="f4cdd-202">Run the program.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-202">Run the program.</span></span>

```java
import java.io.*;
import java.lang.reflect.Type;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

/*
 * Gson: https://github.com/google/gson
 * Maven info:
 *    <dependency>
 *      <groupId>com.google.code.gson</groupId>
 *      <artifactId>gson</artifactId>
 *      <version>2.8.1</version>
 *    </dependency>
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import com.google.gson.reflect.TypeToken;

/* NOTE: To compile and run this code:
1. Save this file as GetKBsByUser.java.
2. Run:
    javac GetKBsByUser.java -cp .;gson-2.8.1.jar -encoding UTF-8
3. Run:
    java -cp .;gson-2.8.1.jar GetKBsByUser
*/

public class GetKBsByUser {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
    static String subscriptionKey = "ENTER KEY HERE";

    static String host = "https://westus.api.cognitive.microsoft.com";
    static String service = "/qnamaker/v4.0";
    static String method = "/knowledgebases";

    public static String PrettyPrint (String json_text) {
        JsonParser parser = new JsonParser();
        JsonElement json = parser.parse(json_text);
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

// Send an HTTP GET request.
    public static String Get (URL url) throws Exception {
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

// Sends the request to get the knowledge bases for the specified user.
    public static String GetKBsByUser () throws Exception {
        URL url = new URL (host + service + method);
        System.out.println ("Calling " + url.toString() + ".");
        return Get(url);
    }

    public static void main(String[] args) {
        try {
            String response = GetKBsByUser ();
            System.out.println (PrettyPrint (response));
        }
        catch (Exception e) {
            System.out.println (e.getCause().getMessage());
        }
    }
}
```

<span data-ttu-id="f4cdd-203">**Get knowledge bases for user response**</span><span class="sxs-lookup"><span data-stu-id="f4cdd-203">**Get knowledge bases for user response**</span></span>

<span data-ttu-id="f4cdd-204">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f4cdd-204">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "knowledgebases": [
    {
      "id": "081c32a7-bd05-4982-9d74-07ac736df0ac",
      "hostName": "https://qna-docs.azurewebsites.net",
      "lastAccessedTimestamp": "2018-04-12T11:51:58Z",
      "lastChangedTimestamp": "2018-04-12T11:51:58Z",
      "name": "QnA Maker FAQ",
      "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
      "urls": [],
      "sources": []
    },
    {
      "id": "140a46f3-b248-4f1b-9349-614bfd6e5563",
      "hostName": "https://qna-docs.azurewebsites.net",
      "lastAccessedTimestamp": "2018-04-12T22:58:01Z",
      "lastChangedTimestamp": "2018-04-12T22:58:01Z",
      "name": "QnA Maker FAQ",
      "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
      "urls": [
        "https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs",
        "https://docs.microsoft.com/en-us/bot-framework/resources-bot-framework-faq"
      ],
      "sources": [
        "Custom Editorial"
      ]
    },
...
  ]
}
Press any key to continue.
```

[<span data-ttu-id="f4cdd-205">Back to top</span><span class="sxs-lookup"><span data-stu-id="f4cdd-205">Back to top</span></span>](#HOLTop)

<a name="Delete"></a>

## <a name="delete-a-knowledge-base"></a><span data-ttu-id="f4cdd-206">Delete a knowledge base</span><span class="sxs-lookup"><span data-stu-id="f4cdd-206">Delete a knowledge base</span></span>

<span data-ttu-id="f4cdd-207">The following code deletes the specified knowledge base, using the [Delete knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_delete) method.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-207">The following code deletes the specified knowledge base, using the [Delete knowledge base](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/knowledgebases_delete) method.</span></span>

1. <span data-ttu-id="f4cdd-208">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-208">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="f4cdd-209">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-209">Add the code provided below.</span></span>
3. <span data-ttu-id="f4cdd-210">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-210">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="f4cdd-211">Run the program.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-211">Run the program.</span></span>

```java
import java.io.*;
import java.lang.reflect.Type;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

/*
 * Gson: https://github.com/google/gson
 * Maven info:
 *    <dependency>
 *      <groupId>com.google.code.gson</groupId>
 *      <artifactId>gson</artifactId>
 *      <version>2.8.1</version>
 *    </dependency>
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import com.google.gson.reflect.TypeToken;

/* NOTE: To compile and run this code:
1. Save this file as DeleteKB.java.
2. Run:
    javac DeleteKB.java -cp .;gson-2.8.1.jar -encoding UTF-8
3. Run:
    java -cp .;gson-2.8.1.jar DeleteKB
*/

public class DeleteKB {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
    static String subscriptionKey = "ENTER KEY HERE";

// Replace this with a valid knowledge base ID.
    static String kb = "ENTER ID HERE";

    static String host = "https://westus.api.cognitive.microsoft.com";
    static String service = "/qnamaker/v4.0";
    static String method = "/knowledgebases/";

    public static String PrettyPrint (String json_text) {
        JsonParser parser = new JsonParser();
        JsonElement json = parser.parse(json_text);
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

// Send an HTTP DELETE request.
    public static String Delete (URL url) throws Exception {
        HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
        connection.setRequestMethod("DELETE");
        connection.setRequestProperty("Ocp-Apim-Subscription-Key", subscriptionKey);
        connection.setDoOutput(true);

        if (connection.getResponseCode() == 204)
        {
            return "{'result' : 'Success.'}";
        }
        else {
            StringBuilder response = new StringBuilder ();
            BufferedReader in = new BufferedReader(new InputStreamReader(connection.getErrorStream(), "UTF-8"));

            String line;
            while ((line = in.readLine()) != null) {
                response.append(line);
            }
            in.close();

            return response.toString();
        }
    }

// Sends the request to delete the knowledge base.
    public static String DeleteKB (String kb) throws Exception {
        URL url = new URL (host + service + method + kb);
        System.out.println ("Calling " + url.toString() + ".");
        return Delete(url);
    }

    public static void main(String[] args) {
        try {
            String response = DeleteKB (kb);
            System.out.println (PrettyPrint (response));
        }
        catch (Exception e) {
            System.out.println (e.getCause().getMessage());
        }
    }
}
```

<span data-ttu-id="f4cdd-212">**Delete knowledge base response**</span><span class="sxs-lookup"><span data-stu-id="f4cdd-212">**Delete knowledge base response**</span></span>

<span data-ttu-id="f4cdd-213">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f4cdd-213">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "result": "Success."
}
```

[<span data-ttu-id="f4cdd-214">Back to top</span><span class="sxs-lookup"><span data-stu-id="f4cdd-214">Back to top</span></span>](#HOLTop)

<a name="GetKeys"></a>

## <a name="get-endpoint-keys"></a><span data-ttu-id="f4cdd-215">Get endpoint keys</span><span class="sxs-lookup"><span data-stu-id="f4cdd-215">Get endpoint keys</span></span>

<span data-ttu-id="f4cdd-216">The following code gets the current endpoint keys, using the [Get endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_getendpointkeys) method.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-216">The following code gets the current endpoint keys, using the [Get endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_getendpointkeys) method.</span></span>

1. <span data-ttu-id="f4cdd-217">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-217">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="f4cdd-218">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-218">Add the code provided below.</span></span>
3. <span data-ttu-id="f4cdd-219">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-219">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="f4cdd-220">Run the program.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-220">Run the program.</span></span>

```java
import java.io.*;
import java.lang.reflect.Type;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

/*
 * Gson: https://github.com/google/gson
 * Maven info:
 *    <dependency>
 *      <groupId>com.google.code.gson</groupId>
 *      <artifactId>gson</artifactId>
 *      <version>2.8.1</version>
 *    </dependency>
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import com.google.gson.reflect.TypeToken;

/* NOTE: To compile and run this code:
1. Save this file as GetEndpointKeys.java.
2. Run:
    javac GetEndpointKeys.java -cp .;gson-2.8.1.jar -encoding UTF-8
3. Run:
    java -cp .;gson-2.8.1.jar GetEndpointKeys
*/

public class GetEndpointKeys {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
    static String subscriptionKey = "ENTER KEY HERE";

    static String host = "https://westus.api.cognitive.microsoft.com";
    static String service = "/qnamaker/v4.0";
    static String method = "/endpointkeys";

    public static String PrettyPrint (String json_text) {
        JsonParser parser = new JsonParser();
        JsonElement json = parser.parse(json_text);
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

// Send an HTTP GET request.
    public static String Get (URL url) throws Exception {
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

// Sends the request to get the endpoint keys.
    public static String GetEndpointKeys () throws Exception {
        URL url = new URL (host + service + method);
        System.out.println ("Calling " + url.toString() + ".");
        return Get(url);
    }

    public static void main(String[] args) {
        try {
            String response = GetEndpointKeys ();
            System.out.println (PrettyPrint (response));
        }
        catch (Exception e) {
            System.out.println (e.getCause().getMessage());
        }
    }
}
```

<span data-ttu-id="f4cdd-221">**Get endpoint keys response**</span><span class="sxs-lookup"><span data-stu-id="f4cdd-221">**Get endpoint keys response**</span></span>

<span data-ttu-id="f4cdd-222">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f4cdd-222">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "primaryEndpointKey": "ac110bdc-34b7-4b1c-b9cd-b05f9a6001f3",
  "secondaryEndpointKey": "1b4ed14e-614f-444a-9f3d-9347f45a9206"
}
```

[<span data-ttu-id="f4cdd-223">Back to top</span><span class="sxs-lookup"><span data-stu-id="f4cdd-223">Back to top</span></span>](#HOLTop)

<a name="PutKeys"></a>

## <a name="refresh-endpoint-keys"></a><span data-ttu-id="f4cdd-224">Refresh endpoint keys</span><span class="sxs-lookup"><span data-stu-id="f4cdd-224">Refresh endpoint keys</span></span>

<span data-ttu-id="f4cdd-225">The following code regenerates the current endpoint keys, using the [Refresh endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_refreshendpointkeys) method.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-225">The following code regenerates the current endpoint keys, using the [Refresh endpoint keys](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/endpointkeys_refreshendpointkeys) method.</span></span>

1. <span data-ttu-id="f4cdd-226">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-226">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="f4cdd-227">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-227">Add the code provided below.</span></span>
3. <span data-ttu-id="f4cdd-228">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-228">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="f4cdd-229">Run the program.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-229">Run the program.</span></span>

```java
import java.io.*;
import java.lang.reflect.Type;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

/*
 * Gson: https://github.com/google/gson
 * Maven info:
 *    <dependency>
 *      <groupId>com.google.code.gson</groupId>
 *      <artifactId>gson</artifactId>
 *      <version>2.8.1</version>
 *    </dependency>
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import com.google.gson.reflect.TypeToken;

// Java does not natively support HTTP PATCH requests, so Apache HttpClient is required.
/*
 * HttpClient: http://hc.apache.org/downloads.cgi
 * Maven info:
 *    <dependency>
 *      <groupId>org.apache.httpcomponents</groupId>
 *      <artifactId>httpclient</artifactId>
 *      <version>4.5.5</version>
 *    </dependency>
 */
import org.apache.commons.logging.LogFactory;
import org.apache.http.client.methods.HttpPatch;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.entity.ByteArrayEntity;
import org.apache.http.Header;
import org.apache.http.HttpEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;

/* NOTE: To compile and run this code:
1. Save this file as RefreshKeys.java.
2. Run:
    javac RefreshKeys.java -cp .;gson-2.8.1.jar;httpclient-4.5.5.jar;httpcore-4.4.9.jar;commons-logging-1.2.jar -encoding UTF-8
3. Run:
    java -cp .;gson-2.8.1.jar;httpclient-4.5.5.jar;httpcore-4.4.9.jar;commons-logging-1.2.jar RefreshKeys
*/

public class RefreshKeys {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
    static String subscriptionKey = "ENTER KEY HERE";

// Replace this with "PrimaryKey" or "SecondaryKey."
    static String key_type = "PrimaryKey";

    static String host = "https://westus.api.cognitive.microsoft.com";
    static String service = "/qnamaker/v4.0";
    static String method = "/endpointkeys/";

    public static String PrettyPrint (String json_text) {
        JsonParser parser = new JsonParser();
        JsonElement json = parser.parse(json_text);
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

// Send an HTTP PATCH request. We use Apache HttpClient to do this, as HttpsURLConnection does not support PATCH.
    public static String Patch (URL url, String content) throws Exception {
        HttpPatch patch = new HttpPatch(url.toString());
        // HttpPatch implements HttpMessage, which includes addHeader. See:
        // https://hc.apache.org/httpcomponents-client-ga/httpclient/apidocs/org/apache/http/client/methods/HttpPatch.html
        // http://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/HttpMessage.html
        patch.addHeader("Content-Type", "application/json");
        // Note: Adding the Content-Length header causes the exception:
        // "Content-Length header already present."
        patch.addHeader("Ocp-Apim-Subscription-Key", subscriptionKey);
        // HttpPatch implements HttpEntityEnclosingRequest, which includes setEntity. See:
        // http://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/HttpEntityEnclosingRequest.html
        HttpEntity entity = new ByteArrayEntity(content.getBytes("UTF-8"));
        patch.setEntity(entity);

        CloseableHttpClient httpClient = HttpClients.createDefault();
        CloseableHttpResponse response = httpClient.execute(patch);

        // CloseableHttpResponse implements HttpMessage, which includes getAllHeaders. See:
        // https://hc.apache.org/httpcomponents-client-ga/httpclient/apidocs/org/apache/http/client/methods/CloseableHttpResponse.html
        // Header implements NameValuePair. See:
        // http://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/Header.html
        // http://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/NameValuePair.html
        Map<String, List<String>> headers = new HashMap<String, List<String>>();
        for (Header header : response.getAllHeaders()) {
            List<String> list = new ArrayList<String>() {
                {
                    add(header.getValue());
                }
            };
            headers.put(header.getName(), list);
        }

        // CloseableHttpResponse implements HttpResponse, which includes getEntity. See:
        // http://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/HttpResponse.html
        // HttpEntity implements getContent, which returns an InputStream. See:
        // http://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/HttpEntity.html
        StringBuilder output = new StringBuilder ();
        BufferedReader reader = new BufferedReader(new InputStreamReader(response.getEntity().getContent(), "UTF-8"));
        String line;
        while ((line = reader.readLine()) != null) {
            output.append(line);
        }
        reader.close();

        return output.toString();
    }

// Sends the request to refresh the endpoint keys.
    public static String RefreshKeys () throws Exception {
        URL url = new URL(host + service + method + key_type);
        System.out.println ("Calling " + url.toString() + ".");
        return Patch(url, "");
    }

    public static void main(String[] args) {
        try {
            String response = RefreshKeys ();
            System.out.println (PrettyPrint (response));
        }
        catch (Exception e) {
            System.out.println (e.getCause().getMessage());
        }
    }
}
```

<span data-ttu-id="f4cdd-230">**Refresh endpoint keys response**</span><span class="sxs-lookup"><span data-stu-id="f4cdd-230">**Refresh endpoint keys response**</span></span>

<span data-ttu-id="f4cdd-231">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f4cdd-231">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "primaryEndpointKey": "ac110bdc-34b7-4b1c-b9cd-b05f9a6001f3",
  "secondaryEndpointKey": "1b4ed14e-614f-444a-9f3d-9347f45a9206"
}
```

[<span data-ttu-id="f4cdd-232">Back to top</span><span class="sxs-lookup"><span data-stu-id="f4cdd-232">Back to top</span></span>](#HOLTop)

<a name="GetAlterations"></a>

## <a name="get-word-alterations"></a><span data-ttu-id="f4cdd-233">Get word alterations</span><span class="sxs-lookup"><span data-stu-id="f4cdd-233">Get word alterations</span></span>

<span data-ttu-id="f4cdd-234">The following code gets the current word alterations, using the [Download alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fc) method.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-234">The following code gets the current word alterations, using the [Download alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fc) method.</span></span>

1. <span data-ttu-id="f4cdd-235">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-235">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="f4cdd-236">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-236">Add the code provided below.</span></span>
3. <span data-ttu-id="f4cdd-237">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-237">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="f4cdd-238">Run the program.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-238">Run the program.</span></span>

```java
import java.io.*;
import java.lang.reflect.Type;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

/*
 * Gson: https://github.com/google/gson
 * Maven info:
 *    <dependency>
 *      <groupId>com.google.code.gson</groupId>
 *      <artifactId>gson</artifactId>
 *      <version>2.8.1</version>
 *    </dependency>
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import com.google.gson.reflect.TypeToken;

/* NOTE: To compile and run this code:
1. Save this file as GetAlterations.java.
2. Run:
    javac GetAlterations.java -cp .;gson-2.8.1.jar -encoding UTF-8
3. Run:
    java -cp .;gson-2.8.1.jar GetAlterations
*/

public class GetAlterations {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
    static String subscriptionKey = "ENTER KEY HERE";

    static String host = "https://westus.api.cognitive.microsoft.com";
    static String service = "/qnamaker/v4.0";
    static String method = "/alterations/";

    public static String PrettyPrint (String json_text) {
        JsonParser parser = new JsonParser();
        JsonElement json = parser.parse(json_text);
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

// Send an HTTP GET request.
    public static String Get (URL url) throws Exception {
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

// Sends the request to get the alterations.
    public static String GetAlterations () throws Exception {
        URL url = new URL (host + service + method);
        System.out.println ("Calling " + url.toString() + ".");
        return Get(url);
    }

    public static void main(String[] args) {
        try {
            String response = GetAlterations ();
            System.out.println (PrettyPrint (response));
        }
        catch (Exception e) {
            System.out.println (e.getCause().getMessage());
        }
    }
}
```

<span data-ttu-id="f4cdd-239">**Get word alterations response**</span><span class="sxs-lookup"><span data-stu-id="f4cdd-239">**Get word alterations response**</span></span>

<span data-ttu-id="f4cdd-240">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f4cdd-240">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "wordAlterations": [
    {
      "alterations": [
        "botframework",
        "bot frame work"
      ]
    }
  ]
}
```

[<span data-ttu-id="f4cdd-241">Back to top</span><span class="sxs-lookup"><span data-stu-id="f4cdd-241">Back to top</span></span>](#HOLTop)

<a name="PutAlterations"></a>

## <a name="replace-word-alterations"></a><span data-ttu-id="f4cdd-242">Replace word alterations</span><span class="sxs-lookup"><span data-stu-id="f4cdd-242">Replace word alterations</span></span>

<span data-ttu-id="f4cdd-243">The following code replaces the current word alterations, using the [Replace alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fd) method.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-243">The following code replaces the current word alterations, using the [Replace alterations](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fd) method.</span></span>

1. <span data-ttu-id="f4cdd-244">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-244">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="f4cdd-245">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-245">Add the code provided below.</span></span>
3. <span data-ttu-id="f4cdd-246">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-246">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="f4cdd-247">Run the program.</span><span class="sxs-lookup"><span data-stu-id="f4cdd-247">Run the program.</span></span>

```java
import java.io.*;
import java.lang.reflect.Type;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

/*
 * Gson: https://github.com/google/gson
 * Maven info:
 *    <dependency>
 *      <groupId>com.google.code.gson</groupId>
 *      <artifactId>gson</artifactId>
 *      <version>2.8.1</version>
 *    </dependency>
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import com.google.gson.reflect.TypeToken;

/* NOTE: To compile and run this code:
1. Save this file as PutAlterations.java.
2. Run:
    javac PutAlterations.java -cp .;gson-2.8.1.jar -encoding UTF-8
3. Run:
    java -cp .;gson-2.8.1.jar PutAlterations
*/

public class PutAlterations {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace this with a valid subscription key.
    static String subscriptionKey = "ENTER KEY HERE";

    static String host = "https://westus.api.cognitive.microsoft.com";
    static String service = "/qnamaker/v4.0";
    static String method = "/alterations/";

// We'll serialize these classes into JSON for our request to the server.
// For the JSON request schema, see:
// https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fd
    public static class Request {
        Alteration[] wordAlterations;
    }

    public static class Alteration {
        String[] alterations;
    }

    public static String PrettyPrint (String json_text) {
        JsonParser parser = new JsonParser();
        JsonElement json = parser.parse(json_text);
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

// Send an HTTP PUT request.
    public static String Put (URL url, String content) throws Exception {
        HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
        connection.setRequestMethod("PUT");
        connection.setRequestProperty("Content-Type", "application/json");
        connection.setRequestProperty("Content-Length", content.length() + "");
        connection.setRequestProperty("Ocp-Apim-Subscription-Key", subscriptionKey);
        connection.setDoOutput(true);

        DataOutputStream wr = new DataOutputStream(connection.getOutputStream());
        byte[] encoded_content = content.getBytes("UTF-8");
        wr.write(encoded_content, 0, encoded_content.length);
        wr.flush();
        wr.close();

        if (connection.getResponseCode() == 204)
        {
            return "{'result' : 'Success.'}";
        }
        else {
            StringBuilder response = new StringBuilder ();
            BufferedReader in = new BufferedReader(new InputStreamReader(connection.getErrorStream(), "UTF-8"));

            String line;
            while ((line = in.readLine()) != null) {
                response.append(line);
            }
            in.close();

            return response.toString();
        }
    }

// Sends the request to replace the alterations.
    public static String PutAlterations (Request req) throws Exception {
        URL url = new URL(host + service + method);
        System.out.println ("Calling " + url.toString() + ".");
        String content = new Gson().toJson(req);

        return Put(url, content);
    }

// Returns a sample request to replace the alterations..
    public static Request GetRequest () {
        Request req = new Request ();

        Alteration alteration = new Alteration();
        alteration.alterations = new String[]{ "botframework", "bot frame work" };
        req.wordAlterations = new Alteration[]{ alteration };

        return req;
    }

    public static void main(String[] args) {
        try {
            String response = PutAlterations (GetRequest ());
            System.out.println (PrettyPrint (response));
        }
        catch (Exception e) {
            System.out.println (e.getCause().getMessage());
        }
    }
}
```

<span data-ttu-id="f4cdd-248">**Replace word alterations response**</span><span class="sxs-lookup"><span data-stu-id="f4cdd-248">**Replace word alterations response**</span></span>

<span data-ttu-id="f4cdd-249">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="f4cdd-249">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "result": "Success."
}
```

[<span data-ttu-id="f4cdd-250">Back to top</span><span class="sxs-lookup"><span data-stu-id="f4cdd-250">Back to top</span></span>](#HOLTop)

## <a name="next-steps"></a><span data-ttu-id="f4cdd-251">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4cdd-251">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f4cdd-252">QnA Maker (V4) REST API Reference</span><span class="sxs-lookup"><span data-stu-id="f4cdd-252">QnA Maker (V4) REST API Reference</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff)

## <a name="see-also"></a><span data-ttu-id="f4cdd-253">See also</span><span class="sxs-lookup"><span data-stu-id="f4cdd-253">See also</span></span> 

[<span data-ttu-id="f4cdd-254">QnA Maker overview</span><span class="sxs-lookup"><span data-stu-id="f4cdd-254">QnA Maker overview</span></span>](../Overview/overview.md)
