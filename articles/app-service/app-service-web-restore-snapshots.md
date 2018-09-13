---
title: Restore an app in Azure
description: Learn how to restore your app from a snapshot.
services: app-service
documentationcenter: ''
author: ahmedelnably
manager: cfowler
editor: ''
ms.assetid: 4164f9b5-f735-41c6-a2bb-71f15cdda417
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.topic: article
ms.date: 04/04/2018
ms.author: aelnably;nicking
ms.openlocfilehash: e1ae8fcc30323c865aa96937f43054515f293394
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867553"
---
# <a name="restore-an-app-in-azure-from-a-snapshot"></a><span data-ttu-id="ec8ad-103">Restore an app in Azure from a snapshot</span><span class="sxs-lookup"><span data-stu-id="ec8ad-103">Restore an app in Azure from a snapshot</span></span>
<span data-ttu-id="ec8ad-104">This article shows you how to restore an app in [Azure App Service](../app-service/app-service-web-overview.md) from a snapshot.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-104">This article shows you how to restore an app in [Azure App Service](../app-service/app-service-web-overview.md) from a snapshot.</span></span> <span data-ttu-id="ec8ad-105">You can restore your app to a previous state, based on one of your app's snapshots.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-105">You can restore your app to a previous state, based on one of your app's snapshots.</span></span> <span data-ttu-id="ec8ad-106">You do not need to enable snapshots backup, the platform automatically saves a snapshot of all apps for data recovery purposes.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-106">You do not need to enable snapshots backup, the platform automatically saves a snapshot of all apps for data recovery purposes.</span></span>

<span data-ttu-id="ec8ad-107">Snapshots are incremental shadow copies, and they offer several advantages over regular [backups](web-sites-backup.md):</span><span class="sxs-lookup"><span data-stu-id="ec8ad-107">Snapshots are incremental shadow copies, and they offer several advantages over regular [backups](web-sites-backup.md):</span></span>
- <span data-ttu-id="ec8ad-108">No file copy errors due to file locks.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-108">No file copy errors due to file locks.</span></span>
- <span data-ttu-id="ec8ad-109">No storage size limitation.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-109">No storage size limitation.</span></span>
- <span data-ttu-id="ec8ad-110">No configuration required.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-110">No configuration required.</span></span>

<span data-ttu-id="ec8ad-111">Restoring from snapshots is available to apps running in **Premium** tier or higher.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-111">Restoring from snapshots is available to apps running in **Premium** tier or higher.</span></span> <span data-ttu-id="ec8ad-112">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="ec8ad-112">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span>

## <a name="limitations"></a><span data-ttu-id="ec8ad-113">Limitations</span><span class="sxs-lookup"><span data-stu-id="ec8ad-113">Limitations</span></span>

- <span data-ttu-id="ec8ad-114">The feature is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-114">The feature is currently in preview.</span></span>
- <span data-ttu-id="ec8ad-115">You can only restore to the same app or to a slot belonging to that app.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-115">You can only restore to the same app or to a slot belonging to that app.</span></span>
- <span data-ttu-id="ec8ad-116">App Service stops the target app or target slot while doing the restore.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-116">App Service stops the target app or target slot while doing the restore.</span></span>
- <span data-ttu-id="ec8ad-117">App Service keeps three months worth of snapshots for platform data recovery purposes.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-117">App Service keeps three months worth of snapshots for platform data recovery purposes.</span></span>
- <span data-ttu-id="ec8ad-118">You can only restore snapshots for the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-118">You can only restore snapshots for the last 30 days.</span></span>
 

## <a name="restore-an-app-from-a-snapshot"></a><span data-ttu-id="ec8ad-119">Restore an app from a snapshot</span><span class="sxs-lookup"><span data-stu-id="ec8ad-119">Restore an app from a snapshot</span></span>

1. <span data-ttu-id="ec8ad-120">On the **Settings** page of your app in the [Azure portal](https://portal.azure.com), click **Backups** to display the **Backups** page.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-120">On the **Settings** page of your app in the [Azure portal](https://portal.azure.com), click **Backups** to display the **Backups** page.</span></span> <span data-ttu-id="ec8ad-121">Then click **Restore** under the **Snapshot(Preview)** section.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-121">Then click **Restore** under the **Snapshot(Preview)** section.</span></span>
   
    ![](./media/app-service-web-restore-snapshots/1.png)

2. <span data-ttu-id="ec8ad-122">In the **Restore** page, select the snapshot to restore.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-122">In the **Restore** page, select the snapshot to restore.</span></span>
   
    ![](./media/app-service-web-restore-snapshots/2.png)
   
3. <span data-ttu-id="ec8ad-123">Specify the destination for the app restore in **Restore destination**.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-123">Specify the destination for the app restore in **Restore destination**.</span></span>
   
    ![](./media/app-service-web-restore-snapshots/3.png)
   
   > [!WARNING]
   > <span data-ttu-id="ec8ad-124">If you choose **Overwrite**, all existing data in your app's current file system is erased and overwritten.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-124">If you choose **Overwrite**, all existing data in your app's current file system is erased and overwritten.</span></span> <span data-ttu-id="ec8ad-125">Before you click **OK**, make sure that it is what you want to do.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-125">Before you click **OK**, make sure that it is what you want to do.</span></span>
   > 
   > 
      
   > [!Note]
   > <span data-ttu-id="ec8ad-126">Due to current technical limitations, you can only restore to apps in the same scale unit.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-126">Due to current technical limitations, you can only restore to apps in the same scale unit.</span></span> <span data-ttu-id="ec8ad-127">This limitation will be removed in a future release.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-127">This limitation will be removed in a future release.</span></span>
   > 
   > 
   
    <span data-ttu-id="ec8ad-128">You can select **Existing App** to restore to a slot.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-128">You can select **Existing App** to restore to a slot.</span></span> <span data-ttu-id="ec8ad-129">Before you use this option, you should have already created a slot in your app.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-129">Before you use this option, you should have already created a slot in your app.</span></span>

4. <span data-ttu-id="ec8ad-130">You can choose to restore your site configuration.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-130">You can choose to restore your site configuration.</span></span>
   
    ![](./media/app-service-web-restore-snapshots/4.png)

5. <span data-ttu-id="ec8ad-131">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec8ad-131">Click **OK**.</span></span>
