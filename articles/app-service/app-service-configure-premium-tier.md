---
title: Configure PremiumV2 tier for Azure App Service | Microsoft Docs
description: Learn how to better performance for your web, mobile, and API app in Azure App Service by scaling to the new PremiumV2 pricing tier.
keywords: app service, azure app service, scale, scalable, app service plan, app service cost
services: app-service
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
ms.assetid: ff00902b-9858-4bee-ab95-d3406018c688
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2018
ms.author: cephalin
ms.openlocfilehash: 04996e772c2989be89ce551bfa45c57154de7b2d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866084"
---
# <a name="configure-premiumv2-tier-for-azure-app-service"></a><span data-ttu-id="b7d42-104">Configure PremiumV2 tier for Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b7d42-104">Configure PremiumV2 tier for Azure App Service</span></span>

<span data-ttu-id="b7d42-105">The new **PremiumV2** pricing tier gives you faster processors, SSD storage, and doubles the memory-to-core ratio of the existing pricing tiers.</span><span class="sxs-lookup"><span data-stu-id="b7d42-105">The new **PremiumV2** pricing tier gives you faster processors, SSD storage, and doubles the memory-to-core ratio of the existing pricing tiers.</span></span> <span data-ttu-id="b7d42-106">With the performance advantage, you could save money by running your apps on fewer instances.</span><span class="sxs-lookup"><span data-stu-id="b7d42-106">With the performance advantage, you could save money by running your apps on fewer instances.</span></span> <span data-ttu-id="b7d42-107">In this article, you learn how to create an app in **PremiumV2** tier or scale up an app to **PremiumV2** tier.</span><span class="sxs-lookup"><span data-stu-id="b7d42-107">In this article, you learn how to create an app in **PremiumV2** tier or scale up an app to **PremiumV2** tier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7d42-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b7d42-108">Prerequisites</span></span>

<span data-ttu-id="b7d42-109">To scale-up a web app to **PremiumV2**, you need to have a Web App in Azure App Service that runs in a pricing tier lower than **PremiumV2**, and the Web App must be running in an App Service deployment that supports PremiumV2.</span><span class="sxs-lookup"><span data-stu-id="b7d42-109">To scale-up a web app to **PremiumV2**, you need to have a Web App in Azure App Service that runs in a pricing tier lower than **PremiumV2**, and the Web App must be running in an App Service deployment that supports PremiumV2.</span></span>

<a name="availability"></a>

## <a name="premiumv2-availability"></a><span data-ttu-id="b7d42-110">PremiumV2 availability</span><span class="sxs-lookup"><span data-stu-id="b7d42-110">PremiumV2 availability</span></span>

<span data-ttu-id="b7d42-111">The **PremiumV2** tier is available for App Service on both _Windows_ as well as _Linux_.</span><span class="sxs-lookup"><span data-stu-id="b7d42-111">The **PremiumV2** tier is available for App Service on both _Windows_ as well as _Linux_.</span></span>

<span data-ttu-id="b7d42-112">**PremiumV2** is available in most Azure regions.</span><span class="sxs-lookup"><span data-stu-id="b7d42-112">**PremiumV2** is available in most Azure regions.</span></span> <span data-ttu-id="b7d42-113">To see if it's available in your region, run the following Azure CLI command in the [Azure Cloud Shell](../cloud-shell/overview.md):</span><span class="sxs-lookup"><span data-stu-id="b7d42-113">To see if it's available in your region, run the following Azure CLI command in the [Azure Cloud Shell](../cloud-shell/overview.md):</span></span>

```azurecli-interactive
az appservice list-locations --sku P1V2
```

<a name="create"></a>

## <a name="create-an-app-in-premiumv2-tier"></a><span data-ttu-id="b7d42-114">Create an app in PremiumV2 tier</span><span class="sxs-lookup"><span data-stu-id="b7d42-114">Create an app in PremiumV2 tier</span></span>

