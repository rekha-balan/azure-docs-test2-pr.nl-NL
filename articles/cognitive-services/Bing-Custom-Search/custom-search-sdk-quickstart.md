---
title: Custom Search SDK C# quickstart | Microsoft Docs
titleSuffix: Cognitive Services
description: Setup Custom Search SDK C# console application.
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-custom-search
ms.topic: article
ms.date: 01/31/2018
ms.author: rosh
ms.openlocfilehash: 59b208b53bec974433c50c0e2304dc96bd9bd09e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871598"
---
# <a name="custom-search-sdk-c-quickstart"></a><span data-ttu-id="dbe1c-103">Custom Search SDK C# quickstart</span><span class="sxs-lookup"><span data-stu-id="dbe1c-103">Custom Search SDK C# quickstart</span></span>

<span data-ttu-id="dbe1c-104">The Bing Custom Search SDK contains the functionality of the REST API for entity search and parsing the results.</span><span class="sxs-lookup"><span data-stu-id="dbe1c-104">The Bing Custom Search SDK contains the functionality of the REST API for entity search and parsing the results.</span></span>

## <a name="application-dependencies"></a><span data-ttu-id="dbe1c-105">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="dbe1c-105">Application dependencies</span></span>

<span data-ttu-id="dbe1c-106">To set up a console application using the Bing Custom Search SDK, browse to the `Manage NuGet Packages` option from the Solution Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dbe1c-106">To set up a console application using the Bing Custom Search SDK, browse to the `Manage NuGet Packages` option from the Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="dbe1c-107">Add the `Microsoft.Azure.CognitiveServices.Search.CustomSearch` package.</span><span class="sxs-lookup"><span data-stu-id="dbe1c-107">Add the `Microsoft.Azure.CognitiveServices.Search.CustomSearch` package.</span></span>

<span data-ttu-id="dbe1c-108">Installing the [NuGet Custom Search](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.CustomSearch/1.2.0) package also installs dependencies, including the following assemblies:</span><span class="sxs-lookup"><span data-stu-id="dbe1c-108">Installing the [NuGet Custom Search](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.CustomSearch/1.2.0) package also installs dependencies, including the following assemblies:</span></span>
* <span data-ttu-id="dbe1c-109">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="dbe1c-109">Microsoft.Rest.ClientRuntime</span></span>
* <span data-ttu-id="dbe1c-110">Microsoft.Rest.ClientRuntime.Azure</span><span class="sxs-lookup"><span data-stu-id="dbe1c-110">Microsoft.Rest.ClientRuntime.Azure</span></span>
* <span data-ttu-id="dbe1c-111">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="dbe1c-111">Newtonsoft.Json</span></span>

## <a name="entity-search-client"></a><span data-ttu-id="dbe1c-112">Entity Search client</span><span class="sxs-lookup"><span data-stu-id="dbe1c-112">Entity Search client</span></span>

<span data-ttu-id="dbe1c-113">To create an instance of the CustomSearchAPI client, add using directives:</span><span class="sxs-lookup"><span data-stu-id="dbe1c-113">To create an instance of the CustomSearchAPI client, add using directives:</span></span>
```
using Microsoft.Azure.CognitiveServices.Search.CustomSearch;

```

