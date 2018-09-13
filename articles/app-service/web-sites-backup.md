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
ms.openlocfilehash: 44b4da7c293da0643fb88cc2de21433c6ea72c5c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968439"
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="7973d-103">Back up your app in Azure</span><span class="sxs-lookup"><span data-stu-id="7973d-103">Back up your app in Azure</span></span>
<span data-ttu-id="7973d-104">The Backup and Restore feature in [Azure App Service](app-service-web-overview.md) lets you easily create app backups manually or on a schedule.</span><span class="sxs-lookup"><span data-stu-id="7973d-104">The Backup and Restore feature in [Azure App Service](app-service-web-overview.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="7973d-105">You can restore the app to a snapshot of a previous state by overwriting the existing app or restoring to another app.</span><span class="sxs-lookup"><span data-stu-id="7973d-105">You can restore the app to a snapshot of a previous state by overwriting the existing app or restoring to another app.</span></span> 

<span data-ttu-id="7973d-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="7973d-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="7973d-107">What gets backed up</span><span class="sxs-lookup"><span data-stu-id="7973d-107">What gets backed up</span></span>
<span data-ttu-id="7973d-108">App Service can back up the following information to an Azure storage account and container that you have configured your app to use.</span><span class="sxs-lookup"><span data-stu-id="7973d-108">App Service can back up the following information to an Azure storage account and container that you have configured your app to use.</span></span> 

* <span data-ttu-id="7973d-109">App configuration</span><span class="sxs-lookup"><span data-stu-id="7973d-109">App configuration</span></span>
* <span data-ttu-id="7973d-110">File content</span><span class="sxs-lookup"><span data-stu-id="7973d-110">File content</span></span>
* <span data-ttu-id="7973d-111">Database connected to your app</span><span class="sxs-lookup"><span data-stu-id="7973d-111">Database connected to your app</span></span>

<span data-ttu-id="7973d-112">The following database solutions are supported with backup feature:</span><span class="sxs-lookup"><span data-stu-id="7973d-112">The following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="7973d-113">SQL Database</span><span class="sxs-lookup"><span data-stu-id="7973d-113">SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/)
   - [<span data-ttu-id="7973d-114">Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="7973d-114">Azure Database for MySQL</span></span>](https://azure.microsoft.com/services/mysql)
   - [<span data-ttu-id="7973d-115">Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="7973d-115">Azure Database for PostgreSQL</span></span>](https://azure.microsoft.com/services/postgresql)
   - [<span data-ttu-id="7973d-116">MySQL in-app</span><span class="sxs-lookup"><span data-stu-id="7973d-116">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  <span data-ttu-id="7973d-117">Each backup is a complete offline copy of your app, not an incremental update.</span><span class="sxs-lookup"><span data-stu-id="7973d-117">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="7973d-118">Requirements and restrictions</span><span class="sxs-lookup"><span data-stu-id="7973d-118">Requirements and restrictions</span></span>
* <span data-ttu-id="7973d-119">The Backup and Restore feature requires the App Service plan to be in the **Standard** tier or **Premium** tier.</span><span class="sxs-lookup"><span data-stu-id="7973d-119">The Backup and Restore feature requires the App Service plan to be in the **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="7973d-120">For more information about scaling your App Service plan to use a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="7973d-120">For more information about scaling your App Service plan to use a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="7973d-121">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span><span class="sxs-lookup"><span data-stu-id="7973d-121">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="7973d-122">You need an Azure storage account and container in the same subscription as the app that you want to back up.</span><span class="sxs-lookup"><span data-stu-id="7973d-122">You need an Azure storage account and container in the same subscription as the app that you want to back up.</span></span> <span data-ttu-id="7973d-123">For more information on Azure storage accounts, see the [links](#moreaboutstorage) at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="7973d-123">For more information on Azure storage accounts, see the [links](#moreaboutstorage) at the end of this article.</span></span>
* <span data-ttu-id="7973d-124">Backups can be up to 10 GB of app and database content.</span><span class="sxs-lookup"><span data-stu-id="7973d-124">Backups can be up to 10 GB of app and database content.</span></span> <span data-ttu-id="7973d-125">If the backup size exceeds this limit, you get an error.</span><span class="sxs-lookup"><span data-stu-id="7973d-125">If the backup size exceeds this limit, you get an error.</span></span>
* <span data-ttu-id="7973d-126">Backups of SSL enabled Azure Database for MySQL is not supported.</span><span class="sxs-lookup"><span data-stu-id="7973d-126">Backups of SSL enabled Azure Database for MySQL is not supported.</span></span> <span data-ttu-id="7973d-127">If a backup is configured, you will get failed backups.</span><span class="sxs-lookup"><span data-stu-id="7973d-127">If a backup is configured, you will get failed backups.</span></span>
* <span data-ttu-id="7973d-128">Backups of SSL enabled Azure Database for PostgreSQL is not supported.</span><span class="sxs-lookup"><span data-stu-id="7973d-128">Backups of SSL enabled Azure Database for PostgreSQL is not supported.</span></span> <span data-ttu-id="7973d-129">If a backup is configured, you will get failed backups.</span><span class="sxs-lookup"><span data-stu-id="7973d-129">If a backup is configured, you will get failed backups.</span></span>
* <span data-ttu-id="7973d-130">In-app MySQL databases are automatically backed up without any configuration.</span><span class="sxs-lookup"><span data-stu-id="7973d-130">In-app MySQL databases are automatically backed up without any configuration.</span></span> <span data-ttu-id="7973d-131">If you make manually settings for in-app MySQL databases, such as adding connection strings, the backups may not work correctly.</span><span class="sxs-lookup"><span data-stu-id="7973d-131">If you make manually settings for in-app MySQL databases, such as adding connection strings, the backups may not work correctly.</span></span>
* <span data-ttu-id="7973d-132">Using a firewall enabled storage account as the destination for your backups is not supported.</span><span class="sxs-lookup"><span data-stu-id="7973d-132">Using a firewall enabled storage account as the destination for your backups is not supported.</span></span> <span data-ttu-id="7973d-133">If a backup is configured, you will get failed backups.</span><span class="sxs-lookup"><span data-stu-id="7973d-133">If a backup is configured, you will get failed backups.</span></span>


<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="7973d-134">Create a manual backup</span><span class="sxs-lookup"><span data-stu-id="7973d-134">Create a manual backup</span></span>
1. <span data-ttu-id="7973d-135">In the [Azure portal](https://portal.azure.com), navigate to your app's page, select **Backups**.</span><span class="sxs-lookup"><span data-stu-id="7973d-135">In the [Azure portal](https://portal.azure.com), navigate to your app's page, select **Backups**.</span></span> <span data-ttu-id="7973d-136">The **Backups** page is displayed.</span><span class="sxs-lookup"><span data-stu-id="7973d-136">The **Backups** page is displayed.</span></span>
   
    ![Backups page][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="7973d-138">If you see the following message, click it to upgrade your App Service plan before you can proceed with backups.</span><span class="sxs-lookup"><span data-stu-id="7973d-138">If you see the following message, click it to upgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="7973d-139">For more information, see [Scale up an app in Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="7973d-139">For more information, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
   > <span data-ttu-id="7973d-140">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="7973d-140">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="7973d-141">In the **Backup** page, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="7973d-141">In the **Backup** page, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="7973d-142">In the **Backup Configuration** page, click **Storage: Not configured** to configure a storage account.</span><span class="sxs-lookup"><span data-stu-id="7973d-142">In the **Backup Configuration** page, click **Storage: Not configured** to configure a storage account.</span></span>
   
    ![Choose storage account][ChooseStorageAccount]
4. <span data-ttu-id="7973d-144">Choose your backup destination by selecting a **Storage Account** and **Container**.</span><span class="sxs-lookup"><span data-stu-id="7973d-144">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="7973d-145">The storage account must belong to the same subscription as the app you want to back up.</span><span class="sxs-lookup"><span data-stu-id="7973d-145">The storage account must belong to the same subscription as the app you want to back up.</span></span> <span data-ttu-id="7973d-146">If you wish, you can create a new storage account or a new container in the respective pages.</span><span class="sxs-lookup"><span data-stu-id="7973d-146">If you wish, you can create a new storage account or a new container in the respective pages.</span></span> <span data-ttu-id="7973d-147">When you're done, click **Select**.</span><span class="sxs-lookup"><span data-stu-id="7973d-147">When you're done, click **Select**.</span></span>
   
    ![Choose storage account](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="7973d-149">In the **Backup Configuration** page that is still left open, you can configure **Backup Database**, then select the databases you want to include in the backups (SQL database or MySQL), then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7973d-149">In the **Backup Configuration** page that is still left open, you can configure **Backup Database**, then select the databases you want to include in the backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Choose storage account](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="7973d-151">For a database to appear in this list, its connection string must exist in the **Connection strings** section of the **Application settings** page for your app.</span><span class="sxs-lookup"><span data-stu-id="7973d-151">For a database to appear in this list, its connection string must exist in the **Connection strings** section of the **Application settings** page for your app.</span></span> 
   >
   > <span data-ttu-id="7973d-152">In-app MySQL databases are automatically backed up without any configuration.</span><span class="sxs-lookup"><span data-stu-id="7973d-152">In-app MySQL databases are automatically backed up without any configuration.</span></span> <span data-ttu-id="7973d-153">If you make manually settings for in-app MySQL databases, such as adding connection strings, the backups may not work correctly.</span><span class="sxs-lookup"><span data-stu-id="7973d-153">If you make manually settings for in-app MySQL databases, such as adding connection strings, the backups may not work correctly.</span></span>
   > 
   > 
6. <span data-ttu-id="7973d-154">In the **Backup Configuration** page, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7973d-154">In the **Backup Configuration** page, click **Save**.</span></span>    
7. <span data-ttu-id="7973d-155">In the  **Backups** page, click **Backup**.</span><span class="sxs-lookup"><span data-stu-id="7973d-155">In the  **Backups** page, click **Backup**.</span></span>
   
    ![BackUpNow button][BackUpNow]
   
    <span data-ttu-id="7973d-157">You see a progress message during the backup process.</span><span class="sxs-lookup"><span data-stu-id="7973d-157">You see a progress message during the backup process.</span></span>

<span data-ttu-id="7973d-158">Once the storage account and container is configured, you can initiate a manual backup at any time.</span><span class="sxs-lookup"><span data-stu-id="7973d-158">Once the storage account and container is configured, you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="7973d-159">Configure automated backups</span><span class="sxs-lookup"><span data-stu-id="7973d-159">Configure automated backups</span></span>
1. <span data-ttu-id="7973d-160">In the **Backup Configuration** page, set **Scheduled backup** to **On**.</span><span class="sxs-lookup"><span data-stu-id="7973d-160">In the **Backup Configuration** page, set **Scheduled backup** to **On**.</span></span> 
   
    ![Choose storage account](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="7973d-162">Backup schedule options will show up, set **Scheduled Backup** to **On**, then configure the backup schedule as desired and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7973d-162">Backup schedule options will show up, set **Scheduled Backup** to **On**, then configure the backup schedule as desired and click **OK**.</span></span>
   
    ![Enable automated backups][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="7973d-164">Configure Partial Backups</span><span class="sxs-lookup"><span data-stu-id="7973d-164">Configure Partial Backups</span></span>
<span data-ttu-id="7973d-165">Sometimes you don't want to back up everything on your app.</span><span class="sxs-lookup"><span data-stu-id="7973d-165">Sometimes you don't want to back up everything on your app.</span></span> <span data-ttu-id="7973d-166">Here are a few examples:</span><span class="sxs-lookup"><span data-stu-id="7973d-166">Here are a few examples:</span></span>

* <span data-ttu-id="7973d-167">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span><span class="sxs-lookup"><span data-stu-id="7973d-167">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="7973d-168">Your app has over 10 GB of content (that's the max amount you can back up at a time).</span><span class="sxs-lookup"><span data-stu-id="7973d-168">Your app has over 10 GB of content (that's the max amount you can back up at a time).</span></span>
* <span data-ttu-id="7973d-169">You don't want to back up the log files.</span><span class="sxs-lookup"><span data-stu-id="7973d-169">You don't want to back up the log files.</span></span>

<span data-ttu-id="7973d-170">Partial backups allow you choose exactly which files you want to back up.</span><span class="sxs-lookup"><span data-stu-id="7973d-170">Partial backups allow you choose exactly which files you want to back up.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="7973d-171">Exclude files from your backup</span><span class="sxs-lookup"><span data-stu-id="7973d-171">Exclude files from your backup</span></span>
<span data-ttu-id="7973d-172">Suppose you have an app that contains log files and static images that have been backup once and are not going to change.</span><span class="sxs-lookup"><span data-stu-id="7973d-172">Suppose you have an app that contains log files and static images that have been backup once and are not going to change.</span></span> <span data-ttu-id="7973d-173">In such cases, you can exclude those folders and files from being stored in your future backups.</span><span class="sxs-lookup"><span data-stu-id="7973d-173">In such cases, you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="7973d-174">To exclude files and folders from your backups, create a `_backup.filter` file in the `D:\home\site\wwwroot` folder of your app.</span><span class="sxs-lookup"><span data-stu-id="7973d-174">To exclude files and folders from your backups, create a `_backup.filter` file in the `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="7973d-175">Specify the list of files and folders you want to exclude in this file.</span><span class="sxs-lookup"><span data-stu-id="7973d-175">Specify the list of files and folders you want to exclude in this file.</span></span> 

<span data-ttu-id="7973d-176">An easy way to access your files is to use Kudu.</span><span class="sxs-lookup"><span data-stu-id="7973d-176">An easy way to access your files is to use Kudu.</span></span> <span data-ttu-id="7973d-177">Click **Advanced Tools -> Go** setting for your web app to access Kudu.</span><span class="sxs-lookup"><span data-stu-id="7973d-177">Click **Advanced Tools -> Go** setting for your web app to access Kudu.</span></span>

![Kudu using portal][kudu-portal]

<span data-ttu-id="7973d-179">Identify the folders that you want to exclude from your backups.</span><span class="sxs-lookup"><span data-stu-id="7973d-179">Identify the folders that you want to exclude from your backups.</span></span>  <span data-ttu-id="7973d-180">For example, you want to filter out the highlighted folder and files.</span><span class="sxs-lookup"><span data-stu-id="7973d-180">For example, you want to filter out the highlighted folder and files.</span></span>

![Images Folder][ImagesFolder]

<span data-ttu-id="7973d-182">Create a file called `_backup.filter` and put the preceding list in the file, but remove `D:\home`.</span><span class="sxs-lookup"><span data-stu-id="7973d-182">Create a file called `_backup.filter` and put the preceding list in the file, but remove `D:\home`.</span></span> <span data-ttu-id="7973d-183">List one directory or file per line.</span><span class="sxs-lookup"><span data-stu-id="7973d-183">List one directory or file per line.</span></span> <span data-ttu-id="7973d-184">So the content of the file should be:</span><span class="sxs-lookup"><span data-stu-id="7973d-184">So the content of the file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="7973d-185">Upload `_backup.filter` file to the `D:\home\site\wwwroot\` directory of your site using [ftp](app-service-deploy-ftp.md) or any other method.</span><span class="sxs-lookup"><span data-stu-id="7973d-185">Upload `_backup.filter` file to the `D:\home\site\wwwroot\` directory of your site using [ftp](app-service-deploy-ftp.md) or any other method.</span></span> <span data-ttu-id="7973d-186">If you wish, you can create the file directly using Kudu  `DebugConsole` and insert the content there.</span><span class="sxs-lookup"><span data-stu-id="7973d-186">If you wish, you can create the file directly using Kudu  `DebugConsole` and insert the content there.</span></span>

<span data-ttu-id="7973d-187">Run backups the same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="7973d-187">Run backups the same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="7973d-188">Now, any files and folders that are specified in `_backup.filter` is excluded from the future backups scheduled or manually initiated.</span><span class="sxs-lookup"><span data-stu-id="7973d-188">Now, any files and folders that are specified in `_backup.filter` is excluded from the future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="7973d-189">You restore partial backups of your site the same way you would [restore a regular backup](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="7973d-189">You restore partial backups of your site the same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="7973d-190">The restore process does the right thing.</span><span class="sxs-lookup"><span data-stu-id="7973d-190">The restore process does the right thing.</span></span>
> 
> <span data-ttu-id="7973d-191">When a full backup is restored, all content on the site is replaced with whatever is in the backup.</span><span class="sxs-lookup"><span data-stu-id="7973d-191">When a full backup is restored, all content on the site is replaced with whatever is in the backup.</span></span> <span data-ttu-id="7973d-192">If a file is on the site, but not in the backup it gets deleted.</span><span class="sxs-lookup"><span data-stu-id="7973d-192">If a file is on the site, but not in the backup it gets deleted.</span></span> <span data-ttu-id="7973d-193">But when a partial backup is restored, any content that is located in one of the blacklisted directories, or any blacklisted file, is left as is.</span><span class="sxs-lookup"><span data-stu-id="7973d-193">But when a partial backup is restored, any content that is located in one of the blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="7973d-194">How backups are stored</span><span class="sxs-lookup"><span data-stu-id="7973d-194">How backups are stored</span></span>
<span data-ttu-id="7973d-195">After you have made one or more backups for your app, the backups are visible on the **Containers** page of your storage account, and your app.</span><span class="sxs-lookup"><span data-stu-id="7973d-195">After you have made one or more backups for your app, the backups are visible on the **Containers** page of your storage account, and your app.</span></span> <span data-ttu-id="7973d-196">In the storage account, each backup consists of a`.zip` file that contains the backup data and an `.xml` file that contains a manifest of the `.zip` file contents.</span><span class="sxs-lookup"><span data-stu-id="7973d-196">In the storage account, each backup consists of a`.zip` file that contains the backup data and an `.xml` file that contains a manifest of the `.zip` file contents.</span></span> <span data-ttu-id="7973d-197">You can unzip and browse these files if you want to access your backups without actually performing an app restore.</span><span class="sxs-lookup"><span data-stu-id="7973d-197">You can unzip and browse these files if you want to access your backups without actually performing an app restore.</span></span>

<span data-ttu-id="7973d-198">The database backup for the app is stored in the root of the .zip file.</span><span class="sxs-lookup"><span data-stu-id="7973d-198">The database backup for the app is stored in the root of the .zip file.</span></span> <span data-ttu-id="7973d-199">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span><span class="sxs-lookup"><span data-stu-id="7973d-199">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="7973d-200">To create a SQL database based on the BACPAC export, see [Import a BACPAC File to Create a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span><span class="sxs-lookup"><span data-stu-id="7973d-200">To create a SQL database based on the BACPAC export, see [Import a BACPAC File to Create a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="7973d-201">Altering any of the files in your **websitebackups** container can cause the backup to become invalid and therefore non-restorable.</span><span class="sxs-lookup"><span data-stu-id="7973d-201">Altering any of the files in your **websitebackups** container can cause the backup to become invalid and therefore non-restorable.</span></span>
> 
> 

## <a name="automate-with-scripts"></a><span data-ttu-id="7973d-202">Automate with scripts</span><span class="sxs-lookup"><span data-stu-id="7973d-202">Automate with scripts</span></span>

<span data-ttu-id="7973d-203">You can automate backup management with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7973d-203">You can automate backup management with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="7973d-204">For samples, see:</span><span class="sxs-lookup"><span data-stu-id="7973d-204">For samples, see:</span></span>

- [<span data-ttu-id="7973d-205">Azure CLI samples</span><span class="sxs-lookup"><span data-stu-id="7973d-205">Azure CLI samples</span></span>](app-service-cli-samples.md)
- [<span data-ttu-id="7973d-206">Azure PowerShell samples</span><span class="sxs-lookup"><span data-stu-id="7973d-206">Azure PowerShell samples</span></span>](app-service-powershell-samples.md)

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="7973d-207">Next Steps</span><span class="sxs-lookup"><span data-stu-id="7973d-207">Next Steps</span></span>
<span data-ttu-id="7973d-208">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="7973d-208">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> 


<!-- IMAGES -->
[ChooseBackupsPage]: ./media/web-sites-backup/01ChooseBackupsPage1.png
[ChooseStorageAccount]: ./media/web-sites-backup/02ChooseStorageAccount-1.png
[BackUpNow]: ./media/web-sites-backup/04BackUpNow1.png
[SetAutomatedBackupOn]: ./media/web-sites-backup/06SetAutomatedBackupOn1.png
[SaveIcon]: ./media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: ./media/web-sites-backup/11Images.png
[LogsFolder]: ./media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: ./media/web-sites-backup/13GhostUpgradeWarning.png
[kudu-portal]:./media/web-sites-backup/kudu-portal.PNG

