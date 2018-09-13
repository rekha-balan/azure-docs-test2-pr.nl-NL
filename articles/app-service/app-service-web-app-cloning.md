---
title: Web App Cloning using PowerShell
description: Learn how to clone your Web Apps to new Web Apps using PowerShell.
services: app-service\web
documentationcenter: ''
author: ahmedelnably
manager: stefsch
editor: ''
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/14/2016
ms.author: aelnably
ms.openlocfilehash: 30817a1a6a8079e7a896305ab0b59e48fad4d644
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868450"
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="c8d9f-103">Azure App Service App Cloning Using PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8d9f-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="c8d9f-104">With the release of Microsoft Azure PowerShell version 1.1.0, a new option has been added to `New-AzureRMWebApp` that lets you clone an existing Web App to a newly created app in a different region or in the same region.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-104">With the release of Microsoft Azure PowerShell version 1.1.0, a new option has been added to `New-AzureRMWebApp` that lets you clone an existing Web App to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="c8d9f-105">This option enables customers to deploy a number of apps across different regions quickly and easily.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-105">This option enables customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="c8d9f-106">App cloning is currently only supported for premium tier app service plans.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="c8d9f-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="c8d9f-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="c8d9f-108">Cloning an existing App</span><span class="sxs-lookup"><span data-stu-id="c8d9f-108">Cloning an existing App</span></span>
<span data-ttu-id="c8d9f-109">Scenario: An existing web app in South Central US region, and you want to clone the contents to a new web app in North Central US region.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-109">Scenario: An existing web app in South Central US region, and you want to clone the contents to a new web app in North Central US region.</span></span> <span data-ttu-id="c8d9f-110">It can be accomplished by using the Azure Resource Manager version of the PowerShell cmdlet to create a new web app with the `-SourceWebApp` option.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-110">It can be accomplished by using the Azure Resource Manager version of the PowerShell cmdlet to create a new web app with the `-SourceWebApp` option.</span></span>

<span data-ttu-id="c8d9f-111">Knowing the resource group name that contains the source web app, you can use the following PowerShell command to get the source web app's information (in this case named `source-webapp`):</span><span class="sxs-lookup"><span data-stu-id="c8d9f-111">Knowing the resource group name that contains the source web app, you can use the following PowerShell command to get the source web app's information (in this case named `source-webapp`):</span></span>

```PowerShell
$srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp
```

<span data-ttu-id="c8d9f-112">To create a new App Service Plan, you can use `New-AzureRmAppServicePlan` command as in the following example</span><span class="sxs-lookup"><span data-stu-id="c8d9f-112">To create a new App Service Plan, you can use `New-AzureRmAppServicePlan` command as in the following example</span></span>

```PowerShell
New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium
```

<span data-ttu-id="c8d9f-113">Using the `New-AzureRmWebApp` command, you can create the new web app in the North Central US region, and tie it to an existing premium tier App Service Plan.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-113">Using the `New-AzureRmWebApp` command, you can create the new web app in the North Central US region, and tie it to an existing premium tier App Service Plan.</span></span> <span data-ttu-id="c8d9f-114">Moreover, you can use the same resource group as the source web app, or define a new resource group, as shown in the following command:</span><span class="sxs-lookup"><span data-stu-id="c8d9f-114">Moreover, you can use the same resource group as the source web app, or define a new resource group, as shown in the following command:</span></span>

```PowerShell
$destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp
```

<span data-ttu-id="c8d9f-115">To clone an existing web app including all associated deployment slots, you need to use the `IncludeSourceWebAppSlots` parameter.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-115">To clone an existing web app including all associated deployment slots, you need to use the `IncludeSourceWebAppSlots` parameter.</span></span> <span data-ttu-id="c8d9f-116">The following PowerShell command demonstrates the use of that parameter with the `New-AzureRmWebApp` command:</span><span class="sxs-lookup"><span data-stu-id="c8d9f-116">The following PowerShell command demonstrates the use of that parameter with the `New-AzureRmWebApp` command:</span></span>

```PowerShell
$destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots
```

<span data-ttu-id="c8d9f-117">To clone an existing web app within the same region, you need to create a new resource group and a new app service plan in the same region, and then use the following PowerShell command to clone the web app</span><span class="sxs-lookup"><span data-stu-id="c8d9f-117">To clone an existing web app within the same region, you need to create a new resource group and a new app service plan in the same region, and then use the following PowerShell command to clone the web app</span></span>

