---
title: Azure Resource Manager-based Cross-platform Command Line Tools for Azure Web App | Microsoft Docs
description: Learn how to use the new Azure Resource Manager-based Cross-platform Command Line Tools to manage your Azure Web Apps.
services: app-service\web
documentationcenter: ''
author: ahmedelnably
manager: stefsch
editor: ''
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 7a03e1417617453c43edcc3787da10d171359757
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555712"
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a>Using Azure Resource Manager-Based XPlat CLI for Azure App Service
> [!div class="op_single_selector"]
> * [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)

With the release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added. These commands give the user the ability to use Azure Resource Manager-based PowerShell commands to manage App Service.

To learn about managing Resource Groups, see [Use the Azure CLI to manage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md). 

> [!NOTE] 
> Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for the resource management deployment model.
>
>

## <a name="managing-app-service-plans"></a>Managing App Service Plans
### <a name="create-an-app-service-plan"></a>Create an App Service Plan
To create an app service plan, use the **azure appserviceplan create** command.

Following are descriptions of the different parameters:

* **--resource-group**: resource group that includes the newly created app service plan.
* **--name**: name of the app service plan.
* **--location**: app service plan location.
* **--sku**:  the desired pricing sku (The options are: F1 (Free). D1 (Shared). B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large). S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large). P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)
* **--instances**: the number of workers in the app service plan (Default value is 1).

Example to use this cmdlet:

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a>Create a Linux App Service Plan

Using the same **azure appserviceplan create** command, with the extra parameter **--islinux true**. Note the restrictions and regions outlined in [Introduction to App Service on Linux](app-service-linux-intro.md)

### <a name="list-existing-app-service-plans"></a>List Existing App Service Plans
To list the existing app service plans, use **azure appserviceplan list** command.

To list all app service plans under a specific resource group, use:

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

To get a specific app service plan, use **azure appserviceplan show** command:

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a>Configure an existing App Service Plan
To change the settings for an existing app service plan, use the **azure appserviceplan config** command. You can change the sku, and the number of workers 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a>Scaling an App Service Plan
To scale an existing App Service Plan, use:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-the-sku-of-an-app-service-plan"></a>Changing the SKU of an App Service Plan
To change the sku of an existing App Service Plan, use:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a>Delete an existing App Service Plan
To delete an existing app service plan, all assigned apps need to be moved or deleted first. Then using the **azure webapp delete** command you can delete the app service plan.

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a>Managing App Service apps
### <a name="create-a-web-app"></a>Create a web app
To create a web app, use the **azure webapp create** command.

Following are descriptions of the different parameters:

* **--name**: name for the web app.
* **--plan**: name for the service plan used to host the web app.
* **--resource-group**: resource group that hosts the App service plan.
* **--location**: the web app location.

Example to use this cmdlet:

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a>Delete an existing app
To delete an existing app, you can use the **azure webapp delete** command. You need to specify the name of the app and the resource group name.

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a>List existing apps
To list the existing apps, use the **azure webapp list** command.

To list all apps in a specific resource group, use:

    azure webapp list --resource-group ContosoAzureResourceGroup

To get a specific app, use the **azure webapp show** command.

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a>Configure an existing app
To change the settings and configurations for an existing app, use the **azure webapp config set** command.

Example (1): change the php version of a app 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

Example (2): add or change app settings

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

To know what other configuration can be changed, use the **azure webapp config set -h** command.

### <a name="change-the-state-of-an-existing-app"></a>Change the state of an existing app
#### <a name="restart-an-app"></a>Restart an app
To restart an app, you must specify the name and resource group of the app.

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a>Stop an app
To stop an app, you must specify the name and resource group of the app.

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a>Start an app
To start an app, you must specify the name and resource group of the app.

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a>Manage publishing profiles of an app
Each app has a publishing profile that can be used to publish your code.

#### <a name="get-publishing-profile"></a>Get Publishing Profile
To get the publishing profile for a app, use:

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

This command echoes the publishing profile username and password to the command line.

### <a name="manage-app-hostnames"></a>Manage app hostnames
To manage hostname bindings for your app, use the **azure webapp config hostnames** command  

#### <a name="list-hostname-bindings"></a>List hostname bindings
To get the current hostname bindings for an app, use:

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a>Add hostname bindings
To add hostname bindings to an app, use:

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a>Delete hostname bindings
To delete hostname bindings, use:

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a>Next Steps
* To learn about Azure Resource Manager CLI support, see [Use the Azure CLI to manage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)
* To learn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)
* To learn about Azure App Service on Linux, see [Introduction to App Service on Linux](app-service-linux-intro.md)
