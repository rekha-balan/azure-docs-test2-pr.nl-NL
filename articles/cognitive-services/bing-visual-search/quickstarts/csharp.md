---
title: C# Quickstart for Bing Visual Search API | Microsoft Docs
titleSuffix: Bing Web Search APIs - Cognitive Services
description: Shows how to upload an image to Bing Visual Search API and get back insights about the image.
services: cognitive-services
author: swhite-msft
manager: rosh
ms.service: cognitive-services
ms.technology: bing-visual-search
ms.topic: article
ms.date: 5/16/2018
ms.author: scottwhi
ms.openlocfilehash: 930a89e3b1996c44f12bd3773565eda40e93ca9c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867251"
---
# <a name="your-first-bing-visual-search-query-in-c"></a><span data-ttu-id="e9333-103">Your first Bing Visual Search query in C#</span><span class="sxs-lookup"><span data-stu-id="e9333-103">Your first Bing Visual Search query in C#</span></span>

<span data-ttu-id="e9333-104">Bing Visual Search API returns information about an image that you provide.</span><span class="sxs-lookup"><span data-stu-id="e9333-104">Bing Visual Search API returns information about an image that you provide.</span></span> <span data-ttu-id="e9333-105">You can provide the image by using the URL of the image, an insights token, or by uploading an image.</span><span class="sxs-lookup"><span data-stu-id="e9333-105">You can provide the image by using the URL of the image, an insights token, or by uploading an image.</span></span> <span data-ttu-id="e9333-106">For information about these options, see [What is Bing Visual Search API?](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="e9333-106">For information about these options, see [What is Bing Visual Search API?](../overview.md)</span></span> <span data-ttu-id="e9333-107">This article demonstrates uploading an image.</span><span class="sxs-lookup"><span data-stu-id="e9333-107">This article demonstrates uploading an image.</span></span> <span data-ttu-id="e9333-108">Uploading an image could be useful in mobile scenarios where you take a picture of a well-known landmark and get back information about it.</span><span class="sxs-lookup"><span data-stu-id="e9333-108">Uploading an image could be useful in mobile scenarios where you take a picture of a well-known landmark and get back information about it.</span></span> <span data-ttu-id="e9333-109">For example, the insights could include trivia about the landmark.</span><span class="sxs-lookup"><span data-stu-id="e9333-109">For example, the insights could include trivia about the landmark.</span></span> 

<span data-ttu-id="e9333-110">If you upload a local image, the following shows the form data you must include in the body of the POST.</span><span class="sxs-lookup"><span data-stu-id="e9333-110">If you upload a local image, the following shows the form data you must include in the body of the POST.</span></span> <span data-ttu-id="e9333-111">The form data must include the Content-Disposition header.</span><span class="sxs-lookup"><span data-stu-id="e9333-111">The form data must include the Content-Disposition header.</span></span> <span data-ttu-id="e9333-112">Its `name` parameter must be set to "image" and the `filename` parameter may be set to any string.</span><span class="sxs-lookup"><span data-stu-id="e9333-112">Its `name` parameter must be set to "image" and the `filename` parameter may be set to any string.</span></span> <span data-ttu-id="e9333-113">The contents of the form is the binary of the image.</span><span class="sxs-lookup"><span data-stu-id="e9333-113">The contents of the form is the binary of the image.</span></span> <span data-ttu-id="e9333-114">The maximum image size you may upload is 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e9333-114">The maximum image size you may upload is 1 MB.</span></span> 

```
--boundary_1234-abcd
Content-Disposition: form-data; name="image"; filename="myimagefile.jpg"

ÿØÿà JFIF ÖÆ68g-¤CWŸþ29ÌÄøÖ‘º«™æ±èuZiÀ)"óÓß°Î= ØJ9á+*G¦...

--boundary_1234-abcd--
```

<span data-ttu-id="e9333-115">This article includes a simple console application that sends a Bing Visual Search API request and displays the JSON search results.</span><span class="sxs-lookup"><span data-stu-id="e9333-115">This article includes a simple console application that sends a Bing Visual Search API request and displays the JSON search results.</span></span> <span data-ttu-id="e9333-116">While this application is written in C#, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span><span class="sxs-lookup"><span data-stu-id="e9333-116">While this application is written in C#, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span></span> 

<span data-ttu-id="e9333-117">The example program uses .NET Core classes only and runs on Windows using the .NET CLR or on Linux or macOS using [Mono](http://www.mono-project.com/).</span><span class="sxs-lookup"><span data-stu-id="e9333-117">The example program uses .NET Core classes only and runs on Windows using the .NET CLR or on Linux or macOS using [Mono](http://www.mono-project.com/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e9333-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e9333-118">Prerequisites</span></span>

<span data-ttu-id="e9333-119">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to get this code running on Windows.</span><span class="sxs-lookup"><span data-stu-id="e9333-119">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to get this code running on Windows.</span></span> <span data-ttu-id="e9333-120">(The free Community Edition will work.)</span><span class="sxs-lookup"><span data-stu-id="e9333-120">(The free Community Edition will work.)</span></span>

<span data-ttu-id="e9333-121">For this quickstart, you may use a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) subscription key or a paid subscription key.</span><span class="sxs-lookup"><span data-stu-id="e9333-121">For this quickstart, you may use a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) subscription key or a paid subscription key.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="e9333-122">Running the application</span><span class="sxs-lookup"><span data-stu-id="e9333-122">Running the application</span></span>

