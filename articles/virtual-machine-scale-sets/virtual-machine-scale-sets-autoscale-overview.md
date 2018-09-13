---
title: Automatic scaling and virtual machine scale sets | Microsoft Docs
description: Learn about using diagnostics and autoscale resources to automatically scale virtual machines in a scale set.
services: virtual-machine-scale-sets
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: d29a3385-179e-4331-a315-daa7ea5701df
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: adegeo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cd797ecdb46dfa23ee129e8b55e41749712cc4a8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554995"
---
# <a name="how-to-use-automatic-scaling-and-virtual-machine-scale-sets"></a><span data-ttu-id="5eef4-103">How to use automatic scaling and Virtual Machine Scale Sets</span><span class="sxs-lookup"><span data-stu-id="5eef4-103">How to use automatic scaling and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="5eef4-104">Automatic scaling of virtual machines in a scale set is the creation or deletion of machines in the set as needed to match performance requirements.</span><span class="sxs-lookup"><span data-stu-id="5eef4-104">Automatic scaling of virtual machines in a scale set is the creation or deletion of machines in the set as needed to match performance requirements.</span></span> <span data-ttu-id="5eef4-105">As the volume of work grows, an application may require additional resources to enable it to effectively perform tasks.</span><span class="sxs-lookup"><span data-stu-id="5eef4-105">As the volume of work grows, an application may require additional resources to enable it to effectively perform tasks.</span></span>

<span data-ttu-id="5eef4-106">Automatic scaling is an automated process that helps ease management overhead.</span><span class="sxs-lookup"><span data-stu-id="5eef4-106">Automatic scaling is an automated process that helps ease management overhead.</span></span> <span data-ttu-id="5eef4-107">By reducing overhead, you don't need to continually monitor system performance or decide how to manage resources.</span><span class="sxs-lookup"><span data-stu-id="5eef4-107">By reducing overhead, you don't need to continually monitor system performance or decide how to manage resources.</span></span> <span data-ttu-id="5eef4-108">Scaling is an elastic process.</span><span class="sxs-lookup"><span data-stu-id="5eef4-108">Scaling is an elastic process.</span></span> <span data-ttu-id="5eef4-109">More resources can be added as the load increases, but as demand decreases resources can be removed to minimize costs and maintain performance levels.</span><span class="sxs-lookup"><span data-stu-id="5eef4-109">More resources can be added as the load increases, but as demand decreases resources can be removed to minimize costs and maintain performance levels.</span></span>

<span data-ttu-id="5eef4-110">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5eef4-110">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or the Azure portal.</span></span>

## <a name="set-up-scaling-by-using-resource-manager-templates"></a><span data-ttu-id="5eef4-111">Set up scaling by using Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="5eef4-111">Set up scaling by using Resource Manager templates</span></span>
<span data-ttu-id="5eef4-112">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span><span class="sxs-lookup"><span data-stu-id="5eef4-112">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span></span> <span data-ttu-id="5eef4-113">In the template, application resources are defined and deployment parameters are specified for different environments.</span><span class="sxs-lookup"><span data-stu-id="5eef4-113">In the template, application resources are defined and deployment parameters are specified for different environments.</span></span> <span data-ttu-id="5eef4-114">The template consists of JSON and expressions that you can use to construct values for your deployment.</span><span class="sxs-lookup"><span data-stu-id="5eef4-114">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="5eef4-115">To learn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5eef4-115">To learn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="5eef4-116">In the template, you specify the capacity element:</span><span class="sxs-lookup"><span data-stu-id="5eef4-116">In the template, you specify the capacity element:</span></span>

    "sku": {
      "name": "Standard_A0",
      "tier": "Standard",
      "capacity": 3
    },

<span data-ttu-id="5eef4-117">Capacity identifies the number of virtual machines in the set.</span><span class="sxs-lookup"><span data-stu-id="5eef4-117">Capacity identifies the number of virtual machines in the set.</span></span> <span data-ttu-id="5eef4-118">You can manually change the capacity by deploying a template with a different value.</span><span class="sxs-lookup"><span data-stu-id="5eef4-118">You can manually change the capacity by deploying a template with a different value.</span></span> <span data-ttu-id="5eef4-119">If you are deploying a template to only change the capacity, you can include only the SKU element with the updated capacity.</span><span class="sxs-lookup"><span data-stu-id="5eef4-119">If you are deploying a template to only change the capacity, you can include only the SKU element with the updated capacity.</span></span>

