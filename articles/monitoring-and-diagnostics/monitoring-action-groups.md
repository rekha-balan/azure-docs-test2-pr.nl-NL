---
title: Create and Manager Action Groups in Azure Portal | Microsoft Docs
description: ''
author: anirudhcavale
manager: carmonm
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ''
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 310ee8e3de58801c285ba97cb406d8ac16bdbf6a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670992"
---
# <a name="create-and-manage-action-groups-in-azure-portal"></a>Create and Manage Action Groups in Azure Portal
## <a name="overview"></a>Overview ##
This article shows you how to create and manage action groups in the Azure portal.

Action groups enable you to configure a list of receivers. These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when the activity log alert is triggered.

An action group can have up to 10 of each action type. An action is defined by the combination of:

**Name:** A unique identifier within the action group.  
**Action Type:** This defines the action that will be performed. Options are send SMS, send Email, or call a Webhook.  
**Details:** Based on the action type, the corresponding phone number, email address or webhook URI needs to be provided.

You can configure and get information about service health notification alerts using:
* [Azure Portal](monitoring-action-groups.md)
- [Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md)

## <a name="creating-an-action-group-for-the-azure-portal"></a>Creating an action group for the Azure portal ##
1.  In the [portal](https://portal.azure.com), navigate to the **Monitor** service

    ![Monitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-action-groups/home-monitor.PNG)
2.  Click the **Monitor** option to open up the Monitor blade. This blade brings together all your monitoring settings and data into one consolidated view. It first opens to the **Activity log** section.

3.  Now click on **Action groups** section

    ![Action-Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-action-groups/action-groups-blade.PNG)
4.  Click on the **Add** action group command and fill in the fields

    ![Add-Action-Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-action-groups/add-action-group.PNG)
5.  Provide a **Name** and **Short Name** for the action group; The Short Name will be referenced in notifications sent to this group

      ![Action-Group-Define](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-action-groups/action-group-define.PNG)

6.  The **Subscription** is the one the Action group will be saved in. It will be auto filled to the subscription you are currently operating under.

7.  Choose the **Resource Group** for this action group.

8.  Then, define a list of actions through a combination of:
  1. **Name:** A unique identifier within the action group.
  2. **Action Type:** This defines the action that will be performed. Options are send SMS, send Email, or call a Webhook.
  3. **Details:** Based on the action type, the corresponding phone number, email address or webhook URI needs to be provided.

9.  Select **OK** when done to create the action group.

## <a name="managing-your-action-groups"></a>Managing your action groups ##
Once you have created an action group, it will be visible in the Action groups section of the Monitor service. Select the action group you wish to manage, you will be able to:
* Add, edit, or remove receivers.
-   Delete the action group.

## <a name="next-steps"></a>Next Steps: ##
Learn more on [SMS alert behavior](monitoring-sms-alert-behavior.md)  
Get an [understanding of the activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)  
Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts  
Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how to get alerted  
How to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md)