<span data-ttu-id="e9333-123">The following shows how to send the message using HttpWebRequest.</span><span class="sxs-lookup"><span data-stu-id="e9333-123">The following shows how to send the message using HttpWebRequest.</span></span> <span data-ttu-id="e9333-124">For an example that uses HttpClient, HttpRequestMessage, and MultipartFormDataContent, see [Using HttpClient](#using-httpclient).</span><span class="sxs-lookup"><span data-stu-id="e9333-124">For an example that uses HttpClient, HttpRequestMessage, and MultipartFormDataContent, see [Using HttpClient](#using-httpclient).</span></span>

<span data-ttu-id="e9333-125">To run this application, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="e9333-125">To run this application, follow these steps:</span></span>

1. <span data-ttu-id="e9333-126">Create a new Console solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e9333-126">Create a new Console solution in Visual Studio.</span></span>
1. <span data-ttu-id="e9333-127">Replace the contents of `Program.cs` with the code shown in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="e9333-127">Replace the contents of `Program.cs` with the code shown in this quickstart.</span></span>
2. <span data-ttu-id="e9333-128">Replace the `accessKey` value with your subscription key.</span><span class="sxs-lookup"><span data-stu-id="e9333-128">Replace the `accessKey` value with your subscription key.</span></span>
2. <span data-ttu-id="e9333-129">Replace the `imagePath` value with the path of the image to upload.</span><span class="sxs-lookup"><span data-stu-id="e9333-129">Replace the `imagePath` value with the path of the image to upload.</span></span>
3. <span data-ttu-id="e9333-130">Run the program.</span><span class="sxs-lookup"><span data-stu-id="e9333-130">Run the program.</span></span>


```csharp
using System;
using System.Text;
using System.Net;
using System.IO;
using System.Collections.Generic;

namespace VisualSearchUpload
{

    class Program
    {
        // **********************************************
        // *** Update and verify the following values. ***
        // **********************************************

        // Replace the accessKey string value with your valid subscription key.
        const string accessKey = "<yoursubscriptionkeygoeshere>";

        const string uriBase = "https://api.cognitive.microsoft.com/bing/v7.0/images/visualsearch";

        // Set the path to the image that you want to get insights of. 
        static string imagePath = @"<pathtoimagegoeshere>";

        // Boundary strings for form data in body of POST.
        const string CRLF = "\r\n";
        static string BoundaryTemplate = "batch_{0}";
        static string StartBoundaryTemplate = "--{0}";
        static string EndBoundaryTemplate = "--{0}--";

        const string CONTENT_TYPE_HEADER_PARAMS = "multipart/form-data; boundary={0}";
        const string POST_BODY_DISPOSITION_HEADER = "Content-Disposition: form-data; name=\"image\"; filename=\"{0}\"" + CRLF +CRLF;


        static void Main()
        {
            try
            {
                Console.OutputEncoding = System.Text.Encoding.UTF8;

                if (accessKey.Length == 32)
                {
                    if (IsImagePathSet(imagePath))
                    {
                        var filename = GetImageFileName(imagePath);
                        Console.WriteLine("Getting image insights for image: " + filename);
                        var imageBinary = GetImageBinary(imagePath);

                        // Set up POST body.
                        var boundary = string.Format(BoundaryTemplate, Guid.NewGuid());
                        var startFormData = BuildFormDataStart(boundary, filename);
                        var endFormData = BuildFormDataEnd(boundary);
                        var contentTypeHdrValue = string.Format(CONTENT_TYPE_HEADER_PARAMS, boundary);

                        var json = BingImageSearch(startFormData, endFormData, imageBinary, contentTypeHdrValue);

                        Console.WriteLine("\nJSON Response:\n");
                        Console.WriteLine(JsonPrettyPrint(json));
                    }
                }
                else
                {
                    Console.WriteLine("Invalid Bing Visual Search API subscription key!");
                    Console.WriteLine("Please paste yours into the source code.");
                }

                Console.Write("\nPress Enter to exit ");
                Console.ReadLine();
            }
            catch (Exception e)
            {
                Console.WriteLine(e.Message);
            }
        }



        /// <summary>
        /// Verify that imagePath exists.
        /// </summary>
        static Boolean IsImagePathSet(string path)
        {
            if (string.IsNullOrEmpty(path))
                throw new ArgumentException("Image path is null or empty.");

            if (!File.Exists(path))
                throw new ArgumentException("Image path does not exist.");

            var size = new FileInfo(path).Length;

            if (size > 1000000)
                throw new ArgumentException("Image is greater than the 1 MB maximum size.");

            return true;
        }



        /// <summary>
        /// Get the binary characters of an image.
        /// </summary>
        static byte[] GetImageBinary(string path)
        {
            return File.ReadAllBytes(path);
        }


        /// <summary>
        /// Get the image's filename.
        /// </summary>
        static string GetImageFileName(string path)
        {
            return new FileInfo(path).Name;
        }


        /// <summary>
        /// Build the beginning part of the form data.
        /// </summary>
        static string BuildFormDataStart(string boundary, string filename)
        {
            var startBoundary = string.Format(StartBoundaryTemplate, boundary);

            var requestBody = startBoundary + CRLF;
            requestBody += string.Format(POST_BODY_DISPOSITION_HEADER, filename);

            return requestBody;
        }


        /// <summary>
        /// Build the ending part of the form data.
        /// </summary>
        static string BuildFormDataEnd(string boundary)
        {
            return CRLF + CRLF + string.Format(EndBoundaryTemplate, boundary) + CRLF;
        }



        /// <summary>
        /// Calls the Bing visual search endpoint and returns the JSON response.
        /// </summary>
        static string BingImageSearch(string startFormData, string endFormData, byte[] image, string contentTypeValue)
        {
            WebRequest request = HttpWebRequest.Create(uriBase);
            request.ContentType = contentTypeValue;
            request.Headers["Ocp-Apim-Subscription-Key"] = accessKey;
            request.Method = "POST";

            // Writes the boundary and Content-Disposition header, then writes
            // the image binary, and finishes by writing the closing boundary.
            using (Stream requestStream = request.GetRequestStream())
            {
                StreamWriter writer = new StreamWriter(requestStream);
                writer.Write(startFormData);
                writer.Flush();
                requestStream.Write(image, 0, image.Length);
                writer.Write(endFormData);
                writer.Flush();
                writer.Close();
            }


            HttpWebResponse response = (HttpWebResponse)request.GetResponseAsync().Result;
            string json = new StreamReader(response.GetResponseStream()).ReadToEnd();

            return json;
        }


        /// <summary>
        /// Formats the given JSON string by adding line breaks and indents.
        /// </summary>
        /// <param name="json">The raw JSON string to format.</param>
        /// <returns>The formatted JSON string.</returns>
        static string JsonPrettyPrint(string json)
        {
            if (string.IsNullOrEmpty(json))
                return string.Empty;

            json = json.Replace(Environment.NewLine, "").Replace("\t", "");

            StringBuilder sb = new StringBuilder();
            bool quote = false;
            bool ignore = false;
            char last = ' ';
            int offset = 0;
            int indentLength = 2;

            foreach (char ch in json)
            {
                switch (ch)
                {
                    case '"':
                        if (!ignore) quote = !quote;
                        break;
                    case '\\':
                        if (quote && last != '\\') ignore = true;
                        break;
                }

                if (quote)
                {
                    sb.Append(ch);
                    if (last == '\\' && ignore) ignore = false;
                }
                else
                {
                    switch (ch)
                    {
                        case '{':
                        case '[':
                            sb.Append(ch);
                            sb.Append(Environment.NewLine);
                            sb.Append(new string(' ', ++offset * indentLength));
                            break;
                        case '}':
                        case ']':
                            sb.Append(Environment.NewLine);
                            sb.Append(new string(' ', --offset * indentLength));
                            sb.Append(ch);
                            break;
                        case ',':
                            sb.Append(ch);
                            sb.Append(Environment.NewLine);
                            sb.Append(new string(' ', offset * indentLength));
                            break;
                        case ':':
                            sb.Append(ch);
                            sb.Append(' ');
                            break;
                        default:
                            if (quote || ch != ' ') sb.Append(ch);
                            break;
                    }
                }
                last = ch;
            }

            return sb.ToString().Trim();
        }
    }
}
```


## <a name="using-httpclient"></a><span data-ttu-id="e9333-131">Using HttpClient</span><span class="sxs-lookup"><span data-stu-id="e9333-131">Using HttpClient</span></span>

<span data-ttu-id="e9333-132">If you use HttpClient, you can use MultipartFormDataContent to build the form data.</span><span class="sxs-lookup"><span data-stu-id="e9333-132">If you use HttpClient, you can use MultipartFormDataContent to build the form data.</span></span> <span data-ttu-id="e9333-133">Just use the following sections of code to replace the same named methods in the previous example.</span><span class="sxs-lookup"><span data-stu-id="e9333-133">Just use the following sections of code to replace the same named methods in the previous example.</span></span>

<span data-ttu-id="e9333-134">Replace the Main method with this code:</span><span class="sxs-lookup"><span data-stu-id="e9333-134">Replace the Main method with this code:</span></span>

```csharp
        static void Main()
        {
            try
            {
                Console.OutputEncoding = System.Text.Encoding.UTF8;

                if (accessKey.Length == 32)
                {
                    if (IsImagePathSet(imagePath))
                    {
                        var filename = GetImageFileName(imagePath);
                        Console.WriteLine("Getting image insights for image: " + filename);
                        var imageBinary = GetImageBinary(imagePath);

                        var boundary = string.Format(BoundaryTemplate, Guid.NewGuid());
                        var json = BingImageSearch(imageBinary, boundary, uriBase, accessKey);

                        Console.WriteLine("\nJSON Response:\n");
                        Console.WriteLine(JsonPrettyPrint(json));
                    }
                }
                else
                {
                    Console.WriteLine("Invalid Bing Visual Search API subscription key!");
                    Console.WriteLine("Please paste yours into the source code.");
                }

                Console.Write("\nPress Enter to exit ");
                Console.ReadLine();
            }
            catch (Exception e)
            {
                Console.WriteLine(e.Message);
            }
        }
```

<span data-ttu-id="e9333-135">Replace the BingImageSearch method with this code:</span><span class="sxs-lookup"><span data-stu-id="e9333-135">Replace the BingImageSearch method with this code:</span></span>

```csharp
        /// <summary>
        /// Calls the Bing visual search endpoint and returns the JSON response.
        /// </summary>
        static string BingImageSearch(byte[] image, string boundary, string uri, string subscriptionKey)
        {
            var requestMessage = new HttpRequestMessage(HttpMethod.Post, uri);
            requestMessage.Headers.Add("Ocp-Apim-Subscription-Key", accessKey);

            var content = new MultipartFormDataContent(boundary);
            content.Add(new ByteArrayContent(image), "image", "myimage");
            requestMessage.Content = content;

            var httpClient = new HttpClient();

            Task<HttpResponseMessage> httpRequest = httpClient.SendAsync(requestMessage, HttpCompletionOption.ResponseContentRead, CancellationToken.None);
            HttpResponseMessage httpResponse = httpRequest.Result;
            HttpStatusCode statusCode = httpResponse.StatusCode;
            HttpContent responseContent = httpResponse.Content;

            string json = null;

            if (responseContent != null)
            {
                Task<String> stringContentsTask = responseContent.ReadAsStringAsync();
                json = stringContentsTask.Result;
            }

            return json;
        }
```




## <a name="next-steps"></a><span data-ttu-id="e9333-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="e9333-136">Next steps</span></span>

[<span data-ttu-id="e9333-137">Get insights about an image using an insights token</span><span class="sxs-lookup"><span data-stu-id="e9333-137">Get insights about an image using an insights token</span></span>](../use-insights-token.md)  
<span data-ttu-id="e9333-138">[Bing Visual Search image upload tutorial](../tutorial-visual-search-image-upload.md)
[Bing Visual Search single-page app tutorial](../tutorial-bing-visual-search-single-page-app.md)
[Bing Visual Search overview](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="e9333-138">[Bing Visual Search image upload tutorial](../tutorial-visual-search-image-upload.md)
[Bing Visual Search single-page app tutorial](../tutorial-bing-visual-search-single-page-app.md)
[Bing Visual Search overview](../overview.md)</span></span>  
[<span data-ttu-id="e9333-139">Try it</span><span class="sxs-lookup"><span data-stu-id="e9333-139">Try it</span></span>](https://aka.ms/bingvisualsearchtryforfree)  
[<span data-ttu-id="e9333-140">Get a free trial access key</span><span class="sxs-lookup"><span data-stu-id="e9333-140">Get a free trial access key</span></span>](https://azure.microsoft.com/try/cognitive-services/?api=bing-visual-search-api)  
[<span data-ttu-id="e9333-141">Bing Visual Search API reference</span><span class="sxs-lookup"><span data-stu-id="e9333-141">Bing Visual Search API reference</span></span>](https://aka.ms/bingvisualsearchreferencedoc)
