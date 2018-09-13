---
title: Save reports in Azure Power BI Embedded | Microsoft Docs
description: Learn how to save reports within Power BI embedded. This requires proper permissions in order to work successfully.
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
ms.openlocfilehash: ad895004cc2972f2ded81566186325a16d401151
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551454"
---
# <a name="save-reports-in-power-bi-embedded"></a><span data-ttu-id="4c636-104">Save reports in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="4c636-104">Save reports in Power BI Embedded</span></span>

<span data-ttu-id="4c636-105">Learn how to save reports within Power BI embedded.</span><span class="sxs-lookup"><span data-stu-id="4c636-105">Learn how to save reports within Power BI embedded.</span></span> <span data-ttu-id="4c636-106">This requires proper permissions in order to work successfully.</span><span class="sxs-lookup"><span data-stu-id="4c636-106">This requires proper permissions in order to work successfully.</span></span>

<span data-ttu-id="4c636-107">Within Power BI Embedded, you can edit existing reports and save them.</span><span class="sxs-lookup"><span data-stu-id="4c636-107">Within Power BI Embedded, you can edit existing reports and save them.</span></span> <span data-ttu-id="4c636-108">You can also create a new report and save as a new report to create one.</span><span class="sxs-lookup"><span data-stu-id="4c636-108">You can also create a new report and save as a new report to create one.</span></span>

<span data-ttu-id="4c636-109">In order to save a report you first need to create a token for the specific report with the right scopes:</span><span class="sxs-lookup"><span data-stu-id="4c636-109">In order to save a report you first need to create a token for the specific report with the right scopes:</span></span>

* <span data-ttu-id="4c636-110">To enable save Report.ReadWrite scope is required</span><span class="sxs-lookup"><span data-stu-id="4c636-110">To enable save Report.ReadWrite scope is required</span></span>
* <span data-ttu-id="4c636-111">To enable save as, Report.Read and Workspace.Report.Copy scopes are required</span><span class="sxs-lookup"><span data-stu-id="4c636-111">To enable save as, Report.Read and Workspace.Report.Copy scopes are required</span></span>
* <span data-ttu-id="4c636-112">To enable save and save as, Report.ReadWrite and Workspace.Report.Copy are requierd</span><span class="sxs-lookup"><span data-stu-id="4c636-112">To enable save and save as, Report.ReadWrite and Workspace.Report.Copy are requierd</span></span>

<span data-ttu-id="4c636-113">Respectively in order to enable the right save/save as buttons in file menu you need to provide the right permission in the Embed configuration when you Embed the report:</span><span class="sxs-lookup"><span data-stu-id="4c636-113">Respectively in order to enable the right save/save as buttons in file menu you need to provide the right permission in the Embed configuration when you Embed the report:</span></span>

* <span data-ttu-id="4c636-114">models.Permissions.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="4c636-114">models.Permissions.ReadWrite</span></span>
* <span data-ttu-id="4c636-115">models.Permissions.Copy</span><span class="sxs-lookup"><span data-stu-id="4c636-115">models.Permissions.Copy</span></span>
* <span data-ttu-id="4c636-116">models.Permissions.All</span><span class="sxs-lookup"><span data-stu-id="4c636-116">models.Permissions.All</span></span>

> [!NOTE]
> <span data-ttu-id="4c636-117">Your access token also needs the appropriate scopes.</span><span class="sxs-lookup"><span data-stu-id="4c636-117">Your access token also needs the appropriate scopes.</span></span> <span data-ttu-id="4c636-118">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="4c636-118">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

## <a name="embed-report-in-edit-mode"></a><span data-ttu-id="4c636-119">Embed report in edit mode</span><span class="sxs-lookup"><span data-stu-id="4c636-119">Embed report in edit mode</span></span>

