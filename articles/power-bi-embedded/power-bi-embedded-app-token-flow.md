---
title: Authenticating and authorizing with Power BI Embedded
description: Authenticating and authorizing with Power BI Embedded
services: power-bi-embedded
documentationcenter: ''
author: guyinacube
manager: erikre
editor: ''
tags: ''
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 4af70a39f561faee6592bcdd9728ce919757a917
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556349"
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="34db0-103">Authenticating and authorizing with Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="34db0-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="34db0-104">The Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span><span class="sxs-lookup"><span data-stu-id="34db0-104">The Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="34db0-105">In this model, your application manages authentication and authorization for your end-users.</span><span class="sxs-lookup"><span data-stu-id="34db0-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="34db0-106">When necessary, your app creates and sends the App Tokens that tells our service to render the requested report.</span><span class="sxs-lookup"><span data-stu-id="34db0-106">When necessary, your app creates and sends the App Tokens that tells our service to render the requested report.</span></span> <span data-ttu-id="34db0-107">This design doesn't require your app to use Azure Active Directory for user authentication and authorization, although you still can.</span><span class="sxs-lookup"><span data-stu-id="34db0-107">This design doesn't require your app to use Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-to-authenticate"></a><span data-ttu-id="34db0-108">Two ways to authenticate</span><span class="sxs-lookup"><span data-stu-id="34db0-108">Two ways to authenticate</span></span>

<span data-ttu-id="34db0-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span><span class="sxs-lookup"><span data-stu-id="34db0-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="34db0-110">The keys can be found in the **Azure portal** by clicking on **All settings** and then **Access keys**.</span><span class="sxs-lookup"><span data-stu-id="34db0-110">The keys can be found in the **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="34db0-111">Always treat your key as if it were a password.</span><span class="sxs-lookup"><span data-stu-id="34db0-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="34db0-112">These keys have permissions to make any REST API call on a particular workspace collection.</span><span class="sxs-lookup"><span data-stu-id="34db0-112">These keys have permissions to make any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="34db0-113">To use a key on a REST call, add the following authorization header:</span><span class="sxs-lookup"><span data-stu-id="34db0-113">To use a key on a REST call, add the following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="34db0-114">**App token** - App tokens are used for all embedding requests.</span><span class="sxs-lookup"><span data-stu-id="34db0-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="34db0-115">They’re designed to be run client-side, so they're restricted to a single report and it’s best practice to set an expiration time.</span><span class="sxs-lookup"><span data-stu-id="34db0-115">They’re designed to be run client-side, so they're restricted to a single report and it’s best practice to set an expiration time.</span></span>

<span data-ttu-id="34db0-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span><span class="sxs-lookup"><span data-stu-id="34db0-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="34db0-117">Your app token can contain the following claims:</span><span class="sxs-lookup"><span data-stu-id="34db0-117">Your app token can contain the following claims:</span></span>

