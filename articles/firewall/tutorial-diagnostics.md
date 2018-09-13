---
title: Tutorial - Monitor Azure Firewall logs
description: In this tutorial, you learn how to enable and manage Azure Firewall logs.
services: firewall
author: vhorne
ms.service: firewall
ms.topic: tutorial
ms.workload: infrastructure-services
ms.date: 7/11/2018
ms.author: victorh
ms.openlocfilehash: a4922fda80b957138a9929090f9d3c349348185d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867883"
---
# <a name="tutorial-monitor-azure-firewall-logs"></a><span data-ttu-id="11201-103">Tutorial: Monitor Azure Firewall logs</span><span class="sxs-lookup"><span data-stu-id="11201-103">Tutorial: Monitor Azure Firewall logs</span></span>

[!INCLUDE [firewall-preview-notice](../../includes/firewall-preview-notice.md)]

<span data-ttu-id="11201-104">The examples in the Azure Firewall articles assume that you have already enabled the Azure Firewall public preview.</span><span class="sxs-lookup"><span data-stu-id="11201-104">The examples in the Azure Firewall articles assume that you have already enabled the Azure Firewall public preview.</span></span> <span data-ttu-id="11201-105">For more information, see [Enable the Azure Firewall public preview](public-preview.md).</span><span class="sxs-lookup"><span data-stu-id="11201-105">For more information, see [Enable the Azure Firewall public preview](public-preview.md).</span></span>

<span data-ttu-id="11201-106">You can monitor Azure Firewall using firewall logs.</span><span class="sxs-lookup"><span data-stu-id="11201-106">You can monitor Azure Firewall using firewall logs.</span></span> <span data-ttu-id="11201-107">You can also use activity logs to audit operations on Azure Firewall resources.</span><span class="sxs-lookup"><span data-stu-id="11201-107">You can also use activity logs to audit operations on Azure Firewall resources.</span></span>

