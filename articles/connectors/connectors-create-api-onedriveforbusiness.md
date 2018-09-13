---
title: OneDrive for Business | Microsoft Docs
description: Create Logic apps with Azure App service. Connect to OneDrive for Business to manage your files. You can perform various actions such as upload, update, get, and delete on files.
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: cf9484e9-7a20-4de0-93c8-0fa132221f2b
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: deonhe
ms.openlocfilehash: 992b4b7bab8878355cbe936b75768e67b086286e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552493"
---
# <a name="get-started-with-the-onedrive-for-business-connector"></a><span data-ttu-id="47dc0-105">Get started with the OneDrive for Business connector</span><span class="sxs-lookup"><span data-stu-id="47dc0-105">Get started with the OneDrive for Business connector</span></span>
<span data-ttu-id="47dc0-106">Connect to OneDrive for Business to manage your files.</span><span class="sxs-lookup"><span data-stu-id="47dc0-106">Connect to OneDrive for Business to manage your files.</span></span> <span data-ttu-id="47dc0-107">You can perform various actions such as upload, update, get, and delete on files.</span><span class="sxs-lookup"><span data-stu-id="47dc0-107">You can perform various actions such as upload, update, get, and delete on files.</span></span>

> [!NOTE]
> <span data-ttu-id="47dc0-108">This version of the article applies to logic apps 2015-08-01-preview schema version.</span><span class="sxs-lookup"><span data-stu-id="47dc0-108">This version of the article applies to logic apps 2015-08-01-preview schema version.</span></span>
> 
> 

<span data-ttu-id="47dc0-109">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="47dc0-109">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="triggers-and-actions"></a><span data-ttu-id="47dc0-110">Triggers and actions</span><span class="sxs-lookup"><span data-stu-id="47dc0-110">Triggers and actions</span></span>
<span data-ttu-id="47dc0-111">The OneDrive for Business connector can be used as an action; it has trigger(s).</span><span class="sxs-lookup"><span data-stu-id="47dc0-111">The OneDrive for Business connector can be used as an action; it has trigger(s).</span></span> <span data-ttu-id="47dc0-112">All connectors support data in JSON and XML formats.</span><span class="sxs-lookup"><span data-stu-id="47dc0-112">All connectors support data in JSON and XML formats.</span></span>

 <span data-ttu-id="47dc0-113">The OneDrive for Business connector has the following action(s) and/or trigger(s) available:</span><span class="sxs-lookup"><span data-stu-id="47dc0-113">The OneDrive for Business connector has the following action(s) and/or trigger(s) available:</span></span>

### <a name="onedrive-for-business-actions"></a><span data-ttu-id="47dc0-114">OneDrive for Business actions</span><span class="sxs-lookup"><span data-stu-id="47dc0-114">OneDrive for Business actions</span></span>
<span data-ttu-id="47dc0-115">You can take these action(s):</span><span class="sxs-lookup"><span data-stu-id="47dc0-115">You can take these action(s):</span></span>

