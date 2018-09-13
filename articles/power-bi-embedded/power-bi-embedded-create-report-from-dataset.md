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
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a>Create a new report from a dataset in Power BI Embedded

Power BI Embedded reports can now be created from a dataset in your own application. 

The authentication method is similar to that of report embed. It is based on access tokens that are specific to a dataset. Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.

When createing an Embedded report, the tokens issued are for a specific dataset. Tokens should be associated with the embed URL on the same element to ensure each has a unique token. In order to create an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in the access token.

## <a name="create-access-token-needed-to-create-new-report"></a>Create access token needed to create new report

Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens. The tokens are signed with the access key from your Azure Power BI Embedded workspace collection. Embed tokens, by default, are used to provide read only access to a report to embed into an application. Embed tokens are issued for a specific report and should be associated with an embed URL.

Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens. For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md). You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method. Here is an example of what this would look like using the .NET SDK for Power BI.

In this example, we have our dataset id that we want to creat the new report on. We also need to add the scopes for *Dataset.Read and Workspace.Report.Create*.

The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**NuGet package install**

```
Install-Package Microsoft.PowerBI.Core
```

**C# code**

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a>Create a new blank report

In order to create a new report, the create configuration should be provided. This should include the access token, the embedURL and the datasetID that we want to create the report against. This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality. It also gives code examples for the different operations that are available.

**NuGet package install**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**JavaScript code**

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

Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within the *div* element.

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a>Save new reports

The report will not actually be created until you call the **save as** operation. This can be done from file menu or from JavaScript.

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
> A new report is created only after **save as** is called. After you save, the canvas will still show the dataset in edit mode and not the report. You will need to reload the new report like you would any other report.

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-the-new-report"></a>Load the new report

In order to interact with the new report you need to embed it in the same way the application embeds a regular report, meaning, a new token must be issued specifically for the new report and then call the embed method.

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

## <a name="automate-save-and-load-of-a-new-report-using-the-saved-event"></a>Automate save and load of a new report using the "saved" event

In order to automate the process of "save as" and then loading the new report you can make use of the "saved" Event. This event is fired when the save operation is complete and it returns a Json object containing the new reportId, report name, the old reportId(if there was one) and if the operation was saveAs or save.

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

To Automate the process you can listen on the "saved" event, take the new reportId, create the new token and embed the new report with it.

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

## <a name="see-also"></a>See also

[Get started with sample](power-bi-embedded-get-started-sample.md)  
[Save reports](power-bi-embedded-save-reports.md)  
[Embed a report](power-bi-embedded-embed-report.md)  
[Authenticating and authorizing in Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
More questions? [Try the Power BI Community](http://community.powerbi.com/)

