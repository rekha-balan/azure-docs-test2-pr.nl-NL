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
ms.openlocfilehash: 69e0e8282ee0b8503fe11a57b8ba6037247822dd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869921"
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="b9961-103">Restore an app in Azure</span><span class="sxs-lookup"><span data-stu-id="b9961-103">Restore an app in Azure</span></span>
<span data-ttu-id="b9961-104">This article shows you how to restore an app in [Azure App Service](../app-service/app-service-web-overview.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="b9961-104">This article shows you how to restore an app in [Azure App Service](../app-service/app-service-web-overview.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="b9961-105">You can restore your app with its linked databases on-demand to a previous state, or create a new app based on one of your original app's backups.</span><span class="sxs-lookup"><span data-stu-id="b9961-105">You can restore your app with its linked databases on-demand to a previous state, or create a new app based on one of your original app's backups.</span></span> <span data-ttu-id="b9961-106">Azure App Service supports the following databases for backup and restore:</span><span class="sxs-lookup"><span data-stu-id="b9961-106">Azure App Service supports the following databases for backup and restore:</span></span>
- [<span data-ttu-id="b9961-107">SQL Database</span><span class="sxs-lookup"><span data-stu-id="b9961-107">SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/)
- [<span data-ttu-id="b9961-108">Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="b9961-108">Azure Database for MySQL</span></span>](https://azure.microsoft.com/services/mysql)
- [<span data-ttu-id="b9961-109">Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="b9961-109">Azure Database for PostgreSQL</span></span>](https://azure.microsoft.com/services/postgresql)
- [<span data-ttu-id="b9961-110">MySQL in-app</span><span class="sxs-lookup"><span data-stu-id="b9961-110">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="b9961-111">Restoring from backups is available to apps running in **Standard** and **Premium** tier.</span><span class="sxs-lookup"><span data-stu-id="b9961-111">Restoring from backups is available to apps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="b9961-112">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="b9961-112">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="b9961-113">**Premium** tier allows a greater number of daily backups to be performed than **Standard** tier.</span><span class="sxs-lookup"><span data-stu-id="b9961-113">**Premium** tier allows a greater number of daily backups to be performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="b9961-114">Restore an app from an existing backup</span><span class="sxs-lookup"><span data-stu-id="b9961-114">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="b9961-115">On the **Settings** page of your app in the Azure portal, click **Backups** to display the **Backups** page.</span><span class="sxs-lookup"><span data-stu-id="b9961-115">On the **Settings** page of your app in the Azure portal, click **Backups** to display the **Backups** page.</span></span> <span data-ttu-id="b9961-116">Then click **Restore**.</span><span class="sxs-lookup"><span data-stu-id="b9961-116">Then click **Restore**.</span></span>
   
    ![Choose restore now][ChooseRestoreNow]
2. <span data-ttu-id="b9961-118">In the **Restore** page, first select the backup source.</span><span class="sxs-lookup"><span data-stu-id="b9961-118">In the **Restore** page, first select the backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="b9961-119">The **App backup** option shows you all the existing backups of the current app, and you can easily select one.</span><span class="sxs-lookup"><span data-stu-id="b9961-119">The **App backup** option shows you all the existing backups of the current app, and you can easily select one.</span></span>
    <span data-ttu-id="b9961-120">The **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span><span class="sxs-lookup"><span data-stu-id="b9961-120">The **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="b9961-121">If you're trying to restore a backup of another app, use the **Storage** option.</span><span class="sxs-lookup"><span data-stu-id="b9961-121">If you're trying to restore a backup of another app, use the **Storage** option.</span></span>
3. <span data-ttu-id="b9961-122">Then, specify the destination for the app restore in **Restore destination**.</span><span class="sxs-lookup"><span data-stu-id="b9961-122">Then, specify the destination for the app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="b9961-123">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span><span class="sxs-lookup"><span data-stu-id="b9961-123">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="b9961-124">Before you click **OK**, make sure that it is exactly what you want to do.</span><span class="sxs-lookup"><span data-stu-id="b9961-124">Before you click **OK**, make sure that it is exactly what you want to do.</span></span>
   > 
   > 
   
   > [!WARNING]
   > <span data-ttu-id="b9961-125">If the App Service is writing data to the database while you are restoring it, it may result in symptoms such as violation of PRIMARY KEY and data loss.</span><span class="sxs-lookup"><span data-stu-id="b9961-125">If the App Service is writing data to the database while you are restoring it, it may result in symptoms such as violation of PRIMARY KEY and data loss.</span></span> <span data-ttu-id="b9961-126">It is suggested to stop the App Service first before you start to restore the database.</span><span class="sxs-lookup"><span data-stu-id="b9961-126">It is suggested to stop the App Service first before you start to restore the database.</span></span>
   > 
   > 
   
    <span data-ttu-id="b9961-127">You can select **Existing App** to restore the app backup to another app in the same resource group.</span><span class="sxs-lookup"><span data-stu-id="b9961-127">You can select **Existing App** to restore the app backup to another app in the same resource group.</span></span> <span data-ttu-id="b9961-128">Before you use this option, you should have already created another app in your resource group with mirroring database configuration to the one defined in the app backup.</span><span class="sxs-lookup"><span data-stu-id="b9961-128">Before you use this option, you should have already created another app in your resource group with mirroring database configuration to the one defined in the app backup.</span></span> <span data-ttu-id="b9961-129">You can also Create a **New** app to restore your content to.</span><span class="sxs-lookup"><span data-stu-id="b9961-129">You can also Create a **New** app to restore your content to.</span></span>

4. <span data-ttu-id="b9961-130">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b9961-130">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="b9961-131">Download or delete a backup from a storage account</span><span class="sxs-lookup"><span data-stu-id="b9961-131">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="b9961-132">From the main **Browse** page of the Azure portal, select **Storage accounts**.</span><span class="sxs-lookup"><span data-stu-id="b9961-132">From the main **Browse** page of the Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="b9961-133">A list of your existing storage accounts is displayed.</span><span class="sxs-lookup"><span data-stu-id="b9961-133">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="b9961-134">Select the storage account that contains the backup that you want to download or delete.</span><span class="sxs-lookup"><span data-stu-id="b9961-134">Select the storage account that contains the backup that you want to download or delete.</span></span> <span data-ttu-id="b9961-135">The page for the storage account is displayed.</span><span class="sxs-lookup"><span data-stu-id="b9961-135">The page for the storage account is displayed.</span></span>
3. <span data-ttu-id="b9961-136">In the storage account page, select the container you want</span><span class="sxs-lookup"><span data-stu-id="b9961-136">In the storage account page, select the container you want</span></span>
   
    ![View Containers][ViewContainers]
4. <span data-ttu-id="b9961-138">Select backup file you want to download or delete.</span><span class="sxs-lookup"><span data-stu-id="b9961-138">Select backup file you want to download or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="b9961-140">Click **Download** or **Delete** depending on what you want to do.</span><span class="sxs-lookup"><span data-stu-id="b9961-140">Click **Download** or **Delete** depending on what you want to do.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="b9961-141">Monitor a restore operation</span><span class="sxs-lookup"><span data-stu-id="b9961-141">Monitor a restore operation</span></span>
<span data-ttu-id="b9961-142">To see details about the success or failure of the app restore operation, navigate to the **Activity Log** page in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b9961-142">To see details about the success or failure of the app restore operation, navigate to the **Activity Log** page in the Azure portal.</span></span>  
 

<span data-ttu-id="b9961-143">Scroll down to find the desired restore operation and click to select it.</span><span class="sxs-lookup"><span data-stu-id="b9961-143">Scroll down to find the desired restore operation and click to select it.</span></span>

<span data-ttu-id="b9961-144">The details page displays the available information related to the restore operation.</span><span class="sxs-lookup"><span data-stu-id="b9961-144">The details page displays the available information related to the restore operation.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="b9961-145">Automate with scripts</span><span class="sxs-lookup"><span data-stu-id="b9961-145">Automate with scripts</span></span>

<span data-ttu-id="b9961-146">You can automate backup management with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b9961-146">You can automate backup management with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="b9961-147">For samples, see:</span><span class="sxs-lookup"><span data-stu-id="b9961-147">For samples, see:</span></span>

- [<span data-ttu-id="b9961-148">Azure CLI samples</span><span class="sxs-lookup"><span data-stu-id="b9961-148">Azure CLI samples</span></span>](app-service-cli-samples.md)
- [<span data-ttu-id="b9961-149">Azure PowerShell samples</span><span class="sxs-lookup"><span data-stu-id="b9961-149">Azure PowerShell samples</span></span>](app-service-powershell-samples.md)

<!-- ## Next Steps
You can backup and restore App Service apps using REST API. -->


<!-- IMAGES -->
[ChooseRestoreNow]: ./media/web-sites-restore/02ChooseRestoreNow1.png
[ViewContainers]: ./media/web-sites-restore/03ViewContainers.png
