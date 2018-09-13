---
title: Sync content from a cloud folder to Azure App Service
description: Learn how to deploy your app to Azure App Service via content sync from a cloud folder.
services: app-service
documentationcenter: ''
author: cephalin
manager: cfowler
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2018
ms.author: cephalin;dariagrigoriu
ms.openlocfilehash: 3781010c74daa51c92813db85ee03eaa4c02a4cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865572"
---
# <a name="sync-content-from-a-cloud-folder-to-azure-app-service"></a><span data-ttu-id="d6eb4-103">Sync content from a cloud folder to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d6eb4-103">Sync content from a cloud folder to Azure App Service</span></span>
<span data-ttu-id="d6eb4-104">This article shows you how to sync your content to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) from Dropbox and OneDrive.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-104">This article shows you how to sync your content to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) from Dropbox and OneDrive.</span></span> 

<span data-ttu-id="d6eb4-105">The on-demand content sync deployment is powered by the App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki).</span><span class="sxs-lookup"><span data-stu-id="d6eb4-105">The on-demand content sync deployment is powered by the App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki).</span></span> <span data-ttu-id="d6eb4-106">You can, work with your app code and content in a designated cloud folder, and then sync to App Service with the click of a button.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-106">You can, work with your app code and content in a designated cloud folder, and then sync to App Service with the click of a button.</span></span> <span data-ttu-id="d6eb4-107">Content sync uses the Kudu build server.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-107">Content sync uses the Kudu build server.</span></span> 

## <a name="enable-content-sync-deployment"></a><span data-ttu-id="d6eb4-108">Enable content sync deployment</span><span class="sxs-lookup"><span data-stu-id="d6eb4-108">Enable content sync deployment</span></span>

<span data-ttu-id="d6eb4-109">To enable content sync, navigate to your App Service app page in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6eb4-109">To enable content sync, navigate to your App Service app page in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="d6eb4-110">In the left menu, click **Deployment Center** > **OneDrive** or **Dropbox** > **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-110">In the left menu, click **Deployment Center** > **OneDrive** or **Dropbox** > **Authorize**.</span></span> <span data-ttu-id="d6eb4-111">Follow the authorization prompts.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-111">Follow the authorization prompts.</span></span> 

![](media/app-service-deploy-content-sync/choose-source.png)

<span data-ttu-id="d6eb4-112">You only need to authorize with OneDrive or Dropbox once.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-112">You only need to authorize with OneDrive or Dropbox once.</span></span> <span data-ttu-id="d6eb4-113">If you're already authorized, just click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-113">If you're already authorized, just click **Continue**.</span></span> <span data-ttu-id="d6eb4-114">You can change the authorized OneDrive or Dropbox account by clicking **Change account**.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-114">You can change the authorized OneDrive or Dropbox account by clicking **Change account**.</span></span>

![](media/app-service-deploy-content-sync/continue.png)

<span data-ttu-id="d6eb4-115">In the **Configure** page, select the folder you want to synchronize.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-115">In the **Configure** page, select the folder you want to synchronize.</span></span> <span data-ttu-id="d6eb4-116">This folder is created under the following designated content path in OneDrive or Dropbox.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-116">This folder is created under the following designated content path in OneDrive or Dropbox.</span></span> 
   
* <span data-ttu-id="d6eb4-117">**OneDrive**: `Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="d6eb4-117">**OneDrive**: `Apps\Azure Web Apps`</span></span>
* <span data-ttu-id="d6eb4-118">**Dropbox**: `Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="d6eb4-118">**Dropbox**: `Apps\Azure`</span></span>

<span data-ttu-id="d6eb4-119">When finished, click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-119">When finished, click **Continue**.</span></span>

<span data-ttu-id="d6eb4-120">In the **Summary** page, verify your options and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-120">In the **Summary** page, verify your options and click **Finish**.</span></span>

## <a name="synchronize-content"></a><span data-ttu-id="d6eb4-121">Synchronize content</span><span class="sxs-lookup"><span data-stu-id="d6eb4-121">Synchronize content</span></span>

<span data-ttu-id="d6eb4-122">When you want to synchronize content in your cloud folder with App Service, go back to the **Deployment Center** page and click **Sync**.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-122">When you want to synchronize content in your cloud folder with App Service, go back to the **Deployment Center** page and click **Sync**.</span></span>

![](media/app-service-deploy-content-sync/synchronize.png)
   
   > [!NOTE]
   > <span data-ttu-id="d6eb4-123">Because of underlying differences in the APIs, **OneDrive for Business** is not supported at this time.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-123">Because of underlying differences in the APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 

## <a name="disable-content-sync-deployment"></a><span data-ttu-id="d6eb4-124">Disable content sync deployment</span><span class="sxs-lookup"><span data-stu-id="d6eb4-124">Disable content sync deployment</span></span>

<span data-ttu-id="d6eb4-125">To disable content sync, navigate to your App Service app page in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6eb4-125">To disable content sync, navigate to your App Service app page in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="d6eb4-126">In the left menu, click **Deployment Center** > **OneDrive** or **Dropbox** > **Disconnect**.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-126">In the left menu, click **Deployment Center** > **OneDrive** or **Dropbox** > **Disconnect**.</span></span>

![](media/app-service-deploy-content-sync/disable.png)

[!INCLUDE [What happens to my app during deployment?](../../includes/app-service-deploy-atomicity.md)]

## <a name="next-steps"></a><span data-ttu-id="d6eb4-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="d6eb4-127">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d6eb4-128">Deploy from local Git repo</span><span class="sxs-lookup"><span data-stu-id="d6eb4-128">Deploy from local Git repo</span></span>](app-service-deploy-local-git.md)
