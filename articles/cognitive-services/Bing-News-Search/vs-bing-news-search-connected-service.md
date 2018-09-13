---
title: Bing News Search C# tutorial | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: Connect to Cognitive Services Bing News Search from an ASP.NET Core web application.
services: cognitive-services
author: ghogen
manager: douge
ms.service: cognitive-services
ms.component: bing-news-search
ms.topic: conceptual
ms.date: 03/01/2018
ms.author: ghogen
ms.openlocfilehash: 5cfa82067d28b05f32bd87e0e83d55a03da8d508
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870708"
---
# <a name="connect-to-bing-news-search-api-by-using-connected-services-in-visual-studio"></a><span data-ttu-id="c313e-103">Connect to Bing News Search API by using Connected Services in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c313e-103">Connect to Bing News Search API by using Connected Services in Visual Studio</span></span>

<span data-ttu-id="c313e-104">By using Bing News Search, you can enable apps and services to harness the power of an ad-free search engine scoped to the web.</span><span class="sxs-lookup"><span data-stu-id="c313e-104">By using Bing News Search, you can enable apps and services to harness the power of an ad-free search engine scoped to the web.</span></span> <span data-ttu-id="c313e-105">Bing News Search is one of the search services available with Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="c313e-105">Bing News Search is one of the search services available with Cognitive Services.</span></span>

<span data-ttu-id="c313e-106">This article provides details for using the Visual Studio Connected Service feature for Bing News Search.</span><span class="sxs-lookup"><span data-stu-id="c313e-106">This article provides details for using the Visual Studio Connected Service feature for Bing News Search.</span></span> <span data-ttu-id="c313e-107">The capability is available in Visual Studio 2017 15.7 or later, with the Cognitive Services extension installed.</span><span class="sxs-lookup"><span data-stu-id="c313e-107">The capability is available in Visual Studio 2017 15.7 or later, with the Cognitive Services extension installed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c313e-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c313e-108">Prerequisites</span></span>

- <span data-ttu-id="c313e-109">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c313e-109">An Azure subscription.</span></span> <span data-ttu-id="c313e-110">If you do not have one, you can sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c313e-110">If you do not have one, you can sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="c313e-111">Visual Studio 2017 version 15.7, with the Web Development workload installed.</span><span class="sxs-lookup"><span data-stu-id="c313e-111">Visual Studio 2017 version 15.7, with the Web Development workload installed.</span></span> <span data-ttu-id="c313e-112">[Download it now](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).</span><span class="sxs-lookup"><span data-stu-id="c313e-112">[Download it now](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).</span></span>

[!INCLUDE [vs-install-cognitive-services-vsix](../../../includes/vs-install-cognitive-services-vsix.md)]

## <a name="add-support-to-your-project-for-bing-news-search-api"></a><span data-ttu-id="c313e-113">Add support to your project for Bing News Search API</span><span class="sxs-lookup"><span data-stu-id="c313e-113">Add support to your project for Bing News Search API</span></span>

1. <span data-ttu-id="c313e-114">Create a new ASP.NET Core web project named MyWebApplication.</span><span class="sxs-lookup"><span data-stu-id="c313e-114">Create a new ASP.NET Core web project named MyWebApplication.</span></span> <span data-ttu-id="c313e-115">Use the **Web Application (Model-View-Controller)** project template, with all the default settings.</span><span class="sxs-lookup"><span data-stu-id="c313e-115">Use the **Web Application (Model-View-Controller)** project template, with all the default settings.</span></span> <span data-ttu-id="c313e-116">It’s important to name the project MyWebApplication, so the namespace matches when you copy code into the project.</span><span class="sxs-lookup"><span data-stu-id="c313e-116">It’s important to name the project MyWebApplication, so the namespace matches when you copy code into the project.</span></span> 

1. <span data-ttu-id="c313e-117">In **Solution Explorer**, choose **Add** > **Connected Service**.</span><span class="sxs-lookup"><span data-stu-id="c313e-117">In **Solution Explorer**, choose **Add** > **Connected Service**.</span></span>
   <span data-ttu-id="c313e-118">The Connected Service page appears, with services you can add to your project.</span><span class="sxs-lookup"><span data-stu-id="c313e-118">The Connected Service page appears, with services you can add to your project.</span></span>

   ![Screenshot of Add Connected Service menu item](../media/vs-common/Connected-Service-Menu.PNG)

