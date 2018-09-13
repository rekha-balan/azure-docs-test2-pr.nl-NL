---
title: Dropbox | Microsoft Docs
description: Create Logic apps with Azure App service. Connect to Dropbox to manage your files. You can perform various actions such as upload, update, get, and delete files in Dropbox.
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: deonhe
ms.openlocfilehash: 7baa8d0a436f64a9f12ea4169aaa6d047ddae52a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564741"
---
# <a name="get-started-with-the-dropbox-connector"></a><span data-ttu-id="c3bd1-105">Get started with the Dropbox connector</span><span class="sxs-lookup"><span data-stu-id="c3bd1-105">Get started with the Dropbox connector</span></span>
<span data-ttu-id="c3bd1-106">Connect to Dropbox to manage your files.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-106">Connect to Dropbox to manage your files.</span></span> <span data-ttu-id="c3bd1-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="c3bd1-108">To use [any connector](apis-list.md), you first need to create a logic app.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="c3bd1-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c3bd1-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-dropbox"></a><span data-ttu-id="c3bd1-110">Connect to Dropbox</span><span class="sxs-lookup"><span data-stu-id="c3bd1-110">Connect to Dropbox</span></span>
<span data-ttu-id="c3bd1-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="c3bd1-112">A connection provides connectivity between a logic app and another service.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="c3bd1-113">For example, in order to connect to Dropbox, you first need a Dropbox *connection*.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-113">For example, in order to connect to Dropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="c3bd1-114">To create a connection, you would need to provide the credentials you normally use to access the service you wish to connect to.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-114">To create a connection, you would need to provide the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="c3bd1-115">So, in the Dropbox example, you would need the credentials to your Dropbox account in order to create the connection to Dropbox.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-115">So, in the Dropbox example, you would need the credentials to your Dropbox account in order to create the connection to Dropbox.</span></span> [<span data-ttu-id="c3bd1-116">Learn more about connections</span><span class="sxs-lookup"><span data-stu-id="c3bd1-116">Learn more about connections</span></span>]()

