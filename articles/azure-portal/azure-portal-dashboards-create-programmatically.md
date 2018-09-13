---
title: Programmatically create Azure Dashboards | Microsoft Docs
description: This article explains how to programmatically create Azure Dashboards.
services: azure-portal
documentationcenter: ''
author: adamabmsft
manager: dougeby
editor: tysonn
ms.service: azure-portal
ms.devlang: NA
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/01/2017
ms.author: adamab
ms.openlocfilehash: 8ac3bb2c95420eb4a608f003f3d937e3a47c272b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869191"
---
# <a name="programmatically-create-azure-dashboards"></a><span data-ttu-id="82944-103">Programmatically create Azure Dashboards</span><span class="sxs-lookup"><span data-stu-id="82944-103">Programmatically create Azure Dashboards</span></span>

<span data-ttu-id="82944-104">This document walks through the process of programmatically creating and publishing Azure dashboards.</span><span class="sxs-lookup"><span data-stu-id="82944-104">This document walks through the process of programmatically creating and publishing Azure dashboards.</span></span> <span data-ttu-id="82944-105">The dashboard shown below is referenced throughout the document.</span><span class="sxs-lookup"><span data-stu-id="82944-105">The dashboard shown below is referenced throughout the document.</span></span>

![sample dashboard](./media/azure-portal-dashboards-create-programmatically/sample-dashboard.png)

## <a name="overview"></a><span data-ttu-id="82944-107">Overview</span><span class="sxs-lookup"><span data-stu-id="82944-107">Overview</span></span>

