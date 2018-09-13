---
title: Restore an app in Azure
description: Learn how to restore your app from a backup.
services: app-service
documentationcenter: ''
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 4444dbf7-363c-47e2-b24a-dbd45cb08491
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 546c6213c8dcd37619c2e18665a1975769df828e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552314"
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="0ab42-103">Restore an app in Azure</span><span class="sxs-lookup"><span data-stu-id="0ab42-103">Restore an app in Azure</span></span>
<span data-ttu-id="0ab42-104">This article shows you how to restore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="0ab42-104">This article shows you how to restore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="0ab42-105">You can restore your app with its linked databases (SQL Database or MySQL) on-demand to a previous state, or create a new app based on one of your original app's backup.</span><span class="sxs-lookup"><span data-stu-id="0ab42-105">You can restore your app with its linked databases (SQL Database or MySQL) on-demand to a previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="0ab42-106">Creating a new app that runs in parallel to the latest version can be useful for A/B testing.</span><span class="sxs-lookup"><span data-stu-id="0ab42-106">Creating a new app that runs in parallel to the latest version can be useful for A/B testing.</span></span>

<span data-ttu-id="0ab42-107">Restoring from backups is available to apps running in **Standard** and **Premium** tier.</span><span class="sxs-lookup"><span data-stu-id="0ab42-107">Restoring from backups is available to apps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="0ab42-108">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="0ab42-108">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="0ab42-109">**Premium** tier allows a greater number of daily backups to be performed than **Standard** tier.</span><span class="sxs-lookup"><span data-stu-id="0ab42-109">**Premium** tier allows a greater number of daily backups to be performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="0ab42-110">Restore an app from an existing backup</span><span class="sxs-lookup"><span data-stu-id="0ab42-110">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="0ab42-111">On the **Settings** blade of your app in the Azure Portal, click **Backups** to display the **Backups** blade.</span><span class="sxs-lookup"><span data-stu-id="0ab42-111">On the **Settings** blade of your app in the Azure Portal, click **Backups** to display the **Backups** blade.</span></span> <span data-ttu-id="0ab42-112">Then click **Restore Now** in the command bar.</span><span class="sxs-lookup"><span data-stu-id="0ab42-112">Then click **Restore Now** in the command bar.</span></span>
   
    ![Choose restore now][ChooseRestoreNow]
2. <span data-ttu-id="0ab42-114">In the **Restore** blade, first select the backup source.</span><span class="sxs-lookup"><span data-stu-id="0ab42-114">In the **Restore** blade, first select the backup source.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-restore/021ChooseSource.png)
   
    <span data-ttu-id="0ab42-115">The **App backup** option shows you all the existing backups of the current app, and you can easily select one.</span><span class="sxs-lookup"><span data-stu-id="0ab42-115">The **App backup** option shows you all the existing backups of the current app, and you can easily select one.</span></span>
    <span data-ttu-id="0ab42-116">The **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span><span class="sxs-lookup"><span data-stu-id="0ab42-116">The **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="0ab42-117">If you're trying to restore a backup of another app, use the **Storage** option.</span><span class="sxs-lookup"><span data-stu-id="0ab42-117">If you're trying to restore a backup of another app, use the **Storage** option.</span></span>
3. <span data-ttu-id="0ab42-118">Then, specify the destination for the app restore in **Restore destination**.</span><span class="sxs-lookup"><span data-stu-id="0ab42-118">Then, specify the destination for the app restore in **Restore destination**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-restore/022ChooseDestination.png)
   
   > [!WARNING]
   > <span data-ttu-id="0ab42-119">If you choose **Overwrite**, all existing data in your current app will be erased.</span><span class="sxs-lookup"><span data-stu-id="0ab42-119">If you choose **Overwrite**, all existing data in your current app will be erased.</span></span> <span data-ttu-id="0ab42-120">Before you click **OK**, make sure that it is exactly what you want to do.</span><span class="sxs-lookup"><span data-stu-id="0ab42-120">Before you click **OK**, make sure that it is exactly what you want to do.</span></span>
   > 
   > 
   
    <span data-ttu-id="0ab42-121">You can select **Existing App** to restore the app backup to another app in the same resoure group.</span><span class="sxs-lookup"><span data-stu-id="0ab42-121">You can select **Existing App** to restore the app backup to another app in the same resoure group.</span></span> <span data-ttu-id="0ab42-122">Before you use this option, you should have already created another app in your resource group with mirroring database configuration to the one defined in the app backup.</span><span class="sxs-lookup"><span data-stu-id="0ab42-122">Before you use this option, you should have already created another app in your resource group with mirroring database configuration to the one defined in the app backup.</span></span>
