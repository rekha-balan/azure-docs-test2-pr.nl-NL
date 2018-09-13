---
title: Call endpoint by using C# - Bing Custom Search - Microsoft Cognitive Services
description: This quickstart shows how to request search results from your custom search instance by using C# to call the Bing Custom Search endpoint.
services: cognitive-services
author: brapel
manager: ehansen
ms.service: cognitive-services
ms.component: bing-custom-search
ms.topic: article
ms.date: 05/07/2018
ms.author: v-brapel
ms.openlocfilehash: 32644fe0cf0a6e1666d2d1ee6efb826bf753f001
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868325"
---
# <a name="call-bing-custom-search-endpoint-c"></a><span data-ttu-id="7c94a-103">Call Bing Custom Search endpoint (C#)</span><span class="sxs-lookup"><span data-stu-id="7c94a-103">Call Bing Custom Search endpoint (C#)</span></span>

<span data-ttu-id="7c94a-104">This quickstart shows how to request search results from your custom search instance by using C# to call the Bing Custom Search endpoint.</span><span class="sxs-lookup"><span data-stu-id="7c94a-104">This quickstart shows how to request search results from your custom search instance by using C# to call the Bing Custom Search endpoint.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7c94a-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7c94a-105">Prerequisites</span></span>

-  <span data-ttu-id="7c94a-106">A ready-to-use custom search instance.</span><span class="sxs-lookup"><span data-stu-id="7c94a-106">A ready-to-use custom search instance.</span></span> <span data-ttu-id="7c94a-107">See [Create your first Bing Custom Search instance](quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="7c94a-107">See [Create your first Bing Custom Search instance](quick-start.md).</span></span>
-  <span data-ttu-id="7c94a-108">[.Net Core](https://www.microsoft.com/net/download/core) installed.</span><span class="sxs-lookup"><span data-stu-id="7c94a-108">[.Net Core](https://www.microsoft.com/net/download/core) installed.</span></span>
- <span data-ttu-id="7c94a-109">A [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span><span class="sxs-lookup"><span data-stu-id="7c94a-109">A [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span></span> <span data-ttu-id="7c94a-110">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-custom-search) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="7c94a-110">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-custom-search) is sufficient for this quickstart.</span></span> <span data-ttu-id="7c94a-111">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="7c94a-111">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>  

  >[!NOTE]  
  ><span data-ttu-id="7c94a-112">Existing Bing Custom Search customers who have a preview key provisioned on or before October 15, 2017 will be able to use their keys until November 30, 2017, or until they have exhausted the maximum number of queries allowed.</span><span class="sxs-lookup"><span data-stu-id="7c94a-112">Existing Bing Custom Search customers who have a preview key provisioned on or before October 15, 2017 will be able to use their keys until November 30, 2017, or until they have exhausted the maximum number of queries allowed.</span></span> <span data-ttu-id="7c94a-113">Afterwards, they need to migrate to the generally available version on Azure.</span><span class="sxs-lookup"><span data-stu-id="7c94a-113">Afterwards, they need to migrate to the generally available version on Azure.</span></span> 
 
## <a name="run-the-code"></a><span data-ttu-id="7c94a-114">Run the code</span><span class="sxs-lookup"><span data-stu-id="7c94a-114">Run the code</span></span>

<span data-ttu-id="7c94a-115">To run this example, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="7c94a-115">To run this example, follow these steps:</span></span>

1. <span data-ttu-id="7c94a-116">Create a folder for your code.</span><span class="sxs-lookup"><span data-stu-id="7c94a-116">Create a folder for your code.</span></span>
2. <span data-ttu-id="7c94a-117">From a command prompt or terminal, navigate to the folder you just created.</span><span class="sxs-lookup"><span data-stu-id="7c94a-117">From a command prompt or terminal, navigate to the folder you just created.</span></span>
3. <span data-ttu-id="7c94a-118">Run the following commands:</span><span class="sxs-lookup"><span data-stu-id="7c94a-118">Run the following commands:</span></span>
    ```
    dotnet new console -o BingCustomSearch
    cd BingCustomSearch
    dotnet add package Newtonsoft.Json
    dotnet restore
   ```

4. <span data-ttu-id="7c94a-119">Copy the following code to Program.cs.</span><span class="sxs-lookup"><span data-stu-id="7c94a-119">Copy the following code to Program.cs.</span></span>
5. <span data-ttu-id="7c94a-120">Replace **YOUR-SUBSCRIPTION-KEY** and **YOUR-CUSTOM-CONFIG-ID** with your key and configuration ID.</span><span class="sxs-lookup"><span data-stu-id="7c94a-120">Replace **YOUR-SUBSCRIPTION-KEY** and **YOUR-CUSTOM-CONFIG-ID** with your key and configuration ID.</span></span>

    ``` CSharp
    using System;
    using System.Net.Http;
    using System.Web;
    using Newtonsoft.Json;
    
    namespace bing_custom_search_example_dotnet
    {
        class Program
        {
            static void Main(string[] args)
            {
                var subscriptionKey = "YOUR-SUBSCRIPTION-KEY";
                var customConfigId = "YOUR-CUSTOM-CONFIG-ID";
                var searchTerm = args.Length > 0 ? args[0]: "microsoft";            
    
                var url = "https://api.cognitive.microsoft.com/bingcustomsearch/v7.0/search?" +
                    "q=" + searchTerm +
                    "&customconfig=" + customConfigId;
    
                var client = new HttpClient();
                client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", subscriptionKey);
                var httpResponseMessage = client.GetAsync(url).Result;
                var responseContent = httpResponseMessage.Content.ReadAsStringAsync().Result;
                BingCustomSearchResponse response = JsonConvert.DeserializeObject<BingCustomSearchResponse>(responseContent);
                
                for(int i = 0; i < response.webPages.value.Length; i++)
                {                
                    var webPage = response.webPages.value[i];
                    
                    Console.WriteLine("name: " + webPage.name);
                    Console.WriteLine("url: " + webPage.url);                
                    Console.WriteLine("displayUrl: " + webPage.displayUrl);
                    Console.WriteLine("snippet: " + webPage.snippet);
                    Console.WriteLine("dateLastCrawled: " + webPage.dateLastCrawled);
                    Console.WriteLine();
                }            
            }
        }
    
        public class BingCustomSearchResponse
        {        
            public string _type{ get; set; }            
            public WebPages webPages { get; set; }
        }
    
        public class WebPages
        {
            public string webSearchUrl { get; set; }
            public int totalEstimatedMatches { get; set; }
            public WebPage[] value { get; set; }        
        }
    
        public class WebPage
        {
            public string name { get; set; }
            public string url { get; set; }
            public string displayUrl { get; set; }
            public string snippet { get; set; }
            public DateTime dateLastCrawled { get; set; }
            public string cachedPageUrl { get; set; }
            public OpenGraphImage openGraphImage { get; set; }        
        }
        
        public class OpenGraphImage
        {
            public string contentUrl { get; set; }
            public int width { get; set; }
            public int height { get; set; }
        }
    }
    ```
6. <span data-ttu-id="7c94a-121">Build the application using the following command.</span><span class="sxs-lookup"><span data-stu-id="7c94a-121">Build the application using the following command.</span></span> <span data-ttu-id="7c94a-122">Note the dll path referenced by the command output.</span><span class="sxs-lookup"><span data-stu-id="7c94a-122">Note the dll path referenced by the command output.</span></span>

    <pre>
    dotnet build 
    </pre>
    
7. <span data-ttu-id="7c94a-123">Run the application using the following command replacing **PATH TO OUTPUT** with the path referenced by the build step.</span><span class="sxs-lookup"><span data-stu-id="7c94a-123">Run the application using the following command replacing **PATH TO OUTPUT** with the path referenced by the build step.</span></span>

    <pre>    
    dotnet **PATH TO OUTPUT**
    </pre>

## <a name="next-steps"></a><span data-ttu-id="7c94a-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c94a-124">Next steps</span></span>
- [<span data-ttu-id="7c94a-125">Configure your hosted UI experience</span><span class="sxs-lookup"><span data-stu-id="7c94a-125">Configure your hosted UI experience</span></span>](./hosted-ui.md)
- [<span data-ttu-id="7c94a-126">Use decoration markers to highlight text</span><span class="sxs-lookup"><span data-stu-id="7c94a-126">Use decoration markers to highlight text</span></span>](./hit-highlighting.md)
- [<span data-ttu-id="7c94a-127">Page webpages</span><span class="sxs-lookup"><span data-stu-id="7c94a-127">Page webpages</span></span>](./page-webpages.md)
