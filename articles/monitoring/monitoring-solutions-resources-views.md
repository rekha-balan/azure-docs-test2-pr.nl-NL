---
title: Views in management solutions | Microsoft Docs
description: 'Management solutions will typically include one or more views to visualize data.  This article describes how to export a view created by the View Designer and include it in a management solution. '
services: monitoring
documentationcenter: ''
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 570b278c-2d47-4e5a-9828-7f01f31ddf8c
ms.service: monitoring
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/16/2018
ms.author: bwren
ms.openlocfilehash: b4f54358f4bc1db973d6fe7163411e3a313c3cf4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866544"
---
# <a name="views-in-management-solutions-preview"></a><span data-ttu-id="91a83-104">Views in management solutions (Preview)</span><span class="sxs-lookup"><span data-stu-id="91a83-104">Views in management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="91a83-105">This is preliminary documentation for creating management solutions which are currently in preview.</span><span class="sxs-lookup"><span data-stu-id="91a83-105">This is preliminary documentation for creating management solutions which are currently in preview.</span></span> <span data-ttu-id="91a83-106">Any schema described below is subject to change.</span><span class="sxs-lookup"><span data-stu-id="91a83-106">Any schema described below is subject to change.</span></span>    


<span data-ttu-id="91a83-107">[Management solutions](monitoring-solutions.md) will typically include one or more views to visualize data.</span><span class="sxs-lookup"><span data-stu-id="91a83-107">[Management solutions](monitoring-solutions.md) will typically include one or more views to visualize data.</span></span>  <span data-ttu-id="91a83-108">This article describes how to export a view created by the [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span><span class="sxs-lookup"><span data-stu-id="91a83-108">This article describes how to export a view created by the [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="91a83-109">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Design and build a management solution in Azure](monitoring-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="91a83-109">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Design and build a management solution in Azure](monitoring-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="91a83-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="91a83-110">Prerequisites</span></span>
<span data-ttu-id="91a83-111">This article assumes that you're already familiar with how to [create a management solution](monitoring-solutions-creating.md) and the structure of a solution file.</span><span class="sxs-lookup"><span data-stu-id="91a83-111">This article assumes that you're already familiar with how to [create a management solution](monitoring-solutions-creating.md) and the structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="91a83-112">Overview</span><span class="sxs-lookup"><span data-stu-id="91a83-112">Overview</span></span>
<span data-ttu-id="91a83-113">To include a view in a management solution, you create a **resource** for it in the [solution file](monitoring-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="91a83-113">To include a view in a management solution, you create a **resource** for it in the [solution file](monitoring-solutions-creating.md).</span></span>  <span data-ttu-id="91a83-114">The JSON that describes the view's detailed configuration is typically complex though and not something that a typical solution author would be able to create manually.</span><span class="sxs-lookup"><span data-stu-id="91a83-114">The JSON that describes the view's detailed configuration is typically complex though and not something that a typical solution author would be able to create manually.</span></span>  <span data-ttu-id="91a83-115">The most common method is to create the view using the [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration to the solution.</span><span class="sxs-lookup"><span data-stu-id="91a83-115">The most common method is to create the view using the [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration to the solution.</span></span>

<span data-ttu-id="91a83-116">The basic steps to add a view to a solution are as follows.</span><span class="sxs-lookup"><span data-stu-id="91a83-116">The basic steps to add a view to a solution are as follows.</span></span>  <span data-ttu-id="91a83-117">Each step is described in further detail in the sections below.</span><span class="sxs-lookup"><span data-stu-id="91a83-117">Each step is described in further detail in the sections below.</span></span>

1. <span data-ttu-id="91a83-118">Export the view to a file.</span><span class="sxs-lookup"><span data-stu-id="91a83-118">Export the view to a file.</span></span>
2. <span data-ttu-id="91a83-119">Create the view resource in the solution.</span><span class="sxs-lookup"><span data-stu-id="91a83-119">Create the view resource in the solution.</span></span>
3. <span data-ttu-id="91a83-120">Add the view details.</span><span class="sxs-lookup"><span data-stu-id="91a83-120">Add the view details.</span></span>

## <a name="export-the-view-to-a-file"></a><span data-ttu-id="91a83-121">Export the view to a file</span><span class="sxs-lookup"><span data-stu-id="91a83-121">Export the view to a file</span></span>
<span data-ttu-id="91a83-122">Follow the instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) to export a view to a file.</span><span class="sxs-lookup"><span data-stu-id="91a83-122">Follow the instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) to export a view to a file.</span></span>  <span data-ttu-id="91a83-123">The exported file will be in JSON format with the same [elements as the solution file](monitoring-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="91a83-123">The exported file will be in JSON format with the same [elements as the solution file](monitoring-solutions-solution-file.md).</span></span>  

<span data-ttu-id="91a83-124">The **resources** element of the view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents the Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="91a83-124">The **resources** element of the view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents the Log Analytics workspace.</span></span>  <span data-ttu-id="91a83-125">This element will have a subelement with a type of **views** that represents the view and contains its detailed configuration.</span><span class="sxs-lookup"><span data-stu-id="91a83-125">This element will have a subelement with a type of **views** that represents the view and contains its detailed configuration.</span></span>  <span data-ttu-id="91a83-126">You will copy the details of this element and then copy it into your solution.</span><span class="sxs-lookup"><span data-stu-id="91a83-126">You will copy the details of this element and then copy it into your solution.</span></span>

## <a name="create-the-view-resource-in-the-solution"></a><span data-ttu-id="91a83-127">Create the view resource in the solution</span><span class="sxs-lookup"><span data-stu-id="91a83-127">Create the view resource in the solution</span></span>
<span data-ttu-id="91a83-128">Add the following view resource to the **resources** element of your solution file.</span><span class="sxs-lookup"><span data-stu-id="91a83-128">Add the following view resource to the **resources** element of your solution file.</span></span>  <span data-ttu-id="91a83-129">This uses variables that are described below that you must also add.</span><span class="sxs-lookup"><span data-stu-id="91a83-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="91a83-130">Note that the **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with the corresponding properties from the exported view file.</span><span class="sxs-lookup"><span data-stu-id="91a83-130">Note that the **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with the corresponding properties from the exported view file.</span></span>

    {
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
        "type": "Microsoft.OperationalInsights/workspaces/views",
        "location": "[parameters('workspaceregionId')]",
        "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
        "dependson": [
            ],
        "properties": {
            "Id": "[variables('ViewName')]",
            "Name": "[variables('ViewName')]",
            "DisplayName": "[variables('ViewName')]",
            "Description": "",
            "Author": "[variables('ViewAuthor')]",
            "Source": "Local",
            "Dashboard": ,
            "OverviewTile":
        }
    }

<span data-ttu-id="91a83-131">Add the following variables to the variables element of the solution file and replace the values to those for your solution.</span><span class="sxs-lookup"><span data-stu-id="91a83-131">Add the following variables to the variables element of the solution file and replace the values to those for your solution.</span></span>

    "LogAnalyticsApiVersion": "<api-version>",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of the view."
    "ViewName": "Provide a name for the view here."

<span data-ttu-id="91a83-132">Note that you could copy the entire view resource from your exported view file, but you would need to make the following changes for it to work in your solution.</span><span class="sxs-lookup"><span data-stu-id="91a83-132">Note that you could copy the entire view resource from your exported view file, but you would need to make the following changes for it to work in your solution.</span></span>  

* <span data-ttu-id="91a83-133">The **type** for the view resource needs to be changed from **views** to **Microsoft.OperationalInsights/workspaces**.</span><span class="sxs-lookup"><span data-stu-id="91a83-133">The **type** for the view resource needs to be changed from **views** to **Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="91a83-134">The **name** property for the view resource needs to be changed to include the workspace name.</span><span class="sxs-lookup"><span data-stu-id="91a83-134">The **name** property for the view resource needs to be changed to include the workspace name.</span></span>
* <span data-ttu-id="91a83-135">The dependency on the workspace needs to be removed since the workspace resource isn't defined in the solution.</span><span class="sxs-lookup"><span data-stu-id="91a83-135">The dependency on the workspace needs to be removed since the workspace resource isn't defined in the solution.</span></span>
* <span data-ttu-id="91a83-136">**DisplayName** property needs to be added to the view.</span><span class="sxs-lookup"><span data-stu-id="91a83-136">**DisplayName** property needs to be added to the view.</span></span>  <span data-ttu-id="91a83-137">The **Id**, **Name**, and **DisplayName** must all match.</span><span class="sxs-lookup"><span data-stu-id="91a83-137">The **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="91a83-138">Parameter names must be changed to match the required set of parameters.</span><span class="sxs-lookup"><span data-stu-id="91a83-138">Parameter names must be changed to match the required set of parameters.</span></span>
* <span data-ttu-id="91a83-139">Variables should be defined in the solution and used in the appropriate properties.</span><span class="sxs-lookup"><span data-stu-id="91a83-139">Variables should be defined in the solution and used in the appropriate properties.</span></span>

### <a name="log-analytics-api-version"></a><span data-ttu-id="91a83-140">Log Analytics API version</span><span class="sxs-lookup"><span data-stu-id="91a83-140">Log Analytics API version</span></span>
<span data-ttu-id="91a83-141">All Log Analytics resources defined in a Resource Manager template have a property **apiVersion** that defines the version of the API the resource should use.</span><span class="sxs-lookup"><span data-stu-id="91a83-141">All Log Analytics resources defined in a Resource Manager template have a property **apiVersion** that defines the version of the API the resource should use.</span></span>  <span data-ttu-id="91a83-142">This version is different for views with queries that use the [legacy and the upgraded query language](../log-analytics/log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="91a83-142">This version is different for views with queries that use the [legacy and the upgraded query language](../log-analytics/log-analytics-log-search-upgrade.md).</span></span>  

 <span data-ttu-id="91a83-143">The following table specifies the Log Analytics API versions for views in legacy and upgraded workspaces:</span><span class="sxs-lookup"><span data-stu-id="91a83-143">The following table specifies the Log Analytics API versions for views in legacy and upgraded workspaces:</span></span> 

| <span data-ttu-id="91a83-144">Workspace version</span><span class="sxs-lookup"><span data-stu-id="91a83-144">Workspace version</span></span> | <span data-ttu-id="91a83-145">API version</span><span class="sxs-lookup"><span data-stu-id="91a83-145">API version</span></span> | <span data-ttu-id="91a83-146">Query</span><span class="sxs-lookup"><span data-stu-id="91a83-146">Query</span></span> |
|:---|:---|:---|
| <span data-ttu-id="91a83-147">v1 (legacy)</span><span class="sxs-lookup"><span data-stu-id="91a83-147">v1 (legacy)</span></span>   | <span data-ttu-id="91a83-148">2015-11-01-preview</span><span class="sxs-lookup"><span data-stu-id="91a83-148">2015-11-01-preview</span></span> | <span data-ttu-id="91a83-149">Legacy format.</span><span class="sxs-lookup"><span data-stu-id="91a83-149">Legacy format.</span></span><br> <span data-ttu-id="91a83-150">Example: Type=Event EventLevelName = Error</span><span class="sxs-lookup"><span data-stu-id="91a83-150">Example: Type=Event EventLevelName = Error</span></span>  |
| <span data-ttu-id="91a83-151">v2 (upgraded)</span><span class="sxs-lookup"><span data-stu-id="91a83-151">v2 (upgraded)</span></span> | <span data-ttu-id="91a83-152">2015-11-01-preview</span><span class="sxs-lookup"><span data-stu-id="91a83-152">2015-11-01-preview</span></span> | <span data-ttu-id="91a83-153">Legacy format.</span><span class="sxs-lookup"><span data-stu-id="91a83-153">Legacy format.</span></span>  <span data-ttu-id="91a83-154">Converted to upgraded format on install.</span><span class="sxs-lookup"><span data-stu-id="91a83-154">Converted to upgraded format on install.</span></span><br> <span data-ttu-id="91a83-155">Example: Type=Event EventLevelName = Error</span><span class="sxs-lookup"><span data-stu-id="91a83-155">Example: Type=Event EventLevelName = Error</span></span><br><span data-ttu-id="91a83-156">Converted to: Event &#124; where EventLevelName == "Error"</span><span class="sxs-lookup"><span data-stu-id="91a83-156">Converted to: Event &#124; where EventLevelName == "Error"</span></span>  |
| <span data-ttu-id="91a83-157">v2 (upgraded)</span><span class="sxs-lookup"><span data-stu-id="91a83-157">v2 (upgraded)</span></span> | <span data-ttu-id="91a83-158">2017-03-03-preview</span><span class="sxs-lookup"><span data-stu-id="91a83-158">2017-03-03-preview</span></span> | <span data-ttu-id="91a83-159">Upgrade format.</span><span class="sxs-lookup"><span data-stu-id="91a83-159">Upgrade format.</span></span> <br><span data-ttu-id="91a83-160">Example: Event &#124; where EventLevelName == "Error"</span><span class="sxs-lookup"><span data-stu-id="91a83-160">Example: Event &#124; where EventLevelName == "Error"</span></span>  |


## <a name="add-the-view-details"></a><span data-ttu-id="91a83-161">Add the view details</span><span class="sxs-lookup"><span data-stu-id="91a83-161">Add the view details</span></span>
<span data-ttu-id="91a83-162">The view resource in the exported view file will contain two elements in the **properties** element named **Dashboard** and **OverviewTile** which contain the detailed configuration of the view.</span><span class="sxs-lookup"><span data-stu-id="91a83-162">The view resource in the exported view file will contain two elements in the **properties** element named **Dashboard** and **OverviewTile** which contain the detailed configuration of the view.</span></span>  <span data-ttu-id="91a83-163">Copy these two elements and their contents into the **properties** element of the view resource in your solution file.</span><span class="sxs-lookup"><span data-stu-id="91a83-163">Copy these two elements and their contents into the **properties** element of the view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="91a83-164">Example</span><span class="sxs-lookup"><span data-stu-id="91a83-164">Example</span></span>
<span data-ttu-id="91a83-165">For example, the following sample shows a simple solution file with a view.</span><span class="sxs-lookup"><span data-stu-id="91a83-165">For example, the following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="91a83-166">Ellipses (...) are shown for the **Dashboard** and **OverviewTile** contents for space reasons.</span><span class="sxs-lookup"><span data-stu-id="91a83-166">Ellipses (...) are shown for the **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspaceName": {
                "type": "string"
            },
            "accountName": {
                "type": "string"
            },
            "workspaceRegionId": {
                "type": "string"
            },
            "regionId": {
                "type": "string"
            },
            "pricingTier": {
                "type": "string"
            }
        },
        "variables": {
            "SolutionVersion": "1.1",
            "SolutionPublisher": "Contoso",
            "SolutionName": "Contoso Solution",
            "LogAnalyticsApiVersion": "2015-11-01-preview",
            "ViewAuthor":  "user@contoso.com",
            "ViewDescription":  "This is a sample view.",
            "ViewName":  "Contoso View"
        },
        "resources": [
            {
                "name": "[concat(variables('SolutionName'), '(' ,parameters('workspacename'), ')')]",
                "location": "[parameters('workspaceRegionId')]",
                "tags": { },
                "type": "Microsoft.OperationsManagement/solutions",
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "dependsOn": [
                    "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspacename'), '/views/', variables('ViewName'))]"
                ],
                "properties": {
                    "workspaceResourceId": "[concat(resourceGroup().id, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspacename'))]",
                    "referencedResources": [
                    ],
                    "containedResources": [
                        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/views/', variables('ViewName'))]"
                    ]
                },
                "plan": {
                    "name": "[concat(variables('SolutionName'), '(' ,parameters('workspaceName'), ')')]",
                    "Version": "[variables('SolutionVersion')]",
                    "product": "ContosoSolution",
                    "publisher": "[variables('SolutionPublisher')]",
                    "promotionCode": ""
                }
            },
            {
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
                "type": "Microsoft.OperationalInsights/workspaces/views",
                "location": "[parameters('workspaceregionId')]",
                "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
                "dependson": [
                ],
                "properties": {
                    "Id": "[variables('ViewName')]",
                    "Name": "[variables('ViewName')]",
                    "DisplayName": "[variables('ViewName')]",
                    "Description": "[variables('ViewDescription')]",
                    "Author": "[variables('ViewAuthor')]",
                    "Source": "Local",
                    "Dashboard": ...,
                    "OverviewTile": ...
                }
            }
          ]
    }




## <a name="next-steps"></a><span data-ttu-id="91a83-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="91a83-167">Next steps</span></span>
* <span data-ttu-id="91a83-168">Learn complete details of creating [management solutions](monitoring-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="91a83-168">Learn complete details of creating [management solutions](monitoring-solutions-creating.md).</span></span>
* <span data-ttu-id="91a83-169">Include [Automation runbooks in your management solution](monitoring-solutions-resources-automation.md).</span><span class="sxs-lookup"><span data-stu-id="91a83-169">Include [Automation runbooks in your management solution](monitoring-solutions-resources-automation.md).</span></span>
