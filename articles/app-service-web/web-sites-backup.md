---
title: Back up your app in Azure
description: Learn how to create backups of your apps in Azure App Service.
services: app-service
documentationcenter: ''
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 6223b6bd-84ec-48df-943f-461d84605694
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: d52d733e46baf2b811aa20623e27ee1856d0bc49
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551113"
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="2119e-103">Back up your app in Azure</span><span class="sxs-lookup"><span data-stu-id="2119e-103">Back up your app in Azure</span></span>
<span data-ttu-id="2119e-104">The Backup and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or automatically.</span><span class="sxs-lookup"><span data-stu-id="2119e-104">The Backup and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or automatically.</span></span> <span data-ttu-id="2119e-105">You can restore your app to a previous state, or create a new app based on one of your original app's backups.</span><span class="sxs-lookup"><span data-stu-id="2119e-105">You can restore your app to a previous state, or create a new app based on one of your original app's backups.</span></span> 

<span data-ttu-id="2119e-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="2119e-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="2119e-107">What gets backed up</span><span class="sxs-lookup"><span data-stu-id="2119e-107">What gets backed up</span></span>
<span data-ttu-id="2119e-108">App Service can back up the following information:</span><span class="sxs-lookup"><span data-stu-id="2119e-108">App Service can back up the following information:</span></span>

* <span data-ttu-id="2119e-109">App configuration</span><span class="sxs-lookup"><span data-stu-id="2119e-109">App configuration</span></span>
* <span data-ttu-id="2119e-110">File content</span><span class="sxs-lookup"><span data-stu-id="2119e-110">File content</span></span>
* <span data-ttu-id="2119e-111">Any Azure SQL Databases or Azure MySQL (ClearDB) databases connected to your app (you can choose which ones to include in the backup)</span><span class="sxs-lookup"><span data-stu-id="2119e-111">Any Azure SQL Databases or Azure MySQL (ClearDB) databases connected to your app (you can choose which ones to include in the backup)</span></span>

<span data-ttu-id="2119e-112">This information is backed up to the Azure storage account and container that you specify.</span><span class="sxs-lookup"><span data-stu-id="2119e-112">This information is backed up to the Azure storage account and container that you specify.</span></span> 