4. <span data-ttu-id="0ab42-123">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0ab42-123">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="0ab42-124">Download or delete a backup from a storage account</span><span class="sxs-lookup"><span data-stu-id="0ab42-124">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="0ab42-125">From the main **Browse** blade of the Azure Portal, select **Storage accounts**.</span><span class="sxs-lookup"><span data-stu-id="0ab42-125">From the main **Browse** blade of the Azure Portal, select **Storage accounts**.</span></span>
   
    <span data-ttu-id="0ab42-126">A list of your existing storage accounts will be displayed.</span><span class="sxs-lookup"><span data-stu-id="0ab42-126">A list of your existing storage accounts will be displayed.</span></span>
2. <span data-ttu-id="0ab42-127">Select the storage account that contains the backup that you want to download or delete.</span><span class="sxs-lookup"><span data-stu-id="0ab42-127">Select the storage account that contains the backup that you want to download or delete.</span></span>
   
    <span data-ttu-id="0ab42-128">The blade for the storage account will be displayed.</span><span class="sxs-lookup"><span data-stu-id="0ab42-128">The blade for the storage account will be displayed.</span></span>
3. <span data-ttu-id="0ab42-129">In the storage account blade, select the container you want</span><span class="sxs-lookup"><span data-stu-id="0ab42-129">In the storage account blade, select the container you want</span></span>
   
    ![View Containers][ViewContainers]
4. <span data-ttu-id="0ab42-131">Select backup file you want to download or delete.</span><span class="sxs-lookup"><span data-stu-id="0ab42-131">Select backup file you want to download or delete.</span></span>
   
    ![ViewContainers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="0ab42-133">Click **Download** or **Delete** depending on what you want to do.</span><span class="sxs-lookup"><span data-stu-id="0ab42-133">Click **Download** or **Delete** depending on what you want to do.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="0ab42-134">Monitor a restore operation</span><span class="sxs-lookup"><span data-stu-id="0ab42-134">Monitor a restore operation</span></span>
1. <span data-ttu-id="0ab42-135">To see details about the success or failure of the app restore operation, navigate to the **Activity Log** blade in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0ab42-135">To see details about the success or failure of the app restore operation, navigate to the **Activity Log** blade in the Azure portal.</span></span>
   
    <span data-ttu-id="0ab42-136">The **Activity log** blade displays all of your operations, along with level, status, resource, and time details.</span><span class="sxs-lookup"><span data-stu-id="0ab42-136">The **Activity log** blade displays all of your operations, along with level, status, resource, and time details.</span></span>
2. <span data-ttu-id="0ab42-137">Scroll down to find the desired restore operation and click to select it.</span><span class="sxs-lookup"><span data-stu-id="0ab42-137">Scroll down to find the desired restore operation and click to select it.</span></span>

<span data-ttu-id="0ab42-138">The details blade will display the available information related to the restore operation.</span><span class="sxs-lookup"><span data-stu-id="0ab42-138">The details blade will display the available information related to the restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ab42-139">Next Steps</span><span class="sxs-lookup"><span data-stu-id="0ab42-139">Next Steps</span></span>
<span data-ttu-id="0ab42-140">You can also backup and restore App Service apps using REST API (see [Use REST to back up and restore App Service apps](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="0ab42-140">You can also backup and restore App Service apps using REST API (see [Use REST to back up and restore App Service apps](websites-csm-backup.md)).</span></span>

> [!NOTE]
> <span data-ttu-id="0ab42-141">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="0ab42-141">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="0ab42-142">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="0ab42-142">No credit cards required; no commitments.</span></span>
> 
> 

<!-- IMAGES -->
[ChooseRestoreNow]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-restore/02ChooseRestoreNow.png
[ViewContainers]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-restore/03ViewContainers.png
[StorageAccountFile]: ./media/web-sites-restore/02StorageAccountFile.png
[BrowseCloudStorage]: ./media/web-sites-restore/03BrowseCloudStorage.png
[StorageAccountFileSelected]: ./media/web-sites-restore/04StorageAccountFileSelected.png
[ChooseRestoreSettings]: ./media/web-sites-restore/05ChooseRestoreSettings.png
[ChooseDBServer]: ./media/web-sites-restore/06ChooseDBServer.png
[RestoreToNewSQLDB]: ./media/web-sites-restore/07RestoreToNewSQLDB.png
[NewSQLDBConfig]: ./media/web-sites-restore/08NewSQLDBConfig.png
[RestoredContosoWebSite]: ./media/web-sites-restore/09RestoredContosoWebSite.png
[DashboardOperationLogsLink]: ./media/web-sites-restore/10DashboardOperationLogsLink.png
[ManagementServicesOperationLogsList]: ./media/web-sites-restore/11ManagementServicesOperationLogsList.png
[DetailsButton]: ./media/web-sites-restore/12DetailsButton.png
[OperationDetails]: ./media/web-sites-restore/13OperationDetails.png





