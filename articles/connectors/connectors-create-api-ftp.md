---
title: Learn how to use the FTP connector in logic apps| Microsoft Docs
description: Create logic apps with Azure App service. Connect to FTP server to manage your files. You can perform various actions such as upload, update, get, and delete files in FTP server.
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: deonhe
ms.openlocfilehash: 030f473ed0be3764151c315b4ceacd213314e73c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563191"
---
# <a name="get-started-with-the-ftp-connector"></a><span data-ttu-id="b2ce6-105">Get started with the FTP connector</span><span class="sxs-lookup"><span data-stu-id="b2ce6-105">Get started with the FTP connector</span></span>
<span data-ttu-id="b2ce6-106">Use the FTP connector to monitor, manage and create files on an  FTP server.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-106">Use the FTP connector to monitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="b2ce6-107">To use [any connector](apis-list.md), you first need to create a logic app.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-107">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="b2ce6-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b2ce6-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-ftp"></a><span data-ttu-id="b2ce6-109">Connect to FTP</span><span class="sxs-lookup"><span data-stu-id="b2ce6-109">Connect to FTP</span></span>
<span data-ttu-id="b2ce6-110">Before your logic app can access any service, you first need to create a *connection* to the service.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-110">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="b2ce6-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-ftp"></a><span data-ttu-id="b2ce6-112">Create a connection to FTP</span><span class="sxs-lookup"><span data-stu-id="b2ce6-112">Create a connection to FTP</span></span>
> [!INCLUDE [Steps to create a connection to FTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="b2ce6-113">Use a FTP trigger</span><span class="sxs-lookup"><span data-stu-id="b2ce6-113">Use a FTP trigger</span></span>
<span data-ttu-id="b2ce6-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="b2ce6-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="b2ce6-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="b2ce6-116">The FTP connector requires an FTP server that  is accessible from the Internet and is configured to operate with PASSIVE mode.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-116">The FTP connector requires an FTP server that  is accessible from the Internet and is configured to operate with PASSIVE mode.</span></span> <span data-ttu-id="b2ce6-117">Also, the FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-117">Also, the FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="b2ce6-118">The FTP connector only supports explicit FTPS (FTP over SSL).</span><span class="sxs-lookup"><span data-stu-id="b2ce6-118">The FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="b2ce6-119">In this example, I will show you how to use the **FTP - When a file is added or modified** trigger to initiate a logic app workflow when a file is added to, or modified on, an FTP server.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-119">In this example, I will show you how to use the **FTP - When a file is added or modified** trigger to initiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="b2ce6-120">In an enterprise example, you could use this trigger to monitor an FTP folder for new files that represent orders from customers.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-120">In an enterprise example, you could use this trigger to monitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="b2ce6-121">You could then use an FTP connector action such as **Get file content** to get the contents of the order for further processing and storage in your orders database.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-121">You could then use an FTP connector action such as **Get file content** to get the contents of the order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="b2ce6-122">Enter *ftp* in the search box on the logic apps designer then select the **FTP - When a file is added or modified**  trigger</span><span class="sxs-lookup"><span data-stu-id="b2ce6-122">Enter *ftp* in the search box on the logic apps designer then select the **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="b2ce6-123">![FTP trigger image 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="b2ce6-123">![FTP trigger image 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="b2ce6-124">The **When a file is added or modified** control opens up</span><span class="sxs-lookup"><span data-stu-id="b2ce6-124">The **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="b2ce6-125">![FTP trigger image 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="b2ce6-125">![FTP trigger image 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="b2ce6-126">Select the **...** located on the right side of the control.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-126">Select the **...** located on the right side of the control.</span></span> <span data-ttu-id="b2ce6-127">This opens the folder picker control</span><span class="sxs-lookup"><span data-stu-id="b2ce6-127">This opens the folder picker control</span></span>  
   <span data-ttu-id="b2ce6-128">![FTP trigger image 3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="b2ce6-128">![FTP trigger image 3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="b2ce6-129">Select the **>** (right arrow) and browse to find the folder that you want to monitor for new or modified files.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-129">Select the **>** (right arrow) and browse to find the folder that you want to monitor for new or modified files.</span></span> <span data-ttu-id="b2ce6-130">Select the folder and notice the folder is now displayed in the **Folder** control.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-130">Select the folder and notice the folder is now displayed in the **Folder** control.</span></span>  
   <span data-ttu-id="b2ce6-131">![FTP trigger image 4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="b2ce6-131">![FTP trigger image 4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="b2ce6-132">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow when a file is either modified or created in the specific FTP folder.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-132">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow when a file is either modified or created in the specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="b2ce6-133">For a logic app to be functional, it must contain at least one trigger and one action.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-133">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="b2ce6-134">Follow the steps in the next section to add an action.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-134">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="b2ce6-135">Use a FTP action</span><span class="sxs-lookup"><span data-stu-id="b2ce6-135">Use a FTP action</span></span>
<span data-ttu-id="b2ce6-136">An action is an operation carried out by the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="b2ce6-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="b2ce6-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="b2ce6-138">Now that you have added a trigger, follow these steps to add an action that will get the contents of the new or modified file found by the trigger.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-138">Now that you have added a trigger, follow these steps to add an action that will get the contents of the new or modified file found by the trigger.</span></span>    

1. <span data-ttu-id="b2ce6-139">Select **+ New step** to add the the action to get the contents of the file on the FTP server</span><span class="sxs-lookup"><span data-stu-id="b2ce6-139">Select **+ New step** to add the the action to get the contents of the file on the FTP server</span></span>  
2. <span data-ttu-id="b2ce6-140">Select the **Add an action** link.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-140">Select the **Add an action** link.</span></span>  
   <span data-ttu-id="b2ce6-141">![FTP action image 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="b2ce6-141">![FTP action image 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="b2ce6-142">Enter *FTP* to search for all actions related to FTP.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-142">Enter *FTP* to search for all actions related to FTP.</span></span>
4. <span data-ttu-id="b2ce6-143">Select **FTP - Get file content**  as the action to take when a new or modified file is found in the FTP folder.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-143">Select **FTP - Get file content**  as the action to take when a new or modified file is found in the FTP folder.</span></span>      
   <span data-ttu-id="b2ce6-144">![FTP action image 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="b2ce6-144">![FTP action image 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="b2ce6-145">The **Get file content** control opens.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-145">The **Get file content** control opens.</span></span> <span data-ttu-id="b2ce6-146">**Note**: you will be prompted to authorize your logic app to access your FTP server account if you have not done so previously.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-146">**Note**: you will be prompted to authorize your logic app to access your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="b2ce6-147">![FTP action image 3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="b2ce6-147">![FTP action image 3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="b2ce6-148">Select the **File** control (the white space located below \*\*FILE\*\*\*).</span><span class="sxs-lookup"><span data-stu-id="b2ce6-148">Select the **File** control (the white space located below \*\*FILE\*\*\*).</span></span> <span data-ttu-id="b2ce6-149">Here, you can use any of the various properties from the new or modified file found on the FTP server.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-149">Here, you can use any of the various properties from the new or modified file found on the FTP server.</span></span>  
6. <span data-ttu-id="b2ce6-150">Select the **File content** option.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-150">Select the **File content** option.</span></span>  
   <span data-ttu-id="b2ce6-151">![FTP action image 4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="b2ce6-151">![FTP action image 4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="b2ce6-152">The control is updated, indicating that the **FTP - Get file content** action will get the *file content* of the new or modified file on the FTP server.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-152">The control is updated, indicating that the **FTP - Get file content** action will get the *file content* of the new or modified file on the FTP server.</span></span>      
   <span data-ttu-id="b2ce6-153">![FTP action image 5](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="b2ce6-153">![FTP action image 5](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="b2ce6-154">Save your work then add a file to the FTP folder to test your workflow.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-154">Save your work then add a file to the FTP folder to test your workflow.</span></span>    

<span data-ttu-id="b2ce6-155">At this point, the logic app has been configured with a trigger to monitor a folder on an FTP server and initiate the workflow when it finds either a new file or a modified file on the FTP server.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-155">At this point, the logic app has been configured with a trigger to monitor a folder on an FTP server and initiate the workflow when it finds either a new file or a modified file on the FTP server.</span></span> 

<span data-ttu-id="b2ce6-156">The logic app also has been configured with an action to get the contents of the new or modified file.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-156">The logic app also has been configured with an action to get the contents of the new or modified file.</span></span>

<span data-ttu-id="b2ce6-157">You can now add another action such as the [SQL Server - insert row](connectors-create-api-sqlazure.md#insert-row) action to insert the contents of the new or modified file into a SQL database table.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-157">You can now add another action such as the [SQL Server - insert row](connectors-create-api-sqlazure.md#insert-row) action to insert the contents of the new or modified file into a SQL database table.</span></span>  

## <a name="technical-details"></a><span data-ttu-id="b2ce6-158">Technical Details</span><span class="sxs-lookup"><span data-stu-id="b2ce6-158">Technical Details</span></span>
<span data-ttu-id="b2ce6-159">Here are the details about the triggers, actions and responses that this connection supports:</span><span class="sxs-lookup"><span data-stu-id="b2ce6-159">Here are the details about the triggers, actions and responses that this connection supports:</span></span>

## <a name="ftp-triggers"></a><span data-ttu-id="b2ce6-160">FTP triggers</span><span class="sxs-lookup"><span data-stu-id="b2ce6-160">FTP triggers</span></span>
<span data-ttu-id="b2ce6-161">FTP has the following trigger(s):</span><span class="sxs-lookup"><span data-stu-id="b2ce6-161">FTP has the following trigger(s):</span></span>  

| <span data-ttu-id="b2ce6-162">Trigger</span><span class="sxs-lookup"><span data-stu-id="b2ce6-162">Trigger</span></span> | <span data-ttu-id="b2ce6-163">Description</span><span class="sxs-lookup"><span data-stu-id="b2ce6-163">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="b2ce6-164">When a file is added or modified</span><span class="sxs-lookup"><span data-stu-id="b2ce6-164">When a file is added or modified</span></span>](connectors-create-api-ftp.md#when-a-file-is-added-or-modified) |<span data-ttu-id="b2ce6-165">This operation triggers a flow when a file is added or modified in a folder.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-165">This operation triggers a flow when a file is added or modified in a folder.</span></span> |

## <a name="ftp-actions"></a><span data-ttu-id="b2ce6-166">FTP actions</span><span class="sxs-lookup"><span data-stu-id="b2ce6-166">FTP actions</span></span>
<span data-ttu-id="b2ce6-167">FTP has the following actions:</span><span class="sxs-lookup"><span data-stu-id="b2ce6-167">FTP has the following actions:</span></span>

| <span data-ttu-id="b2ce6-168">Action</span><span class="sxs-lookup"><span data-stu-id="b2ce6-168">Action</span></span> | <span data-ttu-id="b2ce6-169">Description</span><span class="sxs-lookup"><span data-stu-id="b2ce6-169">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="b2ce6-170">Get file metadata</span><span class="sxs-lookup"><span data-stu-id="b2ce6-170">Get file metadata</span></span>](connectors-create-api-ftp.md#get-file-metadata) |<span data-ttu-id="b2ce6-171">This operation gets the metadata for a file.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-171">This operation gets the metadata for a file.</span></span> |
| [<span data-ttu-id="b2ce6-172">Update file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-172">Update file</span></span>](connectors-create-api-ftp.md#update-file) |<span data-ttu-id="b2ce6-173">This operation updates a file.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-173">This operation updates a file.</span></span> |
| [<span data-ttu-id="b2ce6-174">Delete file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-174">Delete file</span></span>](connectors-create-api-ftp.md#delete-file) |<span data-ttu-id="b2ce6-175">This operation deletes a file.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-175">This operation deletes a file.</span></span> |
| [<span data-ttu-id="b2ce6-176">Get file metadata using path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-176">Get file metadata using path</span></span>](connectors-create-api-ftp.md#get-file-metadata-using-path) |<span data-ttu-id="b2ce6-177">This operation gets the metadata of a file using the path.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-177">This operation gets the metadata of a file using the path.</span></span> |
| [<span data-ttu-id="b2ce6-178">Get file content using path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-178">Get file content using path</span></span>](connectors-create-api-ftp.md#get-file-content-using-path) |<span data-ttu-id="b2ce6-179">This operation gets the content of a file using the path.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-179">This operation gets the content of a file using the path.</span></span> |
| [<span data-ttu-id="b2ce6-180">Get file content</span><span class="sxs-lookup"><span data-stu-id="b2ce6-180">Get file content</span></span>](connectors-create-api-ftp.md#get-file-content) |<span data-ttu-id="b2ce6-181">This operation gets the content of a file.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-181">This operation gets the content of a file.</span></span> |
| [<span data-ttu-id="b2ce6-182">Create file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-182">Create file</span></span>](connectors-create-api-ftp.md#create-file) |<span data-ttu-id="b2ce6-183">This operation creates a file.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-183">This operation creates a file.</span></span> |
| [<span data-ttu-id="b2ce6-184">Copy file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-184">Copy file</span></span>](connectors-create-api-ftp.md#copy-file) |<span data-ttu-id="b2ce6-185">This operation copies a file to an FTP server.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-185">This operation copies a file to an FTP server.</span></span> |
| [<span data-ttu-id="b2ce6-186">List files in folder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-186">List files in folder</span></span>](connectors-create-api-ftp.md#list-files-in-folder) |<span data-ttu-id="b2ce6-187">This operation gets the list of files and subfolders in a folder.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-187">This operation gets the list of files and subfolders in a folder.</span></span> |
| [<span data-ttu-id="b2ce6-188">List files in root folder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-188">List files in root folder</span></span>](connectors-create-api-ftp.md#list-files-in-root-folder) |<span data-ttu-id="b2ce6-189">This operation gets the list of files and subfolders in the root folder.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-189">This operation gets the list of files and subfolders in the root folder.</span></span> |
| [<span data-ttu-id="b2ce6-190">Extract folder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-190">Extract folder</span></span>](connectors-create-api-ftp.md#extract-folder) |<span data-ttu-id="b2ce6-191">This operation extracts an archive file into a folder (example: .zip).</span><span class="sxs-lookup"><span data-stu-id="b2ce6-191">This operation extracts an archive file into a folder (example: .zip).</span></span> |

### <a name="action-details"></a><span data-ttu-id="b2ce6-192">Action details</span><span class="sxs-lookup"><span data-stu-id="b2ce6-192">Action details</span></span>
<span data-ttu-id="b2ce6-193">Here are the details for the actions and triggers for this connector, along with their responses:</span><span class="sxs-lookup"><span data-stu-id="b2ce6-193">Here are the details for the actions and triggers for this connector, along with their responses:</span></span>

### <a name="get-file-metadata"></a><span data-ttu-id="b2ce6-194">Get file metadata</span><span class="sxs-lookup"><span data-stu-id="b2ce6-194">Get file metadata</span></span>
<span data-ttu-id="b2ce6-195">This operation gets the metadata for a file.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-195">This operation gets the metadata for a file.</span></span> 

| <span data-ttu-id="b2ce6-196">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-196">Property Name</span></span> | <span data-ttu-id="b2ce6-197">Display Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-197">Display Name</span></span> | <span data-ttu-id="b2ce6-198">Description</span><span class="sxs-lookup"><span data-stu-id="b2ce6-198">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-199">id\*</span><span class="sxs-lookup"><span data-stu-id="b2ce6-199">id\*</span></span> |<span data-ttu-id="b2ce6-200">File</span><span class="sxs-lookup"><span data-stu-id="b2ce6-200">File</span></span> |<span data-ttu-id="b2ce6-201">Select a file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-201">Select a file</span></span> |

<span data-ttu-id="b2ce6-202">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="b2ce6-202">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="b2ce6-203">Output Details</span><span class="sxs-lookup"><span data-stu-id="b2ce6-203">Output Details</span></span>
<span data-ttu-id="b2ce6-204">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="b2ce6-204">BlobMetadata</span></span>

| <span data-ttu-id="b2ce6-205">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-205">Property Name</span></span> | <span data-ttu-id="b2ce6-206">Data Type</span><span class="sxs-lookup"><span data-stu-id="b2ce6-206">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-207">Id</span><span class="sxs-lookup"><span data-stu-id="b2ce6-207">Id</span></span> |<span data-ttu-id="b2ce6-208">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-208">string</span></span> |
| <span data-ttu-id="b2ce6-209">Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-209">Name</span></span> |<span data-ttu-id="b2ce6-210">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-210">string</span></span> |
| <span data-ttu-id="b2ce6-211">DisplayName</span><span class="sxs-lookup"><span data-stu-id="b2ce6-211">DisplayName</span></span> |<span data-ttu-id="b2ce6-212">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-212">string</span></span> |
| <span data-ttu-id="b2ce6-213">Path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-213">Path</span></span> |<span data-ttu-id="b2ce6-214">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-214">string</span></span> |
| <span data-ttu-id="b2ce6-215">LastModified</span><span class="sxs-lookup"><span data-stu-id="b2ce6-215">LastModified</span></span> |<span data-ttu-id="b2ce6-216">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-216">string</span></span> |
| <span data-ttu-id="b2ce6-217">Size</span><span class="sxs-lookup"><span data-stu-id="b2ce6-217">Size</span></span> |<span data-ttu-id="b2ce6-218">integer</span><span class="sxs-lookup"><span data-stu-id="b2ce6-218">integer</span></span> |
| <span data-ttu-id="b2ce6-219">MediaType</span><span class="sxs-lookup"><span data-stu-id="b2ce6-219">MediaType</span></span> |<span data-ttu-id="b2ce6-220">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-220">string</span></span> |
| <span data-ttu-id="b2ce6-221">IsFolder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-221">IsFolder</span></span> |<span data-ttu-id="b2ce6-222">boolean</span><span class="sxs-lookup"><span data-stu-id="b2ce6-222">boolean</span></span> |
| <span data-ttu-id="b2ce6-223">ETag</span><span class="sxs-lookup"><span data-stu-id="b2ce6-223">ETag</span></span> |<span data-ttu-id="b2ce6-224">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-224">string</span></span> |
| <span data-ttu-id="b2ce6-225">FileLocator</span><span class="sxs-lookup"><span data-stu-id="b2ce6-225">FileLocator</span></span> |<span data-ttu-id="b2ce6-226">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-226">string</span></span> |

### <a name="update-file"></a><span data-ttu-id="b2ce6-227">Update file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-227">Update file</span></span>
<span data-ttu-id="b2ce6-228">This operation updates a file.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-228">This operation updates a file.</span></span> 

| <span data-ttu-id="b2ce6-229">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-229">Property Name</span></span> | <span data-ttu-id="b2ce6-230">Display Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-230">Display Name</span></span> | <span data-ttu-id="b2ce6-231">Description</span><span class="sxs-lookup"><span data-stu-id="b2ce6-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-232">id\*</span><span class="sxs-lookup"><span data-stu-id="b2ce6-232">id\*</span></span> |<span data-ttu-id="b2ce6-233">File</span><span class="sxs-lookup"><span data-stu-id="b2ce6-233">File</span></span> |<span data-ttu-id="b2ce6-234">Select a file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-234">Select a file</span></span> |
| <span data-ttu-id="b2ce6-235">body\*</span><span class="sxs-lookup"><span data-stu-id="b2ce6-235">body\*</span></span> |<span data-ttu-id="b2ce6-236">File content</span><span class="sxs-lookup"><span data-stu-id="b2ce6-236">File content</span></span> |<span data-ttu-id="b2ce6-237">Content of the file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-237">Content of the file</span></span> |

<span data-ttu-id="b2ce6-238">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="b2ce6-238">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="b2ce6-239">Output Details</span><span class="sxs-lookup"><span data-stu-id="b2ce6-239">Output Details</span></span>
<span data-ttu-id="b2ce6-240">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="b2ce6-240">BlobMetadata</span></span>

| <span data-ttu-id="b2ce6-241">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-241">Property Name</span></span> | <span data-ttu-id="b2ce6-242">Data Type</span><span class="sxs-lookup"><span data-stu-id="b2ce6-242">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-243">Id</span><span class="sxs-lookup"><span data-stu-id="b2ce6-243">Id</span></span> |<span data-ttu-id="b2ce6-244">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-244">string</span></span> |
| <span data-ttu-id="b2ce6-245">Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-245">Name</span></span> |<span data-ttu-id="b2ce6-246">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-246">string</span></span> |
| <span data-ttu-id="b2ce6-247">DisplayName</span><span class="sxs-lookup"><span data-stu-id="b2ce6-247">DisplayName</span></span> |<span data-ttu-id="b2ce6-248">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-248">string</span></span> |
| <span data-ttu-id="b2ce6-249">Path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-249">Path</span></span> |<span data-ttu-id="b2ce6-250">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-250">string</span></span> |
| <span data-ttu-id="b2ce6-251">LastModified</span><span class="sxs-lookup"><span data-stu-id="b2ce6-251">LastModified</span></span> |<span data-ttu-id="b2ce6-252">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-252">string</span></span> |
| <span data-ttu-id="b2ce6-253">Size</span><span class="sxs-lookup"><span data-stu-id="b2ce6-253">Size</span></span> |<span data-ttu-id="b2ce6-254">integer</span><span class="sxs-lookup"><span data-stu-id="b2ce6-254">integer</span></span> |
| <span data-ttu-id="b2ce6-255">MediaType</span><span class="sxs-lookup"><span data-stu-id="b2ce6-255">MediaType</span></span> |<span data-ttu-id="b2ce6-256">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-256">string</span></span> |
| <span data-ttu-id="b2ce6-257">IsFolder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-257">IsFolder</span></span> |<span data-ttu-id="b2ce6-258">boolean</span><span class="sxs-lookup"><span data-stu-id="b2ce6-258">boolean</span></span> |
| <span data-ttu-id="b2ce6-259">ETag</span><span class="sxs-lookup"><span data-stu-id="b2ce6-259">ETag</span></span> |<span data-ttu-id="b2ce6-260">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-260">string</span></span> |
| <span data-ttu-id="b2ce6-261">FileLocator</span><span class="sxs-lookup"><span data-stu-id="b2ce6-261">FileLocator</span></span> |<span data-ttu-id="b2ce6-262">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-262">string</span></span> |

### <a name="delete-file"></a><span data-ttu-id="b2ce6-263">Delete file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-263">Delete file</span></span>
<span data-ttu-id="b2ce6-264">This operation deletes a file.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-264">This operation deletes a file.</span></span> 

| <span data-ttu-id="b2ce6-265">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-265">Property Name</span></span> | <span data-ttu-id="b2ce6-266">Display Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-266">Display Name</span></span> | <span data-ttu-id="b2ce6-267">Description</span><span class="sxs-lookup"><span data-stu-id="b2ce6-267">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-268">id\*</span><span class="sxs-lookup"><span data-stu-id="b2ce6-268">id\*</span></span> |<span data-ttu-id="b2ce6-269">File</span><span class="sxs-lookup"><span data-stu-id="b2ce6-269">File</span></span> |<span data-ttu-id="b2ce6-270">Select a file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-270">Select a file</span></span> |

<span data-ttu-id="b2ce6-271">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="b2ce6-271">An \* indicates that a property is required</span></span>

### <a name="get-file-metadata-using-path"></a><span data-ttu-id="b2ce6-272">Get file metadata using path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-272">Get file metadata using path</span></span>
<span data-ttu-id="b2ce6-273">This operation gets the metadata of a file using the path.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-273">This operation gets the metadata of a file using the path.</span></span> 

| <span data-ttu-id="b2ce6-274">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-274">Property Name</span></span> | <span data-ttu-id="b2ce6-275">Display Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-275">Display Name</span></span> | <span data-ttu-id="b2ce6-276">Description</span><span class="sxs-lookup"><span data-stu-id="b2ce6-276">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-277">path\*</span><span class="sxs-lookup"><span data-stu-id="b2ce6-277">path\*</span></span> |<span data-ttu-id="b2ce6-278">File path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-278">File path</span></span> |<span data-ttu-id="b2ce6-279">Select a file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-279">Select a file</span></span> |

<span data-ttu-id="b2ce6-280">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="b2ce6-280">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="b2ce6-281">Output Details</span><span class="sxs-lookup"><span data-stu-id="b2ce6-281">Output Details</span></span>
<span data-ttu-id="b2ce6-282">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="b2ce6-282">BlobMetadata</span></span>

| <span data-ttu-id="b2ce6-283">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-283">Property Name</span></span> | <span data-ttu-id="b2ce6-284">Data Type</span><span class="sxs-lookup"><span data-stu-id="b2ce6-284">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-285">Id</span><span class="sxs-lookup"><span data-stu-id="b2ce6-285">Id</span></span> |<span data-ttu-id="b2ce6-286">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-286">string</span></span> |
| <span data-ttu-id="b2ce6-287">Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-287">Name</span></span> |<span data-ttu-id="b2ce6-288">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-288">string</span></span> |
| <span data-ttu-id="b2ce6-289">DisplayName</span><span class="sxs-lookup"><span data-stu-id="b2ce6-289">DisplayName</span></span> |<span data-ttu-id="b2ce6-290">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-290">string</span></span> |
| <span data-ttu-id="b2ce6-291">Path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-291">Path</span></span> |<span data-ttu-id="b2ce6-292">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-292">string</span></span> |
| <span data-ttu-id="b2ce6-293">LastModified</span><span class="sxs-lookup"><span data-stu-id="b2ce6-293">LastModified</span></span> |<span data-ttu-id="b2ce6-294">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-294">string</span></span> |
| <span data-ttu-id="b2ce6-295">Size</span><span class="sxs-lookup"><span data-stu-id="b2ce6-295">Size</span></span> |<span data-ttu-id="b2ce6-296">integer</span><span class="sxs-lookup"><span data-stu-id="b2ce6-296">integer</span></span> |
| <span data-ttu-id="b2ce6-297">MediaType</span><span class="sxs-lookup"><span data-stu-id="b2ce6-297">MediaType</span></span> |<span data-ttu-id="b2ce6-298">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-298">string</span></span> |
| <span data-ttu-id="b2ce6-299">IsFolder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-299">IsFolder</span></span> |<span data-ttu-id="b2ce6-300">boolean</span><span class="sxs-lookup"><span data-stu-id="b2ce6-300">boolean</span></span> |
| <span data-ttu-id="b2ce6-301">ETag</span><span class="sxs-lookup"><span data-stu-id="b2ce6-301">ETag</span></span> |<span data-ttu-id="b2ce6-302">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-302">string</span></span> |
| <span data-ttu-id="b2ce6-303">FileLocator</span><span class="sxs-lookup"><span data-stu-id="b2ce6-303">FileLocator</span></span> |<span data-ttu-id="b2ce6-304">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-304">string</span></span> |

### <a name="get-file-content-using-path"></a><span data-ttu-id="b2ce6-305">Get file content using path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-305">Get file content using path</span></span>
<span data-ttu-id="b2ce6-306">This operation gets the content of a file using the path.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-306">This operation gets the content of a file using the path.</span></span> 

| <span data-ttu-id="b2ce6-307">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-307">Property Name</span></span> | <span data-ttu-id="b2ce6-308">Display Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-308">Display Name</span></span> | <span data-ttu-id="b2ce6-309">Description</span><span class="sxs-lookup"><span data-stu-id="b2ce6-309">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-310">path\*</span><span class="sxs-lookup"><span data-stu-id="b2ce6-310">path\*</span></span> |<span data-ttu-id="b2ce6-311">File path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-311">File path</span></span> |<span data-ttu-id="b2ce6-312">Select a file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-312">Select a file</span></span> |

<span data-ttu-id="b2ce6-313">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="b2ce6-313">An \* indicates that a property is required</span></span>

### <a name="get-file-content"></a><span data-ttu-id="b2ce6-314">Get file content</span><span class="sxs-lookup"><span data-stu-id="b2ce6-314">Get file content</span></span>
<span data-ttu-id="b2ce6-315">This operation gets the content of a file.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-315">This operation gets the content of a file.</span></span> 

| <span data-ttu-id="b2ce6-316">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-316">Property Name</span></span> | <span data-ttu-id="b2ce6-317">Display Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-317">Display Name</span></span> | <span data-ttu-id="b2ce6-318">Description</span><span class="sxs-lookup"><span data-stu-id="b2ce6-318">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-319">id\*</span><span class="sxs-lookup"><span data-stu-id="b2ce6-319">id\*</span></span> |<span data-ttu-id="b2ce6-320">File</span><span class="sxs-lookup"><span data-stu-id="b2ce6-320">File</span></span> |<span data-ttu-id="b2ce6-321">Select a file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-321">Select a file</span></span> |

<span data-ttu-id="b2ce6-322">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="b2ce6-322">An \* indicates that a property is required</span></span>

### <a name="create-file"></a><span data-ttu-id="b2ce6-323">Create file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-323">Create file</span></span>
<span data-ttu-id="b2ce6-324">This operation creates a file.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-324">This operation creates a file.</span></span> 

| <span data-ttu-id="b2ce6-325">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-325">Property Name</span></span> | <span data-ttu-id="b2ce6-326">Display Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-326">Display Name</span></span> | <span data-ttu-id="b2ce6-327">Description</span><span class="sxs-lookup"><span data-stu-id="b2ce6-327">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-328">folderPath\*</span><span class="sxs-lookup"><span data-stu-id="b2ce6-328">folderPath\*</span></span> |<span data-ttu-id="b2ce6-329">Folder path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-329">Folder path</span></span> |<span data-ttu-id="b2ce6-330">Select a folder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-330">Select a folder</span></span> |
| <span data-ttu-id="b2ce6-331">name\*</span><span class="sxs-lookup"><span data-stu-id="b2ce6-331">name\*</span></span> |<span data-ttu-id="b2ce6-332">File name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-332">File name</span></span> |<span data-ttu-id="b2ce6-333">Name of the file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-333">Name of the file</span></span> |
| <span data-ttu-id="b2ce6-334">body\*</span><span class="sxs-lookup"><span data-stu-id="b2ce6-334">body\*</span></span> |<span data-ttu-id="b2ce6-335">File content</span><span class="sxs-lookup"><span data-stu-id="b2ce6-335">File content</span></span> |<span data-ttu-id="b2ce6-336">Content of the file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-336">Content of the file</span></span> |

<span data-ttu-id="b2ce6-337">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="b2ce6-337">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="b2ce6-338">Output Details</span><span class="sxs-lookup"><span data-stu-id="b2ce6-338">Output Details</span></span>
<span data-ttu-id="b2ce6-339">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="b2ce6-339">BlobMetadata</span></span>

| <span data-ttu-id="b2ce6-340">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-340">Property Name</span></span> | <span data-ttu-id="b2ce6-341">Data Type</span><span class="sxs-lookup"><span data-stu-id="b2ce6-341">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-342">Id</span><span class="sxs-lookup"><span data-stu-id="b2ce6-342">Id</span></span> |<span data-ttu-id="b2ce6-343">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-343">string</span></span> |
| <span data-ttu-id="b2ce6-344">Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-344">Name</span></span> |<span data-ttu-id="b2ce6-345">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-345">string</span></span> |
| <span data-ttu-id="b2ce6-346">DisplayName</span><span class="sxs-lookup"><span data-stu-id="b2ce6-346">DisplayName</span></span> |<span data-ttu-id="b2ce6-347">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-347">string</span></span> |
| <span data-ttu-id="b2ce6-348">Path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-348">Path</span></span> |<span data-ttu-id="b2ce6-349">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-349">string</span></span> |
| <span data-ttu-id="b2ce6-350">LastModified</span><span class="sxs-lookup"><span data-stu-id="b2ce6-350">LastModified</span></span> |<span data-ttu-id="b2ce6-351">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-351">string</span></span> |
| <span data-ttu-id="b2ce6-352">Size</span><span class="sxs-lookup"><span data-stu-id="b2ce6-352">Size</span></span> |<span data-ttu-id="b2ce6-353">integer</span><span class="sxs-lookup"><span data-stu-id="b2ce6-353">integer</span></span> |
| <span data-ttu-id="b2ce6-354">MediaType</span><span class="sxs-lookup"><span data-stu-id="b2ce6-354">MediaType</span></span> |<span data-ttu-id="b2ce6-355">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-355">string</span></span> |
| <span data-ttu-id="b2ce6-356">IsFolder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-356">IsFolder</span></span> |<span data-ttu-id="b2ce6-357">boolean</span><span class="sxs-lookup"><span data-stu-id="b2ce6-357">boolean</span></span> |
| <span data-ttu-id="b2ce6-358">ETag</span><span class="sxs-lookup"><span data-stu-id="b2ce6-358">ETag</span></span> |<span data-ttu-id="b2ce6-359">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-359">string</span></span> |
| <span data-ttu-id="b2ce6-360">FileLocator</span><span class="sxs-lookup"><span data-stu-id="b2ce6-360">FileLocator</span></span> |<span data-ttu-id="b2ce6-361">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-361">string</span></span> |

### <a name="copy-file"></a><span data-ttu-id="b2ce6-362">Copy file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-362">Copy file</span></span>
<span data-ttu-id="b2ce6-363">This operation copies a file to an FTP server.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-363">This operation copies a file to an FTP server.</span></span> 

| <span data-ttu-id="b2ce6-364">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-364">Property Name</span></span> | <span data-ttu-id="b2ce6-365">Display Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-365">Display Name</span></span> | <span data-ttu-id="b2ce6-366">Description</span><span class="sxs-lookup"><span data-stu-id="b2ce6-366">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-367">source\*</span><span class="sxs-lookup"><span data-stu-id="b2ce6-367">source\*</span></span> |<span data-ttu-id="b2ce6-368">Source url</span><span class="sxs-lookup"><span data-stu-id="b2ce6-368">Source url</span></span> |<span data-ttu-id="b2ce6-369">Url to source file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-369">Url to source file</span></span> |
| <span data-ttu-id="b2ce6-370">destination\*</span><span class="sxs-lookup"><span data-stu-id="b2ce6-370">destination\*</span></span> |<span data-ttu-id="b2ce6-371">Destination file path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-371">Destination file path</span></span> |<span data-ttu-id="b2ce6-372">Destination file path, including target filename</span><span class="sxs-lookup"><span data-stu-id="b2ce6-372">Destination file path, including target filename</span></span> |
| <span data-ttu-id="b2ce6-373">overwrite</span><span class="sxs-lookup"><span data-stu-id="b2ce6-373">overwrite</span></span> |<span data-ttu-id="b2ce6-374">Overwrite?</span><span class="sxs-lookup"><span data-stu-id="b2ce6-374">Overwrite?</span></span> |<span data-ttu-id="b2ce6-375">Overwrites the destination file if set to 'true'</span><span class="sxs-lookup"><span data-stu-id="b2ce6-375">Overwrites the destination file if set to 'true'</span></span> |

<span data-ttu-id="b2ce6-376">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="b2ce6-376">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="b2ce6-377">Output Details</span><span class="sxs-lookup"><span data-stu-id="b2ce6-377">Output Details</span></span>
<span data-ttu-id="b2ce6-378">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="b2ce6-378">BlobMetadata</span></span>

| <span data-ttu-id="b2ce6-379">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-379">Property Name</span></span> | <span data-ttu-id="b2ce6-380">Data Type</span><span class="sxs-lookup"><span data-stu-id="b2ce6-380">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-381">Id</span><span class="sxs-lookup"><span data-stu-id="b2ce6-381">Id</span></span> |<span data-ttu-id="b2ce6-382">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-382">string</span></span> |
| <span data-ttu-id="b2ce6-383">Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-383">Name</span></span> |<span data-ttu-id="b2ce6-384">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-384">string</span></span> |
| <span data-ttu-id="b2ce6-385">DisplayName</span><span class="sxs-lookup"><span data-stu-id="b2ce6-385">DisplayName</span></span> |<span data-ttu-id="b2ce6-386">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-386">string</span></span> |
| <span data-ttu-id="b2ce6-387">Path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-387">Path</span></span> |<span data-ttu-id="b2ce6-388">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-388">string</span></span> |
| <span data-ttu-id="b2ce6-389">LastModified</span><span class="sxs-lookup"><span data-stu-id="b2ce6-389">LastModified</span></span> |<span data-ttu-id="b2ce6-390">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-390">string</span></span> |
| <span data-ttu-id="b2ce6-391">Size</span><span class="sxs-lookup"><span data-stu-id="b2ce6-391">Size</span></span> |<span data-ttu-id="b2ce6-392">integer</span><span class="sxs-lookup"><span data-stu-id="b2ce6-392">integer</span></span> |
| <span data-ttu-id="b2ce6-393">MediaType</span><span class="sxs-lookup"><span data-stu-id="b2ce6-393">MediaType</span></span> |<span data-ttu-id="b2ce6-394">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-394">string</span></span> |
| <span data-ttu-id="b2ce6-395">IsFolder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-395">IsFolder</span></span> |<span data-ttu-id="b2ce6-396">boolean</span><span class="sxs-lookup"><span data-stu-id="b2ce6-396">boolean</span></span> |
| <span data-ttu-id="b2ce6-397">ETag</span><span class="sxs-lookup"><span data-stu-id="b2ce6-397">ETag</span></span> |<span data-ttu-id="b2ce6-398">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-398">string</span></span> |
| <span data-ttu-id="b2ce6-399">FileLocator</span><span class="sxs-lookup"><span data-stu-id="b2ce6-399">FileLocator</span></span> |<span data-ttu-id="b2ce6-400">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-400">string</span></span> |

### <a name="when-a-file-is-added-or-modified"></a><span data-ttu-id="b2ce6-401">When a file is added or modified</span><span class="sxs-lookup"><span data-stu-id="b2ce6-401">When a file is added or modified</span></span>
<span data-ttu-id="b2ce6-402">This operation triggers a flow when a file is added or modified in a folder.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-402">This operation triggers a flow when a file is added or modified in a folder.</span></span> 

| <span data-ttu-id="b2ce6-403">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-403">Property Name</span></span> | <span data-ttu-id="b2ce6-404">Display Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-404">Display Name</span></span> | <span data-ttu-id="b2ce6-405">Description</span><span class="sxs-lookup"><span data-stu-id="b2ce6-405">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-406">folderId\*</span><span class="sxs-lookup"><span data-stu-id="b2ce6-406">folderId\*</span></span> |<span data-ttu-id="b2ce6-407">Folder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-407">Folder</span></span> |<span data-ttu-id="b2ce6-408">Select a folder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-408">Select a folder</span></span> |

<span data-ttu-id="b2ce6-409">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="b2ce6-409">An \* indicates that a property is required</span></span>

### <a name="list-files-in-folder"></a><span data-ttu-id="b2ce6-410">List files in folder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-410">List files in folder</span></span>
<span data-ttu-id="b2ce6-411">This operation gets the list of files and subfolders in a folder.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-411">This operation gets the list of files and subfolders in a folder.</span></span> 

| <span data-ttu-id="b2ce6-412">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-412">Property Name</span></span> | <span data-ttu-id="b2ce6-413">Display Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-413">Display Name</span></span> | <span data-ttu-id="b2ce6-414">Description</span><span class="sxs-lookup"><span data-stu-id="b2ce6-414">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-415">id\*</span><span class="sxs-lookup"><span data-stu-id="b2ce6-415">id\*</span></span> |<span data-ttu-id="b2ce6-416">Folder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-416">Folder</span></span> |<span data-ttu-id="b2ce6-417">Select a folder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-417">Select a folder</span></span> |

<span data-ttu-id="b2ce6-418">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="b2ce6-418">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="b2ce6-419">Output Details</span><span class="sxs-lookup"><span data-stu-id="b2ce6-419">Output Details</span></span>
<span data-ttu-id="b2ce6-420">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="b2ce6-420">BlobMetadata</span></span>

| <span data-ttu-id="b2ce6-421">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-421">Property Name</span></span> | <span data-ttu-id="b2ce6-422">Data Type</span><span class="sxs-lookup"><span data-stu-id="b2ce6-422">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-423">Id</span><span class="sxs-lookup"><span data-stu-id="b2ce6-423">Id</span></span> |<span data-ttu-id="b2ce6-424">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-424">string</span></span> |
| <span data-ttu-id="b2ce6-425">Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-425">Name</span></span> |<span data-ttu-id="b2ce6-426">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-426">string</span></span> |
| <span data-ttu-id="b2ce6-427">DisplayName</span><span class="sxs-lookup"><span data-stu-id="b2ce6-427">DisplayName</span></span> |<span data-ttu-id="b2ce6-428">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-428">string</span></span> |
| <span data-ttu-id="b2ce6-429">Path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-429">Path</span></span> |<span data-ttu-id="b2ce6-430">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-430">string</span></span> |
| <span data-ttu-id="b2ce6-431">LastModified</span><span class="sxs-lookup"><span data-stu-id="b2ce6-431">LastModified</span></span> |<span data-ttu-id="b2ce6-432">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-432">string</span></span> |
| <span data-ttu-id="b2ce6-433">Size</span><span class="sxs-lookup"><span data-stu-id="b2ce6-433">Size</span></span> |<span data-ttu-id="b2ce6-434">integer</span><span class="sxs-lookup"><span data-stu-id="b2ce6-434">integer</span></span> |
| <span data-ttu-id="b2ce6-435">MediaType</span><span class="sxs-lookup"><span data-stu-id="b2ce6-435">MediaType</span></span> |<span data-ttu-id="b2ce6-436">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-436">string</span></span> |
| <span data-ttu-id="b2ce6-437">IsFolder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-437">IsFolder</span></span> |<span data-ttu-id="b2ce6-438">boolean</span><span class="sxs-lookup"><span data-stu-id="b2ce6-438">boolean</span></span> |
| <span data-ttu-id="b2ce6-439">ETag</span><span class="sxs-lookup"><span data-stu-id="b2ce6-439">ETag</span></span> |<span data-ttu-id="b2ce6-440">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-440">string</span></span> |
| <span data-ttu-id="b2ce6-441">FileLocator</span><span class="sxs-lookup"><span data-stu-id="b2ce6-441">FileLocator</span></span> |<span data-ttu-id="b2ce6-442">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-442">string</span></span> |

### <a name="list-files-in-root-folder"></a><span data-ttu-id="b2ce6-443">List files in root folder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-443">List files in root folder</span></span>
<span data-ttu-id="b2ce6-444">This operation gets the list of files and subfolders in the root folder.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-444">This operation gets the list of files and subfolders in the root folder.</span></span> 

<span data-ttu-id="b2ce6-445">There are no parameters for this call</span><span class="sxs-lookup"><span data-stu-id="b2ce6-445">There are no parameters for this call</span></span>

#### <a name="output-details"></a><span data-ttu-id="b2ce6-446">Output Details</span><span class="sxs-lookup"><span data-stu-id="b2ce6-446">Output Details</span></span>
<span data-ttu-id="b2ce6-447">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="b2ce6-447">BlobMetadata</span></span>

| <span data-ttu-id="b2ce6-448">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-448">Property Name</span></span> | <span data-ttu-id="b2ce6-449">Data Type</span><span class="sxs-lookup"><span data-stu-id="b2ce6-449">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-450">Id</span><span class="sxs-lookup"><span data-stu-id="b2ce6-450">Id</span></span> |<span data-ttu-id="b2ce6-451">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-451">string</span></span> |
| <span data-ttu-id="b2ce6-452">Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-452">Name</span></span> |<span data-ttu-id="b2ce6-453">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-453">string</span></span> |
| <span data-ttu-id="b2ce6-454">DisplayName</span><span class="sxs-lookup"><span data-stu-id="b2ce6-454">DisplayName</span></span> |<span data-ttu-id="b2ce6-455">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-455">string</span></span> |
| <span data-ttu-id="b2ce6-456">Path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-456">Path</span></span> |<span data-ttu-id="b2ce6-457">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-457">string</span></span> |
| <span data-ttu-id="b2ce6-458">LastModified</span><span class="sxs-lookup"><span data-stu-id="b2ce6-458">LastModified</span></span> |<span data-ttu-id="b2ce6-459">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-459">string</span></span> |
| <span data-ttu-id="b2ce6-460">Size</span><span class="sxs-lookup"><span data-stu-id="b2ce6-460">Size</span></span> |<span data-ttu-id="b2ce6-461">integer</span><span class="sxs-lookup"><span data-stu-id="b2ce6-461">integer</span></span> |
| <span data-ttu-id="b2ce6-462">MediaType</span><span class="sxs-lookup"><span data-stu-id="b2ce6-462">MediaType</span></span> |<span data-ttu-id="b2ce6-463">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-463">string</span></span> |
| <span data-ttu-id="b2ce6-464">IsFolder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-464">IsFolder</span></span> |<span data-ttu-id="b2ce6-465">boolean</span><span class="sxs-lookup"><span data-stu-id="b2ce6-465">boolean</span></span> |
| <span data-ttu-id="b2ce6-466">ETag</span><span class="sxs-lookup"><span data-stu-id="b2ce6-466">ETag</span></span> |<span data-ttu-id="b2ce6-467">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-467">string</span></span> |
| <span data-ttu-id="b2ce6-468">FileLocator</span><span class="sxs-lookup"><span data-stu-id="b2ce6-468">FileLocator</span></span> |<span data-ttu-id="b2ce6-469">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-469">string</span></span> |

### <a name="extract-folder"></a><span data-ttu-id="b2ce6-470">Extract folder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-470">Extract folder</span></span>
<span data-ttu-id="b2ce6-471">This operation extracts an archive file into a folder (example: .zip).</span><span class="sxs-lookup"><span data-stu-id="b2ce6-471">This operation extracts an archive file into a folder (example: .zip).</span></span> 

| <span data-ttu-id="b2ce6-472">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-472">Property Name</span></span> | <span data-ttu-id="b2ce6-473">Display Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-473">Display Name</span></span> | <span data-ttu-id="b2ce6-474">Description</span><span class="sxs-lookup"><span data-stu-id="b2ce6-474">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-475">source\*</span><span class="sxs-lookup"><span data-stu-id="b2ce6-475">source\*</span></span> |<span data-ttu-id="b2ce6-476">Source archive file path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-476">Source archive file path</span></span> |<span data-ttu-id="b2ce6-477">Path to the archive file</span><span class="sxs-lookup"><span data-stu-id="b2ce6-477">Path to the archive file</span></span> |
| <span data-ttu-id="b2ce6-478">destination\*</span><span class="sxs-lookup"><span data-stu-id="b2ce6-478">destination\*</span></span> |<span data-ttu-id="b2ce6-479">Destination folder path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-479">Destination folder path</span></span> |<span data-ttu-id="b2ce6-480">Path to the destination folder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-480">Path to the destination folder</span></span> |
| <span data-ttu-id="b2ce6-481">overwrite</span><span class="sxs-lookup"><span data-stu-id="b2ce6-481">overwrite</span></span> |<span data-ttu-id="b2ce6-482">Overwrite?</span><span class="sxs-lookup"><span data-stu-id="b2ce6-482">Overwrite?</span></span> |<span data-ttu-id="b2ce6-483">Overwrites the destination files if set to 'true'</span><span class="sxs-lookup"><span data-stu-id="b2ce6-483">Overwrites the destination files if set to 'true'</span></span> |

<span data-ttu-id="b2ce6-484">An \* indicates that a property is required</span><span class="sxs-lookup"><span data-stu-id="b2ce6-484">An \* indicates that a property is required</span></span>

#### <a name="output-details"></a><span data-ttu-id="b2ce6-485">Output Details</span><span class="sxs-lookup"><span data-stu-id="b2ce6-485">Output Details</span></span>
<span data-ttu-id="b2ce6-486">BlobMetadata</span><span class="sxs-lookup"><span data-stu-id="b2ce6-486">BlobMetadata</span></span>

| <span data-ttu-id="b2ce6-487">Property Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-487">Property Name</span></span> | <span data-ttu-id="b2ce6-488">Data Type</span><span class="sxs-lookup"><span data-stu-id="b2ce6-488">Data Type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2ce6-489">Id</span><span class="sxs-lookup"><span data-stu-id="b2ce6-489">Id</span></span> |<span data-ttu-id="b2ce6-490">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-490">string</span></span> |
| <span data-ttu-id="b2ce6-491">Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-491">Name</span></span> |<span data-ttu-id="b2ce6-492">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-492">string</span></span> |
| <span data-ttu-id="b2ce6-493">DisplayName</span><span class="sxs-lookup"><span data-stu-id="b2ce6-493">DisplayName</span></span> |<span data-ttu-id="b2ce6-494">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-494">string</span></span> |
| <span data-ttu-id="b2ce6-495">Path</span><span class="sxs-lookup"><span data-stu-id="b2ce6-495">Path</span></span> |<span data-ttu-id="b2ce6-496">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-496">string</span></span> |
| <span data-ttu-id="b2ce6-497">LastModified</span><span class="sxs-lookup"><span data-stu-id="b2ce6-497">LastModified</span></span> |<span data-ttu-id="b2ce6-498">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-498">string</span></span> |
| <span data-ttu-id="b2ce6-499">Size</span><span class="sxs-lookup"><span data-stu-id="b2ce6-499">Size</span></span> |<span data-ttu-id="b2ce6-500">integer</span><span class="sxs-lookup"><span data-stu-id="b2ce6-500">integer</span></span> |
| <span data-ttu-id="b2ce6-501">MediaType</span><span class="sxs-lookup"><span data-stu-id="b2ce6-501">MediaType</span></span> |<span data-ttu-id="b2ce6-502">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-502">string</span></span> |
| <span data-ttu-id="b2ce6-503">IsFolder</span><span class="sxs-lookup"><span data-stu-id="b2ce6-503">IsFolder</span></span> |<span data-ttu-id="b2ce6-504">boolean</span><span class="sxs-lookup"><span data-stu-id="b2ce6-504">boolean</span></span> |
| <span data-ttu-id="b2ce6-505">ETag</span><span class="sxs-lookup"><span data-stu-id="b2ce6-505">ETag</span></span> |<span data-ttu-id="b2ce6-506">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-506">string</span></span> |
| <span data-ttu-id="b2ce6-507">FileLocator</span><span class="sxs-lookup"><span data-stu-id="b2ce6-507">FileLocator</span></span> |<span data-ttu-id="b2ce6-508">string</span><span class="sxs-lookup"><span data-stu-id="b2ce6-508">string</span></span> |

## <a name="http-responses"></a><span data-ttu-id="b2ce6-509">HTTP responses</span><span class="sxs-lookup"><span data-stu-id="b2ce6-509">HTTP responses</span></span>
<span data-ttu-id="b2ce6-510">The actions and triggers above can return one or more of the following HTTP status codes:</span><span class="sxs-lookup"><span data-stu-id="b2ce6-510">The actions and triggers above can return one or more of the following HTTP status codes:</span></span> 

| <span data-ttu-id="b2ce6-511">Name</span><span class="sxs-lookup"><span data-stu-id="b2ce6-511">Name</span></span> | <span data-ttu-id="b2ce6-512">Description</span><span class="sxs-lookup"><span data-stu-id="b2ce6-512">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b2ce6-513">200</span><span class="sxs-lookup"><span data-stu-id="b2ce6-513">200</span></span> |<span data-ttu-id="b2ce6-514">OK</span><span class="sxs-lookup"><span data-stu-id="b2ce6-514">OK</span></span> |
| <span data-ttu-id="b2ce6-515">202</span><span class="sxs-lookup"><span data-stu-id="b2ce6-515">202</span></span> |<span data-ttu-id="b2ce6-516">Accepted</span><span class="sxs-lookup"><span data-stu-id="b2ce6-516">Accepted</span></span> |
| <span data-ttu-id="b2ce6-517">400</span><span class="sxs-lookup"><span data-stu-id="b2ce6-517">400</span></span> |<span data-ttu-id="b2ce6-518">Bad Request</span><span class="sxs-lookup"><span data-stu-id="b2ce6-518">Bad Request</span></span> |
| <span data-ttu-id="b2ce6-519">401</span><span class="sxs-lookup"><span data-stu-id="b2ce6-519">401</span></span> |<span data-ttu-id="b2ce6-520">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="b2ce6-520">Unauthorized</span></span> |
| <span data-ttu-id="b2ce6-521">403</span><span class="sxs-lookup"><span data-stu-id="b2ce6-521">403</span></span> |<span data-ttu-id="b2ce6-522">Forbidden</span><span class="sxs-lookup"><span data-stu-id="b2ce6-522">Forbidden</span></span> |
| <span data-ttu-id="b2ce6-523">404</span><span class="sxs-lookup"><span data-stu-id="b2ce6-523">404</span></span> |<span data-ttu-id="b2ce6-524">Not Found</span><span class="sxs-lookup"><span data-stu-id="b2ce6-524">Not Found</span></span> |
| <span data-ttu-id="b2ce6-525">500</span><span class="sxs-lookup"><span data-stu-id="b2ce6-525">500</span></span> |<span data-ttu-id="b2ce6-526">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-526">Internal Server Error.</span></span> <span data-ttu-id="b2ce6-527">Unknown error occurred.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-527">Unknown error occurred.</span></span> |
| <span data-ttu-id="b2ce6-528">default</span><span class="sxs-lookup"><span data-stu-id="b2ce6-528">default</span></span> |<span data-ttu-id="b2ce6-529">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="b2ce6-529">Operation Failed.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b2ce6-530">Next Steps</span><span class="sxs-lookup"><span data-stu-id="b2ce6-530">Next Steps</span></span>
[<span data-ttu-id="b2ce6-531">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="b2ce6-531">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)










