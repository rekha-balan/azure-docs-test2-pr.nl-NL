---
title: Text Analytics C# tutorial | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: Connect to Text Analytics from an ASP.NET Core web application.
services: cognitive-services
author: ghogen
manager: douge
ms.service: cognitive-services
ms.component: text-analytics
ms.topic: conceptual
ms.date: 06/01/2018
ms.author: ghogen
ms.openlocfilehash: eb9730f785b01a620e36a265216488c401eac63a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857577"
---
# <a name="connect-to-the-text-analytics-service-by-using-connected-services-in-visual-studio"></a><span data-ttu-id="0ca16-103">Connect to the Text Analytics Service by using Connected Services in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0ca16-103">Connect to the Text Analytics Service by using Connected Services in Visual Studio</span></span>

<span data-ttu-id="0ca16-104">By using the Text Analytics Service, you can extract rich information to categorize and process visual data, and perform machine-assisted moderation of images to help curate your services.</span><span class="sxs-lookup"><span data-stu-id="0ca16-104">By using the Text Analytics Service, you can extract rich information to categorize and process visual data, and perform machine-assisted moderation of images to help curate your services.</span></span>

<span data-ttu-id="0ca16-105">This article and its companion articles provide details for using the Visual Studio Connected Service feature for the Text Analytics Service.</span><span class="sxs-lookup"><span data-stu-id="0ca16-105">This article and its companion articles provide details for using the Visual Studio Connected Service feature for the Text Analytics Service.</span></span> <span data-ttu-id="0ca16-106">The capability is available in both Visual Studio 2017 15.7 or later, with the Cognitive Services extension installed.</span><span class="sxs-lookup"><span data-stu-id="0ca16-106">The capability is available in both Visual Studio 2017 15.7 or later, with the Cognitive Services extension installed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ca16-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0ca16-107">Prerequisites</span></span>

- <span data-ttu-id="0ca16-108">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0ca16-108">An Azure subscription.</span></span> <span data-ttu-id="0ca16-109">If you do not have one, you can sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0ca16-109">If you do not have one, you can sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="0ca16-110">Visual Studio 2017 version 15.7, with the Web Development workload installed.</span><span class="sxs-lookup"><span data-stu-id="0ca16-110">Visual Studio 2017 version 15.7, with the Web Development workload installed.</span></span> <span data-ttu-id="0ca16-111">[Download it now](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).</span><span class="sxs-lookup"><span data-stu-id="0ca16-111">[Download it now](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).</span></span>

[!INCLUDE [vs-install-cognitive-services-vsix](../../../includes/vs-install-cognitive-services-vsix.md)]

## <a name="add-support-to-your-project-for-the-text-analytics-service"></a><span data-ttu-id="0ca16-112">Add support to your project for the Text Analytics Service</span><span class="sxs-lookup"><span data-stu-id="0ca16-112">Add support to your project for the Text Analytics Service</span></span>

1. <span data-ttu-id="0ca16-113">Create a new ASP.NET Core web project called TextAnalyticsDemo.</span><span class="sxs-lookup"><span data-stu-id="0ca16-113">Create a new ASP.NET Core web project called TextAnalyticsDemo.</span></span> <span data-ttu-id="0ca16-114">Use the Web Application (Model-View-Controller) project template with all the default settings.</span><span class="sxs-lookup"><span data-stu-id="0ca16-114">Use the Web Application (Model-View-Controller) project template with all the default settings.</span></span> <span data-ttu-id="0ca16-115">It’s important to name the project MyWebApplication, so the namespace matches when you copy code into the project.</span><span class="sxs-lookup"><span data-stu-id="0ca16-115">It’s important to name the project MyWebApplication, so the namespace matches when you copy code into the project.</span></span>  <span data-ttu-id="0ca16-116">The example in this articles uses MVC, but you can use the Text Analytics Connected Service with any ASP.NET project type.</span><span class="sxs-lookup"><span data-stu-id="0ca16-116">The example in this articles uses MVC, but you can use the Text Analytics Connected Service with any ASP.NET project type.</span></span>

1. <span data-ttu-id="0ca16-117">In **Solution Explorer**, double-click on the **Connected Service** item.</span><span class="sxs-lookup"><span data-stu-id="0ca16-117">In **Solution Explorer**, double-click on the **Connected Service** item.</span></span>
   <span data-ttu-id="0ca16-118">The Connected Service page appears, with services you can add to your project.</span><span class="sxs-lookup"><span data-stu-id="0ca16-118">The Connected Service page appears, with services you can add to your project.</span></span>

   ![Screenshot of Connected Service in Solution Explorer](../media/vs-common/Connected-Services-Solution-Explorer.PNG)

