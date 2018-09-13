---
title: Azure Resource Manager-based PowerShell commands for Azure Web App | Microsoft Docs
description: Learn how to use the new Azure Resource Manager-based PowerShell commands to manage your Azure Web Apps.
services: app-service\web
documentationcenter: ''
author: ahmedelnably
manager: stefsch
editor: ''
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 8d574f051a327ba0409e6f25a5886af673d3d5e0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555704"
---
# <a name="using-azure-resource-manager-based-powershell-to-manage-azure-web-apps"></a><span data-ttu-id="c7567-103">Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="c7567-103">Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="c7567-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give the user the ability to use Azure Resource Manager-based PowerShell commands to manage Web Apps.</span><span class="sxs-lookup"><span data-stu-id="c7567-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give the user the ability to use Azure Resource Manager-based PowerShell commands to manage Web Apps.</span></span>

<span data-ttu-id="c7567-107">To learn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c7567-107">To learn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="c7567-108">To learn about the full list of parameters and options for the PowerShell cmdlets, see the [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="c7567-108">To learn about the full list of parameters and options for the PowerShell cmdlets, see the [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="c7567-109">Managing App Service Plans</span><span class="sxs-lookup"><span data-stu-id="c7567-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="c7567-110">Create an App Service Plan</span><span class="sxs-lookup"><span data-stu-id="c7567-110">Create an App Service Plan</span></span>
<span data-ttu-id="c7567-111">To create an app service plan, use the **New-AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c7567-111">To create an app service plan, use the **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="c7567-112">Following are descriptions of the different parameters:</span><span class="sxs-lookup"><span data-stu-id="c7567-112">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="c7567-113">**Name**: name of the app service plan.</span><span class="sxs-lookup"><span data-stu-id="c7567-113">**Name**: name of the app service plan.</span></span>
* <span data-ttu-id="c7567-114">**Location**: service plan location.</span><span class="sxs-lookup"><span data-stu-id="c7567-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="c7567-115">**ResourceGroupName**: resource group that includes the newly created app service plan.</span><span class="sxs-lookup"><span data-stu-id="c7567-115">**ResourceGroupName**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="c7567-116">**Tier**:  the desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span><span class="sxs-lookup"><span data-stu-id="c7567-116">**Tier**:  the desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="c7567-117">**WorkerSize**: the size of workers (Default is small if the Tier parameter was specified as Basic, Standard, or Premium.</span><span class="sxs-lookup"><span data-stu-id="c7567-117">**WorkerSize**: the size of workers (Default is small if the Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="c7567-118">Other options are Medium, and Large.)</span><span class="sxs-lookup"><span data-stu-id="c7567-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="c7567-119">**NumberofWorkers**: the number of workers in the app service plan (Default value is 1).</span><span class="sxs-lookup"><span data-stu-id="c7567-119">**NumberofWorkers**: the number of workers in the app service plan (Default value is 1).</span></span> 