### <a name="create-a-connection-to-dropbox"></a><span data-ttu-id="c3bd1-117">Create a connection to Dropbox</span><span class="sxs-lookup"><span data-stu-id="c3bd1-117">Create a connection to Dropbox</span></span>
> [!INCLUDE [Steps to create a connection to Dropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="c3bd1-118">Use a Dropbox trigger</span><span class="sxs-lookup"><span data-stu-id="c3bd1-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="c3bd1-119">A trigger is an event that can be used to start the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-119">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="c3bd1-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c3bd1-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="c3bd1-121">In this example, we will use the **When a file is created** trigger.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-121">In this example, we will use the **When a file is created** trigger.</span></span> <span data-ttu-id="c3bd1-122">When this trigger occurs, we will call the **Get file content using path** Dropbox action.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-122">When this trigger occurs, we will call the **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="c3bd1-123">Enter *dropbox* in the search box on the Logic Apps designer, then select the **Dropbox - When a file is created** trigger.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-123">Enter *dropbox* in the search box on the Logic Apps designer, then select the **Dropbox - When a file is created** trigger.</span></span>      
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="c3bd1-124">Select the folder in which you want to track file creation.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-124">Select the folder in which you want to track file creation.</span></span> <span data-ttu-id="c3bd1-125">Select ... (identified in the red box) and browse to the folder you wish to select for the trigger's input.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-125">Select ... (identified in the red box) and browse to the folder you wish to select for the trigger's input.</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="c3bd1-126">Use a Dropbox action</span><span class="sxs-lookup"><span data-stu-id="c3bd1-126">Use a Dropbox action</span></span>
<span data-ttu-id="c3bd1-127">An action is an operation carried out by the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-127">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="c3bd1-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c3bd1-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="c3bd1-129">Now that the trigger has been added, follow these steps to add an action that will get the new file's content.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-129">Now that the trigger has been added, follow these steps to add an action that will get the new file's content.</span></span>

1. <span data-ttu-id="c3bd1-130">Select **+ New Step** to add the action you would like to take when a new file is created.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-130">Select **+ New Step** to add the action you would like to take when a new file is created.</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="c3bd1-131">Select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-131">Select **Add an action**.</span></span> <span data-ttu-id="c3bd1-132">This opens the search box where you can search for any action you would like to take.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-132">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="c3bd1-133">Enter *dropbox* to search for actions related to Dropbox.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-133">Enter *dropbox* to search for actions related to Dropbox.</span></span>  
4. <span data-ttu-id="c3bd1-134">Select **Dropbox - Get file content using path** as the action to take when a new file is created in the selected Dropbox folder.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-134">Select **Dropbox - Get file content using path** as the action to take when a new file is created in the selected Dropbox folder.</span></span> <span data-ttu-id="c3bd1-135">The action control block opens.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-135">The action control block opens.</span></span> <span data-ttu-id="c3bd1-136">You will be prompted to authorize your logic app to access your Dropbox account if you have not done so previously.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-136">You will be prompted to authorize your logic app to access your Dropbox account if you have not done so previously.</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="c3bd1-137">Select ... (located at the right side of the **File Path** control) and browse to the file path you would like to use.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-137">Select ... (located at the right side of the **File Path** control) and browse to the file path you would like to use.</span></span> <span data-ttu-id="c3bd1-138">Or, use the **file path** token to speed up your logic app creation.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-138">Or, use the **file path** token to speed up your logic app creation.</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="c3bd1-139">Save your work and create a new file in Dropbox to activate your workflow.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-139">Save your work and create a new file in Dropbox to activate your workflow.</span></span>  

## <a name="technical-details"></a><span data-ttu-id="c3bd1-140">Technical details</span><span class="sxs-lookup"><span data-stu-id="c3bd1-140">Technical details</span></span>
<span data-ttu-id="c3bd1-141">Here are the details about the triggers, actions and responses that this connection supports:</span><span class="sxs-lookup"><span data-stu-id="c3bd1-141">Here are the details about the triggers, actions and responses that this connection supports:</span></span>

## <a name="dropbox-triggers"></a><span data-ttu-id="c3bd1-142">Dropbox triggers</span><span class="sxs-lookup"><span data-stu-id="c3bd1-142">Dropbox triggers</span></span>
<span data-ttu-id="c3bd1-143">The Dropbox connector has the following trigger(s):</span><span class="sxs-lookup"><span data-stu-id="c3bd1-143">The Dropbox connector has the following trigger(s):</span></span>  

| <span data-ttu-id="c3bd1-144">Trigger</span><span class="sxs-lookup"><span data-stu-id="c3bd1-144">Trigger</span></span> | <span data-ttu-id="c3bd1-145">Description</span><span class="sxs-lookup"><span data-stu-id="c3bd1-145">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="c3bd1-146">When a file is created</span><span class="sxs-lookup"><span data-stu-id="c3bd1-146">When a file is created</span></span>](connectors-create-api-dropbox.md#when-a-file-is-created) |<span data-ttu-id="c3bd1-147">This operation triggers a flow when a new file is created in a folder.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-147">This operation triggers a flow when a new file is created in a folder.</span></span> |
| [<span data-ttu-id="c3bd1-148">When a file is modified</span><span class="sxs-lookup"><span data-stu-id="c3bd1-148">When a file is modified</span></span>](connectors-create-api-dropbox.md#when-a-file-is-modified) |<span data-ttu-id="c3bd1-149">This operation triggers a flow when a file is modified in a folder.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-149">This operation triggers a flow when a file is modified in a folder.</span></span> |

## <a name="dropbox-actions"></a><span data-ttu-id="c3bd1-150">Dropbox actions</span><span class="sxs-lookup"><span data-stu-id="c3bd1-150">Dropbox actions</span></span>
<span data-ttu-id="c3bd1-151">The Dropbox connector has the following actions:</span><span class="sxs-lookup"><span data-stu-id="c3bd1-151">The Dropbox connector has the following actions:</span></span>

| <span data-ttu-id="c3bd1-152">Action</span><span class="sxs-lookup"><span data-stu-id="c3bd1-152">Action</span></span> | <span data-ttu-id="c3bd1-153">Description</span><span class="sxs-lookup"><span data-stu-id="c3bd1-153">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="c3bd1-154">Get file metadata</span><span class="sxs-lookup"><span data-stu-id="c3bd1-154">Get file metadata</span></span>](connectors-create-api-dropbox.md#get-file-metadata) |<span data-ttu-id="c3bd1-155">This operation gets the metadata for a file.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-155">This operation gets the metadata for a file.</span></span> |
| [<span data-ttu-id="c3bd1-156">Update file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-156">Update file</span></span>](connectors-create-api-dropbox.md#update-file) |<span data-ttu-id="c3bd1-157">This operation updates a file.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-157">This operation updates a file.</span></span> |
| [<span data-ttu-id="c3bd1-158">Delete file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-158">Delete file</span></span>](connectors-create-api-dropbox.md#delete-file) |<span data-ttu-id="c3bd1-159">This operation deletes a file.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-159">This operation deletes a file.</span></span> |
| [<span data-ttu-id="c3bd1-160">Get file metadata using path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-160">Get file metadata using path</span></span>](connectors-create-api-dropbox.md#get-file-metadata-using-path) |<span data-ttu-id="c3bd1-161">This operation gets the metadata of a file using the path.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-161">This operation gets the metadata of a file using the path.</span></span> |
| [<span data-ttu-id="c3bd1-162">Get file content using path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-162">Get file content using path</span></span>](connectors-create-api-dropbox.md#get-file-content-using-path) |<span data-ttu-id="c3bd1-163">This operation gets the content of a file using the path.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-163">This operation gets the content of a file using the path.</span></span> |
| [<span data-ttu-id="c3bd1-164">Get file content</span><span class="sxs-lookup"><span data-stu-id="c3bd1-164">Get file content</span></span>](connectors-create-api-dropbox.md#get-file-content) |<span data-ttu-id="c3bd1-165">This operation gets the content of a file.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-165">This operation gets the content of a file.</span></span> |
| [<span data-ttu-id="c3bd1-166">Create file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-166">Create file</span></span>](connectors-create-api-dropbox.md#create-file) |<span data-ttu-id="c3bd1-167">This operation creates a file.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-167">This operation creates a file.</span></span> |
| [<span data-ttu-id="c3bd1-168">Copy file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-168">Copy file</span></span>](connectors-create-api-dropbox.md#copy-file) |<span data-ttu-id="c3bd1-169">This operation copies a file to Dropbox.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-169">This operation copies a file to Dropbox.</span></span> |
| [<span data-ttu-id="c3bd1-170">List files in folder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-170">List files in folder</span></span>](connectors-create-api-dropbox.md#list-files-in-folder) |<span data-ttu-id="c3bd1-171">This operation gets the list of files and subfolders in a folder.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-171">This operation gets the list of files and subfolders in a folder.</span></span> |
| [<span data-ttu-id="c3bd1-172">List files in root folder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-172">List files in root folder</span></span>](connectors-create-api-dropbox.md#list-files-in-root-folder) |<span data-ttu-id="c3bd1-173">This operation gets the list of files and subfolders in the root folder.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-173">This operation gets the list of files and subfolders in the root folder.</span></span> |
| [<span data-ttu-id="c3bd1-174">Extract archive to folder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-174">Extract archive to folder</span></span>](connectors-create-api-dropbox.md#extract-archive-to-folder) |<span data-ttu-id="c3bd1-175">This operation extracts an archive file into a folder (example: .zip).</span><span class="sxs-lookup"><span data-stu-id="c3bd1-175">This operation extracts an archive file into a folder (example: .zip).</span></span> |

### <a name="action-details"></a><span data-ttu-id="c3bd1-176">Action details</span><span class="sxs-lookup"><span data-stu-id="c3bd1-176">Action details</span></span>
<span data-ttu-id="c3bd1-177">Here are the details for the actions and triggers for this connector, along with their responses:</span><span class="sxs-lookup"><span data-stu-id="c3bd1-177">Here are the details for the actions and triggers for this connector, along with their responses:</span></span>

### <a name="get-file-metadata"></a><span data-ttu-id="c3bd1-178">Get file metadata</span><span class="sxs-lookup"><span data-stu-id="c3bd1-178">Get file metadata</span></span>
<span data-ttu-id="c3bd1-179">This operation gets the metadata for a file.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-179">This operation gets the metadata for a file.</span></span> 

| <span data-ttu-id="c3bd1-180">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-180">Property Name</span></span> | <span data-ttu-id="c3bd1-181">Display Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-181">Display Name</span></span> | <span data-ttu-id="c3bd1-182">Description</span><span class="sxs-lookup"><span data-stu-id="c3bd1-182">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3bd1-183">id\*</span><span class="sxs-lookup"><span data-stu-id="c3bd1-183">id\*</span></span> |<span data-ttu-id="c3bd1-184">File</span><span class="sxs-lookup"><span data-stu-id="c3bd1-184">File</span></span> |<span data-ttu-id="c3bd1-185">Select a file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-185">Select a file</span></span> |

<span data-ttu-id="c3bd1-186">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="c3bd1-186">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="c3bd1-187">Output Details</span><span class="sxs-lookup"><span data-stu-id="c3bd1-187">Output Details</span></span>
<span data-ttu-id="c3bd1-188">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="c3bd1-188">BlobMetadata</span></span>

| <span data-ttu-id="c3bd1-189">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-189">Property Name</span></span> | <span data-ttu-id="c3bd1-190">Data Type</span><span class="sxs-lookup"><span data-stu-id="c3bd1-190">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="c3bd1-191">Id</span><span class="sxs-lookup"><span data-stu-id="c3bd1-191">Id</span></span> |<span data-ttu-id="c3bd1-192">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-192">string</span></span> |
| <span data-ttu-id="c3bd1-193">Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-193">Name</span></span> |<span data-ttu-id="c3bd1-194">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-194">string</span></span> |
| <span data-ttu-id="c3bd1-195">DisplayName</span><span class="sxs-lookup"><span data-stu-id="c3bd1-195">DisplayName</span></span> |<span data-ttu-id="c3bd1-196">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-196">string</span></span> |
| <span data-ttu-id="c3bd1-197">Path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-197">Path</span></span> |<span data-ttu-id="c3bd1-198">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-198">string</span></span> |
| <span data-ttu-id="c3bd1-199">LastModified</span><span class="sxs-lookup"><span data-stu-id="c3bd1-199">LastModified</span></span> |<span data-ttu-id="c3bd1-200">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-200">string</span></span> |
| <span data-ttu-id="c3bd1-201">Size</span><span class="sxs-lookup"><span data-stu-id="c3bd1-201">Size</span></span> |<span data-ttu-id="c3bd1-202">integer</span><span class="sxs-lookup"><span data-stu-id="c3bd1-202">integer</span></span> |
| <span data-ttu-id="c3bd1-203">MediaType</span><span class="sxs-lookup"><span data-stu-id="c3bd1-203">MediaType</span></span> |<span data-ttu-id="c3bd1-204">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-204">string</span></span> |
| <span data-ttu-id="c3bd1-205">IsFolder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-205">IsFolder</span></span> |<span data-ttu-id="c3bd1-206">boolean</span><span class="sxs-lookup"><span data-stu-id="c3bd1-206">boolean</span></span> |
| <span data-ttu-id="c3bd1-207">ETag</span><span class="sxs-lookup"><span data-stu-id="c3bd1-207">ETag</span></span> |<span data-ttu-id="c3bd1-208">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-208">string</span></span> |
| <span data-ttu-id="c3bd1-209">FileLocator</span><span class="sxs-lookup"><span data-stu-id="c3bd1-209">FileLocator</span></span> |<span data-ttu-id="c3bd1-210">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-210">string</span></span> |

### <a name="update-file"></a><span data-ttu-id="c3bd1-211">Update file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-211">Update file</span></span>
<span data-ttu-id="c3bd1-212">This operation updates a file.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-212">This operation updates a file.</span></span> 

| <span data-ttu-id="c3bd1-213">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-213">Property Name</span></span> | <span data-ttu-id="c3bd1-214">Display Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-214">Display Name</span></span> | <span data-ttu-id="c3bd1-215">Description</span><span class="sxs-lookup"><span data-stu-id="c3bd1-215">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3bd1-216">id\*</span><span class="sxs-lookup"><span data-stu-id="c3bd1-216">id\*</span></span> |<span data-ttu-id="c3bd1-217">File</span><span class="sxs-lookup"><span data-stu-id="c3bd1-217">File</span></span> |<span data-ttu-id="c3bd1-218">Select a file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-218">Select a file</span></span> |
| <span data-ttu-id="c3bd1-219">body\*</span><span class="sxs-lookup"><span data-stu-id="c3bd1-219">body\*</span></span> |<span data-ttu-id="c3bd1-220">File content</span><span class="sxs-lookup"><span data-stu-id="c3bd1-220">File content</span></span> |<span data-ttu-id="c3bd1-221">Content of the file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-221">Content of the file</span></span> |

<span data-ttu-id="c3bd1-222">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="c3bd1-222">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="c3bd1-223">Output Details</span><span class="sxs-lookup"><span data-stu-id="c3bd1-223">Output Details</span></span>
<span data-ttu-id="c3bd1-224">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="c3bd1-224">BlobMetadata</span></span>

| <span data-ttu-id="c3bd1-225">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-225">Property Name</span></span> | <span data-ttu-id="c3bd1-226">Data Type</span><span class="sxs-lookup"><span data-stu-id="c3bd1-226">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="c3bd1-227">Id</span><span class="sxs-lookup"><span data-stu-id="c3bd1-227">Id</span></span> |<span data-ttu-id="c3bd1-228">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-228">string</span></span> |
| <span data-ttu-id="c3bd1-229">Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-229">Name</span></span> |<span data-ttu-id="c3bd1-230">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-230">string</span></span> |
| <span data-ttu-id="c3bd1-231">DisplayName</span><span class="sxs-lookup"><span data-stu-id="c3bd1-231">DisplayName</span></span> |<span data-ttu-id="c3bd1-232">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-232">string</span></span> |
| <span data-ttu-id="c3bd1-233">Path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-233">Path</span></span> |<span data-ttu-id="c3bd1-234">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-234">string</span></span> |
| <span data-ttu-id="c3bd1-235">LastModified</span><span class="sxs-lookup"><span data-stu-id="c3bd1-235">LastModified</span></span> |<span data-ttu-id="c3bd1-236">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-236">string</span></span> |
| <span data-ttu-id="c3bd1-237">Size</span><span class="sxs-lookup"><span data-stu-id="c3bd1-237">Size</span></span> |<span data-ttu-id="c3bd1-238">integer</span><span class="sxs-lookup"><span data-stu-id="c3bd1-238">integer</span></span> |
| <span data-ttu-id="c3bd1-239">MediaType</span><span class="sxs-lookup"><span data-stu-id="c3bd1-239">MediaType</span></span> |<span data-ttu-id="c3bd1-240">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-240">string</span></span> |
| <span data-ttu-id="c3bd1-241">IsFolder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-241">IsFolder</span></span> |<span data-ttu-id="c3bd1-242">boolean</span><span class="sxs-lookup"><span data-stu-id="c3bd1-242">boolean</span></span> |
| <span data-ttu-id="c3bd1-243">ETag</span><span class="sxs-lookup"><span data-stu-id="c3bd1-243">ETag</span></span> |<span data-ttu-id="c3bd1-244">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-244">string</span></span> |
| <span data-ttu-id="c3bd1-245">FileLocator</span><span class="sxs-lookup"><span data-stu-id="c3bd1-245">FileLocator</span></span> |<span data-ttu-id="c3bd1-246">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-246">string</span></span> |

### <a name="delete-file"></a><span data-ttu-id="c3bd1-247">Delete file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-247">Delete file</span></span>
<span data-ttu-id="c3bd1-248">This operation deletes a file.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-248">This operation deletes a file.</span></span> 

| <span data-ttu-id="c3bd1-249">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-249">Property Name</span></span> | <span data-ttu-id="c3bd1-250">Display Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-250">Display Name</span></span> | <span data-ttu-id="c3bd1-251">Description</span><span class="sxs-lookup"><span data-stu-id="c3bd1-251">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3bd1-252">id\*</span><span class="sxs-lookup"><span data-stu-id="c3bd1-252">id\*</span></span> |<span data-ttu-id="c3bd1-253">File</span><span class="sxs-lookup"><span data-stu-id="c3bd1-253">File</span></span> |<span data-ttu-id="c3bd1-254">Select a file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-254">Select a file</span></span> |

<span data-ttu-id="c3bd1-255">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="c3bd1-255">An \* indicates that a property is required</span></span>

### <a name="get-file-metadata-using-path"></a><span data-ttu-id="c3bd1-256">Get file metadata using path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-256">Get file metadata using path</span></span>
<span data-ttu-id="c3bd1-257">This operation gets the metadata of a file using the path.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-257">This operation gets the metadata of a file using the path.</span></span> 

| <span data-ttu-id="c3bd1-258">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-258">Property Name</span></span> | <span data-ttu-id="c3bd1-259">Display Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-259">Display Name</span></span> | <span data-ttu-id="c3bd1-260">Description</span><span class="sxs-lookup"><span data-stu-id="c3bd1-260">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3bd1-261">path\*</span><span class="sxs-lookup"><span data-stu-id="c3bd1-261">path\*</span></span> |<span data-ttu-id="c3bd1-262">File path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-262">File path</span></span> |<span data-ttu-id="c3bd1-263">Select a file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-263">Select a file</span></span> |

<span data-ttu-id="c3bd1-264">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="c3bd1-264">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="c3bd1-265">Output Details</span><span class="sxs-lookup"><span data-stu-id="c3bd1-265">Output Details</span></span>
<span data-ttu-id="c3bd1-266">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="c3bd1-266">BlobMetadata</span></span>

| <span data-ttu-id="c3bd1-267">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-267">Property Name</span></span> | <span data-ttu-id="c3bd1-268">Data Type</span><span class="sxs-lookup"><span data-stu-id="c3bd1-268">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="c3bd1-269">Id</span><span class="sxs-lookup"><span data-stu-id="c3bd1-269">Id</span></span> |<span data-ttu-id="c3bd1-270">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-270">string</span></span> |
| <span data-ttu-id="c3bd1-271">Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-271">Name</span></span> |<span data-ttu-id="c3bd1-272">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-272">string</span></span> |
| <span data-ttu-id="c3bd1-273">DisplayName</span><span class="sxs-lookup"><span data-stu-id="c3bd1-273">DisplayName</span></span> |<span data-ttu-id="c3bd1-274">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-274">string</span></span> |
| <span data-ttu-id="c3bd1-275">Path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-275">Path</span></span> |<span data-ttu-id="c3bd1-276">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-276">string</span></span> |
| <span data-ttu-id="c3bd1-277">LastModified</span><span class="sxs-lookup"><span data-stu-id="c3bd1-277">LastModified</span></span> |<span data-ttu-id="c3bd1-278">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-278">string</span></span> |
| <span data-ttu-id="c3bd1-279">Size</span><span class="sxs-lookup"><span data-stu-id="c3bd1-279">Size</span></span> |<span data-ttu-id="c3bd1-280">integer</span><span class="sxs-lookup"><span data-stu-id="c3bd1-280">integer</span></span> |
| <span data-ttu-id="c3bd1-281">MediaType</span><span class="sxs-lookup"><span data-stu-id="c3bd1-281">MediaType</span></span> |<span data-ttu-id="c3bd1-282">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-282">string</span></span> |
| <span data-ttu-id="c3bd1-283">IsFolder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-283">IsFolder</span></span> |<span data-ttu-id="c3bd1-284">boolean</span><span class="sxs-lookup"><span data-stu-id="c3bd1-284">boolean</span></span> |
| <span data-ttu-id="c3bd1-285">ETag</span><span class="sxs-lookup"><span data-stu-id="c3bd1-285">ETag</span></span> |<span data-ttu-id="c3bd1-286">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-286">string</span></span> |
| <span data-ttu-id="c3bd1-287">FileLocator</span><span class="sxs-lookup"><span data-stu-id="c3bd1-287">FileLocator</span></span> |<span data-ttu-id="c3bd1-288">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-288">string</span></span> |

### <a name="get-file-content-using-path"></a><span data-ttu-id="c3bd1-289">Get file content using path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-289">Get file content using path</span></span>
<span data-ttu-id="c3bd1-290">This operation gets the content of a file using the path.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-290">This operation gets the content of a file using the path.</span></span> 

| <span data-ttu-id="c3bd1-291">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-291">Property Name</span></span> | <span data-ttu-id="c3bd1-292">Display Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-292">Display Name</span></span> | <span data-ttu-id="c3bd1-293">Description</span><span class="sxs-lookup"><span data-stu-id="c3bd1-293">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3bd1-294">path\*</span><span class="sxs-lookup"><span data-stu-id="c3bd1-294">path\*</span></span> |<span data-ttu-id="c3bd1-295">File path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-295">File path</span></span> |<span data-ttu-id="c3bd1-296">Select a file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-296">Select a file</span></span> |

<span data-ttu-id="c3bd1-297">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="c3bd1-297">An \* indicates that a property is required</span></span>

### <a name="get-file-content"></a><span data-ttu-id="c3bd1-298">Get file content</span><span class="sxs-lookup"><span data-stu-id="c3bd1-298">Get file content</span></span>
<span data-ttu-id="c3bd1-299">This operation gets the content of a file.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-299">This operation gets the content of a file.</span></span> 

| <span data-ttu-id="c3bd1-300">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-300">Property Name</span></span> | <span data-ttu-id="c3bd1-301">Display Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-301">Display Name</span></span> | <span data-ttu-id="c3bd1-302">Description</span><span class="sxs-lookup"><span data-stu-id="c3bd1-302">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3bd1-303">id\*</span><span class="sxs-lookup"><span data-stu-id="c3bd1-303">id\*</span></span> |<span data-ttu-id="c3bd1-304">File</span><span class="sxs-lookup"><span data-stu-id="c3bd1-304">File</span></span> |<span data-ttu-id="c3bd1-305">Select a file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-305">Select a file</span></span> |

<span data-ttu-id="c3bd1-306">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="c3bd1-306">An \* indicates that a property is required</span></span>

### <a name="create-file"></a><span data-ttu-id="c3bd1-307">Create file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-307">Create file</span></span>
<span data-ttu-id="c3bd1-308">This operation creates a file.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-308">This operation creates a file.</span></span> 

| <span data-ttu-id="c3bd1-309">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-309">Property Name</span></span> | <span data-ttu-id="c3bd1-310">Display Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-310">Display Name</span></span> | <span data-ttu-id="c3bd1-311">Description</span><span class="sxs-lookup"><span data-stu-id="c3bd1-311">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3bd1-312">folderPath\*</span><span class="sxs-lookup"><span data-stu-id="c3bd1-312">folderPath\*</span></span> |<span data-ttu-id="c3bd1-313">Folder path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-313">Folder path</span></span> |<span data-ttu-id="c3bd1-314">Select a folder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-314">Select a folder</span></span> |
| <span data-ttu-id="c3bd1-315">name\*</span><span class="sxs-lookup"><span data-stu-id="c3bd1-315">name\*</span></span> |<span data-ttu-id="c3bd1-316">File name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-316">File name</span></span> |<span data-ttu-id="c3bd1-317">Name of the file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-317">Name of the file</span></span> |
| <span data-ttu-id="c3bd1-318">body\*</span><span class="sxs-lookup"><span data-stu-id="c3bd1-318">body\*</span></span> |<span data-ttu-id="c3bd1-319">File content</span><span class="sxs-lookup"><span data-stu-id="c3bd1-319">File content</span></span> |<span data-ttu-id="c3bd1-320">Content of the file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-320">Content of the file</span></span> |

<span data-ttu-id="c3bd1-321">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="c3bd1-321">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="c3bd1-322">Output Details</span><span class="sxs-lookup"><span data-stu-id="c3bd1-322">Output Details</span></span>
<span data-ttu-id="c3bd1-323">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="c3bd1-323">BlobMetadata</span></span>

| <span data-ttu-id="c3bd1-324">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-324">Property Name</span></span> | <span data-ttu-id="c3bd1-325">Data Type</span><span class="sxs-lookup"><span data-stu-id="c3bd1-325">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="c3bd1-326">Id</span><span class="sxs-lookup"><span data-stu-id="c3bd1-326">Id</span></span> |<span data-ttu-id="c3bd1-327">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-327">string</span></span> |
| <span data-ttu-id="c3bd1-328">Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-328">Name</span></span> |<span data-ttu-id="c3bd1-329">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-329">string</span></span> |
| <span data-ttu-id="c3bd1-330">DisplayName</span><span class="sxs-lookup"><span data-stu-id="c3bd1-330">DisplayName</span></span> |<span data-ttu-id="c3bd1-331">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-331">string</span></span> |
| <span data-ttu-id="c3bd1-332">Path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-332">Path</span></span> |<span data-ttu-id="c3bd1-333">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-333">string</span></span> |
| <span data-ttu-id="c3bd1-334">LastModified</span><span class="sxs-lookup"><span data-stu-id="c3bd1-334">LastModified</span></span> |<span data-ttu-id="c3bd1-335">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-335">string</span></span> |
| <span data-ttu-id="c3bd1-336">Size</span><span class="sxs-lookup"><span data-stu-id="c3bd1-336">Size</span></span> |<span data-ttu-id="c3bd1-337">integer</span><span class="sxs-lookup"><span data-stu-id="c3bd1-337">integer</span></span> |
| <span data-ttu-id="c3bd1-338">MediaType</span><span class="sxs-lookup"><span data-stu-id="c3bd1-338">MediaType</span></span> |<span data-ttu-id="c3bd1-339">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-339">string</span></span> |
| <span data-ttu-id="c3bd1-340">IsFolder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-340">IsFolder</span></span> |<span data-ttu-id="c3bd1-341">boolean</span><span class="sxs-lookup"><span data-stu-id="c3bd1-341">boolean</span></span> |
| <span data-ttu-id="c3bd1-342">ETag</span><span class="sxs-lookup"><span data-stu-id="c3bd1-342">ETag</span></span> |<span data-ttu-id="c3bd1-343">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-343">string</span></span> |
| <span data-ttu-id="c3bd1-344">FileLocator</span><span class="sxs-lookup"><span data-stu-id="c3bd1-344">FileLocator</span></span> |<span data-ttu-id="c3bd1-345">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-345">string</span></span> |

### <a name="copy-file"></a><span data-ttu-id="c3bd1-346">Copy file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-346">Copy file</span></span>
<span data-ttu-id="c3bd1-347">This operation copies a file to Dropbox.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-347">This operation copies a file to Dropbox.</span></span> 

| <span data-ttu-id="c3bd1-348">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-348">Property Name</span></span> | <span data-ttu-id="c3bd1-349">Display Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-349">Display Name</span></span> | <span data-ttu-id="c3bd1-350">Description</span><span class="sxs-lookup"><span data-stu-id="c3bd1-350">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3bd1-351">source\*</span><span class="sxs-lookup"><span data-stu-id="c3bd1-351">source\*</span></span> |<span data-ttu-id="c3bd1-352">Source url</span><span class="sxs-lookup"><span data-stu-id="c3bd1-352">Source url</span></span> |<span data-ttu-id="c3bd1-353">Url to source file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-353">Url to source file</span></span> |
| <span data-ttu-id="c3bd1-354">destination\*</span><span class="sxs-lookup"><span data-stu-id="c3bd1-354">destination\*</span></span> |<span data-ttu-id="c3bd1-355">Destination file path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-355">Destination file path</span></span> |<span data-ttu-id="c3bd1-356">Destination file path, including target filename</span><span class="sxs-lookup"><span data-stu-id="c3bd1-356">Destination file path, including target filename</span></span> |
| <span data-ttu-id="c3bd1-357">overwrite</span><span class="sxs-lookup"><span data-stu-id="c3bd1-357">overwrite</span></span> |<span data-ttu-id="c3bd1-358">Overwrite?</span><span class="sxs-lookup"><span data-stu-id="c3bd1-358">Overwrite?</span></span> |<span data-ttu-id="c3bd1-359">Overwrites the destination file if set to 'true'</span><span class="sxs-lookup"><span data-stu-id="c3bd1-359">Overwrites the destination file if set to 'true'</span></span> |

<span data-ttu-id="c3bd1-360">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="c3bd1-360">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="c3bd1-361">Output Details</span><span class="sxs-lookup"><span data-stu-id="c3bd1-361">Output Details</span></span>
<span data-ttu-id="c3bd1-362">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="c3bd1-362">BlobMetadata</span></span>

| <span data-ttu-id="c3bd1-363">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-363">Property Name</span></span> | <span data-ttu-id="c3bd1-364">Data Type</span><span class="sxs-lookup"><span data-stu-id="c3bd1-364">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="c3bd1-365">Id</span><span class="sxs-lookup"><span data-stu-id="c3bd1-365">Id</span></span> |<span data-ttu-id="c3bd1-366">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-366">string</span></span> |
| <span data-ttu-id="c3bd1-367">Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-367">Name</span></span> |<span data-ttu-id="c3bd1-368">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-368">string</span></span> |
| <span data-ttu-id="c3bd1-369">DisplayName</span><span class="sxs-lookup"><span data-stu-id="c3bd1-369">DisplayName</span></span> |<span data-ttu-id="c3bd1-370">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-370">string</span></span> |
| <span data-ttu-id="c3bd1-371">Path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-371">Path</span></span> |<span data-ttu-id="c3bd1-372">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-372">string</span></span> |
| <span data-ttu-id="c3bd1-373">LastModified</span><span class="sxs-lookup"><span data-stu-id="c3bd1-373">LastModified</span></span> |<span data-ttu-id="c3bd1-374">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-374">string</span></span> |
| <span data-ttu-id="c3bd1-375">Size</span><span class="sxs-lookup"><span data-stu-id="c3bd1-375">Size</span></span> |<span data-ttu-id="c3bd1-376">integer</span><span class="sxs-lookup"><span data-stu-id="c3bd1-376">integer</span></span> |
| <span data-ttu-id="c3bd1-377">MediaType</span><span class="sxs-lookup"><span data-stu-id="c3bd1-377">MediaType</span></span> |<span data-ttu-id="c3bd1-378">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-378">string</span></span> |
| <span data-ttu-id="c3bd1-379">IsFolder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-379">IsFolder</span></span> |<span data-ttu-id="c3bd1-380">boolean</span><span class="sxs-lookup"><span data-stu-id="c3bd1-380">boolean</span></span> |
| <span data-ttu-id="c3bd1-381">ETag</span><span class="sxs-lookup"><span data-stu-id="c3bd1-381">ETag</span></span> |<span data-ttu-id="c3bd1-382">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-382">string</span></span> |
| <span data-ttu-id="c3bd1-383">FileLocator</span><span class="sxs-lookup"><span data-stu-id="c3bd1-383">FileLocator</span></span> |<span data-ttu-id="c3bd1-384">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-384">string</span></span> |

### <a name="when-a-file-is-created"></a><span data-ttu-id="c3bd1-385">When a file is created</span><span class="sxs-lookup"><span data-stu-id="c3bd1-385">When a file is created</span></span>
<span data-ttu-id="c3bd1-386">This operation triggers a flow when a new file is created in a folder.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-386">This operation triggers a flow when a new file is created in a folder.</span></span> 

| <span data-ttu-id="c3bd1-387">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-387">Property Name</span></span> | <span data-ttu-id="c3bd1-388">Display Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-388">Display Name</span></span> | <span data-ttu-id="c3bd1-389">Description</span><span class="sxs-lookup"><span data-stu-id="c3bd1-389">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3bd1-390">folderId\*</span><span class="sxs-lookup"><span data-stu-id="c3bd1-390">folderId\*</span></span> |<span data-ttu-id="c3bd1-391">Folder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-391">Folder</span></span> |<span data-ttu-id="c3bd1-392">Select a folder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-392">Select a folder</span></span> |

<span data-ttu-id="c3bd1-393">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="c3bd1-393">An \* indicates that a property is required</span></span>

### <a name="when-a-file-is-modified"></a><span data-ttu-id="c3bd1-394">When a file is modified</span><span class="sxs-lookup"><span data-stu-id="c3bd1-394">When a file is modified</span></span>
<span data-ttu-id="c3bd1-395">This operation triggers a flow when a file is modified in a folder.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-395">This operation triggers a flow when a file is modified in a folder.</span></span> 

| <span data-ttu-id="c3bd1-396">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-396">Property Name</span></span> | <span data-ttu-id="c3bd1-397">Display Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-397">Display Name</span></span> | <span data-ttu-id="c3bd1-398">Description</span><span class="sxs-lookup"><span data-stu-id="c3bd1-398">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3bd1-399">folderId\*</span><span class="sxs-lookup"><span data-stu-id="c3bd1-399">folderId\*</span></span> |<span data-ttu-id="c3bd1-400">Folder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-400">Folder</span></span> |<span data-ttu-id="c3bd1-401">Select a folder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-401">Select a folder</span></span> |

<span data-ttu-id="c3bd1-402">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="c3bd1-402">An \* indicates that a property is required</span></span>

### <a name="list-files-in-folder"></a><span data-ttu-id="c3bd1-403">List files in folder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-403">List files in folder</span></span>
<span data-ttu-id="c3bd1-404">This operation gets the list of files and subfolders in a folder.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-404">This operation gets the list of files and subfolders in a folder.</span></span> 

| <span data-ttu-id="c3bd1-405">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-405">Property Name</span></span> | <span data-ttu-id="c3bd1-406">Display Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-406">Display Name</span></span> | <span data-ttu-id="c3bd1-407">Description</span><span class="sxs-lookup"><span data-stu-id="c3bd1-407">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3bd1-408">id\*</span><span class="sxs-lookup"><span data-stu-id="c3bd1-408">id\*</span></span> |<span data-ttu-id="c3bd1-409">Folder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-409">Folder</span></span> |<span data-ttu-id="c3bd1-410">Select a folder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-410">Select a folder</span></span> |

<span data-ttu-id="c3bd1-411">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="c3bd1-411">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="c3bd1-412">Output Details</span><span class="sxs-lookup"><span data-stu-id="c3bd1-412">Output Details</span></span>
<span data-ttu-id="c3bd1-413">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="c3bd1-413">BlobMetadata</span></span>

| <span data-ttu-id="c3bd1-414">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-414">Property Name</span></span> | <span data-ttu-id="c3bd1-415">Data Type</span><span class="sxs-lookup"><span data-stu-id="c3bd1-415">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="c3bd1-416">Id</span><span class="sxs-lookup"><span data-stu-id="c3bd1-416">Id</span></span> |<span data-ttu-id="c3bd1-417">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-417">string</span></span> |
| <span data-ttu-id="c3bd1-418">Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-418">Name</span></span> |<span data-ttu-id="c3bd1-419">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-419">string</span></span> |
| <span data-ttu-id="c3bd1-420">DisplayName</span><span class="sxs-lookup"><span data-stu-id="c3bd1-420">DisplayName</span></span> |<span data-ttu-id="c3bd1-421">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-421">string</span></span> |
| <span data-ttu-id="c3bd1-422">Path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-422">Path</span></span> |<span data-ttu-id="c3bd1-423">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-423">string</span></span> |
| <span data-ttu-id="c3bd1-424">LastModified</span><span class="sxs-lookup"><span data-stu-id="c3bd1-424">LastModified</span></span> |<span data-ttu-id="c3bd1-425">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-425">string</span></span> |
| <span data-ttu-id="c3bd1-426">Size</span><span class="sxs-lookup"><span data-stu-id="c3bd1-426">Size</span></span> |<span data-ttu-id="c3bd1-427">integer</span><span class="sxs-lookup"><span data-stu-id="c3bd1-427">integer</span></span> |
| <span data-ttu-id="c3bd1-428">MediaType</span><span class="sxs-lookup"><span data-stu-id="c3bd1-428">MediaType</span></span> |<span data-ttu-id="c3bd1-429">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-429">string</span></span> |
| <span data-ttu-id="c3bd1-430">IsFolder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-430">IsFolder</span></span> |<span data-ttu-id="c3bd1-431">boolean</span><span class="sxs-lookup"><span data-stu-id="c3bd1-431">boolean</span></span> |
| <span data-ttu-id="c3bd1-432">ETag</span><span class="sxs-lookup"><span data-stu-id="c3bd1-432">ETag</span></span> |<span data-ttu-id="c3bd1-433">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-433">string</span></span> |
| <span data-ttu-id="c3bd1-434">FileLocator</span><span class="sxs-lookup"><span data-stu-id="c3bd1-434">FileLocator</span></span> |<span data-ttu-id="c3bd1-435">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-435">string</span></span> |

### <a name="list-files-in-root-folder"></a><span data-ttu-id="c3bd1-436">List files in root folder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-436">List files in root folder</span></span>
<span data-ttu-id="c3bd1-437">This operation gets the list of files and subfolders in the root folder.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-437">This operation gets the list of files and subfolders in the root folder.</span></span> 

<span data-ttu-id="c3bd1-438">There are no parameters for this call</span><span class="sxs-lookup"><span data-stu-id="c3bd1-438">There are no parameters for this call</span></span>

#### <a name="output-details"></a><span data-ttu-id="c3bd1-439">Output Details</span><span class="sxs-lookup"><span data-stu-id="c3bd1-439">Output Details</span></span>
<span data-ttu-id="c3bd1-440">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="c3bd1-440">BlobMetadata</span></span>

| <span data-ttu-id="c3bd1-441">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-441">Property Name</span></span> | <span data-ttu-id="c3bd1-442">Data Type</span><span class="sxs-lookup"><span data-stu-id="c3bd1-442">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="c3bd1-443">Id</span><span class="sxs-lookup"><span data-stu-id="c3bd1-443">Id</span></span> |<span data-ttu-id="c3bd1-444">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-444">string</span></span> |
| <span data-ttu-id="c3bd1-445">Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-445">Name</span></span> |<span data-ttu-id="c3bd1-446">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-446">string</span></span> |
| <span data-ttu-id="c3bd1-447">DisplayName</span><span class="sxs-lookup"><span data-stu-id="c3bd1-447">DisplayName</span></span> |<span data-ttu-id="c3bd1-448">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-448">string</span></span> |
| <span data-ttu-id="c3bd1-449">Path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-449">Path</span></span> |<span data-ttu-id="c3bd1-450">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-450">string</span></span> |
| <span data-ttu-id="c3bd1-451">LastModified</span><span class="sxs-lookup"><span data-stu-id="c3bd1-451">LastModified</span></span> |<span data-ttu-id="c3bd1-452">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-452">string</span></span> |
| <span data-ttu-id="c3bd1-453">Size</span><span class="sxs-lookup"><span data-stu-id="c3bd1-453">Size</span></span> |<span data-ttu-id="c3bd1-454">integer</span><span class="sxs-lookup"><span data-stu-id="c3bd1-454">integer</span></span> |
| <span data-ttu-id="c3bd1-455">MediaType</span><span class="sxs-lookup"><span data-stu-id="c3bd1-455">MediaType</span></span> |<span data-ttu-id="c3bd1-456">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-456">string</span></span> |
| <span data-ttu-id="c3bd1-457">IsFolder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-457">IsFolder</span></span> |<span data-ttu-id="c3bd1-458">boolean</span><span class="sxs-lookup"><span data-stu-id="c3bd1-458">boolean</span></span> |
| <span data-ttu-id="c3bd1-459">ETag</span><span class="sxs-lookup"><span data-stu-id="c3bd1-459">ETag</span></span> |<span data-ttu-id="c3bd1-460">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-460">string</span></span> |
| <span data-ttu-id="c3bd1-461">FileLocator</span><span class="sxs-lookup"><span data-stu-id="c3bd1-461">FileLocator</span></span> |<span data-ttu-id="c3bd1-462">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-462">string</span></span> |

### <a name="extract-archive-to-folder"></a><span data-ttu-id="c3bd1-463">Extract archive to folder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-463">Extract archive to folder</span></span>
<span data-ttu-id="c3bd1-464">This operation extracts an archive file into a folder (example: .zip).</span><span class="sxs-lookup"><span data-stu-id="c3bd1-464">This operation extracts an archive file into a folder (example: .zip).</span></span> 

| <span data-ttu-id="c3bd1-465">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-465">Property Name</span></span> | <span data-ttu-id="c3bd1-466">Display Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-466">Display Name</span></span> | <span data-ttu-id="c3bd1-467">Description</span><span class="sxs-lookup"><span data-stu-id="c3bd1-467">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3bd1-468">source\*</span><span class="sxs-lookup"><span data-stu-id="c3bd1-468">source\*</span></span> |<span data-ttu-id="c3bd1-469">Source archive file path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-469">Source archive file path</span></span> |<span data-ttu-id="c3bd1-470">Path to the archive file</span><span class="sxs-lookup"><span data-stu-id="c3bd1-470">Path to the archive file</span></span> |
| <span data-ttu-id="c3bd1-471">destination\*</span><span class="sxs-lookup"><span data-stu-id="c3bd1-471">destination\*</span></span> |<span data-ttu-id="c3bd1-472">Destination folder path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-472">Destination folder path</span></span> |<span data-ttu-id="c3bd1-473">Path to extract the archive contents</span><span class="sxs-lookup"><span data-stu-id="c3bd1-473">Path to extract the archive contents</span></span> |
| <span data-ttu-id="c3bd1-474">overwrite</span><span class="sxs-lookup"><span data-stu-id="c3bd1-474">overwrite</span></span> |<span data-ttu-id="c3bd1-475">Overwrite?</span><span class="sxs-lookup"><span data-stu-id="c3bd1-475">Overwrite?</span></span> |<span data-ttu-id="c3bd1-476">Overwrites the destination files if set to 'true'</span><span class="sxs-lookup"><span data-stu-id="c3bd1-476">Overwrites the destination files if set to 'true'</span></span> |

<span data-ttu-id="c3bd1-477">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="c3bd1-477">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="c3bd1-478">Output Details</span><span class="sxs-lookup"><span data-stu-id="c3bd1-478">Output Details</span></span>
<span data-ttu-id="c3bd1-479">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="c3bd1-479">BlobMetadata</span></span>

| <span data-ttu-id="c3bd1-480">Property Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-480">Property Name</span></span> | <span data-ttu-id="c3bd1-481">Data Type</span><span class="sxs-lookup"><span data-stu-id="c3bd1-481">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="c3bd1-482">Id</span><span class="sxs-lookup"><span data-stu-id="c3bd1-482">Id</span></span> |<span data-ttu-id="c3bd1-483">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-483">string</span></span> |
| <span data-ttu-id="c3bd1-484">Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-484">Name</span></span> |<span data-ttu-id="c3bd1-485">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-485">string</span></span> |
| <span data-ttu-id="c3bd1-486">DisplayName</span><span class="sxs-lookup"><span data-stu-id="c3bd1-486">DisplayName</span></span> |<span data-ttu-id="c3bd1-487">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-487">string</span></span> |
| <span data-ttu-id="c3bd1-488">Path</span><span class="sxs-lookup"><span data-stu-id="c3bd1-488">Path</span></span> |<span data-ttu-id="c3bd1-489">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-489">string</span></span> |
| <span data-ttu-id="c3bd1-490">LastModified</span><span class="sxs-lookup"><span data-stu-id="c3bd1-490">LastModified</span></span> |<span data-ttu-id="c3bd1-491">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-491">string</span></span> |
| <span data-ttu-id="c3bd1-492">Size</span><span class="sxs-lookup"><span data-stu-id="c3bd1-492">Size</span></span> |<span data-ttu-id="c3bd1-493">integer</span><span class="sxs-lookup"><span data-stu-id="c3bd1-493">integer</span></span> |
| <span data-ttu-id="c3bd1-494">MediaType</span><span class="sxs-lookup"><span data-stu-id="c3bd1-494">MediaType</span></span> |<span data-ttu-id="c3bd1-495">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-495">string</span></span> |
| <span data-ttu-id="c3bd1-496">IsFolder</span><span class="sxs-lookup"><span data-stu-id="c3bd1-496">IsFolder</span></span> |<span data-ttu-id="c3bd1-497">boolean</span><span class="sxs-lookup"><span data-stu-id="c3bd1-497">boolean</span></span> |
| <span data-ttu-id="c3bd1-498">ETag</span><span class="sxs-lookup"><span data-stu-id="c3bd1-498">ETag</span></span> |<span data-ttu-id="c3bd1-499">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-499">string</span></span> |
| <span data-ttu-id="c3bd1-500">FileLocator</span><span class="sxs-lookup"><span data-stu-id="c3bd1-500">FileLocator</span></span> |<span data-ttu-id="c3bd1-501">string</span><span class="sxs-lookup"><span data-stu-id="c3bd1-501">string</span></span> |

## <a name="http-responses"></a><span data-ttu-id="c3bd1-502">HTTP responses</span><span class="sxs-lookup"><span data-stu-id="c3bd1-502">HTTP responses</span></span>
<span data-ttu-id="c3bd1-503">The actions and triggers above can return one or more of the following HTTP status codes:</span><span class="sxs-lookup"><span data-stu-id="c3bd1-503">The actions and triggers above can return one or more of the following HTTP status codes:</span></span> 

| <span data-ttu-id="c3bd1-504">Name</span><span class="sxs-lookup"><span data-stu-id="c3bd1-504">Name</span></span> | <span data-ttu-id="c3bd1-505">Description</span><span class="sxs-lookup"><span data-stu-id="c3bd1-505">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c3bd1-506">200</span><span class="sxs-lookup"><span data-stu-id="c3bd1-506">200</span></span> |<span data-ttu-id="c3bd1-507">OK</span><span class="sxs-lookup"><span data-stu-id="c3bd1-507">OK</span></span> |
| <span data-ttu-id="c3bd1-508">202</span><span class="sxs-lookup"><span data-stu-id="c3bd1-508">202</span></span> |<span data-ttu-id="c3bd1-509">Accepted</span><span class="sxs-lookup"><span data-stu-id="c3bd1-509">Accepted</span></span> |
| <span data-ttu-id="c3bd1-510">400</span><span class="sxs-lookup"><span data-stu-id="c3bd1-510">400</span></span> |<span data-ttu-id="c3bd1-511">Bad Request</span><span class="sxs-lookup"><span data-stu-id="c3bd1-511">Bad Request</span></span> |
| <span data-ttu-id="c3bd1-512">401</span><span class="sxs-lookup"><span data-stu-id="c3bd1-512">401</span></span> |<span data-ttu-id="c3bd1-513">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="c3bd1-513">Unauthorized</span></span> |
| <span data-ttu-id="c3bd1-514">403</span><span class="sxs-lookup"><span data-stu-id="c3bd1-514">403</span></span> |<span data-ttu-id="c3bd1-515">Forbidden</span><span class="sxs-lookup"><span data-stu-id="c3bd1-515">Forbidden</span></span> |
| <span data-ttu-id="c3bd1-516">404</span><span class="sxs-lookup"><span data-stu-id="c3bd1-516">404</span></span> |<span data-ttu-id="c3bd1-517">Not Found</span><span class="sxs-lookup"><span data-stu-id="c3bd1-517">Not Found</span></span> |
| <span data-ttu-id="c3bd1-518">500</span><span class="sxs-lookup"><span data-stu-id="c3bd1-518">500</span></span> |<span data-ttu-id="c3bd1-519">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-519">Internal Server Error.</span></span> <span data-ttu-id="c3bd1-520">Unknown error occurred.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-520">Unknown error occurred.</span></span> |
| <span data-ttu-id="c3bd1-521">default</span><span class="sxs-lookup"><span data-stu-id="c3bd1-521">default</span></span> |<span data-ttu-id="c3bd1-522">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="c3bd1-522">Operation Failed.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c3bd1-523">Next steps</span><span class="sxs-lookup"><span data-stu-id="c3bd1-523">Next steps</span></span>
[<span data-ttu-id="c3bd1-524">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="c3bd1-524">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)