1. <span data-ttu-id="0ca16-120">In the menu of available services, choose **Evaluate Sentiment with Text Analytics**.</span><span class="sxs-lookup"><span data-stu-id="0ca16-120">In the menu of available services, choose **Evaluate Sentiment with Text Analytics**.</span></span>

   ![Screenshot of Connected Services screen](./media/vs-text-connected-service/Cog-Text-Connected-Service-0.PNG)

   <span data-ttu-id="0ca16-122">If you've signed into Visual Studio, and have an Azure subscription associated with your account, a page appears with a dropdown list with your subscriptions.</span><span class="sxs-lookup"><span data-stu-id="0ca16-122">If you've signed into Visual Studio, and have an Azure subscription associated with your account, a page appears with a dropdown list with your subscriptions.</span></span>

   ![Screenshot of Text Analytics Connected Service screen](media/vs-text-connected-service/Cog-Text-Connected-Service-1.PNG)

1. <span data-ttu-id="0ca16-124">Select the subscription you want to use, and then choose a name for the Text Analytics Service, or choose the **Edit** link to modify the automatically generated name, choose the resource group, and the Pricing Tier.</span><span class="sxs-lookup"><span data-stu-id="0ca16-124">Select the subscription you want to use, and then choose a name for the Text Analytics Service, or choose the **Edit** link to modify the automatically generated name, choose the resource group, and the Pricing Tier.</span></span>

   ![Screenshot of resource group and pricing tier fields](media/vs-text-connected-service/Cog-Text-Connected-Service-2.PNG)

   <span data-ttu-id="0ca16-126">Follow the link for details on the pricing tiers.</span><span class="sxs-lookup"><span data-stu-id="0ca16-126">Follow the link for details on the pricing tiers.</span></span>

1. <span data-ttu-id="0ca16-127">Choose **Add** to add support for the Connected Service.</span><span class="sxs-lookup"><span data-stu-id="0ca16-127">Choose **Add** to add support for the Connected Service.</span></span>
   <span data-ttu-id="0ca16-128">Visual Studio modifies your project to add the NuGet packages, configuration file entries, and other changes to support a connection to the Text Analytics Service.</span><span class="sxs-lookup"><span data-stu-id="0ca16-128">Visual Studio modifies your project to add the NuGet packages, configuration file entries, and other changes to support a connection to the Text Analytics Service.</span></span> <span data-ttu-id="0ca16-129">The **Output Window** shows the log of what is happening to your project.</span><span class="sxs-lookup"><span data-stu-id="0ca16-129">The **Output Window** shows the log of what is happening to your project.</span></span> <span data-ttu-id="0ca16-130">You should see something like the following:</span><span class="sxs-lookup"><span data-stu-id="0ca16-130">You should see something like the following:</span></span>

   ```output
    [6/1/2018 3:04:02.347 PM] Adding Text Analytics to the project.
    [6/1/2018 3:04:02.906 PM] Creating new Text Analytics...
    [6/1/2018 3:04:06.314 PM] Installing NuGet package 'Microsoft.Azure.CognitiveServices.Language' version 1.0.0-preview...
    [6/1/2018 3:04:56.759 PM] Retrieving keys...
    [6/1/2018 3:04:57.822 PM] Updating appsettings.json setting: 'ServiceKey' = '<service key>'
    [6/1/2018 3:04:57.827 PM] Updating appsettings.json setting: 'ServiceEndPoint' = 'https://westus.api.cognitive.microsoft.com/text/analytics/v2.0'
    [6/1/2018 3:04:57.832 PM] Updating appsettings.json setting: 'Name' = 'TextAnalyticsDemo'
    [6/1/2018 3:05:01.840 PM] Successfully added Text Analytics to the project.
    ```
 
## <a name="use-the-text-analytics-service-to-detect-the-language-for-a-text-sample"></a><span data-ttu-id="0ca16-131">Use the Text Analytics Service to detect the language for a text sample.</span><span class="sxs-lookup"><span data-stu-id="0ca16-131">Use the Text Analytics Service to detect the language for a text sample.</span></span>