<span data-ttu-id="5eef4-120">Automatically change the capacity of your scale set by using the combination of the autoscaleSettings resource and the diagnostics extension.</span><span class="sxs-lookup"><span data-stu-id="5eef4-120">Automatically change the capacity of your scale set by using the combination of the autoscaleSettings resource and the diagnostics extension.</span></span>

### <a name="configure-the-azure-diagnostics-extension"></a><span data-ttu-id="5eef4-121">Configure the Azure Diagnostics extension</span><span class="sxs-lookup"><span data-stu-id="5eef4-121">Configure the Azure Diagnostics extension</span></span>
<span data-ttu-id="5eef4-122">Automatic scaling can only be done if metrics collection is successful on each virtual machine in the scale set.</span><span class="sxs-lookup"><span data-stu-id="5eef4-122">Automatic scaling can only be done if metrics collection is successful on each virtual machine in the scale set.</span></span> <span data-ttu-id="5eef4-123">The Azure Diagnostics Extension provides the monitoring and diagnostics capabilities that meets the metrics collection needs of the autoscale resource.</span><span class="sxs-lookup"><span data-stu-id="5eef4-123">The Azure Diagnostics Extension provides the monitoring and diagnostics capabilities that meets the metrics collection needs of the autoscale resource.</span></span> <span data-ttu-id="5eef4-124">You can install the extension as part of the Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="5eef4-124">You can install the extension as part of the Resource Manager template.</span></span>

<span data-ttu-id="5eef4-125">This example shows the variables that are used in the template to configure the diagnostics extension:</span><span class="sxs-lookup"><span data-stu-id="5eef4-125">This example shows the variables that are used in the template to configure the diagnostics extension:</span></span>

    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
    "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"

<span data-ttu-id="5eef4-126">Parameters are provided when the template is deployed.</span><span class="sxs-lookup"><span data-stu-id="5eef4-126">Parameters are provided when the template is deployed.</span></span> <span data-ttu-id="5eef4-127">In this example, the name of the storage account where data is stored and the name of the scale set from which data is collected are provided.</span><span class="sxs-lookup"><span data-stu-id="5eef4-127">In this example, the name of the storage account where data is stored and the name of the scale set from which data is collected are provided.</span></span> <span data-ttu-id="5eef4-128">Also in this Windows Server example, only the Thread Count performance counter is collected.</span><span class="sxs-lookup"><span data-stu-id="5eef4-128">Also in this Windows Server example, only the Thread Count performance counter is collected.</span></span> <span data-ttu-id="5eef4-129">All the available performance counters in Windows or Linux can be used to collect diagnostics information and can be included in the extension configuration.</span><span class="sxs-lookup"><span data-stu-id="5eef4-129">All the available performance counters in Windows or Linux can be used to collect diagnostics information and can be included in the extension configuration.</span></span>

<span data-ttu-id="5eef4-130">This example shows the definition of the extension in the template:</span><span class="sxs-lookup"><span data-stu-id="5eef4-130">This example shows the definition of the extension in the template:</span></span>

    "extensionProfile": {
      "extensions": [
        {
          "name": "Microsoft.Insights.VMDiagnosticsSettings",
          "properties": {
            "publisher": "Microsoft.Azure.Diagnostics",
            "type": "IaaSDiagnostics",
            "typeHandlerVersion": "1.5",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
              "storageAccount": "[variables('diagnosticsStorageAccountName')]"
            },
            "protectedSettings": {
              "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
              "storageAccountKey": "[listkeys(variables('accountid'), variables('apiVersion')).key1]",
              "storageAccountEndPoint": "https://core.windows.net"
            }
          }
        }
      ]
    }

<span data-ttu-id="5eef4-131">When the diagnostics extension runs, the data is collected in a table that is located in the storage account that you specify.</span><span class="sxs-lookup"><span data-stu-id="5eef4-131">When the diagnostics extension runs, the data is collected in a table that is located in the storage account that you specify.</span></span> <span data-ttu-id="5eef4-132">In the WADPerformanceCounters table, you can find the collected data:</span><span class="sxs-lookup"><span data-stu-id="5eef4-132">In the WADPerformanceCounters table, you can find the collected data:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-the-autoscalesettings-resource"></a><span data-ttu-id="5eef4-133">Configure the autoScaleSettings resource</span><span class="sxs-lookup"><span data-stu-id="5eef4-133">Configure the autoScaleSettings resource</span></span>
<span data-ttu-id="5eef4-134">The autoscaleSettings resource uses the information from the diagnostics extension to decide whether to increase or decrease the number of virtual machines in the scale set.</span><span class="sxs-lookup"><span data-stu-id="5eef4-134">The autoscaleSettings resource uses the information from the diagnostics extension to decide whether to increase or decrease the number of virtual machines in the scale set.</span></span>