> [!NOTE]
> <span data-ttu-id="2119e-113">Each backup is a complete offline copy of your app, not an incremental update.</span><span class="sxs-lookup"><span data-stu-id="2119e-113">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
> 
> 

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="2119e-114">Requirements and restrictions</span><span class="sxs-lookup"><span data-stu-id="2119e-114">Requirements and restrictions</span></span>
* <span data-ttu-id="2119e-115">The Backup and Restore feature requires the App Service plan to be in the **Standard** tier or higher.</span><span class="sxs-lookup"><span data-stu-id="2119e-115">The Backup and Restore feature requires the App Service plan to be in the **Standard** tier or higher.</span></span> <span data-ttu-id="2119e-116">For more information about scaling your App Service plan to use a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="2119e-116">For more information about scaling your App Service plan to use a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="2119e-117">Note that **Premium** tier allows a greater number of daily backups than **Standard** tier.</span><span class="sxs-lookup"><span data-stu-id="2119e-117">Note that **Premium** tier allows a greater number of daily backups than **Standard** tier.</span></span>
* <span data-ttu-id="2119e-118">You need an Azure storage account and container in the same subscription as the app that you want to back up.</span><span class="sxs-lookup"><span data-stu-id="2119e-118">You need an Azure storage account and container in the same subscription as the app that you want to back up.</span></span> <span data-ttu-id="2119e-119">For more information on Azure storage accounts, see the [links](#moreaboutstorage) at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="2119e-119">For more information on Azure storage accounts, see the [links](#moreaboutstorage) at the end of this article.</span></span>
* <span data-ttu-id="2119e-120">Backups can be up to 10GB of app and database content.</span><span class="sxs-lookup"><span data-stu-id="2119e-120">Backups can be up to 10GB of app and database content.</span></span> <span data-ttu-id="2119e-121">You will get an error if the backup size exceeds this limit.</span><span class="sxs-lookup"><span data-stu-id="2119e-121">You will get an error if the backup size exceeds this limit.</span></span> 

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="2119e-122">Create a manual backup</span><span class="sxs-lookup"><span data-stu-id="2119e-122">Create a manual backup</span></span>
1. <span data-ttu-id="2119e-123">In the [Azure Portal](https://portal.azure.com), navigate to your app's blade, select **Settings**, then **Backups**.</span><span class="sxs-lookup"><span data-stu-id="2119e-123">In the [Azure Portal](https://portal.azure.com), navigate to your app's blade, select **Settings**, then **Backups**.</span></span> <span data-ttu-id="2119e-124">The **Backups** blade will be displayed.</span><span class="sxs-lookup"><span data-stu-id="2119e-124">The **Backups** blade will be displayed.</span></span>
   
    ![Backups page][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="2119e-126">If you see the message below, click it to upgrade your App Service plan before you can proceed with backups.</span><span class="sxs-lookup"><span data-stu-id="2119e-126">If you see the message below, click it to upgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="2119e-127">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="2119e-127">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="2119e-128">![Choose storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-backup/01UpgradePlan.png)</span><span class="sxs-lookup"><span data-stu-id="2119e-128">![Choose storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-backup/01UpgradePlan.png)</span></span>
   > 
   > 
2. <span data-ttu-id="2119e-129">In the **Backups** blade, click **Storage: Not configured** to configure a storage account.</span><span class="sxs-lookup"><span data-stu-id="2119e-129">In the **Backups** blade, click **Storage: Not configured** to configure a storage account.</span></span>
   
    ![Choose storage account][ChooseStorageAccount]
3. <span data-ttu-id="2119e-131">Choose your backup destination by selecting a **Storage Account** and **Container**.</span><span class="sxs-lookup"><span data-stu-id="2119e-131">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="2119e-132">The storage account must belong to the same subscription as the app you want to back up.</span><span class="sxs-lookup"><span data-stu-id="2119e-132">The storage account must belong to the same subscription as the app you want to back up.</span></span> <span data-ttu-id="2119e-133">If you wish, you can create a new storage account or a new container in the respective blades.</span><span class="sxs-lookup"><span data-stu-id="2119e-133">If you wish, you can create a new storage account or a new container in the respective blades.</span></span> <span data-ttu-id="2119e-134">When you're done, click **Select**.</span><span class="sxs-lookup"><span data-stu-id="2119e-134">When you're done, click **Select**.</span></span>
   
    ![Choose storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-backup/02ChooseStorageAccount1.png)
4. <span data-ttu-id="2119e-136">In the **Configure Backup Settings** blade that is still left open, click **Database Settings**, then select the databases you want to include in the backups (SQL database or MySQL), then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2119e-136">In the **Configure Backup Settings** blade that is still left open, click **Database Settings**, then select the databases you want to include in the backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Choose storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-backup/03ConfigureDatabase.png)
   
   > [!NOTE]
   > <span data-ttu-id="2119e-138">For a database to appear in this list, its connection string must exist in the **Connection strings** section of the **Application settings** blade for your app.</span><span class="sxs-lookup"><span data-stu-id="2119e-138">For a database to appear in this list, its connection string must exist in the **Connection strings** section of the **Application settings** blade for your app.</span></span>
   > 
   > 
5. <span data-ttu-id="2119e-139">In the **Configure Backup Settings** blade, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="2119e-139">In the **Configure Backup Settings** blade, click **Save**.</span></span>    
6. <span data-ttu-id="2119e-140">In the command bar of the **Backups** blade, click **Backup Now**.</span><span class="sxs-lookup"><span data-stu-id="2119e-140">In the command bar of the **Backups** blade, click **Backup Now**.</span></span>
   
    ![BackUpNow button][BackUpNow]
   
    <span data-ttu-id="2119e-142">You will see a progress message during the backup process.</span><span class="sxs-lookup"><span data-stu-id="2119e-142">You will see a progress message during the backup process.</span></span>

<span data-ttu-id="2119e-143">After you have configured a storage account and container for backups, you can make a manual backup at any time.</span><span class="sxs-lookup"><span data-stu-id="2119e-143">After you have configured a storage account and container for backups, you can make a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="2119e-144">Configure automated backups</span><span class="sxs-lookup"><span data-stu-id="2119e-144">Configure automated backups</span></span>
1. <span data-ttu-id="2119e-145">In the **Backups** blade, click **Schedule: Not configured**.</span><span class="sxs-lookup"><span data-stu-id="2119e-145">In the **Backups** blade, click **Schedule: Not configured**.</span></span> 
   
    ![Choose storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-backup/05ScheduleBackup.png)
2. <span data-ttu-id="2119e-147">On the **Backup Schedule Settings** blade, set **Scheduled Backup** to **On**, then configure the backup schedule as desired and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2119e-147">On the **Backup Schedule Settings** blade, set **Scheduled Backup** to **On**, then configure the backup schedule as desired and click **OK**.</span></span>
   
    ![Enable automated backups][SetAutomatedBackupOn]
3. <span data-ttu-id="2119e-149">In the **Configure Backup Settings** blade that is still left open, click **Storage Settings**, then choose your backup destination by selecting a **Storage Account** and **Container**.</span><span class="sxs-lookup"><span data-stu-id="2119e-149">In the **Configure Backup Settings** blade that is still left open, click **Storage Settings**, then choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="2119e-150">The storage account must belong to the same subscription as the app you want to back up.</span><span class="sxs-lookup"><span data-stu-id="2119e-150">The storage account must belong to the same subscription as the app you want to back up.</span></span> <span data-ttu-id="2119e-151">If you wish, you can create a new storage account or a new container in the respective blades.</span><span class="sxs-lookup"><span data-stu-id="2119e-151">If you wish, you can create a new storage account or a new container in the respective blades.</span></span> <span data-ttu-id="2119e-152">When you're done, click **Select**.</span><span class="sxs-lookup"><span data-stu-id="2119e-152">When you're done, click **Select**.</span></span>
   
    ![Choose storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-backup/02ChooseStorageAccount1.png)
4. <span data-ttu-id="2119e-154">In the **Configure Backup Settings** blade, click **Database Settings**, then select the databases you want to include in the backups (SQL database or MySQL), then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2119e-154">In the **Configure Backup Settings** blade, click **Database Settings**, then select the databases you want to include in the backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Choose storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-backup/03ConfigureDatabase.png)
   
   > [!NOTE]
   > <span data-ttu-id="2119e-156">For a database to appear in this list, its connection string must exist in the **Connection strings** section of the **Application settings** blade for your app.</span><span class="sxs-lookup"><span data-stu-id="2119e-156">For a database to appear in this list, its connection string must exist in the **Connection strings** section of the **Application settings** blade for your app.</span></span>
   > 
   > 
5. <span data-ttu-id="2119e-157">In the **Configure Backup Settings** blade, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="2119e-157">In the **Configure Backup Settings** blade, click **Save**.</span></span>    

<a name="partialbackups"></a>

## <a name="backup-just-part-of-your-app"></a><span data-ttu-id="2119e-158">Backup just part of your app</span><span class="sxs-lookup"><span data-stu-id="2119e-158">Backup just part of your app</span></span>
<span data-ttu-id="2119e-159">Sometimes you don't want to backup everything on your app.</span><span class="sxs-lookup"><span data-stu-id="2119e-159">Sometimes you don't want to backup everything on your app.</span></span> <span data-ttu-id="2119e-160">Here are a few examples:</span><span class="sxs-lookup"><span data-stu-id="2119e-160">Here are a few examples:</span></span>

* <span data-ttu-id="2119e-161">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span><span class="sxs-lookup"><span data-stu-id="2119e-161">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="2119e-162">Your app has over 10GB of content (that's the max amount you can backup at a time).</span><span class="sxs-lookup"><span data-stu-id="2119e-162">Your app has over 10GB of content (that's the max amount you can backup at a time).</span></span>
* <span data-ttu-id="2119e-163">You don't want to back up the log files.</span><span class="sxs-lookup"><span data-stu-id="2119e-163">You don't want to back up the log files.</span></span>

<span data-ttu-id="2119e-164">Partial backups will let you choose exactly which files you want to back up.</span><span class="sxs-lookup"><span data-stu-id="2119e-164">Partial backups will let you choose exactly which files you want to back up.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="2119e-165">Exclude files from your backup</span><span class="sxs-lookup"><span data-stu-id="2119e-165">Exclude files from your backup</span></span>
<span data-ttu-id="2119e-166">To exclude files and folders from your backups, create a `_backup.filter` file in the D:\home\site\wwwroot folder of your app and specify the list of files and folders you want to exclude in there.</span><span class="sxs-lookup"><span data-stu-id="2119e-166">To exclude files and folders from your backups, create a `_backup.filter` file in the D:\home\site\wwwroot folder of your app and specify the list of files and folders you want to exclude in there.</span></span> <span data-ttu-id="2119e-167">An easy way to access this is through the [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="2119e-167">An easy way to access this is through the [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> 

<span data-ttu-id="2119e-168">Suppose you have an app that contains log files and static images from past years that are never going to change.</span><span class="sxs-lookup"><span data-stu-id="2119e-168">Suppose you have an app that contains log files and static images from past years that are never going to change.</span></span> <span data-ttu-id="2119e-169">You already have a full backup of the app that includes the old images.</span><span class="sxs-lookup"><span data-stu-id="2119e-169">You already have a full backup of the app that includes the old images.</span></span> <span data-ttu-id="2119e-170">Now you want to backup the app every day, but you don't want to pay for storing log files or the static image files that never change.</span><span class="sxs-lookup"><span data-stu-id="2119e-170">Now you want to backup the app every day, but you don't want to pay for storing log files or the static image files that never change.</span></span>

<span data-ttu-id="2119e-171">![Logs Folder][LogsFolder]
![Images Folder][ImagesFolder]</span><span class="sxs-lookup"><span data-stu-id="2119e-171">![Logs Folder][LogsFolder]
![Images Folder][ImagesFolder]</span></span>

<span data-ttu-id="2119e-172">The below steps show how you would exclude these files from the backup.</span><span class="sxs-lookup"><span data-stu-id="2119e-172">The below steps show how you would exclude these files from the backup.</span></span>

1. <span data-ttu-id="2119e-173">Go to `http://{yourapp}.scm.azurewebsites.net/DebugConsole` and identify the folders that you want to exclude from your backups.</span><span class="sxs-lookup"><span data-stu-id="2119e-173">Go to `http://{yourapp}.scm.azurewebsites.net/DebugConsole` and identify the folders that you want to exclude from your backups.</span></span> <span data-ttu-id="2119e-174">In this example, you would want to exclude the following files and folders shown in that UI:</span><span class="sxs-lookup"><span data-stu-id="2119e-174">In this example, you would want to exclude the following files and folders shown in that UI:</span></span>
   
        D:\home\site\wwwroot\Logs
        D:\home\LogFiles
        D:\home\site\wwwroot\Images\2013
        D:\home\site\wwwroot\Images\2014
        D:\home\site\wwwroot\Images\brand.png
   
    [AZURE.NOTE] <span data-ttu-id="2119e-175">The last line shows that you can exclude individuals files as well as folders.</span><span class="sxs-lookup"><span data-stu-id="2119e-175">The last line shows that you can exclude individuals files as well as folders.</span></span>
2. <span data-ttu-id="2119e-176">Create a file called `_backup.filter` and put the list above in the file, but remove `D:\home`.</span><span class="sxs-lookup"><span data-stu-id="2119e-176">Create a file called `_backup.filter` and put the list above in the file, but remove `D:\home`.</span></span> <span data-ttu-id="2119e-177">List one directory or file per line.</span><span class="sxs-lookup"><span data-stu-id="2119e-177">List one directory or file per line.</span></span> <span data-ttu-id="2119e-178">So the content of the file should be:</span><span class="sxs-lookup"><span data-stu-id="2119e-178">So the content of the file should be:</span></span>
   
    <span data-ttu-id="2119e-179">\site\wwwroot\Logs  \LogFiles  \site\wwwroot\Images\2013  \site\wwwroot\Images\2014  \site\wwwroot\Images\brand.png</span><span class="sxs-lookup"><span data-stu-id="2119e-179">\site\wwwroot\Logs  \LogFiles  \site\wwwroot\Images\2013  \site\wwwroot\Images\2014  \site\wwwroot\Images\brand.png</span></span>
3. <span data-ttu-id="2119e-180">Upload this file to the `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span><span class="sxs-lookup"><span data-stu-id="2119e-180">Upload this file to the `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="2119e-181">If you wish, you can create the file directly in `http://{yourapp}.scm.azurewebsites.net/DebugConsole` and insert the content there.</span><span class="sxs-lookup"><span data-stu-id="2119e-181">If you wish, you can create the file directly in `http://{yourapp}.scm.azurewebsites.net/DebugConsole` and insert the content there.</span></span>
4. <span data-ttu-id="2119e-182">Run backups the same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="2119e-182">Run backups the same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span>

<span data-ttu-id="2119e-183">Now, any files and folders that are specified in `_backup.filter` will be excluded from the backup.</span><span class="sxs-lookup"><span data-stu-id="2119e-183">Now, any files and folders that are specified in `_backup.filter` will be excluded from the backup.</span></span> <span data-ttu-id="2119e-184">In this example, the log files and the 2013 and 2014 image files will no longer be backed up, as well as brand.png.</span><span class="sxs-lookup"><span data-stu-id="2119e-184">In this example, the log files and the 2013 and 2014 image files will no longer be backed up, as well as brand.png.</span></span>

> [!NOTE]
> <span data-ttu-id="2119e-185">You restore partial backups of your site the same way you would [restore a regular backup](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="2119e-185">You restore partial backups of your site the same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="2119e-186">The restore process will do the right thing.</span><span class="sxs-lookup"><span data-stu-id="2119e-186">The restore process will do the right thing.</span></span>
> 
> <span data-ttu-id="2119e-187">When a full backup is restored, all content on the site is replaced with whatever is in the backup.</span><span class="sxs-lookup"><span data-stu-id="2119e-187">When a full backup is restored, all content on the site is replaced with whatever is in the backup.</span></span> <span data-ttu-id="2119e-188">If a file is on the site but not in the backup it gets deleted.</span><span class="sxs-lookup"><span data-stu-id="2119e-188">If a file is on the site but not in the backup it gets deleted.</span></span> <span data-ttu-id="2119e-189">But when a partial backup is restored, any content that is located in one of the blacklisted directories, or any blacklisted file, is left as is.</span><span class="sxs-lookup"><span data-stu-id="2119e-189">But when a partial backup is restored, any content that is located in one of the blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 
> 

<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="2119e-190">How backups are stored</span><span class="sxs-lookup"><span data-stu-id="2119e-190">How backups are stored</span></span>
<span data-ttu-id="2119e-191">After you have made one or more backups for your app, the backups will be visible on the **Containers** blade of your storage account, as well as your app.</span><span class="sxs-lookup"><span data-stu-id="2119e-191">After you have made one or more backups for your app, the backups will be visible on the **Containers** blade of your storage account, as well as your app.</span></span> <span data-ttu-id="2119e-192">In the storage account, each backup consists of a .zip file that contains the backup data and an .xml file that contains a manifest of the .zip file contents.</span><span class="sxs-lookup"><span data-stu-id="2119e-192">In the storage account, each backup consists of a .zip file that contains the backup data and an .xml file that contains a manifest of the .zip file contents.</span></span> <span data-ttu-id="2119e-193">You can unzip and browse these files if you want to access your backups without actually performing an app restore.</span><span class="sxs-lookup"><span data-stu-id="2119e-193">You can unzip and browse these files if you want to access your backups without actually performing an app restore.</span></span>

<span data-ttu-id="2119e-194">The database backup for the app is stored in the root of the .zip file.</span><span class="sxs-lookup"><span data-stu-id="2119e-194">The database backup for the app is stored in the root of the .zip file.</span></span> <span data-ttu-id="2119e-195">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span><span class="sxs-lookup"><span data-stu-id="2119e-195">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="2119e-196">To create a new SQL database based on the BACPAC export, see [Import a BACPAC File to Create a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span><span class="sxs-lookup"><span data-stu-id="2119e-196">To create a new SQL database based on the BACPAC export, see [Import a BACPAC File to Create a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="2119e-197">Altering any of the files in your **websitebackups** container can cause the backup to become invalid and therefore non-restorable.</span><span class="sxs-lookup"><span data-stu-id="2119e-197">Altering any of the files in your **websitebackups** container can cause the backup to become invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="2119e-198">Next Steps</span><span class="sxs-lookup"><span data-stu-id="2119e-198">Next Steps</span></span>
<span data-ttu-id="2119e-199">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="2119e-199">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="2119e-200">You can also backup and restore App Service apps using REST API (see [Use REST to back up and restore App Service apps](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="2119e-200">You can also backup and restore App Service apps using REST API (see [Use REST to back up and restore App Service apps](websites-csm-backup.md)).</span></span>

> [!NOTE]
> <span data-ttu-id="2119e-201">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="2119e-201">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="2119e-202">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="2119e-202">No credit cards required; no commitments.</span></span>
> 
> 

<!-- IMAGES -->
[ChooseBackupsPage]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-backup/01ChooseBackupsPage.png
[ChooseStorageAccount]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-backup/02ChooseStorageAccount.png
[IncludedDatabases]: ./media/web-sites-backup/03IncludedDatabases.png
[BackUpNow]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-backup/04BackUpNow.png
[BackupProgress]: ./media/web-sites-backup/05BackupProgress.png
[SetAutomatedBackupOn]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-backup/06SetAutomatedBackupOn.png
[Frequency]: ./media/web-sites-backup/07Frequency.png
[StartDate]: ./media/web-sites-backup/08StartDate.png
[StartTime]: ./media/web-sites-backup/09StartTime.png
[SaveIcon]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-backup/11Images.png
[LogsFolder]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-backup/13GhostUpgradeWarning.png