<span data-ttu-id="82944-108">Shared dashboards in Azure are [resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) just like virtual machines and storage accounts.</span><span class="sxs-lookup"><span data-stu-id="82944-108">Shared dashboards in Azure are [resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) just like virtual machines and storage accounts.</span></span>  <span data-ttu-id="82944-109">Therefore, they can be managed programmatically via the [Azure Resource Manager REST APIs](/rest/api/), the [Azure CLI](https://docs.microsoft.com/cli/azure), [Azure PowerShell commands](https://docs.microsoft.com/powershell/azure/get-started-azureps?view=azurermps-4.2.0), and many [Azure portal](https://portal.azure.com) features build on top of these APIs to make resource management easier.</span><span class="sxs-lookup"><span data-stu-id="82944-109">Therefore, they can be managed programmatically via the [Azure Resource Manager REST APIs](/rest/api/), the [Azure CLI](https://docs.microsoft.com/cli/azure), [Azure PowerShell commands](https://docs.microsoft.com/powershell/azure/get-started-azureps?view=azurermps-4.2.0), and many [Azure portal](https://portal.azure.com) features build on top of these APIs to make resource management easier.</span></span>  

<span data-ttu-id="82944-110">Each of these APIs and tools offers ways to create, list, retrieve, modify, and delete resources.</span><span class="sxs-lookup"><span data-stu-id="82944-110">Each of these APIs and tools offers ways to create, list, retrieve, modify, and delete resources.</span></span>  <span data-ttu-id="82944-111">Since dashboards are resources, you can pick your favorite API / tool to use.</span><span class="sxs-lookup"><span data-stu-id="82944-111">Since dashboards are resources, you can pick your favorite API / tool to use.</span></span>

<span data-ttu-id="82944-112">Regardless of which tool you use, you need to construct a JSON representation of your dashboard object before you can call any resource creation API.</span><span class="sxs-lookup"><span data-stu-id="82944-112">Regardless of which tool you use, you need to construct a JSON representation of your dashboard object before you can call any resource creation API.</span></span> <span data-ttu-id="82944-113">This object contains information about the parts (a.k.a.</span><span class="sxs-lookup"><span data-stu-id="82944-113">This object contains information about the parts (a.k.a.</span></span> <span data-ttu-id="82944-114">tiles) on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="82944-114">tiles) on the dashboard.</span></span> <span data-ttu-id="82944-115">It includes sizes, positions, resources they are bound to, and any user customizations.</span><span class="sxs-lookup"><span data-stu-id="82944-115">It includes sizes, positions, resources they are bound to, and any user customizations.</span></span>

<span data-ttu-id="82944-116">The most practical way to build up this JSON document is to use [the portal](https://portal.azure.com/) to interactively add and position your tiles.</span><span class="sxs-lookup"><span data-stu-id="82944-116">The most practical way to build up this JSON document is to use [the portal](https://portal.azure.com/) to interactively add and position your tiles.</span></span> <span data-ttu-id="82944-117">You then export the JSON.</span><span class="sxs-lookup"><span data-stu-id="82944-117">You then export the JSON.</span></span> <span data-ttu-id="82944-118">Finally, you create a template from the result for later use in scripts, programs, and deployment tools.</span><span class="sxs-lookup"><span data-stu-id="82944-118">Finally, you create a template from the result for later use in scripts, programs, and deployment tools.</span></span>

## <a name="create-a-dashboard"></a><span data-ttu-id="82944-119">Create a dashboard</span><span class="sxs-lookup"><span data-stu-id="82944-119">Create a dashboard</span></span>

<span data-ttu-id="82944-120">To create a new dashboard, use the New dashboard command on the portal’s main screen.</span><span class="sxs-lookup"><span data-stu-id="82944-120">To create a new dashboard, use the New dashboard command on the portal’s main screen.</span></span>

![new dashboard command](./media/azure-portal-dashboards-create-programmatically/new-dashboard-command.png)

<span data-ttu-id="82944-122">You can then use the tile gallery to find and add tiles.</span><span class="sxs-lookup"><span data-stu-id="82944-122">You can then use the tile gallery to find and add tiles.</span></span> <span data-ttu-id="82944-123">Tiles are added by dragging and dropping them.</span><span class="sxs-lookup"><span data-stu-id="82944-123">Tiles are added by dragging and dropping them.</span></span> <span data-ttu-id="82944-124">Some tiles support resizing via a drag handle, while others support fixes sizes that can be seen in their context menu.</span><span class="sxs-lookup"><span data-stu-id="82944-124">Some tiles support resizing via a drag handle, while others support fixes sizes that can be seen in their context menu.</span></span>

### <a name="drag-handle"></a><span data-ttu-id="82944-125">Drag handle</span><span class="sxs-lookup"><span data-stu-id="82944-125">Drag handle</span></span>
![drag handle](./media/azure-portal-dashboards-create-programmatically/drag-handle.png)

### <a name="fixed-sizes-via-context-menu"></a><span data-ttu-id="82944-127">Fixed sizes via context menu</span><span class="sxs-lookup"><span data-stu-id="82944-127">Fixed sizes via context menu</span></span>
![sizes context menu](./media/azure-portal-dashboards-create-programmatically/sizes-context-menu.png)

## <a name="share-the-dashboard"></a><span data-ttu-id="82944-129">Share the dashboard</span><span class="sxs-lookup"><span data-stu-id="82944-129">Share the dashboard</span></span>

<span data-ttu-id="82944-130">After you have configured the dashboard to your liking the next steps are to publish the dashboard (using the Share command) and then use the resource explorer to fetch the JSON.</span><span class="sxs-lookup"><span data-stu-id="82944-130">After you have configured the dashboard to your liking the next steps are to publish the dashboard (using the Share command) and then use the resource explorer to fetch the JSON.</span></span>

![share command](./media/azure-portal-dashboards-create-programmatically/share-command.png)

<span data-ttu-id="82944-132">Clicking the Share command shows a dialog that asks you to choose which subscription and resource group to publish to.</span><span class="sxs-lookup"><span data-stu-id="82944-132">Clicking the Share command shows a dialog that asks you to choose which subscription and resource group to publish to.</span></span> <span data-ttu-id="82944-133">Keep in mind that [you must have write access](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) to the subscription and resource group that you choose.</span><span class="sxs-lookup"><span data-stu-id="82944-133">Keep in mind that [you must have write access](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) to the subscription and resource group that you choose.</span></span>

![sharing and access](./media/azure-portal-dashboards-create-programmatically/sharing-and-access.png)

## <a name="fetch-the-json-representation-of-the-dashboard"></a><span data-ttu-id="82944-135">Fetch the JSON representation of the dashboard</span><span class="sxs-lookup"><span data-stu-id="82944-135">Fetch the JSON representation of the dashboard</span></span>

<span data-ttu-id="82944-136">Publishing only takes a few seconds.</span><span class="sxs-lookup"><span data-stu-id="82944-136">Publishing only takes a few seconds.</span></span>  <span data-ttu-id="82944-137">When it’s done, the next step is to go to the [Resource Explorer](https://portal.azure.com/#blade/HubsExtension/ArmExplorerBlade) to fetch the JSON.</span><span class="sxs-lookup"><span data-stu-id="82944-137">When it’s done, the next step is to go to the [Resource Explorer](https://portal.azure.com/#blade/HubsExtension/ArmExplorerBlade) to fetch the JSON.</span></span>

![browse resource explorer](./media/azure-portal-dashboards-create-programmatically/browse-resource-explorer.png)

<span data-ttu-id="82944-139">From the resource explorer, navigate to the subscription and resource group that you chose.</span><span class="sxs-lookup"><span data-stu-id="82944-139">From the resource explorer, navigate to the subscription and resource group that you chose.</span></span> <span data-ttu-id="82944-140">Next, click on the newly published dashboard resource to reveal the JSON.</span><span class="sxs-lookup"><span data-stu-id="82944-140">Next, click on the newly published dashboard resource to reveal the JSON.</span></span>

![resource explorer json](./media/azure-portal-dashboards-create-programmatically/resource-explorer-json.png)

## <a name="create-a-template-from-the-json"></a><span data-ttu-id="82944-142">Create a template from the JSON</span><span class="sxs-lookup"><span data-stu-id="82944-142">Create a template from the JSON</span></span>

<span data-ttu-id="82944-143">The next step is to create a template from this JSON so that it can be reused programmatically with the appropriate resource management APIs, command-line tools, or within the portal.</span><span class="sxs-lookup"><span data-stu-id="82944-143">The next step is to create a template from this JSON so that it can be reused programmatically with the appropriate resource management APIs, command-line tools, or within the portal.</span></span>

<span data-ttu-id="82944-144">It is not necessary to fully understand the dashboard JSON structure to create a template.</span><span class="sxs-lookup"><span data-stu-id="82944-144">It is not necessary to fully understand the dashboard JSON structure to create a template.</span></span> <span data-ttu-id="82944-145">In most cases, you want to preserve the structure and configuration of each tile, and then parameterize the set of Azure resources they’re pointing to.</span><span class="sxs-lookup"><span data-stu-id="82944-145">In most cases, you want to preserve the structure and configuration of each tile, and then parameterize the set of Azure resources they’re pointing to.</span></span> <span data-ttu-id="82944-146">Look at your exported JSON dashboard and find all occurrences of Azure resource Ids.</span><span class="sxs-lookup"><span data-stu-id="82944-146">Look at your exported JSON dashboard and find all occurrences of Azure resource Ids.</span></span> <span data-ttu-id="82944-147">Our example dashboard has multiple tiles that all point at a single Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="82944-147">Our example dashboard has multiple tiles that all point at a single Azure virtual machine.</span></span> <span data-ttu-id="82944-148">That’s because our dashboard only looks at this single resource.</span><span class="sxs-lookup"><span data-stu-id="82944-148">That’s because our dashboard only looks at this single resource.</span></span> <span data-ttu-id="82944-149">If you search the sample json (included at the end of the document) for “/subscriptions”, you find several occurrences of this Id.</span><span class="sxs-lookup"><span data-stu-id="82944-149">If you search the sample json (included at the end of the document) for “/subscriptions”, you find several occurrences of this Id.</span></span>

`/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1`

<span data-ttu-id="82944-150">To publish this dashboard for any virtual machine in the future you need to parameterize every occurrence of this string within the JSON.</span><span class="sxs-lookup"><span data-stu-id="82944-150">To publish this dashboard for any virtual machine in the future you need to parameterize every occurrence of this string within the JSON.</span></span> 

<span data-ttu-id="82944-151">There are two flavors of APIs that create resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="82944-151">There are two flavors of APIs that create resources in Azure.</span></span> <span data-ttu-id="82944-152">[Imperative APIs](https://docs.microsoft.com/rest/api/resources/resources) that create one resource at a time, and a [template-based deployment](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) system that can orchestrate the creation of multiple, dependent resources with a single API call.</span><span class="sxs-lookup"><span data-stu-id="82944-152">[Imperative APIs](https://docs.microsoft.com/rest/api/resources/resources) that create one resource at a time, and a [template-based deployment](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) system that can orchestrate the creation of multiple, dependent resources with a single API call.</span></span> <span data-ttu-id="82944-153">The latter natively supports parameterization and templating so we use it for our example.</span><span class="sxs-lookup"><span data-stu-id="82944-153">The latter natively supports parameterization and templating so we use it for our example.</span></span>

## <a name="programmatically-create-a-dashboard-from-your-template-using-a-template-deployment"></a><span data-ttu-id="82944-154">Programmatically create a dashboard from your template using a template deployment</span><span class="sxs-lookup"><span data-stu-id="82944-154">Programmatically create a dashboard from your template using a template deployment</span></span>

<span data-ttu-id="82944-155">Azure offers the ability to orchestrate the deployment of multiple resources.</span><span class="sxs-lookup"><span data-stu-id="82944-155">Azure offers the ability to orchestrate the deployment of multiple resources.</span></span> <span data-ttu-id="82944-156">You create a deployment template that expresses the set of resources to deploy as well as the relationships between them.</span><span class="sxs-lookup"><span data-stu-id="82944-156">You create a deployment template that expresses the set of resources to deploy as well as the relationships between them.</span></span>  <span data-ttu-id="82944-157">The JSON format of each resource is the same as if you were creating them one by one.</span><span class="sxs-lookup"><span data-stu-id="82944-157">The JSON format of each resource is the same as if you were creating them one by one.</span></span> <span data-ttu-id="82944-158">The difference is that the [template language](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) adds a few concepts like variables, parameters, basic functions, and more.</span><span class="sxs-lookup"><span data-stu-id="82944-158">The difference is that the [template language](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) adds a few concepts like variables, parameters, basic functions, and more.</span></span> <span data-ttu-id="82944-159">This extended syntax is only supported in the context of a template deployment and does not work if used with the imperative APIs discussed earlier.</span><span class="sxs-lookup"><span data-stu-id="82944-159">This extended syntax is only supported in the context of a template deployment and does not work if used with the imperative APIs discussed earlier.</span></span>

<span data-ttu-id="82944-160">If you’re going this route, then parameterization should be done using the template’s parameter syntax.</span><span class="sxs-lookup"><span data-stu-id="82944-160">If you’re going this route, then parameterization should be done using the template’s parameter syntax.</span></span>  <span data-ttu-id="82944-161">You replace all instances of the resource id we found earlier as shown here.</span><span class="sxs-lookup"><span data-stu-id="82944-161">You replace all instances of the resource id we found earlier as shown here.</span></span>

### <a name="example-json-property-with-hard-coded-resource-id"></a><span data-ttu-id="82944-162">Example JSON property with hard-coded resource Id</span><span class="sxs-lookup"><span data-stu-id="82944-162">Example JSON property with hard-coded resource Id</span></span>
`id: "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"`

### <a name="example-json-property-converted-to-a-parameterized-version-based-on-template-parameters"></a><span data-ttu-id="82944-163">Example JSON property converted to a parameterized version based on template parameters</span><span class="sxs-lookup"><span data-stu-id="82944-163">Example JSON property converted to a parameterized version based on template parameters</span></span>

`id: "[resourceId(parameters('virtualMachineResourceGroup'), 'Microsoft.Compute/virtualMachines', parameters('virtualMachineName'))]"`

<span data-ttu-id="82944-164">You also need to declare some required template metadata and the parameters at the top of the json template like this:</span><span class="sxs-lookup"><span data-stu-id="82944-164">You also need to declare some required template metadata and the parameters at the top of the json template like this:</span></span>

```json

{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "virtualMachineName": {
            "type": "string"
        },
        "virtualMachineResourceGroup": {
            "type": "string"
        },
        "dashboardName": {
            "type": "string"
        }
    },
    "variables": {},

    ... rest of template omitted ...
```

<span data-ttu-id="82944-165">__You can see the full, working template at the end of this document.__</span><span class="sxs-lookup"><span data-stu-id="82944-165">__You can see the full, working template at the end of this document.__</span></span>

<span data-ttu-id="82944-166">Once you have crafted your template you can deploy it using the [REST APIs](https://docs.microsoft.com/rest/api/resources/deployments), [PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy), The [Azure CLI](https://docs.microsoft.com/cli/azure/group/deployment#az-group-deployment-create), or the [portal’s template deployment page](https://portal.azure.com/#create/Microsoft.Template).</span><span class="sxs-lookup"><span data-stu-id="82944-166">Once you have crafted your template you can deploy it using the [REST APIs](https://docs.microsoft.com/rest/api/resources/deployments), [PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy), The [Azure CLI](https://docs.microsoft.com/cli/azure/group/deployment#az-group-deployment-create), or the [portal’s template deployment page](https://portal.azure.com/#create/Microsoft.Template).</span></span>

<span data-ttu-id="82944-167">Here are two versions of our example dashboard JSON.</span><span class="sxs-lookup"><span data-stu-id="82944-167">Here are two versions of our example dashboard JSON.</span></span> <span data-ttu-id="82944-168">The first is the version that we exported from the portal that was already bound to a resource.</span><span class="sxs-lookup"><span data-stu-id="82944-168">The first is the version that we exported from the portal that was already bound to a resource.</span></span> <span data-ttu-id="82944-169">The second is the template version that can be programmatically bound to any VM and deployed using Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="82944-169">The second is the template version that can be programmatically bound to any VM and deployed using Azure Resource Manager.</span></span>

## <a name="json-representation-of-our-example-dashboard-before-templating"></a><span data-ttu-id="82944-170">JSON representation of our example dashboard (before templating)</span><span class="sxs-lookup"><span data-stu-id="82944-170">JSON representation of our example dashboard (before templating)</span></span>

<span data-ttu-id="82944-171">This is what you can expect to see if you follow the earlier instructions to fetch the JSON representation of a dashboard that is already deployed.</span><span class="sxs-lookup"><span data-stu-id="82944-171">This is what you can expect to see if you follow the earlier instructions to fetch the JSON representation of a dashboard that is already deployed.</span></span> <span data-ttu-id="82944-172">Note the hard-coded resource identifiers that show that this dashboard is pointing at a specific Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="82944-172">Note the hard-coded resource identifiers that show that this dashboard is pointing at a specific Azure virtual machine.</span></span>

```json

{
    "properties": {
        "lenses": {
            "0": {
                "order": 0,
                "parts": {
                    "0": {
                        "position": {
                            "x": 0,
                            "y": 0,
                            "rowSpan": 2,
                            "colSpan": 3
                        },
                        "metadata": {
                            "inputs": [],
                            "type": "Extension[azure]/HubsExtension/PartType/MarkdownPart",
                            "settings": {
                                "content": {
                                    "settings": {
                                        "content": "## Azure Virtual Machines Overview\r\nNew team members should watch this video to get familiar with Azure Virtual Machines.",
                                        "title": "",
                                        "subtitle": ""
                                    }
                                }
                            }
                        }
                    },
                    "1": {
                        "position": {
                            "x": 3,
                            "y": 0,
                            "rowSpan": 4,
                            "colSpan": 8
                        },
                        "metadata": {
                            "inputs": [],
                            "type": "Extension[azure]/HubsExtension/PartType/MarkdownPart",
                            "settings": {
                                "content": {
                                    "settings": {
                                        "content": "This is the team dashboard for the test VM we use on our team. Here are some useful links:\r\n\r\n1. [Getting started](https://www.contoso.com/tsgs)\r\n1. [Troubleshooting guide](https://www.contoso.com/tsgs)\r\n1. [Architecture docs](https://www.contoso.com/tsgs)",
                                        "title": "Test VM Dashboard",
                                        "subtitle": "Contoso"
                                    }
                                }
                            }
                        }
                    },
                    "2": {
                        "position": {
                            "x": 0,
                            "y": 2,
                            "rowSpan": 2,
                            "colSpan": 3
                        },
                        "metadata": {
                            "inputs": [],
                            "type": "Extension[azure]/HubsExtension/PartType/VideoPart",
                            "settings": {
                                "content": {
                                    "settings": {
                                        "title": "",
                                        "subtitle": "",
                                        "src": "https://www.youtube.com/watch?v=YcylDIiKaSU&list=PLLasX02E8BPCsnETz0XAMfpLR1LIBqpgs&index=4",
                                        "autoplay": false
                                    }
                                }
                            }
                        }
                    },
                    "3": {
                        "position": {
                            "x": 0,
                            "y": 4,
                            "rowSpan": 3,
                            "colSpan": 11
                        },
                        "metadata": {
                            "inputs": [
                                {
                                    "name": "queryInputs",
                                    "value": {
                                        "timespan": {
                                            "duration": "PT1H",
                                            "start": null,
                                            "end": null
                                        },
                                        "id": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1",
                                        "chartType": 0,
                                        "metrics": [
                                            {
                                                "name": "Percentage CPU",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            }
                                        ]
                                    }
                                }
                            ],
                            "type": "Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart",
                            "settings": {}
                        }
                    },
                    "4": {
                        "position": {
                            "x": 0,
                            "y": 7,
                            "rowSpan": 2,
                            "colSpan": 3
                        },
                        "metadata": {
                            "inputs": [
                                {
                                    "name": "queryInputs",
                                    "value": {
                                        "timespan": {
                                            "duration": "PT1H",
                                            "start": null,
                                            "end": null
                                        },
                                        "id": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1",
                                        "chartType": 0,
                                        "metrics": [
                                            {
                                                "name": "Disk Read Operations/Sec",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            },
                                            {
                                                "name": "Disk Write Operations/Sec",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            }
                                        ]
                                    }
                                }
                            ],
                            "type": "Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart",
                            "settings": {}
                        }
                    },
                    "5": {
                        "position": {
                            "x": 3,
                            "y": 7,
                            "rowSpan": 2,
                            "colSpan": 3
                        },
                        "metadata": {
                            "inputs": [
                                {
                                    "name": "queryInputs",
                                    "value": {
                                        "timespan": {
                                            "duration": "PT1H",
                                            "start": null,
                                            "end": null
                                        },
                                        "id": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1",
                                        "chartType": 0,
                                        "metrics": [
                                            {
                                                "name": "Disk Read Bytes",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            },
                                            {
                                                "name": "Disk Write Bytes",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            }
                                        ]
                                    }
                                }
                            ],
                            "type": "Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart",
                            "settings": {}
                        }
                    },
                    "6": {
                        "position": {
                            "x": 6,
                            "y": 7,
                            "rowSpan": 2,
                            "colSpan": 3
                        },
                        "metadata": {
                            "inputs": [
                                {
                                    "name": "queryInputs",
                                    "value": {
                                        "timespan": {
                                            "duration": "PT1H",
                                            "start": null,
                                            "end": null
                                        },
                                        "id": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1",
                                        "chartType": 0,
                                        "metrics": [
                                            {
                                                "name": "Network In",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            },
                                            {
                                                "name": "Network Out",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            }
                                        ]
                                    }
                                }
                            ],
                            "type": "Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart",
                            "settings": {}
                        }
                    },
                    "7": {
                        "position": {
                            "x": 9,
                            "y": 7,
                            "rowSpan": 2,
                            "colSpan": 2
                        },
                        "metadata": {
                            "inputs": [
                                {
                                    "name": "id",
                                    "value": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                }
                            ],
                            "type": "Extension/Microsoft_Azure_Compute/PartType/VirtualMachinePart",
                            "asset": {
                                "idInputName": "id",
                                "type": "VirtualMachine"
                            },
                            "defaultMenuItemId": "overview"
                        }
                    }
                }
            }
        },
        "metadata": { }
    },
    "id": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/dashboards/providers/Microsoft.Portal/dashboards/aa9786ae-e159-483f-b05f-1f7f767741a9",
    "name": "aa9786ae-e159-483f-b05f-1f7f767741a9",
    "type": "Microsoft.Portal/dashboards",
    "location": "eastasia",
    "tags": {
        "hidden-title": "Created via API"
    }
}

```

### <a name="template-representation-of-our-example-dashboard"></a><span data-ttu-id="82944-173">Template representation of our example dashboard</span><span class="sxs-lookup"><span data-stu-id="82944-173">Template representation of our example dashboard</span></span>

<span data-ttu-id="82944-174">The template version of the dashboard has defined three parameters called __virtualMachineName__, __virtualMachineResourceGroup__, and __dashboardName__.</span><span class="sxs-lookup"><span data-stu-id="82944-174">The template version of the dashboard has defined three parameters called __virtualMachineName__, __virtualMachineResourceGroup__, and __dashboardName__.</span></span>  <span data-ttu-id="82944-175">The parameters let you point this dashboard at a different Azure virtual machine every time you deploy.</span><span class="sxs-lookup"><span data-stu-id="82944-175">The parameters let you point this dashboard at a different Azure virtual machine every time you deploy.</span></span> <span data-ttu-id="82944-176">The parameterized ids are highlighted to show that this dashboard can be programmatically configured and deployed to point to any Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="82944-176">The parameterized ids are highlighted to show that this dashboard can be programmatically configured and deployed to point to any Azure virtual machine.</span></span> <span data-ttu-id="82944-177">The easiest way to test this feature is to copy the following template and paste it into the [Azure portal’s template deployment page](https://portal.azure.com/#create/Microsoft.Template).</span><span class="sxs-lookup"><span data-stu-id="82944-177">The easiest way to test this feature is to copy the following template and paste it into the [Azure portal’s template deployment page](https://portal.azure.com/#create/Microsoft.Template).</span></span> 

<span data-ttu-id="82944-178">This example deploys a dashboard by itself, but the template language lets you deploy multiple resources, and bundle one or more dashboards along side them.</span><span class="sxs-lookup"><span data-stu-id="82944-178">This example deploys a dashboard by itself, but the template language lets you deploy multiple resources, and bundle one or more dashboards along side them.</span></span> 

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "virtualMachineName": {
            "type": "string"
        },
        "virtualMachineResourceGroup": {
            "type": "string"
        },
        "dashboardName": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "properties": {
                "lenses": {
                    "0": {
                        "order": 0,
                        "parts": {
                            "0": {
                                "position": {
                                    "x": 0,
                                    "y": 0,
                                    "rowSpan": 2,
                                    "colSpan": 3
                                },
                                "metadata": {
                                    "inputs": [],
                                    "type": "Extension[azure]/HubsExtension/PartType/MarkdownPart",
                                    "settings": {
                                        "content": {
                                            "settings": {
                                                "content": "## Azure Virtual Machines Overview\r\nNew team members should watch this video to get familiar with Azure Virtual Machines.",
                                                "title": "",
                                                "subtitle": ""
                                            }
                                        }
                                    }
                                }
                            },
                            "1": {
                                "position": {
                                    "x": 3,
                                    "y": 0,
                                    "rowSpan": 4,
                                    "colSpan": 8
                                },
                                "metadata": {
                                    "inputs": [],
                                    "type": "Extension[azure]/HubsExtension/PartType/MarkdownPart",
                                    "settings": {
                                        "content": {
                                            "settings": {
                                                "content": "This is the team dashboard for the test VM we use on our team. Here are some useful links:\r\n\r\n1. [Getting started](https://www.contoso.com/tsgs)\r\n1. [Troubleshooting guide](https://www.contoso.com/tsgs)\r\n1. [Architecture docs](https://www.contoso.com/tsgs)",
                                                "title": "Test VM Dashboard",
                                                "subtitle": "Contoso"
                                            }
                                        }
                                    }
                                }
                            },
                            "2": {
                                "position": {
                                    "x": 0,
                                    "y": 2,
                                    "rowSpan": 2,
                                    "colSpan": 3
                                },
                                "metadata": {
                                    "inputs": [],
                                    "type": "Extension[azure]/HubsExtension/PartType/VideoPart",
                                    "settings": {
                                        "content": {
                                            "settings": {
                                                "title": "",
                                                "subtitle": "",
                                                "src": "https://www.youtube.com/watch?v=YcylDIiKaSU&list=PLLasX02E8BPCsnETz0XAMfpLR1LIBqpgs&index=4",
                                                "autoplay": false
                                            }
                                        }
                                    }
                                }
                            },
                            "3": {
                                "position": {
                                    "x": 0,
                                    "y": 4,
                                    "rowSpan": 3,
                                    "colSpan": 11
                                },
                                "metadata": {
                                    "inputs": [
                                        {
                                            "name": "queryInputs",
                                            "value": {
                                                "timespan": {
                                                    "duration": "PT1H",
                                                    "start": null,
                                                    "end": null
                                                },
                                                "id": "[resourceId(parameters('virtualMachineResourceGroup'), 'Microsoft.Compute/virtualMachines', parameters('virtualMachineName'))]",
                                                "chartType": 0,
                                                "metrics": [
                                                    {
                                                        "name": "Percentage CPU",
                                                        "resourceId": "[resourceId(parameters('virtualMachineResourceGroup'), 'Microsoft.Compute/virtualMachines', parameters('virtualMachineName'))]"
                                                    }
                                                ]
                                            }
                                        }
                                    ],
                                    "type": "Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart",
                                    "settings": {}
                                }
                            },
                            "4": {
                                "position": {
                                    "x": 0,
                                    "y": 7,
                                    "rowSpan": 2,
                                    "colSpan": 3
                                },
                                "metadata": {
                                    "inputs": [
                                        {
                                            "name": "queryInputs",
                                            "value": {
                                                "timespan": {
                                                    "duration": "PT1H",
                                                    "start": null,
                                                    "end": null
                                                },
                                                "id": "[resourceId(parameters('virtualMachineResourceGroup'), 'Microsoft.Compute/virtualMachines', parameters('virtualMachineName'))]",
                                                "chartType": 0,
                                                "metrics": [
                                                    {
                                                        "name": "Disk Read Operations/Sec",
                                                        "resourceId": "[resourceId(parameters('virtualMachineResourceGroup'), 'Microsoft.Compute/virtualMachines', parameters('virtualMachineName'))]"
                                                    },
                                                    {
                                                        "name": "Disk Write Operations/Sec",
                                                        "resourceId": "[resourceId(parameters('virtualMachineResourceGroup'), 'Microsoft.Compute/virtualMachines', parameters('virtualMachineName'))]"
                                                    }
                                                ]
                                            }
                                        }
                                    ],
                                    "type": "Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart",
                                    "settings": {}
                                }
                            },
                            "5": {
                                "position": {
                                    "x": 3,
                                    "y": 7,
                                    "rowSpan": 2,
                                    "colSpan": 3
                                },
                                "metadata": {
                                    "inputs": [
                                        {
                                            "name": "queryInputs",
                                            "value": {
                                                "timespan": {
                                                    "duration": "PT1H",
                                                    "start": null,
                                                    "end": null
                                                },
                                                "id": "[resourceId(parameters('virtualMachineResourceGroup'), 'Microsoft.Compute/virtualMachines', parameters('virtualMachineName'))]",
                                                "chartType": 0,
                                                "metrics": [
                                                    {
                                                        "name": "Disk Read Bytes",
                                                        "resourceId": "[resourceId(parameters('virtualMachineResourceGroup'), 'Microsoft.Compute/virtualMachines', parameters('virtualMachineName'))]"
                                                    },
                                                    {
                                                        "name": "Disk Write Bytes",
                                                        "resourceId": "[resourceId(parameters('virtualMachineResourceGroup'), 'Microsoft.Compute/virtualMachines', parameters('virtualMachineName'))]"
                                                    }
                                                ]
                                            }
                                        }
                                    ],
                                    "type": "Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart",
                                    "settings": {}
                                }
                            },
                            "6": {
                                "position": {
                                    "x": 6,
                                    "y": 7,
                                    "rowSpan": 2,
                                    "colSpan": 3
                                },
                                "metadata": {
                                    "inputs": [
                                        {
                                            "name": "queryInputs",
                                            "value": {
                                                "timespan": {
                                                    "duration": "PT1H",
                                                    "start": null,
                                                    "end": null
                                                },
                                                "id": "[resourceId(parameters('virtualMachineResourceGroup'), 'Microsoft.Compute/virtualMachines', parameters('virtualMachineName'))]",
                                                "chartType": 0,
                                                "metrics": [
                                                    {
                                                        "name": "Network In",
                                                        "resourceId": "[resourceId(parameters('virtualMachineResourceGroup'), 'Microsoft.Compute/virtualMachines', parameters('virtualMachineName'))]"
                                                    },
                                                    {
                                                        "name": "Network Out",
                                                        "resourceId": "[resourceId(parameters('virtualMachineResourceGroup'), 'Microsoft.Compute/virtualMachines', parameters('virtualMachineName'))]"
                                                    }
                                                ]
                                            }
                                        }
                                    ],
                                    "type": "Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart",
                                    "settings": {}
                                }
                            },
                            "7": {
                                "position": {
                                    "x": 9,
                                    "y": 7,
                                    "rowSpan": 2,
                                    "colSpan": 2
                                },
                                "metadata": {
                                    "inputs": [
                                        {
                                            "name": "id",
                                            "value": "[resourceId(parameters('virtualMachineResourceGroup'), 'Microsoft.Compute/virtualMachines', parameters('virtualMachineName'))]"
                                        }
                                    ],
                                    "type": "Extension/Microsoft_Azure_Compute/PartType/VirtualMachinePart",
                                    "asset": {
                                        "idInputName": "id",
                                        "type": "VirtualMachine"
                                    },
                                    "defaultMenuItemId": "overview"
                                }
                            }
                        }
                    }
                }
            },
            "metadata": { },
            "apiVersion": "2015-08-01-preview",
            "type": "Microsoft.Portal/dashboards",
            "name": "[parameters('dashboardName')]",
            "location": "westus",
            "tags": {
                "hidden-title": "[parameters('dashboardName')]"
            }
        }
    ]
}


```