1. <span data-ttu-id="c313e-120">In the menu of available services, choose **Bring Intelligent Search To Your Apps**.</span><span class="sxs-lookup"><span data-stu-id="c313e-120">In the menu of available services, choose **Bring Intelligent Search To Your Apps**.</span></span>

   ![Screenshot of list of connected services](./media/vs-bing-news-search-connected-service/Cog-Search-Connected-Service-0.PNG)

   <span data-ttu-id="c313e-122">If you've signed into Visual Studio, and have an Azure subscription associated with your account, a page appears with a dropdown list with your subscriptions.</span><span class="sxs-lookup"><span data-stu-id="c313e-122">If you've signed into Visual Studio, and have an Azure subscription associated with your account, a page appears with a dropdown list with your subscriptions.</span></span> <span data-ttu-id="c313e-123">Select the subscription you want to use, and then choose a name for the Bing News Search API.</span><span class="sxs-lookup"><span data-stu-id="c313e-123">Select the subscription you want to use, and then choose a name for the Bing News Search API.</span></span> <span data-ttu-id="c313e-124">You can also choose **Edit** to modify the automatically generated name.</span><span class="sxs-lookup"><span data-stu-id="c313e-124">You can also choose **Edit** to modify the automatically generated name.</span></span>

   ![Screenshot of subscription and name fields](media/vs-bing-news-search-connected-service/Cog-Search-Connected-Service-1.PNG)

1. <span data-ttu-id="c313e-126">Choose the resource group, and the pricing tier.</span><span class="sxs-lookup"><span data-stu-id="c313e-126">Choose the resource group, and the pricing tier.</span></span>

   ![Screenshot of resource group and pricing tier fields](media/vs-bing-news-search-connected-service/Cog-Search-Connected-Service-2.PNG)

   <span data-ttu-id="c313e-128">If you want more details about the pricing tiers, select **Review pricing**.</span><span class="sxs-lookup"><span data-stu-id="c313e-128">If you want more details about the pricing tiers, select **Review pricing**.</span></span>

1. <span data-ttu-id="c313e-129">Choose **Add** to add support for the Connected Service.</span><span class="sxs-lookup"><span data-stu-id="c313e-129">Choose **Add** to add support for the Connected Service.</span></span>
   <span data-ttu-id="c313e-130">Visual Studio modifies your project to add the NuGet packages, configuration file entries, and other changes to support a connection to the Bing News Search API.</span><span class="sxs-lookup"><span data-stu-id="c313e-130">Visual Studio modifies your project to add the NuGet packages, configuration file entries, and other changes to support a connection to the Bing News Search API.</span></span> <span data-ttu-id="c313e-131">The output shows the log of what is happening to your project.</span><span class="sxs-lookup"><span data-stu-id="c313e-131">The output shows the log of what is happening to your project.</span></span> <span data-ttu-id="c313e-132">You should see something like the following:</span><span class="sxs-lookup"><span data-stu-id="c313e-132">You should see something like the following:</span></span>

   ```output
   [5/4/2018 12:41:21.084 PM] Adding Intelligent Search to the project.
   [5/4/2018 12:41:21.271 PM] Creating new Intelligent Search...
   [5/4/2018 12:41:24.128 PM] Installing NuGet package 'Microsoft.Azure.CognitiveServices.Search.ImageSearch' version 1.2.0...
   [5/4/2018 12:41:24.135 PM] Installing NuGet package 'Microsoft.Azure.CognitiveServices.Search.NewsSearch' version 1.2.0...
   [5/4/2018 12:41:24.154 PM] Installing NuGet package 'Microsoft.Azure.CognitiveServices.Search.WebSearch' version 1.2.0...
   [5/4/2018 12:41:24.168 PM] Installing NuGet package 'Microsoft.Azure.CognitiveServices.Search.CustomSearch' version 1.2.0...
   [5/4/2018 12:41:24.187 PM] Installing NuGet package 'Microsoft.Azure.CognitiveServices.Search.VideoSearch' version 1.2.0...
   [5/4/2018 12:42:07.287 PM] Retrieving keys...
   [5/4/2018 12:42:07.741 PM] Updating appsettings.json setting: 'ServiceKey' = 'c271412f3e4c4e1dacc7c4145fa0572a'
   [5/4/2018 12:42:07.745 PM] Updating appsettings.json setting: 'ServiceEndPoint' = 'https://api.cognitive.microsoft.com/bing/v7.0'
   [5/4/2018 12:42:07.749 PM] Updating appsettings.json setting: 'Name' = 'WebApplicationCore-Search_IntelligentSearch'
   [5/4/2018 12:42:10.217 PM] Successfully added Intelligent Search to the project.
   ```

   <span data-ttu-id="c313e-133">The appsettings.json file now contains the following new settings:</span><span class="sxs-lookup"><span data-stu-id="c313e-133">The appsettings.json file now contains the following new settings:</span></span>

   ```json
   "CognitiveServices": {
     "IntelligentSearch": {
       "ServiceKey": "<your service key>",
       "ServiceEndPoint": "https://api.cognitive.microsoft.com/bing/v7.0",
       "Name": "WebApplicationCore-Search_IntelligentSearch"
     }
   }
   ```
 
