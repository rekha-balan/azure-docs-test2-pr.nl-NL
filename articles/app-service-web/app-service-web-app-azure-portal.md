---
title: Reference for navigating the Azure portal
description: Learn the different user experiences for App Service Web between the management portal and the Azure Portal
services: app-service
documentationcenter: ''
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: 1cbfc014189ccc84919edf7cae2fd5d5b741ed12
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550597"
---
# <a name="reference-for-navigating-the-azure-portal"></a><span data-ttu-id="c8164-103">Reference for navigating the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c8164-103">Reference for navigating the Azure portal</span></span>
<span data-ttu-id="c8164-104">Azure Websites are now called [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="c8164-104">Azure Websites are now called [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="c8164-105">We're updating all of our documentation to reflect this name change and to provide instructions for the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c8164-105">We're updating all of our documentation to reflect this name change and to provide instructions for the Azure Portal.</span></span> <span data-ttu-id="c8164-106">Until that process is done, you can use this document as a guide for working with Web Apps in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c8164-106">Until that process is done, you can use this document as a guide for working with Web Apps in the Azure portal.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="the-future-of-the-azure-classic-portal"></a><span data-ttu-id="c8164-107">The future of the Azure Classic Portal</span><span class="sxs-lookup"><span data-stu-id="c8164-107">The future of the Azure Classic Portal</span></span>
<span data-ttu-id="c8164-108">While you will notice the branding changes on the Azure Classic Portal, that portal is in the process of being replaced by the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c8164-108">While you will notice the branding changes on the Azure Classic Portal, that portal is in the process of being replaced by the Azure Portal.</span></span> <span data-ttu-id="c8164-109">As the classic portal is being phased out, the focus for new development is shifting to the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c8164-109">As the classic portal is being phased out, the focus for new development is shifting to the Azure Portal.</span></span> <span data-ttu-id="c8164-110">All upcoming new features for Web Apps will come in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c8164-110">All upcoming new features for Web Apps will come in the Azure Portal.</span></span> <span data-ttu-id="c8164-111">Start using the Azure Portal to take advantage of the latest and greatest that Web Apps have to offer.</span><span class="sxs-lookup"><span data-stu-id="c8164-111">Start using the Azure Portal to take advantage of the latest and greatest that Web Apps have to offer.</span></span>

## <a name="layout-differences-between-the-azure-classic-portal-and-azure-portal"></a><span data-ttu-id="c8164-112">Layout differences between the Azure Classic Portal and Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c8164-112">Layout differences between the Azure Classic Portal and Azure Portal</span></span>
<span data-ttu-id="c8164-113">In the classic portal, all the Azure services are listed on the left hand side.</span><span class="sxs-lookup"><span data-stu-id="c8164-113">In the classic portal, all the Azure services are listed on the left hand side.</span></span> <span data-ttu-id="c8164-114">Navigation in the classic portal follows a tree structure, where you start from the service and navigate into each element.</span><span class="sxs-lookup"><span data-stu-id="c8164-114">Navigation in the classic portal follows a tree structure, where you start from the service and navigate into each element.</span></span> <span data-ttu-id="c8164-115">This structure works well when managing independent components.</span><span class="sxs-lookup"><span data-stu-id="c8164-115">This structure works well when managing independent components.</span></span> <span data-ttu-id="c8164-116">However, applications built on Azure are a collection of interconnected services, and this tree structure isn't ideal for working with collections of services.</span><span class="sxs-lookup"><span data-stu-id="c8164-116">However, applications built on Azure are a collection of interconnected services, and this tree structure isn't ideal for working with collections of services.</span></span> 

<span data-ttu-id="c8164-117">The Azure portal makes it easy to build applications end-to-end with components from multiple services.</span><span class="sxs-lookup"><span data-stu-id="c8164-117">The Azure portal makes it easy to build applications end-to-end with components from multiple services.</span></span> <span data-ttu-id="c8164-118">The portal is organized as *journeys*.</span><span class="sxs-lookup"><span data-stu-id="c8164-118">The portal is organized as *journeys*.</span></span> <span data-ttu-id="c8164-119">A *journey* is a series of *blades*, which are containers for the different components.</span><span class="sxs-lookup"><span data-stu-id="c8164-119">A *journey* is a series of *blades*, which are containers for the different components.</span></span> <span data-ttu-id="c8164-120">For example, setting up auto-scaling for a web app is a *journey* which takes you several blades as shown in the following example: the **web-site** blade (that blade title has not yet been updated to use the new terminology), the **Settings** blade, and the **Scale out** blade.</span><span class="sxs-lookup"><span data-stu-id="c8164-120">For example, setting up auto-scaling for a web app is a *journey* which takes you several blades as shown in the following example: the **web-site** blade (that blade title has not yet been updated to use the new terminology), the **Settings** blade, and the **Scale out** blade.</span></span> <span data-ttu-id="c8164-121">In the example, auto scaling is being set up to depend on CPU usage, so there is also a **CPU Percentage** blade.</span><span class="sxs-lookup"><span data-stu-id="c8164-121">In the example, auto scaling is being set up to depend on CPU usage, so there is also a **CPU Percentage** blade.</span></span> <span data-ttu-id="c8164-122">The components within the *blades* are called *parts*, which look like tiles.</span><span class="sxs-lookup"><span data-stu-id="c8164-122">The components within the *blades* are called *parts*, which look like tiles.</span></span> 

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a><span data-ttu-id="c8164-123">Navigation example: create a web app</span><span class="sxs-lookup"><span data-stu-id="c8164-123">Navigation example: create a web app</span></span>
<span data-ttu-id="c8164-124">Creating new web apps is still as easy as 1-2-3.</span><span class="sxs-lookup"><span data-stu-id="c8164-124">Creating new web apps is still as easy as 1-2-3.</span></span> <span data-ttu-id="c8164-125">The following image shows the classic portal and the portal side-by-side to demonstrate that not much has changed in the number of steps needed to get a web app up and running.</span><span class="sxs-lookup"><span data-stu-id="c8164-125">The following image shows the classic portal and the portal side-by-side to demonstrate that not much has changed in the number of steps needed to get a web app up and running.</span></span> 

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-app-azure-portal/CreateWebApp.png)

<span data-ttu-id="c8164-126">In the portal you can choose from the most common types of web apps, including popular gallery applications like WordPress.</span><span class="sxs-lookup"><span data-stu-id="c8164-126">In the portal you can choose from the most common types of web apps, including popular gallery applications like WordPress.</span></span> <span data-ttu-id="c8164-127">For a full list of available applications, visit the [Azure Marketplace].</span><span class="sxs-lookup"><span data-stu-id="c8164-127">For a full list of available applications, visit the [Azure Marketplace].</span></span>

<span data-ttu-id="c8164-128">When you create a web app, you specify URL, App Service plan, and location in the portal just as you do in the classic portal.</span><span class="sxs-lookup"><span data-stu-id="c8164-128">When you create a web app, you specify URL, App Service plan, and location in the portal just as you do in the classic portal.</span></span> 

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

<span data-ttu-id="c8164-129">In addition, the portal lets you define other common settings.</span><span class="sxs-lookup"><span data-stu-id="c8164-129">In addition, the portal lets you define other common settings.</span></span> <span data-ttu-id="c8164-130">For example, [resource groups](../azure-resource-manager/resource-group-overview.md) make it simple to see and manage related Azure resources.</span><span class="sxs-lookup"><span data-stu-id="c8164-130">For example, [resource groups](../azure-resource-manager/resource-group-overview.md) make it simple to see and manage related Azure resources.</span></span> 

## <a name="navigation-example-settings-and-features"></a><span data-ttu-id="c8164-131">Navigation example: settings and features</span><span class="sxs-lookup"><span data-stu-id="c8164-131">Navigation example: settings and features</span></span>
<span data-ttu-id="c8164-132">All the settings and features are now logically grouped in a single blade, from which you can navigate.</span><span class="sxs-lookup"><span data-stu-id="c8164-132">All the settings and features are now logically grouped in a single blade, from which you can navigate.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-app-azure-portal/WebAppSettings.png)

