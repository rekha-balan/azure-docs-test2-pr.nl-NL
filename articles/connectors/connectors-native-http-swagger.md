---
title: Call REST endpoints with HTTP + Swagger connector for Azure Logic Apps | Microsoft Docs
description: Connect to REST endpoints from logic apps through Swagger with the HTTP + Swagger connector
services: logic-apps
author: jeffhollan
manager: anneta
editor: ''
documentationcenter: ''
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 9925172cb096bc2cd06d89ab62e19e5e31d30800
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562821"
---
# <a name="get-started-with-the-http--swagger-action"></a><span data-ttu-id="80a94-103">Get started with the HTTP + Swagger action</span><span class="sxs-lookup"><span data-stu-id="80a94-103">Get started with the HTTP + Swagger action</span></span>

<span data-ttu-id="80a94-104">You can create a first-class connector to any REST endpoint through a [Swagger document](https://swagger.io) when you use the HTTP + Swagger action in your logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="80a94-104">You can create a first-class connector to any REST endpoint through a [Swagger document](https://swagger.io) when you use the HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="80a94-105">You can also extend logic apps to call any REST endpoint with a first-class Logic App Designer experience.</span><span class="sxs-lookup"><span data-stu-id="80a94-105">You can also extend logic apps to call any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="80a94-106">To learn how to create logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="80a94-106">To learn how to create logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="80a94-107">Use HTTP + Swagger as a trigger or an action</span><span class="sxs-lookup"><span data-stu-id="80a94-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="80a94-108">The HTTP + Swagger trigger and action work the same as the [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing the API structure and outputs from the [Swagger metadata](https://swagger.io).</span><span class="sxs-lookup"><span data-stu-id="80a94-108">The HTTP + Swagger trigger and action work the same as the [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing the API structure and outputs from the [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="80a94-109">You can also use the HTTP + Swagger connector as a trigger.</span><span class="sxs-lookup"><span data-stu-id="80a94-109">You can also use the HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="80a94-110">If you want to implement a polling trigger, follow the polling pattern that's described in [Create custom APIs to call other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span><span class="sxs-lookup"><span data-stu-id="80a94-110">If you want to implement a polling trigger, follow the polling pattern that's described in [Create custom APIs to call other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="80a94-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="80a94-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="80a94-112">Here's an example of how to use the HTTP + Swagger operation as an action in a workflow in a logic app.</span><span class="sxs-lookup"><span data-stu-id="80a94-112">Here's an example of how to use the HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="80a94-113">Select the **New Step** button.</span><span class="sxs-lookup"><span data-stu-id="80a94-113">Select the **New Step** button.</span></span>
2. <span data-ttu-id="80a94-114">Select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="80a94-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="80a94-115">In the action search box, type **swagger** to list the HTTP + Swagger action.</span><span class="sxs-lookup"><span data-stu-id="80a94-115">In the action search box, type **swagger** to list the HTTP + Swagger action.</span></span>
   
    ![Select HTTP + Swagger action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="80a94-117">Type the URL for a Swagger document:</span><span class="sxs-lookup"><span data-stu-id="80a94-117">Type the URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="80a94-118">To work from the Logic App Designer, the URL must be an HTTPS endpoint and have CORS enabled.</span><span class="sxs-lookup"><span data-stu-id="80a94-118">To work from the Logic App Designer, the URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="80a94-119">If the Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) to store the document.</span><span class="sxs-lookup"><span data-stu-id="80a94-119">If the Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) to store the document.</span></span>