<span data-ttu-id="4c636-120">Let's say you want to Embed a report in edit mode inside your app, to do so just pass the right properties in Embed configuration and call powerbi.embed().</span><span class="sxs-lookup"><span data-stu-id="4c636-120">Let's say you want to Embed a report in edit mode inside your app, to do so just pass the right properties in Embed configuration and call powerbi.embed().</span></span> <span data-ttu-id="4c636-121">You will need to supply permissions and a viewMode in order to see the save and save as buttons when in edit mode.</span><span class="sxs-lookup"><span data-stu-id="4c636-121">You will need to supply permissions and a viewMode in order to see the save and save as buttons when in edit mode.</span></span> <span data-ttu-id="4c636-122">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span><span class="sxs-lookup"><span data-stu-id="4c636-122">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="4c636-123">For example in JavaScript:</span><span class="sxs-lookup"><span data-stu-id="4c636-123">For example in JavaScript:</span></span>

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used to describe the what and how to embed.
    // This object is used when calling powerbi.embed.
    // This also includes settings and options such as filters.
    // You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
    var config= {
        type: 'report',
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        id:  '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
        permissions: models.Permissions.All /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.Edit,
        settings: {
            filterPaneEnabled: true,
            navContentPaneEnabled: true
        }
    };

    // Get a reference to the embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed the report and display it within the div container.
    var report = powerbi.embed(reportContainer, config);
```

<span data-ttu-id="4c636-124">Now a report will be embedded in your app in edit mode.</span><span class="sxs-lookup"><span data-stu-id="4c636-124">Now a report will be embedded in your app in edit mode.</span></span>

## <a name="save-report"></a><span data-ttu-id="4c636-125">Save report</span><span class="sxs-lookup"><span data-stu-id="4c636-125">Save report</span></span>

<span data-ttu-id="4c636-126">After Embbeding the report in edit mode with the right token and permissions you can save the report from the file menu or from javascript:</span><span class="sxs-lookup"><span data-stu-id="4c636-126">After Embbeding the report in edit mode with the right token and permissions you can save the report from the file menu or from javascript:</span></span>

```
 // Get a reference to the embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a><span data-ttu-id="4c636-127">Save as</span><span class="sxs-lookup"><span data-stu-id="4c636-127">Save as</span></span>

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
> <span data-ttu-id="4c636-128">Only after *save as* is a new report created.</span><span class="sxs-lookup"><span data-stu-id="4c636-128">Only after *save as* is a new report created.</span></span> <span data-ttu-id="4c636-129">After the save, the canvas is still showing the old report in edit mode and not the new report.</span><span class="sxs-lookup"><span data-stu-id="4c636-129">After the save, the canvas is still showing the old report in edit mode and not the new report.</span></span> <span data-ttu-id="4c636-130">You will need to embed the new report that was created.</span><span class="sxs-lookup"><span data-stu-id="4c636-130">You will need to embed the new report that was created.</span></span> <span data-ttu-id="4c636-131">This requires a new access token as they are created per report.</span><span class="sxs-lookup"><span data-stu-id="4c636-131">This requires a new access token as they are created per report.</span></span>

<span data-ttu-id="4c636-132">You will then need to load the new report after a *save as*.</span><span class="sxs-lookup"><span data-stu-id="4c636-132">You will then need to load the new report after a *save as*.</span></span> <span data-ttu-id="4c636-133">This is similar to embedding any report.</span><span class="sxs-lookup"><span data-stu-id="4c636-133">This is similar to embedding any report.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="4c636-134">See also</span><span class="sxs-lookup"><span data-stu-id="4c636-134">See also</span></span>

[<span data-ttu-id="4c636-135">Get started with sample</span><span class="sxs-lookup"><span data-stu-id="4c636-135">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="4c636-136">Embed a report</span><span class="sxs-lookup"><span data-stu-id="4c636-136">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="4c636-137">Create a new report from a dataset</span><span class="sxs-lookup"><span data-stu-id="4c636-137">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="4c636-138">Authenticating and authorizing in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="4c636-138">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="4c636-139">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="4c636-139">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="4c636-140">JavaScript Embed Sample</span><span class="sxs-lookup"><span data-stu-id="4c636-140">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="4c636-141">More questions?</span><span class="sxs-lookup"><span data-stu-id="4c636-141">More questions?</span></span> [<span data-ttu-id="4c636-142">Try the Power BI Community</span><span class="sxs-lookup"><span data-stu-id="4c636-142">Try the Power BI Community</span></span>](http://community.powerbi.com/)