<span data-ttu-id="c7567-120">Example to use this cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c7567-120">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="c7567-121">Create an App Service Plan in an App Service Environment</span><span class="sxs-lookup"><span data-stu-id="c7567-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="c7567-122">To create an app service plan in an app service environment, use the same command **New-AzureRmAppServicePlan** command with extra parameters to specify the ASE's name and ASE's resource group name.</span><span class="sxs-lookup"><span data-stu-id="c7567-122">To create an app service plan in an app service environment, use the same command **New-AzureRmAppServicePlan** command with extra parameters to specify the ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="c7567-123">Example to use this cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c7567-123">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="c7567-124">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="c7567-124">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="c7567-125">List Existing App Service Plans</span><span class="sxs-lookup"><span data-stu-id="c7567-125">List Existing App Service Plans</span></span>
<span data-ttu-id="c7567-126">To list the existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c7567-126">To list the existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="c7567-127">To list all app service plans under your subscription, use:</span><span class="sxs-lookup"><span data-stu-id="c7567-127">To list all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="c7567-128">To list all app service plans under a specific resource group, use:</span><span class="sxs-lookup"><span data-stu-id="c7567-128">To list all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="c7567-129">To get a specific app service plan, use:</span><span class="sxs-lookup"><span data-stu-id="c7567-129">To get a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="c7567-130">Configure an existing App Service Plan</span><span class="sxs-lookup"><span data-stu-id="c7567-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="c7567-131">To change the settings for an existing app service plan, use the **Set-AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c7567-131">To change the settings for an existing app service plan, use the **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="c7567-132">You can change the tier, worker size, and the number of workers</span><span class="sxs-lookup"><span data-stu-id="c7567-132">You can change the tier, worker size, and the number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="c7567-133">Scaling an App Service Plan</span><span class="sxs-lookup"><span data-stu-id="c7567-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="c7567-134">To scale an existing App Service Plan, use:</span><span class="sxs-lookup"><span data-stu-id="c7567-134">To scale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-the-worker-size-of-an-app-service-plan"></a><span data-ttu-id="c7567-135">Changing the worker size of an App Service Plan</span><span class="sxs-lookup"><span data-stu-id="c7567-135">Changing the worker size of an App Service Plan</span></span>
<span data-ttu-id="c7567-136">To change the size of workers in an existing App Service Plan, use:</span><span class="sxs-lookup"><span data-stu-id="c7567-136">To change the size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-the-tier-of-an-app-service-plan"></a><span data-ttu-id="c7567-137">Changing the Tier of an App Service Plan</span><span class="sxs-lookup"><span data-stu-id="c7567-137">Changing the Tier of an App Service Plan</span></span>
<span data-ttu-id="c7567-138">To change the tier of an existing App Service Plan, use:</span><span class="sxs-lookup"><span data-stu-id="c7567-138">To change the tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="c7567-139">Delete an existing App Service Plan</span><span class="sxs-lookup"><span data-stu-id="c7567-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="c7567-140">To delete an existing app service plan, all assigned web apps need to be moved or deleted first.</span><span class="sxs-lookup"><span data-stu-id="c7567-140">To delete an existing app service plan, all assigned web apps need to be moved or deleted first.</span></span> <span data-ttu-id="c7567-141">Then using the **Remove-AzureRmAppServicePlan** cmdlet you can delete the app service plan.</span><span class="sxs-lookup"><span data-stu-id="c7567-141">Then using the **Remove-AzureRmAppServicePlan** cmdlet you can delete the app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="c7567-142">Managing App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="c7567-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="c7567-143">Create a Web App</span><span class="sxs-lookup"><span data-stu-id="c7567-143">Create a Web App</span></span>
<span data-ttu-id="c7567-144">To create a web app, use the **New-AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c7567-144">To create a web app, use the **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="c7567-145">Following are descriptions of the different parameters:</span><span class="sxs-lookup"><span data-stu-id="c7567-145">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="c7567-146">**Name**: name for the web app.</span><span class="sxs-lookup"><span data-stu-id="c7567-146">**Name**: name for the web app.</span></span>
* <span data-ttu-id="c7567-147">**AppServicePlan**: name for the service plan used to host the web app.</span><span class="sxs-lookup"><span data-stu-id="c7567-147">**AppServicePlan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="c7567-148">**ResourceGroupName**: resource group that hosts the App service plan.</span><span class="sxs-lookup"><span data-stu-id="c7567-148">**ResourceGroupName**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="c7567-149">**Location**: the web app location.</span><span class="sxs-lookup"><span data-stu-id="c7567-149">**Location**: the web app location.</span></span>

