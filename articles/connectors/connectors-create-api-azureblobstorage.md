---
title: Add the Azure blob storage Connector in your Logic Apps | Microsoft Docs
description: Overview of Azure blob storage Connector with REST API parameters
services: ''
documentationcenter: ''
author: MandiOhlinger
manager: anneta
editor: ''
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia
ms.openlocfilehash: 905cdb6580e5f4e4954e3858851ead73f1e689be
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551778"
---
# <a name="get-started-with-the-azure-blob-storage-connector"></a><span data-ttu-id="ada7c-103">Get started with the Azure blob storage connector</span><span class="sxs-lookup"><span data-stu-id="ada7c-103">Get started with the Azure blob storage connector</span></span>
<span data-ttu-id="ada7c-104">Azure Blob storage is a service for storing large amounts of unstructured data.</span><span class="sxs-lookup"><span data-stu-id="ada7c-104">Azure Blob storage is a service for storing large amounts of unstructured data.</span></span> <span data-ttu-id="ada7c-105">Perform various actions such as upload, update, get, and delete blobs in Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="ada7c-105">Perform various actions such as upload, update, get, and delete blobs in Azure blob storage.</span></span> 

<span data-ttu-id="ada7c-106">With Azure blob storage, you:</span><span class="sxs-lookup"><span data-stu-id="ada7c-106">With Azure blob storage, you:</span></span>

* <span data-ttu-id="ada7c-107">Build your workflow by uploading new projects, or getting files that have been  recently updated.</span><span class="sxs-lookup"><span data-stu-id="ada7c-107">Build your workflow by uploading new projects, or getting files that have been  recently updated.</span></span>
* <span data-ttu-id="ada7c-108">Use actions to get file metadata, delete a file, copy files, and more.</span><span class="sxs-lookup"><span data-stu-id="ada7c-108">Use actions to get file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="ada7c-109">For example,  when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span><span class="sxs-lookup"><span data-stu-id="ada7c-109">For example,  when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="ada7c-110">This topic shows you how to use the blob storage connector in a logic app, and also lists the actions.</span><span class="sxs-lookup"><span data-stu-id="ada7c-110">This topic shows you how to use the blob storage connector in a logic app, and also lists the actions.</span></span>

> [!NOTE]
> <span data-ttu-id="ada7c-111">This version of the article applies to Logic Apps general availability (GA).</span><span class="sxs-lookup"><span data-stu-id="ada7c-111">This version of the article applies to Logic Apps general availability (GA).</span></span> 
> 
> 