<span data-ttu-id="c8164-133">For example, you can create custom domains by clicking **Custom domains and SSL** in the **Settings** blade.</span><span class="sxs-lookup"><span data-stu-id="c8164-133">For example, you can create custom domains by clicking **Custom domains and SSL** in the **Settings** blade.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-app-azure-portal/ConfigureWebApp.png)

<span data-ttu-id="c8164-134">To set up a monitoring alert, click **Requests and errors** and then **Add Alert**.</span><span class="sxs-lookup"><span data-stu-id="c8164-134">To set up a monitoring alert, click **Requests and errors** and then **Add Alert**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-app-azure-portal/Monitoring.png)

<span data-ttu-id="c8164-135">To enable diagnostics, click **Diagnostics logs** in the **Settings** blade.</span><span class="sxs-lookup"><span data-stu-id="c8164-135">To enable diagnostics, click **Diagnostics logs** in the **Settings** blade.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-app-azure-portal/Diagnostics.png)

<span data-ttu-id="c8164-136">To configure application settings, click **Application settings** in the **Settings** blade.</span><span class="sxs-lookup"><span data-stu-id="c8164-136">To configure application settings, click **Application settings** in the **Settings** blade.</span></span> 

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-app-azure-portal/AppSettingsPreview.png)

<span data-ttu-id="c8164-137">Other than the brand name, a few things in the portal have been renamed or grouped differently to make it easier to find them.</span><span class="sxs-lookup"><span data-stu-id="c8164-137">Other than the brand name, a few things in the portal have been renamed or grouped differently to make it easier to find them.</span></span> <span data-ttu-id="c8164-138">For example, below is a screenshot of the corresponding page for app settings (**Configure**) in the classic portal.</span><span class="sxs-lookup"><span data-stu-id="c8164-138">For example, below is a screenshot of the corresponding page for app settings (**Configure**) in the classic portal.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a><span data-ttu-id="c8164-139">More Resources</span><span class="sxs-lookup"><span data-stu-id="c8164-139">More Resources</span></span>
[Azure Portal]: https://portal.azure.com
[Azure Marketplace]: /marketplace/

> [!NOTE]
> <span data-ttu-id="c8164-141">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="c8164-141">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c8164-142">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="c8164-142">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="c8164-143">What's changed</span><span class="sxs-lookup"><span data-stu-id="c8164-143">What's changed</span></span>
* <span data-ttu-id="c8164-144">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="c8164-144">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>