```PowerShell
$destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap
```

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="c8d9f-118">Cloning an existing App to an App Service Environment</span><span class="sxs-lookup"><span data-stu-id="c8d9f-118">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="c8d9f-119">Scenario: An existing web app in South Central US region, and you want to clone the contents to a new web app to an existing App Service Environment (ASE).</span><span class="sxs-lookup"><span data-stu-id="c8d9f-119">Scenario: An existing web app in South Central US region, and you want to clone the contents to a new web app to an existing App Service Environment (ASE).</span></span>

<span data-ttu-id="c8d9f-120">Knowing the resource group name that contains the source web app, you can use the following PowerShell command to get the source web app's information (in this case named `source-webapp`):</span><span class="sxs-lookup"><span data-stu-id="c8d9f-120">Knowing the resource group name that contains the source web app, you can use the following PowerShell command to get the source web app's information (in this case named `source-webapp`):</span></span>

```PowerShell
$srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp
```

<span data-ttu-id="c8d9f-121">Knowing the ASE's name, and the resource group name that the ASE belongs to, you can create the new web app in the existing ASE, as shown in the following command:</span><span class="sxs-lookup"><span data-stu-id="c8d9f-121">Knowing the ASE's name, and the resource group name that the ASE belongs to, you can create the new web app in the existing ASE, as shown in the following command:</span></span>

```PowerShell
$destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp
```

<span data-ttu-id="c8d9f-122">The `Location` parameter is required due to legacy reason, but it is ignored when you create the app in an ASE.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-122">The `Location` parameter is required due to legacy reason, but it is ignored when you create the app in an ASE.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="c8d9f-123">Cloning an existing App Slot</span><span class="sxs-lookup"><span data-stu-id="c8d9f-123">Cloning an existing App Slot</span></span>
<span data-ttu-id="c8d9f-124">Scenario: You want to clone an existing Web App Slot to either a new Web App or a new Web App slot.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-124">Scenario: You want to clone an existing Web App Slot to either a new Web App or a new Web App slot.</span></span> <span data-ttu-id="c8d9f-125">The new Web App can be in the same region as the original Web App slot or in a different region.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-125">The new Web App can be in the same region as the original Web App slot or in a different region.</span></span>

<span data-ttu-id="c8d9f-126">Knowing the resource group name that contains the source web app, you can use the following PowerShell command to get the source web app slot's information (in this case named `source-webappslot`) tied to Web App `source-webapp`:</span><span class="sxs-lookup"><span data-stu-id="c8d9f-126">Knowing the resource group name that contains the source web app, you can use the following PowerShell command to get the source web app slot's information (in this case named `source-webappslot`) tied to Web App `source-webapp`:</span></span>

```PowerShell
$srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot
```

<span data-ttu-id="c8d9f-127">The following command demonstrates creating a clone of the source web app to a new web app:</span><span class="sxs-lookup"><span data-stu-id="c8d9f-127">The following command demonstrates creating a clone of the source web app to a new web app:</span></span>

```PowerShell
$destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot
```

## <a name="configuring-traffic-manager-while-cloning-an-app"></a><span data-ttu-id="c8d9f-128">Configuring Traffic Manager while cloning an app</span><span class="sxs-lookup"><span data-stu-id="c8d9f-128">Configuring Traffic Manager while cloning an app</span></span>
<span data-ttu-id="c8d9f-129">Creating multi-region web apps and configuring Azure Traffic Manager to route traffic to all these web apps, is an important scenario to ensure that customers' apps are highly available.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-129">Creating multi-region web apps and configuring Azure Traffic Manager to route traffic to all these web apps, is an important scenario to ensure that customers' apps are highly available.</span></span> <span data-ttu-id="c8d9f-130">When cloning an existing web app, you have the option to connect both web apps to either a new traffic manager profile or an existing one.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-130">When cloning an existing web app, you have the option to connect both web apps to either a new traffic manager profile or an existing one.</span></span> <span data-ttu-id="c8d9f-131">Only Azure Resource Manager version of Traffic Manager is supported.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-131">Only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-an-app"></a><span data-ttu-id="c8d9f-132">Creating a new Traffic Manager profile while cloning an app</span><span class="sxs-lookup"><span data-stu-id="c8d9f-132">Creating a new Traffic Manager profile while cloning an app</span></span>
<span data-ttu-id="c8d9f-133">Scenario: You want to clone a web app to another region, while configuring an Azure Resource Manager traffic manager profile that includes both web apps.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-133">Scenario: You want to clone a web app to another region, while configuring an Azure Resource Manager traffic manager profile that includes both web apps.</span></span> <span data-ttu-id="c8d9f-134">The following command demonstrates creating a clone of the source web app to a new web app while configuring a new Traffic Manager profile:</span><span class="sxs-lookup"><span data-stu-id="c8d9f-134">The following command demonstrates creating a clone of the source web app to a new web app while configuring a new Traffic Manager profile:</span></span>