<span data-ttu-id="5eef4-135">This example shows the configuration of the resource in the template:</span><span class="sxs-lookup"><span data-stu-id="5eef4-135">This example shows the configuration of the resource in the template:</span></span>

    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Process(_Total)\\Thread Count",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 650
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "\\Process(_Total)\\Thread Count",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 550
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
      }
    }

<span data-ttu-id="5eef4-136">In the example above, two rules are created for defining the automatic scaling actions.</span><span class="sxs-lookup"><span data-stu-id="5eef4-136">In the example above, two rules are created for defining the automatic scaling actions.</span></span> <span data-ttu-id="5eef4-137">The first rule defines the scale-out action and the second rule defines the scale-in action.</span><span class="sxs-lookup"><span data-stu-id="5eef4-137">The first rule defines the scale-out action and the second rule defines the scale-in action.</span></span> <span data-ttu-id="5eef4-138">These values are provided in the rules:</span><span class="sxs-lookup"><span data-stu-id="5eef4-138">These values are provided in the rules:</span></span>

* <span data-ttu-id="5eef4-139">**metricName** - This value is the same as the performance counter that you defined in the wadperfcounter variable for the diagnostics extension.</span><span class="sxs-lookup"><span data-stu-id="5eef4-139">**metricName** - This value is the same as the performance counter that you defined in the wadperfcounter variable for the diagnostics extension.</span></span> <span data-ttu-id="5eef4-140">In the example above, the Thread Count counter is used.</span><span class="sxs-lookup"><span data-stu-id="5eef4-140">In the example above, the Thread Count counter is used.</span></span>  
* <span data-ttu-id="5eef4-141">**metricResourceUri** - This value is the resource identifier of the virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="5eef4-141">**metricResourceUri** - This value is the resource identifier of the virtual machine scale set.</span></span> <span data-ttu-id="5eef4-142">This identifier contains the name of the resource group, the name of the resource provider, and the name of the scale set to scale.</span><span class="sxs-lookup"><span data-stu-id="5eef4-142">This identifier contains the name of the resource group, the name of the resource provider, and the name of the scale set to scale.</span></span>
* <span data-ttu-id="5eef4-143">**timeGrain** – This value is the granularity of the metrics that are collected.</span><span class="sxs-lookup"><span data-stu-id="5eef4-143">**timeGrain** – This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="5eef4-144">In the preceding example, data is collected on an interval of one minute.</span><span class="sxs-lookup"><span data-stu-id="5eef4-144">In the preceding example, data is collected on an interval of one minute.</span></span> <span data-ttu-id="5eef4-145">This value is used with timeWindow.</span><span class="sxs-lookup"><span data-stu-id="5eef4-145">This value is used with timeWindow.</span></span>
* <span data-ttu-id="5eef4-146">**statistic** – This value determines how the metrics are combined to accommodate the automatic scaling action.</span><span class="sxs-lookup"><span data-stu-id="5eef4-146">**statistic** – This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="5eef4-147">The possible values are: Average, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="5eef4-147">The possible values are: Average, Min, Max.</span></span>
* <span data-ttu-id="5eef4-148">**timeWindow** – This value is the range of time in which instance data is collected.</span><span class="sxs-lookup"><span data-stu-id="5eef4-148">**timeWindow** – This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="5eef4-149">It must be between 5 minutes and 12 hours.</span><span class="sxs-lookup"><span data-stu-id="5eef4-149">It must be between 5 minutes and 12 hours.</span></span>
* <span data-ttu-id="5eef4-150">**timeAggregation** –This value determines how the data that is collected should be combined over time.</span><span class="sxs-lookup"><span data-stu-id="5eef4-150">**timeAggregation** –This value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="5eef4-151">The default value is Average.</span><span class="sxs-lookup"><span data-stu-id="5eef4-151">The default value is Average.</span></span> <span data-ttu-id="5eef4-152">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span><span class="sxs-lookup"><span data-stu-id="5eef4-152">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
* <span data-ttu-id="5eef4-153">**operator** – This value is the operator that is used to compare the metric data and the threshold.</span><span class="sxs-lookup"><span data-stu-id="5eef4-153">**operator** – This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="5eef4-154">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="5eef4-154">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
* <span data-ttu-id="5eef4-155">**threshold** – This value is the value that triggers the scale action.</span><span class="sxs-lookup"><span data-stu-id="5eef4-155">**threshold** – This value is the value that triggers the scale action.</span></span> <span data-ttu-id="5eef4-156">Be sure to provide a sufficient difference between the threshold for the scale-out action and the threshold for the scale-in action.</span><span class="sxs-lookup"><span data-stu-id="5eef4-156">Be sure to provide a sufficient difference between the threshold for the scale-out action and the threshold for the scale-in action.</span></span> <span data-ttu-id="5eef4-157">If you set the values to be the same, the system anticipates constant change, which prevents it from implementing a scaling action.</span><span class="sxs-lookup"><span data-stu-id="5eef4-157">If you set the values to be the same, the system anticipates constant change, which prevents it from implementing a scaling action.</span></span> <span data-ttu-id="5eef4-158">For example, setting both to 600 threads in the preceding example doesn't work.</span><span class="sxs-lookup"><span data-stu-id="5eef4-158">For example, setting both to 600 threads in the preceding example doesn't work.</span></span>
* <span data-ttu-id="5eef4-159">**direction** – This value determines the action that is taken when the threshold value is achieved.</span><span class="sxs-lookup"><span data-stu-id="5eef4-159">**direction** – This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="5eef4-160">The possible values are Increase or Decrease.</span><span class="sxs-lookup"><span data-stu-id="5eef4-160">The possible values are Increase or Decrease.</span></span>
* <span data-ttu-id="5eef4-161">**type** – This value is the type of action that should occur and must be set to ChangeCount.</span><span class="sxs-lookup"><span data-stu-id="5eef4-161">**type** – This value is the type of action that should occur and must be set to ChangeCount.</span></span>
* <span data-ttu-id="5eef4-162">**value** – This value is the number of virtual machines that are added to or removed from the scale set.</span><span class="sxs-lookup"><span data-stu-id="5eef4-162">**value** – This value is the number of virtual machines that are added to or removed from the scale set.</span></span> <span data-ttu-id="5eef4-163">This value must be 1 or greater.</span><span class="sxs-lookup"><span data-stu-id="5eef4-163">This value must be 1 or greater.</span></span>
* <span data-ttu-id="5eef4-164">**cooldown** – This value is the amount of time to wait since the last scaling action before the next action occurs.</span><span class="sxs-lookup"><span data-stu-id="5eef4-164">**cooldown** – This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="5eef4-165">This value must be between one minute and one week.</span><span class="sxs-lookup"><span data-stu-id="5eef4-165">This value must be between one minute and one week.</span></span>

