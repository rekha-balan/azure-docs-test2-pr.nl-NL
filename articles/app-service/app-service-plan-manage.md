---
title: Manage an App Service plan in Azure | Microsoft Docs
description: Learn how to perform different tasks to manage an App Service plan.
keywords: app service, azure app service, scale, app service plan, change, create, manage, management
services: app-service
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
ms.assetid: 4859d0d5-3e3c-40cc-96eb-f318b2c51a3d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/09/2017
ms.author: cephalin
ms.openlocfilehash: 2c08522df598bd5c6313c3f026efe48e1c4a2c56
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871289"
---
# <a name="manage-an-app-service-plan-in-azure"></a><span data-ttu-id="52488-104">Manage an App Service plan in Azure</span><span class="sxs-lookup"><span data-stu-id="52488-104">Manage an App Service plan in Azure</span></span>

<span data-ttu-id="52488-105">An [Azure App Service plan](azure-web-sites-web-hosting-plans-in-depth-overview.md) provides the resources that an App Service app needs to run.</span><span class="sxs-lookup"><span data-stu-id="52488-105">An [Azure App Service plan](azure-web-sites-web-hosting-plans-in-depth-overview.md) provides the resources that an App Service app needs to run.</span></span> <span data-ttu-id="52488-106">This guide shows how to manage an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="52488-106">This guide shows how to manage an App Service plan.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="52488-107">Create an App Service plan</span><span class="sxs-lookup"><span data-stu-id="52488-107">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="52488-108">If you have an App Service Environment, see [Create an App Service plan in an App Service Environment](environment/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan).</span><span class="sxs-lookup"><span data-stu-id="52488-108">If you have an App Service Environment, see [Create an App Service plan in an App Service Environment](environment/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan).</span></span>

<span data-ttu-id="52488-109">You can create an empty App Service plan, or you can create a plan as part of app creation.</span><span class="sxs-lookup"><span data-stu-id="52488-109">You can create an empty App Service plan, or you can create a plan as part of app creation.</span></span>

