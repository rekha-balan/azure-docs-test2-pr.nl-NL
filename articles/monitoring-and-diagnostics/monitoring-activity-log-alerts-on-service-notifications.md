---
title: Receive Activity Log Alerts on Service Notifications | Microsoft Docs
description: Get notified via SMS, email or webhook when Azure service occur.
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
ms.openlocfilehash: fd5566e20d5c98c37a2d05aa47592515df9f24cc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564271"
---
# <a name="create-activity-log-alerts-on-service-notifications"></a>Create Activity Log Alerts on Service Notifications
## <a name="overview"></a>Overview
This article shows you how to set up activity log alerts for service health notifications using the Azure portal.  

You can receive an alert based on service health notifications for your Azure subscription.  
You can configure the alert based on:
- The class of service health notification (Incident, Maintenance, Information, etc.)
- The status of the notification (Active vs. Resolved)
- The level of the notifications (Informational, Warning, Error)

You can also the configure who the alert should be sent to:
- Select an existing Action Group
- Create a new Action Group (that can be later used for future alerts)

You can learn more about Action Groups [here](monitoring-action-groups.md)

You can configure and get information about service health notification alerts using
- [Azure Portal](monitoring-activity-log-alerts-on-service-notifications.md)
- [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md)

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-with-the-azure-portal"></a>Create an alert on a service health notification for a new action group with the Azure Portal
1.  In the [portal](https://portal.azure.com), navigate to the **Monitor** service

    ![Monitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.PNG)

2.  Click the **Monitor** option to open the Monitor blade. It first opens to the **Activity log** section.

3.  Now click on the **Alerts** section.

    ![Alerts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.PNG)

4.  Select the **Add activity log alert** command and fill in the fields

    ![Add-Alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.PNG)

5.  **Name** your activity log alert, and choose a **Description**. These will appear in the notifications sent when this alert fires.

    ![Add-Alert-New-Action-Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.PNG)

6.  The **Subscription** should be auto filled to the subscription you are currently operating under.

7.  Choose the **Resource Group** for this alert.

8.  Under **Event Category** select the ‘Service Health’ option. Choose for what **Type, Status** and **Level** of Service Health Notifications you would like to be notified.

9.  Create a **New** Action Group by giving it **Name** and **Short Name**; the Short Name will be referenced in the notifications sent when this alert fires.

10. Then, define a list of receivers by providing the receiver’s

    a. **Name:** Receiver’s name, alias or identifier.

    b. **Action Type:** Choose to contact the receiver via SMS, Email, or Webhook

    c. **Details:** Based on the action type chosen, provide a phone number, email address or webhook URI.

11. Select **OK** when done to create the alert.

Within a few minutes, the alert is active and triggers as previously described.

For details on the webhook schema for activity log alerts [click here](monitoring-activity-log-alerts-webhook.md)

>[!NOTE]
>The action group defined in these steps will be reusable, as an existing action group, for all future alert definition.
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-with-the-azure-portal"></a>Create an alert on a service health notification for an existing action group with the Azure Portal
1.  In the [portal](https://portal.azure.com), navigate to the **Monitor** service

    ![Monitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.PNG)
2.  Click the **Monitor** option to open the Monitor blade. It first opens to the **Activity log** section.

3.  Now click on the **Alerts** section.

    ![Alerts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.PNG)
4.  Select the **Add activity log alert** command and fill in the fields

    ![Add-Alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.PNG)
5.  **Name** your activity log alert, and choose a **Description**. These will appear in the notifications sent when this alert fires.

    ![Add-Alert-Existing-Action-Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-existing-action-group.PNG)
6.  The **Subscription** should be auto filled to the subscription you are currently operating under.

7.  Choose the **Resource Group** for this alert.

8.  Under **Event Category** select the ‘Service Health’ option. Choose for what **Type, Status** and **Level** of Service Health Notifications you would like to be notified.

9.  Choose to **Notify Via** an **Existing action group**. Select the respective action group.

10. Select **OK** when done to create the alert.

Within a few minutes, the alert is active and triggers as previously described.

## <a name="managing-your-alerts"></a>Managing your alerts

Once you have created an alert, it will be visible in the Alerts section of the Monitor service. Select the alert you wish to manage, you will be able to:
* **Edit** it.
* **Delete** it.
* **Disable** or **Enable** it if you want to temporarily stop of resume receiving notifications for the alert.

## <a name="next-steps"></a>Next Steps:
Learn about [Service Health Notifications](monitoring-service-notifications.md)  
Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md) Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how to get alerted  
Learn more about [action groups](monitoring-action-groups.md)








