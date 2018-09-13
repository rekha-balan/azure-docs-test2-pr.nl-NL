---
title: Learn how to use the SharePoint Online connector in logic apps | Microsoft Docs
description: Create logic apps with the SharePoint Online connector to mange lists on SharePoint.
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: e0ec3149-507a-409d-8e7b-d5fbded006ce
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/19/2016
ms.author: deonhe
ms.openlocfilehash: 3ecf3e30fe2fcb9d6473d7eda450536cddfa97f4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562741"
---
# <a name="get-started-with-the-sharepoint-online-connector"></a><span data-ttu-id="f1962-103">Get started with the SharePoint Online connector</span><span class="sxs-lookup"><span data-stu-id="f1962-103">Get started with the SharePoint Online connector</span></span>
<span data-ttu-id="f1962-104">Use the SharePoint Online connector to manage SharePoint lists.</span><span class="sxs-lookup"><span data-stu-id="f1962-104">Use the SharePoint Online connector to manage SharePoint lists.</span></span>  

<span data-ttu-id="f1962-105">To use [any connector](apis-list.md), you first need to create a logic app.</span><span class="sxs-lookup"><span data-stu-id="f1962-105">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="f1962-106">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f1962-106">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-sharepoint-online"></a><span data-ttu-id="f1962-107">Connect to SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f1962-107">Connect to SharePoint Online</span></span>
<span data-ttu-id="f1962-108">Before your logic app can access any service, you first need to create a *connection* to the service.</span><span class="sxs-lookup"><span data-stu-id="f1962-108">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="f1962-109">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span><span class="sxs-lookup"><span data-stu-id="f1962-109">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-sharepoint-online"></a><span data-ttu-id="f1962-110">Create a connection to SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f1962-110">Create a connection to SharePoint Online</span></span>
> [!INCLUDE [Steps to create a connection to SharePoint](../../includes/connectors-create-api-sharepointonline.md)]
> 
> 

## <a name="use-a-sharepoint-online-trigger"></a><span data-ttu-id="f1962-111">Use a SharePoint Online trigger</span><span class="sxs-lookup"><span data-stu-id="f1962-111">Use a SharePoint Online trigger</span></span>
<span data-ttu-id="f1962-112">A trigger is an event that can be used to start the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="f1962-112">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="f1962-113">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="f1962-113">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a SharePoint Online trigger](../../includes/connectors-create-api-sharepointonline-trigger.md)]
> 
> 

## <a name="use-a-sharepoint-online-action"></a><span data-ttu-id="f1962-114">Use a SharePoint Online action</span><span class="sxs-lookup"><span data-stu-id="f1962-114">Use a SharePoint Online action</span></span>
<span data-ttu-id="f1962-115">An action is an operation carried out by the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="f1962-115">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="f1962-116">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="f1962-116">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a SharePoint Online action](../../includes/connectors-create-api-sharepointonline-action.md)]
> 
> 

## <a name="technical-details"></a><span data-ttu-id="f1962-117">Technical Details</span><span class="sxs-lookup"><span data-stu-id="f1962-117">Technical Details</span></span>
<span data-ttu-id="f1962-118">Here are the details about the triggers, actions and responses that this connection supports:</span><span class="sxs-lookup"><span data-stu-id="f1962-118">Here are the details about the triggers, actions and responses that this connection supports:</span></span>

## <a name="sharepoint-online-triggers"></a><span data-ttu-id="f1962-119">SharePoint Online triggers</span><span class="sxs-lookup"><span data-stu-id="f1962-119">SharePoint Online triggers</span></span>
<span data-ttu-id="f1962-120">SharePoint has the following trigger(s):</span><span class="sxs-lookup"><span data-stu-id="f1962-120">SharePoint has the following trigger(s):</span></span>  

