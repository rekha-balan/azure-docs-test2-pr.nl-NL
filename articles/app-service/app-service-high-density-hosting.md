---
title: High density hosting on Azure App Service | Microsoft Docs
description: High density hosting on Azure App Service
author: btardif
manager: erikre
editor: ''
services: app-service\web
documentationcenter: ''
ms.assetid: a903cb78-4927-47b0-8427-56412c4e3e64
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/11/2017
ms.author: byvinyal
ms.openlocfilehash: 1111fab637890046f550610c79a9b4cc4f6306a5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556105"
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="dd9a5-103">High density hosting on Azure App Service</span><span class="sxs-lookup"><span data-stu-id="dd9a5-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="dd9a5-104">When using App Service, your application is decoupled from the capacity allocated to it by two concepts:</span><span class="sxs-lookup"><span data-stu-id="dd9a5-104">When using App Service, your application is decoupled from the capacity allocated to it by two concepts:</span></span>

* <span data-ttu-id="dd9a5-105">**The Application:** Represents the app and its runtime configuration.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-105">**The Application:** Represents the app and its runtime configuration.</span></span> <span data-ttu-id="dd9a5-106">For example, it includes the version of .NET that the runtime should load, the app settings, etc.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-106">For example, it includes the version of .NET that the runtime should load, the app settings, etc.</span></span>
* <span data-ttu-id="dd9a5-107">**The App Service Plan:** Defines the characteristics of the capacity, available feature set, and locality of the application.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-107">**The App Service Plan:** Defines the characteristics of the capacity, available feature set, and locality of the application.</span></span> <span data-ttu-id="dd9a5-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="dd9a5-109">An app is always linked to an App Service plan, but an App Service plan can provide capacity to one or more apps.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-109">An app is always linked to an App Service plan, but an App Service plan can provide capacity to one or more apps.</span></span>

<span data-ttu-id="dd9a5-110">As a result, the platform provides the flexibility to isolate a single app or have multiple apps share resources by sharing an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-110">As a result, the platform provides the flexibility to isolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="dd9a5-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="dd9a5-112">Per app scaling</span><span class="sxs-lookup"><span data-stu-id="dd9a5-112">Per app scaling</span></span>
<span data-ttu-id="dd9a5-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="dd9a5-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="dd9a5-115">This way, an App Service plan can be configured to provide 10 instances, but an app can be set to scale to only 5 of them.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-115">This way, an App Service plan can be configured to provide 10 instances, but an app can be set to scale to only 5 of them.</span></span>

   >[!NOTE]
   ><span data-ttu-id="dd9a5-116">Per app scaling is available only for **Premium** SKU App Service plans</span><span class="sxs-lookup"><span data-stu-id="dd9a5-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="dd9a5-117">Per app scaling using PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd9a5-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="dd9a5-118">You can create a new plan configured as a *Per app scaling* plan by passing in the ```-perSiteScaling $true``` attribute to the ```New-AzureRmAppServicePlan``` commandlet</span><span class="sxs-lookup"><span data-stu-id="dd9a5-118">You can create a new plan configured as a *Per app scaling* plan by passing in the ```-perSiteScaling $true``` attribute to the ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="dd9a5-119">If you want to update an existing App Service plan to use this feature:</span><span class="sxs-lookup"><span data-stu-id="dd9a5-119">If you want to update an existing App Service plan to use this feature:</span></span> 

- <span data-ttu-id="dd9a5-120">get the target plan ```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="dd9a5-120">get the target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="dd9a5-121">modifying the property locally ```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="dd9a5-121">modifying the property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="dd9a5-122">posting your changes back to azure ```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="dd9a5-122">posting your changes back to azure ```Set-AzureRmAppServicePlan```</span></span> 

```
    # Get the new App Service Plan and modify the "PerSiteScaling" property.
    $newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
    $newASP

    #Modify the local copy to use "PerSiteScaling" property.
    $newASP.PerSiteScaling = $true
    $newASP
    
    #Post updated app service plan back to azure
    Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="dd9a5-123">Once you have a plan that has been configured, you can set the maximum number of instances that each of the apps.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-123">Once you have a plan that has been configured, you can set the maximum number of instances that each of the apps.</span></span>

<span data-ttu-id="dd9a5-124">In the example below, the app is limited to two instances maximum regardless of how many instances the underlying app service plan scales out to.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-124">In the example below, the app is limited to two instances maximum regardless of how many instances the underlying app service plan scales out to.</span></span>

