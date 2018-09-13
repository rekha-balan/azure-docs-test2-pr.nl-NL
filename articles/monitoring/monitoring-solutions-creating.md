---
title: Build a management solution in Azure | Microsoft Docs
description: Management solutions include packaged management scenarios in Azure that customers can add to their Log Analytics workspace.  This article provides details on how you can create management solutions to be used in your own environment or made available to your customers.
services: monitoring
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: monitoring
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a07a17105b4d84b51689e9636cfacc7a3b5428ad
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857980"
---
# <a name="design-and-build-a-management-solution-in-azure-preview"></a>Design and build a management solution in Azure (Preview)
> [!NOTE]
> This is preliminary documentation for creating management solutions in Azure which are currently in preview. Any schema described below is subject to change.

[Management solutions]( monitoring-solutions.md) provide packaged management scenarios that customers can add to their Log Analytics workspace.  This article presents a basic process to design and build a management solution that is suitable for most common requirements.  If you are new to building management solutions then you can use this process as a starting point and then leverage the concepts for more complex solutions as your requirements evolve.

## <a name="what-is-a-management-solution"></a>What is a management solution?

Management solutions contain Azure resources that work together to achieve a particular management scenario.  They are implemented as [Resource Management templates](../azure-resource-manager/resource-manager-template-walkthrough.md) that contain details of how to install and configure their contained resources when the solution is installed.

The basic strategy is to start your management solution by building the individual components in your Azure environment.  Once you have the functionality working properly, then you can start packaging them into a [management solution file]( monitoring-solutions-solution-file.md). 


## <a name="design-your-solution"></a>Design your solution
The most common pattern for a management solution is shown in the following diagram.  The different components in this pattern are discussed in the below.

![Management solution overview](media/monitoring-solutions-creating/solution-overview.png)


### <a name="data-sources"></a>Data sources
The first step in designing a solution is determining the data that you require from the Log Analytics repository.  This data may be collected by a [data source](../log-analytics/log-analytics-data-sources.md) or [another solution]( monitoring-solutions.md), or your solution may need to provide the process to collect it.

There are a number of ways data sources that can be collected in the Log Analytics repository as described in [Data sources in Log Analytics](../log-analytics/log-analytics-data-sources.md).  This includes events in the Windows Event Log or generated by Syslog in addition to performance counters for both Windows and Linux clients.  You can also gather data from Azure resources collected by Azure Monitor.  

If you require data that's not accessible through any of the available data sources, then you can use the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) which allows you to write data to the Log Analytics repository from any client that can call a REST API.  The most common means of custom data collection in a management solution is to create a [runbook in Azure Automation](../automation/automation-runbook-types.md) that collects the required data from Azure or external resources and uses the Data Collector API to write to the repository.  

### <a name="log-searches"></a>Log searches
[Log searches](../log-analytics/log-analytics-log-searches.md) are used to extract and analyze data in the Log Analytics repository.  They are used by views and alerts in addition to allowing the user to perform ad hoc analysis of data in the repository.  

You should define any queries that you think will be helpful to the user even if they aren't used by any views or alerts.  These will be available to them as Saved Searches in the portal, and you can also include them in a [List of Queries visualization part](../log-analytics/log-analytics-view-designer-parts.md#list-of-queries-part) in your custom view.

### <a name="alerts"></a>Alerts
[Alerts in Log Analytics](../log-analytics/log-analytics-alerts.md) identify issues through [log searches](#log-searches) against the data in the repository.  They either notify the user or automatically run an action in response. You should identify different alert conditions for your application and include corresponding alert rules in your solution file.

If the issue can potentially be corrected with an automated process, then you'll typically create a runbook in Azure Automation to perform this remediation.  Most Azure services can be managed with [cmdlets](/powershell/azure/overview) which the runbook would leverage to perform such functionality.

If your solution requires external functionality in response to an alert, then you can use a [webhook response](../log-analytics/log-analytics-alerts-actions.md).  This allows you to call an external web service sending information from the alert.

### <a name="views"></a>Views
Views in Log Analytics are used to visualize data from the Log Analytics repository.  Each solution will typically contain a single view with a [tile](../log-analytics/log-analytics-view-designer-tiles.md) that is displayed on the user's main dashboard.  The view can contain any number of [visualization parts](../log-analytics/log-analytics-view-designer-parts.md) to provide different visualizations of the collected data to the user.

You [create custom views using the View Designer](../log-analytics/log-analytics-view-designer.md) which you can later export for inclusion in your solution file.  


## <a name="create-solution-file"></a>Create solution file
Once you've configured and tested the components that will be part of your solution, you can [create your solution file]( monitoring-solutions-solution-file.md).  You will implement the solution components in a [Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) that includes a [solution resource]( monitoring-solutions-solution-file.md#solution-resource) with relationships to the other resources in the file.  


## <a name="test-your-solution"></a>Test your solution
While you are developing your solution, you will need to install and test it in your workspace.  You can do this using any of the available methods to [test and install Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="publish-your-solution"></a>Publish your solution
Once you have completed and tested your solution, you can make it available to customers through either the following sources.

- **Azure Quickstart templates**.  [Azure Quickstart templates](https://azure.microsoft.com/resources/templates/) is a set of Resource Manager templates contributed by the community through GitHub.  You can make your solution available by following information in the [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE).
- **Azure Marketplace**.  The [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/) allows you to distribute and sell your solution to other developers, ISVs, and IT professionals.  You can learn how to publish your solution to Azure Marketplace at [How to publish and manage an offer in the Azure Marketplace](../marketplace/marketplace-publishers-guide.md).



## <a name="next-steps"></a>Next steps
* Learn how to [create a solution file]( monitoring-solutions-solution-file.md) for your management solution.
* Learn the details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).
* Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.