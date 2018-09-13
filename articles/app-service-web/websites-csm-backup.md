---
title: Use REST to back up and restore App Service apps
description: Learn how to use RESTful API calls to back up and restore an app in Azure App Service
services: app-service
documentationcenter: ''
author: NKing92
manager: erikre
editor: ''
ms.assetid: f94d0aea-edc1-43ab-9b51-ea7375859276
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: 94447cf93846967d28748115fd05102596961869
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554822"
---
# <a name="use-rest-to-back-up-and-restore-app-service-apps"></a><span data-ttu-id="03f3c-103">Use REST to back up and restore App Service apps</span><span class="sxs-lookup"><span data-stu-id="03f3c-103">Use REST to back up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [PowerShell](../app-service/app-service-powershell-backup.md)
> * [REST API](websites-csm-backup.md)
> 
> 

<span data-ttu-id="03f3c-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="03f3c-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span></span> <span data-ttu-id="03f3c-107">The backup can also contain the app’s databases.</span><span class="sxs-lookup"><span data-stu-id="03f3c-107">The backup can also contain the app’s databases.</span></span> <span data-ttu-id="03f3c-108">If the app is ever accidentally deleted, or if the app needs to be reverted to a previous version, it can be restored from any previous backup.</span><span class="sxs-lookup"><span data-stu-id="03f3c-108">If the app is ever accidentally deleted, or if the app needs to be reverted to a previous version, it can be restored from any previous backup.</span></span> <span data-ttu-id="03f3c-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span><span class="sxs-lookup"><span data-stu-id="03f3c-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span></span>

<span data-ttu-id="03f3c-110">This article explains how to backup and restore an app with RESTful API requests.</span><span class="sxs-lookup"><span data-stu-id="03f3c-110">This article explains how to backup and restore an app with RESTful API requests.</span></span> <span data-ttu-id="03f3c-111">If you would like to create and manage app backups graphically through the Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span><span class="sxs-lookup"><span data-stu-id="03f3c-111">If you would like to create and manage app backups graphically through the Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span></span>

<a name="gettingstarted"></a>

## <a name="getting-started"></a><span data-ttu-id="03f3c-112">Getting Started</span><span class="sxs-lookup"><span data-stu-id="03f3c-112">Getting Started</span></span>
<span data-ttu-id="03f3c-113">To send REST requests, you need to know your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in the **App Service** blade of the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="03f3c-113">To send REST requests, you need to know your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in the **App Service** blade of the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="03f3c-114">For the examples in this article, we are configuring the website **backuprestoreapiexamples.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="03f3c-114">For the examples in this article, we are configuring the website **backuprestoreapiexamples.azurewebsites.net**.</span></span> <span data-ttu-id="03f3c-115">It is stored in the Default-Web-WestUS resource group and is running on a subscription with the ID 00001111-2222-3333-4444-555566667777.</span><span class="sxs-lookup"><span data-stu-id="03f3c-115">It is stored in the Default-Web-WestUS resource group and is running on a subscription with the ID 00001111-2222-3333-4444-555566667777.</span></span>

