---
title: Change blob path from the default | Microsoft Docs
description: Learn how to set up an Azure function to rename a blob file path (private preview)
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: ''
ms.assetid: ''
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: dbb90d1d2b54e37bb4d774b7e0d4f9b61947d88e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555117"
---
# <a name="change-a-blob-path-from-the-default-path-private-preview"></a><span data-ttu-id="4cbdc-103">Change a blob path from the default path (private preview)</span><span class="sxs-lookup"><span data-stu-id="4cbdc-103">Change a blob path from the default path (private preview)</span></span>

<span data-ttu-id="4cbdc-104">This article describes how to set up an Azure function to rename a default blob file path.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-104">This article describes how to set up an Azure function to rename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4cbdc-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4cbdc-105">Prerequisites</span></span>

<span data-ttu-id="4cbdc-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="4cbdc-107">Create an Azure function</span><span class="sxs-lookup"><span data-stu-id="4cbdc-107">Create an Azure function</span></span>

<span data-ttu-id="4cbdc-108">To create an Azure function, do the following:</span><span class="sxs-lookup"><span data-stu-id="4cbdc-108">To create an Azure function, do the following:</span></span>

1. <span data-ttu-id="4cbdc-109">Go to the [Azure portal](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4cbdc-109">Go to the [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="4cbdc-110">At the top of the left pane, click **New**.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-110">At the top of the left pane, click **New**.</span></span> 

3. <span data-ttu-id="4cbdc-111">In the **Search** box, type **Function App**, and then press Enter.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-111">In the **Search** box, type **Function App**, and then press Enter.</span></span>

    ![Type "Function App" in the Search box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="4cbdc-113">In the **Results** list, click **Function App**.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-113">In the **Results** list, click **Function App**.</span></span>

    ![Select the function app resource in the results list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="4cbdc-115">The **Function App** window opens.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-115">The **Function App** window opens.</span></span>

5. <span data-ttu-id="4cbdc-116">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-116">Click **Create**.</span></span>

    ![The Function App window "Create" button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="4cbdc-118">On the **Function App** configuration blade, do the following:</span><span class="sxs-lookup"><span data-stu-id="4cbdc-118">On the **Function App** configuration blade, do the following:</span></span>

    <span data-ttu-id="4cbdc-119">a.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-119">a.</span></span> <span data-ttu-id="4cbdc-120">In the **App name** box, type the app name.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-120">In the **App name** box, type the app name.</span></span>
    
    <span data-ttu-id="4cbdc-121">b.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-121">b.</span></span> <span data-ttu-id="4cbdc-122">In the **Subscription** box, type the name of the subscription.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-122">In the **Subscription** box, type the name of the subscription.</span></span>

    <span data-ttu-id="4cbdc-123">c.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-123">c.</span></span> <span data-ttu-id="4cbdc-124">Under **Resource Group**, click **Create new**, and then type the name of the resource group.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-124">Under **Resource Group**, click **Create new**, and then type the name of the resource group.</span></span>

    <span data-ttu-id="4cbdc-125">d.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-125">d.</span></span> <span data-ttu-id="4cbdc-126">In the **Hosting Plan** box, type **Consumption Plan**.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-126">In the **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="4cbdc-127">e.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-127">e.</span></span> <span data-ttu-id="4cbdc-128">In the **Location** box, type the location.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-128">In the **Location** box, type the location.</span></span>

    <span data-ttu-id="4cbdc-129">f.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-129">f.</span></span> <span data-ttu-id="4cbdc-130">Under **Storage account**, select an existing storage account or create a new storage account.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="4cbdc-131">A storage account is used internally for the function.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-131">A storage account is used internally for the function.</span></span>

    ![Enter new Function App configuration data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="4cbdc-133">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-133">Click **Create**.</span></span>  
    <span data-ttu-id="4cbdc-134">The function app is created.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-134">The function app is created.</span></span>

8. <span data-ttu-id="4cbdc-135">In the left pane, click **More services**, and then do the following:</span><span class="sxs-lookup"><span data-stu-id="4cbdc-135">In the left pane, click **More services**, and then do the following:</span></span>
    
    <span data-ttu-id="4cbdc-136">a.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-136">a.</span></span> <span data-ttu-id="4cbdc-137">In the **Filter** box, type **App services**.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-137">In the **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="4cbdc-138">b.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-138">b.</span></span> <span data-ttu-id="4cbdc-139">Click **App Services**.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-139">Click **App Services**.</span></span> 

    !["More services" link in the left pane](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="4cbdc-141">In the list of app services, click the name of the function app.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-141">In the list of app services, click the name of the function app.</span></span>  
    <span data-ttu-id="4cbdc-142">The function app page opens.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-142">The function app page opens.</span></span>

10. <span data-ttu-id="4cbdc-143">In the left pane, click **New Function**, and then do the following:</span><span class="sxs-lookup"><span data-stu-id="4cbdc-143">In the left pane, click **New Function**, and then do the following:</span></span> 

    <span data-ttu-id="4cbdc-144">a.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-144">a.</span></span> <span data-ttu-id="4cbdc-145">In the **Language** list, select **C#**.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-145">In the **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="4cbdc-146">b.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-146">b.</span></span> <span data-ttu-id="4cbdc-147">In the array of template tiles, select **QueueTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-147">In the array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="4cbdc-148">c.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-148">c.</span></span> <span data-ttu-id="4cbdc-149">In the **Name your function** box, type a name for your function.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-149">In the **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="4cbdc-150">d.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-150">d.</span></span> <span data-ttu-id="4cbdc-151">In the **Queue name** box, type your data-transformation job definition name.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-151">In the **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="4cbdc-152">e.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-152">e.</span></span> <span data-ttu-id="4cbdc-153">Under **Storage account connection**, click **new**, and then select the account that corresponds to the data-transformation job.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-153">Under **Storage account connection**, click **new**, and then select the account that corresponds to the data-transformation job.</span></span>  
        <span data-ttu-id="4cbdc-154">Make a note of the connection name.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-154">Make a note of the connection name.</span></span> <span data-ttu-id="4cbdc-155">The name is required later in the Azure function.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-155">The name is required later in the Azure function.</span></span>

       ![Create a new C# function](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="4cbdc-157">f.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-157">f.</span></span> <span data-ttu-id="4cbdc-158">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-158">Click **Create**.</span></span>  
    <span data-ttu-id="4cbdc-159">The **Function** window opens.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-159">The **Function** window opens.</span></span>

11. <span data-ttu-id="4cbdc-160">In the **Function** window, run _.csx_ file, and then do the following:</span><span class="sxs-lookup"><span data-stu-id="4cbdc-160">In the **Function** window, run _.csx_ file, and then do the following:</span></span>

    <span data-ttu-id="4cbdc-161">a.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-161">a.</span></span> <span data-ttu-id="4cbdc-162">Paste the following code:</span><span class="sxs-lookup"><span data-stu-id="4cbdc-162">Paste the following code:</span></span>

    ```
    using System;
    using System.Configuration;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Queue;
    using Microsoft.WindowsAzure.Storage;
    using System.Collections.Generic;
    using System.Linq;

    public static void Run(QueueItem myQueueItem, TraceWriter log)
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["STORAGE_CONNECTIONNAME"]);

        string storageAccUriEndswith = "windows.net/";
        string uri = myQueueItem.TargetLocation.Replace("%20", " ");
        log.Info($"Blob Uri: {uri}");

        // Remove storage account uri string
        uri = uri.Substring(uri.IndexOf(storageAccUriEndswith) + storageAccUriEndswith.Length);

        string containerName = uri.Substring(0, uri.IndexOf("/")); 

        // Remove container name string
        uri = uri.Substring(containerName.Length + 1);

        // Current blob path
        string blobName = uri; 

        string volumeName = uri.Substring(containerName.Length + 1);
        volumeName = uri.Substring(0, uri.IndexOf("/"));

        // Remove volume name string
        uri = uri.Substring(volumeName.Length + 1);

        string newContainerName = uri.Substring(0, uri.IndexOf("/")).ToLower();
        string newBlobName = uri.Substring(newContainerName.Length + 1);

        log.Info($"Container name: {containerName}");
        log.Info($"Volume name: {volumeName}");
        log.Info($"New container name: {newContainerName}");

        log.Info($"Blob name: {blobName}");
        log.Info($"New blob name: {newBlobName}");

        // Create the blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Container reference
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlobContainer newContainer = blobClient.GetContainerReference(newContainerName);
        newContainer.CreateIfNotExists();

        if(!container.Exists())
        {
            log.Info($"Container - {containerName} not exists");
            return;
        }

        if(!newContainer.Exists())
        {
            log.Info($"Container - {newContainerName} not exists");
            return;
        }

        CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
        if (!blob.Exists())
        {
            // Skip to copy the blob to new container, if source blob doesn't exist
            log.Info($"The specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy to new container
            blob.DeleteIfExists();
            log.Info($"Blob file path renamed completed successfully");
        }
        else
        {
            log.Info($"Blob file path renamed already done");
            // Delete old blob, if already exists.
            blob.DeleteIfExists();
        }
    }

    public class QueueItem
    {
        public string SourceLocation {get;set;}
        public long SizeInBytes {get;set;}
        public string Status {get;set;}
        public string JobID {get;set;}
        public string TargetLocation {get; set;}
    }

    ```

    <span data-ttu-id="4cbdc-163">b.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-163">b.</span></span> <span data-ttu-id="4cbdc-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span><span class="sxs-lookup"><span data-stu-id="4cbdc-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="4cbdc-165">c.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-165">c.</span></span> <span data-ttu-id="4cbdc-166">At the top left, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-166">At the top left, click **Save**.</span></span>

    ![Save function](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="4cbdc-168">To complete the function, add one more file by doing the following:</span><span class="sxs-lookup"><span data-stu-id="4cbdc-168">To complete the function, add one more file by doing the following:</span></span>

    <span data-ttu-id="4cbdc-169">a.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-169">a.</span></span> <span data-ttu-id="4cbdc-170">Click **View files**.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-170">Click **View files**.</span></span>

       ![The "View files" link](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="4cbdc-172">b.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-172">b.</span></span> <span data-ttu-id="4cbdc-173">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-173">Click **Add**.</span></span>
    
    <span data-ttu-id="4cbdc-174">c.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-174">c.</span></span> <span data-ttu-id="4cbdc-175">Type **project.json**, and then press Enter.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="4cbdc-176">d.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-176">d.</span></span> <span data-ttu-id="4cbdc-177">In the **project.json** file, paste the following code:</span><span class="sxs-lookup"><span data-stu-id="4cbdc-177">In the **project.json** file, paste the following code:</span></span>

    ```
    {
    "frameworks": {
        "net46":{
        "dependencies": {
            "windowsazure.storage": "8.1.1"
        }
        }
    }
    }

    ```

    <span data-ttu-id="4cbdc-178">e.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-178">e.</span></span> <span data-ttu-id="4cbdc-179">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-179">Click **Save**.</span></span>

<span data-ttu-id="4cbdc-180">You have created an Azure function.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-180">You have created an Azure function.</span></span> <span data-ttu-id="4cbdc-181">This function is triggered each time a new blob is generated by the data-transformation job.</span><span class="sxs-lookup"><span data-stu-id="4cbdc-181">This function is triggered each time a new blob is generated by the data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cbdc-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="4cbdc-182">Next steps</span></span>

[<span data-ttu-id="4cbdc-183">Use StorSimple Data Manager UI to transform your data</span><span class="sxs-lookup"><span data-stu-id="4cbdc-183">Use StorSimple Data Manager UI to transform your data</span></span>](storsimple-data-manager-ui.md)