<span data-ttu-id="dbe1c-114">Instantiate the custom search client: Replace `YOUR-CUSTOM-SEARCH-KEY` and `YOUR-CUSTOM-CONFIG-ID` with your access key and the API endpoint configuration ID assigned at [My Instances](https://www.customsearch.ai/).</span><span class="sxs-lookup"><span data-stu-id="dbe1c-114">Instantiate the custom search client: Replace `YOUR-CUSTOM-SEARCH-KEY` and `YOUR-CUSTOM-CONFIG-ID` with your access key and the API endpoint configuration ID assigned at [My Instances](https://www.customsearch.ai/).</span></span>
```
var client = new CustomSearchAPI(new ApiKeyServiceClientCredentials("YOUR-CUSTOM-SEARCH-KEY"));

```
<span data-ttu-id="dbe1c-115">Use the client to search with a query text:</span><span class="sxs-lookup"><span data-stu-id="dbe1c-115">Use the client to search with a query text:</span></span>
```
var webData = client.CustomInstance.SearchAsync(query: "Xbox", customConfig: Int32.Parse("YOUR-CUSTOM-CONFIG-ID")).Result;

```
## <a name="parse-the-results"></a><span data-ttu-id="dbe1c-116">Parse the results</span><span class="sxs-lookup"><span data-stu-id="dbe1c-116">Parse the results</span></span>

<span data-ttu-id="dbe1c-117">The `SearchAsync` method returns a `WebData` object that contains `WebPages` if any are found for the query.</span><span class="sxs-lookup"><span data-stu-id="dbe1c-117">The `SearchAsync` method returns a `WebData` object that contains `WebPages` if any are found for the query.</span></span> <span data-ttu-id="dbe1c-118">This code finds the first result and gets its `Name` and `URL`.</span><span class="sxs-lookup"><span data-stu-id="dbe1c-118">This code finds the first result and gets its `Name` and `URL`.</span></span>
```
var webData = client.CustomInstance.SearchAsync(query: "Xbox", customConfig: Int32.Parse("YOUR-CUSTOM-CONFIG-ID")).Result;
 
Console.WriteLine("Searched for Query# \" Xbox \"");

 //WebPages
if (webData?.WebPages?.Value?.Count > 0)
{
    // find the first web page
    var firstWebPagesResult = webData.WebPages.Value.FirstOrDefault();

    if (firstWebPagesResult != null)
    {
        Console.WriteLine("Webpage Results#{0}", webData.WebPages.Value.Count);
        Console.WriteLine("First web page name: {0} ", firstWebPagesResult.Name);
        Console.WriteLine("First web page URL: {0} ", firstWebPagesResult.Url);
    }
    else
    {
        Console.WriteLine("Couldn't find web results!");
    }
}
else
{
    Console.WriteLine("Didn't see any Web data..");
}

```
## <a name="complete-console-application"></a><span data-ttu-id="dbe1c-119">Complete console application</span><span class="sxs-lookup"><span data-stu-id="dbe1c-119">Complete console application</span></span>

<span data-ttu-id="dbe1c-120">The following code searches on query "Xbox" and prints out `Name` and `URL` for first web result.</span><span class="sxs-lookup"><span data-stu-id="dbe1c-120">The following code searches on query "Xbox" and prints out `Name` and `URL` for first web result.</span></span>
```
using System;
using System.Linq;
using Microsoft.Azure.CognitiveServices.Search.CustomSearch;

namespace CustomSrchSDK
{
    class Program
    {
        static void Main(string[] args)
        {

            var client = new CustomSearchAPI(new ApiKeyServiceClientCredentials("YOUR-CUSTOM-SEARCH-KEY"));

            try
            {
                // This will look up a single query (Xbox).
                var webData = client.CustomInstance.SearchAsync(query: "Xbox", customConfig: Int32.Parse("YOUR-CUSTOM-CONFIG-ID")).Result;
                Console.WriteLine("Searched for Query# \" Xbox \"");

                //WebPages
                if (webData?.WebPages?.Value?.Count > 0)
                {
                    // find the first web page
                    var firstWebPagesResult = webData.WebPages.Value.FirstOrDefault();

                    if (firstWebPagesResult != null)
                    {
                        Console.WriteLine("Webpage Results#{0}", webData.WebPages.Value.Count);
                        Console.WriteLine("First web page name: {0} ", firstWebPagesResult.Name);
                        Console.WriteLine("First web page URL: {0} ", firstWebPagesResult.Url);
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find web results!");
                    }
                }
                else
                {
                    Console.WriteLine("Didn't see any Web data..");
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine("Encountered exception. " + ex.Message);
            }

            Console.WriteLine("Any key to exit...");
            Console.ReadKey();
        }

    }
}


```

## <a name="next-steps"></a><span data-ttu-id="dbe1c-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="dbe1c-121">Next steps</span></span>

[<span data-ttu-id="dbe1c-122">Cognitive services .NET SDK samples</span><span class="sxs-lookup"><span data-stu-id="dbe1c-122">Cognitive services .NET SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7)
