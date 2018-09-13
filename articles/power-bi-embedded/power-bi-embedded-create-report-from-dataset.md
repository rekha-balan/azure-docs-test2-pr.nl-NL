---
title: Create a new report from a dataset in Azure Power BI Embedded | Microsoft Docs
description: Power BI Embedded reports can now be created from a dataset in your own application.
services: power-bi-embedded
documentationcenter: ''
author: guyinacube
manager: erikre
editor: ''
tags: ''
ms.assetid: ''
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 749529e3daa1a63942a1069b8cf793fa08083e97
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564477"
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="e676f-103">Create a new report from a dataset in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="e676f-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="e676f-104">Power BI Embedded reports can now be created from a dataset in your own application.</span><span class="sxs-lookup"><span data-stu-id="e676f-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="e676f-105">The authentication method is similar to that of report embed.</span><span class="sxs-lookup"><span data-stu-id="e676f-105">The authentication method is similar to that of report embed.</span></span> <span data-ttu-id="e676f-106">It is based on access tokens that are specific to a dataset.</span><span class="sxs-lookup"><span data-stu-id="e676f-106">It is based on access tokens that are specific to a dataset.</span></span> <span data-ttu-id="e676f-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span><span class="sxs-lookup"><span data-stu-id="e676f-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="e676f-108">When createing an Embedded report, the tokens issued are for a specific dataset.</span><span class="sxs-lookup"><span data-stu-id="e676f-108">When createing an Embedded report, the tokens issued are for a specific dataset.</span></span> <span data-ttu-id="e676f-109">Tokens should be associated with the embed URL on the same element to ensure each has a unique token.</span><span class="sxs-lookup"><span data-stu-id="e676f-109">Tokens should be associated with the embed URL on the same element to ensure each has a unique token.</span></span> <span data-ttu-id="e676f-110">In order to create an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in the access token.</span><span class="sxs-lookup"><span data-stu-id="e676f-110">In order to create an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in the access token.</span></span>

## <a name="create-access-token-needed-to-create-new-report"></a><span data-ttu-id="e676f-111">Create access token needed to create new report</span><span class="sxs-lookup"><span data-stu-id="e676f-111">Create access token needed to create new report</span></span>

<span data-ttu-id="e676f-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span><span class="sxs-lookup"><span data-stu-id="e676f-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="e676f-113">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span><span class="sxs-lookup"><span data-stu-id="e676f-113">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="e676f-114">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span><span class="sxs-lookup"><span data-stu-id="e676f-114">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="e676f-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span><span class="sxs-lookup"><span data-stu-id="e676f-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="e676f-116">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span><span class="sxs-lookup"><span data-stu-id="e676f-116">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="e676f-117">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="e676f-117">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="e676f-118">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span><span class="sxs-lookup"><span data-stu-id="e676f-118">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="e676f-119">Here is an example of what this would look like using the .NET SDK for Power BI.</span><span class="sxs-lookup"><span data-stu-id="e676f-119">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="e676f-120">In this example, we have our dataset id that we want to creat the new report on.</span><span class="sxs-lookup"><span data-stu-id="e676f-120">In this example, we have our dataset id that we want to creat the new report on.</span></span> <span data-ttu-id="e676f-121">We also need to add the scopes for *Dataset.Read and Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="e676f-121">We also need to add the scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="e676f-122">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="e676f-122">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="e676f-123">**NuGet package install**</span><span class="sxs-lookup"><span data-stu-id="e676f-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="e676f-124">**C# code**</span><span class="sxs-lookup"><span data-stu-id="e676f-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="e676f-125">Create a new blank report</span><span class="sxs-lookup"><span data-stu-id="e676f-125">Create a new blank report</span></span>

<span data-ttu-id="e676f-126">In order to create a new report, the create configuration should be provided.</span><span class="sxs-lookup"><span data-stu-id="e676f-126">In order to create a new report, the create configuration should be provided.</span></span> <span data-ttu-id="e676f-127">This should include the access token, the embedURL and the datasetID that we want to create the report against.</span><span class="sxs-lookup"><span data-stu-id="e676f-127">This should include the access token, the embedURL and the datasetID that we want to create the report against.</span></span> <span data-ttu-id="e676f-128">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="e676f-128">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="e676f-129">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="e676f-129">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="e676f-130">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span><span class="sxs-lookup"><span data-stu-id="e676f-130">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="e676f-131">It also gives code examples for the different operations that are available.</span><span class="sxs-lookup"><span data-stu-id="e676f-131">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="e676f-132">**NuGet package install**</span><span class="sxs-lookup"><span data-stu-id="e676f-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="e676f-133">**JavaScript code**</span><span class="sxs-lookup"><span data-stu-id="e676f-133">**JavaScript code**</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

