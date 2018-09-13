---
title: Monitor access, performance logs, backend health, and metrics for Application Gateway | Microsoft Docs
description: Learn how to enable and manage Access and Performance logs for Application Gateway
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: c13101a312f142cb8e6dc3da41efcd8a38a3ed20
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554370"
---
# <a name="backend-health-diagnostics-logging-and-metrics-for-application-gateway"></a>Backend health, diagnostics logging and metrics for Application Gateway

Azure provides the capability to monitor resources with logging and metrics. Application Gateway provides these capabilities with backend health, logging, and metrics.

[**Backend health**](#backend-health) - Application gateway provides the capability to monitor the health of the servers in the backend pools through the portal and through powershell. The health of the backend pools can also be found through the performance diagnostic logs.

[**Logging**](#enable-logging-with-powershell) - Logging allows for performance, access, and other logs to be saved or consumed from a resource for monitoring purposes.

[**Metrics**](#metrics) - Application gateway currently has one metric. This metric measures the throughput of the application gateway in Bytes per second.

## <a name="backend-health"></a>Backend health

Application gateway provides the capability to monitor the health of individual members of the backend pools through the portal, PowerShell, and CLI. Aggregated health summary of backend pools can also be found through the performance diagnostic logs. The backend health report reflects the output of the Application Gateway health probe to the backend instances. When probing is successful and the backend can be served traffic to, it is considered healthy, otherwise it is considered unhealthy.

> [!IMPORTANT]
> If there is an NSG on Application Gateway subnet, port ranges 65503-65534 should be opened on the Application Gateway subnet for Inbound traffic. These ports are required for the backend health API to work.


### <a name="view-backend-health-through-the-portal"></a>View backend health through the portal

There is nothing that is needed to be done to view backend health. In an existing application gateway, navigate to **Monitoring** > **Backend health**. Each member in the backend pool is listed on this page (whether it is a NIC, IP or FQDN). Backend pool name, port, backend http settings name and health status are shown. Valid values for health status are "Healthy", "Unhealthy" and "Unknown".

> [!WARNING]
> If you see a backend health status as **Unknown**, ensure that the access to backend is not blocked by a Network Security Group (NSG) rule or by a custom DNS in the VNet.

![backend health][10]

### <a name="view-backend-health-with-powershell"></a>View backend health with PowerShell

Backend health is also available to be retrieved through PowerShell. The following PowerShell code shows how to pull the backend health with the `Get-AzureRmApplicationGatewayBackendHealth` cmdlet.

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

The results are returned, an example of the response is shown in the following snippet.

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <a name="diagnostic-logging"></a>Diagnostic logging

You can use different types of logs in Azure to manage and troubleshoot application gateways. Some of these logs can be accessed through the portal, and all logs can be extracted from an Azure blob storage, and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and PowerBI. You can learn more about the different types of logs from the following list:

* **Activity log:** You can use [Azure Activity Log](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs and Audit Logs) to view all operations being submitted to your Azure subscription, and their status. Activity log entries are collected by default, and can be viewed in the Azure portal.
* **Access logs:** You can use this log to view application gateway access pattern and analyze important information including caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds. This log contains one record per instance of application gateway. The application gateway instance can be identified by 'instanceId' property.
* **Performance logs:** You can use this log to view how application gateway instances are performing. This log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count. Performance log is collected every 60 seconds.
* **Firewall logs:** You can use this log to view the requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.

> [!WARNING]
> Logs are only available for resources deployed in the Resource Manager deployment model. You cannot use logs for resources in the classic deployment model. For a better understanding of the two models, reference the [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.

For Logs, there are three different options to choose for storing your logs.

* Storage account - Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.
* Event hubs - Event hubs are a great option for integrating with other SEIM tools to get alerts on your resources
* Log analytics - Log analytics is best used for general real time monitoring of your application or looking at trends.

### <a name="enable-logging-with-powershell"></a>Enable logging with PowerShell

Activity logging is automatically enabled for every Resource Manager resource. You must enable access and performance logging to start collecting the data available through those logs. To enable logging, see the following steps:

1. Note your storage account's Resource ID, where the log data is stored. This value would be of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>. Any storage account in your subscription can be used. You can use the preview portal to find this information.

    ![Preview portal - Application Gateway Diagnostics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-diagnostics/diagnostics1.png)

2. Note your application gateway's Resource ID for which logging is to be enabled. This value would be of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>. You can use the preview portal to find this information.

    ![Preview portal - Application Gateway Diagnostics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-diagnostics/diagnostics2.png)

3. Enable diagnostics logging using the following powershell cmdlet:

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
>Activity logs do not require a separate storage account. The use of storage for access and performance logging incurs service charges.

### <a name="enable-logging-with-azure-portal"></a>Enable logging with Azure portal

#### <a name="step-1"></a>Step 1

Navigate to your resource in the Azure portal. Click **Diagnostic logs**. If this is the first time configuring diagnostics the blade looks like the following image:

For application gateway, 3 logs are available.

* Access Log
* Performance Log
* Firewall Log

To start collecting data, click **Turn on diagnostics**.

![diagnostics setting blade][1]

#### <a name="step-2"></a>Step 2

On the **Diagnostics settings** blade, the settings for how the diagnostic logs are set. In this example, Log analytics is used to store the logs. Click **Configure** under **Log Analytics** to configure your workspace. Event hubs and a storage account can be used to save the diagnostics logs as well.

![diagnostics blade][2]

#### <a name="step-3"></a>Step 3

Choose an existing OMS Workspace or create a new one. For this example, an existing one is used.

![oms workspaces][3]

#### <a name="step-4"></a>Step 4

When complete, confirm the settings and click **Save** to save the settings.

![confirm selection][4]

### <a name="activity-log"></a>Activity log

This log (formerly known as the "operational log") is generated by Azure by default.  The logs are preserved for 90 days in Azure’s Event Logs store. Learn more about these logs by reading the [View events and activity  log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.

### <a name="access-log"></a>Access log

This log is only generated if you've enabled it on a per Application Gateway basis as detailed in the preceding steps. The data is stored in the storage account you specified when you enabled the logging. Each access of Application Gateway is logged in JSON format, as seen in the following example:

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2016-04-11T04:24:37Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId":"ApplicationGatewayRole_IN_0",
        "clientIP":"37.186.113.170",
        "clientPort":"12345",
        "httpMethod":"HEAD",
        "requestUri":"/xyz/portal",
        "requestQuery":"",
        "userAgent":"-",
        "httpStatus":"200",
        "httpVersion":"HTTP/1.0",
        "receivedBytes":"27",
        "sentBytes":"202",
        "timeTaken":"359",
        "sslEnabled":"off"
    }
}
```

### <a name="performance-log"></a>Performance log

This log is only generated if you have enabled it on a per Application Gateway basis as detailed in the preceding steps. The data is stored in the storage account you specified when you enabled the logging. The following data is logged:

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> Latency is calculated from the time first byte of the HTTP request is received to the time the last byte of the HTTP response is sent. It is sum of Application Gateway processing time plus the network cost to the backend, plus the time taken by the backend to process request.

### <a name="firewall-log"></a>Firewall log

This log is only generated if you have enabled it on a per application gateway basis as detailed in the preceding steps. This log also requires that web application firewall is configured on an application gateway. The data is stored in the storage account you specified when you enabled the logging. The following data is logged:

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-the-activity-log"></a>View and analyze the activity log

You can view and analyze activity log data using any of the following methods:

* **Azure tools:** Retrieve information from the activity log through Azure PowerShell, the Azure Command Line Interface (CLI), the Azure REST API, or the Azure preview portal.  Step-by-step instructions for each method are detailed in the [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.
* **Power BI:** If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free. Using the [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/) you can analyze your data with pre-configured dashboards that you can use as-is, or customize.

## <a name="view-and-analyze-the-access-performance-and-firewall-log"></a>View and analyze the access, performance, and firewall log

Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect the counter and event log files from your Blob storage account and includes visualizations and powerful search capabilities to analyze your logs.

You can also connect to your storage account and retrieve the JSON log entries for access and performance logs. Once you download the JSON files, you can convert them to CSV and view in Excel, PowerBI, or any other data visualization tool.

> [!TIP]
> If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.
> 
> 

## <a name="metrics"></a>Metrics

Metrics is a feature for certain Azure resources where you can view performance counters in the portal. For Application Gateway, one metric is available at the time of writing this article. This metric is throughput, and can be seen in the portal. Navigate to an application gateway and click **Metrics**. To view the values, select throughput in the **Available metrics** section. In the following image, you can see an example with the filters that can be used to display the data in different time ranges.

To see a list of the current support metrics, visit [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md)

![metric view][5]

### <a name="alert-rules"></a>Alert rules

Alert rules can be started based of on metrics on a resource. This means for application gateway, an alert can call a webhook or email an administrator if the throughput of the application gateway is above, below or at a threshold for a specified period of time.

The following example will walk you through creating an alert rule that sends an email to an administrator after a throughput threshold has been breached.

#### <a name="step-1"></a>Step 1

Click **Add metric alert** to start. This blade can also be reached from the metrics blade.

![alert rules blade][6]

#### <a name="step-2"></a>Step 2

In the **Add rule** blade, fill out the name, condition, and notify sections and click **OK** when done.

The **Condition** selector allows for 4 values, **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.

The **Period** selector, allows for picking of a period from 5 minutes to 6 hours.

By selecting **Email owners, contributors, and readers**, the email can be dynamic based on the users that have access to that resource. Otherwise a comma separated list of users can be provided in the **Additional administrator email(s)** textbox.

![add rule blade][7]

If the threshold is breached, an email arrives similar to the one in the following image:

![threshold breached email][8]

A list of alerts is shown once a metric alert has been created and provides an overview of all the alert rules.

![alert rule view][9]

To learn more about alert notifications, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

To understand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md)

## <a name="next-steps"></a>Next steps

* Visualize counter and event logs with [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md)
* [Visualize your Azure Activity Log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.
* [View and analyze Azure Activity Log in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-diagnostics/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-diagnostics/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-diagnostics/figure3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-diagnostics/figure4.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-diagnostics/figure5.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-diagnostics/figure6.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-diagnostics/figure7.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-diagnostics/figure8.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-diagnostics/figure9.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-diagnostics/figure10.png











