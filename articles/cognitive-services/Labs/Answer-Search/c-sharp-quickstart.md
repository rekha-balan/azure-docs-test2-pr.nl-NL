---
title: C# quickstart for Microsoft Cognitive Services, Project Answer Search | Microsoft Docs
description: Code sample to get started using the Project Answer Search, Microsoft Cognitive Services on Azure.
services: cognitive-services
author: mikedodaro
ms.service: cognitive-services
ms.technology: project-answer-search
ms.topic: article
ms.date: 04/13/2018
ms.author: rosh, v-gedod
ms.openlocfilehash: c8e2a6a7fc3609932a7a1139d7b34553e5f9c291
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857028"
---
# <a name="project-answer-search-query-in-c"></a><span data-ttu-id="e8f90-103">Project Answer Search query in C#</span><span class="sxs-lookup"><span data-stu-id="e8f90-103">Project Answer Search query in C#</span></span>

<span data-ttu-id="e8f90-104">The following C# example creates and sends a query for information about the third law of calculus.</span><span class="sxs-lookup"><span data-stu-id="e8f90-104">The following C# example creates and sends a query for information about the third law of calculus.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8f90-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e8f90-105">Prerequisites</span></span>

<span data-ttu-id="e8f90-106">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span><span class="sxs-lookup"><span data-stu-id="e8f90-106">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span></span> <span data-ttu-id="e8f90-107">(The free Community Edition will work.)</span><span class="sxs-lookup"><span data-stu-id="e8f90-107">(The free Community Edition will work.)</span></span>