<span data-ttu-id="ada7c-112">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ada7c-112">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-blob-storage"></a><span data-ttu-id="ada7c-113">Connect to Azure blob storage</span><span class="sxs-lookup"><span data-stu-id="ada7c-113">Connect to Azure blob storage</span></span>
<span data-ttu-id="ada7c-114">Before your logic app can access any service, you first create a *connection* to the service.</span><span class="sxs-lookup"><span data-stu-id="ada7c-114">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="ada7c-115">A connection provides connectivity between a logic app and another service.</span><span class="sxs-lookup"><span data-stu-id="ada7c-115">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="ada7c-116">For example, to connect to a storage account, you first create a blob storage *connection*.</span><span class="sxs-lookup"><span data-stu-id="ada7c-116">For example, to connect to a storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="ada7c-117">To create a connection, enter the credentials you normally use to access the service you are connecting to.</span><span class="sxs-lookup"><span data-stu-id="ada7c-117">To create a connection, enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="ada7c-118">So with Azure storage, enter the credentials to your storage account to create the connection.</span><span class="sxs-lookup"><span data-stu-id="ada7c-118">So with Azure storage, enter the credentials to your storage account to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="ada7c-119">Create the connection</span><span class="sxs-lookup"><span data-stu-id="ada7c-119">Create the connection</span></span>
> [!INCLUDE [Create a connection to Azure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="ada7c-120">Use a trigger</span><span class="sxs-lookup"><span data-stu-id="ada7c-120">Use a trigger</span></span>
<span data-ttu-id="ada7c-121">This connector does not have any triggers.</span><span class="sxs-lookup"><span data-stu-id="ada7c-121">This connector does not have any triggers.</span></span> <span data-ttu-id="ada7c-122">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span><span class="sxs-lookup"><span data-stu-id="ada7c-122">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="ada7c-123">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span><span class="sxs-lookup"><span data-stu-id="ada7c-123">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="ada7c-124">Use an action</span><span class="sxs-lookup"><span data-stu-id="ada7c-124">Use an action</span></span>
<span data-ttu-id="ada7c-125">An action is an operation carried out by the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="ada7c-125">An action is an operation carried out by the workflow defined in a logic app.</span></span>

1. <span data-ttu-id="ada7c-126">Select the plus sign.</span><span class="sxs-lookup"><span data-stu-id="ada7c-126">Select the plus sign.</span></span> <span data-ttu-id="ada7c-127">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span><span class="sxs-lookup"><span data-stu-id="ada7c-127">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="ada7c-128">Choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="ada7c-128">Choose **Add an action**.</span></span>
3. <span data-ttu-id="ada7c-129">In the text box, type “blob” to get a list of all the available actions.</span><span class="sxs-lookup"><span data-stu-id="ada7c-129">In the text box, type “blob” to get a list of all the available actions.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="ada7c-130">In our example, choose **AzureBlob - Get file metadata using path**.</span><span class="sxs-lookup"><span data-stu-id="ada7c-130">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="ada7c-131">If a connection already exists, then select the **...** (Show Picker) button to select a file.</span><span class="sxs-lookup"><span data-stu-id="ada7c-131">If a connection already exists, then select the **...** (Show Picker) button to select a file.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="ada7c-132">If you are prompted for the connection information, then enter the details to create the connection.</span><span class="sxs-lookup"><span data-stu-id="ada7c-132">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="ada7c-133">[Create the connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span><span class="sxs-lookup"><span data-stu-id="ada7c-133">[Create the connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="ada7c-134">In this example, we get the metadata of a file.</span><span class="sxs-lookup"><span data-stu-id="ada7c-134">In this example, we get the metadata of a file.</span></span> <span data-ttu-id="ada7c-135">To see the metadata, add another action that creates a new file using another connector.</span><span class="sxs-lookup"><span data-stu-id="ada7c-135">To see the metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="ada7c-136">For example, add a OneDrive action that creates a new "test" file based on the metadata.</span><span class="sxs-lookup"><span data-stu-id="ada7c-136">For example, add a OneDrive action that creates a new "test" file based on the metadata.</span></span> 
   > 
   > 
5. <span data-ttu-id="ada7c-137">**Save** your changes (top left corner of the toolbar).</span><span class="sxs-lookup"><span data-stu-id="ada7c-137">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="ada7c-138">Your logic app is saved and may be automatically enabled.</span><span class="sxs-lookup"><span data-stu-id="ada7c-138">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="ada7c-139">[Storage Explorer](http://storageexplorer.com/) is a great tool to  manage multiple storage accounts.</span><span class="sxs-lookup"><span data-stu-id="ada7c-139">[Storage Explorer](http://storageexplorer.com/) is a great tool to  manage multiple storage accounts.</span></span>
> 
> 

## <a name="technical-details"></a><span data-ttu-id="ada7c-140">Technical Details</span><span class="sxs-lookup"><span data-stu-id="ada7c-140">Technical Details</span></span>
## <a name="storage-blob-actions"></a><span data-ttu-id="ada7c-141">Storage Blob actions</span><span class="sxs-lookup"><span data-stu-id="ada7c-141">Storage Blob actions</span></span>
| <span data-ttu-id="ada7c-142">Action</span><span class="sxs-lookup"><span data-stu-id="ada7c-142">Action</span></span> | <span data-ttu-id="ada7c-143">Description</span><span class="sxs-lookup"><span data-stu-id="ada7c-143">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="ada7c-144">Get file metadata</span><span class="sxs-lookup"><span data-stu-id="ada7c-144">Get file metadata</span></span>](connectors-create-api-azureblobstorage.md#get-file-metadata) |<span data-ttu-id="ada7c-145">This operation gets file metadata using file id.</span><span class="sxs-lookup"><span data-stu-id="ada7c-145">This operation gets file metadata using file id.</span></span> |
| [<span data-ttu-id="ada7c-146">Update file</span><span class="sxs-lookup"><span data-stu-id="ada7c-146">Update file</span></span>](connectors-create-api-azureblobstorage.md#update-file) |<span data-ttu-id="ada7c-147">This operation updates a file.</span><span class="sxs-lookup"><span data-stu-id="ada7c-147">This operation updates a file.</span></span> |
| [<span data-ttu-id="ada7c-148">Delete file</span><span class="sxs-lookup"><span data-stu-id="ada7c-148">Delete file</span></span>](connectors-create-api-azureblobstorage.md#delete-file) |<span data-ttu-id="ada7c-149">This operation deletes a file.</span><span class="sxs-lookup"><span data-stu-id="ada7c-149">This operation deletes a file.</span></span> |
| [<span data-ttu-id="ada7c-150">Get file metadata using path</span><span class="sxs-lookup"><span data-stu-id="ada7c-150">Get file metadata using path</span></span>](connectors-create-api-azureblobstorage.md#get-file-metadata-using-path) |<span data-ttu-id="ada7c-151">This operation gets file metadata using the path.</span><span class="sxs-lookup"><span data-stu-id="ada7c-151">This operation gets file metadata using the path.</span></span> |
| [<span data-ttu-id="ada7c-152">Get file content using path</span><span class="sxs-lookup"><span data-stu-id="ada7c-152">Get file content using path</span></span>](connectors-create-api-azureblobstorage.md#get-file-content-using-path) |<span data-ttu-id="ada7c-153">This operation gets file contents using the path.</span><span class="sxs-lookup"><span data-stu-id="ada7c-153">This operation gets file contents using the path.</span></span> |
| [<span data-ttu-id="ada7c-154">Get file content</span><span class="sxs-lookup"><span data-stu-id="ada7c-154">Get file content</span></span>](connectors-create-api-azureblobstorage.md#get-file-content) |<span data-ttu-id="ada7c-155">This operation gets file contents using id.</span><span class="sxs-lookup"><span data-stu-id="ada7c-155">This operation gets file contents using id.</span></span> |
| [<span data-ttu-id="ada7c-156">Create file</span><span class="sxs-lookup"><span data-stu-id="ada7c-156">Create file</span></span>](connectors-create-api-azureblobstorage.md#create-file) |<span data-ttu-id="ada7c-157">This operation uploads a file.</span><span class="sxs-lookup"><span data-stu-id="ada7c-157">This operation uploads a file.</span></span> |
| [<span data-ttu-id="ada7c-158">Copy file</span><span class="sxs-lookup"><span data-stu-id="ada7c-158">Copy file</span></span>](connectors-create-api-azureblobstorage.md#copy-file) |<span data-ttu-id="ada7c-159">This operation copies a file to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ada7c-159">This operation copies a file to Azure Blob Storage.</span></span> |
| [<span data-ttu-id="ada7c-160">Extract archive to folder</span><span class="sxs-lookup"><span data-stu-id="ada7c-160">Extract archive to folder</span></span>](connectors-create-api-azureblobstorage.md#extract-archive-to-folder) |<span data-ttu-id="ada7c-161">This operation extracts an archive file into a folder (example: .zip).</span><span class="sxs-lookup"><span data-stu-id="ada7c-161">This operation extracts an archive file into a folder (example: .zip).</span></span> |

### <a name="action-details"></a><span data-ttu-id="ada7c-162">Action details</span><span class="sxs-lookup"><span data-stu-id="ada7c-162">Action details</span></span>
<span data-ttu-id="ada7c-163">In this section, see the specific details about each action, including any required or optional input properties, and any corresponding output associated with the connector.</span><span class="sxs-lookup"><span data-stu-id="ada7c-163">In this section, see the specific details about each action, including any required or optional input properties, and any corresponding output associated with the connector.</span></span>

#### <a name="get-file-metadata"></a><span data-ttu-id="ada7c-164">Get file metadata</span><span class="sxs-lookup"><span data-stu-id="ada7c-164">Get file metadata</span></span>
<span data-ttu-id="ada7c-165">This operation gets file metadata using file id.</span><span class="sxs-lookup"><span data-stu-id="ada7c-165">This operation gets file metadata using file id.</span></span>  

| <span data-ttu-id="ada7c-166">Property Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-166">Property Name</span></span> | <span data-ttu-id="ada7c-167">Display Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-167">Display Name</span></span> | <span data-ttu-id="ada7c-168">Description</span><span class="sxs-lookup"><span data-stu-id="ada7c-168">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ada7c-169">id\*</span><span class="sxs-lookup"><span data-stu-id="ada7c-169">id\*</span></span> |<span data-ttu-id="ada7c-170">File</span><span class="sxs-lookup"><span data-stu-id="ada7c-170">File</span></span> |<span data-ttu-id="ada7c-171">Select a file</span><span class="sxs-lookup"><span data-stu-id="ada7c-171">Select a file</span></span> |

<span data-ttu-id="ada7c-172">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="ada7c-172">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="ada7c-173">Output Details</span><span class="sxs-lookup"><span data-stu-id="ada7c-173">Output Details</span></span>
<span data-ttu-id="ada7c-174">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="ada7c-174">BlobMetadata</span></span>

| <span data-ttu-id="ada7c-175">Property Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-175">Property Name</span></span> | <span data-ttu-id="ada7c-176">Data Type</span><span class="sxs-lookup"><span data-stu-id="ada7c-176">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="ada7c-177">Id</span><span class="sxs-lookup"><span data-stu-id="ada7c-177">Id</span></span> |<span data-ttu-id="ada7c-178">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-178">string</span></span> |
| <span data-ttu-id="ada7c-179">Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-179">Name</span></span> |<span data-ttu-id="ada7c-180">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-180">string</span></span> |
| <span data-ttu-id="ada7c-181">DisplayName</span><span class="sxs-lookup"><span data-stu-id="ada7c-181">DisplayName</span></span> |<span data-ttu-id="ada7c-182">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-182">string</span></span> |
| <span data-ttu-id="ada7c-183">Path</span><span class="sxs-lookup"><span data-stu-id="ada7c-183">Path</span></span> |<span data-ttu-id="ada7c-184">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-184">string</span></span> |
| <span data-ttu-id="ada7c-185">LastModified</span><span class="sxs-lookup"><span data-stu-id="ada7c-185">LastModified</span></span> |<span data-ttu-id="ada7c-186">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-186">string</span></span> |
| <span data-ttu-id="ada7c-187">Size</span><span class="sxs-lookup"><span data-stu-id="ada7c-187">Size</span></span> |<span data-ttu-id="ada7c-188">integer</span><span class="sxs-lookup"><span data-stu-id="ada7c-188">integer</span></span> |
| <span data-ttu-id="ada7c-189">MediaType</span><span class="sxs-lookup"><span data-stu-id="ada7c-189">MediaType</span></span> |<span data-ttu-id="ada7c-190">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-190">string</span></span> |
| <span data-ttu-id="ada7c-191">IsFolder</span><span class="sxs-lookup"><span data-stu-id="ada7c-191">IsFolder</span></span> |<span data-ttu-id="ada7c-192">boolean</span><span class="sxs-lookup"><span data-stu-id="ada7c-192">boolean</span></span> |
| <span data-ttu-id="ada7c-193">ETag</span><span class="sxs-lookup"><span data-stu-id="ada7c-193">ETag</span></span> |<span data-ttu-id="ada7c-194">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-194">string</span></span> |
| <span data-ttu-id="ada7c-195">FileLocator</span><span class="sxs-lookup"><span data-stu-id="ada7c-195">FileLocator</span></span> |<span data-ttu-id="ada7c-196">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-196">string</span></span> |

#### <a name="update-file"></a><span data-ttu-id="ada7c-197">Update file</span><span class="sxs-lookup"><span data-stu-id="ada7c-197">Update file</span></span>
<span data-ttu-id="ada7c-198">This operation updates a file.</span><span class="sxs-lookup"><span data-stu-id="ada7c-198">This operation updates a file.</span></span>  

| <span data-ttu-id="ada7c-199">Property Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-199">Property Name</span></span> | <span data-ttu-id="ada7c-200">Display Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-200">Display Name</span></span> | <span data-ttu-id="ada7c-201">Description</span><span class="sxs-lookup"><span data-stu-id="ada7c-201">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ada7c-202">id\*</span><span class="sxs-lookup"><span data-stu-id="ada7c-202">id\*</span></span> |<span data-ttu-id="ada7c-203">File</span><span class="sxs-lookup"><span data-stu-id="ada7c-203">File</span></span> |<span data-ttu-id="ada7c-204">Select a file</span><span class="sxs-lookup"><span data-stu-id="ada7c-204">Select a file</span></span> |
| <span data-ttu-id="ada7c-205">body\*</span><span class="sxs-lookup"><span data-stu-id="ada7c-205">body\*</span></span> |<span data-ttu-id="ada7c-206">File content</span><span class="sxs-lookup"><span data-stu-id="ada7c-206">File content</span></span> |<span data-ttu-id="ada7c-207">Content of the file to update</span><span class="sxs-lookup"><span data-stu-id="ada7c-207">Content of the file to update</span></span> |

<span data-ttu-id="ada7c-208">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="ada7c-208">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="ada7c-209">Output Details</span><span class="sxs-lookup"><span data-stu-id="ada7c-209">Output Details</span></span>
<span data-ttu-id="ada7c-210">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="ada7c-210">BlobMetadata</span></span>

| <span data-ttu-id="ada7c-211">Property Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-211">Property Name</span></span> | <span data-ttu-id="ada7c-212">Data Type</span><span class="sxs-lookup"><span data-stu-id="ada7c-212">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="ada7c-213">Id</span><span class="sxs-lookup"><span data-stu-id="ada7c-213">Id</span></span> |<span data-ttu-id="ada7c-214">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-214">string</span></span> |
| <span data-ttu-id="ada7c-215">Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-215">Name</span></span> |<span data-ttu-id="ada7c-216">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-216">string</span></span> |
| <span data-ttu-id="ada7c-217">DisplayName</span><span class="sxs-lookup"><span data-stu-id="ada7c-217">DisplayName</span></span> |<span data-ttu-id="ada7c-218">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-218">string</span></span> |
| <span data-ttu-id="ada7c-219">Path</span><span class="sxs-lookup"><span data-stu-id="ada7c-219">Path</span></span> |<span data-ttu-id="ada7c-220">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-220">string</span></span> |
| <span data-ttu-id="ada7c-221">LastModified</span><span class="sxs-lookup"><span data-stu-id="ada7c-221">LastModified</span></span> |<span data-ttu-id="ada7c-222">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-222">string</span></span> |
| <span data-ttu-id="ada7c-223">Size</span><span class="sxs-lookup"><span data-stu-id="ada7c-223">Size</span></span> |<span data-ttu-id="ada7c-224">integer</span><span class="sxs-lookup"><span data-stu-id="ada7c-224">integer</span></span> |
| <span data-ttu-id="ada7c-225">MediaType</span><span class="sxs-lookup"><span data-stu-id="ada7c-225">MediaType</span></span> |<span data-ttu-id="ada7c-226">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-226">string</span></span> |
| <span data-ttu-id="ada7c-227">IsFolder</span><span class="sxs-lookup"><span data-stu-id="ada7c-227">IsFolder</span></span> |<span data-ttu-id="ada7c-228">boolean</span><span class="sxs-lookup"><span data-stu-id="ada7c-228">boolean</span></span> |
| <span data-ttu-id="ada7c-229">ETag</span><span class="sxs-lookup"><span data-stu-id="ada7c-229">ETag</span></span> |<span data-ttu-id="ada7c-230">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-230">string</span></span> |
| <span data-ttu-id="ada7c-231">FileLocator</span><span class="sxs-lookup"><span data-stu-id="ada7c-231">FileLocator</span></span> |<span data-ttu-id="ada7c-232">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-232">string</span></span> |

#### <a name="delete-file"></a><span data-ttu-id="ada7c-233">Delete file</span><span class="sxs-lookup"><span data-stu-id="ada7c-233">Delete file</span></span>
<span data-ttu-id="ada7c-234">This operation deletes a file.</span><span class="sxs-lookup"><span data-stu-id="ada7c-234">This operation deletes a file.</span></span>  

| <span data-ttu-id="ada7c-235">Property Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-235">Property Name</span></span> | <span data-ttu-id="ada7c-236">Display Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-236">Display Name</span></span> | <span data-ttu-id="ada7c-237">Description</span><span class="sxs-lookup"><span data-stu-id="ada7c-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ada7c-238">id\*</span><span class="sxs-lookup"><span data-stu-id="ada7c-238">id\*</span></span> |<span data-ttu-id="ada7c-239">File</span><span class="sxs-lookup"><span data-stu-id="ada7c-239">File</span></span> |<span data-ttu-id="ada7c-240">Select a file</span><span class="sxs-lookup"><span data-stu-id="ada7c-240">Select a file</span></span> |

<span data-ttu-id="ada7c-241">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="ada7c-241">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="ada7c-242">Output Details</span><span class="sxs-lookup"><span data-stu-id="ada7c-242">Output Details</span></span>
<span data-ttu-id="ada7c-243">None.</span><span class="sxs-lookup"><span data-stu-id="ada7c-243">None.</span></span>

#### <a name="get-file-metadata-using-path"></a><span data-ttu-id="ada7c-244">Get file metadata using path</span><span class="sxs-lookup"><span data-stu-id="ada7c-244">Get file metadata using path</span></span>
<span data-ttu-id="ada7c-245">This operation gets file metadata using the path.</span><span class="sxs-lookup"><span data-stu-id="ada7c-245">This operation gets file metadata using the path.</span></span>  

| <span data-ttu-id="ada7c-246">Property Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-246">Property Name</span></span> | <span data-ttu-id="ada7c-247">Display Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-247">Display Name</span></span> | <span data-ttu-id="ada7c-248">Description</span><span class="sxs-lookup"><span data-stu-id="ada7c-248">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ada7c-249">path\*</span><span class="sxs-lookup"><span data-stu-id="ada7c-249">path\*</span></span> |<span data-ttu-id="ada7c-250">File path</span><span class="sxs-lookup"><span data-stu-id="ada7c-250">File path</span></span> |<span data-ttu-id="ada7c-251">Select a file</span><span class="sxs-lookup"><span data-stu-id="ada7c-251">Select a file</span></span> |

<span data-ttu-id="ada7c-252">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="ada7c-252">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="ada7c-253">Output Details</span><span class="sxs-lookup"><span data-stu-id="ada7c-253">Output Details</span></span>
<span data-ttu-id="ada7c-254">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="ada7c-254">BlobMetadata</span></span>

| <span data-ttu-id="ada7c-255">Property Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-255">Property Name</span></span> | <span data-ttu-id="ada7c-256">Data Type</span><span class="sxs-lookup"><span data-stu-id="ada7c-256">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="ada7c-257">Id</span><span class="sxs-lookup"><span data-stu-id="ada7c-257">Id</span></span> |<span data-ttu-id="ada7c-258">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-258">string</span></span> |
| <span data-ttu-id="ada7c-259">Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-259">Name</span></span> |<span data-ttu-id="ada7c-260">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-260">string</span></span> |
| <span data-ttu-id="ada7c-261">DisplayName</span><span class="sxs-lookup"><span data-stu-id="ada7c-261">DisplayName</span></span> |<span data-ttu-id="ada7c-262">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-262">string</span></span> |
| <span data-ttu-id="ada7c-263">Path</span><span class="sxs-lookup"><span data-stu-id="ada7c-263">Path</span></span> |<span data-ttu-id="ada7c-264">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-264">string</span></span> |
| <span data-ttu-id="ada7c-265">LastModified</span><span class="sxs-lookup"><span data-stu-id="ada7c-265">LastModified</span></span> |<span data-ttu-id="ada7c-266">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-266">string</span></span> |
| <span data-ttu-id="ada7c-267">Size</span><span class="sxs-lookup"><span data-stu-id="ada7c-267">Size</span></span> |<span data-ttu-id="ada7c-268">integer</span><span class="sxs-lookup"><span data-stu-id="ada7c-268">integer</span></span> |
| <span data-ttu-id="ada7c-269">MediaType</span><span class="sxs-lookup"><span data-stu-id="ada7c-269">MediaType</span></span> |<span data-ttu-id="ada7c-270">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-270">string</span></span> |
| <span data-ttu-id="ada7c-271">IsFolder</span><span class="sxs-lookup"><span data-stu-id="ada7c-271">IsFolder</span></span> |<span data-ttu-id="ada7c-272">boolean</span><span class="sxs-lookup"><span data-stu-id="ada7c-272">boolean</span></span> |
| <span data-ttu-id="ada7c-273">ETag</span><span class="sxs-lookup"><span data-stu-id="ada7c-273">ETag</span></span> |<span data-ttu-id="ada7c-274">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-274">string</span></span> |
| <span data-ttu-id="ada7c-275">FileLocator</span><span class="sxs-lookup"><span data-stu-id="ada7c-275">FileLocator</span></span> |<span data-ttu-id="ada7c-276">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-276">string</span></span> |

#### <a name="get-file-content-using-path"></a><span data-ttu-id="ada7c-277">Get file content using path</span><span class="sxs-lookup"><span data-stu-id="ada7c-277">Get file content using path</span></span>
<span data-ttu-id="ada7c-278">This operation gets file contents using the path.</span><span class="sxs-lookup"><span data-stu-id="ada7c-278">This operation gets file contents using the path.</span></span>  

| <span data-ttu-id="ada7c-279">Property Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-279">Property Name</span></span> | <span data-ttu-id="ada7c-280">Display Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-280">Display Name</span></span> | <span data-ttu-id="ada7c-281">Description</span><span class="sxs-lookup"><span data-stu-id="ada7c-281">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ada7c-282">path\*</span><span class="sxs-lookup"><span data-stu-id="ada7c-282">path\*</span></span> |<span data-ttu-id="ada7c-283">File path</span><span class="sxs-lookup"><span data-stu-id="ada7c-283">File path</span></span> |<span data-ttu-id="ada7c-284">Select a file</span><span class="sxs-lookup"><span data-stu-id="ada7c-284">Select a file</span></span> |

<span data-ttu-id="ada7c-285">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="ada7c-285">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="ada7c-286">Output Details</span><span class="sxs-lookup"><span data-stu-id="ada7c-286">Output Details</span></span>
<span data-ttu-id="ada7c-287">None.</span><span class="sxs-lookup"><span data-stu-id="ada7c-287">None.</span></span>

#### <a name="get-file-content"></a><span data-ttu-id="ada7c-288">Get file content</span><span class="sxs-lookup"><span data-stu-id="ada7c-288">Get file content</span></span>
<span data-ttu-id="ada7c-289">This operation gets file contents using id.</span><span class="sxs-lookup"><span data-stu-id="ada7c-289">This operation gets file contents using id.</span></span>  

| <span data-ttu-id="ada7c-290">Property Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-290">Property Name</span></span> | <span data-ttu-id="ada7c-291">Data Type</span><span class="sxs-lookup"><span data-stu-id="ada7c-291">Data Type</span></span> | <span data-ttu-id="ada7c-292">Description</span><span class="sxs-lookup"><span data-stu-id="ada7c-292">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ada7c-293">id\*</span><span class="sxs-lookup"><span data-stu-id="ada7c-293">id\*</span></span> |<span data-ttu-id="ada7c-294">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-294">string</span></span> |<span data-ttu-id="ada7c-295">Select a file</span><span class="sxs-lookup"><span data-stu-id="ada7c-295">Select a file</span></span> |

<span data-ttu-id="ada7c-296">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="ada7c-296">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="ada7c-297">Output Details</span><span class="sxs-lookup"><span data-stu-id="ada7c-297">Output Details</span></span>
<span data-ttu-id="ada7c-298">None.</span><span class="sxs-lookup"><span data-stu-id="ada7c-298">None.</span></span>

#### <a name="create-file"></a><span data-ttu-id="ada7c-299">Create file</span><span class="sxs-lookup"><span data-stu-id="ada7c-299">Create file</span></span>
<span data-ttu-id="ada7c-300">This operation uploads a file.</span><span class="sxs-lookup"><span data-stu-id="ada7c-300">This operation uploads a file.</span></span>  

| <span data-ttu-id="ada7c-301">Property Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-301">Property Name</span></span> | <span data-ttu-id="ada7c-302">Display Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-302">Display Name</span></span> | <span data-ttu-id="ada7c-303">Description</span><span class="sxs-lookup"><span data-stu-id="ada7c-303">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ada7c-304">folderPath\*</span><span class="sxs-lookup"><span data-stu-id="ada7c-304">folderPath\*</span></span> |<span data-ttu-id="ada7c-305">Folder path</span><span class="sxs-lookup"><span data-stu-id="ada7c-305">Folder path</span></span> |<span data-ttu-id="ada7c-306">Select a folder</span><span class="sxs-lookup"><span data-stu-id="ada7c-306">Select a folder</span></span> |
| <span data-ttu-id="ada7c-307">name\*</span><span class="sxs-lookup"><span data-stu-id="ada7c-307">name\*</span></span> |<span data-ttu-id="ada7c-308">File name</span><span class="sxs-lookup"><span data-stu-id="ada7c-308">File name</span></span> |<span data-ttu-id="ada7c-309">Name of file to upload</span><span class="sxs-lookup"><span data-stu-id="ada7c-309">Name of file to upload</span></span> |
| <span data-ttu-id="ada7c-310">body\*</span><span class="sxs-lookup"><span data-stu-id="ada7c-310">body\*</span></span> |<span data-ttu-id="ada7c-311">File content</span><span class="sxs-lookup"><span data-stu-id="ada7c-311">File content</span></span> |<span data-ttu-id="ada7c-312">Content of the file to upload</span><span class="sxs-lookup"><span data-stu-id="ada7c-312">Content of the file to upload</span></span> |

<span data-ttu-id="ada7c-313">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="ada7c-313">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="ada7c-314">Output Details</span><span class="sxs-lookup"><span data-stu-id="ada7c-314">Output Details</span></span>
<span data-ttu-id="ada7c-315">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="ada7c-315">BlobMetadata</span></span>

| <span data-ttu-id="ada7c-316">Property Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-316">Property Name</span></span> | <span data-ttu-id="ada7c-317">Data Type</span><span class="sxs-lookup"><span data-stu-id="ada7c-317">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="ada7c-318">Id</span><span class="sxs-lookup"><span data-stu-id="ada7c-318">Id</span></span> |<span data-ttu-id="ada7c-319">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-319">string</span></span> |
| <span data-ttu-id="ada7c-320">Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-320">Name</span></span> |<span data-ttu-id="ada7c-321">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-321">string</span></span> |
| <span data-ttu-id="ada7c-322">DisplayName</span><span class="sxs-lookup"><span data-stu-id="ada7c-322">DisplayName</span></span> |<span data-ttu-id="ada7c-323">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-323">string</span></span> |
| <span data-ttu-id="ada7c-324">Path</span><span class="sxs-lookup"><span data-stu-id="ada7c-324">Path</span></span> |<span data-ttu-id="ada7c-325">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-325">string</span></span> |
| <span data-ttu-id="ada7c-326">LastModified</span><span class="sxs-lookup"><span data-stu-id="ada7c-326">LastModified</span></span> |<span data-ttu-id="ada7c-327">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-327">string</span></span> |
| <span data-ttu-id="ada7c-328">Size</span><span class="sxs-lookup"><span data-stu-id="ada7c-328">Size</span></span> |<span data-ttu-id="ada7c-329">integer</span><span class="sxs-lookup"><span data-stu-id="ada7c-329">integer</span></span> |
| <span data-ttu-id="ada7c-330">MediaType</span><span class="sxs-lookup"><span data-stu-id="ada7c-330">MediaType</span></span> |<span data-ttu-id="ada7c-331">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-331">string</span></span> |
| <span data-ttu-id="ada7c-332">IsFolder</span><span class="sxs-lookup"><span data-stu-id="ada7c-332">IsFolder</span></span> |<span data-ttu-id="ada7c-333">boolean</span><span class="sxs-lookup"><span data-stu-id="ada7c-333">boolean</span></span> |
| <span data-ttu-id="ada7c-334">ETag</span><span class="sxs-lookup"><span data-stu-id="ada7c-334">ETag</span></span> |<span data-ttu-id="ada7c-335">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-335">string</span></span> |
| <span data-ttu-id="ada7c-336">FileLocator</span><span class="sxs-lookup"><span data-stu-id="ada7c-336">FileLocator</span></span> |<span data-ttu-id="ada7c-337">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-337">string</span></span> |

#### <a name="copy-file"></a><span data-ttu-id="ada7c-338">Copy file</span><span class="sxs-lookup"><span data-stu-id="ada7c-338">Copy file</span></span>
<span data-ttu-id="ada7c-339">This operation copies a file to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ada7c-339">This operation copies a file to Azure Blob Storage.</span></span>  

| <span data-ttu-id="ada7c-340">Property Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-340">Property Name</span></span> | <span data-ttu-id="ada7c-341">Display Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-341">Display Name</span></span> | <span data-ttu-id="ada7c-342">Description</span><span class="sxs-lookup"><span data-stu-id="ada7c-342">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ada7c-343">source\*</span><span class="sxs-lookup"><span data-stu-id="ada7c-343">source\*</span></span> |<span data-ttu-id="ada7c-344">Source url</span><span class="sxs-lookup"><span data-stu-id="ada7c-344">Source url</span></span> |<span data-ttu-id="ada7c-345">Specify Url to source file</span><span class="sxs-lookup"><span data-stu-id="ada7c-345">Specify Url to source file</span></span> |
| <span data-ttu-id="ada7c-346">destination\*</span><span class="sxs-lookup"><span data-stu-id="ada7c-346">destination\*</span></span> |<span data-ttu-id="ada7c-347">Destination file path</span><span class="sxs-lookup"><span data-stu-id="ada7c-347">Destination file path</span></span> |<span data-ttu-id="ada7c-348">Specify the destination file path, including target filename</span><span class="sxs-lookup"><span data-stu-id="ada7c-348">Specify the destination file path, including target filename</span></span> |
| <span data-ttu-id="ada7c-349">overwrite</span><span class="sxs-lookup"><span data-stu-id="ada7c-349">overwrite</span></span> |<span data-ttu-id="ada7c-350">Overwrite?</span><span class="sxs-lookup"><span data-stu-id="ada7c-350">Overwrite?</span></span> |<span data-ttu-id="ada7c-351">Should an existing destination file be overwritten (true/false)?</span><span class="sxs-lookup"><span data-stu-id="ada7c-351">Should an existing destination file be overwritten (true/false)?</span></span> |

<span data-ttu-id="ada7c-352">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="ada7c-352">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="ada7c-353">Output Details</span><span class="sxs-lookup"><span data-stu-id="ada7c-353">Output Details</span></span>
<span data-ttu-id="ada7c-354">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="ada7c-354">BlobMetadata</span></span>

| <span data-ttu-id="ada7c-355">Property Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-355">Property Name</span></span> | <span data-ttu-id="ada7c-356">Data Type</span><span class="sxs-lookup"><span data-stu-id="ada7c-356">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="ada7c-357">Id</span><span class="sxs-lookup"><span data-stu-id="ada7c-357">Id</span></span> |<span data-ttu-id="ada7c-358">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-358">string</span></span> |
| <span data-ttu-id="ada7c-359">Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-359">Name</span></span> |<span data-ttu-id="ada7c-360">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-360">string</span></span> |
| <span data-ttu-id="ada7c-361">DisplayName</span><span class="sxs-lookup"><span data-stu-id="ada7c-361">DisplayName</span></span> |<span data-ttu-id="ada7c-362">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-362">string</span></span> |
| <span data-ttu-id="ada7c-363">Path</span><span class="sxs-lookup"><span data-stu-id="ada7c-363">Path</span></span> |<span data-ttu-id="ada7c-364">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-364">string</span></span> |
| <span data-ttu-id="ada7c-365">LastModified</span><span class="sxs-lookup"><span data-stu-id="ada7c-365">LastModified</span></span> |<span data-ttu-id="ada7c-366">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-366">string</span></span> |
| <span data-ttu-id="ada7c-367">Size</span><span class="sxs-lookup"><span data-stu-id="ada7c-367">Size</span></span> |<span data-ttu-id="ada7c-368">integer</span><span class="sxs-lookup"><span data-stu-id="ada7c-368">integer</span></span> |
| <span data-ttu-id="ada7c-369">MediaType</span><span class="sxs-lookup"><span data-stu-id="ada7c-369">MediaType</span></span> |<span data-ttu-id="ada7c-370">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-370">string</span></span> |
| <span data-ttu-id="ada7c-371">IsFolder</span><span class="sxs-lookup"><span data-stu-id="ada7c-371">IsFolder</span></span> |<span data-ttu-id="ada7c-372">boolean</span><span class="sxs-lookup"><span data-stu-id="ada7c-372">boolean</span></span> |
| <span data-ttu-id="ada7c-373">ETag</span><span class="sxs-lookup"><span data-stu-id="ada7c-373">ETag</span></span> |<span data-ttu-id="ada7c-374">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-374">string</span></span> |
| <span data-ttu-id="ada7c-375">FileLocator</span><span class="sxs-lookup"><span data-stu-id="ada7c-375">FileLocator</span></span> |<span data-ttu-id="ada7c-376">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-376">string</span></span> |

#### <a name="extract-archive-to-folder"></a><span data-ttu-id="ada7c-377">Extract archive to folder</span><span class="sxs-lookup"><span data-stu-id="ada7c-377">Extract archive to folder</span></span>
<span data-ttu-id="ada7c-378">This operation extracts an archive file into a folder (example: .zip).</span><span class="sxs-lookup"><span data-stu-id="ada7c-378">This operation extracts an archive file into a folder (example: .zip).</span></span>  

| <span data-ttu-id="ada7c-379">Property Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-379">Property Name</span></span> | <span data-ttu-id="ada7c-380">Display Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-380">Display Name</span></span> | <span data-ttu-id="ada7c-381">Description</span><span class="sxs-lookup"><span data-stu-id="ada7c-381">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ada7c-382">source\*</span><span class="sxs-lookup"><span data-stu-id="ada7c-382">source\*</span></span> |<span data-ttu-id="ada7c-383">Source archive file path</span><span class="sxs-lookup"><span data-stu-id="ada7c-383">Source archive file path</span></span> |<span data-ttu-id="ada7c-384">Select an archive file</span><span class="sxs-lookup"><span data-stu-id="ada7c-384">Select an archive file</span></span> |
| <span data-ttu-id="ada7c-385">destination\*</span><span class="sxs-lookup"><span data-stu-id="ada7c-385">destination\*</span></span> |<span data-ttu-id="ada7c-386">Destination folder path</span><span class="sxs-lookup"><span data-stu-id="ada7c-386">Destination folder path</span></span> |<span data-ttu-id="ada7c-387">Select the contents to extract</span><span class="sxs-lookup"><span data-stu-id="ada7c-387">Select the contents to extract</span></span> |
| <span data-ttu-id="ada7c-388">overwrite</span><span class="sxs-lookup"><span data-stu-id="ada7c-388">overwrite</span></span> |<span data-ttu-id="ada7c-389">Overwrite?</span><span class="sxs-lookup"><span data-stu-id="ada7c-389">Overwrite?</span></span> |<span data-ttu-id="ada7c-390">Should an existing destination file be overwritten (true/false)?</span><span class="sxs-lookup"><span data-stu-id="ada7c-390">Should an existing destination file be overwritten (true/false)?</span></span> |

<span data-ttu-id="ada7c-391">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="ada7c-391">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="ada7c-392">Output Details</span><span class="sxs-lookup"><span data-stu-id="ada7c-392">Output Details</span></span>
<span data-ttu-id="ada7c-393">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="ada7c-393">BlobMetadata</span></span>

| <span data-ttu-id="ada7c-394">Property Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-394">Property Name</span></span> | <span data-ttu-id="ada7c-395">Data Type</span><span class="sxs-lookup"><span data-stu-id="ada7c-395">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="ada7c-396">Id</span><span class="sxs-lookup"><span data-stu-id="ada7c-396">Id</span></span> |<span data-ttu-id="ada7c-397">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-397">string</span></span> |
| <span data-ttu-id="ada7c-398">Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-398">Name</span></span> |<span data-ttu-id="ada7c-399">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-399">string</span></span> |
| <span data-ttu-id="ada7c-400">DisplayName</span><span class="sxs-lookup"><span data-stu-id="ada7c-400">DisplayName</span></span> |<span data-ttu-id="ada7c-401">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-401">string</span></span> |
| <span data-ttu-id="ada7c-402">Path</span><span class="sxs-lookup"><span data-stu-id="ada7c-402">Path</span></span> |<span data-ttu-id="ada7c-403">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-403">string</span></span> |
| <span data-ttu-id="ada7c-404">LastModified</span><span class="sxs-lookup"><span data-stu-id="ada7c-404">LastModified</span></span> |<span data-ttu-id="ada7c-405">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-405">string</span></span> |
| <span data-ttu-id="ada7c-406">Size</span><span class="sxs-lookup"><span data-stu-id="ada7c-406">Size</span></span> |<span data-ttu-id="ada7c-407">integer</span><span class="sxs-lookup"><span data-stu-id="ada7c-407">integer</span></span> |
| <span data-ttu-id="ada7c-408">MediaType</span><span class="sxs-lookup"><span data-stu-id="ada7c-408">MediaType</span></span> |<span data-ttu-id="ada7c-409">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-409">string</span></span> |
| <span data-ttu-id="ada7c-410">IsFolder</span><span class="sxs-lookup"><span data-stu-id="ada7c-410">IsFolder</span></span> |<span data-ttu-id="ada7c-411">boolean</span><span class="sxs-lookup"><span data-stu-id="ada7c-411">boolean</span></span> |
| <span data-ttu-id="ada7c-412">ETag</span><span class="sxs-lookup"><span data-stu-id="ada7c-412">ETag</span></span> |<span data-ttu-id="ada7c-413">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-413">string</span></span> |
| <span data-ttu-id="ada7c-414">FileLocator</span><span class="sxs-lookup"><span data-stu-id="ada7c-414">FileLocator</span></span> |<span data-ttu-id="ada7c-415">string</span><span class="sxs-lookup"><span data-stu-id="ada7c-415">string</span></span> |

## <a name="http-responses"></a><span data-ttu-id="ada7c-416">HTTP responses</span><span class="sxs-lookup"><span data-stu-id="ada7c-416">HTTP responses</span></span>
<span data-ttu-id="ada7c-417">When making calls to the different actions, you may get certain responses.</span><span class="sxs-lookup"><span data-stu-id="ada7c-417">When making calls to the different actions, you may get certain responses.</span></span> <span data-ttu-id="ada7c-418">The following table outlines the responses and their descriptions:</span><span class="sxs-lookup"><span data-stu-id="ada7c-418">The following table outlines the responses and their descriptions:</span></span>  

| <span data-ttu-id="ada7c-419">Name</span><span class="sxs-lookup"><span data-stu-id="ada7c-419">Name</span></span> | <span data-ttu-id="ada7c-420">Description</span><span class="sxs-lookup"><span data-stu-id="ada7c-420">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ada7c-421">200</span><span class="sxs-lookup"><span data-stu-id="ada7c-421">200</span></span> |<span data-ttu-id="ada7c-422">OK</span><span class="sxs-lookup"><span data-stu-id="ada7c-422">OK</span></span> |
| <span data-ttu-id="ada7c-423">202</span><span class="sxs-lookup"><span data-stu-id="ada7c-423">202</span></span> |<span data-ttu-id="ada7c-424">Accepted</span><span class="sxs-lookup"><span data-stu-id="ada7c-424">Accepted</span></span> |
| <span data-ttu-id="ada7c-425">400</span><span class="sxs-lookup"><span data-stu-id="ada7c-425">400</span></span> |<span data-ttu-id="ada7c-426">Bad Request</span><span class="sxs-lookup"><span data-stu-id="ada7c-426">Bad Request</span></span> |
| <span data-ttu-id="ada7c-427">401</span><span class="sxs-lookup"><span data-stu-id="ada7c-427">401</span></span> |<span data-ttu-id="ada7c-428">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="ada7c-428">Unauthorized</span></span> |
| <span data-ttu-id="ada7c-429">403</span><span class="sxs-lookup"><span data-stu-id="ada7c-429">403</span></span> |<span data-ttu-id="ada7c-430">Forbidden</span><span class="sxs-lookup"><span data-stu-id="ada7c-430">Forbidden</span></span> |
| <span data-ttu-id="ada7c-431">404</span><span class="sxs-lookup"><span data-stu-id="ada7c-431">404</span></span> |<span data-ttu-id="ada7c-432">Not Found</span><span class="sxs-lookup"><span data-stu-id="ada7c-432">Not Found</span></span> |
| <span data-ttu-id="ada7c-433">500</span><span class="sxs-lookup"><span data-stu-id="ada7c-433">500</span></span> |<span data-ttu-id="ada7c-434">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="ada7c-434">Internal Server Error.</span></span> <span data-ttu-id="ada7c-435">Unknown error occurred</span><span class="sxs-lookup"><span data-stu-id="ada7c-435">Unknown error occurred</span></span> |
| <span data-ttu-id="ada7c-436">default</span><span class="sxs-lookup"><span data-stu-id="ada7c-436">default</span></span> |<span data-ttu-id="ada7c-437">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="ada7c-437">Operation Failed.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ada7c-438">Next steps</span><span class="sxs-lookup"><span data-stu-id="ada7c-438">Next steps</span></span>
<span data-ttu-id="ada7c-439">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ada7c-439">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="ada7c-440">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="ada7c-440">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>