<span data-ttu-id="e676f-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within the *div* element.</span><span class="sxs-lookup"><span data-stu-id="e676f-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within the *div* element.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="e676f-135">Save new reports</span><span class="sxs-lookup"><span data-stu-id="e676f-135">Save new reports</span></span>

<span data-ttu-id="e676f-136">The report will not actually be created until you call the **save as** operation.</span><span class="sxs-lookup"><span data-stu-id="e676f-136">The report will not actually be created until you call the **save as** operation.</span></span> <span data-ttu-id="e676f-137">This can be done from file menu or from JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e676f-137">This can be done from file menu or from JavaScript.</span></span>

```
 // Get a reference to the embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> <span data-ttu-id="e676f-138">A new report is created only after **save as** is called.</span><span class="sxs-lookup"><span data-stu-id="e676f-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="e676f-139">After you save, the canvas will still show the dataset in edit mode and not the report.</span><span class="sxs-lookup"><span data-stu-id="e676f-139">After you save, the canvas will still show the dataset in edit mode and not the report.</span></span> <span data-ttu-id="e676f-140">You will need to reload the new report like you would any other report.</span><span class="sxs-lookup"><span data-stu-id="e676f-140">You will need to reload the new report like you would any other report.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-the-new-report"></a><span data-ttu-id="e676f-141">Load the new report</span><span class="sxs-lookup"><span data-stu-id="e676f-141">Load the new report</span></span>

<span data-ttu-id="e676f-142">In order to interact with the new report you need to embed it in the same way the application embeds a regular report, meaning, a new token must be issued specifically for the new report and then call the embed method.</span><span class="sxs-lookup"><span data-stu-id="e676f-142">In order to interact with the new report you need to embed it in the same way the application embeds a regular report, meaning, a new token must be issued specifically for the new report and then call the embed method.</span></span>

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="automate-save-and-load-of-a-new-report-using-the-saved-event"></a><span data-ttu-id="e676f-143">Automate save and load of a new report using the "saved" event</span><span class="sxs-lookup"><span data-stu-id="e676f-143">Automate save and load of a new report using the "saved" event</span></span>

<span data-ttu-id="e676f-144">In order to automate the process of "save as" and then loading the new report you can make use of the "saved" Event.</span><span class="sxs-lookup"><span data-stu-id="e676f-144">In order to automate the process of "save as" and then loading the new report you can make use of the "saved" Event.</span></span> <span data-ttu-id="e676f-145">This event is fired when the save operation is complete and it returns a Json object containing the new reportId, report name, the old reportId(if there was one) and if the operation was saveAs or save.</span><span class="sxs-lookup"><span data-stu-id="e676f-145">This event is fired when the save operation is complete and it returns a Json object containing the new reportId, report name, the old reportId(if there was one) and if the operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="e676f-146">To Automate the process you can listen on the "saved" event, take the new reportId, create the new token and embed the new report with it.</span><span class="sxs-lookup"><span data-stu-id="e676f-146">To Automate the process you can listen on the "saved" event, take the new reportId, create the new token and embed the new report with it.</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints to Log window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that the application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide the wanted scopes*/);
        
        
    var embedConfiguration = {
        accessToken: newToken ,
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: newReportId,
    };

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
       
   // report.off removes a given event handler if it exists.
   report.off("saved");
    });
```

## <a name="see-also"></a><span data-ttu-id="e676f-147">See also</span><span class="sxs-lookup"><span data-stu-id="e676f-147">See also</span></span>

[<span data-ttu-id="e676f-148">Get started with sample</span><span class="sxs-lookup"><span data-stu-id="e676f-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="e676f-149">Save reports</span><span class="sxs-lookup"><span data-stu-id="e676f-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
[<span data-ttu-id="e676f-150">Embed a report</span><span class="sxs-lookup"><span data-stu-id="e676f-150">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="e676f-151">Authenticating and authorizing in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="e676f-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="e676f-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="e676f-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="e676f-153">JavaScript Embed Sample</span><span class="sxs-lookup"><span data-stu-id="e676f-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="e676f-154">Power BI Core NuGut Package</span><span class="sxs-lookup"><span data-stu-id="e676f-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="e676f-155">Power BI JavaScript package</span><span class="sxs-lookup"><span data-stu-id="e676f-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="e676f-156">More questions?</span><span class="sxs-lookup"><span data-stu-id="e676f-156">More questions?</span></span> [<span data-ttu-id="e676f-157">Try the Power BI Community</span><span class="sxs-lookup"><span data-stu-id="e676f-157">Try the Power BI Community</span></span>](http://community.powerbi.com/)

