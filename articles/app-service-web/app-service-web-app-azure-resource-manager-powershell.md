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
# <a name="using-azure-resource-manager-based-powershell-to-manage-azure-web-apps"></a>Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps
> [!div class="op_single_selector"]
> * [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give the user the ability to use Azure Resource Manager-based PowerShell commands to manage Web Apps.

To learn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md). 

To learn about the full list of parameters and options for the PowerShell cmdlets, see the [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)

## <a name="managing-app-service-plans"></a>Managing App Service Plans
### <a name="create-an-app-service-plan"></a>Create an App Service Plan
To create an app service plan, use the **New-AzureRmAppServicePlan** cmdlet.

Following are descriptions of the different parameters:

* **Name**: name of the app service plan.
* **Location**: service plan location.
* **ResourceGroupName**: resource group that includes the newly created app service plan.
* **Tier**:  the desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)
* **WorkerSize**: the size of workers (Default is small if the Tier parameter was specified as Basic, Standard, or Premium. Other options are Medium, and Large.)
* **NumberofWorkers**: the number of workers in the app service plan (Default value is 1). 

Example to use this cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a>Create an App Service Plan in an App Service Environment
To create an app service plan in an app service environment, use the same command **New-AzureRmAppServicePlan** command with extra parameters to specify the ASE's name and ASE's resource group name.

Example to use this cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)

### <a name="list-existing-app-service-plans"></a>List Existing App Service Plans
To list the existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.

To list all app service plans under your subscription, use: 

    Get-AzureRmAppServicePlan

To list all app service plans under a specific resource group, use:

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

To get a specific app service plan, use:

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a>Configure an existing App Service Plan
To change the settings for an existing app service plan, use the **Set-AzureRmAppServicePlan** cmdlet. You can change the tier, worker size, and the number of workers 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a>Scaling an App Service Plan
To scale an existing App Service Plan, use:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-the-worker-size-of-an-app-service-plan"></a>Changing the worker size of an App Service Plan
To change the size of workers in an existing App Service Plan, use:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-the-tier-of-an-app-service-plan"></a>Changing the Tier of an App Service Plan
To change the tier of an existing App Service Plan, use:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a>Delete an existing App Service Plan
To delete an existing app service plan, all assigned web apps need to be moved or deleted first. Then using the **Remove-AzureRmAppServicePlan** cmdlet you can delete the app service plan.

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a>Managing App Service Web Apps
### <a name="create-a-web-app"></a>Create a Web App
To create a web app, use the **New-AzureRmWebApp** cmdlet.

Following are descriptions of the different parameters:

* **Name**: name for the web app.
* **AppServicePlan**: name for the service plan used to host the web app.
* **ResourceGroupName**: resource group that hosts the App service plan.
* **Location**: the web app location.

Example to use this cmdlet:

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a>Create a Web App in an App Service Environment
To create a web app in an App Service Environment (ASE). Use the same **New-AzureRmWebApp** command with extra parameters to specify the ASE name and the resource group name that the ASE belongs to.

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)

### <a name="delete-an-existing-web-app"></a>Delete an existing Web App
To delete an existing web app you can use the **Remove-AzureRmWebApp** cmdlet, you need to specify the name of the web app and the resource group name.

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a>List existing Web Apps
To list the existing web apps, use the **Get-AzureRmWebApp** cmdlet.

To list all web apps under your subscription, use:

    Get-AzureRmWebApp

To list all web apps under a specific resource group, use:

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

To get a specific web app, use:

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a>Configure an existing Web App
To change the settings and configurations for an existing web app, use the **Set-AzureRmWebApp** cmdlet. For a full list of parameters, check the [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)

Example (1): use this cmdlet to change connection strings

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

Example (2): add or change app settings

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


Example (3):  set the web app to run in 64-bit mode

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-the-state-of-an-existing-web-app"></a>Change the state of an existing Web App
#### <a name="restart-a-web-app"></a>Restart a web app
To restart a web app, you must specify the name and resource group of the web app.

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a>Stop a web app
To stop a web app, you must specify the name and resource group of the web app.

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a>Start a web app
To start a web app, you must specify the name and resource group of the web app.

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a>Manage Web App Publishing profiles
Each web app has a publishing profile that can be used to publish your apps, several operations can be executed on publishing profiles.

#### <a name="get-publishing-profile"></a>Get Publishing Profile
To get the publishing profile for a web app, use:

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

This command echoes the publishing profile to the command line as well output the publishing profile to a text file.

#### <a name="reset-publishing-profile"></a>Reset Publishing Profile
To reset both the publishing password for FTP and web deploy for a web app, use:

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a>Manage Web App Certificates
To learn about how to manage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)

### <a name="next-steps"></a>Next Steps
* To learn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)
* To learn about App Service Environments, see [Introduction to App Service Environment.](app-service-app-service-environment-intro.md)
* To learn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)
* To learn about the full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)
* * To learn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)

