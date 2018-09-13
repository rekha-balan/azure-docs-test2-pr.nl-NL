---
title: Embed a report in Azure Power BI Embedded | Microsoft Docs
description: Learn how to embed a report that is in Power BI Embedded into your application.
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
ms.openlocfilehash: 3d865af2418c9c557c861a379766a125d75cebf1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556072"
---
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="b2f85-103">Embed a report in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="b2f85-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="b2f85-104">Learn how to embed a report that is in Power BI Embedded into your application.</span><span class="sxs-lookup"><span data-stu-id="b2f85-104">Learn how to embed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="b2f85-105">We will look at how to actually embed a report into your application.</span><span class="sxs-lookup"><span data-stu-id="b2f85-105">We will look at how to actually embed a report into your application.</span></span> <span data-ttu-id="b2f85-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span><span class="sxs-lookup"><span data-stu-id="b2f85-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="b2f85-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b2f85-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="b2f85-108">You can use the .NET (C#) or Node.js SDK, along with JavaScript, to easily build your application with Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="b2f85-108">You can use the .NET (C#) or Node.js SDK, along with JavaScript, to easily build your application with Power BI Embedded.</span></span> 

## <a name="using-the-access-keys-to-use-rest-apis"></a><span data-ttu-id="b2f85-109">Using the access keys to use REST APIs</span><span class="sxs-lookup"><span data-stu-id="b2f85-109">Using the access keys to use REST APIs</span></span>

<span data-ttu-id="b2f85-110">In order to call the REST API, you can pass the access key which you can get from the Azure portal for a given workspace collection.</span><span class="sxs-lookup"><span data-stu-id="b2f85-110">In order to call the REST API, you can pass the access key which you can get from the Azure portal for a given workspace collection.</span></span> <span data-ttu-id="b2f85-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b2f85-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="b2f85-112">Get a report id</span><span class="sxs-lookup"><span data-stu-id="b2f85-112">Get a report id</span></span>

<span data-ttu-id="b2f85-113">Every access token is based on a report.</span><span class="sxs-lookup"><span data-stu-id="b2f85-113">Every access token is based on a report.</span></span> <span data-ttu-id="b2f85-114">You will need to get the given report id for the report that you want to embed.</span><span class="sxs-lookup"><span data-stu-id="b2f85-114">You will need to get the given report id for the report that you want to embed.</span></span> <span data-ttu-id="b2f85-115">This can be done based on calls to the [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span><span class="sxs-lookup"><span data-stu-id="b2f85-115">This can be done based on calls to the [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="b2f85-116">This will return the report id and the embed url.</span><span class="sxs-lookup"><span data-stu-id="b2f85-116">This will return the report id and the embed url.</span></span> <span data-ttu-id="b2f85-117">This can be done using the Power BI .NET SDK or calling the REST API directly.</span><span class="sxs-lookup"><span data-stu-id="b2f85-117">This can be done using the Power BI .NET SDK or calling the REST API directly.</span></span>

### <a name="using-the-power-bi-net-sdk"></a><span data-ttu-id="b2f85-118">Using the Power BI .NET SDK</span><span class="sxs-lookup"><span data-stu-id="b2f85-118">Using the Power BI .NET SDK</span></span>

<span data-ttu-id="b2f85-119">When using the .NET SDK, you will need to create a token credential which is based on the access key you get from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b2f85-119">When using the .NET SDK, you will need to create a token credential which is based on the access key you get from the Azure portal.</span></span> <span data-ttu-id="b2f85-120">This requires that you install the [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span><span class="sxs-lookup"><span data-stu-id="b2f85-120">This requires that you install the [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="b2f85-121">**NuGet package install**</span><span class="sxs-lookup"><span data-stu-id="b2f85-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="b2f85-122">**C# code**</span><span class="sxs-lookup"><span data-stu-id="b2f85-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select the report that you want to work with from the collection of reports.
```

### <a name="calling-the-rest-api-directly"></a><span data-ttu-id="b2f85-123">Calling the REST API directly</span><span class="sxs-lookup"><span data-stu-id="b2f85-123">Calling the REST API directly</span></span>

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response to get the report you want to work with.
    }

}
```

## <a name="create-an-access-token"></a><span data-ttu-id="b2f85-124">Create an access token</span><span class="sxs-lookup"><span data-stu-id="b2f85-124">Create an access token</span></span>

<span data-ttu-id="b2f85-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span><span class="sxs-lookup"><span data-stu-id="b2f85-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="b2f85-126">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span><span class="sxs-lookup"><span data-stu-id="b2f85-126">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="b2f85-127">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span><span class="sxs-lookup"><span data-stu-id="b2f85-127">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="b2f85-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span><span class="sxs-lookup"><span data-stu-id="b2f85-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="b2f85-129">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span><span class="sxs-lookup"><span data-stu-id="b2f85-129">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="b2f85-130">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="b2f85-130">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="b2f85-131">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span><span class="sxs-lookup"><span data-stu-id="b2f85-131">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="b2f85-132">Here is an example of what this would look like using the .NET SDK for Power BI.</span><span class="sxs-lookup"><span data-stu-id="b2f85-132">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="b2f85-133">You will use the report id that you retrieved earlier.</span><span class="sxs-lookup"><span data-stu-id="b2f85-133">You will use the report id that you retrieved earlier.</span></span> <span data-ttu-id="b2f85-134">Once the embed token is created, you will then use the access key to generate the token which you can use from the javascript perspective.</span><span class="sxs-lookup"><span data-stu-id="b2f85-134">Once the embed token is created, you will then use the access key to generate the token which you can use from the javascript perspective.</span></span> <span data-ttu-id="b2f85-135">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="b2f85-135">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="b2f85-136">**NuGet package install**</span><span class="sxs-lookup"><span data-stu-id="b2f85-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="b2f85-137">**C# code**</span><span class="sxs-lookup"><span data-stu-id="b2f85-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-to-embed-tokens"></a><span data-ttu-id="b2f85-138">Adding permission scopes to embed tokens</span><span class="sxs-lookup"><span data-stu-id="b2f85-138">Adding permission scopes to embed tokens</span></span>

<span data-ttu-id="b2f85-139">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span><span class="sxs-lookup"><span data-stu-id="b2f85-139">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span></span> <span data-ttu-id="b2f85-140">For this reason, you can generate a token with scoped permissions.</span><span class="sxs-lookup"><span data-stu-id="b2f85-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="b2f85-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span><span class="sxs-lookup"><span data-stu-id="b2f85-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="b2f85-142">Embed using JavaScript</span><span class="sxs-lookup"><span data-stu-id="b2f85-142">Embed using JavaScript</span></span>

<span data-ttu-id="b2f85-143">After you have the access token and the report id, we can embed the report using JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b2f85-143">After you have the access token and the report id, we can embed the report using JavaScript.</span></span> <span data-ttu-id="b2f85-144">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="b2f85-144">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="b2f85-145">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="b2f85-145">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="b2f85-146">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span><span class="sxs-lookup"><span data-stu-id="b2f85-146">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="b2f85-147">It also gives code examples for the different operations that are available.</span><span class="sxs-lookup"><span data-stu-id="b2f85-147">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="b2f85-148">**NuGet package install**</span><span class="sxs-lookup"><span data-stu-id="b2f85-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="b2f85-149">**JavaScript code**</span><span class="sxs-lookup"><span data-stu-id="b2f85-149">**JavaScript code**</span></span>

```
<script src="/scripts/powerbi.js"></script>
<div id="reportContainer"></div>

var embedConfiguration = {
    type: 'report',
    accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
    id: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed'
};

var $reportContainer = $('#reportContainer');
var report = powerbi.embed($reportContainer.get(0), embedConfiguration);
```

### <a name="set-the-size-of-embedded-elements"></a><span data-ttu-id="b2f85-150">Set the size of embedded elements</span><span class="sxs-lookup"><span data-stu-id="b2f85-150">Set the size of embedded elements</span></span>

<span data-ttu-id="b2f85-151">The report will automatically be embedded based on the size of its container.</span><span class="sxs-lookup"><span data-stu-id="b2f85-151">The report will automatically be embedded based on the size of its container.</span></span> <span data-ttu-id="b2f85-152">To override the default size of the embeds simply add a CSS class attribute or inline styles for width & height.</span><span class="sxs-lookup"><span data-stu-id="b2f85-152">To override the default size of the embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="b2f85-153">See also</span><span class="sxs-lookup"><span data-stu-id="b2f85-153">See also</span></span>

[<span data-ttu-id="b2f85-154">Get started with sample</span><span class="sxs-lookup"><span data-stu-id="b2f85-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="b2f85-155">Authenticating and authorizing in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="b2f85-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="b2f85-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="b2f85-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="b2f85-157">JavaScript Embed Sample</span><span class="sxs-lookup"><span data-stu-id="b2f85-157">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="b2f85-158">Power BI JavaScript package</span><span class="sxs-lookup"><span data-stu-id="b2f85-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="b2f85-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="b2f85-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="b2f85-160">PowerBI-CSharp Git Repo</span><span class="sxs-lookup"><span data-stu-id="b2f85-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="b2f85-161">PowerBI-Node Git Repo</span><span class="sxs-lookup"><span data-stu-id="b2f85-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="b2f85-162">More questions?</span><span class="sxs-lookup"><span data-stu-id="b2f85-162">More questions?</span></span> [<span data-ttu-id="b2f85-163">Try the Power BI Community</span><span class="sxs-lookup"><span data-stu-id="b2f85-163">Try the Power BI Community</span></span>](http://community.powerbi.com/)