## <a name="use-the-bing-news-search-api-to-add-search-functionality-to-a-web-page"></a><span data-ttu-id="c313e-134">Use the Bing News Search API to add search functionality to a web page</span><span class="sxs-lookup"><span data-stu-id="c313e-134">Use the Bing News Search API to add search functionality to a web page</span></span>

<span data-ttu-id="c313e-135">Now that you’ve added support for the Bing News Search API to your project, here’s how to use the API to add intelligent search to a web page.</span><span class="sxs-lookup"><span data-stu-id="c313e-135">Now that you’ve added support for the Bing News Search API to your project, here’s how to use the API to add intelligent search to a web page.</span></span>

1.  <span data-ttu-id="c313e-136">In *Startup.cs*, in the `ConfigureServices` method, add a call to `IServiceCollection.AddSingleton`.</span><span class="sxs-lookup"><span data-stu-id="c313e-136">In *Startup.cs*, in the `ConfigureServices` method, add a call to `IServiceCollection.AddSingleton`.</span></span> <span data-ttu-id="c313e-137">This makes the configuration object that contains the key settings available to the code in your project.</span><span class="sxs-lookup"><span data-stu-id="c313e-137">This makes the configuration object that contains the key settings available to the code in your project.</span></span>
 
   ```csharp
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddMvc();
            services.AddSingleton<IConfiguration>(Configuration);
        }
   ```


1. <span data-ttu-id="c313e-138">Add a new class file under the **Models** folder, called *BingNewsModel.cs*.</span><span class="sxs-lookup"><span data-stu-id="c313e-138">Add a new class file under the **Models** folder, called *BingNewsModel.cs*.</span></span> <span data-ttu-id="c313e-139">If you named your project differently, use your own project's namespace, instead of MyWebApplication.</span><span class="sxs-lookup"><span data-stu-id="c313e-139">If you named your project differently, use your own project's namespace, instead of MyWebApplication.</span></span> <span data-ttu-id="c313e-140">Replace the contents with the following code:</span><span class="sxs-lookup"><span data-stu-id="c313e-140">Replace the contents with the following code:</span></span>
 
    ```csharp
    using Microsoft.Azure.CognitiveServices.Search.NewsSearch.Models;
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    
    namespace MyWebApplication.Models
    {
        public class BingNewsModel
        {
            public News SearchResult { get; set; } 
            public string SearchText { get; set; }
        }
    }
    ```

   <span data-ttu-id="c313e-141">This model is used to store the results of a call to the Bing News Search service.</span><span class="sxs-lookup"><span data-stu-id="c313e-141">This model is used to store the results of a call to the Bing News Search service.</span></span>
 
