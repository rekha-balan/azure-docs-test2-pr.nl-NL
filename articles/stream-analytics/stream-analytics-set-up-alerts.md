---
title: Set up alerts for queries in Stream Analytics | Microsoft Docs
description: Understanding Stream Analytics Alerting
keywords: set up alerts
services: stream-analytics
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 4fadc9f5d924e1a70d178760002c8c8f654d7057
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556457"
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a>Set up alerts for Azure Stream Analytics jobs
## <a name="introduction-monitor-page"></a>Introduction: Monitor page
You can set up alerts to trigger an alert when a metric reaches a condition that you specify.

For example, “If Output Events for the last 15 minutes is <100, send email notification to email id: xyz@company.com”.

Rules can be set up on metrics through the portal, or can be configured [programmatically](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Operation Logs data.

## <a name="set-up-alerts-through-the-azure-classic-portal"></a>Set up alerts through the Azure Classic Portal
There are two ways to set up alerts in the Azure Classic portal:  

1. The **Monitor** tab of your Stream Analytics job  
2. The Operations Log in the Management services  

## <a name="set-up-alert-through-the-monitor-tab-of-the-job-in-the-portal"></a>Set up alert through the Monitor tab of the job in the portal
1. Select the metric in the monitor tab, and click the **Add Rule** button in the bottom of the dashboard, and setup your rules.  
   
   ![Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-set-up-alerts/01-stream-analytics-set-up-alerts.png)  
2. Define the name and description of the Alert  
   
   ![Create Rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-set-up-alerts/02-stream-analytics-set-up-alerts.png)  
3. Enter the thresholds, alert evaluation window and the actions for the alert  
   
   ![Define Conditions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-set-up-alerts/03-stream-analytics-set-up-alerts.png)  

## <a name="set-up-alerts-through-the-operations-logs"></a>Set up alerts through the Operations logs
1. Go to the **Alerts** tab in Management Services in the [Azure Classic Portal](https://manage.windowsazure.com).  
2. Click **Add Rule**  
   
   ![Criteria](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-set-up-alerts/04-stream-analytics-set-up-alerts.png)  
3. Define the name and description of the Alert. Select ‘Stream Analytics’ as Service Type, and the job name as the Service Name.  
   
   ![Define Alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-set-up-alerts/05-stream-analytics-set-up-alerts.png)  

## <a name="set-up-alerts-in-the-azure-portal"></a>Set up alerts in the Azure portal
In the Azure portal, browse to the Stream Analytics job you are interested in alerting on and click the **Monitoring** section.  In the **Metric** blade that opens, click the **Add alert** command.

  ![Azure portal setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

You can name your alert rule, and choose a description that will show up in the notification email.

When you select Metrics you'll choose a condition and threshold Value for the metric.

  ![Azure portal select metric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-set-up-alerts/07-stream-analytics-set-up-alerts.png)  

For more detail on configuring alerts in the Azure portal, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).  

## <a name="get-help"></a>Get help
For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Next steps
* [Introduction to Azure Stream Analytics](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics](stream-analytics-get-started.md)
* [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference](https://msdn.microsoft.com/library/azure/dn835031.aspx)








