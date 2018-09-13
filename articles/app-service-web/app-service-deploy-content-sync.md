---
title: Sync content from a cloud folder to Azure App Service
description: Learn how to deploy your app to Azure App Service via content sync from a cloud folder.
services: app-service
documentationcenter: ''
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: d33a2e363cffd18825ad3b783af8c34e7835f04d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553444"
---
# <a name="sync-content-from-a-cloud-folder-to-azure-app-service"></a><span data-ttu-id="56818-103">Sync content from a cloud folder to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="56818-103">Sync content from a cloud folder to Azure App Service</span></span>
<span data-ttu-id="56818-104">This tutorial shows you how to deploy to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span><span class="sxs-lookup"><span data-stu-id="56818-104">This tutorial shows you how to deploy to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <a name="overview"></a><span data-ttu-id="56818-105">Overview of content sync deployment</span><span class="sxs-lookup"><span data-stu-id="56818-105">Overview of content sync deployment</span></span>
<span data-ttu-id="56818-106">The on-demand content sync deployment is powered by the [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span><span class="sxs-lookup"><span data-stu-id="56818-106">The on-demand content sync deployment is powered by the [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="56818-107">In the [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync to App Service with the click of a button.</span><span class="sxs-lookup"><span data-stu-id="56818-107">In the [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync to App Service with the click of a button.</span></span> <span data-ttu-id="56818-108">Content sync utilizes the Kudu process for build and deployment.</span><span class="sxs-lookup"><span data-stu-id="56818-108">Content sync utilizes the Kudu process for build and deployment.</span></span> 

## <a name="contentsync"></a><span data-ttu-id="56818-109">How to enable content sync deployment</span><span class="sxs-lookup"><span data-stu-id="56818-109">How to enable content sync deployment</span></span>
<span data-ttu-id="56818-110">To enable content sync from the [Azure Portal](https://portal.azure.com), follow these steps:</span><span class="sxs-lookup"><span data-stu-id="56818-110">To enable content sync from the [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="56818-111">In your app's blade in the Azure Portal, click **Settings** > **Deployment Source**.</span><span class="sxs-lookup"><span data-stu-id="56818-111">In your app's blade in the Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="56818-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as the source for deployment.</span><span class="sxs-lookup"><span data-stu-id="56818-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as the source for deployment.</span></span> 
   
    ![Content Sync](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="56818-114">Because of underlying differences in the APIs, **OneDrive for Business** is not supported at this time.</span><span class="sxs-lookup"><span data-stu-id="56818-114">Because of underlying differences in the APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="56818-115">Complete the authorization workflow to enable App Service to access a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span><span class="sxs-lookup"><span data-stu-id="56818-115">Complete the authorization workflow to enable App Service to access a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="56818-116">After authorization the App Service platform will give you the option to create a content folder under the designated content path, or to choose an existing content folder under this designated content path.</span><span class="sxs-lookup"><span data-stu-id="56818-116">After authorization the App Service platform will give you the option to create a content folder under the designated content path, or to choose an existing content folder under this designated content path.</span></span> <span data-ttu-id="56818-117">The designated content paths under your cloud storage accounts used for App Service sync are the following:</span><span class="sxs-lookup"><span data-stu-id="56818-117">The designated content paths under your cloud storage accounts used for App Service sync are the following:</span></span>  
   
   * <span data-ttu-id="56818-118">**OneDrive**: `Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="56818-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="56818-119">**Dropbox**: `Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="56818-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="56818-120">After the initial content sync the content sync can be initiated on demand from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="56818-120">After the initial content sync the content sync can be initiated on demand from the Azure portal.</span></span> <span data-ttu-id="56818-121">Deployment history is available with the **Deployments** blade.</span><span class="sxs-lookup"><span data-stu-id="56818-121">Deployment history is available with the **Deployments** blade.</span></span>
   
    ![Deployment History](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="56818-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span><span class="sxs-lookup"><span data-stu-id="56818-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 



