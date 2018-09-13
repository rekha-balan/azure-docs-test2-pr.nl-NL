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
# <a name="backend-health-diagnostics-logging-and-metrics-for-application-gateway"></a><span data-ttu-id="8d71c-103">Backend health, diagnostics logging and metrics for Application Gateway</span><span class="sxs-lookup"><span data-stu-id="8d71c-103">Backend health, diagnostics logging and metrics for Application Gateway</span></span>

<span data-ttu-id="8d71c-104">Azure provides the capability to monitor resources with logging and metrics.</span><span class="sxs-lookup"><span data-stu-id="8d71c-104">Azure provides the capability to monitor resources with logging and metrics.</span></span> <span data-ttu-id="8d71c-105">Application Gateway provides these capabilities with backend health, logging, and metrics.</span><span class="sxs-lookup"><span data-stu-id="8d71c-105">Application Gateway provides these capabilities with backend health, logging, and metrics.</span></span>

<span data-ttu-id="8d71c-106">[**Backend health**](#backend-health) - Application gateway provides the capability to monitor the health of the servers in the backend pools through the portal and through powershell.</span><span class="sxs-lookup"><span data-stu-id="8d71c-106">[**Backend health**](#backend-health) - Application gateway provides the capability to monitor the health of the servers in the backend pools through the portal and through powershell.</span></span> <span data-ttu-id="8d71c-107">The health of the backend pools can also be found through the performance diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="8d71c-107">The health of the backend pools can also be found through the performance diagnostic logs.</span></span>

<span data-ttu-id="8d71c-108">[**Logging**](#enable-logging-with-powershell) - Logging allows for performance, access, and other logs to be saved or consumed from a resource for monitoring purposes.</span><span class="sxs-lookup"><span data-stu-id="8d71c-108">[**Logging**](#enable-logging-with-powershell) - Logging allows for performance, access, and other logs to be saved or consumed from a resource for monitoring purposes.</span></span>

<span data-ttu-id="8d71c-109">[**Metrics**](#metrics) - Application gateway currently has one metric.</span><span class="sxs-lookup"><span data-stu-id="8d71c-109">[**Metrics**](#metrics) - Application gateway currently has one metric.</span></span> <span data-ttu-id="8d71c-110">This metric measures the throughput of the application gateway in Bytes per second.</span><span class="sxs-lookup"><span data-stu-id="8d71c-110">This metric measures the throughput of the application gateway in Bytes per second.</span></span>

## <a name="backend-health"></a><span data-ttu-id="8d71c-111">Backend health</span><span class="sxs-lookup"><span data-stu-id="8d71c-111">Backend health</span></span>

<span data-ttu-id="8d71c-112">Application gateway provides the capability to monitor the health of individual members of the backend pools through the portal, PowerShell, and CLI.</span><span class="sxs-lookup"><span data-stu-id="8d71c-112">Application gateway provides the capability to monitor the health of individual members of the backend pools through the portal, PowerShell, and CLI.</span></span> <span data-ttu-id="8d71c-113">Aggregated health summary of backend pools can also be found through the performance diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="8d71c-113">Aggregated health summary of backend pools can also be found through the performance diagnostic logs.</span></span> <span data-ttu-id="8d71c-114">The backend health report reflects the output of the Application Gateway health probe to the backend instances.</span><span class="sxs-lookup"><span data-stu-id="8d71c-114">The backend health report reflects the output of the Application Gateway health probe to the backend instances.</span></span> <span data-ttu-id="8d71c-115">When probing is successful and the backend can be served traffic to, it is considered healthy, otherwise it is considered unhealthy.</span><span class="sxs-lookup"><span data-stu-id="8d71c-115">When probing is successful and the backend can be served traffic to, it is considered healthy, otherwise it is considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8d71c-116">If there is an NSG on Application Gateway subnet, port ranges 65503-65534 should be opened on the Application Gateway subnet for Inbound traffic.</span><span class="sxs-lookup"><span data-stu-id="8d71c-116">If there is an NSG on Application Gateway subnet, port ranges 65503-65534 should be opened on the Application Gateway subnet for Inbound traffic.</span></span> <span data-ttu-id="8d71c-117">These ports are required for the backend health API to work.</span><span class="sxs-lookup"><span data-stu-id="8d71c-117">These ports are required for the backend health API to work.</span></span>


### <a name="view-backend-health-through-the-portal"></a><span data-ttu-id="8d71c-118">View backend health through the portal</span><span class="sxs-lookup"><span data-stu-id="8d71c-118">View backend health through the portal</span></span>

<span data-ttu-id="8d71c-119">There is nothing that is needed to be done to view backend health.</span><span class="sxs-lookup"><span data-stu-id="8d71c-119">There is nothing that is needed to be done to view backend health.</span></span> <span data-ttu-id="8d71c-120">In an existing application gateway, navigate to **Monitoring** > **Backend health**.</span><span class="sxs-lookup"><span data-stu-id="8d71c-120">In an existing application gateway, navigate to **Monitoring** > **Backend health**.</span></span> <span data-ttu-id="8d71c-121">Each member in the backend pool is listed on this page (whether it is a NIC, IP or FQDN).</span><span class="sxs-lookup"><span data-stu-id="8d71c-121">Each member in the backend pool is listed on this page (whether it is a NIC, IP or FQDN).</span></span> <span data-ttu-id="8d71c-122">Backend pool name, port, backend http settings name and health status are shown.</span><span class="sxs-lookup"><span data-stu-id="8d71c-122">Backend pool name, port, backend http settings name and health status are shown.</span></span> <span data-ttu-id="8d71c-123">Valid values for health status are "Healthy", "Unhealthy" and "Unknown".</span><span class="sxs-lookup"><span data-stu-id="8d71c-123">Valid values for health status are "Healthy", "Unhealthy" and "Unknown".</span></span>

> [!WARNING]
> <span data-ttu-id="8d71c-124">If you see a backend health status as **Unknown**, ensure that the access to backend is not blocked by a Network Security Group (NSG) rule or by a custom DNS in the VNet.</span><span class="sxs-lookup"><span data-stu-id="8d71c-124">If you see a backend health status as **Unknown**, ensure that the access to backend is not blocked by a Network Security Group (NSG) rule or by a custom DNS in the VNet.</span></span>

![backend health][10]

### <a name="view-backend-health-with-powershell"></a><span data-ttu-id="8d71c-126">View backend health with PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d71c-126">View backend health with PowerShell</span></span>

<span data-ttu-id="8d71c-127">Backend health is also available to be retrieved through PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8d71c-127">Backend health is also available to be retrieved through PowerShell.</span></span> <span data-ttu-id="8d71c-128">The following PowerShell code shows how to pull the backend health with the `Get-AzureRmApplicationGatewayBackendHealth` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8d71c-128">The following PowerShell code shows how to pull the backend health with the `Get-AzureRmApplicationGatewayBackendHealth` cmdlet.</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

<span data-ttu-id="8d71c-129">The results are returned, an example of the response is shown in the following snippet.</span><span class="sxs-lookup"><span data-stu-id="8d71c-129">The results are returned, an example of the response is shown in the following snippet.</span></span>

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

## <a name="diagnostic-logging"></a><span data-ttu-id="8d71c-130">Diagnostic logging</span><span class="sxs-lookup"><span data-stu-id="8d71c-130">Diagnostic logging</span></span>

<span data-ttu-id="8d71c-131">You can use different types of logs in Azure to manage and troubleshoot application gateways.</span><span class="sxs-lookup"><span data-stu-id="8d71c-131">You can use different types of logs in Azure to manage and troubleshoot application gateways.</span></span> <span data-ttu-id="8d71c-132">Some of these logs can be accessed through the portal, and all logs can be extracted from an Azure blob storage, and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and PowerBI.</span><span class="sxs-lookup"><span data-stu-id="8d71c-132">Some of these logs can be accessed through the portal, and all logs can be extracted from an Azure blob storage, and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and PowerBI.</span></span> <span data-ttu-id="8d71c-133">You can learn more about the different types of logs from the following list:</span><span class="sxs-lookup"><span data-stu-id="8d71c-133">You can learn more about the different types of logs from the following list:</span></span>

* <span data-ttu-id="8d71c-134">**Activity log:** You can use [Azure Activity Log](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs and Audit Logs) to view all operations being submitted to your Azure subscription, and their status.</span><span class="sxs-lookup"><span data-stu-id="8d71c-134">**Activity log:** You can use [Azure Activity Log](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs and Audit Logs) to view all operations being submitted to your Azure subscription, and their status.</span></span> <span data-ttu-id="8d71c-135">Activity log entries are collected by default, and can be viewed in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8d71c-135">Activity log entries are collected by default, and can be viewed in the Azure portal.</span></span>
* <span data-ttu-id="8d71c-136">**Access logs:** You can use this log to view application gateway access pattern and analyze important information including caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span><span class="sxs-lookup"><span data-stu-id="8d71c-136">**Access logs:** You can use this log to view application gateway access pattern and analyze important information including caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span></span> <span data-ttu-id="8d71c-137">This log contains one record per instance of application gateway.</span><span class="sxs-lookup"><span data-stu-id="8d71c-137">This log contains one record per instance of application gateway.</span></span> <span data-ttu-id="8d71c-138">The application gateway instance can be identified by 'instanceId' property.</span><span class="sxs-lookup"><span data-stu-id="8d71c-138">The application gateway instance can be identified by 'instanceId' property.</span></span>
* <span data-ttu-id="8d71c-139">**Performance logs:** You can use this log to view how application gateway instances are performing.</span><span class="sxs-lookup"><span data-stu-id="8d71c-139">**Performance logs:** You can use this log to view how application gateway instances are performing.</span></span> <span data-ttu-id="8d71c-140">This log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span><span class="sxs-lookup"><span data-stu-id="8d71c-140">This log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="8d71c-141">Performance log is collected every 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="8d71c-141">Performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="8d71c-142">**Firewall logs:** You can use this log to view the requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span><span class="sxs-lookup"><span data-stu-id="8d71c-142">**Firewall logs:** You can use this log to view the requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span></span>

> [!WARNING]
> <span data-ttu-id="8d71c-143">Logs are only available for resources deployed in the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="8d71c-143">Logs are only available for resources deployed in the Resource Manager deployment model.</span></span> <span data-ttu-id="8d71c-144">You cannot use logs for resources in the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="8d71c-144">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="8d71c-145">For a better understanding of the two models, reference the [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span><span class="sxs-lookup"><span data-stu-id="8d71c-145">For a better understanding of the two models, reference the [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="8d71c-146">For Logs, there are three different options to choose for storing your logs.</span><span class="sxs-lookup"><span data-stu-id="8d71c-146">For Logs, there are three different options to choose for storing your logs.</span></span>

* <span data-ttu-id="8d71c-147">Storage account - Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span><span class="sxs-lookup"><span data-stu-id="8d71c-147">Storage account - Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="8d71c-148">Event hubs - Event hubs are a great option for integrating with other SEIM tools to get alerts on your resources</span><span class="sxs-lookup"><span data-stu-id="8d71c-148">Event hubs - Event hubs are a great option for integrating with other SEIM tools to get alerts on your resources</span></span>
* <span data-ttu-id="8d71c-149">Log analytics - Log analytics is best used for general real time monitoring of your application or looking at trends.</span><span class="sxs-lookup"><span data-stu-id="8d71c-149">Log analytics - Log analytics is best used for general real time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-with-powershell"></a><span data-ttu-id="8d71c-150">Enable logging with PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d71c-150">Enable logging with PowerShell</span></span>

<span data-ttu-id="8d71c-151">Activity logging is automatically enabled for every Resource Manager resource.</span><span class="sxs-lookup"><span data-stu-id="8d71c-151">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="8d71c-152">You must enable access and performance logging to start collecting the data available through those logs.</span><span class="sxs-lookup"><span data-stu-id="8d71c-152">You must enable access and performance logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="8d71c-153">To enable logging, see the following steps:</span><span class="sxs-lookup"><span data-stu-id="8d71c-153">To enable logging, see the following steps:</span></span>

1. <span data-ttu-id="8d71c-154">Note your storage account's Resource ID, where the log data is stored.</span><span class="sxs-lookup"><span data-stu-id="8d71c-154">Note your storage account's Resource ID, where the log data is stored.</span></span> <span data-ttu-id="8d71c-155">This value would be of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span><span class="sxs-lookup"><span data-stu-id="8d71c-155">This value would be of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="8d71c-156">Any storage account in your subscription can be used.</span><span class="sxs-lookup"><span data-stu-id="8d71c-156">Any storage account in your subscription can be used.</span></span> <span data-ttu-id="8d71c-157">You can use the preview portal to find this information.</span><span class="sxs-lookup"><span data-stu-id="8d71c-157">You can use the preview portal to find this information.</span></span>

    ![Preview portal - Application Gateway Diagnostics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="8d71c-159">Note your application gateway's Resource ID for which logging is to be enabled.</span><span class="sxs-lookup"><span data-stu-id="8d71c-159">Note your application gateway's Resource ID for which logging is to be enabled.</span></span> <span data-ttu-id="8d71c-160">This value would be of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span><span class="sxs-lookup"><span data-stu-id="8d71c-160">This value would be of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="8d71c-161">You can use the preview portal to find this information.</span><span class="sxs-lookup"><span data-stu-id="8d71c-161">You can use the preview portal to find this information.</span></span>

    ![Preview portal - Application Gateway Diagnostics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="8d71c-163">Enable diagnostics logging using the following powershell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8d71c-163">Enable diagnostics logging using the following powershell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="8d71c-164">Activity logs do not require a separate storage account.</span><span class="sxs-lookup"><span data-stu-id="8d71c-164">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="8d71c-165">The use of storage for access and performance logging incurs service charges.</span><span class="sxs-lookup"><span data-stu-id="8d71c-165">The use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="8d71c-166">Enable logging with Azure portal</span><span class="sxs-lookup"><span data-stu-id="8d71c-166">Enable logging with Azure portal</span></span>

#### <a name="step-1"></a><span data-ttu-id="8d71c-167">Step 1</span><span class="sxs-lookup"><span data-stu-id="8d71c-167">Step 1</span></span>

<span data-ttu-id="8d71c-168">Navigate to your resource in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8d71c-168">Navigate to your resource in the Azure portal.</span></span> <span data-ttu-id="8d71c-169">Click **Diagnostic logs**.</span><span class="sxs-lookup"><span data-stu-id="8d71c-169">Click **Diagnostic logs**.</span></span> <span data-ttu-id="8d71c-170">If this is the first time configuring diagnostics the blade looks like the following image:</span><span class="sxs-lookup"><span data-stu-id="8d71c-170">If this is the first time configuring diagnostics the blade looks like the following image:</span></span>

<span data-ttu-id="8d71c-171">For application gateway, 3 logs are available.</span><span class="sxs-lookup"><span data-stu-id="8d71c-171">For application gateway, 3 logs are available.</span></span>

* <span data-ttu-id="8d71c-172">Access Log</span><span class="sxs-lookup"><span data-stu-id="8d71c-172">Access Log</span></span>
* <span data-ttu-id="8d71c-173">Performance Log</span><span class="sxs-lookup"><span data-stu-id="8d71c-173">Performance Log</span></span>
* <span data-ttu-id="8d71c-174">Firewall Log</span><span class="sxs-lookup"><span data-stu-id="8d71c-174">Firewall Log</span></span>

<span data-ttu-id="8d71c-175">To start collecting data, click **Turn on diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="8d71c-175">To start collecting data, click **Turn on diagnostics**.</span></span>

![diagnostics setting blade][1]

#### <a name="step-2"></a><span data-ttu-id="8d71c-177">Step 2</span><span class="sxs-lookup"><span data-stu-id="8d71c-177">Step 2</span></span>

<span data-ttu-id="8d71c-178">On the **Diagnostics settings** blade, the settings for how the diagnostic logs are set.</span><span class="sxs-lookup"><span data-stu-id="8d71c-178">On the **Diagnostics settings** blade, the settings for how the diagnostic logs are set.</span></span> <span data-ttu-id="8d71c-179">In this example, Log analytics is used to store the logs.</span><span class="sxs-lookup"><span data-stu-id="8d71c-179">In this example, Log analytics is used to store the logs.</span></span> <span data-ttu-id="8d71c-180">Click **Configure** under **Log Analytics** to configure your workspace.</span><span class="sxs-lookup"><span data-stu-id="8d71c-180">Click **Configure** under **Log Analytics** to configure your workspace.</span></span> <span data-ttu-id="8d71c-181">Event hubs and a storage account can be used to save the diagnostics logs as well.</span><span class="sxs-lookup"><span data-stu-id="8d71c-181">Event hubs and a storage account can be used to save the diagnostics logs as well.</span></span>

![diagnostics blade][2]

#### <a name="step-3"></a><span data-ttu-id="8d71c-183">Step 3</span><span class="sxs-lookup"><span data-stu-id="8d71c-183">Step 3</span></span>

<span data-ttu-id="8d71c-184">Choose an existing OMS Workspace or create a new one.</span><span class="sxs-lookup"><span data-stu-id="8d71c-184">Choose an existing OMS Workspace or create a new one.</span></span> <span data-ttu-id="8d71c-185">For this example, an existing one is used.</span><span class="sxs-lookup"><span data-stu-id="8d71c-185">For this example, an existing one is used.</span></span>

![oms workspaces][3]

#### <a name="step-4"></a><span data-ttu-id="8d71c-187">Step 4</span><span class="sxs-lookup"><span data-stu-id="8d71c-187">Step 4</span></span>

<span data-ttu-id="8d71c-188">When complete, confirm the settings and click **Save** to save the settings.</span><span class="sxs-lookup"><span data-stu-id="8d71c-188">When complete, confirm the settings and click **Save** to save the settings.</span></span>

![confirm selection][4]

### <a name="activity-log"></a><span data-ttu-id="8d71c-190">Activity log</span><span class="sxs-lookup"><span data-stu-id="8d71c-190">Activity log</span></span>

<span data-ttu-id="8d71c-191">This log (formerly known as the "operational log") is generated by Azure by default.</span><span class="sxs-lookup"><span data-stu-id="8d71c-191">This log (formerly known as the "operational log") is generated by Azure by default.</span></span>  <span data-ttu-id="8d71c-192">The logs are preserved for 90 days in Azure’s Event Logs store.</span><span class="sxs-lookup"><span data-stu-id="8d71c-192">The logs are preserved for 90 days in Azure’s Event Logs store.</span></span> <span data-ttu-id="8d71c-193">Learn more about these logs by reading the [View events and activity  log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span><span class="sxs-lookup"><span data-stu-id="8d71c-193">Learn more about these logs by reading the [View events and activity  log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="8d71c-194">Access log</span><span class="sxs-lookup"><span data-stu-id="8d71c-194">Access log</span></span>

<span data-ttu-id="8d71c-195">This log is only generated if you've enabled it on a per Application Gateway basis as detailed in the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="8d71c-195">This log is only generated if you've enabled it on a per Application Gateway basis as detailed in the preceding steps.</span></span> <span data-ttu-id="8d71c-196">The data is stored in the storage account you specified when you enabled the logging.</span><span class="sxs-lookup"><span data-stu-id="8d71c-196">The data is stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="8d71c-197">Each access of Application Gateway is logged in JSON format, as seen in the following example:</span><span class="sxs-lookup"><span data-stu-id="8d71c-197">Each access of Application Gateway is logged in JSON format, as seen in the following example:</span></span>

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

### <a name="performance-log"></a><span data-ttu-id="8d71c-198">Performance log</span><span class="sxs-lookup"><span data-stu-id="8d71c-198">Performance log</span></span>

<span data-ttu-id="8d71c-199">This log is only generated if you have enabled it on a per Application Gateway basis as detailed in the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="8d71c-199">This log is only generated if you have enabled it on a per Application Gateway basis as detailed in the preceding steps.</span></span> <span data-ttu-id="8d71c-200">The data is stored in the storage account you specified when you enabled the logging.</span><span class="sxs-lookup"><span data-stu-id="8d71c-200">The data is stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="8d71c-201">The following data is logged:</span><span class="sxs-lookup"><span data-stu-id="8d71c-201">The following data is logged:</span></span>

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
> <span data-ttu-id="8d71c-202">Latency is calculated from the time first byte of the HTTP request is received to the time the last byte of the HTTP response is sent.</span><span class="sxs-lookup"><span data-stu-id="8d71c-202">Latency is calculated from the time first byte of the HTTP request is received to the time the last byte of the HTTP response is sent.</span></span> <span data-ttu-id="8d71c-203">It is sum of Application Gateway processing time plus the network cost to the backend, plus the time taken by the backend to process request.</span><span class="sxs-lookup"><span data-stu-id="8d71c-203">It is sum of Application Gateway processing time plus the network cost to the backend, plus the time taken by the backend to process request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="8d71c-204">Firewall log</span><span class="sxs-lookup"><span data-stu-id="8d71c-204">Firewall log</span></span>

<span data-ttu-id="8d71c-205">This log is only generated if you have enabled it on a per application gateway basis as detailed in the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="8d71c-205">This log is only generated if you have enabled it on a per application gateway basis as detailed in the preceding steps.</span></span> <span data-ttu-id="8d71c-206">This log also requires that web application firewall is configured on an application gateway.</span><span class="sxs-lookup"><span data-stu-id="8d71c-206">This log also requires that web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="8d71c-207">The data is stored in the storage account you specified when you enabled the logging.</span><span class="sxs-lookup"><span data-stu-id="8d71c-207">The data is stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="8d71c-208">The following data is logged:</span><span class="sxs-lookup"><span data-stu-id="8d71c-208">The following data is logged:</span></span>

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

### <a name="view-and-analyze-the-activity-log"></a><span data-ttu-id="8d71c-209">View and analyze the activity log</span><span class="sxs-lookup"><span data-stu-id="8d71c-209">View and analyze the activity log</span></span>

<span data-ttu-id="8d71c-210">You can view and analyze activity log data using any of the following methods:</span><span class="sxs-lookup"><span data-stu-id="8d71c-210">You can view and analyze activity log data using any of the following methods:</span></span>

* <span data-ttu-id="8d71c-211">**Azure tools:** Retrieve information from the activity log through Azure PowerShell, the Azure Command Line Interface (CLI), the Azure REST API, or the Azure preview portal.</span><span class="sxs-lookup"><span data-stu-id="8d71c-211">**Azure tools:** Retrieve information from the activity log through Azure PowerShell, the Azure Command Line Interface (CLI), the Azure REST API, or the Azure preview portal.</span></span>  <span data-ttu-id="8d71c-212">Step-by-step instructions for each method are detailed in the [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span><span class="sxs-lookup"><span data-stu-id="8d71c-212">Step-by-step instructions for each method are detailed in the [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="8d71c-213">**Power BI:** If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span><span class="sxs-lookup"><span data-stu-id="8d71c-213">**Power BI:** If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="8d71c-214">Using the [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/) you can analyze your data with pre-configured dashboards that you can use as-is, or customize.</span><span class="sxs-lookup"><span data-stu-id="8d71c-214">Using the [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/) you can analyze your data with pre-configured dashboards that you can use as-is, or customize.</span></span>

## <a name="view-and-analyze-the-access-performance-and-firewall-log"></a><span data-ttu-id="8d71c-215">View and analyze the access, performance, and firewall log</span><span class="sxs-lookup"><span data-stu-id="8d71c-215">View and analyze the access, performance, and firewall log</span></span>

<span data-ttu-id="8d71c-216">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect the counter and event log files from your Blob storage account and includes visualizations and powerful search capabilities to analyze your logs.</span><span class="sxs-lookup"><span data-stu-id="8d71c-216">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect the counter and event log files from your Blob storage account and includes visualizations and powerful search capabilities to analyze your logs.</span></span>

<span data-ttu-id="8d71c-217">You can also connect to your storage account and retrieve the JSON log entries for access and performance logs.</span><span class="sxs-lookup"><span data-stu-id="8d71c-217">You can also connect to your storage account and retrieve the JSON log entries for access and performance logs.</span></span> <span data-ttu-id="8d71c-218">Once you download the JSON files, you can convert them to CSV and view in Excel, PowerBI, or any other data visualization tool.</span><span class="sxs-lookup"><span data-stu-id="8d71c-218">Once you download the JSON files, you can convert them to CSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="8d71c-219">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span><span class="sxs-lookup"><span data-stu-id="8d71c-219">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="8d71c-220">Metrics</span><span class="sxs-lookup"><span data-stu-id="8d71c-220">Metrics</span></span>

<span data-ttu-id="8d71c-221">Metrics is a feature for certain Azure resources where you can view performance counters in the portal.</span><span class="sxs-lookup"><span data-stu-id="8d71c-221">Metrics is a feature for certain Azure resources where you can view performance counters in the portal.</span></span> <span data-ttu-id="8d71c-222">For Application Gateway, one metric is available at the time of writing this article.</span><span class="sxs-lookup"><span data-stu-id="8d71c-222">For Application Gateway, one metric is available at the time of writing this article.</span></span> <span data-ttu-id="8d71c-223">This metric is throughput, and can be seen in the portal.</span><span class="sxs-lookup"><span data-stu-id="8d71c-223">This metric is throughput, and can be seen in the portal.</span></span> <span data-ttu-id="8d71c-224">Navigate to an application gateway and click **Metrics**.</span><span class="sxs-lookup"><span data-stu-id="8d71c-224">Navigate to an application gateway and click **Metrics**.</span></span> <span data-ttu-id="8d71c-225">To view the values, select throughput in the **Available metrics** section.</span><span class="sxs-lookup"><span data-stu-id="8d71c-225">To view the values, select throughput in the **Available metrics** section.</span></span> <span data-ttu-id="8d71c-226">In the following image, you can see an example with the filters that can be used to display the data in different time ranges.</span><span class="sxs-lookup"><span data-stu-id="8d71c-226">In the following image, you can see an example with the filters that can be used to display the data in different time ranges.</span></span>

<span data-ttu-id="8d71c-227">To see a list of the current support metrics, visit [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="8d71c-227">To see a list of the current support metrics, visit [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md)</span></span>

![metric view][5]

### <a name="alert-rules"></a><span data-ttu-id="8d71c-229">Alert rules</span><span class="sxs-lookup"><span data-stu-id="8d71c-229">Alert rules</span></span>

<span data-ttu-id="8d71c-230">Alert rules can be started based of on metrics on a resource.</span><span class="sxs-lookup"><span data-stu-id="8d71c-230">Alert rules can be started based of on metrics on a resource.</span></span> <span data-ttu-id="8d71c-231">This means for application gateway, an alert can call a webhook or email an administrator if the throughput of the application gateway is above, below or at a threshold for a specified period of time.</span><span class="sxs-lookup"><span data-stu-id="8d71c-231">This means for application gateway, an alert can call a webhook or email an administrator if the throughput of the application gateway is above, below or at a threshold for a specified period of time.</span></span>

<span data-ttu-id="8d71c-232">The following example will walk you through creating an alert rule that sends an email to an administrator after a throughput threshold has been breached.</span><span class="sxs-lookup"><span data-stu-id="8d71c-232">The following example will walk you through creating an alert rule that sends an email to an administrator after a throughput threshold has been breached.</span></span>

#### <a name="step-1"></a><span data-ttu-id="8d71c-233">Step 1</span><span class="sxs-lookup"><span data-stu-id="8d71c-233">Step 1</span></span>

<span data-ttu-id="8d71c-234">Click **Add metric alert** to start.</span><span class="sxs-lookup"><span data-stu-id="8d71c-234">Click **Add metric alert** to start.</span></span> <span data-ttu-id="8d71c-235">This blade can also be reached from the metrics blade.</span><span class="sxs-lookup"><span data-stu-id="8d71c-235">This blade can also be reached from the metrics blade.</span></span>

![alert rules blade][6]

#### <a name="step-2"></a><span data-ttu-id="8d71c-237">Step 2</span><span class="sxs-lookup"><span data-stu-id="8d71c-237">Step 2</span></span>

<span data-ttu-id="8d71c-238">In the **Add rule** blade, fill out the name, condition, and notify sections and click **OK** when done.</span><span class="sxs-lookup"><span data-stu-id="8d71c-238">In the **Add rule** blade, fill out the name, condition, and notify sections and click **OK** when done.</span></span>

<span data-ttu-id="8d71c-239">The **Condition** selector allows for 4 values, **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span><span class="sxs-lookup"><span data-stu-id="8d71c-239">The **Condition** selector allows for 4 values, **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

<span data-ttu-id="8d71c-240">The **Period** selector, allows for picking of a period from 5 minutes to 6 hours.</span><span class="sxs-lookup"><span data-stu-id="8d71c-240">The **Period** selector, allows for picking of a period from 5 minutes to 6 hours.</span></span>

<span data-ttu-id="8d71c-241">By selecting **Email owners, contributors, and readers**, the email can be dynamic based on the users that have access to that resource.</span><span class="sxs-lookup"><span data-stu-id="8d71c-241">By selecting **Email owners, contributors, and readers**, the email can be dynamic based on the users that have access to that resource.</span></span> <span data-ttu-id="8d71c-242">Otherwise a comma separated list of users can be provided in the **Additional administrator email(s)** textbox.</span><span class="sxs-lookup"><span data-stu-id="8d71c-242">Otherwise a comma separated list of users can be provided in the **Additional administrator email(s)** textbox.</span></span>

![add rule blade][7]

<span data-ttu-id="8d71c-244">If the threshold is breached, an email arrives similar to the one in the following image:</span><span class="sxs-lookup"><span data-stu-id="8d71c-244">If the threshold is breached, an email arrives similar to the one in the following image:</span></span>

![threshold breached email][8]

<span data-ttu-id="8d71c-246">A list of alerts is shown once a metric alert has been created and provides an overview of all the alert rules.</span><span class="sxs-lookup"><span data-stu-id="8d71c-246">A list of alerts is shown once a metric alert has been created and provides an overview of all the alert rules.</span></span>

![alert rule view][9]

<span data-ttu-id="8d71c-248">To learn more about alert notifications, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="8d71c-248">To learn more about alert notifications, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="8d71c-249">To understand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="8d71c-249">To understand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d71c-250">Next steps</span><span class="sxs-lookup"><span data-stu-id="8d71c-250">Next steps</span></span>

* <span data-ttu-id="8d71c-251">Visualize counter and event logs with [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md)</span><span class="sxs-lookup"><span data-stu-id="8d71c-251">Visualize counter and event logs with [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md)</span></span>
* <span data-ttu-id="8d71c-252">[Visualize your Azure Activity Log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span><span class="sxs-lookup"><span data-stu-id="8d71c-252">[Visualize your Azure Activity Log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="8d71c-253">[View and analyze Azure Activity Log in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span><span class="sxs-lookup"><span data-stu-id="8d71c-253">[View and analyze Azure Activity Log in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

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