1. <span data-ttu-id="c313e-142">In the **Controllers** folder, add a new class file called *IntelligentSearchController.cs*.</span><span class="sxs-lookup"><span data-stu-id="c313e-142">In the **Controllers** folder, add a new class file called *IntelligentSearchController.cs*.</span></span> <span data-ttu-id="c313e-143">Replace the contents with the following code:</span><span class="sxs-lookup"><span data-stu-id="c313e-143">Replace the contents with the following code:</span></span>

   ```csharp
    using System.Net.Http;
    using System.Threading.Tasks;
    using MyWebApplication.Models;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.CognitiveServices.Search.NewsSearch;
    using Microsoft.Extensions.Configuration;
    
    namespace MyWebApplication.Controllers
    {
        // A controller to handle News Search requests
        public class IntelligentSearchController : Controller
        {
            private IConfiguration configuration;
  
            // Set up the configuration that contains the keys
            // (from the appsettings.json file)
            // that you will use to access the service  
            public IntelligentSearchController(IConfiguration configuration)
            {
                this.configuration = configuration;
            }

            // Call the Bing News Search API and put the result in the model object.    
            public async Task<IActionResult> BingSearchResult(BingNewsModel model)
            {
                if (!string.IsNullOrWhiteSpace(model.SearchText))
                { 
                    INewsSearchAPI client = this.GetNewsSearchClient(new MyHandler());
                    model.SearchResult = await client.News.SearchAsync(model.SearchText);
                }
                return View(model);
            }
    
            // Forward requests to the Search endpoint to the BingSearchResult method
            [HttpPost("Search")]
            public IActionResult Search(BingNewsModel model)
            {
                return RedirectToAction("BingSearchResult", model);
            }

            // Get the search client object
            private INewsSearchAPI GetNewsSearchClient(DelegatingHandler handler)
            {
                string key =
                   configuration.GetSection("CognitiveServices")["IntelligentSearch:ServiceKey"];
    
                INewsSearchAPI client = new NewsSearchAPI(
                   new ApiKeyServiceClientCredentials(key), handlers: handler);
    
                return client;
            }
        }
    }
   ```

   <span data-ttu-id="c313e-144">In this code, the constructor sets up the configuration object that contains your keys.</span><span class="sxs-lookup"><span data-stu-id="c313e-144">In this code, the constructor sets up the configuration object that contains your keys.</span></span> <span data-ttu-id="c313e-145">The method for the `Search` route is just a redirection to the `BingSearchResult` function.</span><span class="sxs-lookup"><span data-stu-id="c313e-145">The method for the `Search` route is just a redirection to the `BingSearchResult` function.</span></span> <span data-ttu-id="c313e-146">This calls the `GetNewsSearchClient` method to get the `NewsSearchAPI` client object.</span><span class="sxs-lookup"><span data-stu-id="c313e-146">This calls the `GetNewsSearchClient` method to get the `NewsSearchAPI` client object.</span></span>  <span data-ttu-id="c313e-147">The `NewsSearchAPI` client object contains the `SearchAsync` method, which actually calls the service and returns the results in the `SearchResult` model that you just created.</span><span class="sxs-lookup"><span data-stu-id="c313e-147">The `NewsSearchAPI` client object contains the `SearchAsync` method, which actually calls the service and returns the results in the `SearchResult` model that you just created.</span></span> 

1. <span data-ttu-id="c313e-148">Add a class, `MyHandler`, which was referenced in the preceding code.</span><span class="sxs-lookup"><span data-stu-id="c313e-148">Add a class, `MyHandler`, which was referenced in the preceding code.</span></span> <span data-ttu-id="c313e-149">This delegates the asynchronous call to the search service to its base class, `DelegatingHandler`.</span><span class="sxs-lookup"><span data-stu-id="c313e-149">This delegates the asynchronous call to the search service to its base class, `DelegatingHandler`.</span></span>

   ```csharp
    using System.Net.Http;
    using System.Threading.Tasks;
    using System.Threading;

    class MyHandler : DelegatingHandler
    {
        protected async override Task<HttpResponseMessage> SendAsync(
        HttpRequestMessage request, CancellationToken cancellationToken)
        {
            // Call the inner handler.
            var response = await base.SendAsync(request, cancellationToken);
            
            return response;
        }
    }
   ```

