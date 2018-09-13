---
title: Web App Cloning using Azure Portal
description: Learn how to clone your Web Apps to new Web Apps using Azure Portal.
services: app-service\web
documentationcenter: ''
author: ahmedelnably
manager: stefsch
editor: ''
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: ef40367c8a75a5af6881ac5a60ddeec508b2af94
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552629"
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="36460-103">Azure App Service App Cloning Using Azure Portal</span><span class="sxs-lookup"><span data-stu-id="36460-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="36460-104">The cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps to a newly created app in a different region or in the same region.</span><span class="sxs-lookup"><span data-stu-id="36460-104">The cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="36460-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span><span class="sxs-lookup"><span data-stu-id="36460-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="36460-106">App cloning is currently only supported for premium tier app service plans.</span><span class="sxs-lookup"><span data-stu-id="36460-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="36460-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="36460-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="36460-108">Cloning an existing App</span><span class="sxs-lookup"><span data-stu-id="36460-108">Cloning an existing App</span></span>
<span data-ttu-id="36460-109">The web app must be running in the **Premium** mode in order for you to create a clone for the web app.</span><span class="sxs-lookup"><span data-stu-id="36460-109">The web app must be running in the **Premium** mode in order for you to create a clone for the web app.</span></span>

1. <span data-ttu-id="36460-110">In the [Azure Portal](https://portal.azure.com/), open your web app's blade.</span><span class="sxs-lookup"><span data-stu-id="36460-110">In the [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="36460-111">Click **Tools**.</span><span class="sxs-lookup"><span data-stu-id="36460-111">Click **Tools**.</span></span> <span data-ttu-id="36460-112">Then, in the **Tools** blade, click **Clone App**.</span><span class="sxs-lookup"><span data-stu-id="36460-112">Then, in the **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="36460-113">If the web app is not already in the **Premium** mode, you will receive a message indicating the supported modes for app cloning.</span><span class="sxs-lookup"><span data-stu-id="36460-113">If the web app is not already in the **Premium** mode, you will receive a message indicating the supported modes for app cloning.</span></span> <span data-ttu-id="36460-114">At this point, you have the option to select **Upgrade**.</span><span class="sxs-lookup"><span data-stu-id="36460-114">At this point, you have the option to select **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="36460-115">In the **Clone App** blade provide a name of the new web app, Resource Group, and App Service Plan.</span><span class="sxs-lookup"><span data-stu-id="36460-115">In the **Clone App** blade provide a name of the new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="36460-116">Also the user will be able to choose whether to clone a number of source web app settings or not.</span><span class="sxs-lookup"><span data-stu-id="36460-116">Also the user will be able to choose whether to clone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="36460-117">After clicking **create** the platform will start working on creating a clone of the source web app.</span><span class="sxs-lookup"><span data-stu-id="36460-117">After clicking **create** the platform will start working on creating a clone of the source web app.</span></span>

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="36460-118">Cloning an existing App to an App Service Environment</span><span class="sxs-lookup"><span data-stu-id="36460-118">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="36460-119">In the **Clone App** blade the customer will have the option to choose an app pool in an existing App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="36460-119">In the **Clone App** blade the customer will have the option to choose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="36460-120">Current Restrictions</span><span class="sxs-lookup"><span data-stu-id="36460-120">Current Restrictions</span></span>
<span data-ttu-id="36460-121">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current support of app cloning in Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="36460-121">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="36460-122">Azure Traffic Manager settings are not cloned</span><span class="sxs-lookup"><span data-stu-id="36460-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="36460-123">Auto scale settings are not cloned</span><span class="sxs-lookup"><span data-stu-id="36460-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="36460-124">Backup schedule settings are not cloned</span><span class="sxs-lookup"><span data-stu-id="36460-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="36460-125">VNET settings are not cloned</span><span class="sxs-lookup"><span data-stu-id="36460-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="36460-126">App Insights are not automatically set up on the destination web app</span><span class="sxs-lookup"><span data-stu-id="36460-126">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="36460-127">Easy Auth settings are not cloned</span><span class="sxs-lookup"><span data-stu-id="36460-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="36460-128">Kudu Extension are not cloned</span><span class="sxs-lookup"><span data-stu-id="36460-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="36460-129">TiP rules are not cloned</span><span class="sxs-lookup"><span data-stu-id="36460-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="36460-130">Database content are not cloned</span><span class="sxs-lookup"><span data-stu-id="36460-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="36460-131">References</span><span class="sxs-lookup"><span data-stu-id="36460-131">References</span></span>
* [<span data-ttu-id="36460-132">Web App Cloning using PowerShell</span><span class="sxs-lookup"><span data-stu-id="36460-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="36460-133">Back up a web app in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="36460-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="36460-134">How to Create an App Service Environment</span><span class="sxs-lookup"><span data-stu-id="36460-134">How to Create an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="36460-135">Create a web app in an App Service Environment</span><span class="sxs-lookup"><span data-stu-id="36460-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="36460-136">Introduction to App Service Environment</span><span class="sxs-lookup"><span data-stu-id="36460-136">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-app-cloning-portal/CloneSettings.png


