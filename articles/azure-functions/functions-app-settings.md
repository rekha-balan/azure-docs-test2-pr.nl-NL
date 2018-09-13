---
title: App settings reference for Azure Functions
description: Reference documentation for the Azure Functions app settings or environment variables.
services: functions
author: ggailey777
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 08/22/2018
ms.author: glenga
ms.openlocfilehash: 9f6746f1bf8fb65e39933afa00b74a2b8266a1a9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864540"
---
# <a name="app-settings-reference-for-azure-functions"></a><span data-ttu-id="6bddd-103">App settings reference for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="6bddd-103">App settings reference for Azure Functions</span></span>

<span data-ttu-id="6bddd-104">App settings in a function app contain global configuration options that affect all functions for that function app.</span><span class="sxs-lookup"><span data-stu-id="6bddd-104">App settings in a function app contain global configuration options that affect all functions for that function app.</span></span> <span data-ttu-id="6bddd-105">When you run locally, these settings are in environment variables.</span><span class="sxs-lookup"><span data-stu-id="6bddd-105">When you run locally, these settings are in environment variables.</span></span> <span data-ttu-id="6bddd-106">This article lists the app settings that are available in function apps.</span><span class="sxs-lookup"><span data-stu-id="6bddd-106">This article lists the app settings that are available in function apps.</span></span>

