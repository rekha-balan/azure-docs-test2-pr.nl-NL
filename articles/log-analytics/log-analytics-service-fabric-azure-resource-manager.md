---
title: Assess Service Fabric applications with Log Analytics using the Azure portal | Microsoft Docs
description: You can use the Service Fabric solution in Log Analytics using the Azure portal to assess the risk and health of your Service Fabric applications, micro-services, nodes and clusters.
services: log-analytics
documentationcenter: ''
author: niniikhena
manager: jochan
editor: ''
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/21/2016
ms.author: nini
ms.openlocfilehash: b26d4485b09a8a118482415247e8933ed2c1c10d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552414"
---
# <a name="assess-service-fabric-applications-and-micro-services-with-the-azure-portal"></a><span data-ttu-id="545dc-103">Assess Service Fabric applications and micro-services with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="545dc-103">Assess Service Fabric applications and micro-services with the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [Resource Manager](log-analytics-service-fabric-azure-resource-manager.md)
> * [PowerShell](log-analytics-service-fabric.md)
>
>

<span data-ttu-id="545dc-106">This article describes how to use the Service Fabric solution in Log Analytics to help identify and troubleshoot issues across your Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="545dc-106">This article describes how to use the Service Fabric solution in Log Analytics to help identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="545dc-107">The Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span><span class="sxs-lookup"><span data-stu-id="545dc-107">The Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="545dc-108">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span><span class="sxs-lookup"><span data-stu-id="545dc-108">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="545dc-109">With the solution dashboard, you are able to view notable issues and relevant events in your Service Fabric environment.</span><span class="sxs-lookup"><span data-stu-id="545dc-109">With the solution dashboard, you are able to view notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="545dc-110">To get started with the solution, you will need to connect your Service Fabric cluster to a Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="545dc-110">To get started with the solution, you will need to connect your Service Fabric cluster to a Log Analytics workspace.</span></span> <span data-ttu-id="545dc-111">Here are three scenarios to consider:</span><span class="sxs-lookup"><span data-stu-id="545dc-111">Here are three scenarios to consider:</span></span>

1. <span data-ttu-id="545dc-112">If you have not deployed your Service Fabric cluster, use the steps in ***Deploy a Service Fabric Cluster connected to a Log Analytics workspace*** to deploy a new cluster and have it configured to report to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="545dc-112">If you have not deployed your Service Fabric cluster, use the steps in ***Deploy a Service Fabric Cluster connected to a Log Analytics workspace*** to deploy a new cluster and have it configured to report to Log Analytics.</span></span>
2. <span data-ttu-id="545dc-113">If you need to collect performance counters from your hosts to use other OMS solutions such as Security on your Service Fabric Cluster, follow the steps in ***Deploy a Service Fabric Cluster connected to an OMS workspace with VM Extension installed.***</span><span class="sxs-lookup"><span data-stu-id="545dc-113">If you need to collect performance counters from your hosts to use other OMS solutions such as Security on your Service Fabric Cluster, follow the steps in ***Deploy a Service Fabric Cluster connected to an OMS workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="545dc-114">If you have already deployed your Service Fabric cluster and want to connect it to Log Analytics, follow the steps in ***Adding an existing storage account to Log Analytics.***</span><span class="sxs-lookup"><span data-stu-id="545dc-114">If you have already deployed your Service Fabric cluster and want to connect it to Log Analytics, follow the steps in ***Adding an existing storage account to Log Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-to-a-log-analytics-workspace"></a><span data-ttu-id="545dc-115">Deploy a Service Fabric Cluster connected to a Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="545dc-115">Deploy a Service Fabric Cluster connected to a Log Analytics workspace.</span></span>
<span data-ttu-id="545dc-116">This template does the following:</span><span class="sxs-lookup"><span data-stu-id="545dc-116">This template does the following:</span></span>

