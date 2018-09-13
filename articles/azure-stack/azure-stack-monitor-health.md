---
title: Monitor health and alerts in Azure Stack | Microsoft Docs
description: Learn how to monitor health and alerts in Azure Stack.
services: azure-stack
documentationcenter: ''
author: chasat-MS
manager: dsavage
editor: ''
ms.assetid: 69901c7b-4673-4bd8-acf2-8c6bdd9d1546
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: chasat
ms.openlocfilehash: 0ac519d6b6c1e1d390b67eab1f342f13474c6cff
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552563"
---
# <a name="monitor-health-and-alerts-in-azure-stack"></a>Monitor health and alerts in Azure Stack

Azure Stack includes infrastructure monitoring capabilities that enable a cloud administrator to view health and alerts for an Azure Stack region.

This preview release of Azure Stack has a set of region management capabilities available in the **Region Management** tile. The Region Management tile, pinned by default in the administrator portal for the Default Provider Subscription, lists all the deployed regions of Azure Stack. It also shows the count of active critical and warning alerts for each region. This tile is your entry point into the health and alert functionality of Azure Stack.

 ![The Region Management tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-monitor-health/image1.PNG)

 ## <a name="understand-health-in-azure-stack"></a>Understand health in Azure Stack

 Health and alerts are managed in Azure Stack by the Health resource provider. Azure Stack infrastructure components register with the Health resource provider during Azure Stack deployment and configuration. This registration enables the display of health and alerts for each component. Health in Azure Stack is a simple concept. If alerts for a registered instance of a component exist, the health state of that component reflects the worst active alert severity; warning, or critical.
 
 ## <a name="view-and-manage-component-health-state"></a>View and manage component health state
 
 You can view the health state of components in both the Azure Stack administrator portal and through Rest API and PowerShell.
 
To view the health state in the portal, click the region that you want to view in the **Region Management** tile. You can view the health state of infrastructure roles and of resource providers. However, in the TP3 release, not all infrastructure roles and resource providers report health state.

![List of infrastructure roles](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-monitor-health/image2.PNG)

You can click a resource provider or infrastructure role to view more detailed information.

New in TP3, you can restart or shut down an infrastructure role instance for troubleshooting purposes. To do this, click an infrastructure role, click the role instance, and then in the **Role Instance** blade, click **Restart**, **Shutdown**, or **Start**. (The available options depend on the current state.)

> [!WARNING]
>In an Azure Stack Proof of Concept (POC) environment, there is only one role instance for each infrastructure role. Therefore, if you restart or shut down a role instance, the functionality that the role offers is unavailable until the role instance starts. If you restart or shut down the MAS-XRP01 role instance (associated with the Infrastructure management controller), you must use Hyper-V Manager to start the virtual machine.
>
>
 
## <a name="view-alerts"></a>View alerts

The list of active alerts for each Azure Stack region is available directly from the Region Management blade. The first tile in the default configuration is the Alerts tile, which displays a summary of the critical and warning alerts for the region. You can pin the Alerts tile, like any other tile on this blade, to the dashboard for quick access.   

![Alerts tile that shows a warning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-monitor-health/image3.PNG)

By selecting the top portion of the **Alerts** tile, you navigate to the list of all active alerts for the region. If you select either the **Critical** or **Warning** line item within the tile, you navigate to a filtered list of alerts (Critical or Warning). 

![Filtered warning alerts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-monitor-health/image4.PNG)
  
The Alerts blade supports the ability to filter both on status (Active or Closed) and severity (Critical or Warning). The default view displays all Active alerts. All closed alerts are removed from the system after seven days.

![Filter pane to filter by critical or warning status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-monitor-health/image5.PNG)

The Alerts blade also exposes the **View API** action, which displays the Rest API that was used to generate the list view. This action provides a quick way to become familiar with the Rest API syntax that you can use to query alerts. You can use this API in automation or for integration with your existing datacenter monitoring, reporting, and ticketing solutions. 

![The View API option that shows the Rest API](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-monitor-health/image6.PNG)

From the Alerts blade, you can select an alert to navigate to the **Alert Details** blade. This blade displays all fields that are associated with the alert, and enables quick navigation to the affected component and source of the alert. For example, the following alert occurs if one of the infrastructure role instances goes offline or is not accessible.  

![The Alert Details blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-monitor-health/image7.PNG)

After the infrastructure role instance is back online, this alert automatically closes.

Now that you know more about health and viewing alerts in Azure Stack, it’s time to learn more about how to update Azure Stack.

## <a name="next-steps"></a>Next steps

[Manage updates in Azure Stack](azure-stack-updates.md)

[Region management in Azure Stack](azure-stack-region-management.md)