<span data-ttu-id="e8f90-108">Get an access key for the free trial [Cognitive Services Labs](https://aka.ms/answersearchsubscription)</span><span class="sxs-lookup"><span data-stu-id="e8f90-108">Get an access key for the free trial [Cognitive Services Labs](https://aka.ms/answersearchsubscription)</span></span>

## <a name="code-scenario"></a><span data-ttu-id="e8f90-109">Code scenario</span><span class="sxs-lookup"><span data-stu-id="e8f90-109">Code scenario</span></span>

<span data-ttu-id="e8f90-110">The following C# code creates and sends the query.</span><span class="sxs-lookup"><span data-stu-id="e8f90-110">The following C# code creates and sends the query.</span></span> 

<span data-ttu-id="e8f90-111">It is implemented in the following steps:</span><span class="sxs-lookup"><span data-stu-id="e8f90-111">It is implemented in the following steps:</span></span>
1. <span data-ttu-id="e8f90-112">Declare variables to specify the endpoint and a query URL to preview.</span><span class="sxs-lookup"><span data-stu-id="e8f90-112">Declare variables to specify the endpoint and a query URL to preview.</span></span>  
2. <span data-ttu-id="e8f90-113">Create the request.</span><span class="sxs-lookup"><span data-stu-id="e8f90-113">Create the request.</span></span>
3. <span data-ttu-id="e8f90-114">Add the *Ocp-Apim-Subscription-Key* header.</span><span class="sxs-lookup"><span data-stu-id="e8f90-114">Add the *Ocp-Apim-Subscription-Key* header.</span></span> 
4. <span data-ttu-id="e8f90-115">Run the Web request asynchronously.</span><span class="sxs-lookup"><span data-stu-id="e8f90-115">Run the Web request asynchronously.</span></span> 
5. <span data-ttu-id="e8f90-116">Read the response.</span><span class="sxs-lookup"><span data-stu-id="e8f90-116">Read the response.</span></span>
6. <span data-ttu-id="e8f90-117">Print the headers and JSON results to the console.</span><span class="sxs-lookup"><span data-stu-id="e8f90-117">Print the headers and JSON results to the console.</span></span>

<span data-ttu-id="e8f90-118">**Source code**</span><span class="sxs-lookup"><span data-stu-id="e8f90-118">**Source code**</span></span>

```
using System;
using System.Collections.Generic;
using System.Text;
using System.Net;
using System.IO;

namespace Answers_csharp
{
    class Program
    {
        // Replace the accessKey string value with your valid access key.
        const string accessKey = "YOUR-SUBSCRIPTION-KEY";

        const string uriBase = "https://api.labs.cognitive.microsoft.com/answerSearch/v7.0/search"; 

        const string searchTerm = "third law of calculus"; 

        // Used to return news search results including relevant headers
        struct SearchResult
        {
            public String jsonResult;
            public Dictionary<String, String> relevantHeaders;
        }

        static void Main()
        {
            Console.OutputEncoding = System.Text.Encoding.UTF8;
            Console.WriteLine("Searching locally for: " + searchTerm);

            SearchResult result = BingLocalSearch(searchTerm);

            Console.WriteLine("\nRelevant HTTP Headers:\n");
            foreach (var header in result.relevantHeaders)
                Console.WriteLine(header.Key + ": " + header.Value);

            Console.WriteLine("\nJSON Response:\n");
            Console.WriteLine(JsonPrettyPrint(result.jsonResult));

            Console.Write("\nPress Enter to exit ");
            Console.ReadLine();
        }

        /// <summary>
        /// Does Bing knowledge search and returns the results as a SearchResult.
        /// </summary>
        static SearchResult BingLocalSearch(string searchQuery)
        {
            // Construct the URI of the search request
            var uriQuery = uriBase + "?q=" + Uri.EscapeDataString(searchQuery) + "&mkt=en-us";

            // Send the Web request and get the response.
            WebRequest request = HttpWebRequest.Create(uriQuery);
            request.Headers["Ocp-Apim-Subscription-Key"] = accessKey; 

            HttpWebResponse response = (HttpWebResponse)request.GetResponseAsync().Result;
            string json = new StreamReader(response.GetResponseStream()).ReadToEnd();

            // Create result object for return
            var searchResult = new SearchResult();
            searchResult.jsonResult = json;
            searchResult.relevantHeaders = new Dictionary<String, String>();

            // Extract Bing HTTP headers
            foreach (String header in response.Headers)
            {
                if (header.StartsWith("BingAPIs-") || header.StartsWith("X-MSEdge-"))
                    searchResult.relevantHeaders[header] = response.Headers[header];
            }

            return searchResult;
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
            int offset = 0;
            int indentLength = 3;

            foreach (char ch in json)
            {
                switch (ch)
                {
                    case '"':
                        if (!ignore) quote = !quote;
                        break;
                    case '\'':
                        if (quote) ignore = !ignore;
                        break;
                }

                if (quote)
                    sb.Append(ch);
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
                            if (ch != ' ') sb.Append(ch);
                            break;
                    }
                }
            }

            return sb.ToString().Trim();
        }

    }
}

```
## <a name="running-the-application"></a><span data-ttu-id="e8f90-119">Running the application</span><span class="sxs-lookup"><span data-stu-id="e8f90-119">Running the application</span></span>

<span data-ttu-id="e8f90-120">To run the application:</span><span class="sxs-lookup"><span data-stu-id="e8f90-120">To run the application:</span></span>

1. <span data-ttu-id="e8f90-121">Create a new Console solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e8f90-121">Create a new Console solution in Visual Studio.</span></span>
2. <span data-ttu-id="e8f90-122">Replace `Program.cs` with the provided code.</span><span class="sxs-lookup"><span data-stu-id="e8f90-122">Replace `Program.cs` with the provided code.</span></span>
3. <span data-ttu-id="e8f90-123">Replace the `YOUR-ACCESS-KEY` value with a valid access key for your subscription.</span><span class="sxs-lookup"><span data-stu-id="e8f90-123">Replace the `YOUR-ACCESS-KEY` value with a valid access key for your subscription.</span></span>
4. <span data-ttu-id="e8f90-124">Run the program.</span><span class="sxs-lookup"><span data-stu-id="e8f90-124">Run the program.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8f90-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="e8f90-125">Next steps</span></span>
[<span data-ttu-id="e8f90-126">Java quickstart</span><span class="sxs-lookup"><span data-stu-id="e8f90-126">Java quickstart</span></span>](java-quickstart.md)
