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
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: d47d5a2f7d2462525bf37718a234e222b4f64e6d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555711"
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="0a165-103">Azure App Service App Cloning Using PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a165-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="0a165-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new option has been added to New-AzureRMWebApp that would give the user the ability to clone an existing Web App to a newly created app in a different region or in the same region.</span><span class="sxs-lookup"><span data-stu-id="0a165-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new option has been added to New-AzureRMWebApp that would give the user the ability to clone an existing Web App to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="0a165-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span><span class="sxs-lookup"><span data-stu-id="0a165-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="0a165-106">App cloning is currently only supported for premium tier app service plans.</span><span class="sxs-lookup"><span data-stu-id="0a165-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="0a165-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="0a165-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="0a165-108">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="0a165-108">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="0a165-109">Cloning an existing App</span><span class="sxs-lookup"><span data-stu-id="0a165-109">Cloning an existing App</span></span>
<span data-ttu-id="0a165-110">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app in North Central US region.</span><span class="sxs-lookup"><span data-stu-id="0a165-110">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app in North Central US region.</span></span> <span data-ttu-id="0a165-111">This can be accomplished by using the Azure Resource Manager version of the PowerShell cmdlet to create a new web app with the -SourceWebApp option.</span><span class="sxs-lookup"><span data-stu-id="0a165-111">This can be accomplished by using the Azure Resource Manager version of the PowerShell cmdlet to create a new web app with the -SourceWebApp option.</span></span>

<span data-ttu-id="0a165-112">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span><span class="sxs-lookup"><span data-stu-id="0a165-112">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="0a165-113">To create a new App Service Plan, we can use New-AzureRmAppServicePlan command as in the following example</span><span class="sxs-lookup"><span data-stu-id="0a165-113">To create a new App Service Plan, we can use New-AzureRmAppServicePlan command as in the following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="0a165-114">Using the New-AzureRmWebApp command, we can create the new web app in the North Central US region, and tie it to an existing premium tier App Service Plan, moreover we can use the same resource group as the source web app, or define a new resource group, the following demonstrates that:</span><span class="sxs-lookup"><span data-stu-id="0a165-114">Using the New-AzureRmWebApp command, we can create the new web app in the North Central US region, and tie it to an existing premium tier App Service Plan, moreover we can use the same resource group as the source web app, or define a new resource group, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="0a165-115">To clone an existing web app including all associated deployment slots, the user will need to use the IncludeSourceWebAppSlots parameter, the following PowerShell command demonstrates the use of that parameter with the New-AzureRmWebApp command:</span><span class="sxs-lookup"><span data-stu-id="0a165-115">To clone an existing web app including all associated deployment slots, the user will need to use the IncludeSourceWebAppSlots parameter, the following PowerShell command demonstrates the use of that parameter with the New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="0a165-116">To clone an existing web app within the same region, the user will need to create a new resource group and a new app service plan in the same region, and then using the following PowerShell command to clone the web app</span><span class="sxs-lookup"><span data-stu-id="0a165-116">To clone an existing web app within the same region, the user will need to create a new resource group and a new app service plan in the same region, and then using the following PowerShell command to clone the web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="0a165-117">Cloning an existing App to an App Service Environment</span><span class="sxs-lookup"><span data-stu-id="0a165-117">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="0a165-118">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app to an existing App Service Environment (ASE).</span><span class="sxs-lookup"><span data-stu-id="0a165-118">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app to an existing App Service Environment (ASE).</span></span>

<span data-ttu-id="0a165-119">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span><span class="sxs-lookup"><span data-stu-id="0a165-119">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="0a165-120">Knowing the ASE's name, and the resource group name that the ASE belongs to, the user can use the New-AzureRmWebApp command to create the new web app in the existing ASE, the following demonstrates that:</span><span class="sxs-lookup"><span data-stu-id="0a165-120">Knowing the ASE's name, and the resource group name that the ASE belongs to, the user can use the New-AzureRmWebApp command to create the new web app in the existing ASE, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="0a165-121">The Location parameter is required due to legacy reason, but in the case of creating an app in an ASE it will be ignored.</span><span class="sxs-lookup"><span data-stu-id="0a165-121">The Location parameter is required due to legacy reason, but in the case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="0a165-122">Cloning an existing App Slot</span><span class="sxs-lookup"><span data-stu-id="0a165-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="0a165-123">Scenario: The user would like to clone an existing Web App Slot to either a new Web App or a new Web App slot.</span><span class="sxs-lookup"><span data-stu-id="0a165-123">Scenario: The user would like to clone an existing Web App Slot to either a new Web App or a new Web App slot.</span></span> <span data-ttu-id="0a165-124">The new Web App can be in the same region as the original Web App slot or in a different region.</span><span class="sxs-lookup"><span data-stu-id="0a165-124">The new Web App can be in the same region as the original Web App slot or in a different region.</span></span>

