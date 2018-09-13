---
title: Creating management solutions in Operations Management Suite (OMS) | Microsoft Docs
description: Management solutions extend the functionality of Operations Management Suite (OMS) by providing packaged management scenarios that customers can add to their OMS workspace.  This article provides details on how you can create management solutions to be used in your own environment or made available to your customers.
services: operations-management-suite
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/17/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 742405395a3da792d0df01d7393a6e7fc7a55842
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671966"
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a>Creating a management solution file in Operations Management Suite (OMS) (Preview)
> [!NOTE]
> This is preliminary documentation for creating management solutions in OMS which are currently in preview. Any schema described below is subject to change.  

Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).  The main task in learning how to author management solutions is learning how to [author a template](../azure-resource-manager/resource-group-authoring-templates.md).  This article provides unique details of templates used for solutions and how to configure typical solution resources.


## <a name="tools"></a>Tools

You can use any text editor to work with solution files, but we recommend leveraging the features provided in Visual Studio or Visual Studio Code as described in the following articles.

- [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [Working with Azure Resource Manager Templates in Visual Studio Code](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a>Structure
The basic structure of a management solution file is the same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.  Each of the sections below describes the top level elements and and their contents in a solution.  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a>Parameters
[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from the user when they install the management solution.  There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.  How users will provide parameter values when they install your solution will depend on the particular parameter and how the solution is being installed.

When a user installs your management solution through the [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted to select an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).  These are used to populate the values of each of the standard parameters.  The user is not prompted to directly provide values for the standard parameters, but they are prompted to provide values for any additional parameters.

When the user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.

A sample parameter is shown below.  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

The following table describes the attributes of a parameter.

| Attribute | Description |
|:--- |:--- |
| type |Data type for the parameter. The input control displayed for the user depends on the data type.<br><br>bool - Drop down box<br>string - Text box<br>int - Text box<br>securestring - Password field<br> |
| category |Optional category for the parameter.  Parameters in the same category are grouped together. |
| control |Additional functionality for string parameters.<br><br>datetime - Datetime control is displayed.<br>guid - Guid value is automatically generated, and the parameter is not displayed. |
| description |Optional description for the parameter.  Displayed in an information balloon next to the parameter. |

### <a name="standard-parameters"></a>Standard parameters
The following table lists the standard parameters for all management solutions.  These values are populated for the user instead of prompting for them when your solution is installed from the Azure Marketplace or Quickstart templates.  The user must provide values for them if the solution is installed with another method.

> [!NOTE]
> The user interface in the Azure Marketplace and Quickstart templates is expecting the parameter names in the table.  If you use different parameter names then the user will be prompted for them, and they will not be automatically populated.
>
>

| Parameter | Type | Description |
|:--- |:--- |:--- |
| accountName |string |Azure Automation account name. |
| pricingTier |string |Pricing tier of both Log Analytics workspace and Azure Automation account. |
| regionId |string |Region of the Azure Automation account. |
| solutionName |string |Name of the solution.  If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring the user to specify one. |
| workspaceName |string |Log Analytics workspace name. |
| workspaceRegionId |string |Region of the Log Analytics workspace. |

### <a name="sample"></a>Sample
Following is a sample parameter entity for a solution.  This includes all of the standard  parameters and two additional parameters in the same category.

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of the Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of the Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        },
        "jobIdGuid": {
        "type": "string",
            "metadata": {
                "description": "GUID for a runbook job",
                "control": "guid",
                "category": "Schedule"
            }
        },
        "startTime": {
            "type": "string",
            "metadata": {
                "description": "Time for starting the runbook.",
                "control": "datetime",
                "category": "Schedule"
            }
        }


You refer to parameter values in other elements of the solution with the syntax **parameters('parameter name')**.  For example, to access the workspace name, you would use **parameters('workspaceName')**

## <a name="variables"></a>Variables
[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in the rest of the management solution.  These values are not exposed to the user installing the solution.  They are intended to provide the author with a single location where they can manage values that may be used multiple times throughout the solution. You should put any values specific to your solution in variables as opposed to hard coding them in the **resources** element.  This makes the code more readable and allows you to easily change these values in later versions.

Following is an example of a **variables** element with typical parameters used in solutions.

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

You refer to variable values through the solution with the syntax **variables('variable name')**.  For example, to access the SolutionName variable, you would use **variables('SolutionName')**.

You can also define complex variables that multiple sets of values.  These are particularly useful in management solutions where you are defining multiple properties for different types of resources.  For example, you could restructure the solution variables shown above to the following.

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

In this case, you refer to variable values through the solution with the syntax **variables('variable name').property**.  For example, to access the Solution Name variable, you would use **variables('Solution').Name**.

## <a name="resources"></a>Resources
[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define the different resources that your management solution will install and configure.  This will be the largest and most complex portion of the template.  You can get the structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).  Different resources that you will typically define are detailed in other articles in this documentation. 


### <a name="dependencies"></a>Dependencies
The **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.  When the solution is installed, a resource is not created until all of its dependencies have been created.  For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).  The job resource would be dependent on the runbook resource to make sure that the runbook is created before the job is created.

### <a name="oms-workspace-and-automation-account"></a>OMS workspace and Automation account
Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) to contain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) to contain runbooks and related resources.  These must be available before the resources in the solution are created and should not be defined in the solution itself.  The user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as the author you should consider the following points.

## <a name="solution-resource"></a>Solution resource
Each solution requires a resource entry in the **resources** element that defines the solution itself.  This will have a type of **Microsoft.OperationsManagement/solutions** and have the following structure. This includes [standard parameters](#parameters) and [variables](#variables) that are typically used to define properties of the solution.


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a>Dependencies
The solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in the solution since they need to exist before the solution can be created.  You do this by adding an entry for each resource in the **dependsOn** element.

### <a name="properties"></a>Properties
The solution resource has the properties in the following table.  This includes the resources referenced and contained by the solution which defines how the resource is managed after the solution is installed.  Each resource in the solution should be listed in either the **referencedResources** or the **containedResources** property.

| Property | Description |
|:--- |:--- |
| workspaceResourceId |ID of the Log Analytics workspace in the form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*. |
| referencedResources |List of resources in the solution that should not be removed when the solution is removed. |
| containedResources |List of resources in the solution that should be removed when the solution is removed. |

The example  above is for a solution with a runbook, a schedule, and view.  The schedule and runbook are *referenced* in the  **properties**  element so they are not removed when the solution is removed.  The view is *contained* so it is removed when the solution is removed.

### <a name="plan"></a>Plan
The **plan** entity of the solution resource has the properties in the following table.

| Property | Description |
|:--- |:--- |
| name |Name of the solution. |
| version |Version of the solution as determined by the author. |
| product |Unique string to identify the solution. |
| publisher |Publisher of the solution. |



## <a name="sample"></a>Sample
You can view samples of solution files with a solution resource at the following locations.

- [Automation resources](operations-management-suite-solutions-resources-automation.md#sample)
- [Search and alert resources](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a>Next steps
* [Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) to your management solution.
* [Add views](operations-management-suite-solutions-resources-views.md) to your management solution.
* [Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) to your management solution.
* Learn the details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).
* Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.
