---
title: Learn how to use the SFTP connector in your logic apps | Microsoft Docs
description: Create logic apps with Azure App service. Connect to SFTP API to send and receive files. You can perform various operations such as create, update, get or delete files.
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: deonhe
ms.openlocfilehash: 2977404fb408ea5301c88caa7ce6767a906ca9c7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552504"
---
# <a name="get-started-with-the-sftp-connector"></a><span data-ttu-id="010dd-105">Get started with the SFTP connector</span><span class="sxs-lookup"><span data-stu-id="010dd-105">Get started with the SFTP connector</span></span>
<span data-ttu-id="010dd-106">Use the SFTP connector to access an SFTP account to send and receive files.</span><span class="sxs-lookup"><span data-stu-id="010dd-106">Use the SFTP connector to access an SFTP account to send and receive files.</span></span> <span data-ttu-id="010dd-107">You can perform various operations such as create, update, get or delete files.</span><span class="sxs-lookup"><span data-stu-id="010dd-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="010dd-108">To use [any connector](apis-list.md), you first need to create a logic app.</span><span class="sxs-lookup"><span data-stu-id="010dd-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="010dd-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="010dd-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-sftp"></a><span data-ttu-id="010dd-110">Connect to SFTP</span><span class="sxs-lookup"><span data-stu-id="010dd-110">Connect to SFTP</span></span>
<span data-ttu-id="010dd-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span><span class="sxs-lookup"><span data-stu-id="010dd-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="010dd-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span><span class="sxs-lookup"><span data-stu-id="010dd-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-sftp"></a><span data-ttu-id="010dd-113">Create a connection to SFTP</span><span class="sxs-lookup"><span data-stu-id="010dd-113">Create a connection to SFTP</span></span>
> [!INCLUDE [Steps to create a connection to SFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="010dd-114">Use an SFTP trigger</span><span class="sxs-lookup"><span data-stu-id="010dd-114">Use an SFTP trigger</span></span>
<span data-ttu-id="010dd-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="010dd-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="010dd-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="010dd-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="010dd-117">In this example, I will show you how to use the **SFTP - When a file is added or modified** trigger to initiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span><span class="sxs-lookup"><span data-stu-id="010dd-117">In this example, I will show you how to use the **SFTP - When a file is added or modified** trigger to initiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="010dd-118">In the example, you will also learn how to add a condition that checks the contents of the new or modified file and make a decision to extract the file if its contents indicate that it  should be extracted before using the contents.</span><span class="sxs-lookup"><span data-stu-id="010dd-118">In the example, you will also learn how to add a condition that checks the contents of the new or modified file and make a decision to extract the file if its contents indicate that it  should be extracted before using the contents.</span></span> <span data-ttu-id="010dd-119">Finally, you will learn how to add an action to extract the contents of a file and place the extracted contents in a folder on the SFTP server.</span><span class="sxs-lookup"><span data-stu-id="010dd-119">Finally, you will learn how to add an action to extract the contents of a file and place the extracted contents in a folder on the SFTP server.</span></span> 

<span data-ttu-id="010dd-120">In an enterprise example, you could use this trigger to monitor an SFTP folder for new files that represent orders from customers.</span><span class="sxs-lookup"><span data-stu-id="010dd-120">In an enterprise example, you could use this trigger to monitor an SFTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="010dd-121">You could then use an SFTP connector action such as **Get file content** to get the contents of the order for further processing and storage in your orders database.</span><span class="sxs-lookup"><span data-stu-id="010dd-121">You could then use an SFTP connector action such as **Get file content** to get the contents of the order for further processing and storage in your orders database.</span></span>

> [!INCLUDE [Steps to create an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="010dd-122">Add a condition</span><span class="sxs-lookup"><span data-stu-id="010dd-122">Add a condition</span></span>
> [!INCLUDE [Steps to add a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="010dd-123">Use an SFTP action</span><span class="sxs-lookup"><span data-stu-id="010dd-123">Use an SFTP action</span></span>
<span data-ttu-id="010dd-124">An action is an operation carried out by the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="010dd-124">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="010dd-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="010dd-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="technical-details"></a><span data-ttu-id="010dd-126">Technical Details</span><span class="sxs-lookup"><span data-stu-id="010dd-126">Technical Details</span></span>
<span data-ttu-id="010dd-127">Here are the details about the triggers, actions and responses that this connection supports:</span><span class="sxs-lookup"><span data-stu-id="010dd-127">Here are the details about the triggers, actions and responses that this connection supports:</span></span>

## <a name="sftp-triggers"></a><span data-ttu-id="010dd-128">SFTP triggers</span><span class="sxs-lookup"><span data-stu-id="010dd-128">SFTP triggers</span></span>
<span data-ttu-id="010dd-129">SFTP has the following trigger(s):</span><span class="sxs-lookup"><span data-stu-id="010dd-129">SFTP has the following trigger(s):</span></span>  

| <span data-ttu-id="010dd-130">Trigger</span><span class="sxs-lookup"><span data-stu-id="010dd-130">Trigger</span></span> | <span data-ttu-id="010dd-131">Description</span><span class="sxs-lookup"><span data-stu-id="010dd-131">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="010dd-132">When a file is added or modified</span><span class="sxs-lookup"><span data-stu-id="010dd-132">When a file is added or modified</span></span>](connectors-create-api-sftp.md#when-a-file-is-added-or-modified) |<span data-ttu-id="010dd-133">This operation triggers a flow when a file is added or modified in a folder.</span><span class="sxs-lookup"><span data-stu-id="010dd-133">This operation triggers a flow when a file is added or modified in a folder.</span></span> |

## <a name="sftp-actions"></a><span data-ttu-id="010dd-134">SFTP actions</span><span class="sxs-lookup"><span data-stu-id="010dd-134">SFTP actions</span></span>
<span data-ttu-id="010dd-135">SFTP has the following actions:</span><span class="sxs-lookup"><span data-stu-id="010dd-135">SFTP has the following actions:</span></span>

| <span data-ttu-id="010dd-136">Action</span><span class="sxs-lookup"><span data-stu-id="010dd-136">Action</span></span> | <span data-ttu-id="010dd-137">Description</span><span class="sxs-lookup"><span data-stu-id="010dd-137">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="010dd-138">Get file metadata</span><span class="sxs-lookup"><span data-stu-id="010dd-138">Get file metadata</span></span>](connectors-create-api-sftp.md#get-file-metadata) |<span data-ttu-id="010dd-139">This operation gets file metadata using the file id.</span><span class="sxs-lookup"><span data-stu-id="010dd-139">This operation gets file metadata using the file id.</span></span> |
| [<span data-ttu-id="010dd-140">Update file</span><span class="sxs-lookup"><span data-stu-id="010dd-140">Update file</span></span>](connectors-create-api-sftp.md#update-file) |<span data-ttu-id="010dd-141">This operation updates the file content.</span><span class="sxs-lookup"><span data-stu-id="010dd-141">This operation updates the file content.</span></span> |
| [<span data-ttu-id="010dd-142">Delete file</span><span class="sxs-lookup"><span data-stu-id="010dd-142">Delete file</span></span>](connectors-create-api-sftp.md#delete-file) |<span data-ttu-id="010dd-143">This operation deletes a file.</span><span class="sxs-lookup"><span data-stu-id="010dd-143">This operation deletes a file.</span></span> |
| [<span data-ttu-id="010dd-144">Get file metadata using path</span><span class="sxs-lookup"><span data-stu-id="010dd-144">Get file metadata using path</span></span>](connectors-create-api-sftp.md#get-file-metadata-using-path) |<span data-ttu-id="010dd-145">This operation gets file metadata using the file path.</span><span class="sxs-lookup"><span data-stu-id="010dd-145">This operation gets file metadata using the file path.</span></span> |
| [<span data-ttu-id="010dd-146">Get file content using path</span><span class="sxs-lookup"><span data-stu-id="010dd-146">Get file content using path</span></span>](connectors-create-api-sftp.md#get-file-content-using-path) |<span data-ttu-id="010dd-147">This operation gets file contents using the file path.</span><span class="sxs-lookup"><span data-stu-id="010dd-147">This operation gets file contents using the file path.</span></span> |
| [<span data-ttu-id="010dd-148">Get file content</span><span class="sxs-lookup"><span data-stu-id="010dd-148">Get file content</span></span>](connectors-create-api-sftp.md#get-file-content) |<span data-ttu-id="010dd-149">This operation gets file contents using the file id.</span><span class="sxs-lookup"><span data-stu-id="010dd-149">This operation gets file contents using the file id.</span></span> |
| [<span data-ttu-id="010dd-150">Create file</span><span class="sxs-lookup"><span data-stu-id="010dd-150">Create file</span></span>](connectors-create-api-sftp.md#create-file) |<span data-ttu-id="010dd-151">This operation uploads a file to an SFTP server.</span><span class="sxs-lookup"><span data-stu-id="010dd-151">This operation uploads a file to an SFTP server.</span></span> |
| [<span data-ttu-id="010dd-152">Copy file</span><span class="sxs-lookup"><span data-stu-id="010dd-152">Copy file</span></span>](connectors-create-api-sftp.md#copy-file) |<span data-ttu-id="010dd-153">This operation copies a file to an SFTP server.</span><span class="sxs-lookup"><span data-stu-id="010dd-153">This operation copies a file to an SFTP server.</span></span> |
| [<span data-ttu-id="010dd-154">List files in folder</span><span class="sxs-lookup"><span data-stu-id="010dd-154">List files in folder</span></span>](connectors-create-api-sftp.md#list-files-in-folder) |<span data-ttu-id="010dd-155">This operation gets files contained in a folder.</span><span class="sxs-lookup"><span data-stu-id="010dd-155">This operation gets files contained in a folder.</span></span> |
| [<span data-ttu-id="010dd-156">List files in root folder</span><span class="sxs-lookup"><span data-stu-id="010dd-156">List files in root folder</span></span>](connectors-create-api-sftp.md#list-files-in-root-folder) |<span data-ttu-id="010dd-157">This operation gets the files in the root folder.</span><span class="sxs-lookup"><span data-stu-id="010dd-157">This operation gets the files in the root folder.</span></span> |
| [<span data-ttu-id="010dd-158">Extract folder</span><span class="sxs-lookup"><span data-stu-id="010dd-158">Extract folder</span></span>](connectors-create-api-sftp.md#extract-folder) |<span data-ttu-id="010dd-159">This operation extracts an archive file into a folder (example: .zip).</span><span class="sxs-lookup"><span data-stu-id="010dd-159">This operation extracts an archive file into a folder (example: .zip).</span></span> |

### <a name="action-details"></a><span data-ttu-id="010dd-160">Action details</span><span class="sxs-lookup"><span data-stu-id="010dd-160">Action details</span></span>
<span data-ttu-id="010dd-161">Here are the details for the actions and triggers for this connector, along with their responses:</span><span class="sxs-lookup"><span data-stu-id="010dd-161">Here are the details for the actions and triggers for this connector, along with their responses:</span></span>

### <a name="get-file-metadata"></a><span data-ttu-id="010dd-162">Get file metadata</span><span class="sxs-lookup"><span data-stu-id="010dd-162">Get file metadata</span></span>
<span data-ttu-id="010dd-163">This operation gets file metadata using the file id.</span><span class="sxs-lookup"><span data-stu-id="010dd-163">This operation gets file metadata using the file id.</span></span> 

| <span data-ttu-id="010dd-164">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-164">Property Name</span></span> | <span data-ttu-id="010dd-165">Display Name</span><span class="sxs-lookup"><span data-stu-id="010dd-165">Display Name</span></span> | <span data-ttu-id="010dd-166">Description</span><span class="sxs-lookup"><span data-stu-id="010dd-166">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-167">id\*</span><span class="sxs-lookup"><span data-stu-id="010dd-167">id\*</span></span> |<span data-ttu-id="010dd-168">File</span><span class="sxs-lookup"><span data-stu-id="010dd-168">File</span></span> |<span data-ttu-id="010dd-169">Specify the file</span><span class="sxs-lookup"><span data-stu-id="010dd-169">Specify the file</span></span> |

<span data-ttu-id="010dd-170">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="010dd-170">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="010dd-171">Output Details</span><span class="sxs-lookup"><span data-stu-id="010dd-171">Output Details</span></span>
<span data-ttu-id="010dd-172">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="010dd-172">BlobMetadata</span></span>

| <span data-ttu-id="010dd-173">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-173">Property Name</span></span> | <span data-ttu-id="010dd-174">Data Type</span><span class="sxs-lookup"><span data-stu-id="010dd-174">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-175">Id</span><span class="sxs-lookup"><span data-stu-id="010dd-175">Id</span></span> |<span data-ttu-id="010dd-176">string</span><span class="sxs-lookup"><span data-stu-id="010dd-176">string</span></span> |
| <span data-ttu-id="010dd-177">Name</span><span class="sxs-lookup"><span data-stu-id="010dd-177">Name</span></span> |<span data-ttu-id="010dd-178">string</span><span class="sxs-lookup"><span data-stu-id="010dd-178">string</span></span> |
| <span data-ttu-id="010dd-179">DisplayName</span><span class="sxs-lookup"><span data-stu-id="010dd-179">DisplayName</span></span> |<span data-ttu-id="010dd-180">string</span><span class="sxs-lookup"><span data-stu-id="010dd-180">string</span></span> |
| <span data-ttu-id="010dd-181">Path</span><span class="sxs-lookup"><span data-stu-id="010dd-181">Path</span></span> |<span data-ttu-id="010dd-182">string</span><span class="sxs-lookup"><span data-stu-id="010dd-182">string</span></span> |
| <span data-ttu-id="010dd-183">LastModified</span><span class="sxs-lookup"><span data-stu-id="010dd-183">LastModified</span></span> |<span data-ttu-id="010dd-184">string</span><span class="sxs-lookup"><span data-stu-id="010dd-184">string</span></span> |
| <span data-ttu-id="010dd-185">Size</span><span class="sxs-lookup"><span data-stu-id="010dd-185">Size</span></span> |<span data-ttu-id="010dd-186">integer</span><span class="sxs-lookup"><span data-stu-id="010dd-186">integer</span></span> |
| <span data-ttu-id="010dd-187">MediaType</span><span class="sxs-lookup"><span data-stu-id="010dd-187">MediaType</span></span> |<span data-ttu-id="010dd-188">string</span><span class="sxs-lookup"><span data-stu-id="010dd-188">string</span></span> |
| <span data-ttu-id="010dd-189">IsFolder</span><span class="sxs-lookup"><span data-stu-id="010dd-189">IsFolder</span></span> |<span data-ttu-id="010dd-190">boolean</span><span class="sxs-lookup"><span data-stu-id="010dd-190">boolean</span></span> |
| <span data-ttu-id="010dd-191">ETag</span><span class="sxs-lookup"><span data-stu-id="010dd-191">ETag</span></span> |<span data-ttu-id="010dd-192">string</span><span class="sxs-lookup"><span data-stu-id="010dd-192">string</span></span> |
| <span data-ttu-id="010dd-193">FileLocator</span><span class="sxs-lookup"><span data-stu-id="010dd-193">FileLocator</span></span> |<span data-ttu-id="010dd-194">string</span><span class="sxs-lookup"><span data-stu-id="010dd-194">string</span></span> |

### <a name="update-file"></a><span data-ttu-id="010dd-195">Update file</span><span class="sxs-lookup"><span data-stu-id="010dd-195">Update file</span></span>
<span data-ttu-id="010dd-196">This operation updates the file content.</span><span class="sxs-lookup"><span data-stu-id="010dd-196">This operation updates the file content.</span></span> 

| <span data-ttu-id="010dd-197">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-197">Property Name</span></span> | <span data-ttu-id="010dd-198">Display Name</span><span class="sxs-lookup"><span data-stu-id="010dd-198">Display Name</span></span> | <span data-ttu-id="010dd-199">Description</span><span class="sxs-lookup"><span data-stu-id="010dd-199">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-200">id\*</span><span class="sxs-lookup"><span data-stu-id="010dd-200">id\*</span></span> |<span data-ttu-id="010dd-201">File</span><span class="sxs-lookup"><span data-stu-id="010dd-201">File</span></span> |<span data-ttu-id="010dd-202">Specify the file</span><span class="sxs-lookup"><span data-stu-id="010dd-202">Specify the file</span></span> |
| <span data-ttu-id="010dd-203">body\*</span><span class="sxs-lookup"><span data-stu-id="010dd-203">body\*</span></span> |<span data-ttu-id="010dd-204">File content</span><span class="sxs-lookup"><span data-stu-id="010dd-204">File content</span></span> |<span data-ttu-id="010dd-205">Content of the file to update</span><span class="sxs-lookup"><span data-stu-id="010dd-205">Content of the file to update</span></span> |

<span data-ttu-id="010dd-206">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="010dd-206">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="010dd-207">Output Details</span><span class="sxs-lookup"><span data-stu-id="010dd-207">Output Details</span></span>
<span data-ttu-id="010dd-208">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="010dd-208">BlobMetadata</span></span>

| <span data-ttu-id="010dd-209">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-209">Property Name</span></span> | <span data-ttu-id="010dd-210">Data Type</span><span class="sxs-lookup"><span data-stu-id="010dd-210">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-211">Id</span><span class="sxs-lookup"><span data-stu-id="010dd-211">Id</span></span> |<span data-ttu-id="010dd-212">string</span><span class="sxs-lookup"><span data-stu-id="010dd-212">string</span></span> |
| <span data-ttu-id="010dd-213">Name</span><span class="sxs-lookup"><span data-stu-id="010dd-213">Name</span></span> |<span data-ttu-id="010dd-214">string</span><span class="sxs-lookup"><span data-stu-id="010dd-214">string</span></span> |
| <span data-ttu-id="010dd-215">DisplayName</span><span class="sxs-lookup"><span data-stu-id="010dd-215">DisplayName</span></span> |<span data-ttu-id="010dd-216">string</span><span class="sxs-lookup"><span data-stu-id="010dd-216">string</span></span> |
| <span data-ttu-id="010dd-217">Path</span><span class="sxs-lookup"><span data-stu-id="010dd-217">Path</span></span> |<span data-ttu-id="010dd-218">string</span><span class="sxs-lookup"><span data-stu-id="010dd-218">string</span></span> |
| <span data-ttu-id="010dd-219">LastModified</span><span class="sxs-lookup"><span data-stu-id="010dd-219">LastModified</span></span> |<span data-ttu-id="010dd-220">string</span><span class="sxs-lookup"><span data-stu-id="010dd-220">string</span></span> |
| <span data-ttu-id="010dd-221">Size</span><span class="sxs-lookup"><span data-stu-id="010dd-221">Size</span></span> |<span data-ttu-id="010dd-222">integer</span><span class="sxs-lookup"><span data-stu-id="010dd-222">integer</span></span> |
| <span data-ttu-id="010dd-223">MediaType</span><span class="sxs-lookup"><span data-stu-id="010dd-223">MediaType</span></span> |<span data-ttu-id="010dd-224">string</span><span class="sxs-lookup"><span data-stu-id="010dd-224">string</span></span> |
| <span data-ttu-id="010dd-225">IsFolder</span><span class="sxs-lookup"><span data-stu-id="010dd-225">IsFolder</span></span> |<span data-ttu-id="010dd-226">boolean</span><span class="sxs-lookup"><span data-stu-id="010dd-226">boolean</span></span> |
| <span data-ttu-id="010dd-227">ETag</span><span class="sxs-lookup"><span data-stu-id="010dd-227">ETag</span></span> |<span data-ttu-id="010dd-228">string</span><span class="sxs-lookup"><span data-stu-id="010dd-228">string</span></span> |
| <span data-ttu-id="010dd-229">FileLocator</span><span class="sxs-lookup"><span data-stu-id="010dd-229">FileLocator</span></span> |<span data-ttu-id="010dd-230">string</span><span class="sxs-lookup"><span data-stu-id="010dd-230">string</span></span> |

### <a name="delete-file"></a><span data-ttu-id="010dd-231">Delete file</span><span class="sxs-lookup"><span data-stu-id="010dd-231">Delete file</span></span>
<span data-ttu-id="010dd-232">This operation deletes a file.</span><span class="sxs-lookup"><span data-stu-id="010dd-232">This operation deletes a file.</span></span> 

| <span data-ttu-id="010dd-233">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-233">Property Name</span></span> | <span data-ttu-id="010dd-234">Display Name</span><span class="sxs-lookup"><span data-stu-id="010dd-234">Display Name</span></span> | <span data-ttu-id="010dd-235">Description</span><span class="sxs-lookup"><span data-stu-id="010dd-235">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-236">id\*</span><span class="sxs-lookup"><span data-stu-id="010dd-236">id\*</span></span> |<span data-ttu-id="010dd-237">File</span><span class="sxs-lookup"><span data-stu-id="010dd-237">File</span></span> |<span data-ttu-id="010dd-238">Specify the file</span><span class="sxs-lookup"><span data-stu-id="010dd-238">Specify the file</span></span> |

<span data-ttu-id="010dd-239">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="010dd-239">An \* indicates that a property is required</span></span>

### <a name="get-file-metadata-using-path"></a><span data-ttu-id="010dd-240">Get file metadata using path</span><span class="sxs-lookup"><span data-stu-id="010dd-240">Get file metadata using path</span></span>
<span data-ttu-id="010dd-241">This operation gets file metadata using the file path.</span><span class="sxs-lookup"><span data-stu-id="010dd-241">This operation gets file metadata using the file path.</span></span> 

| <span data-ttu-id="010dd-242">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-242">Property Name</span></span> | <span data-ttu-id="010dd-243">Display Name</span><span class="sxs-lookup"><span data-stu-id="010dd-243">Display Name</span></span> | <span data-ttu-id="010dd-244">Description</span><span class="sxs-lookup"><span data-stu-id="010dd-244">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-245">path\*</span><span class="sxs-lookup"><span data-stu-id="010dd-245">path\*</span></span> |<span data-ttu-id="010dd-246">File path</span><span class="sxs-lookup"><span data-stu-id="010dd-246">File path</span></span> |<span data-ttu-id="010dd-247">Unique path of the file</span><span class="sxs-lookup"><span data-stu-id="010dd-247">Unique path of the file</span></span> |

<span data-ttu-id="010dd-248">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="010dd-248">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="010dd-249">Output Details</span><span class="sxs-lookup"><span data-stu-id="010dd-249">Output Details</span></span>
<span data-ttu-id="010dd-250">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="010dd-250">BlobMetadata</span></span>

| <span data-ttu-id="010dd-251">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-251">Property Name</span></span> | <span data-ttu-id="010dd-252">Data Type</span><span class="sxs-lookup"><span data-stu-id="010dd-252">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-253">Id</span><span class="sxs-lookup"><span data-stu-id="010dd-253">Id</span></span> |<span data-ttu-id="010dd-254">string</span><span class="sxs-lookup"><span data-stu-id="010dd-254">string</span></span> |
| <span data-ttu-id="010dd-255">Name</span><span class="sxs-lookup"><span data-stu-id="010dd-255">Name</span></span> |<span data-ttu-id="010dd-256">string</span><span class="sxs-lookup"><span data-stu-id="010dd-256">string</span></span> |
| <span data-ttu-id="010dd-257">DisplayName</span><span class="sxs-lookup"><span data-stu-id="010dd-257">DisplayName</span></span> |<span data-ttu-id="010dd-258">string</span><span class="sxs-lookup"><span data-stu-id="010dd-258">string</span></span> |
| <span data-ttu-id="010dd-259">Path</span><span class="sxs-lookup"><span data-stu-id="010dd-259">Path</span></span> |<span data-ttu-id="010dd-260">string</span><span class="sxs-lookup"><span data-stu-id="010dd-260">string</span></span> |
| <span data-ttu-id="010dd-261">LastModified</span><span class="sxs-lookup"><span data-stu-id="010dd-261">LastModified</span></span> |<span data-ttu-id="010dd-262">string</span><span class="sxs-lookup"><span data-stu-id="010dd-262">string</span></span> |
| <span data-ttu-id="010dd-263">Size</span><span class="sxs-lookup"><span data-stu-id="010dd-263">Size</span></span> |<span data-ttu-id="010dd-264">integer</span><span class="sxs-lookup"><span data-stu-id="010dd-264">integer</span></span> |
| <span data-ttu-id="010dd-265">MediaType</span><span class="sxs-lookup"><span data-stu-id="010dd-265">MediaType</span></span> |<span data-ttu-id="010dd-266">string</span><span class="sxs-lookup"><span data-stu-id="010dd-266">string</span></span> |
| <span data-ttu-id="010dd-267">IsFolder</span><span class="sxs-lookup"><span data-stu-id="010dd-267">IsFolder</span></span> |<span data-ttu-id="010dd-268">boolean</span><span class="sxs-lookup"><span data-stu-id="010dd-268">boolean</span></span> |
| <span data-ttu-id="010dd-269">ETag</span><span class="sxs-lookup"><span data-stu-id="010dd-269">ETag</span></span> |<span data-ttu-id="010dd-270">string</span><span class="sxs-lookup"><span data-stu-id="010dd-270">string</span></span> |
| <span data-ttu-id="010dd-271">FileLocator</span><span class="sxs-lookup"><span data-stu-id="010dd-271">FileLocator</span></span> |<span data-ttu-id="010dd-272">string</span><span class="sxs-lookup"><span data-stu-id="010dd-272">string</span></span> |

### <a name="get-file-content-using-path"></a><span data-ttu-id="010dd-273">Get file content using path</span><span class="sxs-lookup"><span data-stu-id="010dd-273">Get file content using path</span></span>
<span data-ttu-id="010dd-274">This operation gets file contents using the file path.</span><span class="sxs-lookup"><span data-stu-id="010dd-274">This operation gets file contents using the file path.</span></span> 

| <span data-ttu-id="010dd-275">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-275">Property Name</span></span> | <span data-ttu-id="010dd-276">Display Name</span><span class="sxs-lookup"><span data-stu-id="010dd-276">Display Name</span></span> | <span data-ttu-id="010dd-277">Description</span><span class="sxs-lookup"><span data-stu-id="010dd-277">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-278">path\*</span><span class="sxs-lookup"><span data-stu-id="010dd-278">path\*</span></span> |<span data-ttu-id="010dd-279">File path</span><span class="sxs-lookup"><span data-stu-id="010dd-279">File path</span></span> |<span data-ttu-id="010dd-280">Unique path of the file</span><span class="sxs-lookup"><span data-stu-id="010dd-280">Unique path of the file</span></span> |

<span data-ttu-id="010dd-281">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="010dd-281">An \* indicates that a property is required</span></span>

### <a name="get-file-content"></a><span data-ttu-id="010dd-282">Get file content</span><span class="sxs-lookup"><span data-stu-id="010dd-282">Get file content</span></span>
<span data-ttu-id="010dd-283">This operation gets file contents using the file id.</span><span class="sxs-lookup"><span data-stu-id="010dd-283">This operation gets file contents using the file id.</span></span> 

| <span data-ttu-id="010dd-284">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-284">Property Name</span></span> | <span data-ttu-id="010dd-285">Display Name</span><span class="sxs-lookup"><span data-stu-id="010dd-285">Display Name</span></span> | <span data-ttu-id="010dd-286">Description</span><span class="sxs-lookup"><span data-stu-id="010dd-286">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-287">id\*</span><span class="sxs-lookup"><span data-stu-id="010dd-287">id\*</span></span> |<span data-ttu-id="010dd-288">File</span><span class="sxs-lookup"><span data-stu-id="010dd-288">File</span></span> |<span data-ttu-id="010dd-289">Specify the file</span><span class="sxs-lookup"><span data-stu-id="010dd-289">Specify the file</span></span> |

<span data-ttu-id="010dd-290">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="010dd-290">An \* indicates that a property is required</span></span>

### <a name="create-file"></a><span data-ttu-id="010dd-291">Create file</span><span class="sxs-lookup"><span data-stu-id="010dd-291">Create file</span></span>
<span data-ttu-id="010dd-292">This operation uploads a file to an SFTP server.</span><span class="sxs-lookup"><span data-stu-id="010dd-292">This operation uploads a file to an SFTP server.</span></span> 

| <span data-ttu-id="010dd-293">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-293">Property Name</span></span> | <span data-ttu-id="010dd-294">Display Name</span><span class="sxs-lookup"><span data-stu-id="010dd-294">Display Name</span></span> | <span data-ttu-id="010dd-295">Description</span><span class="sxs-lookup"><span data-stu-id="010dd-295">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-296">folderPath\*</span><span class="sxs-lookup"><span data-stu-id="010dd-296">folderPath\*</span></span> |<span data-ttu-id="010dd-297">Folder path</span><span class="sxs-lookup"><span data-stu-id="010dd-297">Folder path</span></span> |<span data-ttu-id="010dd-298">Unique path of the folder</span><span class="sxs-lookup"><span data-stu-id="010dd-298">Unique path of the folder</span></span> |
| <span data-ttu-id="010dd-299">name\*</span><span class="sxs-lookup"><span data-stu-id="010dd-299">name\*</span></span> |<span data-ttu-id="010dd-300">File name</span><span class="sxs-lookup"><span data-stu-id="010dd-300">File name</span></span> |<span data-ttu-id="010dd-301">Name of the file</span><span class="sxs-lookup"><span data-stu-id="010dd-301">Name of the file</span></span> |
| <span data-ttu-id="010dd-302">body\*</span><span class="sxs-lookup"><span data-stu-id="010dd-302">body\*</span></span> |<span data-ttu-id="010dd-303">File content</span><span class="sxs-lookup"><span data-stu-id="010dd-303">File content</span></span> |<span data-ttu-id="010dd-304">Content of the file to create</span><span class="sxs-lookup"><span data-stu-id="010dd-304">Content of the file to create</span></span> |

<span data-ttu-id="010dd-305">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="010dd-305">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="010dd-306">Output Details</span><span class="sxs-lookup"><span data-stu-id="010dd-306">Output Details</span></span>
<span data-ttu-id="010dd-307">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="010dd-307">BlobMetadata</span></span>

|  | <span data-ttu-id="010dd-308">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-308">Property Name</span></span> | <span data-ttu-id="010dd-309">Data Type</span><span class="sxs-lookup"><span data-stu-id="010dd-309">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-310">Id</span><span class="sxs-lookup"><span data-stu-id="010dd-310">Id</span></span> |<span data-ttu-id="010dd-311">string</span><span class="sxs-lookup"><span data-stu-id="010dd-311">string</span></span> | |
| <span data-ttu-id="010dd-312">Name</span><span class="sxs-lookup"><span data-stu-id="010dd-312">Name</span></span> |<span data-ttu-id="010dd-313">string</span><span class="sxs-lookup"><span data-stu-id="010dd-313">string</span></span> | |
| <span data-ttu-id="010dd-314">DisplayName</span><span class="sxs-lookup"><span data-stu-id="010dd-314">DisplayName</span></span> |<span data-ttu-id="010dd-315">string</span><span class="sxs-lookup"><span data-stu-id="010dd-315">string</span></span> | |
| <span data-ttu-id="010dd-316">Path</span><span class="sxs-lookup"><span data-stu-id="010dd-316">Path</span></span> |<span data-ttu-id="010dd-317">string</span><span class="sxs-lookup"><span data-stu-id="010dd-317">string</span></span> | |
| <span data-ttu-id="010dd-318">LastModified</span><span class="sxs-lookup"><span data-stu-id="010dd-318">LastModified</span></span> |<span data-ttu-id="010dd-319">string</span><span class="sxs-lookup"><span data-stu-id="010dd-319">string</span></span> | |
| <span data-ttu-id="010dd-320">Size</span><span class="sxs-lookup"><span data-stu-id="010dd-320">Size</span></span> |<span data-ttu-id="010dd-321">integer</span><span class="sxs-lookup"><span data-stu-id="010dd-321">integer</span></span> | |
| <span data-ttu-id="010dd-322">MediaType</span><span class="sxs-lookup"><span data-stu-id="010dd-322">MediaType</span></span> |<span data-ttu-id="010dd-323">string</span><span class="sxs-lookup"><span data-stu-id="010dd-323">string</span></span> | |
| <span data-ttu-id="010dd-324">IsFolder</span><span class="sxs-lookup"><span data-stu-id="010dd-324">IsFolder</span></span> |<span data-ttu-id="010dd-325">boolean</span><span class="sxs-lookup"><span data-stu-id="010dd-325">boolean</span></span> | |
| <span data-ttu-id="010dd-326">ETag</span><span class="sxs-lookup"><span data-stu-id="010dd-326">ETag</span></span> |<span data-ttu-id="010dd-327">string</span><span class="sxs-lookup"><span data-stu-id="010dd-327">string</span></span> | |
| <span data-ttu-id="010dd-328">FileLocator</span><span class="sxs-lookup"><span data-stu-id="010dd-328">FileLocator</span></span> |<span data-ttu-id="010dd-329">string</span><span class="sxs-lookup"><span data-stu-id="010dd-329">string</span></span> | |

### <a name="copy-file"></a><span data-ttu-id="010dd-330">Copy file</span><span class="sxs-lookup"><span data-stu-id="010dd-330">Copy file</span></span>
<span data-ttu-id="010dd-331">This operation copies a file to an SFTP server.</span><span class="sxs-lookup"><span data-stu-id="010dd-331">This operation copies a file to an SFTP server.</span></span> 

| <span data-ttu-id="010dd-332">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-332">Property Name</span></span> | <span data-ttu-id="010dd-333">Display Name</span><span class="sxs-lookup"><span data-stu-id="010dd-333">Display Name</span></span> | <span data-ttu-id="010dd-334">Description</span><span class="sxs-lookup"><span data-stu-id="010dd-334">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-335">source\*</span><span class="sxs-lookup"><span data-stu-id="010dd-335">source\*</span></span> |<span data-ttu-id="010dd-336">Source file path</span><span class="sxs-lookup"><span data-stu-id="010dd-336">Source file path</span></span> |<span data-ttu-id="010dd-337">Path to the source file</span><span class="sxs-lookup"><span data-stu-id="010dd-337">Path to the source file</span></span> |
| <span data-ttu-id="010dd-338">destination\*</span><span class="sxs-lookup"><span data-stu-id="010dd-338">destination\*</span></span> |<span data-ttu-id="010dd-339">Destination file path</span><span class="sxs-lookup"><span data-stu-id="010dd-339">Destination file path</span></span> |<span data-ttu-id="010dd-340">Path to the destination file, including file name</span><span class="sxs-lookup"><span data-stu-id="010dd-340">Path to the destination file, including file name</span></span> |
| <span data-ttu-id="010dd-341">overwrite</span><span class="sxs-lookup"><span data-stu-id="010dd-341">overwrite</span></span> |<span data-ttu-id="010dd-342">Overwrite?</span><span class="sxs-lookup"><span data-stu-id="010dd-342">Overwrite?</span></span> |<span data-ttu-id="010dd-343">Overwrites the destination file if set to 'true'</span><span class="sxs-lookup"><span data-stu-id="010dd-343">Overwrites the destination file if set to 'true'</span></span> |

<span data-ttu-id="010dd-344">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="010dd-344">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="010dd-345">Output Details</span><span class="sxs-lookup"><span data-stu-id="010dd-345">Output Details</span></span>
<span data-ttu-id="010dd-346">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="010dd-346">BlobMetadata</span></span>

| <span data-ttu-id="010dd-347">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-347">Property Name</span></span> | <span data-ttu-id="010dd-348">Data Type</span><span class="sxs-lookup"><span data-stu-id="010dd-348">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-349">Id</span><span class="sxs-lookup"><span data-stu-id="010dd-349">Id</span></span> |<span data-ttu-id="010dd-350">string</span><span class="sxs-lookup"><span data-stu-id="010dd-350">string</span></span> |
| <span data-ttu-id="010dd-351">Name</span><span class="sxs-lookup"><span data-stu-id="010dd-351">Name</span></span> |<span data-ttu-id="010dd-352">string</span><span class="sxs-lookup"><span data-stu-id="010dd-352">string</span></span> |
| <span data-ttu-id="010dd-353">DisplayName</span><span class="sxs-lookup"><span data-stu-id="010dd-353">DisplayName</span></span> |<span data-ttu-id="010dd-354">string</span><span class="sxs-lookup"><span data-stu-id="010dd-354">string</span></span> |
| <span data-ttu-id="010dd-355">Path</span><span class="sxs-lookup"><span data-stu-id="010dd-355">Path</span></span> |<span data-ttu-id="010dd-356">string</span><span class="sxs-lookup"><span data-stu-id="010dd-356">string</span></span> |
| <span data-ttu-id="010dd-357">LastModified</span><span class="sxs-lookup"><span data-stu-id="010dd-357">LastModified</span></span> |<span data-ttu-id="010dd-358">string</span><span class="sxs-lookup"><span data-stu-id="010dd-358">string</span></span> |
| <span data-ttu-id="010dd-359">Size</span><span class="sxs-lookup"><span data-stu-id="010dd-359">Size</span></span> |<span data-ttu-id="010dd-360">integer</span><span class="sxs-lookup"><span data-stu-id="010dd-360">integer</span></span> |
| <span data-ttu-id="010dd-361">MediaType</span><span class="sxs-lookup"><span data-stu-id="010dd-361">MediaType</span></span> |<span data-ttu-id="010dd-362">string</span><span class="sxs-lookup"><span data-stu-id="010dd-362">string</span></span> |
| <span data-ttu-id="010dd-363">IsFolder</span><span class="sxs-lookup"><span data-stu-id="010dd-363">IsFolder</span></span> |<span data-ttu-id="010dd-364">boolean</span><span class="sxs-lookup"><span data-stu-id="010dd-364">boolean</span></span> |
| <span data-ttu-id="010dd-365">ETag</span><span class="sxs-lookup"><span data-stu-id="010dd-365">ETag</span></span> |<span data-ttu-id="010dd-366">string</span><span class="sxs-lookup"><span data-stu-id="010dd-366">string</span></span> |
| <span data-ttu-id="010dd-367">FileLocator</span><span class="sxs-lookup"><span data-stu-id="010dd-367">FileLocator</span></span> |<span data-ttu-id="010dd-368">string</span><span class="sxs-lookup"><span data-stu-id="010dd-368">string</span></span> |

### <a name="when-a-file-is-added-or-modified"></a><span data-ttu-id="010dd-369">When a file is added or modified</span><span class="sxs-lookup"><span data-stu-id="010dd-369">When a file is added or modified</span></span>
<span data-ttu-id="010dd-370">This operation triggers a flow when a file is added or modified in a folder.</span><span class="sxs-lookup"><span data-stu-id="010dd-370">This operation triggers a flow when a file is added or modified in a folder.</span></span> 

| <span data-ttu-id="010dd-371">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-371">Property Name</span></span> | <span data-ttu-id="010dd-372">Display Name</span><span class="sxs-lookup"><span data-stu-id="010dd-372">Display Name</span></span> | <span data-ttu-id="010dd-373">Description</span><span class="sxs-lookup"><span data-stu-id="010dd-373">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-374">folderId\*</span><span class="sxs-lookup"><span data-stu-id="010dd-374">folderId\*</span></span> |<span data-ttu-id="010dd-375">Folder</span><span class="sxs-lookup"><span data-stu-id="010dd-375">Folder</span></span> |<span data-ttu-id="010dd-376">Specify a folder</span><span class="sxs-lookup"><span data-stu-id="010dd-376">Specify a folder</span></span> |

<span data-ttu-id="010dd-377">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="010dd-377">An \* indicates that a property is required</span></span>

### <a name="list-files-in-folder"></a><span data-ttu-id="010dd-378">List files in folder</span><span class="sxs-lookup"><span data-stu-id="010dd-378">List files in folder</span></span>
<span data-ttu-id="010dd-379">This operation gets files contained in a folder.</span><span class="sxs-lookup"><span data-stu-id="010dd-379">This operation gets files contained in a folder.</span></span> 

| <span data-ttu-id="010dd-380">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-380">Property Name</span></span> | <span data-ttu-id="010dd-381">Display Name</span><span class="sxs-lookup"><span data-stu-id="010dd-381">Display Name</span></span> | <span data-ttu-id="010dd-382">Description</span><span class="sxs-lookup"><span data-stu-id="010dd-382">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-383">id\*</span><span class="sxs-lookup"><span data-stu-id="010dd-383">id\*</span></span> |<span data-ttu-id="010dd-384">Folder</span><span class="sxs-lookup"><span data-stu-id="010dd-384">Folder</span></span> |<span data-ttu-id="010dd-385">Specify the folder</span><span class="sxs-lookup"><span data-stu-id="010dd-385">Specify the folder</span></span> |

<span data-ttu-id="010dd-386">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="010dd-386">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="010dd-387">Output Details</span><span class="sxs-lookup"><span data-stu-id="010dd-387">Output Details</span></span>
<span data-ttu-id="010dd-388">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="010dd-388">BlobMetadata</span></span>

| <span data-ttu-id="010dd-389">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-389">Property Name</span></span> | <span data-ttu-id="010dd-390">Data Type</span><span class="sxs-lookup"><span data-stu-id="010dd-390">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-391">Id</span><span class="sxs-lookup"><span data-stu-id="010dd-391">Id</span></span> |<span data-ttu-id="010dd-392">string</span><span class="sxs-lookup"><span data-stu-id="010dd-392">string</span></span> |
| <span data-ttu-id="010dd-393">Name</span><span class="sxs-lookup"><span data-stu-id="010dd-393">Name</span></span> |<span data-ttu-id="010dd-394">string</span><span class="sxs-lookup"><span data-stu-id="010dd-394">string</span></span> |
| <span data-ttu-id="010dd-395">DisplayName</span><span class="sxs-lookup"><span data-stu-id="010dd-395">DisplayName</span></span> |<span data-ttu-id="010dd-396">string</span><span class="sxs-lookup"><span data-stu-id="010dd-396">string</span></span> |
| <span data-ttu-id="010dd-397">Path</span><span class="sxs-lookup"><span data-stu-id="010dd-397">Path</span></span> |<span data-ttu-id="010dd-398">string</span><span class="sxs-lookup"><span data-stu-id="010dd-398">string</span></span> |
| <span data-ttu-id="010dd-399">LastModified</span><span class="sxs-lookup"><span data-stu-id="010dd-399">LastModified</span></span> |<span data-ttu-id="010dd-400">string</span><span class="sxs-lookup"><span data-stu-id="010dd-400">string</span></span> |
| <span data-ttu-id="010dd-401">Size</span><span class="sxs-lookup"><span data-stu-id="010dd-401">Size</span></span> |<span data-ttu-id="010dd-402">integer</span><span class="sxs-lookup"><span data-stu-id="010dd-402">integer</span></span> |
| <span data-ttu-id="010dd-403">MediaType</span><span class="sxs-lookup"><span data-stu-id="010dd-403">MediaType</span></span> |<span data-ttu-id="010dd-404">string</span><span class="sxs-lookup"><span data-stu-id="010dd-404">string</span></span> |
| <span data-ttu-id="010dd-405">IsFolder</span><span class="sxs-lookup"><span data-stu-id="010dd-405">IsFolder</span></span> |<span data-ttu-id="010dd-406">boolean</span><span class="sxs-lookup"><span data-stu-id="010dd-406">boolean</span></span> |
| <span data-ttu-id="010dd-407">ETag</span><span class="sxs-lookup"><span data-stu-id="010dd-407">ETag</span></span> |<span data-ttu-id="010dd-408">string</span><span class="sxs-lookup"><span data-stu-id="010dd-408">string</span></span> |
| <span data-ttu-id="010dd-409">FileLocator</span><span class="sxs-lookup"><span data-stu-id="010dd-409">FileLocator</span></span> |<span data-ttu-id="010dd-410">string</span><span class="sxs-lookup"><span data-stu-id="010dd-410">string</span></span> |

### <a name="list-files-in-root-folder"></a><span data-ttu-id="010dd-411">List files in root folder</span><span class="sxs-lookup"><span data-stu-id="010dd-411">List files in root folder</span></span>
<span data-ttu-id="010dd-412">This operation gets the files in the root folder.</span><span class="sxs-lookup"><span data-stu-id="010dd-412">This operation gets the files in the root folder.</span></span> 

<span data-ttu-id="010dd-413">There are no parameters for this call</span><span class="sxs-lookup"><span data-stu-id="010dd-413">There are no parameters for this call</span></span>

#### <a name="output-details"></a><span data-ttu-id="010dd-414">Output Details</span><span class="sxs-lookup"><span data-stu-id="010dd-414">Output Details</span></span>
<span data-ttu-id="010dd-415">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="010dd-415">BlobMetadata</span></span>

| <span data-ttu-id="010dd-416">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-416">Property Name</span></span> | <span data-ttu-id="010dd-417">Data Type</span><span class="sxs-lookup"><span data-stu-id="010dd-417">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-418">Id</span><span class="sxs-lookup"><span data-stu-id="010dd-418">Id</span></span> |<span data-ttu-id="010dd-419">string</span><span class="sxs-lookup"><span data-stu-id="010dd-419">string</span></span> |
| <span data-ttu-id="010dd-420">Name</span><span class="sxs-lookup"><span data-stu-id="010dd-420">Name</span></span> |<span data-ttu-id="010dd-421">string</span><span class="sxs-lookup"><span data-stu-id="010dd-421">string</span></span> |
| <span data-ttu-id="010dd-422">DisplayName</span><span class="sxs-lookup"><span data-stu-id="010dd-422">DisplayName</span></span> |<span data-ttu-id="010dd-423">string</span><span class="sxs-lookup"><span data-stu-id="010dd-423">string</span></span> |
| <span data-ttu-id="010dd-424">Path</span><span class="sxs-lookup"><span data-stu-id="010dd-424">Path</span></span> |<span data-ttu-id="010dd-425">string</span><span class="sxs-lookup"><span data-stu-id="010dd-425">string</span></span> |
| <span data-ttu-id="010dd-426">LastModified</span><span class="sxs-lookup"><span data-stu-id="010dd-426">LastModified</span></span> |<span data-ttu-id="010dd-427">string</span><span class="sxs-lookup"><span data-stu-id="010dd-427">string</span></span> |
| <span data-ttu-id="010dd-428">Size</span><span class="sxs-lookup"><span data-stu-id="010dd-428">Size</span></span> |<span data-ttu-id="010dd-429">integer</span><span class="sxs-lookup"><span data-stu-id="010dd-429">integer</span></span> |
| <span data-ttu-id="010dd-430">MediaType</span><span class="sxs-lookup"><span data-stu-id="010dd-430">MediaType</span></span> |<span data-ttu-id="010dd-431">string</span><span class="sxs-lookup"><span data-stu-id="010dd-431">string</span></span> |
| <span data-ttu-id="010dd-432">IsFolder</span><span class="sxs-lookup"><span data-stu-id="010dd-432">IsFolder</span></span> |<span data-ttu-id="010dd-433">boolean</span><span class="sxs-lookup"><span data-stu-id="010dd-433">boolean</span></span> |
| <span data-ttu-id="010dd-434">ETag</span><span class="sxs-lookup"><span data-stu-id="010dd-434">ETag</span></span> |<span data-ttu-id="010dd-435">string</span><span class="sxs-lookup"><span data-stu-id="010dd-435">string</span></span> |
| <span data-ttu-id="010dd-436">FileLocator</span><span class="sxs-lookup"><span data-stu-id="010dd-436">FileLocator</span></span> |<span data-ttu-id="010dd-437">string</span><span class="sxs-lookup"><span data-stu-id="010dd-437">string</span></span> |

### <a name="extract-folder"></a><span data-ttu-id="010dd-438">Extract folder</span><span class="sxs-lookup"><span data-stu-id="010dd-438">Extract folder</span></span>
<span data-ttu-id="010dd-439">This operation extracts an archive file into a folder (example: .zip).</span><span class="sxs-lookup"><span data-stu-id="010dd-439">This operation extracts an archive file into a folder (example: .zip).</span></span> 

| <span data-ttu-id="010dd-440">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-440">Property Name</span></span> | <span data-ttu-id="010dd-441">Display Name</span><span class="sxs-lookup"><span data-stu-id="010dd-441">Display Name</span></span> | <span data-ttu-id="010dd-442">Description</span><span class="sxs-lookup"><span data-stu-id="010dd-442">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-443">source\*</span><span class="sxs-lookup"><span data-stu-id="010dd-443">source\*</span></span> |<span data-ttu-id="010dd-444">Source archive file path</span><span class="sxs-lookup"><span data-stu-id="010dd-444">Source archive file path</span></span> |<span data-ttu-id="010dd-445">Path to the archive file</span><span class="sxs-lookup"><span data-stu-id="010dd-445">Path to the archive file</span></span> |
| <span data-ttu-id="010dd-446">destination\*</span><span class="sxs-lookup"><span data-stu-id="010dd-446">destination\*</span></span> |<span data-ttu-id="010dd-447">Destination folder path</span><span class="sxs-lookup"><span data-stu-id="010dd-447">Destination folder path</span></span> |<span data-ttu-id="010dd-448">Path to the destination folder</span><span class="sxs-lookup"><span data-stu-id="010dd-448">Path to the destination folder</span></span> |
| <span data-ttu-id="010dd-449">overwrite</span><span class="sxs-lookup"><span data-stu-id="010dd-449">overwrite</span></span> |<span data-ttu-id="010dd-450">Overwrite?</span><span class="sxs-lookup"><span data-stu-id="010dd-450">Overwrite?</span></span> |<span data-ttu-id="010dd-451">Overwrites the destination files if set to 'true'</span><span class="sxs-lookup"><span data-stu-id="010dd-451">Overwrites the destination files if set to 'true'</span></span> |

<span data-ttu-id="010dd-452">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="010dd-452">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="010dd-453">Output Details</span><span class="sxs-lookup"><span data-stu-id="010dd-453">Output Details</span></span>
<span data-ttu-id="010dd-454">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="010dd-454">BlobMetadata</span></span>

| <span data-ttu-id="010dd-455">Property Name</span><span class="sxs-lookup"><span data-stu-id="010dd-455">Property Name</span></span> | <span data-ttu-id="010dd-456">Data Type</span><span class="sxs-lookup"><span data-stu-id="010dd-456">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010dd-457">Id</span><span class="sxs-lookup"><span data-stu-id="010dd-457">Id</span></span> |<span data-ttu-id="010dd-458">string</span><span class="sxs-lookup"><span data-stu-id="010dd-458">string</span></span> |
| <span data-ttu-id="010dd-459">Name</span><span class="sxs-lookup"><span data-stu-id="010dd-459">Name</span></span> |<span data-ttu-id="010dd-460">string</span><span class="sxs-lookup"><span data-stu-id="010dd-460">string</span></span> |
| <span data-ttu-id="010dd-461">DisplayName</span><span class="sxs-lookup"><span data-stu-id="010dd-461">DisplayName</span></span> |<span data-ttu-id="010dd-462">string</span><span class="sxs-lookup"><span data-stu-id="010dd-462">string</span></span> |
| <span data-ttu-id="010dd-463">Path</span><span class="sxs-lookup"><span data-stu-id="010dd-463">Path</span></span> |<span data-ttu-id="010dd-464">string</span><span class="sxs-lookup"><span data-stu-id="010dd-464">string</span></span> |
| <span data-ttu-id="010dd-465">LastModified</span><span class="sxs-lookup"><span data-stu-id="010dd-465">LastModified</span></span> |<span data-ttu-id="010dd-466">string</span><span class="sxs-lookup"><span data-stu-id="010dd-466">string</span></span> |
| <span data-ttu-id="010dd-467">Size</span><span class="sxs-lookup"><span data-stu-id="010dd-467">Size</span></span> |<span data-ttu-id="010dd-468">integer</span><span class="sxs-lookup"><span data-stu-id="010dd-468">integer</span></span> |
| <span data-ttu-id="010dd-469">MediaType</span><span class="sxs-lookup"><span data-stu-id="010dd-469">MediaType</span></span> |<span data-ttu-id="010dd-470">string</span><span class="sxs-lookup"><span data-stu-id="010dd-470">string</span></span> |
| <span data-ttu-id="010dd-471">IsFolder</span><span class="sxs-lookup"><span data-stu-id="010dd-471">IsFolder</span></span> |<span data-ttu-id="010dd-472">boolean</span><span class="sxs-lookup"><span data-stu-id="010dd-472">boolean</span></span> |
| <span data-ttu-id="010dd-473">ETag</span><span class="sxs-lookup"><span data-stu-id="010dd-473">ETag</span></span> |<span data-ttu-id="010dd-474">string</span><span class="sxs-lookup"><span data-stu-id="010dd-474">string</span></span> |
| <span data-ttu-id="010dd-475">FileLocator</span><span class="sxs-lookup"><span data-stu-id="010dd-475">FileLocator</span></span> |<span data-ttu-id="010dd-476">string</span><span class="sxs-lookup"><span data-stu-id="010dd-476">string</span></span> |

## <a name="http-responses"></a><span data-ttu-id="010dd-477">HTTP responses</span><span class="sxs-lookup"><span data-stu-id="010dd-477">HTTP responses</span></span>
<span data-ttu-id="010dd-478">The actions and triggers above can return one or more of the following HTTP status codes:</span><span class="sxs-lookup"><span data-stu-id="010dd-478">The actions and triggers above can return one or more of the following HTTP status codes:</span></span> 

| <span data-ttu-id="010dd-479">Name</span><span class="sxs-lookup"><span data-stu-id="010dd-479">Name</span></span> | <span data-ttu-id="010dd-480">Description</span><span class="sxs-lookup"><span data-stu-id="010dd-480">Description</span></span> |
| --- | --- |
| <span data-ttu-id="010dd-481">200</span><span class="sxs-lookup"><span data-stu-id="010dd-481">200</span></span> |<span data-ttu-id="010dd-482">OK</span><span class="sxs-lookup"><span data-stu-id="010dd-482">OK</span></span> |
| <span data-ttu-id="010dd-483">202</span><span class="sxs-lookup"><span data-stu-id="010dd-483">202</span></span> |<span data-ttu-id="010dd-484">Accepted</span><span class="sxs-lookup"><span data-stu-id="010dd-484">Accepted</span></span> |
| <span data-ttu-id="010dd-485">400</span><span class="sxs-lookup"><span data-stu-id="010dd-485">400</span></span> |<span data-ttu-id="010dd-486">Bad Request</span><span class="sxs-lookup"><span data-stu-id="010dd-486">Bad Request</span></span> |
| <span data-ttu-id="010dd-487">401</span><span class="sxs-lookup"><span data-stu-id="010dd-487">401</span></span> |<span data-ttu-id="010dd-488">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="010dd-488">Unauthorized</span></span> |
| <span data-ttu-id="010dd-489">403</span><span class="sxs-lookup"><span data-stu-id="010dd-489">403</span></span> |<span data-ttu-id="010dd-490">Forbidden</span><span class="sxs-lookup"><span data-stu-id="010dd-490">Forbidden</span></span> |
| <span data-ttu-id="010dd-491">404</span><span class="sxs-lookup"><span data-stu-id="010dd-491">404</span></span> |<span data-ttu-id="010dd-492">Not Found</span><span class="sxs-lookup"><span data-stu-id="010dd-492">Not Found</span></span> |
| <span data-ttu-id="010dd-493">500</span><span class="sxs-lookup"><span data-stu-id="010dd-493">500</span></span> |<span data-ttu-id="010dd-494">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="010dd-494">Internal Server Error.</span></span> <span data-ttu-id="010dd-495">Unknown error occurred.</span><span class="sxs-lookup"><span data-stu-id="010dd-495">Unknown error occurred.</span></span> |
| <span data-ttu-id="010dd-496">default</span><span class="sxs-lookup"><span data-stu-id="010dd-496">default</span></span> |<span data-ttu-id="010dd-497">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="010dd-497">Operation Failed.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="010dd-498">Next Steps</span><span class="sxs-lookup"><span data-stu-id="010dd-498">Next Steps</span></span>
[<span data-ttu-id="010dd-499">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="010dd-499">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