1. <span data-ttu-id="545dc-117">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="545dc-117">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span></span> <span data-ttu-id="545dc-118">You have the option to create a new workspace while deploying the template, or input the name of an already existing Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="545dc-118">You have the option to create a new workspace while deploying the template, or input the name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="545dc-119">Adds the diagnostic storage account to the Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="545dc-119">Adds the diagnostic storage account to the Log Analytics workspace.</span></span>
3. <span data-ttu-id="545dc-120">Enables the Service Fabric solution in your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="545dc-120">Enables the Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="545dc-121">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="545dc-121">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="545dc-122">Once you select the deploy button above, you will arrive on the Azure portal with parameters for you to edit.</span><span class="sxs-lookup"><span data-stu-id="545dc-122">Once you select the deploy button above, you will arrive on the Azure portal with parameters for you to edit.</span></span> <span data-ttu-id="545dc-123">Be sure to create a new resource group if you input a new Log Analytics workspace name: ![Service Fabric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/2.png)</span><span class="sxs-lookup"><span data-stu-id="545dc-123">Be sure to create a new resource group if you input a new Log Analytics workspace name: ![Service Fabric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/2.png)</span></span>

![Service Fabric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/3.png)

<span data-ttu-id="545dc-125">Accept the legal terms and hit "Create" to start the deployment.</span><span class="sxs-lookup"><span data-stu-id="545dc-125">Accept the legal terms and hit "Create" to start the deployment.</span></span> <span data-ttu-id="545dc-126">Once the deployment is completed, you should see the new workspace and cluster created, and the WADServiceFabric\*Event, WADWindowsEventLogs and WADETWEvent tables added:</span><span class="sxs-lookup"><span data-stu-id="545dc-126">Once the deployment is completed, you should see the new workspace and cluster created, and the WADServiceFabric\*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![Service Fabric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-to-an-oms-workspace-with-vm-extension-installed"></a><span data-ttu-id="545dc-128">Deploy a Service Fabric Cluster connected to an OMS workspace with VM Extension installed.</span><span class="sxs-lookup"><span data-stu-id="545dc-128">Deploy a Service Fabric Cluster connected to an OMS workspace with VM Extension installed.</span></span>
<span data-ttu-id="545dc-129">This template does the following:</span><span class="sxs-lookup"><span data-stu-id="545dc-129">This template does the following:</span></span>

1. <span data-ttu-id="545dc-130">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="545dc-130">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span></span> <span data-ttu-id="545dc-131">You can create a new workspace or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="545dc-131">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="545dc-132">Adds the diagnostic storage accounts to the Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="545dc-132">Adds the diagnostic storage accounts to the Log Analytics workspace.</span></span>
3. <span data-ttu-id="545dc-133">Enables the Service Fabric solution in the Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="545dc-133">Enables the Service Fabric solution in the Log Analytics workspace.</span></span>
4. <span data-ttu-id="545dc-134">Installs the MMA agent extension in each VM scale set in your Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="545dc-134">Installs the MMA agent extension in each VM scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="545dc-135">With the MMA agent installed, you are able to view performance metrics about your nodes.</span><span class="sxs-lookup"><span data-stu-id="545dc-135">With the MMA agent installed, you are able to view performance metrics about your nodes.</span></span>

<span data-ttu-id="545dc-136">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="545dc-136">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="545dc-137">Following the same steps above, input the necessary parameters, and kick off a deployment.</span><span class="sxs-lookup"><span data-stu-id="545dc-137">Following the same steps above, input the necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="545dc-138">Once again you should see the new workspace, cluster and WAD tables all created:</span><span class="sxs-lookup"><span data-stu-id="545dc-138">Once again you should see the new workspace, cluster and WAD tables all created:</span></span>

![Service Fabric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="545dc-140">Viewing Performance Data</span><span class="sxs-lookup"><span data-stu-id="545dc-140">Viewing Performance Data</span></span>
<span data-ttu-id="545dc-141">To view Perf Data from your nodes:</span><span class="sxs-lookup"><span data-stu-id="545dc-141">To view Perf Data from your nodes:</span></span>
</br>

* <span data-ttu-id="545dc-142">Launch the Log Analytics workspace from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="545dc-142">Launch the Log Analytics workspace from the Azure portal.</span></span>

![Service Fabric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/6.png)

* <span data-ttu-id="545dc-144">Go to Settings on the left pane, and select Data >> Windows Performance Counters >> "Add the selected performance counters": ![Service Fabric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/7.png)</span><span class="sxs-lookup"><span data-stu-id="545dc-144">Go to Settings on the left pane, and select Data >> Windows Performance Counters >> "Add the selected performance counters": ![Service Fabric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/7.png)</span></span>
* <span data-ttu-id="545dc-145">In Log Search, use the following queries to delve into key metrics about your nodes:</span><span class="sxs-lookup"><span data-stu-id="545dc-145">In Log Search, use the following queries to delve into key metrics about your nodes:</span></span>
  </br>

    <span data-ttu-id="545dc-146">a.</span><span class="sxs-lookup"><span data-stu-id="545dc-146">a.</span></span> <span data-ttu-id="545dc-147">Compare the average CPU Utilization across all your nodes in the last one hour to see which nodes are having issues and at what time interval a node had a spike:</span><span class="sxs-lookup"><span data-stu-id="545dc-147">Compare the average CPU Utilization across all your nodes in the last one hour to see which nodes are having issues and at what time interval a node had a spike:</span></span>

    ``` Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR. ```

    ![Service Fabric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="545dc-149">b.</span><span class="sxs-lookup"><span data-stu-id="545dc-149">b.</span></span> <span data-ttu-id="545dc-150">View similar line charts for available memory on each node with this query:</span><span class="sxs-lookup"><span data-stu-id="545dc-150">View similar line charts for available memory on each node with this query:</span></span>

    ```Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.```

    <span data-ttu-id="545dc-151">To view a listing of all your nodes, showing the exact average value for Available MBytes for each node, use this query:</span><span class="sxs-lookup"><span data-stu-id="545dc-151">To view a listing of all your nodes, showing the exact average value for Available MBytes for each node, use this query:</span></span>

    ```Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer ```

    ![Service Fabric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/11.png)


    <span data-ttu-id="545dc-153">c.</span><span class="sxs-lookup"><span data-stu-id="545dc-153">c.</span></span> <span data-ttu-id="545dc-154">In the case that you want to drill down into a specific node by examining the hourly average, minimum, maximum and 75-percentile CPU usage, you're able to do this by using this query (replace Computer field):</span><span class="sxs-lookup"><span data-stu-id="545dc-154">In the case that you want to drill down into a specific node by examining the hourly average, minimum, maximum and 75-percentile CPU usage, you're able to do this by using this query (replace Computer field):</span></span>

    ```Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR```

    ![Service Fabric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/12.png)

    <span data-ttu-id="545dc-156">Read more information about performance metrics in Log Analytics [here.] (https://blogs.technet.microsoft.com/msoms/tag/metrics/)</span><span class="sxs-lookup"><span data-stu-id="545dc-156">Read more information about performance metrics in Log Analytics [here.] (https://blogs.technet.microsoft.com/msoms/tag/metrics/)</span></span>


## <a name="adding-an-existing-storage-account-to-log-analytics"></a><span data-ttu-id="545dc-157">Adding an existing storage account to Log Analytics</span><span class="sxs-lookup"><span data-stu-id="545dc-157">Adding an existing storage account to Log Analytics</span></span>
<span data-ttu-id="545dc-158">This template simply adds your existing storage accounts to a new or existing Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="545dc-158">This template simply adds your existing storage accounts to a new or existing Log Analytics workspace.</span></span>
</br>

<span data-ttu-id="545dc-159">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="545dc-159">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for the resource group containing the OMS workspace. Create a new one if otherwise.
> ![Service Fabric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/8.png)
>
>

<span data-ttu-id="545dc-163">After this template has been deployed, you will be able to see the storage account connected to your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="545dc-163">After this template has been deployed, you will be able to see the storage account connected to your Log Analytics workspace.</span></span> <span data-ttu-id="545dc-164">In this instance, I added one more storage account to the Exchange workspace I created above.</span><span class="sxs-lookup"><span data-stu-id="545dc-164">In this instance, I added one more storage account to the Exchange workspace I created above.</span></span>
<span data-ttu-id="545dc-165">![Service Fabric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="545dc-165">![Service Fabric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="545dc-166">View Service Fabric events</span><span class="sxs-lookup"><span data-stu-id="545dc-166">View Service Fabric events</span></span>
<span data-ttu-id="545dc-167">Once the deployments are completed and the Service Fabric solution has been enabled in your workspace, select the **Service Fabric** tile in the Log Analytics portal to launch the Service Fabric dashboard.</span><span class="sxs-lookup"><span data-stu-id="545dc-167">Once the deployments are completed and the Service Fabric solution has been enabled in your workspace, select the **Service Fabric** tile in the Log Analytics portal to launch the Service Fabric dashboard.</span></span> <span data-ttu-id="545dc-168">The dashboard includes the columns in the following table.</span><span class="sxs-lookup"><span data-stu-id="545dc-168">The dashboard includes the columns in the following table.</span></span> <span data-ttu-id="545dc-169">Each column lists the top ten events by count matching that column's criteria for the specified time range.</span><span class="sxs-lookup"><span data-stu-id="545dc-169">Each column lists the top ten events by count matching that column's criteria for the specified time range.</span></span> <span data-ttu-id="545dc-170">You can run a log search that provides the entire list by clicking **See all** at the right bottom of each column, or by clicking the column header.</span><span class="sxs-lookup"><span data-stu-id="545dc-170">You can run a log search that provides the entire list by clicking **See all** at the right bottom of each column, or by clicking the column header.</span></span>

| <span data-ttu-id="545dc-171">**Service Fabric event**</span><span class="sxs-lookup"><span data-stu-id="545dc-171">**Service Fabric event**</span></span> | <span data-ttu-id="545dc-172">**description**</span><span class="sxs-lookup"><span data-stu-id="545dc-172">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="545dc-173">Notable Issues</span><span class="sxs-lookup"><span data-stu-id="545dc-173">Notable Issues</span></span> |<span data-ttu-id="545dc-174">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span><span class="sxs-lookup"><span data-stu-id="545dc-174">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="545dc-175">Operational Events</span><span class="sxs-lookup"><span data-stu-id="545dc-175">Operational Events</span></span> |<span data-ttu-id="545dc-176">Notable operational events such as application upgrade and deployments.</span><span class="sxs-lookup"><span data-stu-id="545dc-176">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="545dc-177">Reliable Service Events</span><span class="sxs-lookup"><span data-stu-id="545dc-177">Reliable Service Events</span></span> |<span data-ttu-id="545dc-178">Notable reliable service events such a Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="545dc-178">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="545dc-179">Actor Events</span><span class="sxs-lookup"><span data-stu-id="545dc-179">Actor Events</span></span> |<span data-ttu-id="545dc-180">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span><span class="sxs-lookup"><span data-stu-id="545dc-180">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="545dc-181">Application Events</span><span class="sxs-lookup"><span data-stu-id="545dc-181">Application Events</span></span> |<span data-ttu-id="545dc-182">All custom ETW events generated by your applications.</span><span class="sxs-lookup"><span data-stu-id="545dc-182">All custom ETW events generated by your applications.</span></span> |

![Service Fabric dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/sf3.png)

![Service Fabric dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="545dc-185">The following table shows data collection methods and other details about how data is collected for Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="545dc-185">The following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="545dc-186">platform</span><span class="sxs-lookup"><span data-stu-id="545dc-186">platform</span></span> | <span data-ttu-id="545dc-187">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="545dc-187">Direct Agent</span></span> | <span data-ttu-id="545dc-188">SCOM agent</span><span class="sxs-lookup"><span data-stu-id="545dc-188">SCOM agent</span></span> | <span data-ttu-id="545dc-189">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="545dc-189">Azure Storage</span></span> | <span data-ttu-id="545dc-190">SCOM required?</span><span class="sxs-lookup"><span data-stu-id="545dc-190">SCOM required?</span></span> | <span data-ttu-id="545dc-191">SCOM agent data sent via management group</span><span class="sxs-lookup"><span data-stu-id="545dc-191">SCOM agent data sent via management group</span></span> | <span data-ttu-id="545dc-192">collection frequency</span><span class="sxs-lookup"><span data-stu-id="545dc-192">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="545dc-193">Windows</span><span class="sxs-lookup"><span data-stu-id="545dc-193">Windows</span></span> |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-malware/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-malware/oms-bullet-red.png) |![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-malware/oms-bullet-green.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-malware/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-malware/oms-bullet-red.png) |<span data-ttu-id="545dc-199">10 minutes</span><span class="sxs-lookup"><span data-stu-id="545dc-199">10 minutes</span></span> |

> [!NOTE]
> You can change the scope of these events in the Service Fabric solution by clicking **Data based on last 7 days** at the top of the dashboard. You can also show events generated within the last 7 days, 1 day, or six hours. Or, you can select **Custom** to specify a custom date range.
>
>

## <a name="next-steps"></a><span data-ttu-id="545dc-203">Next steps</span><span class="sxs-lookup"><span data-stu-id="545dc-203">Next steps</span></span>
* <span data-ttu-id="545dc-204">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) to view detailed Service Fabric event data.</span><span class="sxs-lookup"><span data-stu-id="545dc-204">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) to view detailed Service Fabric event data.</span></span>





