<span data-ttu-id="6bddd-107">[!INCLUDE [Function app settings](../../includes/functions-app-settings.md]</span><span class="sxs-lookup"><span data-stu-id="6bddd-107">[!INCLUDE [Function app settings](../../includes/functions-app-settings.md]</span></span>

<span data-ttu-id="6bddd-108">There are other global configuration options in the [host.json](functions-host-json.md) file and in the [local.settings.json](functions-run-local.md#local-settings-file) file.</span><span class="sxs-lookup"><span data-stu-id="6bddd-108">There are other global configuration options in the [host.json](functions-host-json.md) file and in the [local.settings.json](functions-run-local.md#local-settings-file) file.</span></span>

## <a name="appinsightsinstrumentationkey"></a><span data-ttu-id="6bddd-109">APPINSIGHTS_INSTRUMENTATIONKEY</span><span class="sxs-lookup"><span data-stu-id="6bddd-109">APPINSIGHTS_INSTRUMENTATIONKEY</span></span>

<span data-ttu-id="6bddd-110">The Application Insights instrumentation key if you're using Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6bddd-110">The Application Insights instrumentation key if you're using Application Insights.</span></span> <span data-ttu-id="6bddd-111">See [Monitor Azure Functions](functions-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="6bddd-111">See [Monitor Azure Functions](functions-monitoring.md).</span></span>

|<span data-ttu-id="6bddd-112">Key</span><span class="sxs-lookup"><span data-stu-id="6bddd-112">Key</span></span>|<span data-ttu-id="6bddd-113">Sample value</span><span class="sxs-lookup"><span data-stu-id="6bddd-113">Sample value</span></span>|
|---|------------|
|<span data-ttu-id="6bddd-114">APPINSIGHTS_INSTRUMENTATIONKEY</span><span class="sxs-lookup"><span data-stu-id="6bddd-114">APPINSIGHTS_INSTRUMENTATIONKEY</span></span>|<span data-ttu-id="6bddd-115">5dbdd5e9-af77-484b-9032-64f83bb83bb</span><span class="sxs-lookup"><span data-stu-id="6bddd-115">5dbdd5e9-af77-484b-9032-64f83bb83bb</span></span>|

## <a name="azurewebjobsdashboard"></a><span data-ttu-id="6bddd-116">AzureWebJobsDashboard</span><span class="sxs-lookup"><span data-stu-id="6bddd-116">AzureWebJobsDashboard</span></span>

<span data-ttu-id="6bddd-117">Optional storage account connection string for storing logs and displaying them in the **Monitor** tab in the portal.</span><span class="sxs-lookup"><span data-stu-id="6bddd-117">Optional storage account connection string for storing logs and displaying them in the **Monitor** tab in the portal.</span></span> <span data-ttu-id="6bddd-118">The storage account must be a general-purpose one that supports blobs, queues, and tables.</span><span class="sxs-lookup"><span data-stu-id="6bddd-118">The storage account must be a general-purpose one that supports blobs, queues, and tables.</span></span> <span data-ttu-id="6bddd-119">See [Storage account](functions-infrastructure-as-code.md#storage-account) and [Storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="6bddd-119">See [Storage account](functions-infrastructure-as-code.md#storage-account) and [Storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

|<span data-ttu-id="6bddd-120">Key</span><span class="sxs-lookup"><span data-stu-id="6bddd-120">Key</span></span>|<span data-ttu-id="6bddd-121">Sample value</span><span class="sxs-lookup"><span data-stu-id="6bddd-121">Sample value</span></span>|
|---|------------|
|<span data-ttu-id="6bddd-122">AzureWebJobsDashboard</span><span class="sxs-lookup"><span data-stu-id="6bddd-122">AzureWebJobsDashboard</span></span>|<span data-ttu-id="6bddd-123">DefaultEndpointsProtocol=https;AccountName=[name];AccountKey=[key]</span><span class="sxs-lookup"><span data-stu-id="6bddd-123">DefaultEndpointsProtocol=https;AccountName=[name];AccountKey=[key]</span></span>|

## <a name="azurewebjobsdisablehomepage"></a><span data-ttu-id="6bddd-124">AzureWebJobsDisableHomepage</span><span class="sxs-lookup"><span data-stu-id="6bddd-124">AzureWebJobsDisableHomepage</span></span>

<span data-ttu-id="6bddd-125">`true` means disable the default landing page that is shown for the root URL of a function app.</span><span class="sxs-lookup"><span data-stu-id="6bddd-125">`true` means disable the default landing page that is shown for the root URL of a function app.</span></span> <span data-ttu-id="6bddd-126">Default is `false`.</span><span class="sxs-lookup"><span data-stu-id="6bddd-126">Default is `false`.</span></span>

|<span data-ttu-id="6bddd-127">Key</span><span class="sxs-lookup"><span data-stu-id="6bddd-127">Key</span></span>|<span data-ttu-id="6bddd-128">Sample value</span><span class="sxs-lookup"><span data-stu-id="6bddd-128">Sample value</span></span>|
|---|------------|
|<span data-ttu-id="6bddd-129">AzureWebJobsDisableHomepage</span><span class="sxs-lookup"><span data-stu-id="6bddd-129">AzureWebJobsDisableHomepage</span></span>|<span data-ttu-id="6bddd-130">true</span><span class="sxs-lookup"><span data-stu-id="6bddd-130">true</span></span>|

<span data-ttu-id="6bddd-131">When this app setting is omitted or set to `false`, a page similar to the following example is displayed in response to the URL `<functionappname>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="6bddd-131">When this app setting is omitted or set to `false`, a page similar to the following example is displayed in response to the URL `<functionappname>.azurewebsites.net`.</span></span>

![Function app landing page](media/functions-app-settings/function-app-landing-page.png)

## <a name="azurewebjobsdotnetreleasecompilation"></a><span data-ttu-id="6bddd-133">AzureWebJobsDotNetReleaseCompilation</span><span class="sxs-lookup"><span data-stu-id="6bddd-133">AzureWebJobsDotNetReleaseCompilation</span></span>

<span data-ttu-id="6bddd-134">`true` means use Release mode when compiling .NET code; `false` means use Debug mode.</span><span class="sxs-lookup"><span data-stu-id="6bddd-134">`true` means use Release mode when compiling .NET code; `false` means use Debug mode.</span></span> <span data-ttu-id="6bddd-135">Default is `true`.</span><span class="sxs-lookup"><span data-stu-id="6bddd-135">Default is `true`.</span></span>

|<span data-ttu-id="6bddd-136">Key</span><span class="sxs-lookup"><span data-stu-id="6bddd-136">Key</span></span>|<span data-ttu-id="6bddd-137">Sample value</span><span class="sxs-lookup"><span data-stu-id="6bddd-137">Sample value</span></span>|
|---|------------|
|<span data-ttu-id="6bddd-138">AzureWebJobsDotNetReleaseCompilation</span><span class="sxs-lookup"><span data-stu-id="6bddd-138">AzureWebJobsDotNetReleaseCompilation</span></span>|<span data-ttu-id="6bddd-139">true</span><span class="sxs-lookup"><span data-stu-id="6bddd-139">true</span></span>|

## <a name="azurewebjobsfeatureflags"></a><span data-ttu-id="6bddd-140">AzureWebJobsFeatureFlags</span><span class="sxs-lookup"><span data-stu-id="6bddd-140">AzureWebJobsFeatureFlags</span></span>

<span data-ttu-id="6bddd-141">A comma-delimited list of beta features to enable.</span><span class="sxs-lookup"><span data-stu-id="6bddd-141">A comma-delimited list of beta features to enable.</span></span> <span data-ttu-id="6bddd-142">Beta features enabled by these flags are not production ready, but can be enabled for experimental use before they go live.</span><span class="sxs-lookup"><span data-stu-id="6bddd-142">Beta features enabled by these flags are not production ready, but can be enabled for experimental use before they go live.</span></span>

|<span data-ttu-id="6bddd-143">Key</span><span class="sxs-lookup"><span data-stu-id="6bddd-143">Key</span></span>|<span data-ttu-id="6bddd-144">Sample value</span><span class="sxs-lookup"><span data-stu-id="6bddd-144">Sample value</span></span>|
|---|------------|
|<span data-ttu-id="6bddd-145">AzureWebJobsFeatureFlags</span><span class="sxs-lookup"><span data-stu-id="6bddd-145">AzureWebJobsFeatureFlags</span></span>|<span data-ttu-id="6bddd-146">feature1,feature2</span><span class="sxs-lookup"><span data-stu-id="6bddd-146">feature1,feature2</span></span>|

## <a name="azurewebjobsscriptroot"></a><span data-ttu-id="6bddd-147">AzureWebJobsScriptRoot</span><span class="sxs-lookup"><span data-stu-id="6bddd-147">AzureWebJobsScriptRoot</span></span>

<span data-ttu-id="6bddd-148">The path to the root directory where the *host.json* file and function folders are located.</span><span class="sxs-lookup"><span data-stu-id="6bddd-148">The path to the root directory where the *host.json* file and function folders are located.</span></span> <span data-ttu-id="6bddd-149">In a function app, the default is `%HOME%\site\wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="6bddd-149">In a function app, the default is `%HOME%\site\wwwroot`.</span></span>

|<span data-ttu-id="6bddd-150">Key</span><span class="sxs-lookup"><span data-stu-id="6bddd-150">Key</span></span>|<span data-ttu-id="6bddd-151">Sample value</span><span class="sxs-lookup"><span data-stu-id="6bddd-151">Sample value</span></span>|
|---|------------|
|<span data-ttu-id="6bddd-152">AzureWebJobsScriptRoot</span><span class="sxs-lookup"><span data-stu-id="6bddd-152">AzureWebJobsScriptRoot</span></span>|<span data-ttu-id="6bddd-153">%HOME%\site\wwwroot</span><span class="sxs-lookup"><span data-stu-id="6bddd-153">%HOME%\site\wwwroot</span></span>|

## <a name="azurewebjobssecretstoragetype"></a><span data-ttu-id="6bddd-154">AzureWebJobsSecretStorageType</span><span class="sxs-lookup"><span data-stu-id="6bddd-154">AzureWebJobsSecretStorageType</span></span>

<span data-ttu-id="6bddd-155">Specifies the repository or provider to use for key storage.</span><span class="sxs-lookup"><span data-stu-id="6bddd-155">Specifies the repository or provider to use for key storage.</span></span> <span data-ttu-id="6bddd-156">Currently, the supported repositories are blob ("Blob") and file system ("disabled").</span><span class="sxs-lookup"><span data-stu-id="6bddd-156">Currently, the supported repositories are blob ("Blob") and file system ("disabled").</span></span> <span data-ttu-id="6bddd-157">The default is file system ("disabled").</span><span class="sxs-lookup"><span data-stu-id="6bddd-157">The default is file system ("disabled").</span></span>

|<span data-ttu-id="6bddd-158">Key</span><span class="sxs-lookup"><span data-stu-id="6bddd-158">Key</span></span>|<span data-ttu-id="6bddd-159">Sample value</span><span class="sxs-lookup"><span data-stu-id="6bddd-159">Sample value</span></span>|
|---|------------|
|<span data-ttu-id="6bddd-160">AzureWebJobsSecretStorageType</span><span class="sxs-lookup"><span data-stu-id="6bddd-160">AzureWebJobsSecretStorageType</span></span>|<span data-ttu-id="6bddd-161">disabled</span><span class="sxs-lookup"><span data-stu-id="6bddd-161">disabled</span></span>|

## <a name="azurewebjobsstorage"></a><span data-ttu-id="6bddd-162">AzureWebJobsStorage</span><span class="sxs-lookup"><span data-stu-id="6bddd-162">AzureWebJobsStorage</span></span>

<span data-ttu-id="6bddd-163">The Azure Functions runtime uses this storage account connection string for all functions except for HTTP triggered functions.</span><span class="sxs-lookup"><span data-stu-id="6bddd-163">The Azure Functions runtime uses this storage account connection string for all functions except for HTTP triggered functions.</span></span> <span data-ttu-id="6bddd-164">The storage account must be a general-purpose one that supports blobs, queues, and tables.</span><span class="sxs-lookup"><span data-stu-id="6bddd-164">The storage account must be a general-purpose one that supports blobs, queues, and tables.</span></span> <span data-ttu-id="6bddd-165">See [Storage account](functions-infrastructure-as-code.md#storage-account) and [Storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="6bddd-165">See [Storage account](functions-infrastructure-as-code.md#storage-account) and [Storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

|<span data-ttu-id="6bddd-166">Key</span><span class="sxs-lookup"><span data-stu-id="6bddd-166">Key</span></span>|<span data-ttu-id="6bddd-167">Sample value</span><span class="sxs-lookup"><span data-stu-id="6bddd-167">Sample value</span></span>|
|---|------------|
|<span data-ttu-id="6bddd-168">AzureWebJobsStorage</span><span class="sxs-lookup"><span data-stu-id="6bddd-168">AzureWebJobsStorage</span></span>|<span data-ttu-id="6bddd-169">DefaultEndpointsProtocol=https;AccountName=[name];AccountKey=[key]</span><span class="sxs-lookup"><span data-stu-id="6bddd-169">DefaultEndpointsProtocol=https;AccountName=[name];AccountKey=[key]</span></span>|

## <a name="azurewebjobstypescriptpath"></a><span data-ttu-id="6bddd-170">AzureWebJobs_TypeScriptPath</span><span class="sxs-lookup"><span data-stu-id="6bddd-170">AzureWebJobs_TypeScriptPath</span></span>

<span data-ttu-id="6bddd-171">Path to the compiler used for TypeScript.</span><span class="sxs-lookup"><span data-stu-id="6bddd-171">Path to the compiler used for TypeScript.</span></span> <span data-ttu-id="6bddd-172">Allows you to override the default if you need to.</span><span class="sxs-lookup"><span data-stu-id="6bddd-172">Allows you to override the default if you need to.</span></span>

|<span data-ttu-id="6bddd-173">Key</span><span class="sxs-lookup"><span data-stu-id="6bddd-173">Key</span></span>|<span data-ttu-id="6bddd-174">Sample value</span><span class="sxs-lookup"><span data-stu-id="6bddd-174">Sample value</span></span>|
|---|------------|
|<span data-ttu-id="6bddd-175">AzureWebJobs_TypeScriptPath</span><span class="sxs-lookup"><span data-stu-id="6bddd-175">AzureWebJobs_TypeScriptPath</span></span>|<span data-ttu-id="6bddd-176">%HOME%\typescript</span><span class="sxs-lookup"><span data-stu-id="6bddd-176">%HOME%\typescript</span></span>|

## <a name="functionappeditmode"></a><span data-ttu-id="6bddd-177">FUNCTION\_APP\_EDIT\_MODE</span><span class="sxs-lookup"><span data-stu-id="6bddd-177">FUNCTION\_APP\_EDIT\_MODE</span></span>

<span data-ttu-id="6bddd-178">Valid values are "readwrite" and "readonly".</span><span class="sxs-lookup"><span data-stu-id="6bddd-178">Valid values are "readwrite" and "readonly".</span></span>

|<span data-ttu-id="6bddd-179">Key</span><span class="sxs-lookup"><span data-stu-id="6bddd-179">Key</span></span>|<span data-ttu-id="6bddd-180">Sample value</span><span class="sxs-lookup"><span data-stu-id="6bddd-180">Sample value</span></span>|
|---|------------|
|<span data-ttu-id="6bddd-181">FUNCTION\_APP\_EDIT\_MODE</span><span class="sxs-lookup"><span data-stu-id="6bddd-181">FUNCTION\_APP\_EDIT\_MODE</span></span>|<span data-ttu-id="6bddd-182">readonly</span><span class="sxs-lookup"><span data-stu-id="6bddd-182">readonly</span></span>|

## <a name="functionsextensionversion"></a><span data-ttu-id="6bddd-183">FUNCTIONS\_EXTENSION\_VERSION</span><span class="sxs-lookup"><span data-stu-id="6bddd-183">FUNCTIONS\_EXTENSION\_VERSION</span></span>

<span data-ttu-id="6bddd-184">The version of the Azure Functions runtime to use in this function app.</span><span class="sxs-lookup"><span data-stu-id="6bddd-184">The version of the Azure Functions runtime to use in this function app.</span></span> <span data-ttu-id="6bddd-185">A tilde with major version means use the latest version of that major version (for example, "~1").</span><span class="sxs-lookup"><span data-stu-id="6bddd-185">A tilde with major version means use the latest version of that major version (for example, "~1").</span></span> <span data-ttu-id="6bddd-186">When new versions for the same major version are available, they are automatically installed in the function app.</span><span class="sxs-lookup"><span data-stu-id="6bddd-186">When new versions for the same major version are available, they are automatically installed in the function app.</span></span> <span data-ttu-id="6bddd-187">To pin the app to a specific version, use the full version number (for example, "1.0.12345").</span><span class="sxs-lookup"><span data-stu-id="6bddd-187">To pin the app to a specific version, use the full version number (for example, "1.0.12345").</span></span> <span data-ttu-id="6bddd-188">Default is "~1".</span><span class="sxs-lookup"><span data-stu-id="6bddd-188">Default is "~1".</span></span>

|<span data-ttu-id="6bddd-189">Key</span><span class="sxs-lookup"><span data-stu-id="6bddd-189">Key</span></span>|<span data-ttu-id="6bddd-190">Sample value</span><span class="sxs-lookup"><span data-stu-id="6bddd-190">Sample value</span></span>|
|---|------------|
|<span data-ttu-id="6bddd-191">FUNCTIONS\_EXTENSION\_VERSION</span><span class="sxs-lookup"><span data-stu-id="6bddd-191">FUNCTIONS\_EXTENSION\_VERSION</span></span>|<span data-ttu-id="6bddd-192">~1</span><span class="sxs-lookup"><span data-stu-id="6bddd-192">~1</span></span>|

## <a name="websitecontentazurefileconnectionstring"></a><span data-ttu-id="6bddd-193">WEBSITE_CONTENTAZUREFILECONNECTIONSTRING</span><span class="sxs-lookup"><span data-stu-id="6bddd-193">WEBSITE_CONTENTAZUREFILECONNECTIONSTRING</span></span>

<span data-ttu-id="6bddd-194">For consumption plans only.</span><span class="sxs-lookup"><span data-stu-id="6bddd-194">For consumption plans only.</span></span> <span data-ttu-id="6bddd-195">Connection string for storage account where the function app code and configuration are stored.</span><span class="sxs-lookup"><span data-stu-id="6bddd-195">Connection string for storage account where the function app code and configuration are stored.</span></span> <span data-ttu-id="6bddd-196">See [Create a function app](functions-infrastructure-as-code.md#create-a-function-app).</span><span class="sxs-lookup"><span data-stu-id="6bddd-196">See [Create a function app](functions-infrastructure-as-code.md#create-a-function-app).</span></span>

|<span data-ttu-id="6bddd-197">Key</span><span class="sxs-lookup"><span data-stu-id="6bddd-197">Key</span></span>|<span data-ttu-id="6bddd-198">Sample value</span><span class="sxs-lookup"><span data-stu-id="6bddd-198">Sample value</span></span>|
|---|------------|
|<span data-ttu-id="6bddd-199">WEBSITE_CONTENTAZUREFILECONNECTIONSTRING</span><span class="sxs-lookup"><span data-stu-id="6bddd-199">WEBSITE_CONTENTAZUREFILECONNECTIONSTRING</span></span>|<span data-ttu-id="6bddd-200">DefaultEndpointsProtocol=https;AccountName=[name];AccountKey=[key]</span><span class="sxs-lookup"><span data-stu-id="6bddd-200">DefaultEndpointsProtocol=https;AccountName=[name];AccountKey=[key]</span></span>|

## <a name="websitecontentshare"></a><span data-ttu-id="6bddd-201">WEBSITE\_CONTENTSHARE</span><span class="sxs-lookup"><span data-stu-id="6bddd-201">WEBSITE\_CONTENTSHARE</span></span>

<span data-ttu-id="6bddd-202">For consumption plans only.</span><span class="sxs-lookup"><span data-stu-id="6bddd-202">For consumption plans only.</span></span> <span data-ttu-id="6bddd-203">The file path to the function app code and configuration.</span><span class="sxs-lookup"><span data-stu-id="6bddd-203">The file path to the function app code and configuration.</span></span> <span data-ttu-id="6bddd-204">Used with WEBSITE_CONTENTAZUREFILECONNECTIONSTRING.</span><span class="sxs-lookup"><span data-stu-id="6bddd-204">Used with WEBSITE_CONTENTAZUREFILECONNECTIONSTRING.</span></span> <span data-ttu-id="6bddd-205">Default is a unique string that begins with the function app name.</span><span class="sxs-lookup"><span data-stu-id="6bddd-205">Default is a unique string that begins with the function app name.</span></span> <span data-ttu-id="6bddd-206">See [Create a function app](functions-infrastructure-as-code.md#create-a-function-app).</span><span class="sxs-lookup"><span data-stu-id="6bddd-206">See [Create a function app](functions-infrastructure-as-code.md#create-a-function-app).</span></span>

|<span data-ttu-id="6bddd-207">Key</span><span class="sxs-lookup"><span data-stu-id="6bddd-207">Key</span></span>|<span data-ttu-id="6bddd-208">Sample value</span><span class="sxs-lookup"><span data-stu-id="6bddd-208">Sample value</span></span>|
|---|------------|
|<span data-ttu-id="6bddd-209">WEBSITE_CONTENTSHARE</span><span class="sxs-lookup"><span data-stu-id="6bddd-209">WEBSITE_CONTENTSHARE</span></span>|<span data-ttu-id="6bddd-210">functionapp091999e2</span><span class="sxs-lookup"><span data-stu-id="6bddd-210">functionapp091999e2</span></span>|

## <a name="websitemaxdynamicapplicationscaleout"></a><span data-ttu-id="6bddd-211">WEBSITE\_MAX\_DYNAMIC\_APPLICATION\_SCALE\_OUT</span><span class="sxs-lookup"><span data-stu-id="6bddd-211">WEBSITE\_MAX\_DYNAMIC\_APPLICATION\_SCALE\_OUT</span></span>

<span data-ttu-id="6bddd-212">The maximum number of instances that the function app can scale out to.</span><span class="sxs-lookup"><span data-stu-id="6bddd-212">The maximum number of instances that the function app can scale out to.</span></span> <span data-ttu-id="6bddd-213">Default is no limit.</span><span class="sxs-lookup"><span data-stu-id="6bddd-213">Default is no limit.</span></span>

> [!NOTE]
> <span data-ttu-id="6bddd-214">This setting is for a preview feature.</span><span class="sxs-lookup"><span data-stu-id="6bddd-214">This setting is for a preview feature.</span></span>

|<span data-ttu-id="6bddd-215">Key</span><span class="sxs-lookup"><span data-stu-id="6bddd-215">Key</span></span>|<span data-ttu-id="6bddd-216">Sample value</span><span class="sxs-lookup"><span data-stu-id="6bddd-216">Sample value</span></span>|
|---|------------|
|<span data-ttu-id="6bddd-217">WEBSITE\_MAX\_DYNAMIC\_APPLICATION\_SCALE\_OUT</span><span class="sxs-lookup"><span data-stu-id="6bddd-217">WEBSITE\_MAX\_DYNAMIC\_APPLICATION\_SCALE\_OUT</span></span>|<span data-ttu-id="6bddd-218">10</span><span class="sxs-lookup"><span data-stu-id="6bddd-218">10</span></span>|

## <a name="websitenodedefaultversion"></a><span data-ttu-id="6bddd-219">WEBSITE\_NODE\_DEFAULT_VERSION</span><span class="sxs-lookup"><span data-stu-id="6bddd-219">WEBSITE\_NODE\_DEFAULT_VERSION</span></span>

<span data-ttu-id="6bddd-220">Default is "6.5.0".</span><span class="sxs-lookup"><span data-stu-id="6bddd-220">Default is "6.5.0".</span></span>

|<span data-ttu-id="6bddd-221">Key</span><span class="sxs-lookup"><span data-stu-id="6bddd-221">Key</span></span>|<span data-ttu-id="6bddd-222">Sample value</span><span class="sxs-lookup"><span data-stu-id="6bddd-222">Sample value</span></span>|
|---|------------|
|<span data-ttu-id="6bddd-223">WEBSITE\_NODE\_DEFAULT_VERSION</span><span class="sxs-lookup"><span data-stu-id="6bddd-223">WEBSITE\_NODE\_DEFAULT_VERSION</span></span>|<span data-ttu-id="6bddd-224">6.5.0</span><span class="sxs-lookup"><span data-stu-id="6bddd-224">6.5.0</span></span>|

## <a name="websiterunfromzip"></a><span data-ttu-id="6bddd-225">WEBSITE\_RUN\_FROM\_ZIP</span><span class="sxs-lookup"><span data-stu-id="6bddd-225">WEBSITE\_RUN\_FROM\_ZIP</span></span>

<span data-ttu-id="6bddd-226">Enables your function app to run from a mounted package file.</span><span class="sxs-lookup"><span data-stu-id="6bddd-226">Enables your function app to run from a mounted package file.</span></span>

> [!NOTE]
> <span data-ttu-id="6bddd-227">This setting is for a preview feature.</span><span class="sxs-lookup"><span data-stu-id="6bddd-227">This setting is for a preview feature.</span></span>

|<span data-ttu-id="6bddd-228">Key</span><span class="sxs-lookup"><span data-stu-id="6bddd-228">Key</span></span>|<span data-ttu-id="6bddd-229">Sample value</span><span class="sxs-lookup"><span data-stu-id="6bddd-229">Sample value</span></span>|
|---|------------|
|<span data-ttu-id="6bddd-230">WEBSITE\_RUN\_FROM\_ZIP</span><span class="sxs-lookup"><span data-stu-id="6bddd-230">WEBSITE\_RUN\_FROM\_ZIP</span></span>|<span data-ttu-id="6bddd-231">1</span><span class="sxs-lookup"><span data-stu-id="6bddd-231">1</span></span>|

<span data-ttu-id="6bddd-232">Valid values are either a URL that resolves to the location of a deployment package file, or `1`.</span><span class="sxs-lookup"><span data-stu-id="6bddd-232">Valid values are either a URL that resolves to the location of a deployment package file, or `1`.</span></span> <span data-ttu-id="6bddd-233">When set to `1`, the package must be in the `d:\home\data\SitePackages` folder.</span><span class="sxs-lookup"><span data-stu-id="6bddd-233">When set to `1`, the package must be in the `d:\home\data\SitePackages` folder.</span></span> <span data-ttu-id="6bddd-234">When using zip deployment with this setting, the package is automatically uploaded to this location.</span><span class="sxs-lookup"><span data-stu-id="6bddd-234">When using zip deployment with this setting, the package is automatically uploaded to this location.</span></span>  <span data-ttu-id="6bddd-235">For more information, see [Run your functions from a package file](run-functions-from-deployment-package.md).</span><span class="sxs-lookup"><span data-stu-id="6bddd-235">For more information, see [Run your functions from a package file](run-functions-from-deployment-package.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bddd-236">Next steps</span><span class="sxs-lookup"><span data-stu-id="6bddd-236">Next steps</span></span>

[<span data-ttu-id="6bddd-237">Learn how to update app settings</span><span class="sxs-lookup"><span data-stu-id="6bddd-237">Learn how to update app settings</span></span>](functions-how-to-use-azure-function-app-settings.md#manage-app-service-settings)

[<span data-ttu-id="6bddd-238">See global settings in the host.json file</span><span class="sxs-lookup"><span data-stu-id="6bddd-238">See global settings in the host.json file</span></span>](functions-host-json.md)

[<span data-ttu-id="6bddd-239">See other app settings for App Service apps</span><span class="sxs-lookup"><span data-stu-id="6bddd-239">See other app settings for App Service apps</span></span>](https://github.com/projectkudu/kudu/wiki/Configurable-settings)
