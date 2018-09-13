---
title: Add the OneDrive connector in your Logic Apps | Microsoft Docs
description: Overview of the OneDrive connector with REST API parameters
services: logic-apps
documentationcenter: ''
author: MandiOhlinger
manager: anneta
editor: ''
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia
ms.openlocfilehash: c5f6d11a298f2a698fd3c5c035dfcf7f07fdf318
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552111"
---
# <a name="get-started-with-the-onedrive-connector"></a><span data-ttu-id="0f0d8-103">Get started with the OneDrive connector</span><span class="sxs-lookup"><span data-stu-id="0f0d8-103">Get started with the OneDrive connector</span></span>
<span data-ttu-id="0f0d8-104">Connect to OneDrive to manage your files, including upload, get, delete files, and more.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-104">Connect to OneDrive to manage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="0f0d8-105">With OneDrive, you:</span><span class="sxs-lookup"><span data-stu-id="0f0d8-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="0f0d8-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="0f0d8-107">Use triggers to start your workflow when a file is created or updated within your OneDrive.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-107">Use triggers to start your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="0f0d8-108">Use actions to create a file, delete a file, and more.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-108">Use actions to create a file, delete a file, and more.</span></span> <span data-ttu-id="0f0d8-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span><span class="sxs-lookup"><span data-stu-id="0f0d8-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="0f0d8-110">This topic shows you how to use the OneDrive connector in a logic app, and also lists the triggers and actions.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-110">This topic shows you how to use the OneDrive connector in a logic app, and also lists the triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="0f0d8-111">This version of the article applies to Logic Apps general availability (GA).</span><span class="sxs-lookup"><span data-stu-id="0f0d8-111">This version of the article applies to Logic Apps general availability (GA).</span></span> 
> 
> 

<span data-ttu-id="0f0d8-112">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0f0d8-112">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-onedrive"></a><span data-ttu-id="0f0d8-113">Connect to OneDrive</span><span class="sxs-lookup"><span data-stu-id="0f0d8-113">Connect to OneDrive</span></span>
<span data-ttu-id="0f0d8-114">Before your logic app can access any service, you first create a *connection* to the service.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-114">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="0f0d8-115">A connection provides connectivity between a logic app and another service.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-115">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="0f0d8-116">For example, to connect to OneDrive, you first need a OneDrive *connection*.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-116">For example, to connect to OneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="0f0d8-117">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-117">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="0f0d8-118">So, with OneDrive, enter the credentials to your OneDrive account  to create the connection.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-118">So, with OneDrive, enter the credentials to your OneDrive account  to create the connection.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="0f0d8-119">Create the connection</span><span class="sxs-lookup"><span data-stu-id="0f0d8-119">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to OneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="0f0d8-120">Use a trigger</span><span class="sxs-lookup"><span data-stu-id="0f0d8-120">Use a trigger</span></span>
<span data-ttu-id="0f0d8-121">A trigger is an event that can be used to start the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-121">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="0f0d8-122">Triggers "poll" the service at an interval and frequency that you want.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-122">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="0f0d8-123">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="0f0d8-123">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="0f0d8-124">In the logic app, type "onedrive" to get a list of the triggers:</span><span class="sxs-lookup"><span data-stu-id="0f0d8-124">In the logic app, type "onedrive" to get a list of the triggers:</span></span>  
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="0f0d8-125">Select **When a file is modified**.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-125">Select **When a file is modified**.</span></span> <span data-ttu-id="0f0d8-126">If a connection already exists, then select the Show Picker button to select a folder.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-126">If a connection already exists, then select the Show Picker button to select a folder.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="0f0d8-127">If you are prompted to sign in, then enter the sign in details to create the connection.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-127">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="0f0d8-128">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists the steps.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-128">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0f0d8-129">In this example, the logic app runs when a file in the folder you choose is updated.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-129">In this example, the logic app runs when a file in the folder you choose is updated.</span></span> <span data-ttu-id="0f0d8-130">To see the results of this trigger, add another action that sends you an email.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-130">To see the results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="0f0d8-131">For example, add the Office 365 Outlook *Send an email* action that emails you when a file is updated.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-131">For example, add the Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 
   > 
   > 
3. <span data-ttu-id="0f0d8-132">Select the **Edit** button and set the **Frequency** and **Interval** values.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-132">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="0f0d8-133">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-133">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="0f0d8-134">**Save** your changes (top left corner of the toolbar).</span><span class="sxs-lookup"><span data-stu-id="0f0d8-134">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="0f0d8-135">Your logic app is saved and may be automatically enabled.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-135">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="0f0d8-136">Use an action</span><span class="sxs-lookup"><span data-stu-id="0f0d8-136">Use an action</span></span>
<span data-ttu-id="0f0d8-137">An action is an operation carried out by the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-137">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="0f0d8-138">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="0f0d8-138">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="0f0d8-139">Select the plus sign.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-139">Select the plus sign.</span></span> <span data-ttu-id="0f0d8-140">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-140">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="0f0d8-141">Choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-141">Choose **Add an action**.</span></span>
3. <span data-ttu-id="0f0d8-142">In the text box, type “onedrive” to get a list of all the available actions.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-142">In the text box, type “onedrive” to get a list of all the available actions.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="0f0d8-143">In our example, choose **OneDrive - Create file**.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-143">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="0f0d8-144">If a connection already exists, then select the **Folder Path** to put the file, enter the **File Name**, and choose the **File Content** you want:</span><span class="sxs-lookup"><span data-stu-id="0f0d8-144">If a connection already exists, then select the **Folder Path** to put the file, enter the **File Name**, and choose the **File Content** you want:</span></span>  
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="0f0d8-145">If you are prompted for the connection information, then enter the details to create the connection.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-145">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="0f0d8-146">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-146">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0f0d8-147">In this example, we create a new file in a OneDrive folder.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-147">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="0f0d8-148">You can use output from another trigger to create the OneDrive file.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-148">You can use output from another trigger to create the OneDrive file.</span></span> <span data-ttu-id="0f0d8-149">For example, add the Office 365 Outlook *When a new email arrives* trigger.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-149">For example, add the Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="0f0d8-150">Then add the OneDrive *Create file* action that uses the Attachments and Content-Type fields within a ForEach to create the new file in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-150">Then add the OneDrive *Create file* action that uses the Attachments and Content-Type fields within a ForEach to create the new file in OneDrive.</span></span> 
   > 
   > ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-onedrive/foreach-action.png)
   > 
   > 