<span data-ttu-id="0a165-125">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app slot's information (in this case named source-webappslot) tied to Web App source-webapp:</span><span class="sxs-lookup"><span data-stu-id="0a165-125">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app slot's information (in this case named source-webappslot) tied to Web App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="0a165-126">The following demonstrates creating a clone of the source web app to a new web app:</span><span class="sxs-lookup"><span data-stu-id="0a165-126">The following demonstrates creating a clone of the source web app to a new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="0a165-127">Configuring Traffic Manager while cloning a App</span><span class="sxs-lookup"><span data-stu-id="0a165-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="0a165-128">Creating multi-region web apps and configuring Azure Traffic Manager to route traffic to all these web apps, is a n important scenario to insure that customers' apps are highly available, when cloning an existing web app you have the option to connect both web apps to either a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span><span class="sxs-lookup"><span data-stu-id="0a165-128">Creating multi-region web apps and configuring Azure Traffic Manager to route traffic to all these web apps, is a n important scenario to insure that customers' apps are highly available, when cloning an existing web app you have the option to connect both web apps to either a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="0a165-129">Creating a new Traffic Manager profile while cloning a App</span><span class="sxs-lookup"><span data-stu-id="0a165-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="0a165-130">Scenario: The user would like to clone an web app to another region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span><span class="sxs-lookup"><span data-stu-id="0a165-130">Scenario: The user would like to clone an web app to another region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="0a165-131">The following demonstrates creating a clone of the source web app to a new web app while configuring a new Traffic Manager profile:</span><span class="sxs-lookup"><span data-stu-id="0a165-131">The following demonstrates creating a clone of the source web app to a new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-to-an-existing-traffic-manager-profile"></a><span data-ttu-id="0a165-132">Adding new cloned Web App to an existing Traffic Manager profile</span><span class="sxs-lookup"><span data-stu-id="0a165-132">Adding new cloned Web App to an existing Traffic Manager profile</span></span>
<span data-ttu-id="0a165-133">Scenario: The user already have an Azure Resource Manager traffic manager profile that he would like to add both web apps as endpoints.</span><span class="sxs-lookup"><span data-stu-id="0a165-133">Scenario: The user already have an Azure Resource Manager traffic manager profile that he would like to add both web apps as endpoints.</span></span> <span data-ttu-id="0a165-134">To do so, we first need to assemble the existing traffic manager profile id, we will need the subscription id, resource group name and the existing traffic manager profile name.</span><span class="sxs-lookup"><span data-stu-id="0a165-134">To do so, we first need to assemble the existing traffic manager profile id, we will need the subscription id, resource group name and the existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="0a165-135">After having the traffic manger id, the following demonstrates creating a clone of the source web app to a new web app while adding them to an existing Traffic Manager profile:</span><span class="sxs-lookup"><span data-stu-id="0a165-135">After having the traffic manger id, the following demonstrates creating a clone of the source web app to a new web app while adding them to an existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="0a165-136">Current Restrictions</span><span class="sxs-lookup"><span data-stu-id="0a165-136">Current Restrictions</span></span>
<span data-ttu-id="0a165-137">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current version of app cloning:</span><span class="sxs-lookup"><span data-stu-id="0a165-137">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current version of app cloning:</span></span>

* <span data-ttu-id="0a165-138">Auto scale settings are not cloned</span><span class="sxs-lookup"><span data-stu-id="0a165-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="0a165-139">Backup schedule settings are not cloned</span><span class="sxs-lookup"><span data-stu-id="0a165-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="0a165-140">VNET settings are not cloned</span><span class="sxs-lookup"><span data-stu-id="0a165-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="0a165-141">App Insights are not automatically set up on the destination web app</span><span class="sxs-lookup"><span data-stu-id="0a165-141">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="0a165-142">Easy Auth settings are not cloned</span><span class="sxs-lookup"><span data-stu-id="0a165-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="0a165-143">Kudu Extension are not cloned</span><span class="sxs-lookup"><span data-stu-id="0a165-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="0a165-144">TiP rules are not cloned</span><span class="sxs-lookup"><span data-stu-id="0a165-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="0a165-145">Database content are not cloned</span><span class="sxs-lookup"><span data-stu-id="0a165-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="0a165-146">References</span><span class="sxs-lookup"><span data-stu-id="0a165-146">References</span></span>
* [<span data-ttu-id="0a165-147">Azure Resource Manager based PowerShell commands for Azure Web App</span><span class="sxs-lookup"><span data-stu-id="0a165-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="0a165-148">Web App Cloning using Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0a165-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="0a165-149">Back up a web app in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="0a165-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="0a165-150">Azure Resource Manager support for Azure Traffic Manager Preview</span><span class="sxs-lookup"><span data-stu-id="0a165-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="0a165-151">Introduction to App Service Environment</span><span class="sxs-lookup"><span data-stu-id="0a165-151">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="0a165-152">Using Azure PowerShell with Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0a165-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