<span data-ttu-id="5eef4-166">Depending on the performance counter you are using, some of the elements in the template configuration are used differently.</span><span class="sxs-lookup"><span data-stu-id="5eef4-166">Depending on the performance counter you are using, some of the elements in the template configuration are used differently.</span></span> <span data-ttu-id="5eef4-167">In the preceding example, the performance counter is Thread Count, the threshold value is 650 for a scale-out action, and the threshold value is 550 for the scale-in action.</span><span class="sxs-lookup"><span data-stu-id="5eef4-167">In the preceding example, the performance counter is Thread Count, the threshold value is 650 for a scale-out action, and the threshold value is 550 for the scale-in action.</span></span> <span data-ttu-id="5eef4-168">If you use a counter such as %Processor Time, the threshold value is set to the percentage of CPU usage that determines a scaling action.</span><span class="sxs-lookup"><span data-stu-id="5eef4-168">If you use a counter such as %Processor Time, the threshold value is set to the percentage of CPU usage that determines a scaling action.</span></span>

<span data-ttu-id="5eef4-169">When a load is created on the virtual machines that triggers a scaling action, the capacity of the set is increased based on the value in the template.</span><span class="sxs-lookup"><span data-stu-id="5eef4-169">When a load is created on the virtual machines that triggers a scaling action, the capacity of the set is increased based on the value in the template.</span></span> <span data-ttu-id="5eef4-170">For example, in a scale set where the capacity is set to 3 and the scale action value is set to 1:</span><span class="sxs-lookup"><span data-stu-id="5eef4-170">For example, in a scale set where the capacity is set to 3 and the scale action value is set to 1:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

<span data-ttu-id="5eef4-171">When the load is created that causes the average thread count to go above the threshold of 650:</span><span class="sxs-lookup"><span data-stu-id="5eef4-171">When the load is created that causes the average thread count to go above the threshold of 650:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