5. <span data-ttu-id="0f0d8-151">**Save** your changes (top left corner of the toolbar).</span><span class="sxs-lookup"><span data-stu-id="0f0d8-151">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="0f0d8-152">Your logic app is saved and may be automatically enabled.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-152">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="technical-details"></a><span data-ttu-id="0f0d8-153">Technical Details</span><span class="sxs-lookup"><span data-stu-id="0f0d8-153">Technical Details</span></span>
## <a name="triggers"></a><span data-ttu-id="0f0d8-154">Triggers</span><span class="sxs-lookup"><span data-stu-id="0f0d8-154">Triggers</span></span>
| <span data-ttu-id="0f0d8-155">Trigger</span><span class="sxs-lookup"><span data-stu-id="0f0d8-155">Trigger</span></span> | <span data-ttu-id="0f0d8-156">Description</span><span class="sxs-lookup"><span data-stu-id="0f0d8-156">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="0f0d8-157">When a file is created</span><span class="sxs-lookup"><span data-stu-id="0f0d8-157">When a file is created</span></span>](connectors-create-api-onedrive.md#when-a-file-is-created) |<span data-ttu-id="0f0d8-158">This operation triggers a flow when a new file is created in a folder.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-158">This operation triggers a flow when a new file is created in a folder.</span></span> |
| [<span data-ttu-id="0f0d8-159">When a file is modified</span><span class="sxs-lookup"><span data-stu-id="0f0d8-159">When a file is modified</span></span>](connectors-create-api-onedrive.md#when-a-file-is-modified) |<span data-ttu-id="0f0d8-160">This operation triggers a flow when a file is modified in a folder.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-160">This operation triggers a flow when a file is modified in a folder.</span></span> |

## <a name="actions"></a><span data-ttu-id="0f0d8-161">Actions</span><span class="sxs-lookup"><span data-stu-id="0f0d8-161">Actions</span></span>
| <span data-ttu-id="0f0d8-162">Action</span><span class="sxs-lookup"><span data-stu-id="0f0d8-162">Action</span></span> | <span data-ttu-id="0f0d8-163">Description</span><span class="sxs-lookup"><span data-stu-id="0f0d8-163">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="0f0d8-164">Get file metadata</span><span class="sxs-lookup"><span data-stu-id="0f0d8-164">Get file metadata</span></span>](connectors-create-api-onedrive.md#get-file-metadata) |<span data-ttu-id="0f0d8-165">This operation gets the metadata for a file.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-165">This operation gets the metadata for a file.</span></span> |
| [<span data-ttu-id="0f0d8-166">Update file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-166">Update file</span></span>](connectors-create-api-onedrive.md#update-file) |<span data-ttu-id="0f0d8-167">This operation updates a file.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-167">This operation updates a file.</span></span> |
| [<span data-ttu-id="0f0d8-168">Delete file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-168">Delete file</span></span>](connectors-create-api-onedrive.md#delete-file) |<span data-ttu-id="0f0d8-169">This operation deletes a file.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-169">This operation deletes a file.</span></span> |
| [<span data-ttu-id="0f0d8-170">Get file metadata using path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-170">Get file metadata using path</span></span>](connectors-create-api-onedrive.md#get-file-metadata-using-path) |<span data-ttu-id="0f0d8-171">This operation gets the metadata of a file using the path.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-171">This operation gets the metadata of a file using the path.</span></span> |
| [<span data-ttu-id="0f0d8-172">Get file content using path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-172">Get file content using path</span></span>](connectors-create-api-onedrive.md#get-file-content-using-path) |<span data-ttu-id="0f0d8-173">This operation gets the content of a file using the path.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-173">This operation gets the content of a file using the path.</span></span> |
| [<span data-ttu-id="0f0d8-174">Get file content</span><span class="sxs-lookup"><span data-stu-id="0f0d8-174">Get file content</span></span>](connectors-create-api-onedrive.md#get-file-content) |<span data-ttu-id="0f0d8-175">This operation gets the content of a file.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-175">This operation gets the content of a file.</span></span> |
| [<span data-ttu-id="0f0d8-176">Create file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-176">Create file</span></span>](connectors-create-api-onedrive.md#create-file) |<span data-ttu-id="0f0d8-177">This operation creates a file.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-177">This operation creates a file.</span></span> |
| [<span data-ttu-id="0f0d8-178">Copy file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-178">Copy file</span></span>](connectors-create-api-onedrive.md#copy-file) |<span data-ttu-id="0f0d8-179">This operation copies a file to OneDrive.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-179">This operation copies a file to OneDrive.</span></span> |
| [<span data-ttu-id="0f0d8-180">List files in folder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-180">List files in folder</span></span>](connectors-create-api-onedrive.md#list-files-in-folder) |<span data-ttu-id="0f0d8-181">This operation gets the list of files and subfolders in a folder.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-181">This operation gets the list of files and subfolders in a folder.</span></span> |
| [<span data-ttu-id="0f0d8-182">List files in root folder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-182">List files in root folder</span></span>](connectors-create-api-onedrive.md#list-files-in-root-folder) |<span data-ttu-id="0f0d8-183">This operation gets the list of files and subfolders in the root folder.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-183">This operation gets the list of files and subfolders in the root folder.</span></span> |
| [<span data-ttu-id="0f0d8-184">Extract archive to folder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-184">Extract archive to folder</span></span>](connectors-create-api-onedrive.md#extract-archive-to-folder) |<span data-ttu-id="0f0d8-185">This operation extracts an archive file into a folder (example: .zip).</span><span class="sxs-lookup"><span data-stu-id="0f0d8-185">This operation extracts an archive file into a folder (example: .zip).</span></span> |

### <a name="action-details"></a><span data-ttu-id="0f0d8-186">Action details</span><span class="sxs-lookup"><span data-stu-id="0f0d8-186">Action details</span></span>
<span data-ttu-id="0f0d8-187">In this section, see the specific details about each action, including any required or optional input properties, and any corresponding output associated with the connector.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-187">In this section, see the specific details about each action, including any required or optional input properties, and any corresponding output associated with the connector.</span></span>

#### <a name="get-file-metadata"></a><span data-ttu-id="0f0d8-188">Get file metadata</span><span class="sxs-lookup"><span data-stu-id="0f0d8-188">Get file metadata</span></span>
<span data-ttu-id="0f0d8-189">This operation gets the metadata for a file.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-189">This operation gets the metadata for a file.</span></span> 

| <span data-ttu-id="0f0d8-190">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-190">Property Name</span></span> | <span data-ttu-id="0f0d8-191">Display Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-191">Display Name</span></span> | <span data-ttu-id="0f0d8-192">Description</span><span class="sxs-lookup"><span data-stu-id="0f0d8-192">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f0d8-193">id\*</span><span class="sxs-lookup"><span data-stu-id="0f0d8-193">id\*</span></span> |<span data-ttu-id="0f0d8-194">File</span><span class="sxs-lookup"><span data-stu-id="0f0d8-194">File</span></span> |<span data-ttu-id="0f0d8-195">Select a file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-195">Select a file</span></span> |

<span data-ttu-id="0f0d8-196">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-196">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="0f0d8-197">Output Details</span><span class="sxs-lookup"><span data-stu-id="0f0d8-197">Output Details</span></span>
<span data-ttu-id="0f0d8-198">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="0f0d8-198">BlobMetadata</span></span>

| <span data-ttu-id="0f0d8-199">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-199">Property Name</span></span> | <span data-ttu-id="0f0d8-200">Data Type</span><span class="sxs-lookup"><span data-stu-id="0f0d8-200">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="0f0d8-201">Id</span><span class="sxs-lookup"><span data-stu-id="0f0d8-201">Id</span></span> |<span data-ttu-id="0f0d8-202">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-202">string</span></span> |
| <span data-ttu-id="0f0d8-203">Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-203">Name</span></span> |<span data-ttu-id="0f0d8-204">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-204">string</span></span> |
| <span data-ttu-id="0f0d8-205">DisplayName</span><span class="sxs-lookup"><span data-stu-id="0f0d8-205">DisplayName</span></span> |<span data-ttu-id="0f0d8-206">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-206">string</span></span> |
| <span data-ttu-id="0f0d8-207">Path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-207">Path</span></span> |<span data-ttu-id="0f0d8-208">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-208">string</span></span> |
| <span data-ttu-id="0f0d8-209">LastModified</span><span class="sxs-lookup"><span data-stu-id="0f0d8-209">LastModified</span></span> |<span data-ttu-id="0f0d8-210">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-210">string</span></span> |
| <span data-ttu-id="0f0d8-211">Size</span><span class="sxs-lookup"><span data-stu-id="0f0d8-211">Size</span></span> |<span data-ttu-id="0f0d8-212">integer</span><span class="sxs-lookup"><span data-stu-id="0f0d8-212">integer</span></span> |
| <span data-ttu-id="0f0d8-213">MediaType</span><span class="sxs-lookup"><span data-stu-id="0f0d8-213">MediaType</span></span> |<span data-ttu-id="0f0d8-214">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-214">string</span></span> |
| <span data-ttu-id="0f0d8-215">IsFolder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-215">IsFolder</span></span> |<span data-ttu-id="0f0d8-216">boolean</span><span class="sxs-lookup"><span data-stu-id="0f0d8-216">boolean</span></span> |
| <span data-ttu-id="0f0d8-217">ETag</span><span class="sxs-lookup"><span data-stu-id="0f0d8-217">ETag</span></span> |<span data-ttu-id="0f0d8-218">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-218">string</span></span> |
| <span data-ttu-id="0f0d8-219">FileLocator</span><span class="sxs-lookup"><span data-stu-id="0f0d8-219">FileLocator</span></span> |<span data-ttu-id="0f0d8-220">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-220">string</span></span> |

#### <a name="update-file"></a><span data-ttu-id="0f0d8-221">Update file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-221">Update file</span></span>
<span data-ttu-id="0f0d8-222">This operation updates a file.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-222">This operation updates a file.</span></span> 

| <span data-ttu-id="0f0d8-223">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-223">Property Name</span></span> | <span data-ttu-id="0f0d8-224">Display Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-224">Display Name</span></span> | <span data-ttu-id="0f0d8-225">Description</span><span class="sxs-lookup"><span data-stu-id="0f0d8-225">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f0d8-226">id\*</span><span class="sxs-lookup"><span data-stu-id="0f0d8-226">id\*</span></span> |<span data-ttu-id="0f0d8-227">File</span><span class="sxs-lookup"><span data-stu-id="0f0d8-227">File</span></span> |<span data-ttu-id="0f0d8-228">Select a file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-228">Select a file</span></span> |
| <span data-ttu-id="0f0d8-229">body\*</span><span class="sxs-lookup"><span data-stu-id="0f0d8-229">body\*</span></span> |<span data-ttu-id="0f0d8-230">File content</span><span class="sxs-lookup"><span data-stu-id="0f0d8-230">File content</span></span> |<span data-ttu-id="0f0d8-231">Content of the file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-231">Content of the file</span></span> |

<span data-ttu-id="0f0d8-232">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-232">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="0f0d8-233">Output Details</span><span class="sxs-lookup"><span data-stu-id="0f0d8-233">Output Details</span></span>
<span data-ttu-id="0f0d8-234">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="0f0d8-234">BlobMetadata</span></span>

| <span data-ttu-id="0f0d8-235">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-235">Property Name</span></span> | <span data-ttu-id="0f0d8-236">Data Type</span><span class="sxs-lookup"><span data-stu-id="0f0d8-236">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="0f0d8-237">Id</span><span class="sxs-lookup"><span data-stu-id="0f0d8-237">Id</span></span> |<span data-ttu-id="0f0d8-238">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-238">string</span></span> |
| <span data-ttu-id="0f0d8-239">Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-239">Name</span></span> |<span data-ttu-id="0f0d8-240">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-240">string</span></span> |
| <span data-ttu-id="0f0d8-241">DisplayName</span><span class="sxs-lookup"><span data-stu-id="0f0d8-241">DisplayName</span></span> |<span data-ttu-id="0f0d8-242">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-242">string</span></span> |
| <span data-ttu-id="0f0d8-243">Path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-243">Path</span></span> |<span data-ttu-id="0f0d8-244">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-244">string</span></span> |
| <span data-ttu-id="0f0d8-245">LastModified</span><span class="sxs-lookup"><span data-stu-id="0f0d8-245">LastModified</span></span> |<span data-ttu-id="0f0d8-246">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-246">string</span></span> |
| <span data-ttu-id="0f0d8-247">Size</span><span class="sxs-lookup"><span data-stu-id="0f0d8-247">Size</span></span> |<span data-ttu-id="0f0d8-248">integer</span><span class="sxs-lookup"><span data-stu-id="0f0d8-248">integer</span></span> |
| <span data-ttu-id="0f0d8-249">MediaType</span><span class="sxs-lookup"><span data-stu-id="0f0d8-249">MediaType</span></span> |<span data-ttu-id="0f0d8-250">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-250">string</span></span> |
| <span data-ttu-id="0f0d8-251">IsFolder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-251">IsFolder</span></span> |<span data-ttu-id="0f0d8-252">boolean</span><span class="sxs-lookup"><span data-stu-id="0f0d8-252">boolean</span></span> |
| <span data-ttu-id="0f0d8-253">ETag</span><span class="sxs-lookup"><span data-stu-id="0f0d8-253">ETag</span></span> |<span data-ttu-id="0f0d8-254">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-254">string</span></span> |
| <span data-ttu-id="0f0d8-255">FileLocator</span><span class="sxs-lookup"><span data-stu-id="0f0d8-255">FileLocator</span></span> |<span data-ttu-id="0f0d8-256">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-256">string</span></span> |

#### <a name="delete-file"></a><span data-ttu-id="0f0d8-257">Delete file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-257">Delete file</span></span>
<span data-ttu-id="0f0d8-258">This operation deletes a file.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-258">This operation deletes a file.</span></span> 

| <span data-ttu-id="0f0d8-259">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-259">Property Name</span></span> | <span data-ttu-id="0f0d8-260">Display Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-260">Display Name</span></span> | <span data-ttu-id="0f0d8-261">Description</span><span class="sxs-lookup"><span data-stu-id="0f0d8-261">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f0d8-262">id\*</span><span class="sxs-lookup"><span data-stu-id="0f0d8-262">id\*</span></span> |<span data-ttu-id="0f0d8-263">File</span><span class="sxs-lookup"><span data-stu-id="0f0d8-263">File</span></span> |<span data-ttu-id="0f0d8-264">Select a file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-264">Select a file</span></span> |

<span data-ttu-id="0f0d8-265">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-265">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="0f0d8-266">Output Details</span><span class="sxs-lookup"><span data-stu-id="0f0d8-266">Output Details</span></span>
<span data-ttu-id="0f0d8-267">None.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-267">None.</span></span>

#### <a name="get-file-metadata-using-path"></a><span data-ttu-id="0f0d8-268">Get file metadata using path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-268">Get file metadata using path</span></span>
<span data-ttu-id="0f0d8-269">This operation gets the metadata of a file using the path.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-269">This operation gets the metadata of a file using the path.</span></span> 

| <span data-ttu-id="0f0d8-270">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-270">Property Name</span></span> | <span data-ttu-id="0f0d8-271">Display Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-271">Display Name</span></span> | <span data-ttu-id="0f0d8-272">Description</span><span class="sxs-lookup"><span data-stu-id="0f0d8-272">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f0d8-273">path\*</span><span class="sxs-lookup"><span data-stu-id="0f0d8-273">path\*</span></span> |<span data-ttu-id="0f0d8-274">File path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-274">File path</span></span> |<span data-ttu-id="0f0d8-275">Select a file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-275">Select a file</span></span> |

<span data-ttu-id="0f0d8-276">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-276">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="0f0d8-277">Output Details</span><span class="sxs-lookup"><span data-stu-id="0f0d8-277">Output Details</span></span>
<span data-ttu-id="0f0d8-278">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="0f0d8-278">BlobMetadata</span></span>

| <span data-ttu-id="0f0d8-279">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-279">Property Name</span></span> | <span data-ttu-id="0f0d8-280">Data Type</span><span class="sxs-lookup"><span data-stu-id="0f0d8-280">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="0f0d8-281">Id</span><span class="sxs-lookup"><span data-stu-id="0f0d8-281">Id</span></span> |<span data-ttu-id="0f0d8-282">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-282">string</span></span> |
| <span data-ttu-id="0f0d8-283">Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-283">Name</span></span> |<span data-ttu-id="0f0d8-284">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-284">string</span></span> |
| <span data-ttu-id="0f0d8-285">DisplayName</span><span class="sxs-lookup"><span data-stu-id="0f0d8-285">DisplayName</span></span> |<span data-ttu-id="0f0d8-286">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-286">string</span></span> |
| <span data-ttu-id="0f0d8-287">Path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-287">Path</span></span> |<span data-ttu-id="0f0d8-288">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-288">string</span></span> |
| <span data-ttu-id="0f0d8-289">LastModified</span><span class="sxs-lookup"><span data-stu-id="0f0d8-289">LastModified</span></span> |<span data-ttu-id="0f0d8-290">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-290">string</span></span> |
| <span data-ttu-id="0f0d8-291">Size</span><span class="sxs-lookup"><span data-stu-id="0f0d8-291">Size</span></span> |<span data-ttu-id="0f0d8-292">integer</span><span class="sxs-lookup"><span data-stu-id="0f0d8-292">integer</span></span> |
| <span data-ttu-id="0f0d8-293">MediaType</span><span class="sxs-lookup"><span data-stu-id="0f0d8-293">MediaType</span></span> |<span data-ttu-id="0f0d8-294">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-294">string</span></span> |
| <span data-ttu-id="0f0d8-295">IsFolder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-295">IsFolder</span></span> |<span data-ttu-id="0f0d8-296">boolean</span><span class="sxs-lookup"><span data-stu-id="0f0d8-296">boolean</span></span> |
| <span data-ttu-id="0f0d8-297">ETag</span><span class="sxs-lookup"><span data-stu-id="0f0d8-297">ETag</span></span> |<span data-ttu-id="0f0d8-298">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-298">string</span></span> |
| <span data-ttu-id="0f0d8-299">FileLocator</span><span class="sxs-lookup"><span data-stu-id="0f0d8-299">FileLocator</span></span> |<span data-ttu-id="0f0d8-300">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-300">string</span></span> |

#### <a name="get-file-content-using-path"></a><span data-ttu-id="0f0d8-301">Get file content using path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-301">Get file content using path</span></span>
<span data-ttu-id="0f0d8-302">This operation gets the content of a file using the path.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-302">This operation gets the content of a file using the path.</span></span> 

| <span data-ttu-id="0f0d8-303">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-303">Property Name</span></span> | <span data-ttu-id="0f0d8-304">Display Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-304">Display Name</span></span> | <span data-ttu-id="0f0d8-305">Description</span><span class="sxs-lookup"><span data-stu-id="0f0d8-305">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f0d8-306">path\*</span><span class="sxs-lookup"><span data-stu-id="0f0d8-306">path\*</span></span> |<span data-ttu-id="0f0d8-307">File path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-307">File path</span></span> |<span data-ttu-id="0f0d8-308">Select a file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-308">Select a file</span></span> |

<span data-ttu-id="0f0d8-309">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-309">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="0f0d8-310">Output Details</span><span class="sxs-lookup"><span data-stu-id="0f0d8-310">Output Details</span></span>
<span data-ttu-id="0f0d8-311">None.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-311">None.</span></span>

#### <a name="get-file-content"></a><span data-ttu-id="0f0d8-312">Get file content</span><span class="sxs-lookup"><span data-stu-id="0f0d8-312">Get file content</span></span>
<span data-ttu-id="0f0d8-313">This operation gets the content of a file.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-313">This operation gets the content of a file.</span></span> 

| <span data-ttu-id="0f0d8-314">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-314">Property Name</span></span> | <span data-ttu-id="0f0d8-315">Display Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-315">Display Name</span></span> | <span data-ttu-id="0f0d8-316">Description</span><span class="sxs-lookup"><span data-stu-id="0f0d8-316">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f0d8-317">id\*</span><span class="sxs-lookup"><span data-stu-id="0f0d8-317">id\*</span></span> |<span data-ttu-id="0f0d8-318">File</span><span class="sxs-lookup"><span data-stu-id="0f0d8-318">File</span></span> |<span data-ttu-id="0f0d8-319">Select a file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-319">Select a file</span></span> |

<span data-ttu-id="0f0d8-320">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-320">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="0f0d8-321">Output Details</span><span class="sxs-lookup"><span data-stu-id="0f0d8-321">Output Details</span></span>
<span data-ttu-id="0f0d8-322">None.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-322">None.</span></span>

#### <a name="create-file"></a><span data-ttu-id="0f0d8-323">Create file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-323">Create file</span></span>
<span data-ttu-id="0f0d8-324">This operation creates a file.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-324">This operation creates a file.</span></span> 

| <span data-ttu-id="0f0d8-325">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-325">Property Name</span></span> | <span data-ttu-id="0f0d8-326">Display Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-326">Display Name</span></span> | <span data-ttu-id="0f0d8-327">Description</span><span class="sxs-lookup"><span data-stu-id="0f0d8-327">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f0d8-328">folderPath\*</span><span class="sxs-lookup"><span data-stu-id="0f0d8-328">folderPath\*</span></span> |<span data-ttu-id="0f0d8-329">Folder path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-329">Folder path</span></span> |<span data-ttu-id="0f0d8-330">Select a folder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-330">Select a folder</span></span> |
| <span data-ttu-id="0f0d8-331">name\*</span><span class="sxs-lookup"><span data-stu-id="0f0d8-331">name\*</span></span> |<span data-ttu-id="0f0d8-332">File name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-332">File name</span></span> |<span data-ttu-id="0f0d8-333">Name of the file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-333">Name of the file</span></span> |
| <span data-ttu-id="0f0d8-334">body\*</span><span class="sxs-lookup"><span data-stu-id="0f0d8-334">body\*</span></span> |<span data-ttu-id="0f0d8-335">File content</span><span class="sxs-lookup"><span data-stu-id="0f0d8-335">File content</span></span> |<span data-ttu-id="0f0d8-336">Content of the file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-336">Content of the file</span></span> |

<span data-ttu-id="0f0d8-337">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-337">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="0f0d8-338">Output Details</span><span class="sxs-lookup"><span data-stu-id="0f0d8-338">Output Details</span></span>
<span data-ttu-id="0f0d8-339">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="0f0d8-339">BlobMetadata</span></span>

| <span data-ttu-id="0f0d8-340">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-340">Property Name</span></span> | <span data-ttu-id="0f0d8-341">Data Type</span><span class="sxs-lookup"><span data-stu-id="0f0d8-341">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="0f0d8-342">Id</span><span class="sxs-lookup"><span data-stu-id="0f0d8-342">Id</span></span> |<span data-ttu-id="0f0d8-343">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-343">string</span></span> |
| <span data-ttu-id="0f0d8-344">Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-344">Name</span></span> |<span data-ttu-id="0f0d8-345">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-345">string</span></span> |
| <span data-ttu-id="0f0d8-346">DisplayName</span><span class="sxs-lookup"><span data-stu-id="0f0d8-346">DisplayName</span></span> |<span data-ttu-id="0f0d8-347">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-347">string</span></span> |
| <span data-ttu-id="0f0d8-348">Path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-348">Path</span></span> |<span data-ttu-id="0f0d8-349">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-349">string</span></span> |
| <span data-ttu-id="0f0d8-350">LastModified</span><span class="sxs-lookup"><span data-stu-id="0f0d8-350">LastModified</span></span> |<span data-ttu-id="0f0d8-351">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-351">string</span></span> |
| <span data-ttu-id="0f0d8-352">Size</span><span class="sxs-lookup"><span data-stu-id="0f0d8-352">Size</span></span> |<span data-ttu-id="0f0d8-353">integer</span><span class="sxs-lookup"><span data-stu-id="0f0d8-353">integer</span></span> |
| <span data-ttu-id="0f0d8-354">MediaType</span><span class="sxs-lookup"><span data-stu-id="0f0d8-354">MediaType</span></span> |<span data-ttu-id="0f0d8-355">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-355">string</span></span> |
| <span data-ttu-id="0f0d8-356">IsFolder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-356">IsFolder</span></span> |<span data-ttu-id="0f0d8-357">boolean</span><span class="sxs-lookup"><span data-stu-id="0f0d8-357">boolean</span></span> |
| <span data-ttu-id="0f0d8-358">ETag</span><span class="sxs-lookup"><span data-stu-id="0f0d8-358">ETag</span></span> |<span data-ttu-id="0f0d8-359">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-359">string</span></span> |
| <span data-ttu-id="0f0d8-360">FileLocator</span><span class="sxs-lookup"><span data-stu-id="0f0d8-360">FileLocator</span></span> |<span data-ttu-id="0f0d8-361">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-361">string</span></span> |

#### <a name="copy-file"></a><span data-ttu-id="0f0d8-362">Copy file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-362">Copy file</span></span>
<span data-ttu-id="0f0d8-363">This operation copies a file to OneDrive.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-363">This operation copies a file to OneDrive.</span></span> 

| <span data-ttu-id="0f0d8-364">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-364">Property Name</span></span> | <span data-ttu-id="0f0d8-365">Display Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-365">Display Name</span></span> | <span data-ttu-id="0f0d8-366">Description</span><span class="sxs-lookup"><span data-stu-id="0f0d8-366">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f0d8-367">source\*</span><span class="sxs-lookup"><span data-stu-id="0f0d8-367">source\*</span></span> |<span data-ttu-id="0f0d8-368">Source url</span><span class="sxs-lookup"><span data-stu-id="0f0d8-368">Source url</span></span> |<span data-ttu-id="0f0d8-369">Url to source file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-369">Url to source file</span></span> |
| <span data-ttu-id="0f0d8-370">destination\*</span><span class="sxs-lookup"><span data-stu-id="0f0d8-370">destination\*</span></span> |<span data-ttu-id="0f0d8-371">Destination file path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-371">Destination file path</span></span> |<span data-ttu-id="0f0d8-372">Destination file path, including target filename</span><span class="sxs-lookup"><span data-stu-id="0f0d8-372">Destination file path, including target filename</span></span> |
| <span data-ttu-id="0f0d8-373">overwrite</span><span class="sxs-lookup"><span data-stu-id="0f0d8-373">overwrite</span></span> |<span data-ttu-id="0f0d8-374">Overwrite?</span><span class="sxs-lookup"><span data-stu-id="0f0d8-374">Overwrite?</span></span> |<span data-ttu-id="0f0d8-375">Overwrites the destination file if set to 'true'</span><span class="sxs-lookup"><span data-stu-id="0f0d8-375">Overwrites the destination file if set to 'true'</span></span> |

<span data-ttu-id="0f0d8-376">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-376">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="0f0d8-377">Output Details</span><span class="sxs-lookup"><span data-stu-id="0f0d8-377">Output Details</span></span>
<span data-ttu-id="0f0d8-378">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="0f0d8-378">BlobMetadata</span></span>

| <span data-ttu-id="0f0d8-379">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-379">Property Name</span></span> | <span data-ttu-id="0f0d8-380">Data Type</span><span class="sxs-lookup"><span data-stu-id="0f0d8-380">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="0f0d8-381">Id</span><span class="sxs-lookup"><span data-stu-id="0f0d8-381">Id</span></span> |<span data-ttu-id="0f0d8-382">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-382">string</span></span> |
| <span data-ttu-id="0f0d8-383">Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-383">Name</span></span> |<span data-ttu-id="0f0d8-384">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-384">string</span></span> |
| <span data-ttu-id="0f0d8-385">DisplayName</span><span class="sxs-lookup"><span data-stu-id="0f0d8-385">DisplayName</span></span> |<span data-ttu-id="0f0d8-386">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-386">string</span></span> |
| <span data-ttu-id="0f0d8-387">Path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-387">Path</span></span> |<span data-ttu-id="0f0d8-388">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-388">string</span></span> |
| <span data-ttu-id="0f0d8-389">LastModified</span><span class="sxs-lookup"><span data-stu-id="0f0d8-389">LastModified</span></span> |<span data-ttu-id="0f0d8-390">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-390">string</span></span> |
| <span data-ttu-id="0f0d8-391">Size</span><span class="sxs-lookup"><span data-stu-id="0f0d8-391">Size</span></span> |<span data-ttu-id="0f0d8-392">integer</span><span class="sxs-lookup"><span data-stu-id="0f0d8-392">integer</span></span> |
| <span data-ttu-id="0f0d8-393">MediaType</span><span class="sxs-lookup"><span data-stu-id="0f0d8-393">MediaType</span></span> |<span data-ttu-id="0f0d8-394">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-394">string</span></span> |
| <span data-ttu-id="0f0d8-395">IsFolder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-395">IsFolder</span></span> |<span data-ttu-id="0f0d8-396">boolean</span><span class="sxs-lookup"><span data-stu-id="0f0d8-396">boolean</span></span> |
| <span data-ttu-id="0f0d8-397">ETag</span><span class="sxs-lookup"><span data-stu-id="0f0d8-397">ETag</span></span> |<span data-ttu-id="0f0d8-398">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-398">string</span></span> |
| <span data-ttu-id="0f0d8-399">FileLocator</span><span class="sxs-lookup"><span data-stu-id="0f0d8-399">FileLocator</span></span> |<span data-ttu-id="0f0d8-400">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-400">string</span></span> |

#### <a name="when-a-file-is-created"></a><span data-ttu-id="0f0d8-401">When a file is created</span><span class="sxs-lookup"><span data-stu-id="0f0d8-401">When a file is created</span></span>
<span data-ttu-id="0f0d8-402">This operation triggers a flow when a new file is created in a folder.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-402">This operation triggers a flow when a new file is created in a folder.</span></span> 

| <span data-ttu-id="0f0d8-403">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-403">Property Name</span></span> | <span data-ttu-id="0f0d8-404">Display Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-404">Display Name</span></span> | <span data-ttu-id="0f0d8-405">Description</span><span class="sxs-lookup"><span data-stu-id="0f0d8-405">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f0d8-406">folderId\*</span><span class="sxs-lookup"><span data-stu-id="0f0d8-406">folderId\*</span></span> |<span data-ttu-id="0f0d8-407">Folder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-407">Folder</span></span> |<span data-ttu-id="0f0d8-408">Select a folder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-408">Select a folder</span></span> |

<span data-ttu-id="0f0d8-409">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-409">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="0f0d8-410">Output Details</span><span class="sxs-lookup"><span data-stu-id="0f0d8-410">Output Details</span></span>
<span data-ttu-id="0f0d8-411">None.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-411">None.</span></span>

#### <a name="when-a-file-is-modified"></a><span data-ttu-id="0f0d8-412">When a file is modified</span><span class="sxs-lookup"><span data-stu-id="0f0d8-412">When a file is modified</span></span>
<span data-ttu-id="0f0d8-413">This operation triggers a flow when a file is modified in a folder.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-413">This operation triggers a flow when a file is modified in a folder.</span></span> 

| <span data-ttu-id="0f0d8-414">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-414">Property Name</span></span> | <span data-ttu-id="0f0d8-415">Display Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-415">Display Name</span></span> | <span data-ttu-id="0f0d8-416">Description</span><span class="sxs-lookup"><span data-stu-id="0f0d8-416">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f0d8-417">folderId\*</span><span class="sxs-lookup"><span data-stu-id="0f0d8-417">folderId\*</span></span> |<span data-ttu-id="0f0d8-418">Folder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-418">Folder</span></span> |<span data-ttu-id="0f0d8-419">Select a folder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-419">Select a folder</span></span> |

<span data-ttu-id="0f0d8-420">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-420">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="0f0d8-421">Output Details</span><span class="sxs-lookup"><span data-stu-id="0f0d8-421">Output Details</span></span>
<span data-ttu-id="0f0d8-422">None.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-422">None.</span></span>

#### <a name="list-files-in-folder"></a><span data-ttu-id="0f0d8-423">List files in folder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-423">List files in folder</span></span>
<span data-ttu-id="0f0d8-424">This operation gets the list of files and subfolders in a folder.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-424">This operation gets the list of files and subfolders in a folder.</span></span>

| <span data-ttu-id="0f0d8-425">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-425">Property Name</span></span> | <span data-ttu-id="0f0d8-426">Display Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-426">Display Name</span></span> | <span data-ttu-id="0f0d8-427">Description</span><span class="sxs-lookup"><span data-stu-id="0f0d8-427">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f0d8-428">id\*</span><span class="sxs-lookup"><span data-stu-id="0f0d8-428">id\*</span></span> |<span data-ttu-id="0f0d8-429">Folder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-429">Folder</span></span> |<span data-ttu-id="0f0d8-430">Select a folder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-430">Select a folder</span></span> |

<span data-ttu-id="0f0d8-431">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-431">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="0f0d8-432">Output Details</span><span class="sxs-lookup"><span data-stu-id="0f0d8-432">Output Details</span></span>
<span data-ttu-id="0f0d8-433">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="0f0d8-433">BlobMetadata</span></span>

| <span data-ttu-id="0f0d8-434">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-434">Property Name</span></span> | <span data-ttu-id="0f0d8-435">Data Type</span><span class="sxs-lookup"><span data-stu-id="0f0d8-435">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="0f0d8-436">Id</span><span class="sxs-lookup"><span data-stu-id="0f0d8-436">Id</span></span> |<span data-ttu-id="0f0d8-437">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-437">string</span></span> |
| <span data-ttu-id="0f0d8-438">Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-438">Name</span></span> |<span data-ttu-id="0f0d8-439">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-439">string</span></span> |
| <span data-ttu-id="0f0d8-440">DisplayName</span><span class="sxs-lookup"><span data-stu-id="0f0d8-440">DisplayName</span></span> |<span data-ttu-id="0f0d8-441">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-441">string</span></span> |
| <span data-ttu-id="0f0d8-442">Path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-442">Path</span></span> |<span data-ttu-id="0f0d8-443">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-443">string</span></span> |
| <span data-ttu-id="0f0d8-444">LastModified</span><span class="sxs-lookup"><span data-stu-id="0f0d8-444">LastModified</span></span> |<span data-ttu-id="0f0d8-445">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-445">string</span></span> |
| <span data-ttu-id="0f0d8-446">Size</span><span class="sxs-lookup"><span data-stu-id="0f0d8-446">Size</span></span> |<span data-ttu-id="0f0d8-447">integer</span><span class="sxs-lookup"><span data-stu-id="0f0d8-447">integer</span></span> |
| <span data-ttu-id="0f0d8-448">MediaType</span><span class="sxs-lookup"><span data-stu-id="0f0d8-448">MediaType</span></span> |<span data-ttu-id="0f0d8-449">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-449">string</span></span> |
| <span data-ttu-id="0f0d8-450">IsFolder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-450">IsFolder</span></span> |<span data-ttu-id="0f0d8-451">boolean</span><span class="sxs-lookup"><span data-stu-id="0f0d8-451">boolean</span></span> |
| <span data-ttu-id="0f0d8-452">ETag</span><span class="sxs-lookup"><span data-stu-id="0f0d8-452">ETag</span></span> |<span data-ttu-id="0f0d8-453">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-453">string</span></span> |
| <span data-ttu-id="0f0d8-454">FileLocator</span><span class="sxs-lookup"><span data-stu-id="0f0d8-454">FileLocator</span></span> |<span data-ttu-id="0f0d8-455">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-455">string</span></span> |

#### <a name="list-files-in-root-folder"></a><span data-ttu-id="0f0d8-456">List files in root folder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-456">List files in root folder</span></span>
<span data-ttu-id="0f0d8-457">This operation gets the list of files and subfolders in the root folder.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-457">This operation gets the list of files and subfolders in the root folder.</span></span> 

<span data-ttu-id="0f0d8-458">There are no parameters for this call.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-458">There are no parameters for this call.</span></span>

##### <a name="output-details"></a><span data-ttu-id="0f0d8-459">Output Details</span><span class="sxs-lookup"><span data-stu-id="0f0d8-459">Output Details</span></span>
<span data-ttu-id="0f0d8-460">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="0f0d8-460">BlobMetadata</span></span>

| <span data-ttu-id="0f0d8-461">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-461">Property Name</span></span> | <span data-ttu-id="0f0d8-462">Data Type</span><span class="sxs-lookup"><span data-stu-id="0f0d8-462">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="0f0d8-463">Id</span><span class="sxs-lookup"><span data-stu-id="0f0d8-463">Id</span></span> |<span data-ttu-id="0f0d8-464">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-464">string</span></span> |
| <span data-ttu-id="0f0d8-465">Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-465">Name</span></span> |<span data-ttu-id="0f0d8-466">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-466">string</span></span> |
| <span data-ttu-id="0f0d8-467">DisplayName</span><span class="sxs-lookup"><span data-stu-id="0f0d8-467">DisplayName</span></span> |<span data-ttu-id="0f0d8-468">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-468">string</span></span> |
| <span data-ttu-id="0f0d8-469">Path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-469">Path</span></span> |<span data-ttu-id="0f0d8-470">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-470">string</span></span> |
| <span data-ttu-id="0f0d8-471">LastModified</span><span class="sxs-lookup"><span data-stu-id="0f0d8-471">LastModified</span></span> |<span data-ttu-id="0f0d8-472">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-472">string</span></span> |
| <span data-ttu-id="0f0d8-473">Size</span><span class="sxs-lookup"><span data-stu-id="0f0d8-473">Size</span></span> |<span data-ttu-id="0f0d8-474">integer</span><span class="sxs-lookup"><span data-stu-id="0f0d8-474">integer</span></span> |
| <span data-ttu-id="0f0d8-475">MediaType</span><span class="sxs-lookup"><span data-stu-id="0f0d8-475">MediaType</span></span> |<span data-ttu-id="0f0d8-476">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-476">string</span></span> |
| <span data-ttu-id="0f0d8-477">IsFolder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-477">IsFolder</span></span> |<span data-ttu-id="0f0d8-478">boolean</span><span class="sxs-lookup"><span data-stu-id="0f0d8-478">boolean</span></span> |
| <span data-ttu-id="0f0d8-479">ETag</span><span class="sxs-lookup"><span data-stu-id="0f0d8-479">ETag</span></span> |<span data-ttu-id="0f0d8-480">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-480">string</span></span> |
| <span data-ttu-id="0f0d8-481">FileLocator</span><span class="sxs-lookup"><span data-stu-id="0f0d8-481">FileLocator</span></span> |<span data-ttu-id="0f0d8-482">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-482">string</span></span> |

#### <a name="extract-archive-to-folder"></a><span data-ttu-id="0f0d8-483">Extract archive to folder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-483">Extract archive to folder</span></span>
<span data-ttu-id="0f0d8-484">This operation extracts an archive file into a folder (example: .zip).</span><span class="sxs-lookup"><span data-stu-id="0f0d8-484">This operation extracts an archive file into a folder (example: .zip).</span></span> 

| <span data-ttu-id="0f0d8-485">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-485">Property Name</span></span> | <span data-ttu-id="0f0d8-486">Display Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-486">Display Name</span></span> | <span data-ttu-id="0f0d8-487">Description</span><span class="sxs-lookup"><span data-stu-id="0f0d8-487">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f0d8-488">source\*</span><span class="sxs-lookup"><span data-stu-id="0f0d8-488">source\*</span></span> |<span data-ttu-id="0f0d8-489">Source archive file path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-489">Source archive file path</span></span> |<span data-ttu-id="0f0d8-490">Path to the archive file</span><span class="sxs-lookup"><span data-stu-id="0f0d8-490">Path to the archive file</span></span> |
| <span data-ttu-id="0f0d8-491">destination\*</span><span class="sxs-lookup"><span data-stu-id="0f0d8-491">destination\*</span></span> |<span data-ttu-id="0f0d8-492">Destination folder path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-492">Destination folder path</span></span> |<span data-ttu-id="0f0d8-493">Path to extract the archive contents</span><span class="sxs-lookup"><span data-stu-id="0f0d8-493">Path to extract the archive contents</span></span> |
| <span data-ttu-id="0f0d8-494">overwrite</span><span class="sxs-lookup"><span data-stu-id="0f0d8-494">overwrite</span></span> |<span data-ttu-id="0f0d8-495">Overwrite?</span><span class="sxs-lookup"><span data-stu-id="0f0d8-495">Overwrite?</span></span> |<span data-ttu-id="0f0d8-496">Overwrites the destination files if set to 'true'</span><span class="sxs-lookup"><span data-stu-id="0f0d8-496">Overwrites the destination files if set to 'true'</span></span> |

<span data-ttu-id="0f0d8-497">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-497">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="0f0d8-498">Output Details</span><span class="sxs-lookup"><span data-stu-id="0f0d8-498">Output Details</span></span>
<span data-ttu-id="0f0d8-499">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="0f0d8-499">BlobMetadata</span></span>

| <span data-ttu-id="0f0d8-500">Property Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-500">Property Name</span></span> | <span data-ttu-id="0f0d8-501">Data Type</span><span class="sxs-lookup"><span data-stu-id="0f0d8-501">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="0f0d8-502">Id</span><span class="sxs-lookup"><span data-stu-id="0f0d8-502">Id</span></span> |<span data-ttu-id="0f0d8-503">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-503">string</span></span> |
| <span data-ttu-id="0f0d8-504">Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-504">Name</span></span> |<span data-ttu-id="0f0d8-505">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-505">string</span></span> |
| <span data-ttu-id="0f0d8-506">DisplayName</span><span class="sxs-lookup"><span data-stu-id="0f0d8-506">DisplayName</span></span> |<span data-ttu-id="0f0d8-507">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-507">string</span></span> |
| <span data-ttu-id="0f0d8-508">Path</span><span class="sxs-lookup"><span data-stu-id="0f0d8-508">Path</span></span> |<span data-ttu-id="0f0d8-509">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-509">string</span></span> |
| <span data-ttu-id="0f0d8-510">LastModified</span><span class="sxs-lookup"><span data-stu-id="0f0d8-510">LastModified</span></span> |<span data-ttu-id="0f0d8-511">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-511">string</span></span> |
| <span data-ttu-id="0f0d8-512">Size</span><span class="sxs-lookup"><span data-stu-id="0f0d8-512">Size</span></span> |<span data-ttu-id="0f0d8-513">integer</span><span class="sxs-lookup"><span data-stu-id="0f0d8-513">integer</span></span> |
| <span data-ttu-id="0f0d8-514">MediaType</span><span class="sxs-lookup"><span data-stu-id="0f0d8-514">MediaType</span></span> |<span data-ttu-id="0f0d8-515">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-515">string</span></span> |
| <span data-ttu-id="0f0d8-516">IsFolder</span><span class="sxs-lookup"><span data-stu-id="0f0d8-516">IsFolder</span></span> |<span data-ttu-id="0f0d8-517">boolean</span><span class="sxs-lookup"><span data-stu-id="0f0d8-517">boolean</span></span> |
| <span data-ttu-id="0f0d8-518">ETag</span><span class="sxs-lookup"><span data-stu-id="0f0d8-518">ETag</span></span> |<span data-ttu-id="0f0d8-519">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-519">string</span></span> |
| <span data-ttu-id="0f0d8-520">FileLocator</span><span class="sxs-lookup"><span data-stu-id="0f0d8-520">FileLocator</span></span> |<span data-ttu-id="0f0d8-521">string</span><span class="sxs-lookup"><span data-stu-id="0f0d8-521">string</span></span> |

## <a name="http-responses"></a><span data-ttu-id="0f0d8-522">HTTP responses</span><span class="sxs-lookup"><span data-stu-id="0f0d8-522">HTTP responses</span></span>
<span data-ttu-id="0f0d8-523">The following table outlines the responses to the actions and triggers, and the response descriptions:</span><span class="sxs-lookup"><span data-stu-id="0f0d8-523">The following table outlines the responses to the actions and triggers, and the response descriptions:</span></span>  

| <span data-ttu-id="0f0d8-524">Name</span><span class="sxs-lookup"><span data-stu-id="0f0d8-524">Name</span></span> | <span data-ttu-id="0f0d8-525">Description</span><span class="sxs-lookup"><span data-stu-id="0f0d8-525">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0f0d8-526">200</span><span class="sxs-lookup"><span data-stu-id="0f0d8-526">200</span></span> |<span data-ttu-id="0f0d8-527">OK</span><span class="sxs-lookup"><span data-stu-id="0f0d8-527">OK</span></span> |
| <span data-ttu-id="0f0d8-528">202</span><span class="sxs-lookup"><span data-stu-id="0f0d8-528">202</span></span> |<span data-ttu-id="0f0d8-529">Accepted</span><span class="sxs-lookup"><span data-stu-id="0f0d8-529">Accepted</span></span> |
| <span data-ttu-id="0f0d8-530">400</span><span class="sxs-lookup"><span data-stu-id="0f0d8-530">400</span></span> |<span data-ttu-id="0f0d8-531">Bad Request</span><span class="sxs-lookup"><span data-stu-id="0f0d8-531">Bad Request</span></span> |
| <span data-ttu-id="0f0d8-532">401</span><span class="sxs-lookup"><span data-stu-id="0f0d8-532">401</span></span> |<span data-ttu-id="0f0d8-533">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="0f0d8-533">Unauthorized</span></span> |
| <span data-ttu-id="0f0d8-534">403</span><span class="sxs-lookup"><span data-stu-id="0f0d8-534">403</span></span> |<span data-ttu-id="0f0d8-535">Forbidden</span><span class="sxs-lookup"><span data-stu-id="0f0d8-535">Forbidden</span></span> |
| <span data-ttu-id="0f0d8-536">404</span><span class="sxs-lookup"><span data-stu-id="0f0d8-536">404</span></span> |<span data-ttu-id="0f0d8-537">Not Found</span><span class="sxs-lookup"><span data-stu-id="0f0d8-537">Not Found</span></span> |
| <span data-ttu-id="0f0d8-538">500</span><span class="sxs-lookup"><span data-stu-id="0f0d8-538">500</span></span> |<span data-ttu-id="0f0d8-539">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-539">Internal Server Error.</span></span> <span data-ttu-id="0f0d8-540">Unknown error occurred</span><span class="sxs-lookup"><span data-stu-id="0f0d8-540">Unknown error occurred</span></span> |
| <span data-ttu-id="0f0d8-541">default</span><span class="sxs-lookup"><span data-stu-id="0f0d8-541">default</span></span> |<span data-ttu-id="0f0d8-542">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="0f0d8-542">Operation Failed.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0f0d8-543">Next Steps</span><span class="sxs-lookup"><span data-stu-id="0f0d8-543">Next Steps</span></span>
<span data-ttu-id="0f0d8-544">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0f0d8-544">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="0f0d8-545">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="0f0d8-545">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>








