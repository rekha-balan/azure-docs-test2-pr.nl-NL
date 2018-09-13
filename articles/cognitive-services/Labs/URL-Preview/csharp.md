---
title: C# quickstart for Project URL Preview - Microsoft Cognitive Services | Microsoft Docs
description: Get started using Project URL Preview in Microsoft Cognitive Services on Azure.
services: cognitive-services
author: mikedodaro
ms.service: cognitive-services
ms.technology: project-url-preview
ms.topic: article
ms.date: 03/16/2018
ms.author: rosh, v-gedod
ms.openlocfilehash: 17d44bd0c23d0a1e67da5a0e91248700d3166c1a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867136"
---
# <a name="url-preview-query-in-c"></a><span data-ttu-id="38f31-103">URL Preview query in C#</span><span class="sxs-lookup"><span data-stu-id="38f31-103">URL Preview query in C#</span></span>

<span data-ttu-id="38f31-104">The following C# example creates a Url Preview for the SwiftKey Web site: https://swiftkey.com/en.</span><span class="sxs-lookup"><span data-stu-id="38f31-104">The following C# example creates a Url Preview for the SwiftKey Web site: https://swiftkey.com/en.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38f31-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="38f31-105">Prerequisites</span></span>

<span data-ttu-id="38f31-106">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span><span class="sxs-lookup"><span data-stu-id="38f31-106">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span></span> <span data-ttu-id="38f31-107">(The free Community Edition will work.)</span><span class="sxs-lookup"><span data-stu-id="38f31-107">(The free Community Edition will work.)</span></span>

<span data-ttu-id="38f31-108">Get an access key for the free trial [Cognitive Services Labs](https://aka.ms/answersearchsubscription)</span><span class="sxs-lookup"><span data-stu-id="38f31-108">Get an access key for the free trial [Cognitive Services Labs](https://aka.ms/answersearchsubscription)</span></span>

## <a name="code-scenario"></a><span data-ttu-id="38f31-109">Code scenario</span><span class="sxs-lookup"><span data-stu-id="38f31-109">Code scenario</span></span>

<span data-ttu-id="38f31-110">The following C# code creates a URL Preview of the SwiftKey Web site: https://swiftkey.com/en.</span><span class="sxs-lookup"><span data-stu-id="38f31-110">The following C# code creates a URL Preview of the SwiftKey Web site: https://swiftkey.com/en.</span></span> 

<span data-ttu-id="38f31-111">It is implemented in the following steps:</span><span class="sxs-lookup"><span data-stu-id="38f31-111">It is implemented in the following steps:</span></span>
1. <span data-ttu-id="38f31-112">Declare variables to specify the endpoint and a query URL to preview.</span><span class="sxs-lookup"><span data-stu-id="38f31-112">Declare variables to specify the endpoint and a query URL to preview.</span></span>  
2. <span data-ttu-id="38f31-113">Create the request.</span><span class="sxs-lookup"><span data-stu-id="38f31-113">Create the request.</span></span>
3. <span data-ttu-id="38f31-114">Add the *Ocp-Apim-Subscription-Key* header.</span><span class="sxs-lookup"><span data-stu-id="38f31-114">Add the *Ocp-Apim-Subscription-Key* header.</span></span> 
4. <span data-ttu-id="38f31-115">Run the Web request asynchronously.</span><span class="sxs-lookup"><span data-stu-id="38f31-115">Run the Web request asynchronously.</span></span> 
5. <span data-ttu-id="38f31-116">Read the response.</span><span class="sxs-lookup"><span data-stu-id="38f31-116">Read the response.</span></span>
6. <span data-ttu-id="38f31-117">Print the headers and JSON results to the console.</span><span class="sxs-lookup"><span data-stu-id="38f31-117">Print the headers and JSON results to the console.</span></span>

<span data-ttu-id="38f31-118">**Source code**</span><span class="sxs-lookup"><span data-stu-id="38f31-118">**Source code**</span></span>

```
using System;
using System.IO;
using System.Net;
using System.Text;

namespace UrlPrevCshp
{
    class Program
    {
        static void Main(string[] args)
        {
            String uriBase = "https://api.labs.cognitive.microsoft.com/urlpreview/v7.0/search";
            String searchQuery = "https://swiftkey.com/en"; 
            var uriQuery = uriBase + "?q=" + Uri.EscapeDataString(searchQuery);

            // Do the Web request and get response
            WebRequest request = HttpWebRequest.Create(uriQuery);
            request.Headers["Ocp-Apim-Subscription-Key"] = "YOUR-SUBSCRIPTION-KEY";
            HttpWebResponse response = (HttpWebResponse)request.GetResponseAsync().Result;
            string json = new StreamReader(response.GetResponseStream()).ReadToEnd();

            Console.WriteLine("\nHTTP Headers:\n");
            foreach (String header in response.Headers)
            {
                if (header.StartsWith("BingAPIs-") || header.StartsWith("X-MSEdge-"))
                    Console.WriteLine(header + ": " + response.Headers[header]);
            }

            Console.WriteLine(JsonPrettyPrint(json));
            

            Console.ReadKey();
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
## <a name="running-the-application"></a><span data-ttu-id="38f31-119">Running the application</span><span class="sxs-lookup"><span data-stu-id="38f31-119">Running the application</span></span>

<span data-ttu-id="38f31-120">To run the application:</span><span class="sxs-lookup"><span data-stu-id="38f31-120">To run the application:</span></span>

1. <span data-ttu-id="38f31-121">Create a new Console solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="38f31-121">Create a new Console solution in Visual Studio.</span></span>
2. <span data-ttu-id="38f31-122">Replace `Program.cs` with the provided code.</span><span class="sxs-lookup"><span data-stu-id="38f31-122">Replace `Program.cs` with the provided code.</span></span>
3. <span data-ttu-id="38f31-123">Replace the `YOUR-ACCESS-KEY` value with a valid access key for your subscription.</span><span class="sxs-lookup"><span data-stu-id="38f31-123">Replace the `YOUR-ACCESS-KEY` value with a valid access key for your subscription.</span></span>
4. <span data-ttu-id="38f31-124">Run the program.</span><span class="sxs-lookup"><span data-stu-id="38f31-124">Run the program.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38f31-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="38f31-125">Next steps</span></span>
- [<span data-ttu-id="38f31-126">Java quickstart</span><span class="sxs-lookup"><span data-stu-id="38f31-126">Java quickstart</span></span>](java-quickstart.md)
- [<span data-ttu-id="38f31-127">JavaScript quickstart</span><span class="sxs-lookup"><span data-stu-id="38f31-127">JavaScript quickstart</span></span>](javascript.md)
- [<span data-ttu-id="38f31-128">Node quickstart</span><span class="sxs-lookup"><span data-stu-id="38f31-128">Node quickstart</span></span>](node-quickstart.md)
- [<span data-ttu-id="38f31-129">Python quickstart</span><span class="sxs-lookup"><span data-stu-id="38f31-129">Python quickstart</span></span>](python-quickstart.md)