```PowerShell
$destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile
```

### <a name="adding-new-cloned-web-app-to-an-existing-traffic-manager-profile"></a><span data-ttu-id="c8d9f-135">Adding new cloned Web App to an existing Traffic Manager profile</span><span class="sxs-lookup"><span data-stu-id="c8d9f-135">Adding new cloned Web App to an existing Traffic Manager profile</span></span>
<span data-ttu-id="c8d9f-136">Scenario: You already have an Azure Resource Manager traffic manager profile and want to add both web apps as endpoints.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-136">Scenario: You already have an Azure Resource Manager traffic manager profile and want to add both web apps as endpoints.</span></span> <span data-ttu-id="c8d9f-137">To do so, you first need to assemble the existing traffic manager profile ID.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-137">To do so, you first need to assemble the existing traffic manager profile ID.</span></span> <span data-ttu-id="c8d9f-138">You need the subscription ID, the resource group name, and the existing traffic manager profile name.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-138">You need the subscription ID, the resource group name, and the existing traffic manager profile name.</span></span>

```PowerShell
$TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"
```

<span data-ttu-id="c8d9f-139">After having the traffic manger ID, the following command demonstrates creating a clone of the source web app to a new web app while adding them to an existing Traffic Manager profile:</span><span class="sxs-lookup"><span data-stu-id="c8d9f-139">After having the traffic manger ID, the following command demonstrates creating a clone of the source web app to a new web app while adding them to an existing Traffic Manager profile:</span></span>

```PowerShell
$destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID
```

## <a name="current-restrictions"></a><span data-ttu-id="c8d9f-140">Current Restrictions</span><span class="sxs-lookup"><span data-stu-id="c8d9f-140">Current Restrictions</span></span>
<span data-ttu-id="c8d9f-141">This feature is currently in preview, and new capabilities are added over time.</span><span class="sxs-lookup"><span data-stu-id="c8d9f-141">This feature is currently in preview, and new capabilities are added over time.</span></span> <span data-ttu-id="c8d9f-142">Here are the known restrictions on the current version of app cloning:</span><span class="sxs-lookup"><span data-stu-id="c8d9f-142">Here are the known restrictions on the current version of app cloning:</span></span>

* <span data-ttu-id="c8d9f-143">Auto scale settings are not cloned</span><span class="sxs-lookup"><span data-stu-id="c8d9f-143">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="c8d9f-144">Backup schedule settings are not cloned</span><span class="sxs-lookup"><span data-stu-id="c8d9f-144">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="c8d9f-145">VNET settings are not cloned</span><span class="sxs-lookup"><span data-stu-id="c8d9f-145">VNET settings are not cloned</span></span>
* <span data-ttu-id="c8d9f-146">App Insights are not automatically set up on the destination web app</span><span class="sxs-lookup"><span data-stu-id="c8d9f-146">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="c8d9f-147">Easy Auth settings are not cloned</span><span class="sxs-lookup"><span data-stu-id="c8d9f-147">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="c8d9f-148">Kudu Extension are not cloned</span><span class="sxs-lookup"><span data-stu-id="c8d9f-148">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="c8d9f-149">TiP rules are not cloned</span><span class="sxs-lookup"><span data-stu-id="c8d9f-149">TiP rules are not cloned</span></span>
* <span data-ttu-id="c8d9f-150">Database content is not cloned</span><span class="sxs-lookup"><span data-stu-id="c8d9f-150">Database content is not cloned</span></span>
* <span data-ttu-id="c8d9f-151">Outbound IP Addresses changes if cloning to a different scale unit</span><span class="sxs-lookup"><span data-stu-id="c8d9f-151">Outbound IP Addresses changes if cloning to a different scale unit</span></span>

### <a name="references"></a><span data-ttu-id="c8d9f-152">References</span><span class="sxs-lookup"><span data-stu-id="c8d9f-152">References</span></span>
* [<span data-ttu-id="c8d9f-153">Web App Cloning</span><span class="sxs-lookup"><span data-stu-id="c8d9f-153">Web App Cloning</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="c8d9f-154">Back up a web app in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c8d9f-154">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="c8d9f-155">Azure Resource Manager support for Azure Traffic Manager Preview</span><span class="sxs-lookup"><span data-stu-id="c8d9f-155">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="c8d9f-156">Introduction to App Service Environment</span><span class="sxs-lookup"><span data-stu-id="c8d9f-156">Introduction to App Service Environment</span></span>](environment/intro.md)
* [<span data-ttu-id="c8d9f-157">Using Azure PowerShell with Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c8d9f-157">Using Azure PowerShell with Azure Resource Manager</span></span>](../azure-resource-manager/powershell-azure-resource-manager.md)

