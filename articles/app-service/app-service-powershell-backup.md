---
title: Use PowerShell to back up and restore App Service apps
description: Learn how to use PowerShell to back up and restore an app in Azure App Service
services: app-service
documentationcenter: ''
author: NKing92
manager: erikre
editor: ''
ms.assetid: 7ea8661e-aefb-4823-9626-6bff980cdebf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: 7aa071dedf41f3d06068e622881e71aaabc00c3b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550109"
---
# <a name="use-powershell-to-back-up-and-restore-app-service-apps"></a><span data-ttu-id="11445-103">Use PowerShell to back up and restore App Service apps</span><span class="sxs-lookup"><span data-stu-id="11445-103">Use PowerShell to back up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [PowerShell](app-service-powershell-backup.md)
> * [REST API](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="11445-106">Learn how to use Azure PowerShell to back up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="11445-106">Learn how to use Azure PowerShell to back up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="11445-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="11445-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11445-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="11445-108">Prerequisites</span></span>
<span data-ttu-id="11445-109">To use PowerShell to manage your app backups, you need the following:</span><span class="sxs-lookup"><span data-stu-id="11445-109">To use PowerShell to manage your app backups, you need the following:</span></span>

* <span data-ttu-id="11445-110">**A SAS URL** that allows read and write access to an Azure Storage container.</span><span class="sxs-lookup"><span data-stu-id="11445-110">**A SAS URL** that allows read and write access to an Azure Storage container.</span></span> <span data-ttu-id="11445-111">See [Understanding the SAS model](../storage/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span><span class="sxs-lookup"><span data-stu-id="11445-111">See [Understanding the SAS model](../storage/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="11445-112">See [Using Azure PowerShell with Azure Storage](../storage/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="11445-112">See [Using Azure PowerShell with Azure Storage](../storage/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="11445-113">**A database connection string** if you want to back up a database along with your web app.</span><span class="sxs-lookup"><span data-stu-id="11445-113">**A database connection string** if you want to back up a database along with your web app.</span></span>

### <a name="how-to-generate-a-sas-url-to-use-with-the-web-app-backup-cmdlets"></a><span data-ttu-id="11445-114">How to generate a SAS URL to use with the web app backup cmdlets</span><span class="sxs-lookup"><span data-stu-id="11445-114">How to generate a SAS URL to use with the web app backup cmdlets</span></span>
<span data-ttu-id="11445-115">A SAS URL can be generated with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="11445-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="11445-116">Here is an example of how to generate one that can be used with the cmdlets discussed in this article.</span><span class="sxs-lookup"><span data-stu-id="11445-116">Here is an example of how to generate one that can be used with the cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure to select the appropriate key. Here we select the first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="11445-117">Install Azure PowerShell 1.3.2 or greater</span><span class="sxs-lookup"><span data-stu-id="11445-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="11445-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azureps-cmdlets-docs) for instructions on installing and using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="11445-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azureps-cmdlets-docs) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="11445-119">Create a backup</span><span class="sxs-lookup"><span data-stu-id="11445-119">Create a backup</span></span>
<span data-ttu-id="11445-120">Use the New-AzureRmWebAppBackup cmdlet to create a backup of a web app.</span><span class="sxs-lookup"><span data-stu-id="11445-120">Use the New-AzureRmWebAppBackup cmdlet to create a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="11445-121">This creates a backup with an automatically generated name.</span><span class="sxs-lookup"><span data-stu-id="11445-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="11445-122">If you would like to provide a name for your backup, use the BackupName optional parameter.</span><span class="sxs-lookup"><span data-stu-id="11445-122">If you would like to provide a name for your backup, use the BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="11445-123">To include a database in the backup, first create a database backup setting using the New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in the Databases parameter of the New-AzureRmWebAppBackup cmdlet.</span><span class="sxs-lookup"><span data-stu-id="11445-123">To include a database in the backup, first create a database backup setting using the New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in the Databases parameter of the New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="11445-124">The Databases parameter accepts an array of database settings, allowing you to back up more than one database.</span><span class="sxs-lookup"><span data-stu-id="11445-124">The Databases parameter accepts an array of database settings, allowing you to back up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="11445-125">Get backups</span><span class="sxs-lookup"><span data-stu-id="11445-125">Get backups</span></span>
<span data-ttu-id="11445-126">The Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span><span class="sxs-lookup"><span data-stu-id="11445-126">The Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="11445-127">You must supply the name of the web app and its resource group.</span><span class="sxs-lookup"><span data-stu-id="11445-127">You must supply the name of the web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="11445-128">To get a specific backup, use the Get-AzureRmWebAppBackup cmdlet.</span><span class="sxs-lookup"><span data-stu-id="11445-128">To get a specific backup, use the Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="11445-129">You can also pipe a web app object into any of the backup management cmdlets for convenience.</span><span class="sxs-lookup"><span data-stu-id="11445-129">You can also pipe a web app object into any of the backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="11445-130">Schedule automatic backups</span><span class="sxs-lookup"><span data-stu-id="11445-130">Schedule automatic backups</span></span>
<span data-ttu-id="11445-131">You can schedule backups to happen automatically at a specified interval.</span><span class="sxs-lookup"><span data-stu-id="11445-131">You can schedule backups to happen automatically at a specified interval.</span></span> <span data-ttu-id="11445-132">To configure a backup schedule, use the Edit-AzureRmWebAppBackupConfiguration cmdlet.</span><span class="sxs-lookup"><span data-stu-id="11445-132">To configure a backup schedule, use the Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="11445-133">This cmdlet takes several parameters:</span><span class="sxs-lookup"><span data-stu-id="11445-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="11445-134">**Name** - The name of the web app.</span><span class="sxs-lookup"><span data-stu-id="11445-134">**Name** - The name of the web app.</span></span>
* <span data-ttu-id="11445-135">**ResourceGroupName** - The name of the resource group containing the web app.</span><span class="sxs-lookup"><span data-stu-id="11445-135">**ResourceGroupName** - The name of the resource group containing the web app.</span></span>
* <span data-ttu-id="11445-136">**Slot** - Optional.</span><span class="sxs-lookup"><span data-stu-id="11445-136">**Slot** - Optional.</span></span> <span data-ttu-id="11445-137">The name of the web app slot.</span><span class="sxs-lookup"><span data-stu-id="11445-137">The name of the web app slot.</span></span>
* <span data-ttu-id="11445-138">**StorageAccountUrl** - The SAS URL for the Azure Storage container used to store the backups.</span><span class="sxs-lookup"><span data-stu-id="11445-138">**StorageAccountUrl** - The SAS URL for the Azure Storage container used to store the backups.</span></span>
* <span data-ttu-id="11445-139">**FrequencyInterval** - Numeric value for how often the backups should be made.</span><span class="sxs-lookup"><span data-stu-id="11445-139">**FrequencyInterval** - Numeric value for how often the backups should be made.</span></span> <span data-ttu-id="11445-140">Must be a positive integer.</span><span class="sxs-lookup"><span data-stu-id="11445-140">Must be a positive integer.</span></span>
* <span data-ttu-id="11445-141">**FrequencyUnit** - Unit of time for how often the backups should be made.</span><span class="sxs-lookup"><span data-stu-id="11445-141">**FrequencyUnit** - Unit of time for how often the backups should be made.</span></span> <span data-ttu-id="11445-142">Options are Hour and Day.</span><span class="sxs-lookup"><span data-stu-id="11445-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="11445-143">**RetentionPeriodInDays** - How many days the automatic backups should be saved before being automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="11445-143">**RetentionPeriodInDays** - How many days the automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="11445-144">**StartTime** - Optional.</span><span class="sxs-lookup"><span data-stu-id="11445-144">**StartTime** - Optional.</span></span> <span data-ttu-id="11445-145">The time when the automatic backups should begin.</span><span class="sxs-lookup"><span data-stu-id="11445-145">The time when the automatic backups should begin.</span></span> <span data-ttu-id="11445-146">Backups begin immediately if this is null.</span><span class="sxs-lookup"><span data-stu-id="11445-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="11445-147">Must be a DateTime.</span><span class="sxs-lookup"><span data-stu-id="11445-147">Must be a DateTime.</span></span>
* <span data-ttu-id="11445-148">**Databases** - Optional.</span><span class="sxs-lookup"><span data-stu-id="11445-148">**Databases** - Optional.</span></span> <span data-ttu-id="11445-149">An array of DatabaseBackupSettings for the databases to backup.</span><span class="sxs-lookup"><span data-stu-id="11445-149">An array of DatabaseBackupSettings for the databases to backup.</span></span>
* <span data-ttu-id="11445-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span><span class="sxs-lookup"><span data-stu-id="11445-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="11445-151">Supply this if one backup should always be kept in the storage account, regardless of how old it is.</span><span class="sxs-lookup"><span data-stu-id="11445-151">Supply this if one backup should always be kept in the storage account, regardless of how old it is.</span></span>

<span data-ttu-id="11445-152">Following is an example of how to use this cmdlet.</span><span class="sxs-lookup"><span data-stu-id="11445-152">Following is an example of how to use this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="11445-153">To get the current backup schedule, use the Get-AzureRmWebAppBackupConfiguration cmdlet.</span><span class="sxs-lookup"><span data-stu-id="11445-153">To get the current backup schedule, use the Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="11445-154">This can be useful for modifying a schedule that has already been configured.</span><span class="sxs-lookup"><span data-stu-id="11445-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify the configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply the new configuration by piping it into the Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="11445-155">Restore a web app from a backup</span><span class="sxs-lookup"><span data-stu-id="11445-155">Restore a web app from a backup</span></span>
<span data-ttu-id="11445-156">To restore a web app from a backup, use the Restore-AzureRmWebAppBackup cmdlet.</span><span class="sxs-lookup"><span data-stu-id="11445-156">To restore a web app from a backup, use the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="11445-157">The easiest way to use this cmdlet is to pipe in a backup object retrieved from the Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span><span class="sxs-lookup"><span data-stu-id="11445-157">The easiest way to use this cmdlet is to pipe in a backup object retrieved from the Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="11445-158">Once you have a backup object, you can pipe it into the Restore-AzureRmWebAppBackup cmdlet.</span><span class="sxs-lookup"><span data-stu-id="11445-158">Once you have a backup object, you can pipe it into the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="11445-159">Specify the Overwrite switch parameter to indicate that you intend to overwrite the contents of your web app with the contents of the backup.</span><span class="sxs-lookup"><span data-stu-id="11445-159">Specify the Overwrite switch parameter to indicate that you intend to overwrite the contents of your web app with the contents of the backup.</span></span> <span data-ttu-id="11445-160">If the backup contains databases, those databases are restored as well.</span><span class="sxs-lookup"><span data-stu-id="11445-160">If the backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="11445-161">Following is an example of how to use the Restore-AzureRmWebAppBackup by specifying all the parameters.</span><span class="sxs-lookup"><span data-stu-id="11445-161">Following is an example of how to use the Restore-AzureRmWebAppBackup by specifying all the parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="11445-162">Delete a backup</span><span class="sxs-lookup"><span data-stu-id="11445-162">Delete a backup</span></span>
<span data-ttu-id="11445-163">To delete a backup, use the Remove-AzureRmWebAppBackup cmdlet.</span><span class="sxs-lookup"><span data-stu-id="11445-163">To delete a backup, use the Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="11445-164">This removes the backup from your storage account.</span><span class="sxs-lookup"><span data-stu-id="11445-164">This removes the backup from your storage account.</span></span> <span data-ttu-id="11445-165">Specify your app name, its resource group, and the ID of the backup you want to delete.</span><span class="sxs-lookup"><span data-stu-id="11445-165">Specify your app name, its resource group, and the ID of the backup you want to delete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="11445-166">You can also pipe a backup object into the Remove-AzureRmWebAppBackup cmdlet to delete it.</span><span class="sxs-lookup"><span data-stu-id="11445-166">You can also pipe a backup object into the Remove-AzureRmWebAppBackup cmdlet to delete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
