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
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="0b40d-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span><span class="sxs-lookup"><span data-stu-id="0b40d-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="0b40d-106">With the release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span><span class="sxs-lookup"><span data-stu-id="0b40d-106">With the release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="0b40d-107">These commands give the user the ability to use Azure Resource Manager-based PowerShell commands to manage App Service.</span><span class="sxs-lookup"><span data-stu-id="0b40d-107">These commands give the user the ability to use Azure Resource Manager-based PowerShell commands to manage App Service.</span></span>

<span data-ttu-id="0b40d-108">To learn about managing Resource Groups, see [Use the Azure CLI to manage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="0b40d-108">To learn about managing Resource Groups, see [Use the Azure CLI to manage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for the resource management deployment model.
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="0b40d-110">Managing App Service Plans</span><span class="sxs-lookup"><span data-stu-id="0b40d-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="0b40d-111">Create an App Service Plan</span><span class="sxs-lookup"><span data-stu-id="0b40d-111">Create an App Service Plan</span></span>
<span data-ttu-id="0b40d-112">To create an app service plan, use the **azure appserviceplan create** command.</span><span class="sxs-lookup"><span data-stu-id="0b40d-112">To create an app service plan, use the **azure appserviceplan create** command.</span></span>

<span data-ttu-id="0b40d-113">Following are descriptions of the different parameters:</span><span class="sxs-lookup"><span data-stu-id="0b40d-113">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="0b40d-114">**--resource-group**: resource group that includes the newly created app service plan.</span><span class="sxs-lookup"><span data-stu-id="0b40d-114">**--resource-group**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="0b40d-115">**--name**: name of the app service plan.</span><span class="sxs-lookup"><span data-stu-id="0b40d-115">**--name**: name of the app service plan.</span></span>
* <span data-ttu-id="0b40d-116">**--location**: app service plan location.</span><span class="sxs-lookup"><span data-stu-id="0b40d-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="0b40d-117">**--sku**:  the desired pricing sku (The options are: F1 (Free).</span><span class="sxs-lookup"><span data-stu-id="0b40d-117">**--sku**:  the desired pricing sku (The options are: F1 (Free).</span></span> <span data-ttu-id="0b40d-118">D1 (Shared).</span><span class="sxs-lookup"><span data-stu-id="0b40d-118">D1 (Shared).</span></span> <span data-ttu-id="0b40d-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span><span class="sxs-lookup"><span data-stu-id="0b40d-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="0b40d-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span><span class="sxs-lookup"><span data-stu-id="0b40d-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="0b40d-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span><span class="sxs-lookup"><span data-stu-id="0b40d-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="0b40d-122">**--instances**: the number of workers in the app service plan (Default value is 1).</span><span class="sxs-lookup"><span data-stu-id="0b40d-122">**--instances**: the number of workers in the app service plan (Default value is 1).</span></span>

<span data-ttu-id="0b40d-123">Example to use this cmdlet:</span><span class="sxs-lookup"><span data-stu-id="0b40d-123">Example to use this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="0b40d-124">Create a Linux App Service Plan</span><span class="sxs-lookup"><span data-stu-id="0b40d-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="0b40d-125">Using the same **azure appserviceplan create** command, with the extra parameter **--islinux true**.</span><span class="sxs-lookup"><span data-stu-id="0b40d-125">Using the same **azure appserviceplan create** command, with the extra parameter **--islinux true**.</span></span> <span data-ttu-id="0b40d-126">Note the restrictions and regions outlined in [Introduction to App Service on Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="0b40d-126">Note the restrictions and regions outlined in [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="0b40d-127">List Existing App Service Plans</span><span class="sxs-lookup"><span data-stu-id="0b40d-127">List Existing App Service Plans</span></span>
<span data-ttu-id="0b40d-128">To list the existing app service plans, use **azure appserviceplan list** command.</span><span class="sxs-lookup"><span data-stu-id="0b40d-128">To list the existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="0b40d-129">To list all app service plans under a specific resource group, use:</span><span class="sxs-lookup"><span data-stu-id="0b40d-129">To list all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="0b40d-130">To get a specific app service plan, use **azure appserviceplan show** command:</span><span class="sxs-lookup"><span data-stu-id="0b40d-130">To get a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="0b40d-131">Configure an existing App Service Plan</span><span class="sxs-lookup"><span data-stu-id="0b40d-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="0b40d-132">To change the settings for an existing app service plan, use the **azure appserviceplan config** command.</span><span class="sxs-lookup"><span data-stu-id="0b40d-132">To change the settings for an existing app service plan, use the **azure appserviceplan config** command.</span></span> <span data-ttu-id="0b40d-133">You can change the sku, and the number of workers</span><span class="sxs-lookup"><span data-stu-id="0b40d-133">You can change the sku, and the number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="0b40d-134">Scaling an App Service Plan</span><span class="sxs-lookup"><span data-stu-id="0b40d-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="0b40d-135">To scale an existing App Service Plan, use:</span><span class="sxs-lookup"><span data-stu-id="0b40d-135">To scale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-the-sku-of-an-app-service-plan"></a><span data-ttu-id="0b40d-136">Changing the SKU of an App Service Plan</span><span class="sxs-lookup"><span data-stu-id="0b40d-136">Changing the SKU of an App Service Plan</span></span>
<span data-ttu-id="0b40d-137">To change the sku of an existing App Service Plan, use:</span><span class="sxs-lookup"><span data-stu-id="0b40d-137">To change the sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="0b40d-138">Delete an existing App Service Plan</span><span class="sxs-lookup"><span data-stu-id="0b40d-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="0b40d-139">To delete an existing app service plan, all assigned apps need to be moved or deleted first.</span><span class="sxs-lookup"><span data-stu-id="0b40d-139">To delete an existing app service plan, all assigned apps need to be moved or deleted first.</span></span> <span data-ttu-id="0b40d-140">Then using the **azure webapp delete** command you can delete the app service plan.</span><span class="sxs-lookup"><span data-stu-id="0b40d-140">Then using the **azure webapp delete** command you can delete the app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="0b40d-141">Managing App Service apps</span><span class="sxs-lookup"><span data-stu-id="0b40d-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="0b40d-142">Create a web app</span><span class="sxs-lookup"><span data-stu-id="0b40d-142">Create a web app</span></span>
<span data-ttu-id="0b40d-143">To create a web app, use the **azure webapp create** command.</span><span class="sxs-lookup"><span data-stu-id="0b40d-143">To create a web app, use the **azure webapp create** command.</span></span>

<span data-ttu-id="0b40d-144">Following are descriptions of the different parameters:</span><span class="sxs-lookup"><span data-stu-id="0b40d-144">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="0b40d-145">**--name**: name for the web app.</span><span class="sxs-lookup"><span data-stu-id="0b40d-145">**--name**: name for the web app.</span></span>
* <span data-ttu-id="0b40d-146">**--plan**: name for the service plan used to host the web app.</span><span class="sxs-lookup"><span data-stu-id="0b40d-146">**--plan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="0b40d-147">**--resource-group**: resource group that hosts the App service plan.</span><span class="sxs-lookup"><span data-stu-id="0b40d-147">**--resource-group**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="0b40d-148">**--location**: the web app location.</span><span class="sxs-lookup"><span data-stu-id="0b40d-148">**--location**: the web app location.</span></span>

<span data-ttu-id="0b40d-149">Example to use this cmdlet:</span><span class="sxs-lookup"><span data-stu-id="0b40d-149">Example to use this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="0b40d-150">Delete an existing app</span><span class="sxs-lookup"><span data-stu-id="0b40d-150">Delete an existing app</span></span>
<span data-ttu-id="0b40d-151">To delete an existing app, you can use the **azure webapp delete** command.</span><span class="sxs-lookup"><span data-stu-id="0b40d-151">To delete an existing app, you can use the **azure webapp delete** command.</span></span> <span data-ttu-id="0b40d-152">You need to specify the name of the app and the resource group name.</span><span class="sxs-lookup"><span data-stu-id="0b40d-152">You need to specify the name of the app and the resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="0b40d-153">List existing apps</span><span class="sxs-lookup"><span data-stu-id="0b40d-153">List existing apps</span></span>
<span data-ttu-id="0b40d-154">To list the existing apps, use the **azure webapp list** command.</span><span class="sxs-lookup"><span data-stu-id="0b40d-154">To list the existing apps, use the **azure webapp list** command.</span></span>

<span data-ttu-id="0b40d-155">To list all apps in a specific resource group, use:</span><span class="sxs-lookup"><span data-stu-id="0b40d-155">To list all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="0b40d-156">To get a specific app, use the **azure webapp show** command.</span><span class="sxs-lookup"><span data-stu-id="0b40d-156">To get a specific app, use the **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="0b40d-157">Configure an existing app</span><span class="sxs-lookup"><span data-stu-id="0b40d-157">Configure an existing app</span></span>
<span data-ttu-id="0b40d-158">To change the settings and configurations for an existing app, use the **azure webapp config set** command.</span><span class="sxs-lookup"><span data-stu-id="0b40d-158">To change the settings and configurations for an existing app, use the **azure webapp config set** command.</span></span>

<span data-ttu-id="0b40d-159">Example (1): change the php version of a app</span><span class="sxs-lookup"><span data-stu-id="0b40d-159">Example (1): change the php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="0b40d-160">Example (2): add or change app settings</span><span class="sxs-lookup"><span data-stu-id="0b40d-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="0b40d-161">To know what other configuration can be changed, use the **azure webapp config set -h** command.</span><span class="sxs-lookup"><span data-stu-id="0b40d-161">To know what other configuration can be changed, use the **azure webapp config set -h** command.</span></span>

### <a name="change-the-state-of-an-existing-app"></a><span data-ttu-id="0b40d-162">Change the state of an existing app</span><span class="sxs-lookup"><span data-stu-id="0b40d-162">Change the state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="0b40d-163">Restart an app</span><span class="sxs-lookup"><span data-stu-id="0b40d-163">Restart an app</span></span>
<span data-ttu-id="0b40d-164">To restart an app, you must specify the name and resource group of the app.</span><span class="sxs-lookup"><span data-stu-id="0b40d-164">To restart an app, you must specify the name and resource group of the app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="0b40d-165">Stop an app</span><span class="sxs-lookup"><span data-stu-id="0b40d-165">Stop an app</span></span>
<span data-ttu-id="0b40d-166">To stop an app, you must specify the name and resource group of the app.</span><span class="sxs-lookup"><span data-stu-id="0b40d-166">To stop an app, you must specify the name and resource group of the app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="0b40d-167">Start an app</span><span class="sxs-lookup"><span data-stu-id="0b40d-167">Start an app</span></span>
<span data-ttu-id="0b40d-168">To start an app, you must specify the name and resource group of the app.</span><span class="sxs-lookup"><span data-stu-id="0b40d-168">To start an app, you must specify the name and resource group of the app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="0b40d-169">Manage publishing profiles of an app</span><span class="sxs-lookup"><span data-stu-id="0b40d-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="0b40d-170">Each app has a publishing profile that can be used to publish your code.</span><span class="sxs-lookup"><span data-stu-id="0b40d-170">Each app has a publishing profile that can be used to publish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="0b40d-171">Get Publishing Profile</span><span class="sxs-lookup"><span data-stu-id="0b40d-171">Get Publishing Profile</span></span>
<span data-ttu-id="0b40d-172">To get the publishing profile for a app, use:</span><span class="sxs-lookup"><span data-stu-id="0b40d-172">To get the publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="0b40d-173">This command echoes the publishing profile username and password to the command line.</span><span class="sxs-lookup"><span data-stu-id="0b40d-173">This command echoes the publishing profile username and password to the command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="0b40d-174">Manage app hostnames</span><span class="sxs-lookup"><span data-stu-id="0b40d-174">Manage app hostnames</span></span>
<span data-ttu-id="0b40d-175">To manage hostname bindings for your app, use the **azure webapp config hostnames** command</span><span class="sxs-lookup"><span data-stu-id="0b40d-175">To manage hostname bindings for your app, use the **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="0b40d-176">List hostname bindings</span><span class="sxs-lookup"><span data-stu-id="0b40d-176">List hostname bindings</span></span>
<span data-ttu-id="0b40d-177">To get the current hostname bindings for an app, use:</span><span class="sxs-lookup"><span data-stu-id="0b40d-177">To get the current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="0b40d-178">Add hostname bindings</span><span class="sxs-lookup"><span data-stu-id="0b40d-178">Add hostname bindings</span></span>
<span data-ttu-id="0b40d-179">To add hostname bindings to an app, use:</span><span class="sxs-lookup"><span data-stu-id="0b40d-179">To add hostname bindings to an app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="0b40d-180">Delete hostname bindings</span><span class="sxs-lookup"><span data-stu-id="0b40d-180">Delete hostname bindings</span></span>
<span data-ttu-id="0b40d-181">To delete hostname bindings, use:</span><span class="sxs-lookup"><span data-stu-id="0b40d-181">To delete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="0b40d-182">Next Steps</span><span class="sxs-lookup"><span data-stu-id="0b40d-182">Next Steps</span></span>
* <span data-ttu-id="0b40d-183">To learn about Azure Resource Manager CLI support, see [Use the Azure CLI to manage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="0b40d-183">To learn about Azure Resource Manager CLI support, see [Use the Azure CLI to manage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="0b40d-184">To learn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="0b40d-184">To learn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="0b40d-185">To learn about Azure App Service on Linux, see [Introduction to App Service on Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="0b40d-185">To learn about Azure App Service on Linux, see [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>