| <span data-ttu-id="34db0-118">Claim</span><span class="sxs-lookup"><span data-stu-id="34db0-118">Claim</span></span> | <span data-ttu-id="34db0-119">Description</span><span class="sxs-lookup"><span data-stu-id="34db0-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="34db0-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="34db0-120">**ver**</span></span> |<span data-ttu-id="34db0-121">The version of the app token.</span><span class="sxs-lookup"><span data-stu-id="34db0-121">The version of the app token.</span></span> <span data-ttu-id="34db0-122">0.2.0 is the current version.</span><span class="sxs-lookup"><span data-stu-id="34db0-122">0.2.0 is the current version.</span></span> |
| <span data-ttu-id="34db0-123">**aud**</span><span class="sxs-lookup"><span data-stu-id="34db0-123">**aud**</span></span> |<span data-ttu-id="34db0-124">The intended recipient of the token.</span><span class="sxs-lookup"><span data-stu-id="34db0-124">The intended recipient of the token.</span></span> <span data-ttu-id="34db0-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span><span class="sxs-lookup"><span data-stu-id="34db0-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="34db0-126">**iss**</span><span class="sxs-lookup"><span data-stu-id="34db0-126">**iss**</span></span> |<span data-ttu-id="34db0-127">A string indicating the application which issued the token.</span><span class="sxs-lookup"><span data-stu-id="34db0-127">A string indicating the application which issued the token.</span></span> |
| <span data-ttu-id="34db0-128">**type**</span><span class="sxs-lookup"><span data-stu-id="34db0-128">**type**</span></span> |<span data-ttu-id="34db0-129">The type of app token which is being created.</span><span class="sxs-lookup"><span data-stu-id="34db0-129">The type of app token which is being created.</span></span> <span data-ttu-id="34db0-130">Current the only supported type is **embed**.</span><span class="sxs-lookup"><span data-stu-id="34db0-130">Current the only supported type is **embed**.</span></span> |
| <span data-ttu-id="34db0-131">**wcn**</span><span class="sxs-lookup"><span data-stu-id="34db0-131">**wcn**</span></span> |<span data-ttu-id="34db0-132">Workspace collection name the token is being issued for.</span><span class="sxs-lookup"><span data-stu-id="34db0-132">Workspace collection name the token is being issued for.</span></span> |
| <span data-ttu-id="34db0-133">**wid**</span><span class="sxs-lookup"><span data-stu-id="34db0-133">**wid**</span></span> |<span data-ttu-id="34db0-134">Workspace ID the token is being issued for.</span><span class="sxs-lookup"><span data-stu-id="34db0-134">Workspace ID the token is being issued for.</span></span> |
| <span data-ttu-id="34db0-135">**rid**</span><span class="sxs-lookup"><span data-stu-id="34db0-135">**rid**</span></span> |<span data-ttu-id="34db0-136">Report ID the token is being issued for.</span><span class="sxs-lookup"><span data-stu-id="34db0-136">Report ID the token is being issued for.</span></span> |
| <span data-ttu-id="34db0-137">**username** (optional)</span><span class="sxs-lookup"><span data-stu-id="34db0-137">**username** (optional)</span></span> |<span data-ttu-id="34db0-138">Used with RLS, this is a string that can help identify the user when applying RLS rules.</span><span class="sxs-lookup"><span data-stu-id="34db0-138">Used with RLS, this is a string that can help identify the user when applying RLS rules.</span></span> |
| <span data-ttu-id="34db0-139">**roles** (optional)</span><span class="sxs-lookup"><span data-stu-id="34db0-139">**roles** (optional)</span></span> |<span data-ttu-id="34db0-140">A string containing the roles to select when applying Row Level Security rules.</span><span class="sxs-lookup"><span data-stu-id="34db0-140">A string containing the roles to select when applying Row Level Security rules.</span></span> <span data-ttu-id="34db0-141">If passing more than one role, they should be passed as a sting array.</span><span class="sxs-lookup"><span data-stu-id="34db0-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="34db0-142">**scp** (optional)</span><span class="sxs-lookup"><span data-stu-id="34db0-142">**scp** (optional)</span></span> |<span data-ttu-id="34db0-143">A string containing the permissions scopes.</span><span class="sxs-lookup"><span data-stu-id="34db0-143">A string containing the permissions scopes.</span></span> <span data-ttu-id="34db0-144">If passing more than one role, they should be passed as a sting array.</span><span class="sxs-lookup"><span data-stu-id="34db0-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="34db0-145">**exp** (optional)</span><span class="sxs-lookup"><span data-stu-id="34db0-145">**exp** (optional)</span></span> |<span data-ttu-id="34db0-146">Indicates the time in which the token will expire.</span><span class="sxs-lookup"><span data-stu-id="34db0-146">Indicates the time in which the token will expire.</span></span> <span data-ttu-id="34db0-147">These should be passed in as Unix timestamps.</span><span class="sxs-lookup"><span data-stu-id="34db0-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="34db0-148">**nbf** (optional)</span><span class="sxs-lookup"><span data-stu-id="34db0-148">**nbf** (optional)</span></span> |<span data-ttu-id="34db0-149">Indicates the time in which the token starts being valid.</span><span class="sxs-lookup"><span data-stu-id="34db0-149">Indicates the time in which the token starts being valid.</span></span> <span data-ttu-id="34db0-150">These should be passed in as Unix timestamps.</span><span class="sxs-lookup"><span data-stu-id="34db0-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="34db0-151">A sample app token will look like this:</span><span class="sxs-lookup"><span data-stu-id="34db0-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="34db0-152">When decoded, it will look something like this:</span><span class="sxs-lookup"><span data-stu-id="34db0-152">When decoded, it will look something like this:</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