<span data-ttu-id="b7d42-115">The pricing tier of an App Service app is defined in the [App Service plan](azure-web-sites-web-hosting-plans-in-depth-overview.md) that it runs on.</span><span class="sxs-lookup"><span data-stu-id="b7d42-115">The pricing tier of an App Service app is defined in the [App Service plan](azure-web-sites-web-hosting-plans-in-depth-overview.md) that it runs on.</span></span> <span data-ttu-id="b7d42-116">You can create an App Service plan by itself or as part of Web App creation.</span><span class="sxs-lookup"><span data-stu-id="b7d42-116">You can create an App Service plan by itself or as part of Web App creation.</span></span>

<span data-ttu-id="b7d42-117">When configuring the App Service plan in the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, select **Pricing tier**.</span><span class="sxs-lookup"><span data-stu-id="b7d42-117">When configuring the App Service plan in the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, select **Pricing tier**.</span></span> 

<span data-ttu-id="b7d42-118">Select **Production**, then select **P1V2**, **P2V2**, or **P3V2**, then click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="b7d42-118">Select **Production**, then select **P1V2**, **P2V2**, or **P3V2**, then click **Apply**.</span></span>

![](media/app-service-configure-premium-tier/scale-up-tier-select.png)

> [!IMPORTANT] 
> <span data-ttu-id="b7d42-119">If you don't see **P1V2**, **P2V2**, and **P3V2** as options, or if the options are greyed out, then **PremiumV2** likely isn't available in the underlying App Service deployment that contains the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="b7d42-119">If you don't see **P1V2**, **P2V2**, and **P3V2** as options, or if the options are greyed out, then **PremiumV2** likely isn't available in the underlying App Service deployment that contains the App Service plan.</span></span> <span data-ttu-id="b7d42-120">See see [Scale up from an unsupported resource group and region combination](#unsupported) for more details.</span><span class="sxs-lookup"><span data-stu-id="b7d42-120">See see [Scale up from an unsupported resource group and region combination](#unsupported) for more details.</span></span>

## <a name="scale-up-an-existing-app-to-premiumv2-tier"></a><span data-ttu-id="b7d42-121">Scale up an existing app to PremiumV2 tier</span><span class="sxs-lookup"><span data-stu-id="b7d42-121">Scale up an existing app to PremiumV2 tier</span></span>

<span data-ttu-id="b7d42-122">Before scaling an existing app to **PremiumV2** tier, make sure that **PremiumV2** is available.</span><span class="sxs-lookup"><span data-stu-id="b7d42-122">Before scaling an existing app to **PremiumV2** tier, make sure that **PremiumV2** is available.</span></span> <span data-ttu-id="b7d42-123">For information, see [PremiumV2 availability](#availability).</span><span class="sxs-lookup"><span data-stu-id="b7d42-123">For information, see [PremiumV2 availability](#availability).</span></span> <span data-ttu-id="b7d42-124">If it's not available, see [Scale up from an unsupported resource group and region combination](#unsupported).</span><span class="sxs-lookup"><span data-stu-id="b7d42-124">If it's not available, see [Scale up from an unsupported resource group and region combination](#unsupported).</span></span>

<span data-ttu-id="b7d42-125">Depending on your hosting environment, scaling up may require extra steps.</span><span class="sxs-lookup"><span data-stu-id="b7d42-125">Depending on your hosting environment, scaling up may require extra steps.</span></span> 

<span data-ttu-id="b7d42-126">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, open your App Service app page.</span><span class="sxs-lookup"><span data-stu-id="b7d42-126">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, open your App Service app page.</span></span>

<span data-ttu-id="b7d42-127">In the left navigation of your App Service app page, select **Scale up (App Service plan)**.</span><span class="sxs-lookup"><span data-stu-id="b7d42-127">In the left navigation of your App Service app page, select **Scale up (App Service plan)**.</span></span>

![](media/app-service-configure-premium-tier/scale-up-tier-portal.png)

<span data-ttu-id="b7d42-128">Select **Production**, then select **P1V2**, **P2V2**, or **P3V2**, then click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="b7d42-128">Select **Production**, then select **P1V2**, **P2V2**, or **P3V2**, then click **Apply**.</span></span>

![](media/app-service-configure-premium-tier/scale-up-tier-select.png)

<span data-ttu-id="b7d42-129">If your operation finishes successfully, your app's overview page shows that it's now in a **PremiumV2** tier.</span><span class="sxs-lookup"><span data-stu-id="b7d42-129">If your operation finishes successfully, your app's overview page shows that it's now in a **PremiumV2** tier.</span></span>

![](media/app-service-configure-premium-tier/finished.png)

### <a name="if-you-get-an-error"></a><span data-ttu-id="b7d42-130">If you get an error</span><span class="sxs-lookup"><span data-stu-id="b7d42-130">If you get an error</span></span>

<span data-ttu-id="b7d42-131">Some App Service plans can't scale up to the PremiumV2 tier if the underlying App Service deployment doesn’t support PremiumV2.</span><span class="sxs-lookup"><span data-stu-id="b7d42-131">Some App Service plans can't scale up to the PremiumV2 tier if the underlying App Service deployment doesn’t support PremiumV2.</span></span>  <span data-ttu-id="b7d42-132">See [Scale up from an unsupported resource group and region combination](#unsupported) for more details.</span><span class="sxs-lookup"><span data-stu-id="b7d42-132">See [Scale up from an unsupported resource group and region combination](#unsupported) for more details.</span></span>

<a name="unsupported"></a>

## <a name="scale-up-from-an-unsupported-resource-group-and-region-combination"></a><span data-ttu-id="b7d42-133">Scale up from an unsupported resource group and region combination</span><span class="sxs-lookup"><span data-stu-id="b7d42-133">Scale up from an unsupported resource group and region combination</span></span>

<span data-ttu-id="b7d42-134">If your app runs in an App Service deployment where **PremiumV2** isn't available, or if your app runs in a region that currently does not support **PremiumV2**, you will need to re-deploy your app to take advantage of **PremiumV2**.</span><span class="sxs-lookup"><span data-stu-id="b7d42-134">If your app runs in an App Service deployment where **PremiumV2** isn't available, or if your app runs in a region that currently does not support **PremiumV2**, you will need to re-deploy your app to take advantage of **PremiumV2**.</span></span>  <span data-ttu-id="b7d42-135">You have two options:</span><span class="sxs-lookup"><span data-stu-id="b7d42-135">You have two options:</span></span>

- <span data-ttu-id="b7d42-136">Create a **new** resource group, and then create a **new** web app and app service plan in the **new** resource group, choosing your desired Azure region during the creation process.</span><span class="sxs-lookup"><span data-stu-id="b7d42-136">Create a **new** resource group, and then create a **new** web app and app service plan in the **new** resource group, choosing your desired Azure region during the creation process.</span></span>  <span data-ttu-id="b7d42-137">You **must** select the **PremiumV2** plan at the time the new app service plan is created.</span><span class="sxs-lookup"><span data-stu-id="b7d42-137">You **must** select the **PremiumV2** plan at the time the new app service plan is created.</span></span>  <span data-ttu-id="b7d42-138">This ensures the combination of resource group, App Service plan, and Azure region will result in the App Service plan being created in an App Service deployment that supports **PremiumV2**.</span><span class="sxs-lookup"><span data-stu-id="b7d42-138">This ensures the combination of resource group, App Service plan, and Azure region will result in the App Service plan being created in an App Service deployment that supports **PremiumV2**.</span></span>  <span data-ttu-id="b7d42-139">Then redeploy your application code into the newly created app and app service plan.</span><span class="sxs-lookup"><span data-stu-id="b7d42-139">Then redeploy your application code into the newly created app and app service plan.</span></span> <span data-ttu-id="b7d42-140">If desired you can subsequently scale the App Service plan down from **PremiumV2** to save costs, and you will still be able to successfully scale back up again in the future using **PremiumV2**.</span><span class="sxs-lookup"><span data-stu-id="b7d42-140">If desired you can subsequently scale the App Service plan down from **PremiumV2** to save costs, and you will still be able to successfully scale back up again in the future using **PremiumV2**.</span></span>
- <span data-ttu-id="b7d42-141">If your app already runs in an existing **Premium** tier, then you can clone your app with all app settings, connection strings, and deployment configuration into a new app service plan that uses **PremiumV2**.</span><span class="sxs-lookup"><span data-stu-id="b7d42-141">If your app already runs in an existing **Premium** tier, then you can clone your app with all app settings, connection strings, and deployment configuration into a new app service plan that uses **PremiumV2**.</span></span>

    ![](media/app-service-configure-premium-tier/clone-app.png)

    <span data-ttu-id="b7d42-142">In the **Clone app** page, you can create an App Service plan using **PremiumV2** in the region you want, and specify the app settings and configuration that you want to clone.</span><span class="sxs-lookup"><span data-stu-id="b7d42-142">In the **Clone app** page, you can create an App Service plan using **PremiumV2** in the region you want, and specify the app settings and configuration that you want to clone.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="b7d42-143">Automate with scripts</span><span class="sxs-lookup"><span data-stu-id="b7d42-143">Automate with scripts</span></span>

<span data-ttu-id="b7d42-144">You can automate app creation in the **PremiumV2** tier with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b7d42-144">You can automate app creation in the **PremiumV2** tier with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="b7d42-145">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b7d42-145">Azure CLI</span></span>

<span data-ttu-id="b7d42-146">The following command creates an App Service plan in _P1V2_.</span><span class="sxs-lookup"><span data-stu-id="b7d42-146">The following command creates an App Service plan in _P1V2_.</span></span> <span data-ttu-id="b7d42-147">You can run it in the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="b7d42-147">You can run it in the Cloud Shell.</span></span> <span data-ttu-id="b7d42-148">The options for `--sku` are P1V2, _P2V2_, and _P3V2_.</span><span class="sxs-lookup"><span data-stu-id="b7d42-148">The options for `--sku` are P1V2, _P2V2_, and _P3V2_.</span></span>

```azurecli-interactive
az appservice plan create \
    --resource-group <resource_group_name> \
    --name <app_service_plan_name> \
    --sku P1V2
```

### <a name="azure-powershell"></a><span data-ttu-id="b7d42-149">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7d42-149">Azure PowerShell</span></span>

<span data-ttu-id="b7d42-150">The following command creates an App Service plan in _P1V2_.</span><span class="sxs-lookup"><span data-stu-id="b7d42-150">The following command creates an App Service plan in _P1V2_.</span></span> <span data-ttu-id="b7d42-151">The options for `-WorkerSize` are _Small_, _Medium_, and _Large_.</span><span class="sxs-lookup"><span data-stu-id="b7d42-151">The options for `-WorkerSize` are _Small_, _Medium_, and _Large_.</span></span>

```PowerShell
New-AzureRmAppServicePlan -ResourceGroupName <resource_group_name> `
    -Name <app_service_plan_name> `
    -Location <region_name> `
    -Tier "PremiumV2" `
    -WorkerSize "Small"
```
## <a name="more-resources"></a><span data-ttu-id="b7d42-152">More resources</span><span class="sxs-lookup"><span data-stu-id="b7d42-152">More resources</span></span>

[<span data-ttu-id="b7d42-153">Scale up an app in Azure</span><span class="sxs-lookup"><span data-stu-id="b7d42-153">Scale up an app in Azure</span></span>](web-sites-scale.md)  
[<span data-ttu-id="b7d42-154">Scale instance count manually or automatically</span><span class="sxs-lookup"><span data-stu-id="b7d42-154">Scale instance count manually or automatically</span></span>](../monitoring-and-diagnostics/insights-how-to-scale.md)