---
title: View Azure activity logs to monitor resources | Microsoft Docs
description: Use the activity logs to review user actions and errors. Shows Azure Portal PowerShell, Azure CLI, and REST.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fcdb3125-13ce-4c3b-9087-f514c5e41e73
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: tomfitz
ms.openlocfilehash: 20dcecc6fade37d74f7e5d6c361257ea8b96dd9e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553184"
---
# <a name="view-activity-logs-to-audit-actions-on-resources"></a><span data-ttu-id="166e2-104">View activity logs to audit actions on resources</span><span class="sxs-lookup"><span data-stu-id="166e2-104">View activity logs to audit actions on resources</span></span>
<span data-ttu-id="166e2-105">Through activity logs, you can determine:</span><span class="sxs-lookup"><span data-stu-id="166e2-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="166e2-106">what operations were taken on the resources in your subscription</span><span class="sxs-lookup"><span data-stu-id="166e2-106">what operations were taken on the resources in your subscription</span></span>
* <span data-ttu-id="166e2-107">who initiated the operation (although operations initiated by a backend service do not return a user as the caller)</span><span class="sxs-lookup"><span data-stu-id="166e2-107">who initiated the operation (although operations initiated by a backend service do not return a user as the caller)</span></span>
* <span data-ttu-id="166e2-108">when the operation occurred</span><span class="sxs-lookup"><span data-stu-id="166e2-108">when the operation occurred</span></span>
* <span data-ttu-id="166e2-109">the status of the operation</span><span class="sxs-lookup"><span data-stu-id="166e2-109">the status of the operation</span></span>
* <span data-ttu-id="166e2-110">the values of other properties that might help you research the operation</span><span class="sxs-lookup"><span data-stu-id="166e2-110">the values of other properties that might help you research the operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="166e2-111">You can retrieve information from the activity logs through the portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span><span class="sxs-lookup"><span data-stu-id="166e2-111">You can retrieve information from the activity logs through the portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="166e2-112">Portal</span><span class="sxs-lookup"><span data-stu-id="166e2-112">Portal</span></span>
1. <span data-ttu-id="166e2-113">To view the activity logs through the portal, select **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="166e2-113">To view the activity logs through the portal, select **Monitor**.</span></span>
   
    ![select activity logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="166e2-115">Or, to automatically filter the activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span><span class="sxs-lookup"><span data-stu-id="166e2-115">Or, to automatically filter the activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="166e2-116">Notice that the activity log is automatically filtered by the selected resource.</span><span class="sxs-lookup"><span data-stu-id="166e2-116">Notice that the activity log is automatically filtered by the selected resource.</span></span>
   
    ![filter by resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="166e2-118">In the **Activity Log** blade, you see a summary of recent operations.</span><span class="sxs-lookup"><span data-stu-id="166e2-118">In the **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![show actions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="166e2-120">To restrict the number of operations displayed, select different conditions.</span><span class="sxs-lookup"><span data-stu-id="166e2-120">To restrict the number of operations displayed, select different conditions.</span></span> <span data-ttu-id="166e2-121">For example, the following image shows the **Timespan** and **Event initiated by** fields changed to view the actions taken by a particular user or application for the past month.</span><span class="sxs-lookup"><span data-stu-id="166e2-121">For example, the following image shows the **Timespan** and **Event initiated by** fields changed to view the actions taken by a particular user or application for the past month.</span></span> <span data-ttu-id="166e2-122">Select **Apply** to view the results of your query.</span><span class="sxs-lookup"><span data-stu-id="166e2-122">Select **Apply** to view the results of your query.</span></span>
   
    ![set filter options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="166e2-124">If you need to run the query again later, select **Save** and give the query a name.</span><span class="sxs-lookup"><span data-stu-id="166e2-124">If you need to run the query again later, select **Save** and give the query a name.</span></span>
   
    ![save query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-audit/save-query.png)
5. <span data-ttu-id="166e2-126">To quickly run a query, you can select one of the built-in queries, such as failed deployments.</span><span class="sxs-lookup"><span data-stu-id="166e2-126">To quickly run a query, you can select one of the built-in queries, such as failed deployments.</span></span>

    ![select query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="166e2-128">The selected query automatically sets the required filter values.</span><span class="sxs-lookup"><span data-stu-id="166e2-128">The selected query automatically sets the required filter values.</span></span>

    ![view deployment errors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="166e2-130">Select one of the operations to see a summary of the event.</span><span class="sxs-lookup"><span data-stu-id="166e2-130">Select one of the operations to see a summary of the event.</span></span>

    ![view operation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="166e2-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="166e2-132">PowerShell</span></span>
1. <span data-ttu-id="166e2-133">To retrieve log entries, run the **Get-AzureRmLog** command.</span><span class="sxs-lookup"><span data-stu-id="166e2-133">To retrieve log entries, run the **Get-AzureRmLog** command.</span></span> <span data-ttu-id="166e2-134">You provide additional parameters to filter the list of entries.</span><span class="sxs-lookup"><span data-stu-id="166e2-134">You provide additional parameters to filter the list of entries.</span></span> <span data-ttu-id="166e2-135">If you do not specify a start and end time, entries for the last hour are returned.</span><span class="sxs-lookup"><span data-stu-id="166e2-135">If you do not specify a start and end time, entries for the last hour are returned.</span></span> <span data-ttu-id="166e2-136">For example, to retrieve the operations for a resource group during the past hour run:</span><span class="sxs-lookup"><span data-stu-id="166e2-136">For example, to retrieve the operations for a resource group during the past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="166e2-137">The following example shows how to use the activity log to research operations taken during a specified time.</span><span class="sxs-lookup"><span data-stu-id="166e2-137">The following example shows how to use the activity log to research operations taken during a specified time.</span></span> <span data-ttu-id="166e2-138">The start and end dates are specified in a date format.</span><span class="sxs-lookup"><span data-stu-id="166e2-138">The start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="166e2-139">Or, you can use date functions to specify the date range, such as the last 14 days.</span><span class="sxs-lookup"><span data-stu-id="166e2-139">Or, you can use date functions to specify the date range, such as the last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="166e2-140">Depending on the start time you specify, the previous commands can return a long list of operations for the resource group.</span><span class="sxs-lookup"><span data-stu-id="166e2-140">Depending on the start time you specify, the previous commands can return a long list of operations for the resource group.</span></span> <span data-ttu-id="166e2-141">You can filter the results for what you are looking for by providing search criteria.</span><span class="sxs-lookup"><span data-stu-id="166e2-141">You can filter the results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="166e2-142">For example, if you are trying to research how a web app was stopped, you could run the following command:</span><span class="sxs-lookup"><span data-stu-id="166e2-142">For example, if you are trying to research how a web app was stopped, you could run the following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="166e2-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="166e2-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

  ```powershell 
  Authorization     :
  Scope     : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Action    : Microsoft.Web/sites/stop/action
  Role      : Subscription Admin
  Condition :
  Caller            : someone@contoso.com
  CorrelationId     : 84beae59-92aa-4662-a6fc-b6fecc0ff8da
  EventSource       : Administrative
  EventTimestamp    : 8/28/2015 4:08:18 PM
  OperationName     : Microsoft.Web/sites/stop/action
  ResourceGroupName : ExampleGroup
  ResourceId        : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Status            : Succeeded
  SubscriptionId    : xxxxx
  SubStatus         : OK
  ```

3. <span data-ttu-id="166e2-144">You can look up the actions taken by a particular user, even for a resource group that no longer exists.</span><span class="sxs-lookup"><span data-stu-id="166e2-144">You can look up the actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="166e2-145">You can filter for failed operations.</span><span class="sxs-lookup"><span data-stu-id="166e2-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="166e2-146">You can focus on one error by looking at the status message for that entry.</span><span class="sxs-lookup"><span data-stu-id="166e2-146">You can focus on one error by looking at the status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="166e2-147">Which returns:</span><span class="sxs-lookup"><span data-stu-id="166e2-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="166e2-148">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="166e2-148">Azure CLI</span></span>
* <span data-ttu-id="166e2-149">To retrieve log entries, you run the **azure group log show** command.</span><span class="sxs-lookup"><span data-stu-id="166e2-149">To retrieve log entries, you run the **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="166e2-150">REST API</span><span class="sxs-lookup"><span data-stu-id="166e2-150">REST API</span></span>
<span data-ttu-id="166e2-151">The REST operations for working with the activity log are part of the [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="166e2-151">The REST operations for working with the activity log are part of the [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="166e2-152">To retrieve activity log events, see [List the management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span><span class="sxs-lookup"><span data-stu-id="166e2-152">To retrieve activity log events, see [List the management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="166e2-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="166e2-153">Next steps</span></span>
* <span data-ttu-id="166e2-154">Azure Activity logs can be used with Power BI to gain greater insights about the actions in your subscription.</span><span class="sxs-lookup"><span data-stu-id="166e2-154">Azure Activity logs can be used with Power BI to gain greater insights about the actions in your subscription.</span></span> <span data-ttu-id="166e2-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span><span class="sxs-lookup"><span data-stu-id="166e2-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="166e2-156">To learn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="166e2-156">To learn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="166e2-157">To learn about the commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="166e2-157">To learn about the commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="166e2-158">To learn how to prevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="166e2-158">To learn how to prevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>