<span data-ttu-id="34db0-153">There are methods available within the SDKs that make creation of apptokens easier.</span><span class="sxs-lookup"><span data-stu-id="34db0-153">There are methods available within the SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="34db0-154">For example, for .NET you can look at the [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span><span class="sxs-lookup"><span data-stu-id="34db0-154">For example, for .NET you can look at the [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="34db0-155">For the .NET SDK, you can refer to [Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span><span class="sxs-lookup"><span data-stu-id="34db0-155">For the .NET SDK, you can refer to [Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="34db0-156">Scopes</span><span class="sxs-lookup"><span data-stu-id="34db0-156">Scopes</span></span>

<span data-ttu-id="34db0-157">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span><span class="sxs-lookup"><span data-stu-id="34db0-157">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span></span> <span data-ttu-id="34db0-158">For this reason, you can generate a token with scoped permissions.</span><span class="sxs-lookup"><span data-stu-id="34db0-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="34db0-159">The following are the available scopes for Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="34db0-159">The following are the available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="34db0-160">Scope</span><span class="sxs-lookup"><span data-stu-id="34db0-160">Scope</span></span>|<span data-ttu-id="34db0-161">Description</span><span class="sxs-lookup"><span data-stu-id="34db0-161">Description</span></span>|
|---|---|
|<span data-ttu-id="34db0-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="34db0-162">Dataset.Read</span></span>|<span data-ttu-id="34db0-163">Provides permission to read the specified dataset.</span><span class="sxs-lookup"><span data-stu-id="34db0-163">Provides permission to read the specified dataset.</span></span>|
|<span data-ttu-id="34db0-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="34db0-164">Dataset.Write</span></span>|<span data-ttu-id="34db0-165">Provides permission to write to the specified dataset.</span><span class="sxs-lookup"><span data-stu-id="34db0-165">Provides permission to write to the specified dataset.</span></span>|
|<span data-ttu-id="34db0-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="34db0-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="34db0-167">Provides permission to read and write to the specificed dataset.</span><span class="sxs-lookup"><span data-stu-id="34db0-167">Provides permission to read and write to the specificed dataset.</span></span>|
|<span data-ttu-id="34db0-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="34db0-168">Report.Read</span></span>|<span data-ttu-id="34db0-169">Provides permission to view the specified report.</span><span class="sxs-lookup"><span data-stu-id="34db0-169">Provides permission to view the specified report.</span></span>|
|<span data-ttu-id="34db0-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="34db0-170">Report.ReadWrite</span></span>|<span data-ttu-id="34db0-171">Provides permission to view and edit the specified report.</span><span class="sxs-lookup"><span data-stu-id="34db0-171">Provides permission to view and edit the specified report.</span></span>|
|<span data-ttu-id="34db0-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="34db0-172">Workspace.Report.Create</span></span>|<span data-ttu-id="34db0-173">Provides permission to create a new report within the specified workspace.</span><span class="sxs-lookup"><span data-stu-id="34db0-173">Provides permission to create a new report within the specified workspace.</span></span>|
|<span data-ttu-id="34db0-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="34db0-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="34db0-175">Provides permission to clone an existing report within the specified workspace.</span><span class="sxs-lookup"><span data-stu-id="34db0-175">Provides permission to clone an existing report within the specified workspace.</span></span>|

<span data-ttu-id="34db0-176">You can supply multiple scopes by using a space between the scopes like the following.</span><span class="sxs-lookup"><span data-stu-id="34db0-176">You can supply multiple scopes by using a space between the scopes like the following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="34db0-177">**Required claims - scopes**</span><span class="sxs-lookup"><span data-stu-id="34db0-177">**Required claims - scopes**</span></span>

<span data-ttu-id="34db0-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting the allowed permissions to workspace resources (Report, Dataset, etc.)</span><span class="sxs-lookup"><span data-stu-id="34db0-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting the allowed permissions to workspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="34db0-179">A decoded token, with scopes defined, would look similar to the following.</span><span class="sxs-lookup"><span data-stu-id="34db0-179">A decoded token, with scopes defined, would look similar to the following.</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a><span data-ttu-id="34db0-180">Operations and scopes</span><span class="sxs-lookup"><span data-stu-id="34db0-180">Operations and scopes</span></span>

|<span data-ttu-id="34db0-181">Operation</span><span class="sxs-lookup"><span data-stu-id="34db0-181">Operation</span></span>|<span data-ttu-id="34db0-182">Target resource</span><span class="sxs-lookup"><span data-stu-id="34db0-182">Target resource</span></span>|<span data-ttu-id="34db0-183">Token permissions</span><span class="sxs-lookup"><span data-stu-id="34db0-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="34db0-184">Create (in-memory) a new report based on a dataset.</span><span class="sxs-lookup"><span data-stu-id="34db0-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="34db0-185">Dataset</span><span class="sxs-lookup"><span data-stu-id="34db0-185">Dataset</span></span>|<span data-ttu-id="34db0-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="34db0-186">Dataset.Read</span></span>|
|<span data-ttu-id="34db0-187">Create (in-memory) a new report based on a dataset and save the report.</span><span class="sxs-lookup"><span data-stu-id="34db0-187">Create (in-memory) a new report based on a dataset and save the report.</span></span>|<span data-ttu-id="34db0-188">Dataset</span><span class="sxs-lookup"><span data-stu-id="34db0-188">Dataset</span></span>|<span data-ttu-id="34db0-189">\* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="34db0-189">\* Dataset.Read</span></span><br><span data-ttu-id="34db0-190">\* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="34db0-190">\* Workspace.Report.Create</span></span>|
|<span data-ttu-id="34db0-191">View and explore/edit (in-memory) an existing report.</span><span class="sxs-lookup"><span data-stu-id="34db0-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="34db0-192">Report.Read implies Dataset.Read.</span><span class="sxs-lookup"><span data-stu-id="34db0-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="34db0-193">This will not allow permissions to save edits.</span><span class="sxs-lookup"><span data-stu-id="34db0-193">This will not allow permissions to save edits.</span></span>|<span data-ttu-id="34db0-194">Report</span><span class="sxs-lookup"><span data-stu-id="34db0-194">Report</span></span>|<span data-ttu-id="34db0-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="34db0-195">Report.Read</span></span>|
|<span data-ttu-id="34db0-196">Edit and save an existing report.</span><span class="sxs-lookup"><span data-stu-id="34db0-196">Edit and save an existing report.</span></span>|<span data-ttu-id="34db0-197">Report</span><span class="sxs-lookup"><span data-stu-id="34db0-197">Report</span></span>|<span data-ttu-id="34db0-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="34db0-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="34db0-199">Save a copy of a report (Save As).</span><span class="sxs-lookup"><span data-stu-id="34db0-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="34db0-200">Report</span><span class="sxs-lookup"><span data-stu-id="34db0-200">Report</span></span>|<span data-ttu-id="34db0-201">\* Report.Read</span><span class="sxs-lookup"><span data-stu-id="34db0-201">\* Report.Read</span></span><br><span data-ttu-id="34db0-202">\* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="34db0-202">\* Workspace.Report.Copy</span></span>|

## <a name="heres-how-the-flow-works"></a><span data-ttu-id="34db0-203">Here's how the flow works</span><span class="sxs-lookup"><span data-stu-id="34db0-203">Here's how the flow works</span></span>
1. <span data-ttu-id="34db0-204">Copy the API keys to your application.</span><span class="sxs-lookup"><span data-stu-id="34db0-204">Copy the API keys to your application.</span></span> <span data-ttu-id="34db0-205">You can get the keys in **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="34db0-205">You can get the keys in **Azure Portal**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="34db0-206">Token asserts a claim and has an expiration time.</span><span class="sxs-lookup"><span data-stu-id="34db0-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="34db0-207">Token gets signed with an API access keys.</span><span class="sxs-lookup"><span data-stu-id="34db0-207">Token gets signed with an API access keys.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="34db0-208">User requests to view a report.</span><span class="sxs-lookup"><span data-stu-id="34db0-208">User requests to view a report.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="34db0-209">Token is validated with an API access keys.</span><span class="sxs-lookup"><span data-stu-id="34db0-209">Token is validated with an API access keys.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="34db0-210">Power BI Embedded sends a report to user.</span><span class="sxs-lookup"><span data-stu-id="34db0-210">Power BI Embedded sends a report to user.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="34db0-211">After **Power BI Embedded** sends a report to the user, the user can view the report in your custom app.</span><span class="sxs-lookup"><span data-stu-id="34db0-211">After **Power BI Embedded** sends a report to the user, the user can view the report in your custom app.</span></span> <span data-ttu-id="34db0-212">For example, if you imported the [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), the sample web app would look like this:</span><span class="sxs-lookup"><span data-stu-id="34db0-212">For example, if you imported the [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), the sample web app would look like this:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="34db0-213">See Also</span><span class="sxs-lookup"><span data-stu-id="34db0-213">See Also</span></span>

[<span data-ttu-id="34db0-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="34db0-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="34db0-215">Get started with Microsoft Power BI Embedded sample</span><span class="sxs-lookup"><span data-stu-id="34db0-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="34db0-216">Common Microsoft Power BI Embedded scenarios</span><span class="sxs-lookup"><span data-stu-id="34db0-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="34db0-217">Get started with Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="34db0-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="34db0-218">PowerBI-CSharp Git Repo</span><span class="sxs-lookup"><span data-stu-id="34db0-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="34db0-219">More questions?</span><span class="sxs-lookup"><span data-stu-id="34db0-219">More questions?</span></span> [<span data-ttu-id="34db0-220">Try the Power BI Community</span><span class="sxs-lookup"><span data-stu-id="34db0-220">Try the Power BI Community</span></span>](http://community.powerbi.com/)