| <span data-ttu-id="47dc0-116">Action</span><span class="sxs-lookup"><span data-stu-id="47dc0-116">Action</span></span> | <span data-ttu-id="47dc0-117">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-117">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="47dc0-118">GetFileMetadata</span><span class="sxs-lookup"><span data-stu-id="47dc0-118">GetFileMetadata</span></span>](connectors-create-api-onedriveforbusiness.md#getfilemetadata) |<span data-ttu-id="47dc0-119">Retrieves metadata of a file in OneDrive for Business using id</span><span class="sxs-lookup"><span data-stu-id="47dc0-119">Retrieves metadata of a file in OneDrive for Business using id</span></span> |
| [<span data-ttu-id="47dc0-120">UpdateFile</span><span class="sxs-lookup"><span data-stu-id="47dc0-120">UpdateFile</span></span>](connectors-create-api-onedriveforbusiness.md#updatefile) |<span data-ttu-id="47dc0-121">Updates a file in OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-121">Updates a file in OneDrive for Business</span></span> |
| [<span data-ttu-id="47dc0-122">DeleteFile</span><span class="sxs-lookup"><span data-stu-id="47dc0-122">DeleteFile</span></span>](connectors-create-api-onedriveforbusiness.md#deletefile) |<span data-ttu-id="47dc0-123">Deletes a file from OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-123">Deletes a file from OneDrive for Business</span></span> |
| [<span data-ttu-id="47dc0-124">GetFileMetadataByPath</span><span class="sxs-lookup"><span data-stu-id="47dc0-124">GetFileMetadataByPath</span></span>](connectors-create-api-onedriveforbusiness.md#getfilemetadatabypath) |<span data-ttu-id="47dc0-125">Retrieves metadata of a file in OneDrive for Business using path</span><span class="sxs-lookup"><span data-stu-id="47dc0-125">Retrieves metadata of a file in OneDrive for Business using path</span></span> |
| [<span data-ttu-id="47dc0-126">GetFileContentByPath</span><span class="sxs-lookup"><span data-stu-id="47dc0-126">GetFileContentByPath</span></span>](connectors-create-api-onedriveforbusiness.md#getfilecontentbypath) |<span data-ttu-id="47dc0-127">Retrieves contents of a file in OneDrive for Business using path</span><span class="sxs-lookup"><span data-stu-id="47dc0-127">Retrieves contents of a file in OneDrive for Business using path</span></span> |
| [<span data-ttu-id="47dc0-128">GetFileContent</span><span class="sxs-lookup"><span data-stu-id="47dc0-128">GetFileContent</span></span>](connectors-create-api-onedriveforbusiness.md#getfilecontent) |<span data-ttu-id="47dc0-129">Retrieves contents of a file in OneDrive for Business using id</span><span class="sxs-lookup"><span data-stu-id="47dc0-129">Retrieves contents of a file in OneDrive for Business using id</span></span> |
| [<span data-ttu-id="47dc0-130">CreateFile</span><span class="sxs-lookup"><span data-stu-id="47dc0-130">CreateFile</span></span>](connectors-create-api-onedriveforbusiness.md#createfile) |<span data-ttu-id="47dc0-131">Uploads a file to OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-131">Uploads a file to OneDrive for Business</span></span> |
| [<span data-ttu-id="47dc0-132">CopyFile</span><span class="sxs-lookup"><span data-stu-id="47dc0-132">CopyFile</span></span>](connectors-create-api-onedriveforbusiness.md#copyfile) |<span data-ttu-id="47dc0-133">Copies a file to OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-133">Copies a file to OneDrive for Business</span></span> |
| [<span data-ttu-id="47dc0-134">ListFolder</span><span class="sxs-lookup"><span data-stu-id="47dc0-134">ListFolder</span></span>](connectors-create-api-onedriveforbusiness.md#listfolder) |<span data-ttu-id="47dc0-135">Lists files in a OneDrive for Business folder</span><span class="sxs-lookup"><span data-stu-id="47dc0-135">Lists files in a OneDrive for Business folder</span></span> |
| [<span data-ttu-id="47dc0-136">ListRootFolder</span><span class="sxs-lookup"><span data-stu-id="47dc0-136">ListRootFolder</span></span>](connectors-create-api-onedriveforbusiness.md#listrootfolder) |<span data-ttu-id="47dc0-137">Lists files in the OneDrive for Business root folder</span><span class="sxs-lookup"><span data-stu-id="47dc0-137">Lists files in the OneDrive for Business root folder</span></span> |
| [<span data-ttu-id="47dc0-138">ExtractFolderV2</span><span class="sxs-lookup"><span data-stu-id="47dc0-138">ExtractFolderV2</span></span>](connectors-create-api-onedriveforbusiness.md#extractfolderv2) |<span data-ttu-id="47dc0-139">Extracts a folder to OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-139">Extracts a folder to OneDrive for Business</span></span> |

### <a name="onedrive-for-business-triggers"></a><span data-ttu-id="47dc0-140">OneDrive for Business triggers</span><span class="sxs-lookup"><span data-stu-id="47dc0-140">OneDrive for Business triggers</span></span>
<span data-ttu-id="47dc0-141">You can listen for these event(s):</span><span class="sxs-lookup"><span data-stu-id="47dc0-141">You can listen for these event(s):</span></span>

| <span data-ttu-id="47dc0-142">Trigger</span><span class="sxs-lookup"><span data-stu-id="47dc0-142">Trigger</span></span> | <span data-ttu-id="47dc0-143">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47dc0-144">When a file is created</span><span class="sxs-lookup"><span data-stu-id="47dc0-144">When a file is created</span></span> |<span data-ttu-id="47dc0-145">Triggers a flow when a new file is created in a OneDrive for Business folder</span><span class="sxs-lookup"><span data-stu-id="47dc0-145">Triggers a flow when a new file is created in a OneDrive for Business folder</span></span> |
| <span data-ttu-id="47dc0-146">When a file is modified</span><span class="sxs-lookup"><span data-stu-id="47dc0-146">When a file is modified</span></span> |<span data-ttu-id="47dc0-147">Triggers a flow when a file is modified in a OneDrive for Business folder</span><span class="sxs-lookup"><span data-stu-id="47dc0-147">Triggers a flow when a file is modified in a OneDrive for Business folder</span></span> |

## <a name="create-a-connection-to-onedrive-for-business"></a><span data-ttu-id="47dc0-148">Create a connection to OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-148">Create a connection to OneDrive for Business</span></span>
<span data-ttu-id="47dc0-149">To create Logic apps with OneDrive for Business, you must first create a **connection** then provide the details for the following properties:</span><span class="sxs-lookup"><span data-stu-id="47dc0-149">To create Logic apps with OneDrive for Business, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="47dc0-150">Property</span><span class="sxs-lookup"><span data-stu-id="47dc0-150">Property</span></span> | <span data-ttu-id="47dc0-151">Required</span><span class="sxs-lookup"><span data-stu-id="47dc0-151">Required</span></span> | <span data-ttu-id="47dc0-152">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-152">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47dc0-153">Token</span><span class="sxs-lookup"><span data-stu-id="47dc0-153">Token</span></span> |<span data-ttu-id="47dc0-154">Yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-154">Yes</span></span> |<span data-ttu-id="47dc0-155">Provide OneDrive for Business Credentials</span><span class="sxs-lookup"><span data-stu-id="47dc0-155">Provide OneDrive for Business Credentials</span></span> |

<span data-ttu-id="47dc0-156">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span><span class="sxs-lookup"><span data-stu-id="47dc0-156">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span>

> [!INCLUDE [Steps to create a connection to OneDrive for Business](../../includes/connectors-create-api-onedriveforbusiness.md)]
> 
> [!TIP]
> <span data-ttu-id="47dc0-157">You can use this connection in other logic apps.</span><span class="sxs-lookup"><span data-stu-id="47dc0-157">You can use this connection in other logic apps.</span></span>
> 
> 

## <a name="reference-for-onedrive-for-business"></a><span data-ttu-id="47dc0-158">Reference for OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-158">Reference for OneDrive for Business</span></span>
<span data-ttu-id="47dc0-159">Applies to version: 1.0</span><span class="sxs-lookup"><span data-stu-id="47dc0-159">Applies to version: 1.0</span></span>

## <a name="getfilemetadata"></a><span data-ttu-id="47dc0-160">GetFileMetadata</span><span class="sxs-lookup"><span data-stu-id="47dc0-160">GetFileMetadata</span></span>
<span data-ttu-id="47dc0-161">Get file metadata using id: Retrieves metadata of a file in OneDrive for Business using id</span><span class="sxs-lookup"><span data-stu-id="47dc0-161">Get file metadata using id: Retrieves metadata of a file in OneDrive for Business using id</span></span>

```GET: /datasets/default/files/{id}```

| <span data-ttu-id="47dc0-162">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-162">Name</span></span> | <span data-ttu-id="47dc0-163">Data Type</span><span class="sxs-lookup"><span data-stu-id="47dc0-163">Data Type</span></span> | <span data-ttu-id="47dc0-164">Required</span><span class="sxs-lookup"><span data-stu-id="47dc0-164">Required</span></span> | <span data-ttu-id="47dc0-165">Located In</span><span class="sxs-lookup"><span data-stu-id="47dc0-165">Located In</span></span> | <span data-ttu-id="47dc0-166">Default Value</span><span class="sxs-lookup"><span data-stu-id="47dc0-166">Default Value</span></span> | <span data-ttu-id="47dc0-167">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-167">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="47dc0-168">id</span><span class="sxs-lookup"><span data-stu-id="47dc0-168">id</span></span> |<span data-ttu-id="47dc0-169">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-169">string</span></span> |<span data-ttu-id="47dc0-170">yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-170">yes</span></span> |<span data-ttu-id="47dc0-171">path</span><span class="sxs-lookup"><span data-stu-id="47dc0-171">path</span></span> |<span data-ttu-id="47dc0-172">none</span><span class="sxs-lookup"><span data-stu-id="47dc0-172">none</span></span> |<span data-ttu-id="47dc0-173">Specify the file</span><span class="sxs-lookup"><span data-stu-id="47dc0-173">Specify the file</span></span> |

#### <a name="response"></a><span data-ttu-id="47dc0-174">Response</span><span class="sxs-lookup"><span data-stu-id="47dc0-174">Response</span></span>
| <span data-ttu-id="47dc0-175">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-175">Name</span></span> | <span data-ttu-id="47dc0-176">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-176">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47dc0-177">200</span><span class="sxs-lookup"><span data-stu-id="47dc0-177">200</span></span> |<span data-ttu-id="47dc0-178">OK</span><span class="sxs-lookup"><span data-stu-id="47dc0-178">OK</span></span> |
| <span data-ttu-id="47dc0-179">default</span><span class="sxs-lookup"><span data-stu-id="47dc0-179">default</span></span> |<span data-ttu-id="47dc0-180">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="47dc0-180">Operation Failed.</span></span> |

## <a name="updatefile"></a><span data-ttu-id="47dc0-181">UpdateFile</span><span class="sxs-lookup"><span data-stu-id="47dc0-181">UpdateFile</span></span>
<span data-ttu-id="47dc0-182">Update file: Updates a file in OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-182">Update file: Updates a file in OneDrive for Business</span></span>

```PUT: /datasets/default/files/{id}```

| <span data-ttu-id="47dc0-183">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-183">Name</span></span> | <span data-ttu-id="47dc0-184">Data Type</span><span class="sxs-lookup"><span data-stu-id="47dc0-184">Data Type</span></span> | <span data-ttu-id="47dc0-185">Required</span><span class="sxs-lookup"><span data-stu-id="47dc0-185">Required</span></span> | <span data-ttu-id="47dc0-186">Located In</span><span class="sxs-lookup"><span data-stu-id="47dc0-186">Located In</span></span> | <span data-ttu-id="47dc0-187">Default Value</span><span class="sxs-lookup"><span data-stu-id="47dc0-187">Default Value</span></span> | <span data-ttu-id="47dc0-188">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-188">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="47dc0-189">id</span><span class="sxs-lookup"><span data-stu-id="47dc0-189">id</span></span> |<span data-ttu-id="47dc0-190">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-190">string</span></span> |<span data-ttu-id="47dc0-191">yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-191">yes</span></span> |<span data-ttu-id="47dc0-192">path</span><span class="sxs-lookup"><span data-stu-id="47dc0-192">path</span></span> |<span data-ttu-id="47dc0-193">none</span><span class="sxs-lookup"><span data-stu-id="47dc0-193">none</span></span> |<span data-ttu-id="47dc0-194">Specify the file to update</span><span class="sxs-lookup"><span data-stu-id="47dc0-194">Specify the file to update</span></span> |
| <span data-ttu-id="47dc0-195">body</span><span class="sxs-lookup"><span data-stu-id="47dc0-195">body</span></span> | |<span data-ttu-id="47dc0-196">yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-196">yes</span></span> |<span data-ttu-id="47dc0-197">body</span><span class="sxs-lookup"><span data-stu-id="47dc0-197">body</span></span> |<span data-ttu-id="47dc0-198">none</span><span class="sxs-lookup"><span data-stu-id="47dc0-198">none</span></span> |<span data-ttu-id="47dc0-199">Content of the file to update in OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-199">Content of the file to update in OneDrive for Business</span></span> |

#### <a name="response"></a><span data-ttu-id="47dc0-200">Response</span><span class="sxs-lookup"><span data-stu-id="47dc0-200">Response</span></span>
| <span data-ttu-id="47dc0-201">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-201">Name</span></span> | <span data-ttu-id="47dc0-202">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-202">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47dc0-203">200</span><span class="sxs-lookup"><span data-stu-id="47dc0-203">200</span></span> |<span data-ttu-id="47dc0-204">OK</span><span class="sxs-lookup"><span data-stu-id="47dc0-204">OK</span></span> |
| <span data-ttu-id="47dc0-205">default</span><span class="sxs-lookup"><span data-stu-id="47dc0-205">default</span></span> |<span data-ttu-id="47dc0-206">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="47dc0-206">Operation Failed.</span></span> |

## <a name="deletefile"></a><span data-ttu-id="47dc0-207">DeleteFile</span><span class="sxs-lookup"><span data-stu-id="47dc0-207">DeleteFile</span></span>
<span data-ttu-id="47dc0-208">Delete file: Deletes a file from OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-208">Delete file: Deletes a file from OneDrive for Business</span></span>

```DELETE: /datasets/default/files/{id}```

| <span data-ttu-id="47dc0-209">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-209">Name</span></span> | <span data-ttu-id="47dc0-210">Data Type</span><span class="sxs-lookup"><span data-stu-id="47dc0-210">Data Type</span></span> | <span data-ttu-id="47dc0-211">Required</span><span class="sxs-lookup"><span data-stu-id="47dc0-211">Required</span></span> | <span data-ttu-id="47dc0-212">Located In</span><span class="sxs-lookup"><span data-stu-id="47dc0-212">Located In</span></span> | <span data-ttu-id="47dc0-213">Default Value</span><span class="sxs-lookup"><span data-stu-id="47dc0-213">Default Value</span></span> | <span data-ttu-id="47dc0-214">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-214">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="47dc0-215">id</span><span class="sxs-lookup"><span data-stu-id="47dc0-215">id</span></span> |<span data-ttu-id="47dc0-216">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-216">string</span></span> |<span data-ttu-id="47dc0-217">yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-217">yes</span></span> |<span data-ttu-id="47dc0-218">path</span><span class="sxs-lookup"><span data-stu-id="47dc0-218">path</span></span> |<span data-ttu-id="47dc0-219">none</span><span class="sxs-lookup"><span data-stu-id="47dc0-219">none</span></span> |<span data-ttu-id="47dc0-220">Specify the file to delete</span><span class="sxs-lookup"><span data-stu-id="47dc0-220">Specify the file to delete</span></span> |

#### <a name="response"></a><span data-ttu-id="47dc0-221">Response</span><span class="sxs-lookup"><span data-stu-id="47dc0-221">Response</span></span>
| <span data-ttu-id="47dc0-222">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-222">Name</span></span> | <span data-ttu-id="47dc0-223">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-223">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47dc0-224">200</span><span class="sxs-lookup"><span data-stu-id="47dc0-224">200</span></span> |<span data-ttu-id="47dc0-225">OK</span><span class="sxs-lookup"><span data-stu-id="47dc0-225">OK</span></span> |
| <span data-ttu-id="47dc0-226">default</span><span class="sxs-lookup"><span data-stu-id="47dc0-226">default</span></span> |<span data-ttu-id="47dc0-227">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="47dc0-227">Operation Failed.</span></span> |

## <a name="getfilemetadatabypath"></a><span data-ttu-id="47dc0-228">GetFileMetadataByPath</span><span class="sxs-lookup"><span data-stu-id="47dc0-228">GetFileMetadataByPath</span></span>
<span data-ttu-id="47dc0-229">Get file metadata using path: Retrieves metadata of a file in OneDrive for Business using path</span><span class="sxs-lookup"><span data-stu-id="47dc0-229">Get file metadata using path: Retrieves metadata of a file in OneDrive for Business using path</span></span>

```GET: /datasets/default/GetFileByPath```

| <span data-ttu-id="47dc0-230">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-230">Name</span></span> | <span data-ttu-id="47dc0-231">Data Type</span><span class="sxs-lookup"><span data-stu-id="47dc0-231">Data Type</span></span> | <span data-ttu-id="47dc0-232">Required</span><span class="sxs-lookup"><span data-stu-id="47dc0-232">Required</span></span> | <span data-ttu-id="47dc0-233">Located In</span><span class="sxs-lookup"><span data-stu-id="47dc0-233">Located In</span></span> | <span data-ttu-id="47dc0-234">Default Value</span><span class="sxs-lookup"><span data-stu-id="47dc0-234">Default Value</span></span> | <span data-ttu-id="47dc0-235">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-235">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="47dc0-236">path</span><span class="sxs-lookup"><span data-stu-id="47dc0-236">path</span></span> |<span data-ttu-id="47dc0-237">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-237">string</span></span> |<span data-ttu-id="47dc0-238">yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-238">yes</span></span> |<span data-ttu-id="47dc0-239">query</span><span class="sxs-lookup"><span data-stu-id="47dc0-239">query</span></span> |<span data-ttu-id="47dc0-240">none</span><span class="sxs-lookup"><span data-stu-id="47dc0-240">none</span></span> |<span data-ttu-id="47dc0-241">Unique path to the file in OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-241">Unique path to the file in OneDrive for Business</span></span> |

#### <a name="response"></a><span data-ttu-id="47dc0-242">Response</span><span class="sxs-lookup"><span data-stu-id="47dc0-242">Response</span></span>
| <span data-ttu-id="47dc0-243">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-243">Name</span></span> | <span data-ttu-id="47dc0-244">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-244">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47dc0-245">200</span><span class="sxs-lookup"><span data-stu-id="47dc0-245">200</span></span> |<span data-ttu-id="47dc0-246">OK</span><span class="sxs-lookup"><span data-stu-id="47dc0-246">OK</span></span> |
| <span data-ttu-id="47dc0-247">default</span><span class="sxs-lookup"><span data-stu-id="47dc0-247">default</span></span> |<span data-ttu-id="47dc0-248">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="47dc0-248">Operation Failed.</span></span> |

## <a name="getfilecontentbypath"></a><span data-ttu-id="47dc0-249">GetFileContentByPath</span><span class="sxs-lookup"><span data-stu-id="47dc0-249">GetFileContentByPath</span></span>
<span data-ttu-id="47dc0-250">Get file content using path: Retrieves contents of a file in OneDrive for Business using path</span><span class="sxs-lookup"><span data-stu-id="47dc0-250">Get file content using path: Retrieves contents of a file in OneDrive for Business using path</span></span>

```GET: /datasets/default/GetFileContentByPath```

| <span data-ttu-id="47dc0-251">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-251">Name</span></span> | <span data-ttu-id="47dc0-252">Data Type</span><span class="sxs-lookup"><span data-stu-id="47dc0-252">Data Type</span></span> | <span data-ttu-id="47dc0-253">Required</span><span class="sxs-lookup"><span data-stu-id="47dc0-253">Required</span></span> | <span data-ttu-id="47dc0-254">Located In</span><span class="sxs-lookup"><span data-stu-id="47dc0-254">Located In</span></span> | <span data-ttu-id="47dc0-255">Default Value</span><span class="sxs-lookup"><span data-stu-id="47dc0-255">Default Value</span></span> | <span data-ttu-id="47dc0-256">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-256">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="47dc0-257">path</span><span class="sxs-lookup"><span data-stu-id="47dc0-257">path</span></span> |<span data-ttu-id="47dc0-258">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-258">string</span></span> |<span data-ttu-id="47dc0-259">yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-259">yes</span></span> |<span data-ttu-id="47dc0-260">query</span><span class="sxs-lookup"><span data-stu-id="47dc0-260">query</span></span> |<span data-ttu-id="47dc0-261">none</span><span class="sxs-lookup"><span data-stu-id="47dc0-261">none</span></span> |<span data-ttu-id="47dc0-262">Unique path to the file in OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-262">Unique path to the file in OneDrive for Business</span></span> |

#### <a name="response"></a><span data-ttu-id="47dc0-263">Response</span><span class="sxs-lookup"><span data-stu-id="47dc0-263">Response</span></span>
| <span data-ttu-id="47dc0-264">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-264">Name</span></span> | <span data-ttu-id="47dc0-265">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-265">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47dc0-266">200</span><span class="sxs-lookup"><span data-stu-id="47dc0-266">200</span></span> |<span data-ttu-id="47dc0-267">OK</span><span class="sxs-lookup"><span data-stu-id="47dc0-267">OK</span></span> |
| <span data-ttu-id="47dc0-268">default</span><span class="sxs-lookup"><span data-stu-id="47dc0-268">default</span></span> |<span data-ttu-id="47dc0-269">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="47dc0-269">Operation Failed.</span></span> |

## <a name="getfilecontent"></a><span data-ttu-id="47dc0-270">GetFileContent</span><span class="sxs-lookup"><span data-stu-id="47dc0-270">GetFileContent</span></span>
<span data-ttu-id="47dc0-271">Get file content using id: Retrieves contents of a file in OneDrive for Business using id</span><span class="sxs-lookup"><span data-stu-id="47dc0-271">Get file content using id: Retrieves contents of a file in OneDrive for Business using id</span></span>

```GET: /datasets/default/files/{id}/content```

| <span data-ttu-id="47dc0-272">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-272">Name</span></span> | <span data-ttu-id="47dc0-273">Data Type</span><span class="sxs-lookup"><span data-stu-id="47dc0-273">Data Type</span></span> | <span data-ttu-id="47dc0-274">Required</span><span class="sxs-lookup"><span data-stu-id="47dc0-274">Required</span></span> | <span data-ttu-id="47dc0-275">Located In</span><span class="sxs-lookup"><span data-stu-id="47dc0-275">Located In</span></span> | <span data-ttu-id="47dc0-276">Default Value</span><span class="sxs-lookup"><span data-stu-id="47dc0-276">Default Value</span></span> | <span data-ttu-id="47dc0-277">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-277">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="47dc0-278">id</span><span class="sxs-lookup"><span data-stu-id="47dc0-278">id</span></span> |<span data-ttu-id="47dc0-279">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-279">string</span></span> |<span data-ttu-id="47dc0-280">yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-280">yes</span></span> |<span data-ttu-id="47dc0-281">path</span><span class="sxs-lookup"><span data-stu-id="47dc0-281">path</span></span> |<span data-ttu-id="47dc0-282">none</span><span class="sxs-lookup"><span data-stu-id="47dc0-282">none</span></span> |<span data-ttu-id="47dc0-283">Specify the file</span><span class="sxs-lookup"><span data-stu-id="47dc0-283">Specify the file</span></span> |

#### <a name="response"></a><span data-ttu-id="47dc0-284">Response</span><span class="sxs-lookup"><span data-stu-id="47dc0-284">Response</span></span>
| <span data-ttu-id="47dc0-285">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-285">Name</span></span> | <span data-ttu-id="47dc0-286">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47dc0-287">200</span><span class="sxs-lookup"><span data-stu-id="47dc0-287">200</span></span> |<span data-ttu-id="47dc0-288">OK</span><span class="sxs-lookup"><span data-stu-id="47dc0-288">OK</span></span> |
| <span data-ttu-id="47dc0-289">default</span><span class="sxs-lookup"><span data-stu-id="47dc0-289">default</span></span> |<span data-ttu-id="47dc0-290">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="47dc0-290">Operation Failed.</span></span> |

## <a name="createfile"></a><span data-ttu-id="47dc0-291">CreateFile</span><span class="sxs-lookup"><span data-stu-id="47dc0-291">CreateFile</span></span>
<span data-ttu-id="47dc0-292">Create file: Uploads a file to OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-292">Create file: Uploads a file to OneDrive for Business</span></span>

```POST: /datasets/default/files```

| <span data-ttu-id="47dc0-293">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-293">Name</span></span> | <span data-ttu-id="47dc0-294">Data Type</span><span class="sxs-lookup"><span data-stu-id="47dc0-294">Data Type</span></span> | <span data-ttu-id="47dc0-295">Required</span><span class="sxs-lookup"><span data-stu-id="47dc0-295">Required</span></span> | <span data-ttu-id="47dc0-296">Located In</span><span class="sxs-lookup"><span data-stu-id="47dc0-296">Located In</span></span> | <span data-ttu-id="47dc0-297">Default Value</span><span class="sxs-lookup"><span data-stu-id="47dc0-297">Default Value</span></span> | <span data-ttu-id="47dc0-298">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-298">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="47dc0-299">folderPath</span><span class="sxs-lookup"><span data-stu-id="47dc0-299">folderPath</span></span> |<span data-ttu-id="47dc0-300">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-300">string</span></span> |<span data-ttu-id="47dc0-301">yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-301">yes</span></span> |<span data-ttu-id="47dc0-302">query</span><span class="sxs-lookup"><span data-stu-id="47dc0-302">query</span></span> |<span data-ttu-id="47dc0-303">none</span><span class="sxs-lookup"><span data-stu-id="47dc0-303">none</span></span> |<span data-ttu-id="47dc0-304">Folder path to upload the file to OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-304">Folder path to upload the file to OneDrive for Business</span></span> |
| <span data-ttu-id="47dc0-305">name</span><span class="sxs-lookup"><span data-stu-id="47dc0-305">name</span></span> |<span data-ttu-id="47dc0-306">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-306">string</span></span> |<span data-ttu-id="47dc0-307">yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-307">yes</span></span> |<span data-ttu-id="47dc0-308">query</span><span class="sxs-lookup"><span data-stu-id="47dc0-308">query</span></span> |<span data-ttu-id="47dc0-309">none</span><span class="sxs-lookup"><span data-stu-id="47dc0-309">none</span></span> |<span data-ttu-id="47dc0-310">Name of the file to create in OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-310">Name of the file to create in OneDrive for Business</span></span> |
| <span data-ttu-id="47dc0-311">body</span><span class="sxs-lookup"><span data-stu-id="47dc0-311">body</span></span> | |<span data-ttu-id="47dc0-312">yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-312">yes</span></span> |<span data-ttu-id="47dc0-313">body</span><span class="sxs-lookup"><span data-stu-id="47dc0-313">body</span></span> |<span data-ttu-id="47dc0-314">none</span><span class="sxs-lookup"><span data-stu-id="47dc0-314">none</span></span> |<span data-ttu-id="47dc0-315">Content of the file to upload to OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-315">Content of the file to upload to OneDrive for Business</span></span> |

#### <a name="response"></a><span data-ttu-id="47dc0-316">Response</span><span class="sxs-lookup"><span data-stu-id="47dc0-316">Response</span></span>
| <span data-ttu-id="47dc0-317">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-317">Name</span></span> | <span data-ttu-id="47dc0-318">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-318">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47dc0-319">200</span><span class="sxs-lookup"><span data-stu-id="47dc0-319">200</span></span> |<span data-ttu-id="47dc0-320">OK</span><span class="sxs-lookup"><span data-stu-id="47dc0-320">OK</span></span> |
| <span data-ttu-id="47dc0-321">default</span><span class="sxs-lookup"><span data-stu-id="47dc0-321">default</span></span> |<span data-ttu-id="47dc0-322">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="47dc0-322">Operation Failed.</span></span> |

## <a name="copyfile"></a><span data-ttu-id="47dc0-323">CopyFile</span><span class="sxs-lookup"><span data-stu-id="47dc0-323">CopyFile</span></span>
<span data-ttu-id="47dc0-324">Copy file: Copies a file to OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-324">Copy file: Copies a file to OneDrive for Business</span></span>

```POST: /datasets/default/copyFile```

| <span data-ttu-id="47dc0-325">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-325">Name</span></span> | <span data-ttu-id="47dc0-326">Data Type</span><span class="sxs-lookup"><span data-stu-id="47dc0-326">Data Type</span></span> | <span data-ttu-id="47dc0-327">Required</span><span class="sxs-lookup"><span data-stu-id="47dc0-327">Required</span></span> | <span data-ttu-id="47dc0-328">Located In</span><span class="sxs-lookup"><span data-stu-id="47dc0-328">Located In</span></span> | <span data-ttu-id="47dc0-329">Default Value</span><span class="sxs-lookup"><span data-stu-id="47dc0-329">Default Value</span></span> | <span data-ttu-id="47dc0-330">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-330">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="47dc0-331">source</span><span class="sxs-lookup"><span data-stu-id="47dc0-331">source</span></span> |<span data-ttu-id="47dc0-332">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-332">string</span></span> |<span data-ttu-id="47dc0-333">yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-333">yes</span></span> |<span data-ttu-id="47dc0-334">query</span><span class="sxs-lookup"><span data-stu-id="47dc0-334">query</span></span> |<span data-ttu-id="47dc0-335">none</span><span class="sxs-lookup"><span data-stu-id="47dc0-335">none</span></span> |<span data-ttu-id="47dc0-336">Url to source file</span><span class="sxs-lookup"><span data-stu-id="47dc0-336">Url to source file</span></span> |
| <span data-ttu-id="47dc0-337">destination</span><span class="sxs-lookup"><span data-stu-id="47dc0-337">destination</span></span> |<span data-ttu-id="47dc0-338">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-338">string</span></span> |<span data-ttu-id="47dc0-339">yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-339">yes</span></span> |<span data-ttu-id="47dc0-340">query</span><span class="sxs-lookup"><span data-stu-id="47dc0-340">query</span></span> |<span data-ttu-id="47dc0-341">none</span><span class="sxs-lookup"><span data-stu-id="47dc0-341">none</span></span> |<span data-ttu-id="47dc0-342">Destination file path in OneDrive for Business, including target filename</span><span class="sxs-lookup"><span data-stu-id="47dc0-342">Destination file path in OneDrive for Business, including target filename</span></span> |
| <span data-ttu-id="47dc0-343">overwrite</span><span class="sxs-lookup"><span data-stu-id="47dc0-343">overwrite</span></span> |<span data-ttu-id="47dc0-344">boolean</span><span class="sxs-lookup"><span data-stu-id="47dc0-344">boolean</span></span> |<span data-ttu-id="47dc0-345">no</span><span class="sxs-lookup"><span data-stu-id="47dc0-345">no</span></span> |<span data-ttu-id="47dc0-346">query</span><span class="sxs-lookup"><span data-stu-id="47dc0-346">query</span></span> |<span data-ttu-id="47dc0-347">false</span><span class="sxs-lookup"><span data-stu-id="47dc0-347">false</span></span> |<span data-ttu-id="47dc0-348">Overwrites the destination file if set to 'true'</span><span class="sxs-lookup"><span data-stu-id="47dc0-348">Overwrites the destination file if set to 'true'</span></span> |

#### <a name="response"></a><span data-ttu-id="47dc0-349">Response</span><span class="sxs-lookup"><span data-stu-id="47dc0-349">Response</span></span>
| <span data-ttu-id="47dc0-350">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-350">Name</span></span> | <span data-ttu-id="47dc0-351">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-351">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47dc0-352">200</span><span class="sxs-lookup"><span data-stu-id="47dc0-352">200</span></span> |<span data-ttu-id="47dc0-353">OK</span><span class="sxs-lookup"><span data-stu-id="47dc0-353">OK</span></span> |
| <span data-ttu-id="47dc0-354">default</span><span class="sxs-lookup"><span data-stu-id="47dc0-354">default</span></span> |<span data-ttu-id="47dc0-355">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="47dc0-355">Operation Failed.</span></span> |

## <a name="onnewfile"></a><span data-ttu-id="47dc0-356">OnNewFile</span><span class="sxs-lookup"><span data-stu-id="47dc0-356">OnNewFile</span></span>
<span data-ttu-id="47dc0-357">When a file is created: Triggers a flow when a new file is created in a OneDrive for Business folder</span><span class="sxs-lookup"><span data-stu-id="47dc0-357">When a file is created: Triggers a flow when a new file is created in a OneDrive for Business folder</span></span>

```GET: /datasets/default/triggers/onnewfile```

| <span data-ttu-id="47dc0-358">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-358">Name</span></span> | <span data-ttu-id="47dc0-359">Data Type</span><span class="sxs-lookup"><span data-stu-id="47dc0-359">Data Type</span></span> | <span data-ttu-id="47dc0-360">Required</span><span class="sxs-lookup"><span data-stu-id="47dc0-360">Required</span></span> | <span data-ttu-id="47dc0-361">Located In</span><span class="sxs-lookup"><span data-stu-id="47dc0-361">Located In</span></span> | <span data-ttu-id="47dc0-362">Default Value</span><span class="sxs-lookup"><span data-stu-id="47dc0-362">Default Value</span></span> | <span data-ttu-id="47dc0-363">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-363">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="47dc0-364">folderId</span><span class="sxs-lookup"><span data-stu-id="47dc0-364">folderId</span></span> |<span data-ttu-id="47dc0-365">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-365">string</span></span> |<span data-ttu-id="47dc0-366">yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-366">yes</span></span> |<span data-ttu-id="47dc0-367">query</span><span class="sxs-lookup"><span data-stu-id="47dc0-367">query</span></span> |<span data-ttu-id="47dc0-368">none</span><span class="sxs-lookup"><span data-stu-id="47dc0-368">none</span></span> |<span data-ttu-id="47dc0-369">Specify a folder</span><span class="sxs-lookup"><span data-stu-id="47dc0-369">Specify a folder</span></span> |

#### <a name="response"></a><span data-ttu-id="47dc0-370">Response</span><span class="sxs-lookup"><span data-stu-id="47dc0-370">Response</span></span>
| <span data-ttu-id="47dc0-371">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-371">Name</span></span> | <span data-ttu-id="47dc0-372">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-372">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47dc0-373">200</span><span class="sxs-lookup"><span data-stu-id="47dc0-373">200</span></span> |<span data-ttu-id="47dc0-374">OK</span><span class="sxs-lookup"><span data-stu-id="47dc0-374">OK</span></span> |
| <span data-ttu-id="47dc0-375">default</span><span class="sxs-lookup"><span data-stu-id="47dc0-375">default</span></span> |<span data-ttu-id="47dc0-376">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="47dc0-376">Operation Failed.</span></span> |

## <a name="onupdatedfile"></a><span data-ttu-id="47dc0-377">OnUpdatedFile</span><span class="sxs-lookup"><span data-stu-id="47dc0-377">OnUpdatedFile</span></span>
<span data-ttu-id="47dc0-378">When a file is modified: Triggers a flow when a file is modified in a OneDrive for Business folder</span><span class="sxs-lookup"><span data-stu-id="47dc0-378">When a file is modified: Triggers a flow when a file is modified in a OneDrive for Business folder</span></span>

```GET: /datasets/default/triggers/onupdatedfile```

| <span data-ttu-id="47dc0-379">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-379">Name</span></span> | <span data-ttu-id="47dc0-380">Data Type</span><span class="sxs-lookup"><span data-stu-id="47dc0-380">Data Type</span></span> | <span data-ttu-id="47dc0-381">Required</span><span class="sxs-lookup"><span data-stu-id="47dc0-381">Required</span></span> | <span data-ttu-id="47dc0-382">Located In</span><span class="sxs-lookup"><span data-stu-id="47dc0-382">Located In</span></span> | <span data-ttu-id="47dc0-383">Default Value</span><span class="sxs-lookup"><span data-stu-id="47dc0-383">Default Value</span></span> | <span data-ttu-id="47dc0-384">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-384">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="47dc0-385">folderId</span><span class="sxs-lookup"><span data-stu-id="47dc0-385">folderId</span></span> |<span data-ttu-id="47dc0-386">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-386">string</span></span> |<span data-ttu-id="47dc0-387">yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-387">yes</span></span> |<span data-ttu-id="47dc0-388">query</span><span class="sxs-lookup"><span data-stu-id="47dc0-388">query</span></span> |<span data-ttu-id="47dc0-389">none</span><span class="sxs-lookup"><span data-stu-id="47dc0-389">none</span></span> |<span data-ttu-id="47dc0-390">Specify a folder</span><span class="sxs-lookup"><span data-stu-id="47dc0-390">Specify a folder</span></span> |

#### <a name="response"></a><span data-ttu-id="47dc0-391">Response</span><span class="sxs-lookup"><span data-stu-id="47dc0-391">Response</span></span>
| <span data-ttu-id="47dc0-392">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-392">Name</span></span> | <span data-ttu-id="47dc0-393">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-393">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47dc0-394">200</span><span class="sxs-lookup"><span data-stu-id="47dc0-394">200</span></span> |<span data-ttu-id="47dc0-395">OK</span><span class="sxs-lookup"><span data-stu-id="47dc0-395">OK</span></span> |
| <span data-ttu-id="47dc0-396">default</span><span class="sxs-lookup"><span data-stu-id="47dc0-396">default</span></span> |<span data-ttu-id="47dc0-397">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="47dc0-397">Operation Failed.</span></span> |

## <a name="listfolder"></a><span data-ttu-id="47dc0-398">ListFolder</span><span class="sxs-lookup"><span data-stu-id="47dc0-398">ListFolder</span></span>
<span data-ttu-id="47dc0-399">List files in folder: Lists files in a OneDrive for Business folder</span><span class="sxs-lookup"><span data-stu-id="47dc0-399">List files in folder: Lists files in a OneDrive for Business folder</span></span>

```GET: /datasets/default/folders/{id}```

| <span data-ttu-id="47dc0-400">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-400">Name</span></span> | <span data-ttu-id="47dc0-401">Data Type</span><span class="sxs-lookup"><span data-stu-id="47dc0-401">Data Type</span></span> | <span data-ttu-id="47dc0-402">Required</span><span class="sxs-lookup"><span data-stu-id="47dc0-402">Required</span></span> | <span data-ttu-id="47dc0-403">Located In</span><span class="sxs-lookup"><span data-stu-id="47dc0-403">Located In</span></span> | <span data-ttu-id="47dc0-404">Default Value</span><span class="sxs-lookup"><span data-stu-id="47dc0-404">Default Value</span></span> | <span data-ttu-id="47dc0-405">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-405">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="47dc0-406">id</span><span class="sxs-lookup"><span data-stu-id="47dc0-406">id</span></span> |<span data-ttu-id="47dc0-407">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-407">string</span></span> |<span data-ttu-id="47dc0-408">yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-408">yes</span></span> |<span data-ttu-id="47dc0-409">path</span><span class="sxs-lookup"><span data-stu-id="47dc0-409">path</span></span> |<span data-ttu-id="47dc0-410">none</span><span class="sxs-lookup"><span data-stu-id="47dc0-410">none</span></span> |<span data-ttu-id="47dc0-411">Specify the folder</span><span class="sxs-lookup"><span data-stu-id="47dc0-411">Specify the folder</span></span> |

#### <a name="response"></a><span data-ttu-id="47dc0-412">Response</span><span class="sxs-lookup"><span data-stu-id="47dc0-412">Response</span></span>
| <span data-ttu-id="47dc0-413">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-413">Name</span></span> | <span data-ttu-id="47dc0-414">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-414">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47dc0-415">200</span><span class="sxs-lookup"><span data-stu-id="47dc0-415">200</span></span> |<span data-ttu-id="47dc0-416">OK</span><span class="sxs-lookup"><span data-stu-id="47dc0-416">OK</span></span> |
| <span data-ttu-id="47dc0-417">default</span><span class="sxs-lookup"><span data-stu-id="47dc0-417">default</span></span> |<span data-ttu-id="47dc0-418">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="47dc0-418">Operation Failed.</span></span> |

## <a name="listrootfolder"></a><span data-ttu-id="47dc0-419">ListRootFolder</span><span class="sxs-lookup"><span data-stu-id="47dc0-419">ListRootFolder</span></span>
<span data-ttu-id="47dc0-420">List root folder: Lists files in the OneDrive for Business root folder</span><span class="sxs-lookup"><span data-stu-id="47dc0-420">List root folder: Lists files in the OneDrive for Business root folder</span></span>

```GET: /datasets/default/folders```

<span data-ttu-id="47dc0-421">There are no parameters for this call</span><span class="sxs-lookup"><span data-stu-id="47dc0-421">There are no parameters for this call</span></span>

#### <a name="response"></a><span data-ttu-id="47dc0-422">Response</span><span class="sxs-lookup"><span data-stu-id="47dc0-422">Response</span></span>
| <span data-ttu-id="47dc0-423">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-423">Name</span></span> | <span data-ttu-id="47dc0-424">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-424">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47dc0-425">200</span><span class="sxs-lookup"><span data-stu-id="47dc0-425">200</span></span> |<span data-ttu-id="47dc0-426">OK</span><span class="sxs-lookup"><span data-stu-id="47dc0-426">OK</span></span> |
| <span data-ttu-id="47dc0-427">default</span><span class="sxs-lookup"><span data-stu-id="47dc0-427">default</span></span> |<span data-ttu-id="47dc0-428">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="47dc0-428">Operation Failed.</span></span> |

## <a name="extractfolderv2"></a><span data-ttu-id="47dc0-429">ExtractFolderV2</span><span class="sxs-lookup"><span data-stu-id="47dc0-429">ExtractFolderV2</span></span>
<span data-ttu-id="47dc0-430">Extract folder: Extracts a folder to OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="47dc0-430">Extract folder: Extracts a folder to OneDrive for Business</span></span>

```POST: /datasets/default/extractFolderV2```

| <span data-ttu-id="47dc0-431">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-431">Name</span></span> | <span data-ttu-id="47dc0-432">Data Type</span><span class="sxs-lookup"><span data-stu-id="47dc0-432">Data Type</span></span> | <span data-ttu-id="47dc0-433">Required</span><span class="sxs-lookup"><span data-stu-id="47dc0-433">Required</span></span> | <span data-ttu-id="47dc0-434">Located In</span><span class="sxs-lookup"><span data-stu-id="47dc0-434">Located In</span></span> | <span data-ttu-id="47dc0-435">Default Value</span><span class="sxs-lookup"><span data-stu-id="47dc0-435">Default Value</span></span> | <span data-ttu-id="47dc0-436">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-436">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="47dc0-437">source</span><span class="sxs-lookup"><span data-stu-id="47dc0-437">source</span></span> |<span data-ttu-id="47dc0-438">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-438">string</span></span> |<span data-ttu-id="47dc0-439">yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-439">yes</span></span> |<span data-ttu-id="47dc0-440">query</span><span class="sxs-lookup"><span data-stu-id="47dc0-440">query</span></span> |<span data-ttu-id="47dc0-441">none</span><span class="sxs-lookup"><span data-stu-id="47dc0-441">none</span></span> |<span data-ttu-id="47dc0-442">Path to the archive file</span><span class="sxs-lookup"><span data-stu-id="47dc0-442">Path to the archive file</span></span> |
| <span data-ttu-id="47dc0-443">destination</span><span class="sxs-lookup"><span data-stu-id="47dc0-443">destination</span></span> |<span data-ttu-id="47dc0-444">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-444">string</span></span> |<span data-ttu-id="47dc0-445">yes</span><span class="sxs-lookup"><span data-stu-id="47dc0-445">yes</span></span> |<span data-ttu-id="47dc0-446">query</span><span class="sxs-lookup"><span data-stu-id="47dc0-446">query</span></span> |<span data-ttu-id="47dc0-447">none</span><span class="sxs-lookup"><span data-stu-id="47dc0-447">none</span></span> |<span data-ttu-id="47dc0-448">Path in OneDrive for Business to extract the archive contents</span><span class="sxs-lookup"><span data-stu-id="47dc0-448">Path in OneDrive for Business to extract the archive contents</span></span> |
| <span data-ttu-id="47dc0-449">overwrite</span><span class="sxs-lookup"><span data-stu-id="47dc0-449">overwrite</span></span> |<span data-ttu-id="47dc0-450">boolean</span><span class="sxs-lookup"><span data-stu-id="47dc0-450">boolean</span></span> |<span data-ttu-id="47dc0-451">no</span><span class="sxs-lookup"><span data-stu-id="47dc0-451">no</span></span> |<span data-ttu-id="47dc0-452">query</span><span class="sxs-lookup"><span data-stu-id="47dc0-452">query</span></span> |<span data-ttu-id="47dc0-453">false</span><span class="sxs-lookup"><span data-stu-id="47dc0-453">false</span></span> |<span data-ttu-id="47dc0-454">Overwrites the destination files if set to 'true'</span><span class="sxs-lookup"><span data-stu-id="47dc0-454">Overwrites the destination files if set to 'true'</span></span> |

#### <a name="response"></a><span data-ttu-id="47dc0-455">Response</span><span class="sxs-lookup"><span data-stu-id="47dc0-455">Response</span></span>
| <span data-ttu-id="47dc0-456">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-456">Name</span></span> | <span data-ttu-id="47dc0-457">Description</span><span class="sxs-lookup"><span data-stu-id="47dc0-457">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47dc0-458">200</span><span class="sxs-lookup"><span data-stu-id="47dc0-458">200</span></span> |<span data-ttu-id="47dc0-459">OK</span><span class="sxs-lookup"><span data-stu-id="47dc0-459">OK</span></span> |
| <span data-ttu-id="47dc0-460">default</span><span class="sxs-lookup"><span data-stu-id="47dc0-460">default</span></span> |<span data-ttu-id="47dc0-461">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="47dc0-461">Operation Failed.</span></span> |

## <a name="object-definitions"></a><span data-ttu-id="47dc0-462">Object definitions</span><span class="sxs-lookup"><span data-stu-id="47dc0-462">Object definitions</span></span>
### <a name="datasetsmetadata"></a><span data-ttu-id="47dc0-463">DataSetsMetadata</span><span class="sxs-lookup"><span data-stu-id="47dc0-463">DataSetsMetadata</span></span>
| <span data-ttu-id="47dc0-464">Property Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-464">Property Name</span></span> | <span data-ttu-id="47dc0-465">Data Type</span><span class="sxs-lookup"><span data-stu-id="47dc0-465">Data Type</span></span> | <span data-ttu-id="47dc0-466">Required</span><span class="sxs-lookup"><span data-stu-id="47dc0-466">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47dc0-467">tabular</span><span class="sxs-lookup"><span data-stu-id="47dc0-467">tabular</span></span> |<span data-ttu-id="47dc0-468">not defined</span><span class="sxs-lookup"><span data-stu-id="47dc0-468">not defined</span></span> |<span data-ttu-id="47dc0-469">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-469">No</span></span> |
| <span data-ttu-id="47dc0-470">blob</span><span class="sxs-lookup"><span data-stu-id="47dc0-470">blob</span></span> |<span data-ttu-id="47dc0-471">not defined</span><span class="sxs-lookup"><span data-stu-id="47dc0-471">not defined</span></span> |<span data-ttu-id="47dc0-472">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-472">No</span></span> |

### <a name="tabulardatasetsmetadata"></a><span data-ttu-id="47dc0-473">TabularDataSetsMetadata</span><span class="sxs-lookup"><span data-stu-id="47dc0-473">TabularDataSetsMetadata</span></span>
| <span data-ttu-id="47dc0-474">Property Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-474">Property Name</span></span> | <span data-ttu-id="47dc0-475">Data Type</span><span class="sxs-lookup"><span data-stu-id="47dc0-475">Data Type</span></span> | <span data-ttu-id="47dc0-476">Required</span><span class="sxs-lookup"><span data-stu-id="47dc0-476">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47dc0-477">source</span><span class="sxs-lookup"><span data-stu-id="47dc0-477">source</span></span> |<span data-ttu-id="47dc0-478">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-478">string</span></span> |<span data-ttu-id="47dc0-479">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-479">No</span></span> |
| <span data-ttu-id="47dc0-480">displayName</span><span class="sxs-lookup"><span data-stu-id="47dc0-480">displayName</span></span> |<span data-ttu-id="47dc0-481">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-481">string</span></span> |<span data-ttu-id="47dc0-482">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-482">No</span></span> |
| <span data-ttu-id="47dc0-483">urlEncoding</span><span class="sxs-lookup"><span data-stu-id="47dc0-483">urlEncoding</span></span> |<span data-ttu-id="47dc0-484">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-484">string</span></span> |<span data-ttu-id="47dc0-485">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-485">No</span></span> |
| <span data-ttu-id="47dc0-486">tableDisplayName</span><span class="sxs-lookup"><span data-stu-id="47dc0-486">tableDisplayName</span></span> |<span data-ttu-id="47dc0-487">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-487">string</span></span> |<span data-ttu-id="47dc0-488">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-488">No</span></span> |
| <span data-ttu-id="47dc0-489">tablePluralName</span><span class="sxs-lookup"><span data-stu-id="47dc0-489">tablePluralName</span></span> |<span data-ttu-id="47dc0-490">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-490">string</span></span> |<span data-ttu-id="47dc0-491">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-491">No</span></span> |

### <a name="blobdatasetsmetadata"></a><span data-ttu-id="47dc0-492">BlobDataSetsMetadata</span><span class="sxs-lookup"><span data-stu-id="47dc0-492">BlobDataSetsMetadata</span></span>
| <span data-ttu-id="47dc0-493">Property Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-493">Property Name</span></span> | <span data-ttu-id="47dc0-494">Data Type</span><span class="sxs-lookup"><span data-stu-id="47dc0-494">Data Type</span></span> | <span data-ttu-id="47dc0-495">Required</span><span class="sxs-lookup"><span data-stu-id="47dc0-495">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47dc0-496">source</span><span class="sxs-lookup"><span data-stu-id="47dc0-496">source</span></span> |<span data-ttu-id="47dc0-497">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-497">string</span></span> |<span data-ttu-id="47dc0-498">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-498">No</span></span> |
| <span data-ttu-id="47dc0-499">displayName</span><span class="sxs-lookup"><span data-stu-id="47dc0-499">displayName</span></span> |<span data-ttu-id="47dc0-500">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-500">string</span></span> |<span data-ttu-id="47dc0-501">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-501">No</span></span> |
| <span data-ttu-id="47dc0-502">urlEncoding</span><span class="sxs-lookup"><span data-stu-id="47dc0-502">urlEncoding</span></span> |<span data-ttu-id="47dc0-503">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-503">string</span></span> |<span data-ttu-id="47dc0-504">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-504">No</span></span> |

### <a name="blobmetadata"></a><span data-ttu-id="47dc0-505">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="47dc0-505">BlobMetadata</span></span>
| <span data-ttu-id="47dc0-506">Property Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-506">Property Name</span></span> | <span data-ttu-id="47dc0-507">Data Type</span><span class="sxs-lookup"><span data-stu-id="47dc0-507">Data Type</span></span> | <span data-ttu-id="47dc0-508">Required</span><span class="sxs-lookup"><span data-stu-id="47dc0-508">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47dc0-509">Id</span><span class="sxs-lookup"><span data-stu-id="47dc0-509">Id</span></span> |<span data-ttu-id="47dc0-510">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-510">string</span></span> |<span data-ttu-id="47dc0-511">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-511">No</span></span> |
| <span data-ttu-id="47dc0-512">Name</span><span class="sxs-lookup"><span data-stu-id="47dc0-512">Name</span></span> |<span data-ttu-id="47dc0-513">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-513">string</span></span> |<span data-ttu-id="47dc0-514">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-514">No</span></span> |
| <span data-ttu-id="47dc0-515">DisplayName</span><span class="sxs-lookup"><span data-stu-id="47dc0-515">DisplayName</span></span> |<span data-ttu-id="47dc0-516">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-516">string</span></span> |<span data-ttu-id="47dc0-517">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-517">No</span></span> |
| <span data-ttu-id="47dc0-518">Path</span><span class="sxs-lookup"><span data-stu-id="47dc0-518">Path</span></span> |<span data-ttu-id="47dc0-519">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-519">string</span></span> |<span data-ttu-id="47dc0-520">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-520">No</span></span> |
| <span data-ttu-id="47dc0-521">LastModified</span><span class="sxs-lookup"><span data-stu-id="47dc0-521">LastModified</span></span> |<span data-ttu-id="47dc0-522">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-522">string</span></span> |<span data-ttu-id="47dc0-523">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-523">No</span></span> |
| <span data-ttu-id="47dc0-524">Size</span><span class="sxs-lookup"><span data-stu-id="47dc0-524">Size</span></span> |<span data-ttu-id="47dc0-525">integer</span><span class="sxs-lookup"><span data-stu-id="47dc0-525">integer</span></span> |<span data-ttu-id="47dc0-526">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-526">No</span></span> |
| <span data-ttu-id="47dc0-527">MediaType</span><span class="sxs-lookup"><span data-stu-id="47dc0-527">MediaType</span></span> |<span data-ttu-id="47dc0-528">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-528">string</span></span> |<span data-ttu-id="47dc0-529">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-529">No</span></span> |
| <span data-ttu-id="47dc0-530">IsFolder</span><span class="sxs-lookup"><span data-stu-id="47dc0-530">IsFolder</span></span> |<span data-ttu-id="47dc0-531">boolean</span><span class="sxs-lookup"><span data-stu-id="47dc0-531">boolean</span></span> |<span data-ttu-id="47dc0-532">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-532">No</span></span> |
| <span data-ttu-id="47dc0-533">ETag</span><span class="sxs-lookup"><span data-stu-id="47dc0-533">ETag</span></span> |<span data-ttu-id="47dc0-534">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-534">string</span></span> |<span data-ttu-id="47dc0-535">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-535">No</span></span> |
| <span data-ttu-id="47dc0-536">FileLocator</span><span class="sxs-lookup"><span data-stu-id="47dc0-536">FileLocator</span></span> |<span data-ttu-id="47dc0-537">string</span><span class="sxs-lookup"><span data-stu-id="47dc0-537">string</span></span> |<span data-ttu-id="47dc0-538">No</span><span class="sxs-lookup"><span data-stu-id="47dc0-538">No</span></span> |

### <a name="object"></a><span data-ttu-id="47dc0-539">Object</span><span class="sxs-lookup"><span data-stu-id="47dc0-539">Object</span></span>
## <a name="next-steps"></a><span data-ttu-id="47dc0-540">Next Steps</span><span class="sxs-lookup"><span data-stu-id="47dc0-540">Next Steps</span></span>
[<span data-ttu-id="47dc0-541">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="47dc0-541">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

