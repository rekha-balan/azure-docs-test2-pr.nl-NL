---
title: Collect logs by using Azure Diagnostics | Microsoft Docs
description: This article describes how to set up Azure Diagnostics to collect logs from a Service Fabric cluster running in Azure.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: ''
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/17/2017
ms.author: dekapur
ms.openlocfilehash: 5979839814ef5987fe168e42811618a8750bd226
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564538"
---
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="48e3e-103">Collect logs by using Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="48e3e-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="48e3e-106">When you're running an Azure Service Fabric cluster, it's a good idea to collect the logs from all the nodes in a central location.</span><span class="sxs-lookup"><span data-stu-id="48e3e-106">When you're running an Azure Service Fabric cluster, it's a good idea to collect the logs from all the nodes in a central location.</span></span> <span data-ttu-id="48e3e-107">Having the logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in the applications and services running in that cluster.</span><span class="sxs-lookup"><span data-stu-id="48e3e-107">Having the logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in the applications and services running in that cluster.</span></span>

<span data-ttu-id="48e3e-108">One way to upload and collect logs is to use the Azure Diagnostics extension, which uploads logs to Azure Storage, Azure Application Insights, or Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="48e3e-108">One way to upload and collect logs is to use the Azure Diagnostics extension, which uploads logs to Azure Storage, Azure Application Insights, or Azure Event Hubs.</span></span> <span data-ttu-id="48e3e-109">The logs are not that useful directly in storage or in Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="48e3e-109">The logs are not that useful directly in storage or in Event Hubs.</span></span> <span data-ttu-id="48e3e-110">But you can use an external process to read the events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span><span class="sxs-lookup"><span data-stu-id="48e3e-110">But you can use an external process to read the events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="48e3e-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span><span class="sxs-lookup"><span data-stu-id="48e3e-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48e3e-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="48e3e-112">Prerequisites</span></span>
<span data-ttu-id="48e3e-113">You use these tools to perform some of the operations in this document:</span><span class="sxs-lookup"><span data-stu-id="48e3e-113">You use these tools to perform some of the operations in this document:</span></span>