1. <span data-ttu-id="0ca16-132">Add the following using statements in Startup.cs.</span><span class="sxs-lookup"><span data-stu-id="0ca16-132">Add the following using statements in Startup.cs.</span></span>
 
   ```csharp
   using System.IO;
   using System.Net.Http;
   using System.Net.Http.Headers;
   using System.Text;
   using Microsoft.Extensions.Configuration;
   ```
 
1. <span data-ttu-id="0ca16-133">Add a configuration field, and add a constructor that initializes the configuration field in the Startup class to enable Configuration in your program.</span><span class="sxs-lookup"><span data-stu-id="0ca16-133">Add a configuration field, and add a constructor that initializes the configuration field in the Startup class to enable Configuration in your program.</span></span>

   ```csharp
      private IConfiguration configuration;

      public Startup(IConfiguration configuration)
      {
          this.configuration = configuration;
      }
   ```

1. <span data-ttu-id="0ca16-134">Add a class file in the Controllers folder called DemoTextAnalyzeController and replace its contents with the following code:</span><span class="sxs-lookup"><span data-stu-id="0ca16-134">Add a class file in the Controllers folder called DemoTextAnalyzeController and replace its contents with the following code:</span></span>

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Net.Http;
    using System.Threading.Tasks;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.CognitiveServices.Language.TextAnalytics;
    using Microsoft.Azure.CognitiveServices.Language.TextAnalytics.Models;
    using Microsoft.Extensions.Configuration;
    using TextAnalyticsDemo.Models;
    
    namespace TextAnalyticsDemo.Controllers
    {
        public class DemoTextAnalyzeController : Controller
        {
            private IConfiguration configuration;
    
            public DemoTextAnalyzeController(IConfiguration configuration)
            {
                this.configuration = configuration;
            }
    
            public IActionResult TextAnalyzeResult(TextAnalyzeModel model)
            {
    
                if (!string.IsNullOrWhiteSpace(model.TextStr))
                {
                    ITextAnalyticsAPI client = this.GetTextAnalyzeClient(new MyHandler());
                    model.AnalyzeResult = client.DetectLanguage(
                        new BatchInput(
                            new List<Input>()
                            {
                                new Input("id",model.TextStr)
                            }));
                }
                return View(model);
            }
    
            [HttpPost("Analyze")]
            public IActionResult Analyze(TextAnalyzeModel model)
            {
                return RedirectToAction("TextAnalyzeResult", model);
            }
    
            // Using the ServiceKey from the configuration file,
            // get an instance of the Text Analytics client.
            private ITextAnalyticsAPI GetTextAnalyzeClient(DelegatingHandler handler)
            {
                string key = configuration.GetSection("CognitiveServices")["TextAnalytics:ServiceKey"];
    
                ITextAnalyticsAPI client = new TextAnalyticsAPI( handlers: handler);
                client.SubscriptionKey = key;
                client.AzureRegion = AzureRegions.Westus;
    
                return client;
            }
        }
    }
    ```
    
    <span data-ttu-id="0ca16-135">The code includes GetTextAnalyzeClient to get the client object which you can use to call the Text Analytics API, and a request handler that calls DetectLanguage on a given text.</span><span class="sxs-lookup"><span data-stu-id="0ca16-135">The code includes GetTextAnalyzeClient to get the client object which you can use to call the Text Analytics API, and a request handler that calls DetectLanguage on a given text.</span></span>

1. <span data-ttu-id="0ca16-136">Add the MyHandler helper class which is used by the preceding code.</span><span class="sxs-lookup"><span data-stu-id="0ca16-136">Add the MyHandler helper class which is used by the preceding code.</span></span>

    ```csharp
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