![Sample Website Information][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a><span data-ttu-id="03f3c-117">Backup and restore REST API</span><span class="sxs-lookup"><span data-stu-id="03f3c-117">Backup and restore REST API</span></span>
<span data-ttu-id="03f3c-118">We will now cover several examples of how to use the REST API to backup and restore an app.</span><span class="sxs-lookup"><span data-stu-id="03f3c-118">We will now cover several examples of how to use the REST API to backup and restore an app.</span></span> <span data-ttu-id="03f3c-119">Each example includes a URL and HTTP request body.</span><span class="sxs-lookup"><span data-stu-id="03f3c-119">Each example includes a URL and HTTP request body.</span></span> <span data-ttu-id="03f3c-120">The sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span><span class="sxs-lookup"><span data-stu-id="03f3c-120">The sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span></span> <span data-ttu-id="03f3c-121">Replace the placeholders with the corresponding information for your app.</span><span class="sxs-lookup"><span data-stu-id="03f3c-121">Replace the placeholders with the corresponding information for your app.</span></span> <span data-ttu-id="03f3c-122">For reference, here is an explanation of each placeholder that appears in the example URLs.</span><span class="sxs-lookup"><span data-stu-id="03f3c-122">For reference, here is an explanation of each placeholder that appears in the example URLs.</span></span>

* <span data-ttu-id="03f3c-123">subscription-id – ID of the Azure subscription containing the app</span><span class="sxs-lookup"><span data-stu-id="03f3c-123">subscription-id – ID of the Azure subscription containing the app</span></span>
* <span data-ttu-id="03f3c-124">resource-group-name – Name of the resource group containing the app</span><span class="sxs-lookup"><span data-stu-id="03f3c-124">resource-group-name – Name of the resource group containing the app</span></span>
* <span data-ttu-id="03f3c-125">name – Name of the app</span><span class="sxs-lookup"><span data-stu-id="03f3c-125">name – Name of the app</span></span>
* <span data-ttu-id="03f3c-126">backup-id – ID of the app backup</span><span class="sxs-lookup"><span data-stu-id="03f3c-126">backup-id – ID of the app backup</span></span>

<span data-ttu-id="03f3c-127">For the complete documentation of the API, including several optional parameters that can be included in the HTTP request, see the [Azure Resource Explorer](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="03f3c-127">For the complete documentation of the API, including several optional parameters that can be included in the HTTP request, see the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a><span data-ttu-id="03f3c-128">Backup an app on demand</span><span class="sxs-lookup"><span data-stu-id="03f3c-128">Backup an app on demand</span></span>
<span data-ttu-id="03f3c-129">To back up an app immediately, send a **POST** request to **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span><span class="sxs-lookup"><span data-stu-id="03f3c-129">To back up an app immediately, send a **POST** request to **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span></span>

<span data-ttu-id="03f3c-130">Here is what the URL looks like using our example website.</span><span class="sxs-lookup"><span data-stu-id="03f3c-130">Here is what the URL looks like using our example website.</span></span> **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**

<span data-ttu-id="03f3c-131">Supply a JSON object in the body of your request to specify which storage account to use to store the backup.</span><span class="sxs-lookup"><span data-stu-id="03f3c-131">Supply a JSON object in the body of your request to specify which storage account to use to store the backup.</span></span> <span data-ttu-id="03f3c-132">The JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/storage-dotnet-shared-access-signature-part-1.md) granting write access to the Azure Storage container that holds the backup blob.</span><span class="sxs-lookup"><span data-stu-id="03f3c-132">The JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/storage-dotnet-shared-access-signature-part-1.md) granting write access to the Azure Storage container that holds the backup blob.</span></span> <span data-ttu-id="03f3c-133">If you want to back up your databases, you must also supply a list containing the names, types, and connection strings of the databases to be backed up.</span><span class="sxs-lookup"><span data-stu-id="03f3c-133">If you want to back up your databases, you must also supply a list containing the names, types, and connection strings of the databases to be backed up.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        “databases”: [
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”,
                "connectionString": "<your database connection string>"
            }
        ]
    }
}
```

<span data-ttu-id="03f3c-134">A backup of the app begins immediately when the request is received.</span><span class="sxs-lookup"><span data-stu-id="03f3c-134">A backup of the app begins immediately when the request is received.</span></span> <span data-ttu-id="03f3c-135">The backup process may take a long time to complete.</span><span class="sxs-lookup"><span data-stu-id="03f3c-135">The backup process may take a long time to complete.</span></span> <span data-ttu-id="03f3c-136">The HTTP response contains an ID that you can use in another request to see the status of the backup.</span><span class="sxs-lookup"><span data-stu-id="03f3c-136">The HTTP response contains an ID that you can use in another request to see the status of the backup.</span></span> <span data-ttu-id="03f3c-137">Here is an example of the body of the HTTP response to our backup request.</span><span class="sxs-lookup"><span data-stu-id="03f3c-137">Here is an example of the body of the HTTP response to our backup request.</span></span>

```
{
    "id": "/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples",
    "name": " backuprestoreapiexamples ",
    "type": "Microsoft.Web/sites",
    "location": "WestUS",
    "properties":    {
        "id": 1,
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        "blobName": “backup_201509291825.zip”,
        "name": "backup_201509291825",
        "status": 4,
        "sizeInBytes": 0,
        "created": "2015-09-29T18:25:26.3992707Z",
        "log": null,
        "databases": [
            {
                "databaseType": "SqlAzure",
                "name": "MyDatabase1",
                "connectionString": "<your database connection string>"
            }
        ],
        "scheduled": false,
        "correlationId": "ea730f4d-dd06-4f7f-a090-9aa09k662h36",
    }
}
```

> [!NOTE]
> Error messages can be found in the log property of the HTTP response.
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a><span data-ttu-id="03f3c-139">Schedule automatic backups</span><span class="sxs-lookup"><span data-stu-id="03f3c-139">Schedule automatic backups</span></span>
<span data-ttu-id="03f3c-140">In addition to backing up an app on demand, you can also schedule a backup to happen automatically.</span><span class="sxs-lookup"><span data-stu-id="03f3c-140">In addition to backing up an app on demand, you can also schedule a backup to happen automatically.</span></span>

### <a name="set-up-a-new-automatic-backup-schedule"></a><span data-ttu-id="03f3c-141">Set up a new automatic backup schedule</span><span class="sxs-lookup"><span data-stu-id="03f3c-141">Set up a new automatic backup schedule</span></span>
<span data-ttu-id="03f3c-142">To set up a backup schedule, send a **PUT** request to **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span><span class="sxs-lookup"><span data-stu-id="03f3c-142">To set up a backup schedule, send a **PUT** request to **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span></span>

<span data-ttu-id="03f3c-143">Here is what the URL looks like for our example website.</span><span class="sxs-lookup"><span data-stu-id="03f3c-143">Here is what the URL looks like for our example website.</span></span> **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**

<span data-ttu-id="03f3c-144">The request body must have a JSON object that specifies the backup configuration.</span><span class="sxs-lookup"><span data-stu-id="03f3c-144">The request body must have a JSON object that specifies the backup configuration.</span></span> <span data-ttu-id="03f3c-145">Here is an example with all the required parameters.</span><span class="sxs-lookup"><span data-stu-id="03f3c-145">Here is an example with all the required parameters.</span></span>

```
{
    "location": "WestUS",
    "properties": // Represents an app restore request
    {
        "backupSchedule": { // Required for automatically scheduled backups
            "frequencyInterval": "7",
            "frequencyUnit": "Day",
            "keepAtLeastOneBackup": "True",
            "retentionPeriodInDays": "10",
        },
        "enabled": "True", // Must be set to true to enable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

<span data-ttu-id="03f3c-146">This example configures the app to be automatically backed up every seven days.</span><span class="sxs-lookup"><span data-stu-id="03f3c-146">This example configures the app to be automatically backed up every seven days.</span></span> <span data-ttu-id="03f3c-147">The parameters **frequencyInterval** and **frequencyUnit** together determine how often the backups happen.</span><span class="sxs-lookup"><span data-stu-id="03f3c-147">The parameters **frequencyInterval** and **frequencyUnit** together determine how often the backups happen.</span></span> <span data-ttu-id="03f3c-148">Valid values for **frequencyUnit** are **hour** and **day**.</span><span class="sxs-lookup"><span data-stu-id="03f3c-148">Valid values for **frequencyUnit** are **hour** and **day**.</span></span> <span data-ttu-id="03f3c-149">For example, to back up an app every 12 hours, set frequencyInterval to 12 and frequencyUnit to hour.</span><span class="sxs-lookup"><span data-stu-id="03f3c-149">For example, to back up an app every 12 hours, set frequencyInterval to 12 and frequencyUnit to hour.</span></span>

<span data-ttu-id="03f3c-150">Old backups are automatically removed from the storage account.</span><span class="sxs-lookup"><span data-stu-id="03f3c-150">Old backups are automatically removed from the storage account.</span></span> <span data-ttu-id="03f3c-151">You can control how old the backups can be by setting the **retentionPeriodInDays** parameter.</span><span class="sxs-lookup"><span data-stu-id="03f3c-151">You can control how old the backups can be by setting the **retentionPeriodInDays** parameter.</span></span> <span data-ttu-id="03f3c-152">If you want to always have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** to true.</span><span class="sxs-lookup"><span data-stu-id="03f3c-152">If you want to always have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** to true.</span></span>

### <a name="get-the-automatic-backup-schedule"></a><span data-ttu-id="03f3c-153">Get the automatic backup schedule</span><span class="sxs-lookup"><span data-stu-id="03f3c-153">Get the automatic backup schedule</span></span>
<span data-ttu-id="03f3c-154">To get an app’s backup configuration, send a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span><span class="sxs-lookup"><span data-stu-id="03f3c-154">To get an app’s backup configuration, send a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span></span>

<span data-ttu-id="03f3c-155">The URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span><span class="sxs-lookup"><span data-stu-id="03f3c-155">The URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span></span>

<a name="get-backup-status"></a>

## <a name="get-the-status-of-a-backup"></a><span data-ttu-id="03f3c-156">Get the status of a backup</span><span class="sxs-lookup"><span data-stu-id="03f3c-156">Get the status of a backup</span></span>
<span data-ttu-id="03f3c-157">Depending on how large the app is, a backup may take a while to complete.</span><span class="sxs-lookup"><span data-stu-id="03f3c-157">Depending on how large the app is, a backup may take a while to complete.</span></span> <span data-ttu-id="03f3c-158">Backups might also fail, time out, or partially succeed.</span><span class="sxs-lookup"><span data-stu-id="03f3c-158">Backups might also fail, time out, or partially succeed.</span></span> <span data-ttu-id="03f3c-159">To see the status of all an app’s backups, send a **GET** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span><span class="sxs-lookup"><span data-stu-id="03f3c-159">To see the status of all an app’s backups, send a **GET** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span></span>

<span data-ttu-id="03f3c-160">To see the status of a specific backup, send a GET request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span><span class="sxs-lookup"><span data-stu-id="03f3c-160">To see the status of a specific backup, send a GET request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="03f3c-161">Here is what the URL looks like for our example website.</span><span class="sxs-lookup"><span data-stu-id="03f3c-161">Here is what the URL looks like for our example website.</span></span> **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

<span data-ttu-id="03f3c-162">The response body contains a JSON object similar to this example.</span><span class="sxs-lookup"><span data-stu-id="03f3c-162">The response body contains a JSON object similar to this example.</span></span>

```
{
    "properties":  {
        "id": 1,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl",
        "blobName": "backup_201509291734.zip",
        "name": "backup_201509291734",
        "status": 2,
        "sizeInBytes": 151973,
        "created": "2015-09-29T17:34:57.2091605",
        "scheduled": false,
        "lastRestoreTimeStamp": null,
        "finishedTimeStamp": "2015-09-29T17:35:11.3293602",
        "correlationId": "2379fc13-418a-4b9c-920d-d06e73c5028d",
        "websiteSizeInBytes": 209920
    }
}
```

<span data-ttu-id="03f3c-163">The status of a backup is an enumerated type.</span><span class="sxs-lookup"><span data-stu-id="03f3c-163">The status of a backup is an enumerated type.</span></span> <span data-ttu-id="03f3c-164">Here is every possible state.</span><span class="sxs-lookup"><span data-stu-id="03f3c-164">Here is every possible state.</span></span>

* <span data-ttu-id="03f3c-165">0 – InProgress: The backup has been started but has not yet completed.</span><span class="sxs-lookup"><span data-stu-id="03f3c-165">0 – InProgress: The backup has been started but has not yet completed.</span></span>
* <span data-ttu-id="03f3c-166">1 – Failed: The backup was unsuccessful.</span><span class="sxs-lookup"><span data-stu-id="03f3c-166">1 – Failed: The backup was unsuccessful.</span></span>
* <span data-ttu-id="03f3c-167">2 – Succeeded: The backup completed successfully.</span><span class="sxs-lookup"><span data-stu-id="03f3c-167">2 – Succeeded: The backup completed successfully.</span></span>
* <span data-ttu-id="03f3c-168">3 – TimedOut: The backup did not finish in time and was canceled.</span><span class="sxs-lookup"><span data-stu-id="03f3c-168">3 – TimedOut: The backup did not finish in time and was canceled.</span></span>
* <span data-ttu-id="03f3c-169">4 – Created: The backup request is queued but has not been started.</span><span class="sxs-lookup"><span data-stu-id="03f3c-169">4 – Created: The backup request is queued but has not been started.</span></span>
* <span data-ttu-id="03f3c-170">5 – Skipped: The backup did not proceed due to a schedule triggering too many backups.</span><span class="sxs-lookup"><span data-stu-id="03f3c-170">5 – Skipped: The backup did not proceed due to a schedule triggering too many backups.</span></span>
* <span data-ttu-id="03f3c-171">6 – PartiallySucceeded: The backup succeeded, but some files were not backed up because they could not be read.</span><span class="sxs-lookup"><span data-stu-id="03f3c-171">6 – PartiallySucceeded: The backup succeeded, but some files were not backed up because they could not be read.</span></span> <span data-ttu-id="03f3c-172">This usually happens because an exclusive lock was placed on the files.</span><span class="sxs-lookup"><span data-stu-id="03f3c-172">This usually happens because an exclusive lock was placed on the files.</span></span>
* <span data-ttu-id="03f3c-173">7 – DeleteInProgress: The backup has been requested to be deleted, but has not yet been deleted.</span><span class="sxs-lookup"><span data-stu-id="03f3c-173">7 – DeleteInProgress: The backup has been requested to be deleted, but has not yet been deleted.</span></span>
* <span data-ttu-id="03f3c-174">8 – DeleteFailed: The backup could not be deleted.</span><span class="sxs-lookup"><span data-stu-id="03f3c-174">8 – DeleteFailed: The backup could not be deleted.</span></span> <span data-ttu-id="03f3c-175">This might happen because the SAS URL that was used to create the backup has expired.</span><span class="sxs-lookup"><span data-stu-id="03f3c-175">This might happen because the SAS URL that was used to create the backup has expired.</span></span>
* <span data-ttu-id="03f3c-176">9 – Deleted: The backup was deleted successfully.</span><span class="sxs-lookup"><span data-stu-id="03f3c-176">9 – Deleted: The backup was deleted successfully.</span></span>

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a><span data-ttu-id="03f3c-177">Restore an app from a backup</span><span class="sxs-lookup"><span data-stu-id="03f3c-177">Restore an app from a backup</span></span>
<span data-ttu-id="03f3c-178">If your app has been deleted, or if you want to revert your app to a previous version, you can restore the app from a backup.</span><span class="sxs-lookup"><span data-stu-id="03f3c-178">If your app has been deleted, or if you want to revert your app to a previous version, you can restore the app from a backup.</span></span> <span data-ttu-id="03f3c-179">To invoke a restore, send a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span><span class="sxs-lookup"><span data-stu-id="03f3c-179">To invoke a restore, send a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span></span>

<span data-ttu-id="03f3c-180">Here is what the URL looks like for our example website.</span><span class="sxs-lookup"><span data-stu-id="03f3c-180">Here is what the URL looks like for our example website.</span></span> **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**

<span data-ttu-id="03f3c-181">In the request body, send a JSON object that contains the properties for the restore operation.</span><span class="sxs-lookup"><span data-stu-id="03f3c-181">In the request body, send a JSON object that contains the properties for the restore operation.</span></span> <span data-ttu-id="03f3c-182">Here is an example containing all required properties:</span><span class="sxs-lookup"><span data-stu-id="03f3c-182">Here is an example containing all required properties:</span></span>

```
{
    "location": "WestUS",
    "properties":
    {
        "blobName": "backup_201509280431.zip",
        "databases": [ // Not required unless you’re restoring databases
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”
        }],
        "overwrite": "true",
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL to storage container containing your website backup
    }
}
```

### <a name="restore-to-a-new-app"></a><span data-ttu-id="03f3c-183">Restore to a new app</span><span class="sxs-lookup"><span data-stu-id="03f3c-183">Restore to a new app</span></span>
<span data-ttu-id="03f3c-184">Sometimes you might want to create a new app when you restore a backup, instead of overwriting an already existing app.</span><span class="sxs-lookup"><span data-stu-id="03f3c-184">Sometimes you might want to create a new app when you restore a backup, instead of overwriting an already existing app.</span></span> <span data-ttu-id="03f3c-185">To do this, change the request URL to point to the new app you want to create, and change the **overwrite** property in the JSON to **false**.</span><span class="sxs-lookup"><span data-stu-id="03f3c-185">To do this, change the request URL to point to the new app you want to create, and change the **overwrite** property in the JSON to **false**.</span></span>

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a><span data-ttu-id="03f3c-186">Delete an app backup</span><span class="sxs-lookup"><span data-stu-id="03f3c-186">Delete an app backup</span></span>
<span data-ttu-id="03f3c-187">If you would like to delete a backup, send a **DELETE** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span><span class="sxs-lookup"><span data-stu-id="03f3c-187">If you would like to delete a backup, send a **DELETE** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="03f3c-188">Here is what the URL looks like for our example website.</span><span class="sxs-lookup"><span data-stu-id="03f3c-188">Here is what the URL looks like for our example website.</span></span> **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a><span data-ttu-id="03f3c-189">Manage a backup’s SAS URL</span><span class="sxs-lookup"><span data-stu-id="03f3c-189">Manage a backup’s SAS URL</span></span>
<span data-ttu-id="03f3c-190">Azure App Service will attempt to delete your backup from Azure Storage using the SAS URL that was provided when the backup was created.</span><span class="sxs-lookup"><span data-stu-id="03f3c-190">Azure App Service will attempt to delete your backup from Azure Storage using the SAS URL that was provided when the backup was created.</span></span> <span data-ttu-id="03f3c-191">If this SAS URL is no longer valid, the backup cannot be deleted through the REST API.</span><span class="sxs-lookup"><span data-stu-id="03f3c-191">If this SAS URL is no longer valid, the backup cannot be deleted through the REST API.</span></span> <span data-ttu-id="03f3c-192">However, you can update the SAS URL associated with a backup by sending a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span><span class="sxs-lookup"><span data-stu-id="03f3c-192">However, you can update the SAS URL associated with a backup by sending a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span></span>

<span data-ttu-id="03f3c-193">Here is what the URL looks like for our example website.</span><span class="sxs-lookup"><span data-stu-id="03f3c-193">Here is what the URL looks like for our example website.</span></span> **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**

<span data-ttu-id="03f3c-194">In the request body, send a JSON object that contains the new SAS URL.</span><span class="sxs-lookup"><span data-stu-id="03f3c-194">In the request body, send a JSON object that contains the new SAS URL.</span></span> <span data-ttu-id="03f3c-195">Here is an example.</span><span class="sxs-lookup"><span data-stu-id="03f3c-195">Here is an example.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> For security reasons, the SAS URL associated with a backup is not returned when sending a GET request for a specific backup. If you want to view the SAS URL associated with a backup, send a POST request to the same URL above. Include an empty JSON object in the request body. The response from the server contains all of that backup’s information, including its SAS URL.
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-csm-backup/01siteconfig.png