<span data-ttu-id="5eef4-172">A scale-out action is triggered that causes the capacity of the set to be increased by one:</span><span class="sxs-lookup"><span data-stu-id="5eef4-172">A scale-out action is triggered that causes the capacity of the set to be increased by one:</span></span>

    "sku": {
      "name": "Standard_A0",
      "tier": "Standard",
      "capacity": 4
    },

<span data-ttu-id="5eef4-173">And a virtual machine is added to the scale set:</span><span class="sxs-lookup"><span data-stu-id="5eef4-173">And a virtual machine is added to the scale set:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

<span data-ttu-id="5eef4-174">After a cooldown period of five minutes, if the average number of threads on the machines stays over 600, another machine is added to the set.</span><span class="sxs-lookup"><span data-stu-id="5eef4-174">After a cooldown period of five minutes, if the average number of threads on the machines stays over 600, another machine is added to the set.</span></span> <span data-ttu-id="5eef4-175">If the average thread count stays below 550, the capacity of the scale set is reduced by one and a machine is removed from the set.</span><span class="sxs-lookup"><span data-stu-id="5eef4-175">If the average thread count stays below 550, the capacity of the scale set is reduced by one and a machine is removed from the set.</span></span>

## <a name="set-up-scaling-using-azure-powershell"></a><span data-ttu-id="5eef4-176">Set up scaling using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5eef4-176">Set up scaling using Azure PowerShell</span></span>
<span data-ttu-id="5eef4-177">To see examples of using PowerShell to set up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5eef4-177">To see examples of using PowerShell to set up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span></span>

## <a name="set-up-scaling-using-azure-cli"></a><span data-ttu-id="5eef4-178">Set up scaling using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5eef4-178">Set up scaling using Azure CLI</span></span>
<span data-ttu-id="5eef4-179">To see examples of using Azure CLI to set up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5eef4-179">To see examples of using Azure CLI to set up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span></span>

## <a name="set-up-scaling-using-the-azure-portal"></a><span data-ttu-id="5eef4-180">Set up scaling using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="5eef4-180">Set up scaling using the Azure portal</span></span>
<span data-ttu-id="5eef4-181">To see an example of using the Azure portal to set up autoscaling, look at [Create a Virtual Machine Scale Set using the Azure portal](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="5eef4-181">To see an example of using the Azure portal to set up autoscaling, look at [Create a Virtual Machine Scale Set using the Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="investigate-scaling-actions"></a><span data-ttu-id="5eef4-182">Investigate scaling actions</span><span class="sxs-lookup"><span data-stu-id="5eef4-182">Investigate scaling actions</span></span>
* <span data-ttu-id="5eef4-183">Azure portal - You can currently get a limited amount of information using the portal.</span><span class="sxs-lookup"><span data-stu-id="5eef4-183">Azure portal - You can currently get a limited amount of information using the portal.</span></span>
* <span data-ttu-id="5eef4-184">Azure Resource Explorer - This tool is the best for exploring the current state of your scale set.</span><span class="sxs-lookup"><span data-stu-id="5eef4-184">Azure Resource Explorer - This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="5eef4-185">Follow this path and you should see the instance view of the scale set that you created: Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines</span><span class="sxs-lookup"><span data-stu-id="5eef4-185">Follow this path and you should see the instance view of the scale set that you created: Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines</span></span>
* <span data-ttu-id="5eef4-186">Azure PowerShell - Use this command to get some information:</span><span class="sxs-lookup"><span data-stu-id="5eef4-186">Azure PowerShell - Use this command to get some information:</span></span>
  
        Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
        Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
* <span data-ttu-id="5eef4-187">Connect to the jumpbox virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span><span class="sxs-lookup"><span data-stu-id="5eef4-187">Connect to the jumpbox virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5eef4-188">Next Steps</span><span class="sxs-lookup"><span data-stu-id="5eef4-188">Next Steps</span></span>
* <span data-ttu-id="5eef4-189">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) to see an example of how to create a scale set with automatic scaling configured.</span><span class="sxs-lookup"><span data-stu-id="5eef4-189">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) to see an example of how to create a scale set with automatic scaling configured.</span></span>
* <span data-ttu-id="5eef4-190">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span><span class="sxs-lookup"><span data-stu-id="5eef4-190">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>
* <span data-ttu-id="5eef4-191">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="5eef4-191">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span></span>
* <span data-ttu-id="5eef4-192">Learn about how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="5eef4-192">Learn about how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>
* <span data-ttu-id="5eef4-193">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="5eef4-193">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span></span>





