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
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a>Views in Operations Management Suite (OMS) management solutions (Preview)
> [!NOTE]
> This is preliminary documentation for creating management solutions in OMS which are currently in preview. Any schema described below is subject to change.    
>
>

[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views to visualize data.  This article describes how to export a view created by the [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.  

> [!NOTE]
> The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)
>
>

## <a name="prerequisites"></a>Prerequisites
This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of a solution file.

## <a name="overview"></a>Overview
To include a view in a management solution, you create a **resource** for it in the [solution file](operations-management-suite-solutions-creating.md).  The JSON that describes the view's detailed configuration is typically complex though and not something that a typical solution author would be able to create manually.  The most common method is to create the view using the [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration to the solution.

The basic steps to add a view to a solution are as follows.  Each step is described in further detail in the sections below.

1. Export the view to a file.
2. Create the view resource in the solution.
3. Add the view details.

## <a name="export-the-view-to-a-file"></a>Export the view to a file
Follow the instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) to export a view to a file.  The exported file will be in JSON format with the same [elements as the solution file](operations-management-suite-solutions-solution-file.md).  

The **resources** element of the view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents the OMS workspace.  This element will have a subelement with a type of **views** that represents the view and contains its detailed configuration.  You will copy the details of this element and then copy it into your solution.

## <a name="create-the-view-resource-in-the-solution"></a>Create the view resource in the solution
Add the following view resource to the **resources** element of your solution file.  This uses variables that are described below that you must also add.  Note that the **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with the corresponding properties from the exported view file.

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

Add the following variables to the variables element of the solution file and replace the values to those for your solution.

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of the view."
    "ViewName": "Provide a name for the view here."


Note that you could copy the entire view resource from your exported view file, but you would need to make the following changes for it to work in your solution.  

* The **type** for the view resource needs to be changed from **views** to **Microsoft.OperationalInsights/workspaces**.
* The **name** property for the view resource needs to be changed to include the workspace name.
* The dependency on the workspace needs to be removed since the workspace resource isn't defined in the solution.
* **DisplayName** property needs to be added to the view.  The **Id**, **Name**, and **DisplayName** must all match.
* Parameter names must be changed to match the required set of parameters.
* Variables should be defined in the solution and used in the appropriate properties.

## <a name="add-the-view-details"></a>Add the view details
The view resource in the exported view file will contain two elements in the **properties** element named **Dashboard** and **OverviewTile** which contain the detailed configuration of the view.  Copy these two elements and their contents into the **properties** element of the view resource in your solution file.

## <a name="example"></a>Example
For example, the following sample shows a simple solution file with a view.  Ellipses (...) are shown for the **Dashboard** and **OverviewTile** contents for space reasons.

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




## <a name="next-steps"></a>Next steps
* Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).
* Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).