* <span data-ttu-id="48e3e-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related to Azure Cloud Services but has good information and examples)</span><span class="sxs-lookup"><span data-stu-id="48e3e-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related to Azure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="48e3e-115">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="48e3e-115">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="48e3e-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="48e3e-116">Azure PowerShell</span></span>](/powershell/azureps-cmdlets-docs)
* [<span data-ttu-id="48e3e-117">Azure Resource Manager client</span><span class="sxs-lookup"><span data-stu-id="48e3e-117">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="48e3e-118">Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="48e3e-118">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-to-collect"></a><span data-ttu-id="48e3e-119">Log sources that you might want to collect</span><span class="sxs-lookup"><span data-stu-id="48e3e-119">Log sources that you might want to collect</span></span>
* <span data-ttu-id="48e3e-120">**Service Fabric logs**: Emitted from the platform to standard Event Tracing for Windows (ETW) and EventSource channels.</span><span class="sxs-lookup"><span data-stu-id="48e3e-120">**Service Fabric logs**: Emitted from the platform to standard Event Tracing for Windows (ETW) and EventSource channels.</span></span> <span data-ttu-id="48e3e-121">Logs can be one of several types:</span><span class="sxs-lookup"><span data-stu-id="48e3e-121">Logs can be one of several types:</span></span>
  * <span data-ttu-id="48e3e-122">Operational events: Logs for operations that the Service Fabric platform performs.</span><span class="sxs-lookup"><span data-stu-id="48e3e-122">Operational events: Logs for operations that the Service Fabric platform performs.</span></span> <span data-ttu-id="48e3e-123">Examples include creation of applications and services, node state changes, and upgrade information.</span><span class="sxs-lookup"><span data-stu-id="48e3e-123">Examples include creation of applications and services, node state changes, and upgrade information.</span></span>
  * [<span data-ttu-id="48e3e-124">Reliable Actors programming model events</span><span class="sxs-lookup"><span data-stu-id="48e3e-124">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="48e3e-125">Reliable Services programming model events</span><span class="sxs-lookup"><span data-stu-id="48e3e-125">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)
* <span data-ttu-id="48e3e-126">**Application events**: Events emitted from your service's code and written out by using the EventSource helper class provided in the Visual Studio templates.</span><span class="sxs-lookup"><span data-stu-id="48e3e-126">**Application events**: Events emitted from your service's code and written out by using the EventSource helper class provided in the Visual Studio templates.</span></span> <span data-ttu-id="48e3e-127">For more information on how to write logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="48e3e-127">For more information on how to write logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-the-diagnostics-extension"></a><span data-ttu-id="48e3e-128">Deploy the Diagnostics extension</span><span class="sxs-lookup"><span data-stu-id="48e3e-128">Deploy the Diagnostics extension</span></span>
<span data-ttu-id="48e3e-129">The first step in collecting logs is to deploy the Diagnostics extension on each of the VMs in the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="48e3e-129">The first step in collecting logs is to deploy the Diagnostics extension on each of the VMs in the Service Fabric cluster.</span></span> <span data-ttu-id="48e3e-130">The Diagnostics extension collects logs on each VM and uploads them to the storage account that you specify.</span><span class="sxs-lookup"><span data-stu-id="48e3e-130">The Diagnostics extension collects logs on each VM and uploads them to the storage account that you specify.</span></span> <span data-ttu-id="48e3e-131">The steps vary a little based on whether you use the Azure portal or Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="48e3e-131">The steps vary a little based on whether you use the Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="48e3e-132">The steps also vary based on whether the deployment is part of cluster creation or is for a cluster that already exists.</span><span class="sxs-lookup"><span data-stu-id="48e3e-132">The steps also vary based on whether the deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="48e3e-133">Let's look at the steps for each scenario.</span><span class="sxs-lookup"><span data-stu-id="48e3e-133">Let's look at the steps for each scenario.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-through-the-portal"></a><span data-ttu-id="48e3e-134">Deploy the Diagnostics extension as part of cluster creation through the portal</span><span class="sxs-lookup"><span data-stu-id="48e3e-134">Deploy the Diagnostics extension as part of cluster creation through the portal</span></span>
<span data-ttu-id="48e3e-135">To deploy the Diagnostics extension to the VMs in the cluster as part of cluster creation, you use the Diagnostics settings panel shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="48e3e-135">To deploy the Diagnostics extension to the VMs in the cluster as part of cluster creation, you use the Diagnostics settings panel shown in the following image.</span></span> <span data-ttu-id="48e3e-136">To enable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set to **On** (the default setting).</span><span class="sxs-lookup"><span data-stu-id="48e3e-136">To enable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set to **On** (the default setting).</span></span> <span data-ttu-id="48e3e-137">After you create the cluster, you can't change these settings by using the portal.</span><span class="sxs-lookup"><span data-stu-id="48e3e-137">After you create the cluster, you can't change these settings by using the portal.</span></span>

![Azure Diagnostics settings in the portal for cluster creation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

<span data-ttu-id="48e3e-139">The Azure support team *requires* support logs to help resolve any support requests that you create.</span><span class="sxs-lookup"><span data-stu-id="48e3e-139">The Azure support team *requires* support logs to help resolve any support requests that you create.</span></span> <span data-ttu-id="48e3e-140">These logs are collected in real time and are stored in one of the storage accounts created in the resource group.</span><span class="sxs-lookup"><span data-stu-id="48e3e-140">These logs are collected in real time and are stored in one of the storage accounts created in the resource group.</span></span> <span data-ttu-id="48e3e-141">The Diagnostics settings configure application-level events.</span><span class="sxs-lookup"><span data-stu-id="48e3e-141">The Diagnostics settings configure application-level events.</span></span> <span data-ttu-id="48e3e-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events to be stored in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="48e3e-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events to be stored in Azure Storage.</span></span>

<span data-ttu-id="48e3e-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get the events from the storage account.</span><span class="sxs-lookup"><span data-stu-id="48e3e-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get the events from the storage account.</span></span> <span data-ttu-id="48e3e-144">There is currently no way to filter or groom the events that are sent to the table.</span><span class="sxs-lookup"><span data-stu-id="48e3e-144">There is currently no way to filter or groom the events that are sent to the table.</span></span> <span data-ttu-id="48e3e-145">If you don't implement a process to remove events from the table, the table will continue to grow.</span><span class="sxs-lookup"><span data-stu-id="48e3e-145">If you don't implement a process to remove events from the table, the table will continue to grow.</span></span>

<span data-ttu-id="48e3e-146">When you're creating a cluster by using the portal, we highly recommend that you download the template **before you click OK** to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="48e3e-146">When you're creating a cluster by using the portal, we highly recommend that you download the template **before you click OK** to create the cluster.</span></span> <span data-ttu-id="48e3e-147">For details, refer to [Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="48e3e-147">For details, refer to [Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="48e3e-148">You'll need the template to make changes later, because you can't make some changes by using the portal.</span><span class="sxs-lookup"><span data-stu-id="48e3e-148">You'll need the template to make changes later, because you can't make some changes by using the portal.</span></span>

<span data-ttu-id="48e3e-149">You can export templates from the portal by using the following steps.</span><span class="sxs-lookup"><span data-stu-id="48e3e-149">You can export templates from the portal by using the following steps.</span></span> <span data-ttu-id="48e3e-150">However, these templates can be more difficult to use because they might have null values that are missing required information.</span><span class="sxs-lookup"><span data-stu-id="48e3e-150">However, these templates can be more difficult to use because they might have null values that are missing required information.</span></span>

1. <span data-ttu-id="48e3e-151">Open your resource group.</span><span class="sxs-lookup"><span data-stu-id="48e3e-151">Open your resource group.</span></span>
2. <span data-ttu-id="48e3e-152">Select **Settings** to display the settings panel.</span><span class="sxs-lookup"><span data-stu-id="48e3e-152">Select **Settings** to display the settings panel.</span></span>
3. <span data-ttu-id="48e3e-153">Select **Deployments** to display the deployment history panel.</span><span class="sxs-lookup"><span data-stu-id="48e3e-153">Select **Deployments** to display the deployment history panel.</span></span>
4. <span data-ttu-id="48e3e-154">Select a deployment to display the details of the deployment.</span><span class="sxs-lookup"><span data-stu-id="48e3e-154">Select a deployment to display the details of the deployment.</span></span>
5. <span data-ttu-id="48e3e-155">Select **Export Template** to display the template panel.</span><span class="sxs-lookup"><span data-stu-id="48e3e-155">Select **Export Template** to display the template panel.</span></span>
6. <span data-ttu-id="48e3e-156">Select **Save to file** to export a .zip file that contains the template, parameter, and PowerShell files.</span><span class="sxs-lookup"><span data-stu-id="48e3e-156">Select **Save to file** to export a .zip file that contains the template, parameter, and PowerShell files.</span></span>

<span data-ttu-id="48e3e-157">After you export the files, you need to make a modification.</span><span class="sxs-lookup"><span data-stu-id="48e3e-157">After you export the files, you need to make a modification.</span></span> <span data-ttu-id="48e3e-158">Edit the parameters.json file and remove the **adminPassword** element.</span><span class="sxs-lookup"><span data-stu-id="48e3e-158">Edit the parameters.json file and remove the **adminPassword** element.</span></span> <span data-ttu-id="48e3e-159">This will cause a prompt for the password when the deployment script is run.</span><span class="sxs-lookup"><span data-stu-id="48e3e-159">This will cause a prompt for the password when the deployment script is run.</span></span> <span data-ttu-id="48e3e-160">When you're running the deployment script, you might have to fix null parameter values.</span><span class="sxs-lookup"><span data-stu-id="48e3e-160">When you're running the deployment script, you might have to fix null parameter values.</span></span>

<span data-ttu-id="48e3e-161">To use the downloaded template to update a configuration:</span><span class="sxs-lookup"><span data-stu-id="48e3e-161">To use the downloaded template to update a configuration:</span></span>

1. <span data-ttu-id="48e3e-162">Extract the contents to a folder on your local computer.</span><span class="sxs-lookup"><span data-stu-id="48e3e-162">Extract the contents to a folder on your local computer.</span></span>
2. <span data-ttu-id="48e3e-163">Modify the contents to reflect the new configuration.</span><span class="sxs-lookup"><span data-stu-id="48e3e-163">Modify the contents to reflect the new configuration.</span></span>
3. <span data-ttu-id="48e3e-164">Start PowerShell and change to the folder where you extracted the content.</span><span class="sxs-lookup"><span data-stu-id="48e3e-164">Start PowerShell and change to the folder where you extracted the content.</span></span>
4. <span data-ttu-id="48e3e-165">Run **deploy.ps1** and fill in the subscription ID, the resource group name (use the same name to update the configuration), and a unique deployment name.</span><span class="sxs-lookup"><span data-stu-id="48e3e-165">Run **deploy.ps1** and fill in the subscription ID, the resource group name (use the same name to update the configuration), and a unique deployment name.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="48e3e-166">Deploy the Diagnostics extension as part of cluster creation by using Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="48e3e-166">Deploy the Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="48e3e-167">To create a cluster by using Resource Manager, you need to add the Diagnostics configuration JSON to the full cluster Resource Manager template before you create the cluster.</span><span class="sxs-lookup"><span data-stu-id="48e3e-167">To create a cluster by using Resource Manager, you need to add the Diagnostics configuration JSON to the full cluster Resource Manager template before you create the cluster.</span></span> <span data-ttu-id="48e3e-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added to it as part of our Resource Manager template samples.</span><span class="sxs-lookup"><span data-stu-id="48e3e-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added to it as part of our Resource Manager template samples.</span></span> <span data-ttu-id="48e3e-169">You can see it at this location in the Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span><span class="sxs-lookup"><span data-stu-id="48e3e-169">You can see it at this location in the Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span></span>

<span data-ttu-id="48e3e-170">To see the Diagnostics setting in the Resource Manager template, open the azuredeploy.json file and search for **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="48e3e-170">To see the Diagnostics setting in the Resource Manager template, open the azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="48e3e-171">To create a cluster by using this template, select the **Deploy to Azure** button available at the previous link.</span><span class="sxs-lookup"><span data-stu-id="48e3e-171">To create a cluster by using this template, select the **Deploy to Azure** button available at the previous link.</span></span>

<span data-ttu-id="48e3e-172">Alternatively, you can download the Resource Manager sample, make changes to it, and create a cluster with the modified template by using the `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span><span class="sxs-lookup"><span data-stu-id="48e3e-172">Alternatively, you can download the Resource Manager sample, make changes to it, and create a cluster with the modified template by using the `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="48e3e-173">See the following code for the parameters that you pass in to the command.</span><span class="sxs-lookup"><span data-stu-id="48e3e-173">See the following code for the parameters that you pass in to the command.</span></span> <span data-ttu-id="48e3e-174">For detailed information on how to deploy a resource group by using PowerShell, see the article [Deploy a resource group with the Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="48e3e-174">For detailed information on how to deploy a resource group by using PowerShell, see the article [Deploy a resource group with the Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-the-diagnostics-extension-to-an-existing-cluster"></a><span data-ttu-id="48e3e-175">Deploy the Diagnostics extension to an existing cluster</span><span class="sxs-lookup"><span data-stu-id="48e3e-175">Deploy the Diagnostics extension to an existing cluster</span></span>
<span data-ttu-id="48e3e-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want to modify an existing configuration, you can add or update it.</span><span class="sxs-lookup"><span data-stu-id="48e3e-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want to modify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="48e3e-177">Modify the Resource Manager template that's used to create the existing cluster or download the template from the portal as described earlier.</span><span class="sxs-lookup"><span data-stu-id="48e3e-177">Modify the Resource Manager template that's used to create the existing cluster or download the template from the portal as described earlier.</span></span> <span data-ttu-id="48e3e-178">Modify the template.json file by performing the following tasks.</span><span class="sxs-lookup"><span data-stu-id="48e3e-178">Modify the template.json file by performing the following tasks.</span></span>

<span data-ttu-id="48e3e-179">Add a new storage resource to the template by adding to the resources section.</span><span class="sxs-lookup"><span data-stu-id="48e3e-179">Add a new storage resource to the template by adding to the resources section.</span></span>

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 <span data-ttu-id="48e3e-180">Next, add to the parameters section just after the storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="48e3e-180">Next, add to the parameters section just after the storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="48e3e-181">Replace the placeholder text *storage account name goes here* with the name of the storage account.</span><span class="sxs-lookup"><span data-stu-id="48e3e-181">Replace the placeholder text *storage account name goes here* with the name of the storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for the application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for the storage account that contains application diagnostics data from the cluster"
      }
    },
```
<span data-ttu-id="48e3e-182">Then, update the `VirtualMachineProfile` section of the template.json file by adding the following code within the extensions array.</span><span class="sxs-lookup"><span data-stu-id="48e3e-182">Then, update the `VirtualMachineProfile` section of the template.json file by adding the following code within the extensions array.</span></span> <span data-ttu-id="48e3e-183">Be sure to add a comma at the beginning or the end, depending on where it's inserted.</span><span class="sxs-lookup"><span data-stu-id="48e3e-183">Be sure to add a comma at the beginning or the end, depending on where it's inserted.</span></span>

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

<span data-ttu-id="48e3e-184">After you modify the template.json file as described, republish the Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="48e3e-184">After you modify the template.json file as described, republish the Resource Manager template.</span></span> <span data-ttu-id="48e3e-185">If the template was exported, running the deploy.ps1 file republishes the template.</span><span class="sxs-lookup"><span data-stu-id="48e3e-185">If the template was exported, running the deploy.ps1 file republishes the template.</span></span> <span data-ttu-id="48e3e-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="48e3e-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="update-diagnostics-to-collect-health-and-load-events"></a><span data-ttu-id="48e3e-187">Update diagnostics to collect health and load events</span><span class="sxs-lookup"><span data-stu-id="48e3e-187">Update diagnostics to collect health and load events</span></span>

<span data-ttu-id="48e3e-188">Starting with the 5.4 release of Service Fabric, health and load metric events are available for collection.</span><span class="sxs-lookup"><span data-stu-id="48e3e-188">Starting with the 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="48e3e-189">These events reflect events generated by the system or your code by using the health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="48e3e-189">These events reflect events generated by the system or your code by using the health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="48e3e-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span><span class="sxs-lookup"><span data-stu-id="48e3e-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="48e3e-191">To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" to the list of ETW providers.</span><span class="sxs-lookup"><span data-stu-id="48e3e-191">To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" to the list of ETW providers.</span></span>

<span data-ttu-id="48e3e-192">To collect the events, modify the resource manager template to include</span><span class="sxs-lookup"><span data-stu-id="48e3e-192">To collect the events, modify the resource manager template to include</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="update-diagnostics-to-collect-and-upload-logs-from-new-eventsource-channels"></a><span data-ttu-id="48e3e-193">Update Diagnostics to collect and upload logs from new EventSource channels</span><span class="sxs-lookup"><span data-stu-id="48e3e-193">Update Diagnostics to collect and upload logs from new EventSource channels</span></span>
<span data-ttu-id="48e3e-194">To update Diagnostics to collect logs from new EventSource channels that represent a new application that you're about to deploy, perform the same steps as in the [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span><span class="sxs-lookup"><span data-stu-id="48e3e-194">To update Diagnostics to collect logs from new EventSource channels that represent a new application that you're about to deploy, perform the same steps as in the [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="48e3e-195">Update the `EtwEventSourceProviderConfiguration` section in the template.json file to add entries for the new EventSource channels before you apply the configuration update by using the `New-AzureRmResourceGroupDeployment` PowerShell command.</span><span class="sxs-lookup"><span data-stu-id="48e3e-195">Update the `EtwEventSourceProviderConfiguration` section in the template.json file to add entries for the new EventSource channels before you apply the configuration update by using the `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="48e3e-196">The name of the event source is defined as part of your code in the Visual Studio-generated ServiceEventSource.cs file.</span><span class="sxs-lookup"><span data-stu-id="48e3e-196">The name of the event source is defined as part of your code in the Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="48e3e-197">For example, if your event source is named My-Eventsource, add the following code to place the events from My-Eventsource into a table named MyDestinationTableName.</span><span class="sxs-lookup"><span data-stu-id="48e3e-197">For example, if your event source is named My-Eventsource, add the following code to place the events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="48e3e-198">To collect performance counters or event logs, modify the Resource Manager template by using the examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="48e3e-198">To collect performance counters or event logs, modify the Resource Manager template by using the examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="48e3e-199">Then, republish the Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="48e3e-199">Then, republish the Resource Manager template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48e3e-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="48e3e-200">Next steps</span></span>
<span data-ttu-id="48e3e-201">To understand in more detail what events you should look for while troubleshooting issues, see the diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="48e3e-201">To understand in more detail what events you should look for while troubleshooting issues, see the diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="48e3e-202">Related articles</span><span class="sxs-lookup"><span data-stu-id="48e3e-202">Related articles</span></span>
* [<span data-ttu-id="48e3e-203">Learn how to collect performance counters or logs by using the Diagnostics extension</span><span class="sxs-lookup"><span data-stu-id="48e3e-203">Learn how to collect performance counters or logs by using the Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="48e3e-204">Service Fabric solution in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="48e3e-204">Service Fabric solution in Log Analytics</span></span>](../log-analytics/log-analytics-service-fabric.md)