1. <span data-ttu-id="52488-110">In the [Azure portal](https://portal.azure.com), select **New** > **Web + mobile**, and then select **Web App** or another kind of App Service app.</span><span class="sxs-lookup"><span data-stu-id="52488-110">In the [Azure portal](https://portal.azure.com), select **New** > **Web + mobile**, and then select **Web App** or another kind of App Service app.</span></span>

1. <span data-ttu-id="52488-111">Select an existing App Service plan or create a plan for the new app.</span><span class="sxs-lookup"><span data-stu-id="52488-111">Select an existing App Service plan or create a plan for the new app.</span></span>

   ![Create an app in the Azure portal.][createWebApp]

   <span data-ttu-id="52488-113">To create a plan:</span><span class="sxs-lookup"><span data-stu-id="52488-113">To create a plan:</span></span>

   <span data-ttu-id="52488-114">a.</span><span class="sxs-lookup"><span data-stu-id="52488-114">a.</span></span> <span data-ttu-id="52488-115">Select **[+] Create New**.</span><span class="sxs-lookup"><span data-stu-id="52488-115">Select **[+] Create New**.</span></span>

      ![Create an App Service plan.][createASP] 

   <span data-ttu-id="52488-117">b.</span><span class="sxs-lookup"><span data-stu-id="52488-117">b.</span></span> <span data-ttu-id="52488-118">For **App Service plan**, enter the name of the plan.</span><span class="sxs-lookup"><span data-stu-id="52488-118">For **App Service plan**, enter the name of the plan.</span></span>

   <span data-ttu-id="52488-119">c.</span><span class="sxs-lookup"><span data-stu-id="52488-119">c.</span></span> <span data-ttu-id="52488-120">For **Location**, select an appropriate location.</span><span class="sxs-lookup"><span data-stu-id="52488-120">For **Location**, select an appropriate location.</span></span>

   <span data-ttu-id="52488-121">d.</span><span class="sxs-lookup"><span data-stu-id="52488-121">d.</span></span> <span data-ttu-id="52488-122">For **Pricing tier**, select an appropriate pricing tier for the service.</span><span class="sxs-lookup"><span data-stu-id="52488-122">For **Pricing tier**, select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="52488-123">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span><span class="sxs-lookup"><span data-stu-id="52488-123">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="52488-124">After you have selected the pricing tier, click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="52488-124">After you have selected the pricing tier, click the **Select** button.</span></span>

<a name="move"></a>

## <a name="move-an-app-to-another-app-service-plan"></a><span data-ttu-id="52488-125">Move an app to another App Service plan</span><span class="sxs-lookup"><span data-stu-id="52488-125">Move an app to another App Service plan</span></span>

<span data-ttu-id="52488-126">You can move an app to another App Service plan, as long as the source plan and the target plan are in the _same resource group and geographical region_.</span><span class="sxs-lookup"><span data-stu-id="52488-126">You can move an app to another App Service plan, as long as the source plan and the target plan are in the _same resource group and geographical region_.</span></span>

1. <span data-ttu-id="52488-127">In the [Azure portal](https://portal.azure.com), browse to the app that you want to move.</span><span class="sxs-lookup"><span data-stu-id="52488-127">In the [Azure portal](https://portal.azure.com), browse to the app that you want to move.</span></span>

1. <span data-ttu-id="52488-128">On the menu, look for the **App Service Plan** section.</span><span class="sxs-lookup"><span data-stu-id="52488-128">On the menu, look for the **App Service Plan** section.</span></span>

1. <span data-ttu-id="52488-129">Select **Change App Service plan** to open the **App Service plan** selector.</span><span class="sxs-lookup"><span data-stu-id="52488-129">Select **Change App Service plan** to open the **App Service plan** selector.</span></span>

   ![App Service plan selector.][change] 

1. <span data-ttu-id="52488-131">In the **App Service plan** selector, select an existing plan to move this app into.</span><span class="sxs-lookup"><span data-stu-id="52488-131">In the **App Service plan** selector, select an existing plan to move this app into.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="52488-132">The **Select App Service plan** page is filtered by the following criteria:</span><span class="sxs-lookup"><span data-stu-id="52488-132">The **Select App Service plan** page is filtered by the following criteria:</span></span> 
> - <span data-ttu-id="52488-133">Exists in the same resource group</span><span class="sxs-lookup"><span data-stu-id="52488-133">Exists in the same resource group</span></span> 
> - <span data-ttu-id="52488-134">Exists in the same geographical region</span><span class="sxs-lookup"><span data-stu-id="52488-134">Exists in the same geographical region</span></span> 
> - <span data-ttu-id="52488-135">Exists in the same webspace</span><span class="sxs-lookup"><span data-stu-id="52488-135">Exists in the same webspace</span></span>  
> 
> <span data-ttu-id="52488-136">A _webspace_ is a logical construct in App Service that defines a grouping of server resources.</span><span class="sxs-lookup"><span data-stu-id="52488-136">A _webspace_ is a logical construct in App Service that defines a grouping of server resources.</span></span> <span data-ttu-id="52488-137">A geographical region (such as West US) contains many webspaces in order to allocate customers who use App Service.</span><span class="sxs-lookup"><span data-stu-id="52488-137">A geographical region (such as West US) contains many webspaces in order to allocate customers who use App Service.</span></span> <span data-ttu-id="52488-138">Currently, you can't move App Service resources between webspaces.</span><span class="sxs-lookup"><span data-stu-id="52488-138">Currently, you can't move App Service resources between webspaces.</span></span> 
> 

[!INCLUDE [app-service-dev-test-note](../../includes/app-service-dev-test-note.md)]

<span data-ttu-id="52488-139">Each plan has its own pricing tier.</span><span class="sxs-lookup"><span data-stu-id="52488-139">Each plan has its own pricing tier.</span></span> <span data-ttu-id="52488-140">For example, moving a site from a **Free** tier to a **Standard** tier enables all apps assigned to it to use the features and resources of the **Standard** tier.</span><span class="sxs-lookup"><span data-stu-id="52488-140">For example, moving a site from a **Free** tier to a **Standard** tier enables all apps assigned to it to use the features and resources of the **Standard** tier.</span></span> <span data-ttu-id="52488-141">However, moving an app from a higher-tiered plan to a lower-tiered plan means that you no longer have access to certain features.</span><span class="sxs-lookup"><span data-stu-id="52488-141">However, moving an app from a higher-tiered plan to a lower-tiered plan means that you no longer have access to certain features.</span></span> <span data-ttu-id="52488-142">If your app uses a feature that is not available in the target plan, you get an error that shows which feature is in use that is not available.</span><span class="sxs-lookup"><span data-stu-id="52488-142">If your app uses a feature that is not available in the target plan, you get an error that shows which feature is in use that is not available.</span></span> 

<span data-ttu-id="52488-143">For example, if one of your apps uses SSL certificates, you might see this error message:</span><span class="sxs-lookup"><span data-stu-id="52488-143">For example, if one of your apps uses SSL certificates, you might see this error message:</span></span>

`Cannot update the site with hostname '<app_name>' because its current SSL configuration 'SNI based SSL enabled' is not allowed in the target compute mode. Allowed SSL configuration is 'Disabled'.`

<span data-ttu-id="52488-144">In this case, before you can move the app to the target plan, you need to either:</span><span class="sxs-lookup"><span data-stu-id="52488-144">In this case, before you can move the app to the target plan, you need to either:</span></span>
- <span data-ttu-id="52488-145">Scale up the pricing tier of the target plan to **Basic** or higher.</span><span class="sxs-lookup"><span data-stu-id="52488-145">Scale up the pricing tier of the target plan to **Basic** or higher.</span></span>
- <span data-ttu-id="52488-146">Remove all SSL connections to your app.</span><span class="sxs-lookup"><span data-stu-id="52488-146">Remove all SSL connections to your app.</span></span>

## <a name="move-an-app-to-a-different-region"></a><span data-ttu-id="52488-147">Move an app to a different region</span><span class="sxs-lookup"><span data-stu-id="52488-147">Move an app to a different region</span></span>

<span data-ttu-id="52488-148">The region in which your app runs is the region of the App Service plan it's in.</span><span class="sxs-lookup"><span data-stu-id="52488-148">The region in which your app runs is the region of the App Service plan it's in.</span></span> <span data-ttu-id="52488-149">However, you cannot change an App Service plan's region.</span><span class="sxs-lookup"><span data-stu-id="52488-149">However, you cannot change an App Service plan's region.</span></span> <span data-ttu-id="52488-150">If you want to run your app in a different region, one alternative is app cloning.</span><span class="sxs-lookup"><span data-stu-id="52488-150">If you want to run your app in a different region, one alternative is app cloning.</span></span> <span data-ttu-id="52488-151">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span><span class="sxs-lookup"><span data-stu-id="52488-151">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="52488-152">You can find **Clone App** in the **Development Tools** section of the menu.</span><span class="sxs-lookup"><span data-stu-id="52488-152">You can find **Clone App** in the **Development Tools** section of the menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52488-153">Cloning has some limitations.</span><span class="sxs-lookup"><span data-stu-id="52488-153">Cloning has some limitations.</span></span> <span data-ttu-id="52488-154">You can read about them in [Azure App Service App cloning](app-service-web-app-cloning.md).</span><span class="sxs-lookup"><span data-stu-id="52488-154">You can read about them in [Azure App Service App cloning](app-service-web-app-cloning.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="52488-155">Scale an App Service plan</span><span class="sxs-lookup"><span data-stu-id="52488-155">Scale an App Service plan</span></span>

<span data-ttu-id="52488-156">To scale up an App Service plan's pricing tier, see [Scale up an app in Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="52488-156">To scale up an App Service plan's pricing tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>

<span data-ttu-id="52488-157">To scale out an app's instance count, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="52488-157">To scale out an app's instance count, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span>

<a name="delete"></a>

## <a name="delete-an-app-service-plan"></a><span data-ttu-id="52488-158">Delete an App Service plan</span><span class="sxs-lookup"><span data-stu-id="52488-158">Delete an App Service plan</span></span>

<span data-ttu-id="52488-159">To avoid unexpected charges, when you delete the last app in an App Service plan, App Service also deletes the plan by default.</span><span class="sxs-lookup"><span data-stu-id="52488-159">To avoid unexpected charges, when you delete the last app in an App Service plan, App Service also deletes the plan by default.</span></span> <span data-ttu-id="52488-160">If you choose to keep the plan instead, you should change the plan to **Free** tier so you're not charged.</span><span class="sxs-lookup"><span data-stu-id="52488-160">If you choose to keep the plan instead, you should change the plan to **Free** tier so you're not charged.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52488-161">App Service plans that have no apps associated with them still incur charges because they continue to reserve the configured VM instances.</span><span class="sxs-lookup"><span data-stu-id="52488-161">App Service plans that have no apps associated with them still incur charges because they continue to reserve the configured VM instances.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52488-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="52488-162">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52488-163">Scale up an app in Azure</span><span class="sxs-lookup"><span data-stu-id="52488-163">Scale up an app in Azure</span></span>](web-sites-scale.md)

[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