```
    # Get the app we want to configure to use "PerSiteScaling"
    $newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
    # Modify the NumberOfWorkers setting to the desired value.
    $newapp.SiteConfig.NumberOfWorkers = 2
    
    # Post updated app back to azure
    Set-AzureRmWebApp $newapp
```

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="dd9a5-125">Per app scaling using Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dd9a5-125">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="dd9a5-126">The following *Azure Resource Manager template* creates:</span><span class="sxs-lookup"><span data-stu-id="dd9a5-126">The following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="dd9a5-127">An App Service plan that's scaled out to 10 instances</span><span class="sxs-lookup"><span data-stu-id="dd9a5-127">An App Service plan that's scaled out to 10 instances</span></span>
- <span data-ttu-id="dd9a5-128">an app that's configured to scale to a max of five instances.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-128">an app that's configured to scale to a max of five instances.</span></span>

<span data-ttu-id="dd9a5-129">The App Service plan is setting the **PerSiteScaling** property to true ```"perSiteScaling": true```.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-129">The App Service plan is setting the **PerSiteScaling** property to true ```"perSiteScaling": true```.</span></span> <span data-ttu-id="dd9a5-130">The app is setting the **number of workers** to use to 5 ```"properties": { "numberOfWorkers": "5" }```.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-130">The app is setting the **number of workers** to use to 5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

```
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters":{
            "appServicePlanName": { "type": "string" },
            "appName": { "type": "string" }
         },
        "resources": [
        {
            "comments": "App Service Plan with per site perSiteScaling = true",
            "type": "Microsoft.Web/serverFarms",
            "sku": {
                "name": "P1",
                "tier": "Premium",
                "size": "P1",
                "family": "P",
                "capacity": 10
                },
            "name": "[parameters('appServicePlanName')]",
            "apiVersion": "2015-08-01",
            "location": "West US",
            "properties": {
                "name": "[parameters('appServicePlanName')]",
                "perSiteScaling": true
            }
        },
        {
            "type": "Microsoft.Web/sites",
            "name": "[parameters('appName')]",
            "apiVersion": "2015-08-01-preview",
            "location": "West US",
            "dependsOn": [ "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" ],
            "properties": { "serverFarmId": "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" },
            "resources": [ {
                    "comments": "",
                    "type": "config",
                    "name": "web",
                    "apiVersion": "2015-08-01",
                    "location": "West US",
                    "dependsOn": [ "[resourceId('Microsoft.Web/Sites', parameters('appName'))]" ],
                    "properties": { "numberOfWorkers": "5" }
             } ]
         }]
    }
```

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="dd9a5-131">Recommended configuration for high density hosting</span><span class="sxs-lookup"><span data-stu-id="dd9a5-131">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="dd9a5-132">Per app scaling is a feature that is enabled in both public Azure regions and App Service Environments.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-132">Per app scaling is a feature that is enabled in both public Azure regions and App Service Environments.</span></span> <span data-ttu-id="dd9a5-133">However, the recommended strategy is to use App Service Environments to take advantage of their advanced features and the larger pools of capacity.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-133">However, the recommended strategy is to use App Service Environments to take advantage of their advanced features and the larger pools of capacity.</span></span>  

<span data-ttu-id="dd9a5-134">Follow these steps to configure high density hosting for your apps:</span><span class="sxs-lookup"><span data-stu-id="dd9a5-134">Follow these steps to configure high density hosting for your apps:</span></span>

1. <span data-ttu-id="dd9a5-135">Configure the App Service Environment and choose a worker pool that is dedicated to the high density hosting scenario.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-135">Configure the App Service Environment and choose a worker pool that is dedicated to the high density hosting scenario.</span></span>
2. <span data-ttu-id="dd9a5-136">Create a single App Service plan, and scale it to use all the available capacity on the worker pool.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-136">Create a single App Service plan, and scale it to use all the available capacity on the worker pool.</span></span>
3. <span data-ttu-id="dd9a5-137">Set the PerSiteScaling flag to true on the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-137">Set the PerSiteScaling flag to true on the App Service plan.</span></span>
4. <span data-ttu-id="dd9a5-138">New apps are created and assigned to that App Service plan with the **numberOfWorkers** property set to **1**.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-138">New apps are created and assigned to that App Service plan with the **numberOfWorkers** property set to **1**.</span></span> <span data-ttu-id="dd9a5-139">Using this configuration yields the highest density possible on this worker pool.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-139">Using this configuration yields the highest density possible on this worker pool.</span></span>
5. <span data-ttu-id="dd9a5-140">The number of workers can be configured independently per app to grant additional resources as needed.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-140">The number of workers can be configured independently per app to grant additional resources as needed.</span></span> <span data-ttu-id="dd9a5-141">For example, a high-use app might set **numberOfWorkers** to **3** to have more processing capacity for that app, while low-use apps would set **numberOfWorkers** to **1**.</span><span class="sxs-lookup"><span data-stu-id="dd9a5-141">For example, a high-use app might set **numberOfWorkers** to **3** to have more processing capacity for that app, while low-use apps would set **numberOfWorkers** to **1**.</span></span>

