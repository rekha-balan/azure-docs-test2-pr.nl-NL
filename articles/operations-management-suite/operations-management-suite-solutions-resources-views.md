---
title: Views in Operations Management Suite (OMS) management solutions | Microsoft Docs
description: 'Management solutions in Operations Management Suite (OMS) will typically include one or more views to visualize data.  This article describes how to export a view created by the View Designer and include it in a management solution. '
services: operations-management-suite
documentationcenter: ''
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 570b278c-2d47-4e5a-9828-7f01f31ddf8c
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 533b5564a805e0b41f2b1a4ad92e12b133220952
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549550"
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="0c5ca-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span><span class="sxs-lookup"><span data-stu-id="0c5ca-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="0c5ca-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="0c5ca-106">Any schema described below is subject to change.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-106">Any schema described below is subject to change.</span></span>    
>
>

<span data-ttu-id="0c5ca-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views to visualize data.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views to visualize data.</span></span>  <span data-ttu-id="0c5ca-108">This article describes how to export a view created by the [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-108">This article describes how to export a view created by the [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="0c5ca-109">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="0c5ca-109">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="0c5ca-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0c5ca-110">Prerequisites</span></span>
<span data-ttu-id="0c5ca-111">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of a solution file.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-111">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="0c5ca-112">Overview</span><span class="sxs-lookup"><span data-stu-id="0c5ca-112">Overview</span></span>
<span data-ttu-id="0c5ca-113">To include a view in a management solution, you create a **resource** for it in the [solution file](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="0c5ca-113">To include a view in a management solution, you create a **resource** for it in the [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="0c5ca-114">The JSON that describes the view's detailed configuration is typically complex though and not something that a typical solution author would be able to create manually.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-114">The JSON that describes the view's detailed configuration is typically complex though and not something that a typical solution author would be able to create manually.</span></span>  <span data-ttu-id="0c5ca-115">The most common method is to create the view using the [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration to the solution.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-115">The most common method is to create the view using the [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration to the solution.</span></span>

<span data-ttu-id="0c5ca-116">The basic steps to add a view to a solution are as follows.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-116">The basic steps to add a view to a solution are as follows.</span></span>  <span data-ttu-id="0c5ca-117">Each step is described in further detail in the sections below.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-117">Each step is described in further detail in the sections below.</span></span>

1. <span data-ttu-id="0c5ca-118">Export the view to a file.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-118">Export the view to a file.</span></span>
2. <span data-ttu-id="0c5ca-119">Create the view resource in the solution.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-119">Create the view resource in the solution.</span></span>
3. <span data-ttu-id="0c5ca-120">Add the view details.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-120">Add the view details.</span></span>

## <a name="export-the-view-to-a-file"></a><span data-ttu-id="0c5ca-121">Export the view to a file</span><span class="sxs-lookup"><span data-stu-id="0c5ca-121">Export the view to a file</span></span>
<span data-ttu-id="0c5ca-122">Follow the instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) to export a view to a file.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-122">Follow the instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) to export a view to a file.</span></span>  <span data-ttu-id="0c5ca-123">The exported file will be in JSON format with the same [elements as the solution file](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="0c5ca-123">The exported file will be in JSON format with the same [elements as the solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="0c5ca-124">The **resources** element of the view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents the OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-124">The **resources** element of the view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents the OMS workspace.</span></span>  <span data-ttu-id="0c5ca-125">This element will have a subelement with a type of **views** that represents the view and contains its detailed configuration.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-125">This element will have a subelement with a type of **views** that represents the view and contains its detailed configuration.</span></span>  <span data-ttu-id="0c5ca-126">You will copy the details of this element and then copy it into your solution.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-126">You will copy the details of this element and then copy it into your solution.</span></span>

## <a name="create-the-view-resource-in-the-solution"></a><span data-ttu-id="0c5ca-127">Create the view resource in the solution</span><span class="sxs-lookup"><span data-stu-id="0c5ca-127">Create the view resource in the solution</span></span>
<span data-ttu-id="0c5ca-128">Add the following view resource to the **resources** element of your solution file.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-128">Add the following view resource to the **resources** element of your solution file.</span></span>  <span data-ttu-id="0c5ca-129">This uses variables that are described below that you must also add.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="0c5ca-130">Note that the **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with the corresponding properties from the exported view file.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-130">Note that the **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with the corresponding properties from the exported view file.</span></span>

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

<span data-ttu-id="0c5ca-131">Add the following variables to the variables element of the solution file and replace the values to those for your solution.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-131">Add the following variables to the variables element of the solution file and replace the values to those for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of the view."
    "ViewName": "Provide a name for the view here."


<span data-ttu-id="0c5ca-132">Note that you could copy the entire view resource from your exported view file, but you would need to make the following changes for it to work in your solution.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-132">Note that you could copy the entire view resource from your exported view file, but you would need to make the following changes for it to work in your solution.</span></span>  

* <span data-ttu-id="0c5ca-133">The **type** for the view resource needs to be changed from **views** to **Microsoft.OperationalInsights/workspaces**.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-133">The **type** for the view resource needs to be changed from **views** to **Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="0c5ca-134">The **name** property for the view resource needs to be changed to include the workspace name.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-134">The **name** property for the view resource needs to be changed to include the workspace name.</span></span>
* <span data-ttu-id="0c5ca-135">The dependency on the workspace needs to be removed since the workspace resource isn't defined in the solution.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-135">The dependency on the workspace needs to be removed since the workspace resource isn't defined in the solution.</span></span>
* <span data-ttu-id="0c5ca-136">**DisplayName** property needs to be added to the view.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-136">**DisplayName** property needs to be added to the view.</span></span>  <span data-ttu-id="0c5ca-137">The **Id**, **Name**, and **DisplayName** must all match.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-137">The **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="0c5ca-138">Parameter names must be changed to match the required set of parameters.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-138">Parameter names must be changed to match the required set of parameters.</span></span>
* <span data-ttu-id="0c5ca-139">Variables should be defined in the solution and used in the appropriate properties.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-139">Variables should be defined in the solution and used in the appropriate properties.</span></span>

## <a name="add-the-view-details"></a><span data-ttu-id="0c5ca-140">Add the view details</span><span class="sxs-lookup"><span data-stu-id="0c5ca-140">Add the view details</span></span>
<span data-ttu-id="0c5ca-141">The view resource in the exported view file will contain two elements in the **properties** element named **Dashboard** and **OverviewTile** which contain the detailed configuration of the view.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-141">The view resource in the exported view file will contain two elements in the **properties** element named **Dashboard** and **OverviewTile** which contain the detailed configuration of the view.</span></span>  <span data-ttu-id="0c5ca-142">Copy these two elements and their contents into the **properties** element of the view resource in your solution file.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-142">Copy these two elements and their contents into the **properties** element of the view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="0c5ca-143">Example</span><span class="sxs-lookup"><span data-stu-id="0c5ca-143">Example</span></span>
<span data-ttu-id="0c5ca-144">For example, the following sample shows a simple solution file with a view.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-144">For example, the following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="0c5ca-145">Ellipses (...) are shown for the **Dashboard** and **OverviewTile** contents for space reasons.</span><span class="sxs-lookup"><span data-stu-id="0c5ca-145">Ellipses (...) are shown for the **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="0c5ca-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="0c5ca-146">Next steps</span></span>
* <span data-ttu-id="0c5ca-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="0c5ca-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="0c5ca-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span><span class="sxs-lookup"><span data-stu-id="0c5ca-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