1. <span data-ttu-id="0ca16-137">In the Models folder, add a class for the model.</span><span class="sxs-lookup"><span data-stu-id="0ca16-137">In the Models folder, add a class for the model.</span></span>

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    using Microsoft.Azure.CognitiveServices.Language.TextAnalytics.Models;
    
    namespace Demo.Models
    {
        public class TextAnalyzeModel
        {
            public string TextStr { get; set; }
    
            public LanguageBatchResult AnalyzeResult { get; set; }
    
            public SentimentBatchResult AnalyzeResult2 { get; set; }
        }
    }
    ```

1. <span data-ttu-id="0ca16-138">Add a View to show the analyzed text, the language determined, and the score that represents the confidence level in the analysis.</span><span class="sxs-lookup"><span data-stu-id="0ca16-138">Add a View to show the analyzed text, the language determined, and the score that represents the confidence level in the analysis.</span></span> <span data-ttu-id="0ca16-139">To do this, right-click on the **Views** folder, choose **Add**, then **View**.</span><span class="sxs-lookup"><span data-stu-id="0ca16-139">To do this, right-click on the **Views** folder, choose **Add**, then **View**.</span></span> <span data-ttu-id="0ca16-140">In the dialog box that appears, provide a name _TextAnalyzeResult_, accept the defaults to add a new file called _TextAnalyzeResult.cshtml_ in the **Views** folder and copy the following contents into it:</span><span class="sxs-lookup"><span data-stu-id="0ca16-140">In the dialog box that appears, provide a name _TextAnalyzeResult_, accept the defaults to add a new file called _TextAnalyzeResult.cshtml_ in the **Views** folder and copy the following contents into it:</span></span>
    
    ```cshtml
    @using System
    @model Demo.Models.TextAnalyzeModel
    
    @{
        ViewData["Title"] = "TextAnalyzeResult";
    }
    
    <h2>Text Language</h2>
    
    <div class="row">
        <section>
            <form asp-controller="DemoTextAnalyze" asp-action="Analyze" method="POST"
                  class="form-horizontal" enctype="multipart/form-data">
                <table width="90%">
                    <tr>
                        <td>
                            <input type="text" name="TextStr" class="form-control" />
                        </td>
                        <td>
                            <button type="submit" class="btn btn-default">Analyze</button>
                        </td>
                    </tr>
                </table>
            </form>
        </section>
    </div>
    
    <h2>Result</h2>
    <div>
        <dl class="dl-horizontal">
            <dt>
                Text :
            </dt>
            <dd>
                @Html.DisplayFor(model => model.TextStr)
            </dd>
            <dt>
                Language Name :
            </dt>
            <dd>
                @Html.DisplayFor(model => model.AnalyzeResult.Documents[0].DetectedLanguages[0].Name)
            </dd>
            <dt>
                Score :
            </dt>
            <dd>
                @Html.DisplayFor(model => model.AnalyzeResult.Documents[0].DetectedLanguages[0].Score)
            </dd>
        </dl>
    </div>
    <div>
        <hr />
        <p>
            <a asp-controller="Home" asp-action="Index">Return to Index</a>
        </p>
    </div>
    
    ```
 
1. <span data-ttu-id="0ca16-141">Build and run the example locally.</span><span class="sxs-lookup"><span data-stu-id="0ca16-141">Build and run the example locally.</span></span> <span data-ttu-id="0ca16-142">Enter some text and see what language Text Analytics detects.</span><span class="sxs-lookup"><span data-stu-id="0ca16-142">Enter some text and see what language Text Analytics detects.</span></span>
   
## <a name="clean-up-resources"></a><span data-ttu-id="0ca16-143">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="0ca16-143">Clean up resources</span></span>

<span data-ttu-id="0ca16-144">When no longer needed, delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="0ca16-144">When no longer needed, delete the resource group.</span></span> <span data-ttu-id="0ca16-145">This deletes the cognitive service and related resources.</span><span class="sxs-lookup"><span data-stu-id="0ca16-145">This deletes the cognitive service and related resources.</span></span> <span data-ttu-id="0ca16-146">To delete the resource group through the portal:</span><span class="sxs-lookup"><span data-stu-id="0ca16-146">To delete the resource group through the portal:</span></span>

1. <span data-ttu-id="0ca16-147">Enter the name of your resource group in the Search box at the top of the portal.</span><span class="sxs-lookup"><span data-stu-id="0ca16-147">Enter the name of your resource group in the Search box at the top of the portal.</span></span> <span data-ttu-id="0ca16-148">When you see the resource group used in this tutorial in the search results, select it.</span><span class="sxs-lookup"><span data-stu-id="0ca16-148">When you see the resource group used in this tutorial in the search results, select it.</span></span>
2. <span data-ttu-id="0ca16-149">Select **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="0ca16-149">Select **Delete resource group**.</span></span>
3. <span data-ttu-id="0ca16-150">In the **TYPE THE RESOURCE GROUP NAME:** box type in the name of the resource group and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="0ca16-150">In the **TYPE THE RESOURCE GROUP NAME:** box type in the name of the resource group and select **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ca16-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="0ca16-151">Next steps</span></span>

<span data-ttu-id="0ca16-152">Learn more about the Text Analytics Service by reading the [Text Analytics Service Documentation](index.yml).</span><span class="sxs-lookup"><span data-stu-id="0ca16-152">Learn more about the Text Analytics Service by reading the [Text Analytics Service Documentation](index.yml).</span></span>