1. <span data-ttu-id="c313e-150">To add support for submitting searches and viewing the results, in the **Views** folder, create a new folder called **IntelligentSearch**.</span><span class="sxs-lookup"><span data-stu-id="c313e-150">To add support for submitting searches and viewing the results, in the **Views** folder, create a new folder called **IntelligentSearch**.</span></span> <span data-ttu-id="c313e-151">In this new folder, add a view *BingSearchResult.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="c313e-151">In this new folder, add a view *BingSearchResult.cshtml*.</span></span> <span data-ttu-id="c313e-152">Copy in the following code:</span><span class="sxs-lookup"><span data-stu-id="c313e-152">Copy in the following code:</span></span>

    ```cshtml
    @using System
    @model MyWebApplication.Models.BingNewsModel
    
    @{
        ViewData["Title"] = "BingSearchResult";
    }
    
    <h2>Search News</h2>
    
    <div class="row">
        <section>
            <form asp-controller="IntelligentSearch" asp-action="Search" method="POST"
                  class="form-horizontal" enctype="multipart/form-data">
                <table width ="90%">
                    <tr>
                        <td>
                            <input type="text" name="SearchText" class="form-control" />
                        </td>
                        <td>
                            <button type="submit" class="btn btn-default">Search</button>
                        </td>
                    </tr>
                </table>
            </form>
        </section>
    </div>
    <h2>Search Result</h2=
    <table>
    @if (!string.IsNullOrEmpty(Model.SearchText)) {
        foreach (var item in Model.SearchResult.Value) {
        <tr>
            <td rowspan="2" width="90">
               <img src=@item?.Image?.Thumbnail?.ContentUrl width="80" height="80" />
            </td>
            <td><a href=@item.Url>@item.Name</a></td>
        </tr>   
        <tr>
            <td>@item.Description</td>
        </tr>
        <tr height="10">
            <td/><td/>
         </tr>
        } }
     </table>
    <div>
        <hr />
        <p>
            <a asp-controller="Home" asp-action="Index">Return to Index</a>
        </p>
    </div>
    ```

1. <span data-ttu-id="c313e-153">Start the web application locally, enter the URL for the page you just created (/IntelligentSearch/BingSearchResult), and post a search request by using the Search button.</span><span class="sxs-lookup"><span data-stu-id="c313e-153">Start the web application locally, enter the URL for the page you just created (/IntelligentSearch/BingSearchResult), and post a search request by using the Search button.</span></span>

   ![Screenshot of Bing News Search results](media/vs-bing-news-search-connected-service/Cog-News-Search-Results.PNG)
           
## <a name="clean-up-resources"></a><span data-ttu-id="c313e-155">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="c313e-155">Clean up resources</span></span>

<span data-ttu-id="c313e-156">When the resource group is no longer needed, you can delete it.</span><span class="sxs-lookup"><span data-stu-id="c313e-156">When the resource group is no longer needed, you can delete it.</span></span> <span data-ttu-id="c313e-157">This deletes the cognitive service and related resources.</span><span class="sxs-lookup"><span data-stu-id="c313e-157">This deletes the cognitive service and related resources.</span></span> <span data-ttu-id="c313e-158">To delete the resource group through the portal:</span><span class="sxs-lookup"><span data-stu-id="c313e-158">To delete the resource group through the portal:</span></span>

1. <span data-ttu-id="c313e-159">Enter the name of your resource group in the search box at the top of the portal.</span><span class="sxs-lookup"><span data-stu-id="c313e-159">Enter the name of your resource group in the search box at the top of the portal.</span></span> <span data-ttu-id="c313e-160">Select the resource group you want to delete.</span><span class="sxs-lookup"><span data-stu-id="c313e-160">Select the resource group you want to delete.</span></span>
2. <span data-ttu-id="c313e-161">Select **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="c313e-161">Select **Delete resource group**.</span></span>
3. <span data-ttu-id="c313e-162">In the **Type the Resource Group Name** box, enter the name of the resource group and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="c313e-162">In the **Type the Resource Group Name** box, enter the name of the resource group and select **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c313e-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="c313e-163">Next steps</span></span>

<span data-ttu-id="c313e-164">To learn more about the Bing News Search API, see [What is Bing News Search?](index.yml).</span><span class="sxs-lookup"><span data-stu-id="c313e-164">To learn more about the Bing News Search API, see [What is Bing News Search?](index.yml).</span></span>