5. <span data-ttu-id="80a94-120">Click **Next** to read and render from the Swagger document.</span><span class="sxs-lookup"><span data-stu-id="80a94-120">Click **Next** to read and render from the Swagger document.</span></span>
6. <span data-ttu-id="80a94-121">Add in any parameters that are required for the HTTP call.</span><span class="sxs-lookup"><span data-stu-id="80a94-121">Add in any parameters that are required for the HTTP call.</span></span>
   
    ![Complete HTTP action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="80a94-123">To save and publish your logic app, click **Save** on designer toolbar.</span><span class="sxs-lookup"><span data-stu-id="80a94-123">To save and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="80a94-124">Host Swagger from Azure Storage</span><span class="sxs-lookup"><span data-stu-id="80a94-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="80a94-125">You might want to reference a Swagger document that's not hosted, or that doesn't meet the security and cross-origin requirements for the designer.</span><span class="sxs-lookup"><span data-stu-id="80a94-125">You might want to reference a Swagger document that's not hosted, or that doesn't meet the security and cross-origin requirements for the designer.</span></span> <span data-ttu-id="80a94-126">To resolve this issue, you can store the Swagger document in Azure Storage and enable CORS to reference the document.</span><span class="sxs-lookup"><span data-stu-id="80a94-126">To resolve this issue, you can store the Swagger document in Azure Storage and enable CORS to reference the document.</span></span>  

<span data-ttu-id="80a94-127">Here are the steps to create, configure, and store Swagger documents in Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="80a94-127">Here are the steps to create, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="80a94-128">[Create an Azure storage account with Azure Blob storage](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="80a94-128">[Create an Azure storage account with Azure Blob storage](../storage/storage-create-storage-account.md).</span></span> <span data-ttu-id="80a94-129">To perform this step, set permissions to **Public Access**.</span><span class="sxs-lookup"><span data-stu-id="80a94-129">To perform this step, set permissions to **Public Access**.</span></span>

2. <span data-ttu-id="80a94-130">Enable CORS on the blob.</span><span class="sxs-lookup"><span data-stu-id="80a94-130">Enable CORS on the blob.</span></span> 

   <span data-ttu-id="80a94-131">To automatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span><span class="sxs-lookup"><span data-stu-id="80a94-131">To automatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="80a94-132">Upload the Swagger file to the blob.</span><span class="sxs-lookup"><span data-stu-id="80a94-132">Upload the Swagger file to the blob.</span></span> 

   <span data-ttu-id="80a94-133">You can perform this step from the [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="80a94-133">You can perform this step from the [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="80a94-134">Reference an HTTPS link to the document in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="80a94-134">Reference an HTTPS link to the document in Azure Blob storage.</span></span> 

   <span data-ttu-id="80a94-135">The link uses this format:</span><span class="sxs-lookup"><span data-stu-id="80a94-135">The link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="80a94-136">Technical details</span><span class="sxs-lookup"><span data-stu-id="80a94-136">Technical details</span></span>
<span data-ttu-id="80a94-137">Following are the details for the triggers and actions that this HTTP + Swagger connector supports.</span><span class="sxs-lookup"><span data-stu-id="80a94-137">Following are the details for the triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="80a94-138">HTTP + Swagger triggers</span><span class="sxs-lookup"><span data-stu-id="80a94-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="80a94-139">A trigger is an event that can be used to start the workflow that's defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="80a94-139">A trigger is an event that can be used to start the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="80a94-140">Learn more about triggers.</span><span class="sxs-lookup"><span data-stu-id="80a94-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="80a94-141">The HTTP + Swagger connector has one trigger.</span><span class="sxs-lookup"><span data-stu-id="80a94-141">The HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="80a94-142">Trigger</span><span class="sxs-lookup"><span data-stu-id="80a94-142">Trigger</span></span> | <span data-ttu-id="80a94-143">Description</span><span class="sxs-lookup"><span data-stu-id="80a94-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="80a94-144">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="80a94-144">HTTP + Swagger</span></span> |<span data-ttu-id="80a94-145">Make an HTTP call and return the response content</span><span class="sxs-lookup"><span data-stu-id="80a94-145">Make an HTTP call and return the response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="80a94-146">HTTP + Swagger actions</span><span class="sxs-lookup"><span data-stu-id="80a94-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="80a94-147">An action is an operation that's carried out by the workflow that's defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="80a94-147">An action is an operation that's carried out by the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="80a94-148">Learn more about actions.</span><span class="sxs-lookup"><span data-stu-id="80a94-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="80a94-149">The HTTP + Swagger connector has one possible action.</span><span class="sxs-lookup"><span data-stu-id="80a94-149">The HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="80a94-150">Action</span><span class="sxs-lookup"><span data-stu-id="80a94-150">Action</span></span> | <span data-ttu-id="80a94-151">Description</span><span class="sxs-lookup"><span data-stu-id="80a94-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="80a94-152">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="80a94-152">HTTP + Swagger</span></span> |<span data-ttu-id="80a94-153">Make an HTTP call and return the response content</span><span class="sxs-lookup"><span data-stu-id="80a94-153">Make an HTTP call and return the response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="80a94-154">Action details</span><span class="sxs-lookup"><span data-stu-id="80a94-154">Action details</span></span>
<span data-ttu-id="80a94-155">The HTTP + Swagger connector comes with one possible action.</span><span class="sxs-lookup"><span data-stu-id="80a94-155">The HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="80a94-156">Following is information about each of the actions, their required and optional input fields, and the corresponding output details that are associated with their usage.</span><span class="sxs-lookup"><span data-stu-id="80a94-156">Following is information about each of the actions, their required and optional input fields, and the corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="80a94-157">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="80a94-157">HTTP + Swagger</span></span>
<span data-ttu-id="80a94-158">Make an HTTP outbound request with assistance of Swagger metadata.</span><span class="sxs-lookup"><span data-stu-id="80a94-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="80a94-159">An asterisk (\*) means a required field.</span><span class="sxs-lookup"><span data-stu-id="80a94-159">An asterisk (\*) means a required field.</span></span>

| <span data-ttu-id="80a94-160">Display name</span><span class="sxs-lookup"><span data-stu-id="80a94-160">Display name</span></span> | <span data-ttu-id="80a94-161">Property name</span><span class="sxs-lookup"><span data-stu-id="80a94-161">Property name</span></span> | <span data-ttu-id="80a94-162">Description</span><span class="sxs-lookup"><span data-stu-id="80a94-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="80a94-163">Method\*</span><span class="sxs-lookup"><span data-stu-id="80a94-163">Method\*</span></span> |<span data-ttu-id="80a94-164">method</span><span class="sxs-lookup"><span data-stu-id="80a94-164">method</span></span> |<span data-ttu-id="80a94-165">HTTP verb to use.</span><span class="sxs-lookup"><span data-stu-id="80a94-165">HTTP verb to use.</span></span> |
| <span data-ttu-id="80a94-166">URI\*</span><span class="sxs-lookup"><span data-stu-id="80a94-166">URI\*</span></span> |<span data-ttu-id="80a94-167">uri</span><span class="sxs-lookup"><span data-stu-id="80a94-167">uri</span></span> |<span data-ttu-id="80a94-168">URI for the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="80a94-168">URI for the HTTP request.</span></span> |
| <span data-ttu-id="80a94-169">Headers</span><span class="sxs-lookup"><span data-stu-id="80a94-169">Headers</span></span> |<span data-ttu-id="80a94-170">headers</span><span class="sxs-lookup"><span data-stu-id="80a94-170">headers</span></span> |<span data-ttu-id="80a94-171">A JSON object of HTTP headers to include.</span><span class="sxs-lookup"><span data-stu-id="80a94-171">A JSON object of HTTP headers to include.</span></span> |
| <span data-ttu-id="80a94-172">Body</span><span class="sxs-lookup"><span data-stu-id="80a94-172">Body</span></span> |<span data-ttu-id="80a94-173">body</span><span class="sxs-lookup"><span data-stu-id="80a94-173">body</span></span> |<span data-ttu-id="80a94-174">The HTTP request body.</span><span class="sxs-lookup"><span data-stu-id="80a94-174">The HTTP request body.</span></span> |
| <span data-ttu-id="80a94-175">Authentication</span><span class="sxs-lookup"><span data-stu-id="80a94-175">Authentication</span></span> |<span data-ttu-id="80a94-176">authentication</span><span class="sxs-lookup"><span data-stu-id="80a94-176">authentication</span></span> |<span data-ttu-id="80a94-177">Authentication to use for request.</span><span class="sxs-lookup"><span data-stu-id="80a94-177">Authentication to use for request.</span></span> <span data-ttu-id="80a94-178">For more information, see the [HTTP connector](connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="80a94-178">For more information, see the [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="80a94-179">**Output details**</span><span class="sxs-lookup"><span data-stu-id="80a94-179">**Output details**</span></span>

<span data-ttu-id="80a94-180">HTTP response</span><span class="sxs-lookup"><span data-stu-id="80a94-180">HTTP response</span></span>

| <span data-ttu-id="80a94-181">Property Name</span><span class="sxs-lookup"><span data-stu-id="80a94-181">Property Name</span></span> | <span data-ttu-id="80a94-182">Data type</span><span class="sxs-lookup"><span data-stu-id="80a94-182">Data type</span></span> | <span data-ttu-id="80a94-183">Description</span><span class="sxs-lookup"><span data-stu-id="80a94-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="80a94-184">Headers</span><span class="sxs-lookup"><span data-stu-id="80a94-184">Headers</span></span> |<span data-ttu-id="80a94-185">object</span><span class="sxs-lookup"><span data-stu-id="80a94-185">object</span></span> |<span data-ttu-id="80a94-186">Response headers</span><span class="sxs-lookup"><span data-stu-id="80a94-186">Response headers</span></span> |
| <span data-ttu-id="80a94-187">Body</span><span class="sxs-lookup"><span data-stu-id="80a94-187">Body</span></span> |<span data-ttu-id="80a94-188">object</span><span class="sxs-lookup"><span data-stu-id="80a94-188">object</span></span> |<span data-ttu-id="80a94-189">Response object</span><span class="sxs-lookup"><span data-stu-id="80a94-189">Response object</span></span> |
| <span data-ttu-id="80a94-190">Status Code</span><span class="sxs-lookup"><span data-stu-id="80a94-190">Status Code</span></span> |<span data-ttu-id="80a94-191">int</span><span class="sxs-lookup"><span data-stu-id="80a94-191">int</span></span> |<span data-ttu-id="80a94-192">HTTP status code</span><span class="sxs-lookup"><span data-stu-id="80a94-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="80a94-193">HTTP responses</span><span class="sxs-lookup"><span data-stu-id="80a94-193">HTTP responses</span></span>
<span data-ttu-id="80a94-194">When making calls to various actions, you might get certain responses.</span><span class="sxs-lookup"><span data-stu-id="80a94-194">When making calls to various actions, you might get certain responses.</span></span> <span data-ttu-id="80a94-195">Following is a table that outlines corresponding responses and descriptions.</span><span class="sxs-lookup"><span data-stu-id="80a94-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="80a94-196">Name</span><span class="sxs-lookup"><span data-stu-id="80a94-196">Name</span></span> | <span data-ttu-id="80a94-197">Description</span><span class="sxs-lookup"><span data-stu-id="80a94-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="80a94-198">200</span><span class="sxs-lookup"><span data-stu-id="80a94-198">200</span></span> |<span data-ttu-id="80a94-199">OK</span><span class="sxs-lookup"><span data-stu-id="80a94-199">OK</span></span> |
| <span data-ttu-id="80a94-200">202</span><span class="sxs-lookup"><span data-stu-id="80a94-200">202</span></span> |<span data-ttu-id="80a94-201">Accepted</span><span class="sxs-lookup"><span data-stu-id="80a94-201">Accepted</span></span> |
| <span data-ttu-id="80a94-202">400</span><span class="sxs-lookup"><span data-stu-id="80a94-202">400</span></span> |<span data-ttu-id="80a94-203">Bad request</span><span class="sxs-lookup"><span data-stu-id="80a94-203">Bad request</span></span> |
| <span data-ttu-id="80a94-204">401</span><span class="sxs-lookup"><span data-stu-id="80a94-204">401</span></span> |<span data-ttu-id="80a94-205">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="80a94-205">Unauthorized</span></span> |
| <span data-ttu-id="80a94-206">403</span><span class="sxs-lookup"><span data-stu-id="80a94-206">403</span></span> |<span data-ttu-id="80a94-207">Forbidden</span><span class="sxs-lookup"><span data-stu-id="80a94-207">Forbidden</span></span> |
| <span data-ttu-id="80a94-208">404</span><span class="sxs-lookup"><span data-stu-id="80a94-208">404</span></span> |<span data-ttu-id="80a94-209">Not Found</span><span class="sxs-lookup"><span data-stu-id="80a94-209">Not Found</span></span> |
| <span data-ttu-id="80a94-210">500</span><span class="sxs-lookup"><span data-stu-id="80a94-210">500</span></span> |<span data-ttu-id="80a94-211">Internal server error.</span><span class="sxs-lookup"><span data-stu-id="80a94-211">Internal server error.</span></span> <span data-ttu-id="80a94-212">Unknown error occurred.</span><span class="sxs-lookup"><span data-stu-id="80a94-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="80a94-213">Next steps</span><span class="sxs-lookup"><span data-stu-id="80a94-213">Next steps</span></span>

* [<span data-ttu-id="80a94-214">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="80a94-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="80a94-215">Find other connectors</span><span class="sxs-lookup"><span data-stu-id="80a94-215">Find other connectors</span></span>](apis-list.md)