<span data-ttu-id="c7567-150">Example to use this cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c7567-150">Example to use this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="c7567-151">Create a Web App in an App Service Environment</span><span class="sxs-lookup"><span data-stu-id="c7567-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="c7567-152">To create a web app in an App Service Environment (ASE).</span><span class="sxs-lookup"><span data-stu-id="c7567-152">To create a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="c7567-153">Use the same **New-AzureRmWebApp** command with extra parameters to specify the ASE name and the resource group name that the ASE belongs to.</span><span class="sxs-lookup"><span data-stu-id="c7567-153">Use the same **New-AzureRmWebApp** command with extra parameters to specify the ASE name and the resource group name that the ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="c7567-154">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="c7567-154">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="c7567-155">Delete an existing Web App</span><span class="sxs-lookup"><span data-stu-id="c7567-155">Delete an existing Web App</span></span>
<span data-ttu-id="c7567-156">To delete an existing web app you can use the **Remove-AzureRmWebApp** cmdlet, you need to specify the name of the web app and the resource group name.</span><span class="sxs-lookup"><span data-stu-id="c7567-156">To delete an existing web app you can use the **Remove-AzureRmWebApp** cmdlet, you need to specify the name of the web app and the resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="c7567-157">List existing Web Apps</span><span class="sxs-lookup"><span data-stu-id="c7567-157">List existing Web Apps</span></span>
<span data-ttu-id="c7567-158">To list the existing web apps, use the **Get-AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c7567-158">To list the existing web apps, use the **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="c7567-159">To list all web apps under your subscription, use:</span><span class="sxs-lookup"><span data-stu-id="c7567-159">To list all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="c7567-160">To list all web apps under a specific resource group, use:</span><span class="sxs-lookup"><span data-stu-id="c7567-160">To list all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="c7567-161">To get a specific web app, use:</span><span class="sxs-lookup"><span data-stu-id="c7567-161">To get a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="c7567-162">Configure an existing Web App</span><span class="sxs-lookup"><span data-stu-id="c7567-162">Configure an existing Web App</span></span>
<span data-ttu-id="c7567-163">To change the settings and configurations for an existing web app, use the **Set-AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c7567-163">To change the settings and configurations for an existing web app, use the **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="c7567-164">For a full list of parameters, check the [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="c7567-164">For a full list of parameters, check the [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="c7567-165">Example (1): use this cmdlet to change connection strings</span><span class="sxs-lookup"><span data-stu-id="c7567-165">Example (1): use this cmdlet to change connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="c7567-166">Example (2): add or change app settings</span><span class="sxs-lookup"><span data-stu-id="c7567-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="c7567-167">Example (3):  set the web app to run in 64-bit mode</span><span class="sxs-lookup"><span data-stu-id="c7567-167">Example (3):  set the web app to run in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-the-state-of-an-existing-web-app"></a><span data-ttu-id="c7567-168">Change the state of an existing Web App</span><span class="sxs-lookup"><span data-stu-id="c7567-168">Change the state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="c7567-169">Restart a web app</span><span class="sxs-lookup"><span data-stu-id="c7567-169">Restart a web app</span></span>
<span data-ttu-id="c7567-170">To restart a web app, you must specify the name and resource group of the web app.</span><span class="sxs-lookup"><span data-stu-id="c7567-170">To restart a web app, you must specify the name and resource group of the web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="c7567-171">Stop a web app</span><span class="sxs-lookup"><span data-stu-id="c7567-171">Stop a web app</span></span>
<span data-ttu-id="c7567-172">To stop a web app, you must specify the name and resource group of the web app.</span><span class="sxs-lookup"><span data-stu-id="c7567-172">To stop a web app, you must specify the name and resource group of the web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="c7567-173">Start a web app</span><span class="sxs-lookup"><span data-stu-id="c7567-173">Start a web app</span></span>
<span data-ttu-id="c7567-174">To start a web app, you must specify the name and resource group of the web app.</span><span class="sxs-lookup"><span data-stu-id="c7567-174">To start a web app, you must specify the name and resource group of the web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="c7567-175">Manage Web App Publishing profiles</span><span class="sxs-lookup"><span data-stu-id="c7567-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="c7567-176">Each web app has a publishing profile that can be used to publish your apps, several operations can be executed on publishing profiles.</span><span class="sxs-lookup"><span data-stu-id="c7567-176">Each web app has a publishing profile that can be used to publish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="c7567-177">Get Publishing Profile</span><span class="sxs-lookup"><span data-stu-id="c7567-177">Get Publishing Profile</span></span>
<span data-ttu-id="c7567-178">To get the publishing profile for a web app, use:</span><span class="sxs-lookup"><span data-stu-id="c7567-178">To get the publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="c7567-179">This command echoes the publishing profile to the command line as well output the publishing profile to a text file.</span><span class="sxs-lookup"><span data-stu-id="c7567-179">This command echoes the publishing profile to the command line as well output the publishing profile to a text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="c7567-180">Reset Publishing Profile</span><span class="sxs-lookup"><span data-stu-id="c7567-180">Reset Publishing Profile</span></span>
<span data-ttu-id="c7567-181">To reset both the publishing password for FTP and web deploy for a web app, use:</span><span class="sxs-lookup"><span data-stu-id="c7567-181">To reset both the publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="c7567-182">Manage Web App Certificates</span><span class="sxs-lookup"><span data-stu-id="c7567-182">Manage Web App Certificates</span></span>
<span data-ttu-id="c7567-183">To learn about how to manage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="c7567-183">To learn about how to manage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="c7567-184">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c7567-184">Next Steps</span></span>
* <span data-ttu-id="c7567-185">To learn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="c7567-185">To learn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="c7567-186">To learn about App Service Environments, see [Introduction to App Service Environment.](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="c7567-186">To learn about App Service Environments, see [Introduction to App Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="c7567-187">To learn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="c7567-187">To learn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="c7567-188">To learn about the full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="c7567-188">To learn about the full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="c7567-189">To learn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span><span class="sxs-lookup"><span data-stu-id="c7567-189">To learn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