| <span data-ttu-id="f1962-121">Trigger</span><span class="sxs-lookup"><span data-stu-id="f1962-121">Trigger</span></span> | <span data-ttu-id="f1962-122">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-122">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="f1962-123">When a file is created</span><span class="sxs-lookup"><span data-stu-id="f1962-123">When a file is created</span></span>](connectors-create-api-sharepointonline.md#when-a-file-is-created) |<span data-ttu-id="f1962-124">This operation triggers a flow when a new file is created in a SharePoint folder.</span><span class="sxs-lookup"><span data-stu-id="f1962-124">This operation triggers a flow when a new file is created in a SharePoint folder.</span></span> |
| [<span data-ttu-id="f1962-125">When a file is modified</span><span class="sxs-lookup"><span data-stu-id="f1962-125">When a file is modified</span></span>](connectors-create-api-sharepointonline.md#when-a-file-is-modified) |<span data-ttu-id="f1962-126">This operation triggers a flow when a file is modified in a SharePoint folder.</span><span class="sxs-lookup"><span data-stu-id="f1962-126">This operation triggers a flow when a file is modified in a SharePoint folder.</span></span> |
| [<span data-ttu-id="f1962-127">When a new item is created</span><span class="sxs-lookup"><span data-stu-id="f1962-127">When a new item is created</span></span>](connectors-create-api-sharepointonline.md#when-a-new-item-is-created) |<span data-ttu-id="f1962-128">This operation triggers a flow when a new item is created in a SharePoint list.</span><span class="sxs-lookup"><span data-stu-id="f1962-128">This operation triggers a flow when a new item is created in a SharePoint list.</span></span> |
| [<span data-ttu-id="f1962-129">When an existing item is modified</span><span class="sxs-lookup"><span data-stu-id="f1962-129">When an existing item is modified</span></span>](connectors-create-api-sharepointonline.md#when-an-existing-item-is-modified) |<span data-ttu-id="f1962-130">This operation triggers a flow when an existing item is modified in a SharePoint list.</span><span class="sxs-lookup"><span data-stu-id="f1962-130">This operation triggers a flow when an existing item is modified in a SharePoint list.</span></span> |

## <a name="sharepoint-online-actions"></a><span data-ttu-id="f1962-131">SharePoint Online actions</span><span class="sxs-lookup"><span data-stu-id="f1962-131">SharePoint Online actions</span></span>
<span data-ttu-id="f1962-132">SharePoint has the following actions:</span><span class="sxs-lookup"><span data-stu-id="f1962-132">SharePoint has the following actions:</span></span>

| <span data-ttu-id="f1962-133">Action</span><span class="sxs-lookup"><span data-stu-id="f1962-133">Action</span></span> | <span data-ttu-id="f1962-134">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-134">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="f1962-135">Get file metadata</span><span class="sxs-lookup"><span data-stu-id="f1962-135">Get file metadata</span></span>](connectors-create-api-sharepointonline.md#get-file-metadata) |<span data-ttu-id="f1962-136">This operation gets file metadata using the file id.</span><span class="sxs-lookup"><span data-stu-id="f1962-136">This operation gets file metadata using the file id.</span></span> |
| [<span data-ttu-id="f1962-137">Update file</span><span class="sxs-lookup"><span data-stu-id="f1962-137">Update file</span></span>](connectors-create-api-sharepointonline.md#update-file) |<span data-ttu-id="f1962-138">This operation updates file content.</span><span class="sxs-lookup"><span data-stu-id="f1962-138">This operation updates file content.</span></span> |
| [<span data-ttu-id="f1962-139">Delete file</span><span class="sxs-lookup"><span data-stu-id="f1962-139">Delete file</span></span>](connectors-create-api-sharepointonline.md#delete-file) |<span data-ttu-id="f1962-140">This operation deletes a file.</span><span class="sxs-lookup"><span data-stu-id="f1962-140">This operation deletes a file.</span></span> |
| [<span data-ttu-id="f1962-141">Get file metadata using path</span><span class="sxs-lookup"><span data-stu-id="f1962-141">Get file metadata using path</span></span>](connectors-create-api-sharepointonline.md#get-file-metadata-using-path) |<span data-ttu-id="f1962-142">This operation gets file metadata using the file path.</span><span class="sxs-lookup"><span data-stu-id="f1962-142">This operation gets file metadata using the file path.</span></span> |
| [<span data-ttu-id="f1962-143">Get file content using path</span><span class="sxs-lookup"><span data-stu-id="f1962-143">Get file content using path</span></span>](connectors-create-api-sharepointonline.md#get-file-content-using-path) |<span data-ttu-id="f1962-144">This operation gets file contents using the file path.</span><span class="sxs-lookup"><span data-stu-id="f1962-144">This operation gets file contents using the file path.</span></span> |
| [<span data-ttu-id="f1962-145">Get file content</span><span class="sxs-lookup"><span data-stu-id="f1962-145">Get file content</span></span>](connectors-create-api-sharepointonline.md#get-file-content) |<span data-ttu-id="f1962-146">This operation gets file content using the file id.</span><span class="sxs-lookup"><span data-stu-id="f1962-146">This operation gets file content using the file id.</span></span> |
| [<span data-ttu-id="f1962-147">Create file</span><span class="sxs-lookup"><span data-stu-id="f1962-147">Create file</span></span>](connectors-create-api-sharepointonline.md#create-file) |<span data-ttu-id="f1962-148">This operation uploads a file to a SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="f1962-148">This operation uploads a file to a SharePoint site.</span></span> |
| [<span data-ttu-id="f1962-149">Copy file</span><span class="sxs-lookup"><span data-stu-id="f1962-149">Copy file</span></span>](connectors-create-api-sharepointonline.md#copy-file) |<span data-ttu-id="f1962-150">This operation copies a file to a SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="f1962-150">This operation copies a file to a SharePoint site.</span></span> |
| [<span data-ttu-id="f1962-151">List folder</span><span class="sxs-lookup"><span data-stu-id="f1962-151">List folder</span></span>](connectors-create-api-sharepointonline.md#list-folder) |<span data-ttu-id="f1962-152">This operation gets files contained in a SharePoint folder.</span><span class="sxs-lookup"><span data-stu-id="f1962-152">This operation gets files contained in a SharePoint folder.</span></span> |
| [<span data-ttu-id="f1962-153">List root folder</span><span class="sxs-lookup"><span data-stu-id="f1962-153">List root folder</span></span>](connectors-create-api-sharepointonline.md#list-root-folder) |<span data-ttu-id="f1962-154">This operaiton gets the files in the root SharePoint folder.</span><span class="sxs-lookup"><span data-stu-id="f1962-154">This operaiton gets the files in the root SharePoint folder.</span></span> |
| [<span data-ttu-id="f1962-155">Extract folder</span><span class="sxs-lookup"><span data-stu-id="f1962-155">Extract folder</span></span>](connectors-create-api-sharepointonline.md#extract-folder) |<span data-ttu-id="f1962-156">This operation extracts an archive file into a SharePoint folder (example: .zip).</span><span class="sxs-lookup"><span data-stu-id="f1962-156">This operation extracts an archive file into a SharePoint folder (example: .zip).</span></span> |
| [<span data-ttu-id="f1962-157">Get items</span><span class="sxs-lookup"><span data-stu-id="f1962-157">Get items</span></span>](connectors-create-api-sharepointonline.md#get-items) |<span data-ttu-id="f1962-158">This operation gets items from a SharePoint list.</span><span class="sxs-lookup"><span data-stu-id="f1962-158">This operation gets items from a SharePoint list.</span></span> |
| [<span data-ttu-id="f1962-159">Create item</span><span class="sxs-lookup"><span data-stu-id="f1962-159">Create item</span></span>](connectors-create-api-sharepointonline.md#create-item) |<span data-ttu-id="f1962-160">This operation creates a new item in a SharePoint list.</span><span class="sxs-lookup"><span data-stu-id="f1962-160">This operation creates a new item in a SharePoint list.</span></span> |
| [<span data-ttu-id="f1962-161">Get item</span><span class="sxs-lookup"><span data-stu-id="f1962-161">Get item</span></span>](connectors-create-api-sharepointonline.md#get-item) |<span data-ttu-id="f1962-162">This operation gets a single item by its id from a SharePoint list.</span><span class="sxs-lookup"><span data-stu-id="f1962-162">This operation gets a single item by its id from a SharePoint list.</span></span> |
| [<span data-ttu-id="f1962-163">Delete item</span><span class="sxs-lookup"><span data-stu-id="f1962-163">Delete item</span></span>](connectors-create-api-sharepointonline.md#delete-item) |<span data-ttu-id="f1962-164">This operation deletes an item from a SharePoint list.</span><span class="sxs-lookup"><span data-stu-id="f1962-164">This operation deletes an item from a SharePoint list.</span></span> |
| [<span data-ttu-id="f1962-165">Update item</span><span class="sxs-lookup"><span data-stu-id="f1962-165">Update item</span></span>](connectors-create-api-sharepointonline.md#update-item) |<span data-ttu-id="f1962-166">This operation updates an item in a SharePoint list.</span><span class="sxs-lookup"><span data-stu-id="f1962-166">This operation updates an item in a SharePoint list.</span></span> |
| [<span data-ttu-id="f1962-167">Get entity values</span><span class="sxs-lookup"><span data-stu-id="f1962-167">Get entity values</span></span>](connectors-create-api-sharepointonline.md#get-entity-values) |<span data-ttu-id="f1962-168">This operation gets possible values for a SharePoint entity.</span><span class="sxs-lookup"><span data-stu-id="f1962-168">This operation gets possible values for a SharePoint entity.</span></span> |
| [<span data-ttu-id="f1962-169">Get lists</span><span class="sxs-lookup"><span data-stu-id="f1962-169">Get lists</span></span>](connectors-create-api-sharepointonline.md#get-lists) |<span data-ttu-id="f1962-170">This operation gets SharePoint lists from a site.</span><span class="sxs-lookup"><span data-stu-id="f1962-170">This operation gets SharePoint lists from a site.</span></span> |

### <a name="action-details"></a><span data-ttu-id="f1962-171">Action details</span><span class="sxs-lookup"><span data-stu-id="f1962-171">Action details</span></span>
<span data-ttu-id="f1962-172">Here are the details for the actions and triggers for this connector, along with their responses:</span><span class="sxs-lookup"><span data-stu-id="f1962-172">Here are the details for the actions and triggers for this connector, along with their responses:</span></span>

### <a name="get-file-metadata"></a><span data-ttu-id="f1962-173">Get file metadata</span><span class="sxs-lookup"><span data-stu-id="f1962-173">Get file metadata</span></span>
<span data-ttu-id="f1962-174">This operation gets file metadata using the file id.</span><span class="sxs-lookup"><span data-stu-id="f1962-174">This operation gets file metadata using the file id.</span></span> 

| <span data-ttu-id="f1962-175">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-175">Property Name</span></span> | <span data-ttu-id="f1962-176">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-176">Display Name</span></span> | <span data-ttu-id="f1962-177">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-178">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-178">dataset\*</span></span> |<span data-ttu-id="f1962-179">Site URL</span><span class="sxs-lookup"><span data-stu-id="f1962-179">Site URL</span></span> |<span data-ttu-id="f1962-180">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span><span class="sxs-lookup"><span data-stu-id="f1962-180">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span></span> |
| <span data-ttu-id="f1962-181">id\*</span><span class="sxs-lookup"><span data-stu-id="f1962-181">id\*</span></span> |<span data-ttu-id="f1962-182">File identifier</span><span class="sxs-lookup"><span data-stu-id="f1962-182">File identifier</span></span> |<span data-ttu-id="f1962-183">Select a file</span><span class="sxs-lookup"><span data-stu-id="f1962-183">Select a file</span></span> |

<span data-ttu-id="f1962-184">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-184">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="f1962-185">Output Details</span><span class="sxs-lookup"><span data-stu-id="f1962-185">Output Details</span></span>
<span data-ttu-id="f1962-186">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="f1962-186">BlobMetadata</span></span>

| <span data-ttu-id="f1962-187">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-187">Property Name</span></span> | <span data-ttu-id="f1962-188">Data Type</span><span class="sxs-lookup"><span data-stu-id="f1962-188">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-189">Id</span><span class="sxs-lookup"><span data-stu-id="f1962-189">Id</span></span> |<span data-ttu-id="f1962-190">string</span><span class="sxs-lookup"><span data-stu-id="f1962-190">string</span></span> |
| <span data-ttu-id="f1962-191">Name</span><span class="sxs-lookup"><span data-stu-id="f1962-191">Name</span></span> |<span data-ttu-id="f1962-192">string</span><span class="sxs-lookup"><span data-stu-id="f1962-192">string</span></span> |
| <span data-ttu-id="f1962-193">DisplayName</span><span class="sxs-lookup"><span data-stu-id="f1962-193">DisplayName</span></span> |<span data-ttu-id="f1962-194">string</span><span class="sxs-lookup"><span data-stu-id="f1962-194">string</span></span> |
| <span data-ttu-id="f1962-195">Path</span><span class="sxs-lookup"><span data-stu-id="f1962-195">Path</span></span> |<span data-ttu-id="f1962-196">string</span><span class="sxs-lookup"><span data-stu-id="f1962-196">string</span></span> |
| <span data-ttu-id="f1962-197">LastModified</span><span class="sxs-lookup"><span data-stu-id="f1962-197">LastModified</span></span> |<span data-ttu-id="f1962-198">string</span><span class="sxs-lookup"><span data-stu-id="f1962-198">string</span></span> |
| <span data-ttu-id="f1962-199">Size</span><span class="sxs-lookup"><span data-stu-id="f1962-199">Size</span></span> |<span data-ttu-id="f1962-200">integer</span><span class="sxs-lookup"><span data-stu-id="f1962-200">integer</span></span> |
| <span data-ttu-id="f1962-201">MediaType</span><span class="sxs-lookup"><span data-stu-id="f1962-201">MediaType</span></span> |<span data-ttu-id="f1962-202">string</span><span class="sxs-lookup"><span data-stu-id="f1962-202">string</span></span> |
| <span data-ttu-id="f1962-203">IsFolder</span><span class="sxs-lookup"><span data-stu-id="f1962-203">IsFolder</span></span> |<span data-ttu-id="f1962-204">boolean</span><span class="sxs-lookup"><span data-stu-id="f1962-204">boolean</span></span> |
| <span data-ttu-id="f1962-205">ETag</span><span class="sxs-lookup"><span data-stu-id="f1962-205">ETag</span></span> |<span data-ttu-id="f1962-206">string</span><span class="sxs-lookup"><span data-stu-id="f1962-206">string</span></span> |
| <span data-ttu-id="f1962-207">FileLocator</span><span class="sxs-lookup"><span data-stu-id="f1962-207">FileLocator</span></span> |<span data-ttu-id="f1962-208">string</span><span class="sxs-lookup"><span data-stu-id="f1962-208">string</span></span> |

### <a name="update-file"></a><span data-ttu-id="f1962-209">Update file</span><span class="sxs-lookup"><span data-stu-id="f1962-209">Update file</span></span>
<span data-ttu-id="f1962-210">This operation updates file content.</span><span class="sxs-lookup"><span data-stu-id="f1962-210">This operation updates file content.</span></span> 

| <span data-ttu-id="f1962-211">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-211">Property Name</span></span> | <span data-ttu-id="f1962-212">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-212">Display Name</span></span> | <span data-ttu-id="f1962-213">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-213">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-214">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-214">dataset\*</span></span> |<span data-ttu-id="f1962-215">Site URL</span><span class="sxs-lookup"><span data-stu-id="f1962-215">Site URL</span></span> |<span data-ttu-id="f1962-216">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span><span class="sxs-lookup"><span data-stu-id="f1962-216">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span></span> |
| <span data-ttu-id="f1962-217">id\*</span><span class="sxs-lookup"><span data-stu-id="f1962-217">id\*</span></span> |<span data-ttu-id="f1962-218">File identifier</span><span class="sxs-lookup"><span data-stu-id="f1962-218">File identifier</span></span> |<span data-ttu-id="f1962-219">Select a file</span><span class="sxs-lookup"><span data-stu-id="f1962-219">Select a file</span></span> |
| <span data-ttu-id="f1962-220">body\*</span><span class="sxs-lookup"><span data-stu-id="f1962-220">body\*</span></span> |<span data-ttu-id="f1962-221">File Content</span><span class="sxs-lookup"><span data-stu-id="f1962-221">File Content</span></span> |<span data-ttu-id="f1962-222">Content of the file</span><span class="sxs-lookup"><span data-stu-id="f1962-222">Content of the file</span></span> |

<span data-ttu-id="f1962-223">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-223">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="f1962-224">Output Details</span><span class="sxs-lookup"><span data-stu-id="f1962-224">Output Details</span></span>
<span data-ttu-id="f1962-225">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="f1962-225">BlobMetadata</span></span>

| <span data-ttu-id="f1962-226">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-226">Property Name</span></span> | <span data-ttu-id="f1962-227">Data Type</span><span class="sxs-lookup"><span data-stu-id="f1962-227">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-228">Id</span><span class="sxs-lookup"><span data-stu-id="f1962-228">Id</span></span> |<span data-ttu-id="f1962-229">string</span><span class="sxs-lookup"><span data-stu-id="f1962-229">string</span></span> |
| <span data-ttu-id="f1962-230">Name</span><span class="sxs-lookup"><span data-stu-id="f1962-230">Name</span></span> |<span data-ttu-id="f1962-231">string</span><span class="sxs-lookup"><span data-stu-id="f1962-231">string</span></span> |
| <span data-ttu-id="f1962-232">DisplayName</span><span class="sxs-lookup"><span data-stu-id="f1962-232">DisplayName</span></span> |<span data-ttu-id="f1962-233">string</span><span class="sxs-lookup"><span data-stu-id="f1962-233">string</span></span> |
| <span data-ttu-id="f1962-234">Path</span><span class="sxs-lookup"><span data-stu-id="f1962-234">Path</span></span> |<span data-ttu-id="f1962-235">string</span><span class="sxs-lookup"><span data-stu-id="f1962-235">string</span></span> |
| <span data-ttu-id="f1962-236">LastModified</span><span class="sxs-lookup"><span data-stu-id="f1962-236">LastModified</span></span> |<span data-ttu-id="f1962-237">string</span><span class="sxs-lookup"><span data-stu-id="f1962-237">string</span></span> |
| <span data-ttu-id="f1962-238">Size</span><span class="sxs-lookup"><span data-stu-id="f1962-238">Size</span></span> |<span data-ttu-id="f1962-239">integer</span><span class="sxs-lookup"><span data-stu-id="f1962-239">integer</span></span> |
| <span data-ttu-id="f1962-240">MediaType</span><span class="sxs-lookup"><span data-stu-id="f1962-240">MediaType</span></span> |<span data-ttu-id="f1962-241">string</span><span class="sxs-lookup"><span data-stu-id="f1962-241">string</span></span> |
| <span data-ttu-id="f1962-242">IsFolder</span><span class="sxs-lookup"><span data-stu-id="f1962-242">IsFolder</span></span> |<span data-ttu-id="f1962-243">boolean</span><span class="sxs-lookup"><span data-stu-id="f1962-243">boolean</span></span> |
| <span data-ttu-id="f1962-244">ETag</span><span class="sxs-lookup"><span data-stu-id="f1962-244">ETag</span></span> |<span data-ttu-id="f1962-245">string</span><span class="sxs-lookup"><span data-stu-id="f1962-245">string</span></span> |
| <span data-ttu-id="f1962-246">FileLocator</span><span class="sxs-lookup"><span data-stu-id="f1962-246">FileLocator</span></span> |<span data-ttu-id="f1962-247">string</span><span class="sxs-lookup"><span data-stu-id="f1962-247">string</span></span> |

### <a name="delete-file"></a><span data-ttu-id="f1962-248">Delete file</span><span class="sxs-lookup"><span data-stu-id="f1962-248">Delete file</span></span>
<span data-ttu-id="f1962-249">This operation deletes a file.</span><span class="sxs-lookup"><span data-stu-id="f1962-249">This operation deletes a file.</span></span> 

| <span data-ttu-id="f1962-250">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-250">Property Name</span></span> | <span data-ttu-id="f1962-251">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-251">Display Name</span></span> | <span data-ttu-id="f1962-252">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-252">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-253">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-253">dataset\*</span></span> |<span data-ttu-id="f1962-254">Site URL</span><span class="sxs-lookup"><span data-stu-id="f1962-254">Site URL</span></span> |<span data-ttu-id="f1962-255">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span><span class="sxs-lookup"><span data-stu-id="f1962-255">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span></span> |
| <span data-ttu-id="f1962-256">id\*</span><span class="sxs-lookup"><span data-stu-id="f1962-256">id\*</span></span> |<span data-ttu-id="f1962-257">File identifier</span><span class="sxs-lookup"><span data-stu-id="f1962-257">File identifier</span></span> |<span data-ttu-id="f1962-258">Select a file</span><span class="sxs-lookup"><span data-stu-id="f1962-258">Select a file</span></span> |

<span data-ttu-id="f1962-259">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-259">An \* indicates that a property is required</span></span>

### <a name="get-file-metadata-using-path"></a><span data-ttu-id="f1962-260">Get file metadata using path</span><span class="sxs-lookup"><span data-stu-id="f1962-260">Get file metadata using path</span></span>
<span data-ttu-id="f1962-261">This operation gets file metadata using the file path.</span><span class="sxs-lookup"><span data-stu-id="f1962-261">This operation gets file metadata using the file path.</span></span> 

| <span data-ttu-id="f1962-262">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-262">Property Name</span></span> | <span data-ttu-id="f1962-263">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-263">Display Name</span></span> | <span data-ttu-id="f1962-264">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-264">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-265">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-265">dataset\*</span></span> |<span data-ttu-id="f1962-266">Site URL</span><span class="sxs-lookup"><span data-stu-id="f1962-266">Site URL</span></span> |<span data-ttu-id="f1962-267">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span><span class="sxs-lookup"><span data-stu-id="f1962-267">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span></span> |
| <span data-ttu-id="f1962-268">path\*</span><span class="sxs-lookup"><span data-stu-id="f1962-268">path\*</span></span> |<span data-ttu-id="f1962-269">File path</span><span class="sxs-lookup"><span data-stu-id="f1962-269">File path</span></span> |<span data-ttu-id="f1962-270">Select a file</span><span class="sxs-lookup"><span data-stu-id="f1962-270">Select a file</span></span> |

<span data-ttu-id="f1962-271">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-271">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="f1962-272">Output Details</span><span class="sxs-lookup"><span data-stu-id="f1962-272">Output Details</span></span>
<span data-ttu-id="f1962-273">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="f1962-273">BlobMetadata</span></span>

| <span data-ttu-id="f1962-274">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-274">Property Name</span></span> | <span data-ttu-id="f1962-275">Data Type</span><span class="sxs-lookup"><span data-stu-id="f1962-275">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-276">Id</span><span class="sxs-lookup"><span data-stu-id="f1962-276">Id</span></span> |<span data-ttu-id="f1962-277">string</span><span class="sxs-lookup"><span data-stu-id="f1962-277">string</span></span> |
| <span data-ttu-id="f1962-278">Name</span><span class="sxs-lookup"><span data-stu-id="f1962-278">Name</span></span> |<span data-ttu-id="f1962-279">string</span><span class="sxs-lookup"><span data-stu-id="f1962-279">string</span></span> |
| <span data-ttu-id="f1962-280">DisplayName</span><span class="sxs-lookup"><span data-stu-id="f1962-280">DisplayName</span></span> |<span data-ttu-id="f1962-281">string</span><span class="sxs-lookup"><span data-stu-id="f1962-281">string</span></span> |
| <span data-ttu-id="f1962-282">Path</span><span class="sxs-lookup"><span data-stu-id="f1962-282">Path</span></span> |<span data-ttu-id="f1962-283">string</span><span class="sxs-lookup"><span data-stu-id="f1962-283">string</span></span> |
| <span data-ttu-id="f1962-284">LastModified</span><span class="sxs-lookup"><span data-stu-id="f1962-284">LastModified</span></span> |<span data-ttu-id="f1962-285">string</span><span class="sxs-lookup"><span data-stu-id="f1962-285">string</span></span> |
| <span data-ttu-id="f1962-286">Size</span><span class="sxs-lookup"><span data-stu-id="f1962-286">Size</span></span> |<span data-ttu-id="f1962-287">integer</span><span class="sxs-lookup"><span data-stu-id="f1962-287">integer</span></span> |
| <span data-ttu-id="f1962-288">MediaType</span><span class="sxs-lookup"><span data-stu-id="f1962-288">MediaType</span></span> |<span data-ttu-id="f1962-289">string</span><span class="sxs-lookup"><span data-stu-id="f1962-289">string</span></span> |
| <span data-ttu-id="f1962-290">IsFolder</span><span class="sxs-lookup"><span data-stu-id="f1962-290">IsFolder</span></span> |<span data-ttu-id="f1962-291">boolean</span><span class="sxs-lookup"><span data-stu-id="f1962-291">boolean</span></span> |
| <span data-ttu-id="f1962-292">ETag</span><span class="sxs-lookup"><span data-stu-id="f1962-292">ETag</span></span> |<span data-ttu-id="f1962-293">string</span><span class="sxs-lookup"><span data-stu-id="f1962-293">string</span></span> |
| <span data-ttu-id="f1962-294">FileLocator</span><span class="sxs-lookup"><span data-stu-id="f1962-294">FileLocator</span></span> |<span data-ttu-id="f1962-295">string</span><span class="sxs-lookup"><span data-stu-id="f1962-295">string</span></span> |

### <a name="get-file-content-using-path"></a><span data-ttu-id="f1962-296">Get file content using path</span><span class="sxs-lookup"><span data-stu-id="f1962-296">Get file content using path</span></span>
<span data-ttu-id="f1962-297">This operation gets file contents using the file path.</span><span class="sxs-lookup"><span data-stu-id="f1962-297">This operation gets file contents using the file path.</span></span> 

| <span data-ttu-id="f1962-298">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-298">Property Name</span></span> | <span data-ttu-id="f1962-299">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-299">Display Name</span></span> | <span data-ttu-id="f1962-300">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-300">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-301">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-301">dataset\*</span></span> |<span data-ttu-id="f1962-302">Site URL</span><span class="sxs-lookup"><span data-stu-id="f1962-302">Site URL</span></span> |<span data-ttu-id="f1962-303">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span><span class="sxs-lookup"><span data-stu-id="f1962-303">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span></span> |
| <span data-ttu-id="f1962-304">path\*</span><span class="sxs-lookup"><span data-stu-id="f1962-304">path\*</span></span> |<span data-ttu-id="f1962-305">File path</span><span class="sxs-lookup"><span data-stu-id="f1962-305">File path</span></span> |<span data-ttu-id="f1962-306">Select a file</span><span class="sxs-lookup"><span data-stu-id="f1962-306">Select a file</span></span> |

<span data-ttu-id="f1962-307">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-307">An \* indicates that a property is required</span></span>

### <a name="get-file-content"></a><span data-ttu-id="f1962-308">Get file content</span><span class="sxs-lookup"><span data-stu-id="f1962-308">Get file content</span></span>
<span data-ttu-id="f1962-309">This operation gets file content using the file id.</span><span class="sxs-lookup"><span data-stu-id="f1962-309">This operation gets file content using the file id.</span></span> 

| <span data-ttu-id="f1962-310">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-310">Property Name</span></span> | <span data-ttu-id="f1962-311">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-311">Display Name</span></span> | <span data-ttu-id="f1962-312">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-312">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-313">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-313">dataset\*</span></span> |<span data-ttu-id="f1962-314">Site URL</span><span class="sxs-lookup"><span data-stu-id="f1962-314">Site URL</span></span> |<span data-ttu-id="f1962-315">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span><span class="sxs-lookup"><span data-stu-id="f1962-315">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span></span> |
| <span data-ttu-id="f1962-316">id\*</span><span class="sxs-lookup"><span data-stu-id="f1962-316">id\*</span></span> |<span data-ttu-id="f1962-317">File identifier</span><span class="sxs-lookup"><span data-stu-id="f1962-317">File identifier</span></span> |<span data-ttu-id="f1962-318">Select a file</span><span class="sxs-lookup"><span data-stu-id="f1962-318">Select a file</span></span> |

<span data-ttu-id="f1962-319">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-319">An \* indicates that a property is required</span></span>

### <a name="create-file"></a><span data-ttu-id="f1962-320">Create file</span><span class="sxs-lookup"><span data-stu-id="f1962-320">Create file</span></span>
<span data-ttu-id="f1962-321">This operation uploads a file to a SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="f1962-321">This operation uploads a file to a SharePoint site.</span></span> 

| <span data-ttu-id="f1962-322">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-322">Property Name</span></span> | <span data-ttu-id="f1962-323">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-323">Display Name</span></span> | <span data-ttu-id="f1962-324">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-324">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-325">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-325">dataset\*</span></span> |<span data-ttu-id="f1962-326">Site URL</span><span class="sxs-lookup"><span data-stu-id="f1962-326">Site URL</span></span> |<span data-ttu-id="f1962-327">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span><span class="sxs-lookup"><span data-stu-id="f1962-327">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span></span> |
| <span data-ttu-id="f1962-328">folderPath\*</span><span class="sxs-lookup"><span data-stu-id="f1962-328">folderPath\*</span></span> |<span data-ttu-id="f1962-329">Folder Path</span><span class="sxs-lookup"><span data-stu-id="f1962-329">Folder Path</span></span> |<span data-ttu-id="f1962-330">Select a file</span><span class="sxs-lookup"><span data-stu-id="f1962-330">Select a file</span></span> |
| <span data-ttu-id="f1962-331">name\*</span><span class="sxs-lookup"><span data-stu-id="f1962-331">name\*</span></span> |<span data-ttu-id="f1962-332">File name</span><span class="sxs-lookup"><span data-stu-id="f1962-332">File name</span></span> |<span data-ttu-id="f1962-333">Name of the file</span><span class="sxs-lookup"><span data-stu-id="f1962-333">Name of the file</span></span> |
| <span data-ttu-id="f1962-334">body\*</span><span class="sxs-lookup"><span data-stu-id="f1962-334">body\*</span></span> |<span data-ttu-id="f1962-335">File Content</span><span class="sxs-lookup"><span data-stu-id="f1962-335">File Content</span></span> |<span data-ttu-id="f1962-336">Content of the file</span><span class="sxs-lookup"><span data-stu-id="f1962-336">Content of the file</span></span> |

<span data-ttu-id="f1962-337">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-337">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="f1962-338">Output Details</span><span class="sxs-lookup"><span data-stu-id="f1962-338">Output Details</span></span>
<span data-ttu-id="f1962-339">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="f1962-339">BlobMetadata</span></span>

| <span data-ttu-id="f1962-340">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-340">Property Name</span></span> | <span data-ttu-id="f1962-341">Data Type</span><span class="sxs-lookup"><span data-stu-id="f1962-341">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-342">Id</span><span class="sxs-lookup"><span data-stu-id="f1962-342">Id</span></span> |<span data-ttu-id="f1962-343">string</span><span class="sxs-lookup"><span data-stu-id="f1962-343">string</span></span> |
| <span data-ttu-id="f1962-344">Name</span><span class="sxs-lookup"><span data-stu-id="f1962-344">Name</span></span> |<span data-ttu-id="f1962-345">string</span><span class="sxs-lookup"><span data-stu-id="f1962-345">string</span></span> |
| <span data-ttu-id="f1962-346">DisplayName</span><span class="sxs-lookup"><span data-stu-id="f1962-346">DisplayName</span></span> |<span data-ttu-id="f1962-347">string</span><span class="sxs-lookup"><span data-stu-id="f1962-347">string</span></span> |
| <span data-ttu-id="f1962-348">Path</span><span class="sxs-lookup"><span data-stu-id="f1962-348">Path</span></span> |<span data-ttu-id="f1962-349">string</span><span class="sxs-lookup"><span data-stu-id="f1962-349">string</span></span> |
| <span data-ttu-id="f1962-350">LastModified</span><span class="sxs-lookup"><span data-stu-id="f1962-350">LastModified</span></span> |<span data-ttu-id="f1962-351">string</span><span class="sxs-lookup"><span data-stu-id="f1962-351">string</span></span> |
| <span data-ttu-id="f1962-352">Size</span><span class="sxs-lookup"><span data-stu-id="f1962-352">Size</span></span> |<span data-ttu-id="f1962-353">integer</span><span class="sxs-lookup"><span data-stu-id="f1962-353">integer</span></span> |
| <span data-ttu-id="f1962-354">MediaType</span><span class="sxs-lookup"><span data-stu-id="f1962-354">MediaType</span></span> |<span data-ttu-id="f1962-355">string</span><span class="sxs-lookup"><span data-stu-id="f1962-355">string</span></span> |
| <span data-ttu-id="f1962-356">IsFolder</span><span class="sxs-lookup"><span data-stu-id="f1962-356">IsFolder</span></span> |<span data-ttu-id="f1962-357">boolean</span><span class="sxs-lookup"><span data-stu-id="f1962-357">boolean</span></span> |
| <span data-ttu-id="f1962-358">ETag</span><span class="sxs-lookup"><span data-stu-id="f1962-358">ETag</span></span> |<span data-ttu-id="f1962-359">string</span><span class="sxs-lookup"><span data-stu-id="f1962-359">string</span></span> |
| <span data-ttu-id="f1962-360">FileLocator</span><span class="sxs-lookup"><span data-stu-id="f1962-360">FileLocator</span></span> |<span data-ttu-id="f1962-361">string</span><span class="sxs-lookup"><span data-stu-id="f1962-361">string</span></span> |

### <a name="copy-file"></a><span data-ttu-id="f1962-362">Copy file</span><span class="sxs-lookup"><span data-stu-id="f1962-362">Copy file</span></span>
<span data-ttu-id="f1962-363">This operation copies a file to a SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="f1962-363">This operation copies a file to a SharePoint site.</span></span> 

| <span data-ttu-id="f1962-364">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-364">Property Name</span></span> | <span data-ttu-id="f1962-365">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-365">Display Name</span></span> | <span data-ttu-id="f1962-366">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-366">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-367">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-367">dataset\*</span></span> |<span data-ttu-id="f1962-368">Site URL</span><span class="sxs-lookup"><span data-stu-id="f1962-368">Site URL</span></span> |<span data-ttu-id="f1962-369">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span><span class="sxs-lookup"><span data-stu-id="f1962-369">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span></span> |
| <span data-ttu-id="f1962-370">source\*</span><span class="sxs-lookup"><span data-stu-id="f1962-370">source\*</span></span> |<span data-ttu-id="f1962-371">Source file Path</span><span class="sxs-lookup"><span data-stu-id="f1962-371">Source file Path</span></span> |<span data-ttu-id="f1962-372">Path to the source file</span><span class="sxs-lookup"><span data-stu-id="f1962-372">Path to the source file</span></span> |
| <span data-ttu-id="f1962-373">destination\*</span><span class="sxs-lookup"><span data-stu-id="f1962-373">destination\*</span></span> |<span data-ttu-id="f1962-374">Destination file path</span><span class="sxs-lookup"><span data-stu-id="f1962-374">Destination file path</span></span> |<span data-ttu-id="f1962-375">Path to the destination file</span><span class="sxs-lookup"><span data-stu-id="f1962-375">Path to the destination file</span></span> |
| <span data-ttu-id="f1962-376">overwrite</span><span class="sxs-lookup"><span data-stu-id="f1962-376">overwrite</span></span> |<span data-ttu-id="f1962-377">Overwrite flag</span><span class="sxs-lookup"><span data-stu-id="f1962-377">Overwrite flag</span></span> |<span data-ttu-id="f1962-378">Whether or not to overwrite the destination file if it exists</span><span class="sxs-lookup"><span data-stu-id="f1962-378">Whether or not to overwrite the destination file if it exists</span></span> |

<span data-ttu-id="f1962-379">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-379">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="f1962-380">Output Details</span><span class="sxs-lookup"><span data-stu-id="f1962-380">Output Details</span></span>
<span data-ttu-id="f1962-381">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="f1962-381">BlobMetadata</span></span>

| <span data-ttu-id="f1962-382">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-382">Property Name</span></span> | <span data-ttu-id="f1962-383">Data Type</span><span class="sxs-lookup"><span data-stu-id="f1962-383">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-384">Id</span><span class="sxs-lookup"><span data-stu-id="f1962-384">Id</span></span> |<span data-ttu-id="f1962-385">string</span><span class="sxs-lookup"><span data-stu-id="f1962-385">string</span></span> |
| <span data-ttu-id="f1962-386">Name</span><span class="sxs-lookup"><span data-stu-id="f1962-386">Name</span></span> |<span data-ttu-id="f1962-387">string</span><span class="sxs-lookup"><span data-stu-id="f1962-387">string</span></span> |
| <span data-ttu-id="f1962-388">DisplayName</span><span class="sxs-lookup"><span data-stu-id="f1962-388">DisplayName</span></span> |<span data-ttu-id="f1962-389">string</span><span class="sxs-lookup"><span data-stu-id="f1962-389">string</span></span> |
| <span data-ttu-id="f1962-390">Path</span><span class="sxs-lookup"><span data-stu-id="f1962-390">Path</span></span> |<span data-ttu-id="f1962-391">string</span><span class="sxs-lookup"><span data-stu-id="f1962-391">string</span></span> |
| <span data-ttu-id="f1962-392">LastModified</span><span class="sxs-lookup"><span data-stu-id="f1962-392">LastModified</span></span> |<span data-ttu-id="f1962-393">string</span><span class="sxs-lookup"><span data-stu-id="f1962-393">string</span></span> |
| <span data-ttu-id="f1962-394">Size</span><span class="sxs-lookup"><span data-stu-id="f1962-394">Size</span></span> |<span data-ttu-id="f1962-395">integer</span><span class="sxs-lookup"><span data-stu-id="f1962-395">integer</span></span> |
| <span data-ttu-id="f1962-396">MediaType</span><span class="sxs-lookup"><span data-stu-id="f1962-396">MediaType</span></span> |<span data-ttu-id="f1962-397">string</span><span class="sxs-lookup"><span data-stu-id="f1962-397">string</span></span> |
| <span data-ttu-id="f1962-398">IsFolder</span><span class="sxs-lookup"><span data-stu-id="f1962-398">IsFolder</span></span> |<span data-ttu-id="f1962-399">boolean</span><span class="sxs-lookup"><span data-stu-id="f1962-399">boolean</span></span> |
| <span data-ttu-id="f1962-400">ETag</span><span class="sxs-lookup"><span data-stu-id="f1962-400">ETag</span></span> |<span data-ttu-id="f1962-401">string</span><span class="sxs-lookup"><span data-stu-id="f1962-401">string</span></span> |
| <span data-ttu-id="f1962-402">FileLocator</span><span class="sxs-lookup"><span data-stu-id="f1962-402">FileLocator</span></span> |<span data-ttu-id="f1962-403">string</span><span class="sxs-lookup"><span data-stu-id="f1962-403">string</span></span> |

### <a name="when-a-file-is-created"></a><span data-ttu-id="f1962-404">When a file is created</span><span class="sxs-lookup"><span data-stu-id="f1962-404">When a file is created</span></span>
<span data-ttu-id="f1962-405">This operation triggers a flow when a new file is created in a SharePoint folder.</span><span class="sxs-lookup"><span data-stu-id="f1962-405">This operation triggers a flow when a new file is created in a SharePoint folder.</span></span> 

| <span data-ttu-id="f1962-406">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-406">Property Name</span></span> | <span data-ttu-id="f1962-407">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-407">Display Name</span></span> | <span data-ttu-id="f1962-408">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-408">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-409">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-409">dataset\*</span></span> |<span data-ttu-id="f1962-410">Site URL</span><span class="sxs-lookup"><span data-stu-id="f1962-410">Site URL</span></span> |<span data-ttu-id="f1962-411">SharePoint site url</span><span class="sxs-lookup"><span data-stu-id="f1962-411">SharePoint site url</span></span> |
| <span data-ttu-id="f1962-412">folderId\*</span><span class="sxs-lookup"><span data-stu-id="f1962-412">folderId\*</span></span> |<span data-ttu-id="f1962-413">Folder Id</span><span class="sxs-lookup"><span data-stu-id="f1962-413">Folder Id</span></span> |<span data-ttu-id="f1962-414">Select a folder</span><span class="sxs-lookup"><span data-stu-id="f1962-414">Select a folder</span></span> |

<span data-ttu-id="f1962-415">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-415">An \* indicates that a property is required</span></span>

### <a name="when-a-file-is-modified"></a><span data-ttu-id="f1962-416">When a file is modified</span><span class="sxs-lookup"><span data-stu-id="f1962-416">When a file is modified</span></span>
<span data-ttu-id="f1962-417">This operation triggers a flow when a file is modified in a SharePoint folder.</span><span class="sxs-lookup"><span data-stu-id="f1962-417">This operation triggers a flow when a file is modified in a SharePoint folder.</span></span> 

| <span data-ttu-id="f1962-418">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-418">Property Name</span></span> | <span data-ttu-id="f1962-419">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-419">Display Name</span></span> | <span data-ttu-id="f1962-420">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-420">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-421">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-421">dataset\*</span></span> |<span data-ttu-id="f1962-422">Site URL</span><span class="sxs-lookup"><span data-stu-id="f1962-422">Site URL</span></span> |<span data-ttu-id="f1962-423">SharePoint site url</span><span class="sxs-lookup"><span data-stu-id="f1962-423">SharePoint site url</span></span> |
| <span data-ttu-id="f1962-424">folderId\*</span><span class="sxs-lookup"><span data-stu-id="f1962-424">folderId\*</span></span> |<span data-ttu-id="f1962-425">Folder Id</span><span class="sxs-lookup"><span data-stu-id="f1962-425">Folder Id</span></span> |<span data-ttu-id="f1962-426">Select a folder</span><span class="sxs-lookup"><span data-stu-id="f1962-426">Select a folder</span></span> |

<span data-ttu-id="f1962-427">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-427">An \* indicates that a property is required</span></span>

### <a name="list-folder"></a><span data-ttu-id="f1962-428">List folder</span><span class="sxs-lookup"><span data-stu-id="f1962-428">List folder</span></span>
<span data-ttu-id="f1962-429">This operation gets files contained in a SharePoint folder.</span><span class="sxs-lookup"><span data-stu-id="f1962-429">This operation gets files contained in a SharePoint folder.</span></span> 

| <span data-ttu-id="f1962-430">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-430">Property Name</span></span> | <span data-ttu-id="f1962-431">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-431">Display Name</span></span> | <span data-ttu-id="f1962-432">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-432">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-433">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-433">dataset\*</span></span> |<span data-ttu-id="f1962-434">Site URL</span><span class="sxs-lookup"><span data-stu-id="f1962-434">Site URL</span></span> |<span data-ttu-id="f1962-435">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span><span class="sxs-lookup"><span data-stu-id="f1962-435">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span></span> |
| <span data-ttu-id="f1962-436">id\*</span><span class="sxs-lookup"><span data-stu-id="f1962-436">id\*</span></span> |<span data-ttu-id="f1962-437">File identifier</span><span class="sxs-lookup"><span data-stu-id="f1962-437">File identifier</span></span> |<span data-ttu-id="f1962-438">Unique identifier of the folder</span><span class="sxs-lookup"><span data-stu-id="f1962-438">Unique identifier of the folder</span></span> |

<span data-ttu-id="f1962-439">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-439">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="f1962-440">Output Details</span><span class="sxs-lookup"><span data-stu-id="f1962-440">Output Details</span></span>
<span data-ttu-id="f1962-441">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="f1962-441">BlobMetadata</span></span>

| <span data-ttu-id="f1962-442">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-442">Property Name</span></span> | <span data-ttu-id="f1962-443">Data Type</span><span class="sxs-lookup"><span data-stu-id="f1962-443">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-444">Id</span><span class="sxs-lookup"><span data-stu-id="f1962-444">Id</span></span> |<span data-ttu-id="f1962-445">string</span><span class="sxs-lookup"><span data-stu-id="f1962-445">string</span></span> |
| <span data-ttu-id="f1962-446">Name</span><span class="sxs-lookup"><span data-stu-id="f1962-446">Name</span></span> |<span data-ttu-id="f1962-447">string</span><span class="sxs-lookup"><span data-stu-id="f1962-447">string</span></span> |
| <span data-ttu-id="f1962-448">DisplayName</span><span class="sxs-lookup"><span data-stu-id="f1962-448">DisplayName</span></span> |<span data-ttu-id="f1962-449">string</span><span class="sxs-lookup"><span data-stu-id="f1962-449">string</span></span> |
| <span data-ttu-id="f1962-450">Path</span><span class="sxs-lookup"><span data-stu-id="f1962-450">Path</span></span> |<span data-ttu-id="f1962-451">string</span><span class="sxs-lookup"><span data-stu-id="f1962-451">string</span></span> |
| <span data-ttu-id="f1962-452">LastModified</span><span class="sxs-lookup"><span data-stu-id="f1962-452">LastModified</span></span> |<span data-ttu-id="f1962-453">string</span><span class="sxs-lookup"><span data-stu-id="f1962-453">string</span></span> |
| <span data-ttu-id="f1962-454">Size</span><span class="sxs-lookup"><span data-stu-id="f1962-454">Size</span></span> |<span data-ttu-id="f1962-455">integer</span><span class="sxs-lookup"><span data-stu-id="f1962-455">integer</span></span> |
| <span data-ttu-id="f1962-456">MediaType</span><span class="sxs-lookup"><span data-stu-id="f1962-456">MediaType</span></span> |<span data-ttu-id="f1962-457">string</span><span class="sxs-lookup"><span data-stu-id="f1962-457">string</span></span> |
| <span data-ttu-id="f1962-458">IsFolder</span><span class="sxs-lookup"><span data-stu-id="f1962-458">IsFolder</span></span> |<span data-ttu-id="f1962-459">boolean</span><span class="sxs-lookup"><span data-stu-id="f1962-459">boolean</span></span> |
| <span data-ttu-id="f1962-460">ETag</span><span class="sxs-lookup"><span data-stu-id="f1962-460">ETag</span></span> |<span data-ttu-id="f1962-461">string</span><span class="sxs-lookup"><span data-stu-id="f1962-461">string</span></span> |
| <span data-ttu-id="f1962-462">FileLocator</span><span class="sxs-lookup"><span data-stu-id="f1962-462">FileLocator</span></span> |<span data-ttu-id="f1962-463">string</span><span class="sxs-lookup"><span data-stu-id="f1962-463">string</span></span> |

### <a name="list-root-folder"></a><span data-ttu-id="f1962-464">List root folder</span><span class="sxs-lookup"><span data-stu-id="f1962-464">List root folder</span></span>
<span data-ttu-id="f1962-465">This operaiton gets the files in the root SharePoint folder.</span><span class="sxs-lookup"><span data-stu-id="f1962-465">This operaiton gets the files in the root SharePoint folder.</span></span> 

| <span data-ttu-id="f1962-466">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-466">Property Name</span></span> | <span data-ttu-id="f1962-467">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-467">Display Name</span></span> | <span data-ttu-id="f1962-468">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-468">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-469">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-469">dataset\*</span></span> |<span data-ttu-id="f1962-470">Site URL</span><span class="sxs-lookup"><span data-stu-id="f1962-470">Site URL</span></span> |<span data-ttu-id="f1962-471">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span><span class="sxs-lookup"><span data-stu-id="f1962-471">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span></span> |

<span data-ttu-id="f1962-472">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-472">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="f1962-473">Output Details</span><span class="sxs-lookup"><span data-stu-id="f1962-473">Output Details</span></span>
<span data-ttu-id="f1962-474">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="f1962-474">BlobMetadata</span></span>

| <span data-ttu-id="f1962-475">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-475">Property Name</span></span> | <span data-ttu-id="f1962-476">Data Type</span><span class="sxs-lookup"><span data-stu-id="f1962-476">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-477">Id</span><span class="sxs-lookup"><span data-stu-id="f1962-477">Id</span></span> |<span data-ttu-id="f1962-478">string</span><span class="sxs-lookup"><span data-stu-id="f1962-478">string</span></span> |
| <span data-ttu-id="f1962-479">Name</span><span class="sxs-lookup"><span data-stu-id="f1962-479">Name</span></span> |<span data-ttu-id="f1962-480">string</span><span class="sxs-lookup"><span data-stu-id="f1962-480">string</span></span> |
| <span data-ttu-id="f1962-481">DisplayName</span><span class="sxs-lookup"><span data-stu-id="f1962-481">DisplayName</span></span> |<span data-ttu-id="f1962-482">string</span><span class="sxs-lookup"><span data-stu-id="f1962-482">string</span></span> |
| <span data-ttu-id="f1962-483">Path</span><span class="sxs-lookup"><span data-stu-id="f1962-483">Path</span></span> |<span data-ttu-id="f1962-484">string</span><span class="sxs-lookup"><span data-stu-id="f1962-484">string</span></span> |
| <span data-ttu-id="f1962-485">LastModified</span><span class="sxs-lookup"><span data-stu-id="f1962-485">LastModified</span></span> |<span data-ttu-id="f1962-486">string</span><span class="sxs-lookup"><span data-stu-id="f1962-486">string</span></span> |
| <span data-ttu-id="f1962-487">Size</span><span class="sxs-lookup"><span data-stu-id="f1962-487">Size</span></span> |<span data-ttu-id="f1962-488">integer</span><span class="sxs-lookup"><span data-stu-id="f1962-488">integer</span></span> |
| <span data-ttu-id="f1962-489">MediaType</span><span class="sxs-lookup"><span data-stu-id="f1962-489">MediaType</span></span> |<span data-ttu-id="f1962-490">string</span><span class="sxs-lookup"><span data-stu-id="f1962-490">string</span></span> |
| <span data-ttu-id="f1962-491">IsFolder</span><span class="sxs-lookup"><span data-stu-id="f1962-491">IsFolder</span></span> |<span data-ttu-id="f1962-492">boolean</span><span class="sxs-lookup"><span data-stu-id="f1962-492">boolean</span></span> |
| <span data-ttu-id="f1962-493">ETag</span><span class="sxs-lookup"><span data-stu-id="f1962-493">ETag</span></span> |<span data-ttu-id="f1962-494">string</span><span class="sxs-lookup"><span data-stu-id="f1962-494">string</span></span> |
| <span data-ttu-id="f1962-495">FileLocator</span><span class="sxs-lookup"><span data-stu-id="f1962-495">FileLocator</span></span> |<span data-ttu-id="f1962-496">string</span><span class="sxs-lookup"><span data-stu-id="f1962-496">string</span></span> |

### <a name="extract-folder"></a><span data-ttu-id="f1962-497">Extract folder</span><span class="sxs-lookup"><span data-stu-id="f1962-497">Extract folder</span></span>
<span data-ttu-id="f1962-498">This operation extracts an archive file into a SharePoint folder (example: .zip).</span><span class="sxs-lookup"><span data-stu-id="f1962-498">This operation extracts an archive file into a SharePoint folder (example: .zip).</span></span> 

| <span data-ttu-id="f1962-499">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-499">Property Name</span></span> | <span data-ttu-id="f1962-500">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-500">Display Name</span></span> | <span data-ttu-id="f1962-501">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-501">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-502">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-502">dataset\*</span></span> |<span data-ttu-id="f1962-503">Site URL</span><span class="sxs-lookup"><span data-stu-id="f1962-503">Site URL</span></span> |<span data-ttu-id="f1962-504">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span><span class="sxs-lookup"><span data-stu-id="f1962-504">SharePoint site url like http://contoso.sharepoint.com/sites/mysite</span></span> |
| <span data-ttu-id="f1962-505">source\*</span><span class="sxs-lookup"><span data-stu-id="f1962-505">source\*</span></span> |<span data-ttu-id="f1962-506">Source file Path</span><span class="sxs-lookup"><span data-stu-id="f1962-506">Source file Path</span></span> |<span data-ttu-id="f1962-507">Path to the source file</span><span class="sxs-lookup"><span data-stu-id="f1962-507">Path to the source file</span></span> |
| <span data-ttu-id="f1962-508">destination\*</span><span class="sxs-lookup"><span data-stu-id="f1962-508">destination\*</span></span> |<span data-ttu-id="f1962-509">Destination folder path</span><span class="sxs-lookup"><span data-stu-id="f1962-509">Destination folder path</span></span> |<span data-ttu-id="f1962-510">Path to the destination folder</span><span class="sxs-lookup"><span data-stu-id="f1962-510">Path to the destination folder</span></span> |
| <span data-ttu-id="f1962-511">overwrite</span><span class="sxs-lookup"><span data-stu-id="f1962-511">overwrite</span></span> |<span data-ttu-id="f1962-512">Overwrite flag</span><span class="sxs-lookup"><span data-stu-id="f1962-512">Overwrite flag</span></span> |<span data-ttu-id="f1962-513">Whether or not to overwrite the destination file if it exists</span><span class="sxs-lookup"><span data-stu-id="f1962-513">Whether or not to overwrite the destination file if it exists</span></span> |

<span data-ttu-id="f1962-514">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-514">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="f1962-515">Output Details</span><span class="sxs-lookup"><span data-stu-id="f1962-515">Output Details</span></span>
<span data-ttu-id="f1962-516">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="f1962-516">BlobMetadata</span></span>

| <span data-ttu-id="f1962-517">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-517">Property Name</span></span> | <span data-ttu-id="f1962-518">Data Type</span><span class="sxs-lookup"><span data-stu-id="f1962-518">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-519">Id</span><span class="sxs-lookup"><span data-stu-id="f1962-519">Id</span></span> |<span data-ttu-id="f1962-520">string</span><span class="sxs-lookup"><span data-stu-id="f1962-520">string</span></span> |
| <span data-ttu-id="f1962-521">Name</span><span class="sxs-lookup"><span data-stu-id="f1962-521">Name</span></span> |<span data-ttu-id="f1962-522">string</span><span class="sxs-lookup"><span data-stu-id="f1962-522">string</span></span> |
| <span data-ttu-id="f1962-523">DisplayName</span><span class="sxs-lookup"><span data-stu-id="f1962-523">DisplayName</span></span> |<span data-ttu-id="f1962-524">string</span><span class="sxs-lookup"><span data-stu-id="f1962-524">string</span></span> |
| <span data-ttu-id="f1962-525">Path</span><span class="sxs-lookup"><span data-stu-id="f1962-525">Path</span></span> |<span data-ttu-id="f1962-526">string</span><span class="sxs-lookup"><span data-stu-id="f1962-526">string</span></span> |
| <span data-ttu-id="f1962-527">LastModified</span><span class="sxs-lookup"><span data-stu-id="f1962-527">LastModified</span></span> |<span data-ttu-id="f1962-528">string</span><span class="sxs-lookup"><span data-stu-id="f1962-528">string</span></span> |
| <span data-ttu-id="f1962-529">Size</span><span class="sxs-lookup"><span data-stu-id="f1962-529">Size</span></span> |<span data-ttu-id="f1962-530">integer</span><span class="sxs-lookup"><span data-stu-id="f1962-530">integer</span></span> |
| <span data-ttu-id="f1962-531">MediaType</span><span class="sxs-lookup"><span data-stu-id="f1962-531">MediaType</span></span> |<span data-ttu-id="f1962-532">string</span><span class="sxs-lookup"><span data-stu-id="f1962-532">string</span></span> |
| <span data-ttu-id="f1962-533">IsFolder</span><span class="sxs-lookup"><span data-stu-id="f1962-533">IsFolder</span></span> |<span data-ttu-id="f1962-534">boolean</span><span class="sxs-lookup"><span data-stu-id="f1962-534">boolean</span></span> |
| <span data-ttu-id="f1962-535">ETag</span><span class="sxs-lookup"><span data-stu-id="f1962-535">ETag</span></span> |<span data-ttu-id="f1962-536">string</span><span class="sxs-lookup"><span data-stu-id="f1962-536">string</span></span> |
| <span data-ttu-id="f1962-537">FileLocator</span><span class="sxs-lookup"><span data-stu-id="f1962-537">FileLocator</span></span> |<span data-ttu-id="f1962-538">string</span><span class="sxs-lookup"><span data-stu-id="f1962-538">string</span></span> |

### <a name="when-a-new-item-is-created"></a><span data-ttu-id="f1962-539">When a new item is created</span><span class="sxs-lookup"><span data-stu-id="f1962-539">When a new item is created</span></span>
<span data-ttu-id="f1962-540">This operation triggers a flow when a new item is created in a SharePoint list.</span><span class="sxs-lookup"><span data-stu-id="f1962-540">This operation triggers a flow when a new item is created in a SharePoint list.</span></span> 

| <span data-ttu-id="f1962-541">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-541">Property Name</span></span> | <span data-ttu-id="f1962-542">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-542">Display Name</span></span> | <span data-ttu-id="f1962-543">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-543">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-544">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-544">dataset\*</span></span> |<span data-ttu-id="f1962-545">Site url</span><span class="sxs-lookup"><span data-stu-id="f1962-545">Site url</span></span> |<span data-ttu-id="f1962-546">SharePoint site url (example: http://contoso.sharepoint.com/sites/mysite)</span><span class="sxs-lookup"><span data-stu-id="f1962-546">SharePoint site url (example: http://contoso.sharepoint.com/sites/mysite)</span></span> |
| <span data-ttu-id="f1962-547">table\*</span><span class="sxs-lookup"><span data-stu-id="f1962-547">table\*</span></span> |<span data-ttu-id="f1962-548">List name</span><span class="sxs-lookup"><span data-stu-id="f1962-548">List name</span></span> |<span data-ttu-id="f1962-549">SharePoint list name</span><span class="sxs-lookup"><span data-stu-id="f1962-549">SharePoint list name</span></span> |
| <span data-ttu-id="f1962-550">$filter</span><span class="sxs-lookup"><span data-stu-id="f1962-550">$filter</span></span> |<span data-ttu-id="f1962-551">Filter Query</span><span class="sxs-lookup"><span data-stu-id="f1962-551">Filter Query</span></span> |<span data-ttu-id="f1962-552">An ODATA filter query to restrict the entries returned</span><span class="sxs-lookup"><span data-stu-id="f1962-552">An ODATA filter query to restrict the entries returned</span></span> |
| <span data-ttu-id="f1962-553">$orderby</span><span class="sxs-lookup"><span data-stu-id="f1962-553">$orderby</span></span> |<span data-ttu-id="f1962-554">Order By</span><span class="sxs-lookup"><span data-stu-id="f1962-554">Order By</span></span> |<span data-ttu-id="f1962-555">An ODATA orderBy query for specifying the order of entries</span><span class="sxs-lookup"><span data-stu-id="f1962-555">An ODATA orderBy query for specifying the order of entries</span></span> |
| <span data-ttu-id="f1962-556">$skip</span><span class="sxs-lookup"><span data-stu-id="f1962-556">$skip</span></span> |<span data-ttu-id="f1962-557">Skip Count</span><span class="sxs-lookup"><span data-stu-id="f1962-557">Skip Count</span></span> |<span data-ttu-id="f1962-558">Number of entries to skip (default = 0)</span><span class="sxs-lookup"><span data-stu-id="f1962-558">Number of entries to skip (default = 0)</span></span> |
| <span data-ttu-id="f1962-559">$top</span><span class="sxs-lookup"><span data-stu-id="f1962-559">$top</span></span> |<span data-ttu-id="f1962-560">Maximum Get Count</span><span class="sxs-lookup"><span data-stu-id="f1962-560">Maximum Get Count</span></span> |<span data-ttu-id="f1962-561">Maximum number of entries to retrieve (default = 256)</span><span class="sxs-lookup"><span data-stu-id="f1962-561">Maximum number of entries to retrieve (default = 256)</span></span> |

<span data-ttu-id="f1962-562">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-562">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="f1962-563">Output Details</span><span class="sxs-lookup"><span data-stu-id="f1962-563">Output Details</span></span>
<span data-ttu-id="f1962-564">ItemsList</span><span class="sxs-lookup"><span data-stu-id="f1962-564">ItemsList</span></span>

| <span data-ttu-id="f1962-565">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-565">Property Name</span></span> | <span data-ttu-id="f1962-566">Data Type</span><span class="sxs-lookup"><span data-stu-id="f1962-566">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="f1962-567">value</span><span class="sxs-lookup"><span data-stu-id="f1962-567">value</span></span> |<span data-ttu-id="f1962-568">array</span><span class="sxs-lookup"><span data-stu-id="f1962-568">array</span></span> |

### <a name="when-an-existing-item-is-modified"></a><span data-ttu-id="f1962-569">When an existing item is modified</span><span class="sxs-lookup"><span data-stu-id="f1962-569">When an existing item is modified</span></span>
<span data-ttu-id="f1962-570">This operation triggers a flow when an existing item is modified in a SharePoint list.</span><span class="sxs-lookup"><span data-stu-id="f1962-570">This operation triggers a flow when an existing item is modified in a SharePoint list.</span></span> 

| <span data-ttu-id="f1962-571">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-571">Property Name</span></span> | <span data-ttu-id="f1962-572">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-572">Display Name</span></span> | <span data-ttu-id="f1962-573">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-573">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-574">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-574">dataset\*</span></span> |<span data-ttu-id="f1962-575">Site url</span><span class="sxs-lookup"><span data-stu-id="f1962-575">Site url</span></span> |<span data-ttu-id="f1962-576">SharePoint site url (example: http://contoso.sharepoint.com/sites/mysite)</span><span class="sxs-lookup"><span data-stu-id="f1962-576">SharePoint site url (example: http://contoso.sharepoint.com/sites/mysite)</span></span> |
| <span data-ttu-id="f1962-577">table\*</span><span class="sxs-lookup"><span data-stu-id="f1962-577">table\*</span></span> |<span data-ttu-id="f1962-578">List name</span><span class="sxs-lookup"><span data-stu-id="f1962-578">List name</span></span> |<span data-ttu-id="f1962-579">SharePoint list name</span><span class="sxs-lookup"><span data-stu-id="f1962-579">SharePoint list name</span></span> |
| <span data-ttu-id="f1962-580">$filter</span><span class="sxs-lookup"><span data-stu-id="f1962-580">$filter</span></span> |<span data-ttu-id="f1962-581">Filter Query</span><span class="sxs-lookup"><span data-stu-id="f1962-581">Filter Query</span></span> |<span data-ttu-id="f1962-582">An ODATA filter query to restrict the entries returned</span><span class="sxs-lookup"><span data-stu-id="f1962-582">An ODATA filter query to restrict the entries returned</span></span> |
| <span data-ttu-id="f1962-583">$orderby</span><span class="sxs-lookup"><span data-stu-id="f1962-583">$orderby</span></span> |<span data-ttu-id="f1962-584">Order By</span><span class="sxs-lookup"><span data-stu-id="f1962-584">Order By</span></span> |<span data-ttu-id="f1962-585">An ODATA orderBy query for specifying the order of entries</span><span class="sxs-lookup"><span data-stu-id="f1962-585">An ODATA orderBy query for specifying the order of entries</span></span> |
| <span data-ttu-id="f1962-586">$skip</span><span class="sxs-lookup"><span data-stu-id="f1962-586">$skip</span></span> |<span data-ttu-id="f1962-587">Skip Count</span><span class="sxs-lookup"><span data-stu-id="f1962-587">Skip Count</span></span> |<span data-ttu-id="f1962-588">Number of entries to skip (default = 0)</span><span class="sxs-lookup"><span data-stu-id="f1962-588">Number of entries to skip (default = 0)</span></span> |
| <span data-ttu-id="f1962-589">$top</span><span class="sxs-lookup"><span data-stu-id="f1962-589">$top</span></span> |<span data-ttu-id="f1962-590">Maximum Get Count</span><span class="sxs-lookup"><span data-stu-id="f1962-590">Maximum Get Count</span></span> |<span data-ttu-id="f1962-591">Maximum number of entries to retrieve (default = 256)</span><span class="sxs-lookup"><span data-stu-id="f1962-591">Maximum number of entries to retrieve (default = 256)</span></span> |

<span data-ttu-id="f1962-592">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-592">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="f1962-593">Output Details</span><span class="sxs-lookup"><span data-stu-id="f1962-593">Output Details</span></span>
<span data-ttu-id="f1962-594">ItemsList</span><span class="sxs-lookup"><span data-stu-id="f1962-594">ItemsList</span></span>

| <span data-ttu-id="f1962-595">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-595">Property Name</span></span> | <span data-ttu-id="f1962-596">Data Type</span><span class="sxs-lookup"><span data-stu-id="f1962-596">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="f1962-597">value</span><span class="sxs-lookup"><span data-stu-id="f1962-597">value</span></span> |<span data-ttu-id="f1962-598">array</span><span class="sxs-lookup"><span data-stu-id="f1962-598">array</span></span> |

### <a name="get-items"></a><span data-ttu-id="f1962-599">Get items</span><span class="sxs-lookup"><span data-stu-id="f1962-599">Get items</span></span>
<span data-ttu-id="f1962-600">This operation gets items from a SharePoint list.</span><span class="sxs-lookup"><span data-stu-id="f1962-600">This operation gets items from a SharePoint list.</span></span> 

| <span data-ttu-id="f1962-601">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-601">Property Name</span></span> | <span data-ttu-id="f1962-602">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-602">Display Name</span></span> | <span data-ttu-id="f1962-603">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-603">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-604">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-604">dataset\*</span></span> |<span data-ttu-id="f1962-605">Site url</span><span class="sxs-lookup"><span data-stu-id="f1962-605">Site url</span></span> |<span data-ttu-id="f1962-606">SharePoint site url (example: http://contoso.sharepoint.com/sites/mysite)</span><span class="sxs-lookup"><span data-stu-id="f1962-606">SharePoint site url (example: http://contoso.sharepoint.com/sites/mysite)</span></span> |
| <span data-ttu-id="f1962-607">table\*</span><span class="sxs-lookup"><span data-stu-id="f1962-607">table\*</span></span> |<span data-ttu-id="f1962-608">List name</span><span class="sxs-lookup"><span data-stu-id="f1962-608">List name</span></span> |<span data-ttu-id="f1962-609">SharePoint list name</span><span class="sxs-lookup"><span data-stu-id="f1962-609">SharePoint list name</span></span> |
| <span data-ttu-id="f1962-610">$filter</span><span class="sxs-lookup"><span data-stu-id="f1962-610">$filter</span></span> |<span data-ttu-id="f1962-611">Filter Query</span><span class="sxs-lookup"><span data-stu-id="f1962-611">Filter Query</span></span> |<span data-ttu-id="f1962-612">An ODATA filter query to restrict the entries returned</span><span class="sxs-lookup"><span data-stu-id="f1962-612">An ODATA filter query to restrict the entries returned</span></span> |
| <span data-ttu-id="f1962-613">$orderby</span><span class="sxs-lookup"><span data-stu-id="f1962-613">$orderby</span></span> |<span data-ttu-id="f1962-614">Order By</span><span class="sxs-lookup"><span data-stu-id="f1962-614">Order By</span></span> |<span data-ttu-id="f1962-615">An ODATA orderBy query for specifying the order of entries</span><span class="sxs-lookup"><span data-stu-id="f1962-615">An ODATA orderBy query for specifying the order of entries</span></span> |
| <span data-ttu-id="f1962-616">$skip</span><span class="sxs-lookup"><span data-stu-id="f1962-616">$skip</span></span> |<span data-ttu-id="f1962-617">Skip Count</span><span class="sxs-lookup"><span data-stu-id="f1962-617">Skip Count</span></span> |<span data-ttu-id="f1962-618">Number of entries to skip (default = 0)</span><span class="sxs-lookup"><span data-stu-id="f1962-618">Number of entries to skip (default = 0)</span></span> |
| <span data-ttu-id="f1962-619">$top</span><span class="sxs-lookup"><span data-stu-id="f1962-619">$top</span></span> |<span data-ttu-id="f1962-620">Maximum Get Count</span><span class="sxs-lookup"><span data-stu-id="f1962-620">Maximum Get Count</span></span> |<span data-ttu-id="f1962-621">Maximum number of entries to retrieve (default = 256)</span><span class="sxs-lookup"><span data-stu-id="f1962-621">Maximum number of entries to retrieve (default = 256)</span></span> |

<span data-ttu-id="f1962-622">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-622">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="f1962-623">Output Details</span><span class="sxs-lookup"><span data-stu-id="f1962-623">Output Details</span></span>
<span data-ttu-id="f1962-624">ItemsList</span><span class="sxs-lookup"><span data-stu-id="f1962-624">ItemsList</span></span>

| <span data-ttu-id="f1962-625">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-625">Property Name</span></span> | <span data-ttu-id="f1962-626">Data Type</span><span class="sxs-lookup"><span data-stu-id="f1962-626">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="f1962-627">value</span><span class="sxs-lookup"><span data-stu-id="f1962-627">value</span></span> |<span data-ttu-id="f1962-628">array</span><span class="sxs-lookup"><span data-stu-id="f1962-628">array</span></span> |

### <a name="create-item"></a><span data-ttu-id="f1962-629">Create item</span><span class="sxs-lookup"><span data-stu-id="f1962-629">Create item</span></span>
<span data-ttu-id="f1962-630">This operation creates a new item in a SharePoint list.</span><span class="sxs-lookup"><span data-stu-id="f1962-630">This operation creates a new item in a SharePoint list.</span></span> 

| <span data-ttu-id="f1962-631">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-631">Property Name</span></span> | <span data-ttu-id="f1962-632">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-632">Display Name</span></span> | <span data-ttu-id="f1962-633">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-633">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-634">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-634">dataset\*</span></span> |<span data-ttu-id="f1962-635">Site url</span><span class="sxs-lookup"><span data-stu-id="f1962-635">Site url</span></span> |<span data-ttu-id="f1962-636">SharePoint site url (example: http://contoso.sharepoint.com/sites/mysite)</span><span class="sxs-lookup"><span data-stu-id="f1962-636">SharePoint site url (example: http://contoso.sharepoint.com/sites/mysite)</span></span> |
| <span data-ttu-id="f1962-637">table\*</span><span class="sxs-lookup"><span data-stu-id="f1962-637">table\*</span></span> |<span data-ttu-id="f1962-638">List name</span><span class="sxs-lookup"><span data-stu-id="f1962-638">List name</span></span> |<span data-ttu-id="f1962-639">SharePoint list name</span><span class="sxs-lookup"><span data-stu-id="f1962-639">SharePoint list name</span></span> |
| <span data-ttu-id="f1962-640">item\*</span><span class="sxs-lookup"><span data-stu-id="f1962-640">item\*</span></span> |<span data-ttu-id="f1962-641">Item</span><span class="sxs-lookup"><span data-stu-id="f1962-641">Item</span></span> |<span data-ttu-id="f1962-642">Item to create</span><span class="sxs-lookup"><span data-stu-id="f1962-642">Item to create</span></span> |

<span data-ttu-id="f1962-643">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-643">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="f1962-644">Output Details</span><span class="sxs-lookup"><span data-stu-id="f1962-644">Output Details</span></span>
<span data-ttu-id="f1962-645">Item</span><span class="sxs-lookup"><span data-stu-id="f1962-645">Item</span></span>

| <span data-ttu-id="f1962-646">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-646">Property Name</span></span> | <span data-ttu-id="f1962-647">Data Type</span><span class="sxs-lookup"><span data-stu-id="f1962-647">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="f1962-648">ItemInternalId</span><span class="sxs-lookup"><span data-stu-id="f1962-648">ItemInternalId</span></span> |<span data-ttu-id="f1962-649">string</span><span class="sxs-lookup"><span data-stu-id="f1962-649">string</span></span> |

### <a name="get-item"></a><span data-ttu-id="f1962-650">Get item</span><span class="sxs-lookup"><span data-stu-id="f1962-650">Get item</span></span>
<span data-ttu-id="f1962-651">This operation gets a single item by its id from a SharePoint list.</span><span class="sxs-lookup"><span data-stu-id="f1962-651">This operation gets a single item by its id from a SharePoint list.</span></span> 

| <span data-ttu-id="f1962-652">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-652">Property Name</span></span> | <span data-ttu-id="f1962-653">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-653">Display Name</span></span> | <span data-ttu-id="f1962-654">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-654">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-655">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-655">dataset\*</span></span> |<span data-ttu-id="f1962-656">Site url</span><span class="sxs-lookup"><span data-stu-id="f1962-656">Site url</span></span> |<span data-ttu-id="f1962-657">SharePoint site url (example: http://contoso.sharepoint.com/sites/mysite)</span><span class="sxs-lookup"><span data-stu-id="f1962-657">SharePoint site url (example: http://contoso.sharepoint.com/sites/mysite)</span></span> |
| <span data-ttu-id="f1962-658">table\*</span><span class="sxs-lookup"><span data-stu-id="f1962-658">table\*</span></span> |<span data-ttu-id="f1962-659">List name</span><span class="sxs-lookup"><span data-stu-id="f1962-659">List name</span></span> |<span data-ttu-id="f1962-660">SharePoint list name</span><span class="sxs-lookup"><span data-stu-id="f1962-660">SharePoint list name</span></span> |
| <span data-ttu-id="f1962-661">id\*</span><span class="sxs-lookup"><span data-stu-id="f1962-661">id\*</span></span> |<span data-ttu-id="f1962-662">Id</span><span class="sxs-lookup"><span data-stu-id="f1962-662">Id</span></span> |<span data-ttu-id="f1962-663">Unique identifier of item to be retrieved</span><span class="sxs-lookup"><span data-stu-id="f1962-663">Unique identifier of item to be retrieved</span></span> |

<span data-ttu-id="f1962-664">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-664">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="f1962-665">Output Details</span><span class="sxs-lookup"><span data-stu-id="f1962-665">Output Details</span></span>
<span data-ttu-id="f1962-666">Item</span><span class="sxs-lookup"><span data-stu-id="f1962-666">Item</span></span>

| <span data-ttu-id="f1962-667">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-667">Property Name</span></span> | <span data-ttu-id="f1962-668">Data Type</span><span class="sxs-lookup"><span data-stu-id="f1962-668">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="f1962-669">ItemInternalId</span><span class="sxs-lookup"><span data-stu-id="f1962-669">ItemInternalId</span></span> |<span data-ttu-id="f1962-670">string</span><span class="sxs-lookup"><span data-stu-id="f1962-670">string</span></span> |

### <a name="delete-item"></a><span data-ttu-id="f1962-671">Delete item</span><span class="sxs-lookup"><span data-stu-id="f1962-671">Delete item</span></span>
<span data-ttu-id="f1962-672">This operation deletes an item from a SharePoint list.</span><span class="sxs-lookup"><span data-stu-id="f1962-672">This operation deletes an item from a SharePoint list.</span></span> 

| <span data-ttu-id="f1962-673">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-673">Property Name</span></span> | <span data-ttu-id="f1962-674">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-674">Display Name</span></span> | <span data-ttu-id="f1962-675">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-675">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-676">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-676">dataset\*</span></span> |<span data-ttu-id="f1962-677">Site url</span><span class="sxs-lookup"><span data-stu-id="f1962-677">Site url</span></span> |<span data-ttu-id="f1962-678">SharePoint site url (example: http://contoso.sharepoint.com/sites/mysite)</span><span class="sxs-lookup"><span data-stu-id="f1962-678">SharePoint site url (example: http://contoso.sharepoint.com/sites/mysite)</span></span> |
| <span data-ttu-id="f1962-679">table\*</span><span class="sxs-lookup"><span data-stu-id="f1962-679">table\*</span></span> |<span data-ttu-id="f1962-680">List name</span><span class="sxs-lookup"><span data-stu-id="f1962-680">List name</span></span> |<span data-ttu-id="f1962-681">SharePoint list name</span><span class="sxs-lookup"><span data-stu-id="f1962-681">SharePoint list name</span></span> |
| <span data-ttu-id="f1962-682">id\*</span><span class="sxs-lookup"><span data-stu-id="f1962-682">id\*</span></span> |<span data-ttu-id="f1962-683">Id</span><span class="sxs-lookup"><span data-stu-id="f1962-683">Id</span></span> |<span data-ttu-id="f1962-684">Unique identifier of item to be deleted</span><span class="sxs-lookup"><span data-stu-id="f1962-684">Unique identifier of item to be deleted</span></span> |

<span data-ttu-id="f1962-685">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-685">An \* indicates that a property is required</span></span>

### <a name="update-item"></a><span data-ttu-id="f1962-686">Update item</span><span class="sxs-lookup"><span data-stu-id="f1962-686">Update item</span></span>
<span data-ttu-id="f1962-687">This operation updates an item in a SharePoint list.</span><span class="sxs-lookup"><span data-stu-id="f1962-687">This operation updates an item in a SharePoint list.</span></span> 

| <span data-ttu-id="f1962-688">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-688">Property Name</span></span> | <span data-ttu-id="f1962-689">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-689">Display Name</span></span> | <span data-ttu-id="f1962-690">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-690">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-691">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-691">dataset\*</span></span> |<span data-ttu-id="f1962-692">Site url</span><span class="sxs-lookup"><span data-stu-id="f1962-692">Site url</span></span> |<span data-ttu-id="f1962-693">SharePoint site url (example: http://contoso.sharepoint.com/sites/mysite)</span><span class="sxs-lookup"><span data-stu-id="f1962-693">SharePoint site url (example: http://contoso.sharepoint.com/sites/mysite)</span></span> |
| <span data-ttu-id="f1962-694">table\*</span><span class="sxs-lookup"><span data-stu-id="f1962-694">table\*</span></span> |<span data-ttu-id="f1962-695">List name</span><span class="sxs-lookup"><span data-stu-id="f1962-695">List name</span></span> |<span data-ttu-id="f1962-696">SharePoint list name</span><span class="sxs-lookup"><span data-stu-id="f1962-696">SharePoint list name</span></span> |
| <span data-ttu-id="f1962-697">id\*</span><span class="sxs-lookup"><span data-stu-id="f1962-697">id\*</span></span> |<span data-ttu-id="f1962-698">Id</span><span class="sxs-lookup"><span data-stu-id="f1962-698">Id</span></span> |<span data-ttu-id="f1962-699">Unique identifier of item to be updated</span><span class="sxs-lookup"><span data-stu-id="f1962-699">Unique identifier of item to be updated</span></span> |
| <span data-ttu-id="f1962-700">item\*</span><span class="sxs-lookup"><span data-stu-id="f1962-700">item\*</span></span> |<span data-ttu-id="f1962-701">Item</span><span class="sxs-lookup"><span data-stu-id="f1962-701">Item</span></span> |<span data-ttu-id="f1962-702">Item with changed properties</span><span class="sxs-lookup"><span data-stu-id="f1962-702">Item with changed properties</span></span> |

<span data-ttu-id="f1962-703">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-703">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="f1962-704">Output Details</span><span class="sxs-lookup"><span data-stu-id="f1962-704">Output Details</span></span>
<span data-ttu-id="f1962-705">Item</span><span class="sxs-lookup"><span data-stu-id="f1962-705">Item</span></span>

| <span data-ttu-id="f1962-706">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-706">Property Name</span></span> | <span data-ttu-id="f1962-707">Data Type</span><span class="sxs-lookup"><span data-stu-id="f1962-707">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="f1962-708">ItemInternalId</span><span class="sxs-lookup"><span data-stu-id="f1962-708">ItemInternalId</span></span> |<span data-ttu-id="f1962-709">string</span><span class="sxs-lookup"><span data-stu-id="f1962-709">string</span></span> |

### <a name="get-entity-values"></a><span data-ttu-id="f1962-710">Get entity values</span><span class="sxs-lookup"><span data-stu-id="f1962-710">Get entity values</span></span>
<span data-ttu-id="f1962-711">This operation gets possible values for a SharePoint entity.</span><span class="sxs-lookup"><span data-stu-id="f1962-711">This operation gets possible values for a SharePoint entity.</span></span> 

| <span data-ttu-id="f1962-712">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-712">Property Name</span></span> | <span data-ttu-id="f1962-713">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-713">Display Name</span></span> | <span data-ttu-id="f1962-714">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-714">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-715">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-715">dataset\*</span></span> |<span data-ttu-id="f1962-716">SharePoint site url</span><span class="sxs-lookup"><span data-stu-id="f1962-716">SharePoint site url</span></span> |<span data-ttu-id="f1962-717">SharePoint site url</span><span class="sxs-lookup"><span data-stu-id="f1962-717">SharePoint site url</span></span> |
| <span data-ttu-id="f1962-718">table\*</span><span class="sxs-lookup"><span data-stu-id="f1962-718">table\*</span></span> |<span data-ttu-id="f1962-719">table name</span><span class="sxs-lookup"><span data-stu-id="f1962-719">table name</span></span> |<span data-ttu-id="f1962-720">table name</span><span class="sxs-lookup"><span data-stu-id="f1962-720">table name</span></span> |
| <span data-ttu-id="f1962-721">id\*</span><span class="sxs-lookup"><span data-stu-id="f1962-721">id\*</span></span> |<span data-ttu-id="f1962-722">entity id</span><span class="sxs-lookup"><span data-stu-id="f1962-722">entity id</span></span> |<span data-ttu-id="f1962-723">entity id</span><span class="sxs-lookup"><span data-stu-id="f1962-723">entity id</span></span> |

<span data-ttu-id="f1962-724">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-724">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="f1962-725">Output Details</span><span class="sxs-lookup"><span data-stu-id="f1962-725">Output Details</span></span>
### <a name="get-lists"></a><span data-ttu-id="f1962-726">Get lists</span><span class="sxs-lookup"><span data-stu-id="f1962-726">Get lists</span></span>
<span data-ttu-id="f1962-727">This operation gets SharePoint lists from a site.</span><span class="sxs-lookup"><span data-stu-id="f1962-727">This operation gets SharePoint lists from a site.</span></span> 

| <span data-ttu-id="f1962-728">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-728">Property Name</span></span> | <span data-ttu-id="f1962-729">Display Name</span><span class="sxs-lookup"><span data-stu-id="f1962-729">Display Name</span></span> | <span data-ttu-id="f1962-730">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-730">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1962-731">dataset\*</span><span class="sxs-lookup"><span data-stu-id="f1962-731">dataset\*</span></span> |<span data-ttu-id="f1962-732">Site url</span><span class="sxs-lookup"><span data-stu-id="f1962-732">Site url</span></span> |<span data-ttu-id="f1962-733">SharePoint site url (example: http://contoso.sharepoint.com/sites/mysite)</span><span class="sxs-lookup"><span data-stu-id="f1962-733">SharePoint site url (example: http://contoso.sharepoint.com/sites/mysite)</span></span> |

<span data-ttu-id="f1962-734">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="f1962-734">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="f1962-735">Output Details</span><span class="sxs-lookup"><span data-stu-id="f1962-735">Output Details</span></span>
<span data-ttu-id="f1962-736">TablesList</span><span class="sxs-lookup"><span data-stu-id="f1962-736">TablesList</span></span>

| <span data-ttu-id="f1962-737">Property Name</span><span class="sxs-lookup"><span data-stu-id="f1962-737">Property Name</span></span> | <span data-ttu-id="f1962-738">Data Type</span><span class="sxs-lookup"><span data-stu-id="f1962-738">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="f1962-739">value</span><span class="sxs-lookup"><span data-stu-id="f1962-739">value</span></span> |<span data-ttu-id="f1962-740">array</span><span class="sxs-lookup"><span data-stu-id="f1962-740">array</span></span> |

## <a name="http-responses"></a><span data-ttu-id="f1962-741">HTTP responses</span><span class="sxs-lookup"><span data-stu-id="f1962-741">HTTP responses</span></span>
<span data-ttu-id="f1962-742">The actions and triggers above can return one or more of the following HTTP status codes:</span><span class="sxs-lookup"><span data-stu-id="f1962-742">The actions and triggers above can return one or more of the following HTTP status codes:</span></span> 

| <span data-ttu-id="f1962-743">Name</span><span class="sxs-lookup"><span data-stu-id="f1962-743">Name</span></span> | <span data-ttu-id="f1962-744">Description</span><span class="sxs-lookup"><span data-stu-id="f1962-744">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f1962-745">200</span><span class="sxs-lookup"><span data-stu-id="f1962-745">200</span></span> |<span data-ttu-id="f1962-746">OK</span><span class="sxs-lookup"><span data-stu-id="f1962-746">OK</span></span> |
| <span data-ttu-id="f1962-747">202</span><span class="sxs-lookup"><span data-stu-id="f1962-747">202</span></span> |<span data-ttu-id="f1962-748">Accepted</span><span class="sxs-lookup"><span data-stu-id="f1962-748">Accepted</span></span> |
| <span data-ttu-id="f1962-749">400</span><span class="sxs-lookup"><span data-stu-id="f1962-749">400</span></span> |<span data-ttu-id="f1962-750">Bad Request</span><span class="sxs-lookup"><span data-stu-id="f1962-750">Bad Request</span></span> |
| <span data-ttu-id="f1962-751">401</span><span class="sxs-lookup"><span data-stu-id="f1962-751">401</span></span> |<span data-ttu-id="f1962-752">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="f1962-752">Unauthorized</span></span> |
| <span data-ttu-id="f1962-753">403</span><span class="sxs-lookup"><span data-stu-id="f1962-753">403</span></span> |<span data-ttu-id="f1962-754">Forbidden</span><span class="sxs-lookup"><span data-stu-id="f1962-754">Forbidden</span></span> |
| <span data-ttu-id="f1962-755">404</span><span class="sxs-lookup"><span data-stu-id="f1962-755">404</span></span> |<span data-ttu-id="f1962-756">Not Found</span><span class="sxs-lookup"><span data-stu-id="f1962-756">Not Found</span></span> |
| <span data-ttu-id="f1962-757">500</span><span class="sxs-lookup"><span data-stu-id="f1962-757">500</span></span> |<span data-ttu-id="f1962-758">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="f1962-758">Internal Server Error.</span></span> <span data-ttu-id="f1962-759">Unknown error occurred.</span><span class="sxs-lookup"><span data-stu-id="f1962-759">Unknown error occurred.</span></span> |
| <span data-ttu-id="f1962-760">default</span><span class="sxs-lookup"><span data-stu-id="f1962-760">default</span></span> |<span data-ttu-id="f1962-761">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="f1962-761">Operation Failed.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f1962-762">Next Steps</span><span class="sxs-lookup"><span data-stu-id="f1962-762">Next Steps</span></span>
[<span data-ttu-id="f1962-763">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="f1962-763">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