<span data-ttu-id="11201-108">You can access some of these logs through the portal.</span><span class="sxs-lookup"><span data-stu-id="11201-108">You can access some of these logs through the portal.</span></span> <span data-ttu-id="11201-109">Logs can be sent to [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Storage, and Event Hubs and analyzed in Log Analytics or by different tools such as Excel and Power BI.</span><span class="sxs-lookup"><span data-stu-id="11201-109">Logs can be sent to [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Storage, and Event Hubs and analyzed in Log Analytics or by different tools such as Excel and Power BI.</span></span>

<span data-ttu-id="11201-110">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="11201-110">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="11201-111">Enable logging through the Azure portal</span><span class="sxs-lookup"><span data-stu-id="11201-111">Enable logging through the Azure portal</span></span>
> * <span data-ttu-id="11201-112">Enable logging with PowerShell</span><span class="sxs-lookup"><span data-stu-id="11201-112">Enable logging with PowerShell</span></span>
> * <span data-ttu-id="11201-113">View and analyze the activity log</span><span class="sxs-lookup"><span data-stu-id="11201-113">View and analyze the activity log</span></span>
> * <span data-ttu-id="11201-114">View and analyze the network and application rule logs</span><span class="sxs-lookup"><span data-stu-id="11201-114">View and analyze the network and application rule logs</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="11201-115">Diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="11201-115">Diagnostic logs</span></span>

 <span data-ttu-id="11201-116">The following diagnostic logs are available for Azure Firewall:</span><span class="sxs-lookup"><span data-stu-id="11201-116">The following diagnostic logs are available for Azure Firewall:</span></span>

* <span data-ttu-id="11201-117">**Application rule log**</span><span class="sxs-lookup"><span data-stu-id="11201-117">**Application rule log**</span></span>

   <span data-ttu-id="11201-118">The Application rule log is saved to a storage account, streamed to Event hubs and/or sent to Log Analytics only if you have enabled it for each Azure Firewall.</span><span class="sxs-lookup"><span data-stu-id="11201-118">The Application rule log is saved to a storage account, streamed to Event hubs and/or sent to Log Analytics only if you have enabled it for each Azure Firewall.</span></span> <span data-ttu-id="11201-119">Each new connection that matches one of your configured application rules results in a log for the accepted/denied connection.</span><span class="sxs-lookup"><span data-stu-id="11201-119">Each new connection that matches one of your configured application rules results in a log for the accepted/denied connection.</span></span> <span data-ttu-id="11201-120">The data is logged in JSON format, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="11201-120">The data is logged in JSON format, as shown in the following example:</span></span>

   ```
   Category: access logs are either application or network rule logs.
   Time: log timestamp.
   Properties: currently contains the full message. 
   note: this field will be parsed to specific fields in the future, while maintaining backward compatibility with the existing properties field.
   ```

   ```json
   {
    "category": "AzureFirewallApplicationRule",
    "time": "2018-04-16T23:45:04.8295030Z",
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/AZUREFIREWALLS/{resourceName}",
    "operationName": "AzureFirewallApplicationRuleLog",
    "properties": {
        "msg": "HTTPS request from 10.1.0.5:55640 to mydestination.com:443. Action: Allow. Rule Collection: collection1000. Rule: rule1002"
    }
   }
   ```

* <span data-ttu-id="11201-121">**Network rule log**</span><span class="sxs-lookup"><span data-stu-id="11201-121">**Network rule log**</span></span>

   <span data-ttu-id="11201-122">The Network rule log is saved to a storage account, streamed to Event hubs and/or sent Log Analytics only if you have enabled it for each Azure Firewall.</span><span class="sxs-lookup"><span data-stu-id="11201-122">The Network rule log is saved to a storage account, streamed to Event hubs and/or sent Log Analytics only if you have enabled it for each Azure Firewall.</span></span> <span data-ttu-id="11201-123">Each new connection that matches one of your configured network rules results in a log for the accepted/denied connection.</span><span class="sxs-lookup"><span data-stu-id="11201-123">Each new connection that matches one of your configured network rules results in a log for the accepted/denied connection.</span></span> <span data-ttu-id="11201-124">The data is logged in JSON format, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="11201-124">The data is logged in JSON format, as shown in the following example:</span></span>

   ```
   Category: access logs are either application or network rule logs.
   Time: log timestamp.
   Properties: currently contains the full message. 
   note: this field will be parsed to specific fields in the future, while maintaining backward compatibility with the existing properties field.
   ```

   ```json
  {
    "category": "AzureFirewallNetworkRule",
    "time": "2018-06-14T23:44:11.0590400Z",
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/AZUREFIREWALLS/{resourceName}",
    "operationName": "AzureFirewallNetworkRuleLog",
    "properties": {
        "msg": "TCP request from 111.35.136.173:12518 to 13.78.143.217:2323. Action: Deny"
    }
   }

   ```

<span data-ttu-id="11201-125">You have three options for storing your logs:</span><span class="sxs-lookup"><span data-stu-id="11201-125">You have three options for storing your logs:</span></span>

* <span data-ttu-id="11201-126">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span><span class="sxs-lookup"><span data-stu-id="11201-126">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="11201-127">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools to get alerts on your resources.</span><span class="sxs-lookup"><span data-stu-id="11201-127">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools to get alerts on your resources.</span></span>
* <span data-ttu-id="11201-128">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span><span class="sxs-lookup"><span data-stu-id="11201-128">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

## <a name="activity-logs"></a><span data-ttu-id="11201-129">Activity logs</span><span class="sxs-lookup"><span data-stu-id="11201-129">Activity logs</span></span>

   <span data-ttu-id="11201-130">Activity log entries are collected by default, and you can view them in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="11201-130">Activity log entries are collected by default, and you can view them in the Azure portal.</span></span>

   <span data-ttu-id="11201-131">You can use [Azure activity logs](../azure-resource-manager/resource-group-audit.md) (formerly known as operational logs and audit logs) to view all operations that are submitted to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="11201-131">You can use [Azure activity logs](../azure-resource-manager/resource-group-audit.md) (formerly known as operational logs and audit logs) to view all operations that are submitted to your Azure subscription.</span></span>

## <a name="enable-diagnostic-logging-through-the-azure-portal"></a><span data-ttu-id="11201-132">Enable diagnostic logging through the Azure portal</span><span class="sxs-lookup"><span data-stu-id="11201-132">Enable diagnostic logging through the Azure portal</span></span>

<span data-ttu-id="11201-133">It can take a few minutes for the data to appear in your logs after you complete this procedure to turn on diagnostic logging.</span><span class="sxs-lookup"><span data-stu-id="11201-133">It can take a few minutes for the data to appear in your logs after you complete this procedure to turn on diagnostic logging.</span></span> <span data-ttu-id="11201-134">If you don't see anything at first, check again in  a few more minutes.</span><span class="sxs-lookup"><span data-stu-id="11201-134">If you don't see anything at first, check again in  a few more minutes.</span></span>

1. <span data-ttu-id="11201-135">In the Azure portal, open your firewall resource group and click the firewall.</span><span class="sxs-lookup"><span data-stu-id="11201-135">In the Azure portal, open your firewall resource group and click the firewall.</span></span>
2. <span data-ttu-id="11201-136">Under **Monitoring**, click **Diagnostic logs**.</span><span class="sxs-lookup"><span data-stu-id="11201-136">Under **Monitoring**, click **Diagnostic logs**.</span></span>

   <span data-ttu-id="11201-137">For Azure Firewall, two service-specific logs are available:</span><span class="sxs-lookup"><span data-stu-id="11201-137">For Azure Firewall, two service-specific logs are available:</span></span>

   * <span data-ttu-id="11201-138">Application rule log</span><span class="sxs-lookup"><span data-stu-id="11201-138">Application rule log</span></span>
   * <span data-ttu-id="11201-139">Network rule log</span><span class="sxs-lookup"><span data-stu-id="11201-139">Network rule log</span></span>

3. <span data-ttu-id="11201-140">To start collecting data, click **Turn on diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="11201-140">To start collecting data, click **Turn on diagnostics**.</span></span>
4. <span data-ttu-id="11201-141">The **Diagnostics settings** page provides the settings for the diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="11201-141">The **Diagnostics settings** page provides the settings for the diagnostic logs.</span></span> 
5. <span data-ttu-id="11201-142">In this example, Log Analytics stores the logs, so type **Firewall log analytics** for the name.</span><span class="sxs-lookup"><span data-stu-id="11201-142">In this example, Log Analytics stores the logs, so type **Firewall log analytics** for the name.</span></span>
6. <span data-ttu-id="11201-143">Click **Send to Log Analytics** to configure your workspace.</span><span class="sxs-lookup"><span data-stu-id="11201-143">Click **Send to Log Analytics** to configure your workspace.</span></span> <span data-ttu-id="11201-144">You can also use event hubs and a storage account to save the diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="11201-144">You can also use event hubs and a storage account to save the diagnostic logs.</span></span>
7. <span data-ttu-id="11201-145">Under **Log Analytics**, click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="11201-145">Under **Log Analytics**, click **Configure**.</span></span>
8. <span data-ttu-id="11201-146">In the OMS Workspaces page, click **Create New Workspace**.</span><span class="sxs-lookup"><span data-stu-id="11201-146">In the OMS Workspaces page, click **Create New Workspace**.</span></span>
9. <span data-ttu-id="11201-147">On the **Log analytics workspace** page, type **firewall-oms** for the new **OMS Workspace** name.</span><span class="sxs-lookup"><span data-stu-id="11201-147">On the **Log analytics workspace** page, type **firewall-oms** for the new **OMS Workspace** name.</span></span>
10. <span data-ttu-id="11201-148">Select your subscription, use the existing firewall resource group (**Test-FW-RG**), select **East US** for the location, and select the **Free** pricing tier.</span><span class="sxs-lookup"><span data-stu-id="11201-148">Select your subscription, use the existing firewall resource group (**Test-FW-RG**), select **East US** for the location, and select the **Free** pricing tier.</span></span>
11. <span data-ttu-id="11201-149">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="11201-149">Click **OK**.</span></span>
   <span data-ttu-id="11201-150">![Starting the configuration process][1]</span><span class="sxs-lookup"><span data-stu-id="11201-150">![Starting the configuration process][1]</span></span>
12. <span data-ttu-id="11201-151">Under **Log**, click **AzureFirewallApplicationRule** and **AzureFirewallNetworkRule** to collect logs for application and network rules.</span><span class="sxs-lookup"><span data-stu-id="11201-151">Under **Log**, click **AzureFirewallApplicationRule** and **AzureFirewallNetworkRule** to collect logs for application and network rules.</span></span>
   <span data-ttu-id="11201-152">![Save diagnostics settings][2]</span><span class="sxs-lookup"><span data-stu-id="11201-152">![Save diagnostics settings][2]</span></span>
13. <span data-ttu-id="11201-153">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="11201-153">Click **Save**.</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="11201-154">Enable logging with PowerShell</span><span class="sxs-lookup"><span data-stu-id="11201-154">Enable logging with PowerShell</span></span>

<span data-ttu-id="11201-155">Activity logging is automatically enabled for every Resource Manager resource.</span><span class="sxs-lookup"><span data-stu-id="11201-155">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="11201-156">Diagnostic logging must be enabled to start collecting the data available through those logs.</span><span class="sxs-lookup"><span data-stu-id="11201-156">Diagnostic logging must be enabled to start collecting the data available through those logs.</span></span>

<span data-ttu-id="11201-157">To enable diagnostic logging, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="11201-157">To enable diagnostic logging, use the following steps:</span></span>

1. <span data-ttu-id="11201-158">Note your storage account's resource ID, where the log data is stored.</span><span class="sxs-lookup"><span data-stu-id="11201-158">Note your storage account's resource ID, where the log data is stored.</span></span> <span data-ttu-id="11201-159">This value is of the form: */subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>*.</span><span class="sxs-lookup"><span data-stu-id="11201-159">This value is of the form: */subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>*.</span></span>

   <span data-ttu-id="11201-160">You can use any storage account in your subscription.</span><span class="sxs-lookup"><span data-stu-id="11201-160">You can use any storage account in your subscription.</span></span> <span data-ttu-id="11201-161">You can use the Azure portal to find this information.</span><span class="sxs-lookup"><span data-stu-id="11201-161">You can use the Azure portal to find this information.</span></span> <span data-ttu-id="11201-162">The information is located in the resource **Property** page.</span><span class="sxs-lookup"><span data-stu-id="11201-162">The information is located in the resource **Property** page.</span></span>

2. <span data-ttu-id="11201-163">Note your Firewall's resource ID for which logging is enabled.</span><span class="sxs-lookup"><span data-stu-id="11201-163">Note your Firewall's resource ID for which logging is enabled.</span></span> <span data-ttu-id="11201-164">This value is of the form: */subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/azureFirewalls/\<Firewall name\>*.</span><span class="sxs-lookup"><span data-stu-id="11201-164">This value is of the form: */subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/azureFirewalls/\<Firewall name\>*.</span></span>

   <span data-ttu-id="11201-165">You can use the portal to find this information.</span><span class="sxs-lookup"><span data-stu-id="11201-165">You can use the portal to find this information.</span></span>

3. <span data-ttu-id="11201-166">Enable diagnostic logging by using the following PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="11201-166">Enable diagnostic logging by using the following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/azureFirewalls/<Firewall name> `
   -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> `
   -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="11201-167">Diagnostic logs do not require a separate storage account.</span><span class="sxs-lookup"><span data-stu-id="11201-167">Diagnostic logs do not require a separate storage account.</span></span> <span data-ttu-id="11201-168">The use of storage for access and performance logging incurs service charges.</span><span class="sxs-lookup"><span data-stu-id="11201-168">The use of storage for access and performance logging incurs service charges.</span></span>

## <a name="view-and-analyze-the-activity-log"></a><span data-ttu-id="11201-169">View and analyze the activity log</span><span class="sxs-lookup"><span data-stu-id="11201-169">View and analyze the activity log</span></span>

<span data-ttu-id="11201-170">You can view and analyze activity log data by using any of the following methods:</span><span class="sxs-lookup"><span data-stu-id="11201-170">You can view and analyze activity log data by using any of the following methods:</span></span>

* <span data-ttu-id="11201-171">**Azure tools**: Retrieve information from the activity log through Azure PowerShell, the Azure CLI, the Azure REST API, or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="11201-171">**Azure tools**: Retrieve information from the activity log through Azure PowerShell, the Azure CLI, the Azure REST API, or the Azure portal.</span></span> <span data-ttu-id="11201-172">Step-by-step instructions for each method are detailed in the [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span><span class="sxs-lookup"><span data-stu-id="11201-172">Step-by-step instructions for each method are detailed in the [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="11201-173">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span><span class="sxs-lookup"><span data-stu-id="11201-173">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="11201-174">By using the [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span><span class="sxs-lookup"><span data-stu-id="11201-174">By using the [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

## <a name="view-and-analyze-the-network-and-application-rule-logs"></a><span data-ttu-id="11201-175">View and analyze the network and application rule logs</span><span class="sxs-lookup"><span data-stu-id="11201-175">View and analyze the network and application rule logs</span></span>

<span data-ttu-id="11201-176">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) collects the counter and event log files.</span><span class="sxs-lookup"><span data-stu-id="11201-176">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) collects the counter and event log files.</span></span> <span data-ttu-id="11201-177">It includes visualizations and powerful search capabilities to analyze your logs.</span><span class="sxs-lookup"><span data-stu-id="11201-177">It includes visualizations and powerful search capabilities to analyze your logs.</span></span>

<span data-ttu-id="11201-178">You can also connect to your storage account and retrieve the JSON log entries for access and performance logs.</span><span class="sxs-lookup"><span data-stu-id="11201-178">You can also connect to your storage account and retrieve the JSON log entries for access and performance logs.</span></span> <span data-ttu-id="11201-179">After you download the JSON files, you can convert them to CSV and view them in Excel, Power BI, or any other data-visualization tool.</span><span class="sxs-lookup"><span data-stu-id="11201-179">After you download the JSON files, you can convert them to CSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="11201-180">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span><span class="sxs-lookup"><span data-stu-id="11201-180">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>


## <a name="next-steps"></a><span data-ttu-id="11201-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="11201-181">Next steps</span></span>

<span data-ttu-id="11201-182">Now that you've configured your firewall to collect logs, you can explore Log Anaytics to view your data.</span><span class="sxs-lookup"><span data-stu-id="11201-182">Now that you've configured your firewall to collect logs, you can explore Log Anaytics to view your data.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="11201-183">Networking monitoring solutions in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="11201-183">Networking monitoring solutions in Log Analytics</span></span>](../log-analytics/log-analytics-azure-networking-analytics.md)

[1]: ./media/tutorial-diagnostics/figure1.png
[2]: ./media/tutorial-diagnostics/figure2.png
