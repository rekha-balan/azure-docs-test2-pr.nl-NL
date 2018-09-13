---
title: Monitor Azure Kubernetes Service (AKS) health (preview) | Microsoft Docs
description: This article describes how you can easily review the performance of your AKS container to quickly understand the utilization of your hosted Kubernetes environment.
services: log-analytics
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2018
ms.author: magoedte
ms.openlocfilehash: caf290477a4fd4f03bb248cc89f91027dbe68f3e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967176"
---
# <a name="monitor-azure-kubernetes-service-aks-container-health-preview"></a><span data-ttu-id="bb0fa-103">Monitor Azure Kubernetes Service (AKS) container health (preview)</span><span class="sxs-lookup"><span data-stu-id="bb0fa-103">Monitor Azure Kubernetes Service (AKS) container health (preview)</span></span>

<span data-ttu-id="bb0fa-104">This article describes how to set up and use Azure Monitor container health to monitor the performance of workloads that are deployed to Kubernetes environments and hosted on Azure Kubernetes Service (AKS).</span><span class="sxs-lookup"><span data-stu-id="bb0fa-104">This article describes how to set up and use Azure Monitor container health to monitor the performance of workloads that are deployed to Kubernetes environments and hosted on Azure Kubernetes Service (AKS).</span></span> <span data-ttu-id="bb0fa-105">Monitoring your Kubernetes cluster and containers is critical, especially when you're running a production cluster, at scale, with multiple applications.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-105">Monitoring your Kubernetes cluster and containers is critical, especially when you're running a production cluster, at scale, with multiple applications.</span></span>

<span data-ttu-id="bb0fa-106">Container health gives you performance monitoring ability by collecting memory and processor metrics from controllers, nodes, and containers that are available in Kubernetes through the Metrics API.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-106">Container health gives you performance monitoring ability by collecting memory and processor metrics from controllers, nodes, and containers that are available in Kubernetes through the Metrics API.</span></span> <span data-ttu-id="bb0fa-107">After you enable container health, these metrics are automatically collected for you through a containerized version of the Log Analytics agent for Linux and stored in your [Log Analytics](../log-analytics/log-analytics-overview.md) workspace.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-107">After you enable container health, these metrics are automatically collected for you through a containerized version of the Log Analytics agent for Linux and stored in your [Log Analytics](../log-analytics/log-analytics-overview.md) workspace.</span></span> <span data-ttu-id="bb0fa-108">The included pre-defined views display the residing container workloads and what affects the performance health of the Kubernetes cluster so that you can:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-108">The included pre-defined views display the residing container workloads and what affects the performance health of the Kubernetes cluster so that you can:</span></span>  

* <span data-ttu-id="bb0fa-109">Identify containers that are running on the node and their average processor and memory utilization.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-109">Identify containers that are running on the node and their average processor and memory utilization.</span></span> <span data-ttu-id="bb0fa-110">This knowledge can help you identify resource bottlenecks.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-110">This knowledge can help you identify resource bottlenecks.</span></span>
* <span data-ttu-id="bb0fa-111">Identify where the container resides in a controller or a pod.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-111">Identify where the container resides in a controller or a pod.</span></span> <span data-ttu-id="bb0fa-112">This knowledge can help you view the controller's or pod's overall performance.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-112">This knowledge can help you view the controller's or pod's overall performance.</span></span> 
* <span data-ttu-id="bb0fa-113">Review the resource utilization of workloads running on the host that are unrelated to the standard processes that support the pod.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-113">Review the resource utilization of workloads running on the host that are unrelated to the standard processes that support the pod.</span></span>
* <span data-ttu-id="bb0fa-114">Understand the behavior of the cluster under average and heaviest loads.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-114">Understand the behavior of the cluster under average and heaviest loads.</span></span> <span data-ttu-id="bb0fa-115">This knowledge can help you identify capacity needs and determine the maximum load that the cluster can sustain.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-115">This knowledge can help you identify capacity needs and determine the maximum load that the cluster can sustain.</span></span> 

<span data-ttu-id="bb0fa-116">If you are interested in monitoring and managing your Docker and Windows container hosts to view configuration, audit, and resource utilization, see the [Container Monitoring solution](../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="bb0fa-116">If you are interested in monitoring and managing your Docker and Windows container hosts to view configuration, audit, and resource utilization, see the [Container Monitoring solution](../log-analytics/log-analytics-containers.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb0fa-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bb0fa-117">Prerequisites</span></span> 
<span data-ttu-id="bb0fa-118">Before you start, make sure that you have the following:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-118">Before you start, make sure that you have the following:</span></span>

- <span data-ttu-id="bb0fa-119">A new or existing AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-119">A new or existing AKS cluster.</span></span>
- <span data-ttu-id="bb0fa-120">A containerized Log Analytics agent for Linux version microsoft/oms:ciprod04202018 or later.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-120">A containerized Log Analytics agent for Linux version microsoft/oms:ciprod04202018 or later.</span></span> <span data-ttu-id="bb0fa-121">The version number is represented by a date in the following format: *mmddyyyy*.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-121">The version number is represented by a date in the following format: *mmddyyyy*.</span></span> <span data-ttu-id="bb0fa-122">The agent is installed automatically during the onboarding of container health.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-122">The agent is installed automatically during the onboarding of container health.</span></span> 
- <span data-ttu-id="bb0fa-123">A Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-123">A Log Analytics workspace.</span></span> <span data-ttu-id="bb0fa-124">You can create it when you enable monitoring of your new AKS cluster or let the onboarding experience create a default workspace in the default resource group of the AKS cluster subscription.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-124">You can create it when you enable monitoring of your new AKS cluster or let the onboarding experience create a default workspace in the default resource group of the AKS cluster subscription.</span></span> <span data-ttu-id="bb0fa-125">If you chose to create it yourself, you can create it through [Azure Resource Manager](../log-analytics/log-analytics-template-workspace-configuration.md), through [PowerShell](https://docs.microsoft.com/azure/log-analytics/scripts/log-analytics-powershell-sample-create-workspace?toc=%2fpowershell%2fmodule%2ftoc.json), or in the [Azure portal](../log-analytics/log-analytics-quick-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="bb0fa-125">If you chose to create it yourself, you can create it through [Azure Resource Manager](../log-analytics/log-analytics-template-workspace-configuration.md), through [PowerShell](https://docs.microsoft.com/azure/log-analytics/scripts/log-analytics-powershell-sample-create-workspace?toc=%2fpowershell%2fmodule%2ftoc.json), or in the [Azure portal](../log-analytics/log-analytics-quick-create-workspace.md).</span></span>
- <span data-ttu-id="bb0fa-126">The Log Analytics contributor role, to enable container monitoring.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-126">The Log Analytics contributor role, to enable container monitoring.</span></span> <span data-ttu-id="bb0fa-127">For more information about how to control access to a Log Analytics workspace, see [Manage workspaces](../log-analytics/log-analytics-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="bb0fa-127">For more information about how to control access to a Log Analytics workspace, see [Manage workspaces](../log-analytics/log-analytics-manage-access.md).</span></span>

[!INCLUDE [log-analytics-agent-note](../../includes/log-analytics-agent-note.md)]

## <a name="components"></a><span data-ttu-id="bb0fa-128">Components</span><span class="sxs-lookup"><span data-stu-id="bb0fa-128">Components</span></span> 

<span data-ttu-id="bb0fa-129">Your ability to monitor performance relies on a containerized Log Analytics agent for Linux, which collects performance and event data from all nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-129">Your ability to monitor performance relies on a containerized Log Analytics agent for Linux, which collects performance and event data from all nodes in the cluster.</span></span> <span data-ttu-id="bb0fa-130">The agent is automatically deployed and registered with the specified Log Analytics workspace after you enable container monitoring.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-130">The agent is automatically deployed and registered with the specified Log Analytics workspace after you enable container monitoring.</span></span> 

>[!NOTE] 
><span data-ttu-id="bb0fa-131">If you have already deployed an AKS cluster, you enable monitoring by using either Azure CLI or a provided Azure Resource Manager template, as demonstrated later in this article.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-131">If you have already deployed an AKS cluster, you enable monitoring by using either Azure CLI or a provided Azure Resource Manager template, as demonstrated later in this article.</span></span> <span data-ttu-id="bb0fa-132">You cannot use `kubectl` to upgrade, delete, re-deploy, or deploy the agent.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-132">You cannot use `kubectl` to upgrade, delete, re-deploy, or deploy the agent.</span></span> 
>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="bb0fa-133">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bb0fa-133">Sign in to the Azure portal</span></span>
<span data-ttu-id="bb0fa-134">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bb0fa-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span> 

## <a name="enable-container-health-monitoring-for-a-new-cluster"></a><span data-ttu-id="bb0fa-135">Enable container health monitoring for a new cluster</span><span class="sxs-lookup"><span data-stu-id="bb0fa-135">Enable container health monitoring for a new cluster</span></span>
<span data-ttu-id="bb0fa-136">During deployment, you can enable monitoring of a new AKS cluster in the Azure portal or with Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-136">During deployment, you can enable monitoring of a new AKS cluster in the Azure portal or with Azure CLI.</span></span> <span data-ttu-id="bb0fa-137">Follow the steps in the quickstart article [Deploy an Azure Kubernetes Service (AKS) cluster](../aks/kubernetes-walkthrough-portal.md) if you want to enable from the portal.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-137">Follow the steps in the quickstart article [Deploy an Azure Kubernetes Service (AKS) cluster](../aks/kubernetes-walkthrough-portal.md) if you want to enable from the portal.</span></span> <span data-ttu-id="bb0fa-138">On the **Monitoring** page, for the **Enable Monitoring** option, select **Yes**, and then select an existing Log Analytics workspace or create a new one.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-138">On the **Monitoring** page, for the **Enable Monitoring** option, select **Yes**, and then select an existing Log Analytics workspace or create a new one.</span></span> 

<span data-ttu-id="bb0fa-139">To enable monitoring of a new AKS cluster created with Azure CLI, follow the step in the quickstart article under the section [Create AKS cluster](../aks/kubernetes-walkthrough.md#create-aks-cluster).</span><span class="sxs-lookup"><span data-stu-id="bb0fa-139">To enable monitoring of a new AKS cluster created with Azure CLI, follow the step in the quickstart article under the section [Create AKS cluster](../aks/kubernetes-walkthrough.md#create-aks-cluster).</span></span>  

>[!NOTE]
><span data-ttu-id="bb0fa-140">If you choose to use the Azure CLI, you first need to install and use the CLI locally.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-140">If you choose to use the Azure CLI, you first need to install and use the CLI locally.</span></span> <span data-ttu-id="bb0fa-141">You must be running the Azure CLI version 2.0.43 or later.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-141">You must be running the Azure CLI version 2.0.43 or later.</span></span> <span data-ttu-id="bb0fa-142">To identify your version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-142">To identify your version, run `az --version`.</span></span> <span data-ttu-id="bb0fa-143">If you need to install or upgrade the Azure CLI, see [Install the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bb0fa-143">If you need to install or upgrade the Azure CLI, see [Install the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 
>

<span data-ttu-id="bb0fa-144">After you've enabled monitoring and all configuration tasks are completed successfully, you can monitor the performance of your cluster in either of two ways:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-144">After you've enabled monitoring and all configuration tasks are completed successfully, you can monitor the performance of your cluster in either of two ways:</span></span>

* <span data-ttu-id="bb0fa-145">Directly in the AKS cluster by selecting **Health** in the left pane.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-145">Directly in the AKS cluster by selecting **Health** in the left pane.</span></span>
* <span data-ttu-id="bb0fa-146">By selecting the **Monitor container health** tile in the AKS cluster page for the selected cluster.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-146">By selecting the **Monitor container health** tile in the AKS cluster page for the selected cluster.</span></span> <span data-ttu-id="bb0fa-147">In Azure Monitor, in the left pane, select **Health**.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-147">In Azure Monitor, in the left pane, select **Health**.</span></span> 

  ![Options for selecting container health in AKS](./media/monitoring-container-health/container-performance-and-health-select-01.png)

<span data-ttu-id="bb0fa-149">After you've enabled monitoring, it might take about 15 minutes before you can view operational data for the cluster.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-149">After you've enabled monitoring, it might take about 15 minutes before you can view operational data for the cluster.</span></span> 

## <a name="enable-container-health-monitoring-for-existing-managed-clusters"></a><span data-ttu-id="bb0fa-150">Enable container health monitoring for existing managed clusters</span><span class="sxs-lookup"><span data-stu-id="bb0fa-150">Enable container health monitoring for existing managed clusters</span></span>
<span data-ttu-id="bb0fa-151">You can enable monitoring of an AKS cluster that's already deployed either using Azure CLI, from the portal, or with the provided Azure Resource Manager template by using the PowerShell cmdlet `New-AzureRmResourceGroupDeployment`.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-151">You can enable monitoring of an AKS cluster that's already deployed either using Azure CLI, from the portal, or with the provided Azure Resource Manager template by using the PowerShell cmdlet `New-AzureRmResourceGroupDeployment`.</span></span> 

### <a name="enable-monitoring-using-azure-cli"></a><span data-ttu-id="bb0fa-152">Enable monitoring using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bb0fa-152">Enable monitoring using Azure CLI</span></span>
<span data-ttu-id="bb0fa-153">The following step enables monitoring of your AKS cluster using Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-153">The following step enables monitoring of your AKS cluster using Azure CLI.</span></span> <span data-ttu-id="bb0fa-154">In this example, you are not required to per-create or specify an existing workspace.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-154">In this example, you are not required to per-create or specify an existing workspace.</span></span> <span data-ttu-id="bb0fa-155">This command simplifies the process for you by creating a default workspace in the default resource group of the AKS cluster subscription if one does not already exist in the region.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-155">This command simplifies the process for you by creating a default workspace in the default resource group of the AKS cluster subscription if one does not already exist in the region.</span></span>  <span data-ttu-id="bb0fa-156">The default workspace created resembles the format of *DefaultWorkspace-<GUID>-<Region>*.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-156">The default workspace created resembles the format of *DefaultWorkspace-<GUID>-<Region>*.</span></span>  

```azurecli
az aks enable-addons -a monitoring -n MyExistingManagedCluster -g MyExistingManagedClusterRG  
```

<span data-ttu-id="bb0fa-157">The output will resemble the following:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-157">The output will resemble the following:</span></span>

```azurecli
provisioningState       : Succeeded
```

### <a name="enable-monitoring-in-the-azure-portal"></a><span data-ttu-id="bb0fa-158">Enable monitoring in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bb0fa-158">Enable monitoring in the Azure portal</span></span>
<span data-ttu-id="bb0fa-159">To enable monitoring of your AKS container in the Azure portal, do the following:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-159">To enable monitoring of your AKS container in the Azure portal, do the following:</span></span>

1. <span data-ttu-id="bb0fa-160">In the Azure portal, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-160">In the Azure portal, select **All services**.</span></span> 
2. <span data-ttu-id="bb0fa-161">In the list of resources, begin typing **Containers**.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-161">In the list of resources, begin typing **Containers**.</span></span>  
    <span data-ttu-id="bb0fa-162">The list filters based on your input.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-162">The list filters based on your input.</span></span> 
3. <span data-ttu-id="bb0fa-163">Select **Kubernetes services**.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-163">Select **Kubernetes services**.</span></span>  

    ![The Kubernetes services link](./media/monitoring-container-health/azure-portal-01.png)

4. <span data-ttu-id="bb0fa-165">In the list of containers, select a container.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-165">In the list of containers, select a container.</span></span>
5. <span data-ttu-id="bb0fa-166">On the container overview page, select **Monitor container health**.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-166">On the container overview page, select **Monitor container health**.</span></span>  
6. <span data-ttu-id="bb0fa-167">On the **Onboarding to Container Health and Logs** page, if you have an existing Log Analytics workspace in the same subscription as the cluster, select it in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-167">On the **Onboarding to Container Health and Logs** page, if you have an existing Log Analytics workspace in the same subscription as the cluster, select it in the drop-down list.</span></span>  
    <span data-ttu-id="bb0fa-168">The list preselects the default workspace and location that the AKS container is deployed to in the subscription.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-168">The list preselects the default workspace and location that the AKS container is deployed to in the subscription.</span></span> 

    ![Enable AKS container health monitoring](./media/monitoring-container-health/container-health-enable-brownfield-02.png)

>[!NOTE]
><span data-ttu-id="bb0fa-170">If you want to create a new Log Analytics workspace for storing the monitoring data from the cluster, follow the instructions in [Create a Log Analytics workspace](../log-analytics/log-analytics-quick-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="bb0fa-170">If you want to create a new Log Analytics workspace for storing the monitoring data from the cluster, follow the instructions in [Create a Log Analytics workspace](../log-analytics/log-analytics-quick-create-workspace.md).</span></span> <span data-ttu-id="bb0fa-171">Be sure to create the workspace in the same subscription that the AKS container is deployed to.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-171">Be sure to create the workspace in the same subscription that the AKS container is deployed to.</span></span> 
 
<span data-ttu-id="bb0fa-172">After you've enabled monitoring, it might take about 15 minutes before you can view operational data for the cluster.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-172">After you've enabled monitoring, it might take about 15 minutes before you can view operational data for the cluster.</span></span> 

### <a name="enable-monitoring-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="bb0fa-173">Enable monitoring by using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="bb0fa-173">Enable monitoring by using an Azure Resource Manager template</span></span>
<span data-ttu-id="bb0fa-174">This method includes two JSON templates.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-174">This method includes two JSON templates.</span></span> <span data-ttu-id="bb0fa-175">One template specifies the configuration to enable monitoring, and the other contains parameter values that you configure to specify the following:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-175">One template specifies the configuration to enable monitoring, and the other contains parameter values that you configure to specify the following:</span></span>

* <span data-ttu-id="bb0fa-176">The AKS container resource ID.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-176">The AKS container resource ID.</span></span> 
* <span data-ttu-id="bb0fa-177">The resource group that the cluster is deployed in.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-177">The resource group that the cluster is deployed in.</span></span>
* <span data-ttu-id="bb0fa-178">The Log Analytics workspace and region to create the workspace in.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-178">The Log Analytics workspace and region to create the workspace in.</span></span> 

<span data-ttu-id="bb0fa-179">The Log Analytics workspace has to be created manually.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-179">The Log Analytics workspace has to be created manually.</span></span> <span data-ttu-id="bb0fa-180">To create the workspace, you can set it up through [Azure Resource Manager](../log-analytics/log-analytics-template-workspace-configuration.md), through [PowerShell](https://docs.microsoft.com/azure/log-analytics/scripts/log-analytics-powershell-sample-create-workspace?toc=%2fpowershell%2fmodule%2ftoc.json), or in the [Azure portal](../log-analytics/log-analytics-quick-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="bb0fa-180">To create the workspace, you can set it up through [Azure Resource Manager](../log-analytics/log-analytics-template-workspace-configuration.md), through [PowerShell](https://docs.microsoft.com/azure/log-analytics/scripts/log-analytics-powershell-sample-create-workspace?toc=%2fpowershell%2fmodule%2ftoc.json), or in the [Azure portal](../log-analytics/log-analytics-quick-create-workspace.md).</span></span>

<span data-ttu-id="bb0fa-181">If you are unfamiliar with the concept of deploying resources by using a template, see:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-181">If you are unfamiliar with the concept of deploying resources by using a template, see:</span></span>
* [<span data-ttu-id="bb0fa-182">Deploy resources with Resource Manager templates and Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb0fa-182">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="bb0fa-183">Deploy resources with Resource Manager templates and the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bb0fa-183">Deploy resources with Resource Manager templates and the Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)

<span data-ttu-id="bb0fa-184">If you choose to use the Azure CLI, you first need to install and use the CLI locally.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-184">If you choose to use the Azure CLI, you first need to install and use the CLI locally.</span></span> <span data-ttu-id="bb0fa-185">You must be running the Azure CLI version 2.0.27 or later.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-185">You must be running the Azure CLI version 2.0.27 or later.</span></span> <span data-ttu-id="bb0fa-186">To identify your version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-186">To identify your version, run `az --version`.</span></span> <span data-ttu-id="bb0fa-187">If you need to install or upgrade the Azure CLI, see [Install the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bb0fa-187">If you need to install or upgrade the Azure CLI, see [Install the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

#### <a name="create-and-execute-a-template"></a><span data-ttu-id="bb0fa-188">Create and execute a template</span><span class="sxs-lookup"><span data-stu-id="bb0fa-188">Create and execute a template</span></span>

1. <span data-ttu-id="bb0fa-189">Copy and paste the following JSON syntax into your file:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-189">Copy and paste the following JSON syntax into your file:</span></span>

    ```json
    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "aksResourceId": {
        "type": "string",
        "metadata": {
           "description": "AKS Cluster Resource ID"
           }
    },
    "aksResourceLocation": {
    "type": "string",
     "metadata": {
        "description": "Location of the AKS resource e.g. \"East US\""
       }
    },
    "workspaceResourceId": {
      "type": "string",
      "metadata": {
         "description": "Azure Monitor Log Analytics Resource ID"
       }
    },
    "workspaceRegion": {
    "type": "string",
    "metadata": {
       "description": "Azure Monitor Log Analytics workspace region"
      }
     }
    },
    "resources": [
      {
    "name": "[split(parameters('aksResourceId'),'/')[8]]",
    "type": "Microsoft.ContainerService/managedClusters",
    "location": "[parameters('aksResourceLocation')]",
    "apiVersion": "2018-03-31",
    "properties": {
      "mode": "Incremental",
      "id": "[parameters('aksResourceId')]",
      "addonProfiles": {
        "omsagent": {
          "enabled": true,
          "config": {
            "logAnalyticsWorkspaceResourceID": "[parameters('workspaceResourceId')]"
          }
         }
       }
      }
     },
    {
        "type": "Microsoft.Resources/deployments",
        "name": "[Concat('ContainerInsights', '(', split(parameters('workspaceResourceId'),'/')[8], ')')]",
        "apiVersion": "2017-05-10",
        "subscriptionId": "[split(parameters('workspaceResourceId'),'/')[2]]",
        "resourceGroup": "[split(parameters('workspaceResourceId'),'/')[4]]",
        "properties": {
            "mode": "Incremental",
            "template": {
                "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                "contentVersion": "1.0.0.0",
                "parameters": {},
                "variables": {},
                "resources": [
                    {
                        "apiVersion": "2015-11-01-preview",
                        "type": "Microsoft.OperationsManagement/solutions",
                        "location": "[parameters('workspaceRegion')]",
                        "name": "[Concat('ContainerInsights', '(', split(parameters('workspaceResourceId'),'/')[8], ')')]",
                        "properties": {
                            "workspaceResourceId": "[parameters('workspaceResourceId')]"
                        },
                        "plan": {
                            "name": "[Concat('ContainerInsights', '(', split(parameters('workspaceResourceId'),'/')[8], ')')]",
                            "product": "[Concat('OMSGallery/', 'ContainerInsights')]",
                            "promotionCode": "",
                            "publisher": "Microsoft"
                        }
                    }
                ]
            },
            "parameters": {}
        }
       }
     ]
    }
    ```

2. <span data-ttu-id="bb0fa-190">Save this file as **existingClusterOnboarding.json** to a local folder.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-190">Save this file as **existingClusterOnboarding.json** to a local folder.</span></span>
3. <span data-ttu-id="bb0fa-191">Paste the following JSON syntax into your file:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-191">Paste the following JSON syntax into your file:</span></span>

    ```json
    {
       "$schema": "https://schema.management.azure.com/  schemas/2015-01-01/deploymentParameters.json#",
       "contentVersion": "1.0.0.0",
       "parameters": {
         "aksResourceId": {
           "value": "/subscriptions/<SubscriptionId>/resourcegroups/<ResourceGroup>/providers/Microsoft.ContainerService/managedClusters/<ResourceName>"
       },
       "aksResourceLocation": {
         "value": "East US"
       },
       "workspaceResourceId": {
         "value": "/subscriptions/<SubscriptionId>/resourceGroups/<ResourceGroup>/providers/Microsoft.OperationalInsights/workspaces/<workspaceName>"
       },
       "workspaceRegion": {
         "value": "eastus"
       }
     }
    }
    ```

4. <span data-ttu-id="bb0fa-192">Edit the values for **aksResourceId** and **aksResourceLocation** by using the values on the **AKS Overview** page for the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-192">Edit the values for **aksResourceId** and **aksResourceLocation** by using the values on the **AKS Overview** page for the AKS cluster.</span></span> <span data-ttu-id="bb0fa-193">The value for **workspaceResourceId** is the full resource ID of your Log Analytics workspace, which includes the workspace name.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-193">The value for **workspaceResourceId** is the full resource ID of your Log Analytics workspace, which includes the workspace name.</span></span> <span data-ttu-id="bb0fa-194">Also specify the location of the workspace for **workspaceRegion**.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-194">Also specify the location of the workspace for **workspaceRegion**.</span></span> 
5. <span data-ttu-id="bb0fa-195">Save this file as **existingClusterParam.json** to a local folder.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-195">Save this file as **existingClusterParam.json** to a local folder.</span></span>
6. <span data-ttu-id="bb0fa-196">You are ready to deploy this template.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-196">You are ready to deploy this template.</span></span> 

    * <span data-ttu-id="bb0fa-197">Use the following PowerShell commands in the folder that contains the template:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-197">Use the following PowerShell commands in the folder that contains the template:</span></span>

        ```powershell
        New-AzureRmResourceGroupDeployment -Name OnboardCluster -ResourceGroupName ClusterResourceGroupName -TemplateFile .\existingClusterOnboarding.json -TemplateParameterFile .\existingClusterParam.json
        ```
        <span data-ttu-id="bb0fa-198">The configuration change can take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-198">The configuration change can take a few minutes to complete.</span></span> <span data-ttu-id="bb0fa-199">When it's completed, a message is displayed that's similar to the following and includes the result:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-199">When it's completed, a message is displayed that's similar to the following and includes the result:</span></span>

        ```powershell
        provisioningState       : Succeeded
        ```

    * <span data-ttu-id="bb0fa-200">To run the following command by using the Azure CLI on Linux:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-200">To run the following command by using the Azure CLI on Linux:</span></span>
    
        ```azurecli
        az login
        az account set --subscription "Subscription Name"
        az group deployment create --resource-group <ResourceGroupName> --template-file ./existingClusterOnboarding.json --parameters @./existingClusterParam.json
        ```

        <span data-ttu-id="bb0fa-201">The configuration change can take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-201">The configuration change can take a few minutes to complete.</span></span> <span data-ttu-id="bb0fa-202">When it's completed, a message is displayed that's similar to the following and includes the result:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-202">When it's completed, a message is displayed that's similar to the following and includes the result:</span></span>

        ```azurecli
        provisioningState       : Succeeded
        ```
<span data-ttu-id="bb0fa-203">After you've enabled monitoring, it might take about 15 minutes before you can view operational data for the cluster.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-203">After you've enabled monitoring, it might take about 15 minutes before you can view operational data for the cluster.</span></span> 

## <a name="verify-agent-and-solution-deployment"></a><span data-ttu-id="bb0fa-204">Verify agent and solution deployment</span><span class="sxs-lookup"><span data-stu-id="bb0fa-204">Verify agent and solution deployment</span></span>
<span data-ttu-id="bb0fa-205">With agent version *06072018* or later, you can verify that both the agent and the solution were deployed successfully.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-205">With agent version *06072018* or later, you can verify that both the agent and the solution were deployed successfully.</span></span> <span data-ttu-id="bb0fa-206">With earlier versions of the agent, you can verify only agent deployment.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-206">With earlier versions of the agent, you can verify only agent deployment.</span></span>

### <a name="agent-version-06072018-or-later"></a><span data-ttu-id="bb0fa-207">Agent version 06072018 or later</span><span class="sxs-lookup"><span data-stu-id="bb0fa-207">Agent version 06072018 or later</span></span>
<span data-ttu-id="bb0fa-208">Run the following command to verify that the agent is deployed successfully.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-208">Run the following command to verify that the agent is deployed successfully.</span></span> 

```
kubectl get ds omsagent --namespace=kube-system
```

<span data-ttu-id="bb0fa-209">The output should resemble the following, which indicates that it was deployed properly:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-209">The output should resemble the following, which indicates that it was deployed properly:</span></span>

```
User@aksuser:~$ kubectl get ds omsagent --namespace=kube-system 
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE SELECTOR                 AGE
omsagent   2         2         2         2            2           beta.kubernetes.io/os=linux   1d
```  

<span data-ttu-id="bb0fa-210">To verify deployment of the solution, run the following command:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-210">To verify deployment of the solution, run the following command:</span></span>

```
kubectl get deployment omsagent-rs -n=kube-system
```

<span data-ttu-id="bb0fa-211">The output should resemble the following, which indicates that it was deployed properly:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-211">The output should resemble the following, which indicates that it was deployed properly:</span></span>

```
User@aksuser:~$ kubectl get deployment omsagent-rs -n=kube-system 
NAME       DESIRED   CURRENT   UP-TO-DATE   AVAILABLE    AGE
omsagent   1         1         1            1            3h
```

### <a name="agent-version-earlier-than-06072018"></a><span data-ttu-id="bb0fa-212">Agent version earlier than 06072018</span><span class="sxs-lookup"><span data-stu-id="bb0fa-212">Agent version earlier than 06072018</span></span>

<span data-ttu-id="bb0fa-213">To verify that the Log Analytics agent version released before *06072018* is deployed properly, run the following command:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-213">To verify that the Log Analytics agent version released before *06072018* is deployed properly, run the following command:</span></span>  

```
kubectl get ds omsagent --namespace=kube-system
```

<span data-ttu-id="bb0fa-214">The output should resemble the following, which indicates that it was deployed properly:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-214">The output should resemble the following, which indicates that it was deployed properly:</span></span>  

```
User@aksuser:~$ kubectl get ds omsagent --namespace=kube-system 
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE SELECTOR                 AGE
omsagent   2         2         2         2            2           beta.kubernetes.io/os=linux   1d
```  

## <a name="view-configuration-with-cli"></a><span data-ttu-id="bb0fa-215">View configuration with CLI</span><span class="sxs-lookup"><span data-stu-id="bb0fa-215">View configuration with CLI</span></span>
<span data-ttu-id="bb0fa-216">Use the `aks show` command to get details such as is the solution enabled or not, what is the Log Analytics workspace resourceID, and summary details about the cluster.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-216">Use the `aks show` command to get details such as is the solution enabled or not, what is the Log Analytics workspace resourceID, and summary details about the cluster.</span></span>  

```azurecli
az aks show -g <resoourceGroupofAKSCluster> -n <nameofAksCluster>
```

<span data-ttu-id="bb0fa-217">After a few minutes, the command completes and returns JSON-formatted information about solution.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-217">After a few minutes, the command completes and returns JSON-formatted information about solution.</span></span>  <span data-ttu-id="bb0fa-218">The results of the command should show the monitoring add-on profile and resembles the following example output:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-218">The results of the command should show the monitoring add-on profile and resembles the following example output:</span></span>

```
"addonProfiles": {
    "omsagent": {
      "config": {
        "logAnalyticsWorkspaceResourceID": "/subscriptions/<WorkspaceSubscription>/resourceGroups/<DefaultWorkspaceRG>/providers/Microsoft.OperationalInsights/workspaces/<defaultWorkspaceName>"
      },
      "enabled": true
    }
  }
```

## <a name="view-performance-utilization"></a><span data-ttu-id="bb0fa-219">View performance utilization</span><span class="sxs-lookup"><span data-stu-id="bb0fa-219">View performance utilization</span></span>
<span data-ttu-id="bb0fa-220">When you open container health, the page immediately presents the performance utilization of your entire cluster.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-220">When you open container health, the page immediately presents the performance utilization of your entire cluster.</span></span> <span data-ttu-id="bb0fa-221">Viewing information about your AKS cluster is organized into four perspectives:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-221">Viewing information about your AKS cluster is organized into four perspectives:</span></span>

- <span data-ttu-id="bb0fa-222">Cluster</span><span class="sxs-lookup"><span data-stu-id="bb0fa-222">Cluster</span></span>
- <span data-ttu-id="bb0fa-223">Nodes</span><span class="sxs-lookup"><span data-stu-id="bb0fa-223">Nodes</span></span> 
- <span data-ttu-id="bb0fa-224">Controllers</span><span class="sxs-lookup"><span data-stu-id="bb0fa-224">Controllers</span></span>  
- <span data-ttu-id="bb0fa-225">Containers</span><span class="sxs-lookup"><span data-stu-id="bb0fa-225">Containers</span></span>

<span data-ttu-id="bb0fa-226">On the **Cluster** tab, the four line performance charts display key performance metrics of your cluster.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-226">On the **Cluster** tab, the four line performance charts display key performance metrics of your cluster.</span></span> 

![Example performance charts on the Cluster tab](./media/monitoring-container-health/container-health-cluster-perfview.png)

<span data-ttu-id="bb0fa-228">The performance chart displays four performance metrics:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-228">The performance chart displays four performance metrics:</span></span>

- <span data-ttu-id="bb0fa-229">**Node CPU Utilization&nbsp;%**: An aggregated perspective of CPU utilization for the entire cluster.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-229">**Node CPU Utilization&nbsp;%**: An aggregated perspective of CPU utilization for the entire cluster.</span></span> <span data-ttu-id="bb0fa-230">You can filter the results for the time range by selecting **Avg**, **Min**, **Max**, **50th**, **90th**, and **95th** in the percentiles selector above the chart, either individually or combined.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-230">You can filter the results for the time range by selecting **Avg**, **Min**, **Max**, **50th**, **90th**, and **95th** in the percentiles selector above the chart, either individually or combined.</span></span> 
- <span data-ttu-id="bb0fa-231">**Node memory utilization&nbsp;%**: An aggregated perspective of memory utilization for the entire cluster.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-231">**Node memory utilization&nbsp;%**: An aggregated perspective of memory utilization for the entire cluster.</span></span> <span data-ttu-id="bb0fa-232">You can filter the results for the time range by selecting **Avg**, **Min**, **Max**, **50th**, **90th**, and **95th** in the percentiles selector above the chart, either individually or combined.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-232">You can filter the results for the time range by selecting **Avg**, **Min**, **Max**, **50th**, **90th**, and **95th** in the percentiles selector above the chart, either individually or combined.</span></span> 
- <span data-ttu-id="bb0fa-233">**Node count**: A node count and status from Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-233">**Node count**: A node count and status from Kubernetes.</span></span> <span data-ttu-id="bb0fa-234">Statuses of the cluster nodes represented are *All*, *Ready*, and *Not Ready* and can be filtered individually or combined in the selector above the chart.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-234">Statuses of the cluster nodes represented are *All*, *Ready*, and *Not Ready* and can be filtered individually or combined in the selector above the chart.</span></span> 
- <span data-ttu-id="bb0fa-235">**Activity pod count**: A pod count and status from Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-235">**Activity pod count**: A pod count and status from Kubernetes.</span></span> <span data-ttu-id="bb0fa-236">Statuses of the pods represented are *All*, *Pending*, *Running*, and *Unknown* and can be filtered individually or combined in the selector above the chart.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-236">Statuses of the pods represented are *All*, *Pending*, *Running*, and *Unknown* and can be filtered individually or combined in the selector above the chart.</span></span> 

<span data-ttu-id="bb0fa-237">When you switch to **Nodes**, **Controllers**, and **Containers** tab, automatically displayed on the right-side of the page is the property pane.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-237">When you switch to **Nodes**, **Controllers**, and **Containers** tab, automatically displayed on the right-side of the page is the property pane.</span></span>  <span data-ttu-id="bb0fa-238">It shows the properties of the item selected, including labels you define to organize Kubernetes objects.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-238">It shows the properties of the item selected, including labels you define to organize Kubernetes objects.</span></span>  <span data-ttu-id="bb0fa-239">Click on the **>>** link in the pane to view\hide the pane.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-239">Click on the **>>** link in the pane to view\hide the pane.</span></span>  

![Example Kubernetes perspectives properties pane](./media/monitoring-container-health/perspectives-preview-pane-01.png)

<span data-ttu-id="bb0fa-241">As you expand the objects in the hierarchy, the properties pane updates based on the object selected.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-241">As you expand the objects in the hierarchy, the properties pane updates based on the object selected.</span></span> <span data-ttu-id="bb0fa-242">From the pane you can also view Kubernetes events with pre-defined log searches by clicking on the **View Kubernetes event logs** link at the top of the pane.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-242">From the pane you can also view Kubernetes events with pre-defined log searches by clicking on the **View Kubernetes event logs** link at the top of the pane.</span></span> <span data-ttu-id="bb0fa-243">For additional information about viewing Kubernetes log data, see [Search logs to analyze data](#search-logs-to-analyze-data).</span><span class="sxs-lookup"><span data-stu-id="bb0fa-243">For additional information about viewing Kubernetes log data, see [Search logs to analyze data](#search-logs-to-analyze-data).</span></span>

<span data-ttu-id="bb0fa-244">Switch to the **Nodes** tab and the row hierarchy follows the Kubernetes object model, starting with a node in your cluster.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-244">Switch to the **Nodes** tab and the row hierarchy follows the Kubernetes object model, starting with a node in your cluster.</span></span> <span data-ttu-id="bb0fa-245">Expand the node and you can view one or more pods running on the node.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-245">Expand the node and you can view one or more pods running on the node.</span></span> <span data-ttu-id="bb0fa-246">If more than one container is grouped to a pod, they are displayed as the last row in the hierarchy.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-246">If more than one container is grouped to a pod, they are displayed as the last row in the hierarchy.</span></span> <span data-ttu-id="bb0fa-247">You can also view how many non-pod related workloads are running on the host if the host has processor or memory pressure.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-247">You can also view how many non-pod related workloads are running on the host if the host has processor or memory pressure.</span></span>

![Example Kubernetes Node hierarchy in the performance view](./media/monitoring-container-health/container-health-nodes-view.png)

<span data-ttu-id="bb0fa-249">You can select controllers or containers at the top of the page and review the status and resource utilization for those objects.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-249">You can select controllers or containers at the top of the page and review the status and resource utilization for those objects.</span></span> <span data-ttu-id="bb0fa-250">Use the drop-down boxes at the top to filter by namespace, service, and node.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-250">Use the drop-down boxes at the top to filter by namespace, service, and node.</span></span> <span data-ttu-id="bb0fa-251">If instead you want to review memory utilization, in the **Metric** drop-down list, select **Memory RSS** or **Memory working set**.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-251">If instead you want to review memory utilization, in the **Metric** drop-down list, select **Memory RSS** or **Memory working set**.</span></span> <span data-ttu-id="bb0fa-252">**Memory RSS** is supported only for Kubernetes version 1.8 and later.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-252">**Memory RSS** is supported only for Kubernetes version 1.8 and later.</span></span> <span data-ttu-id="bb0fa-253">Otherwise, you view values for **Min&nbsp;%** as *NaN&nbsp;%*, which is a numeric data type value that represents an undefined or unrepresentable value.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-253">Otherwise, you view values for **Min&nbsp;%** as *NaN&nbsp;%*, which is a numeric data type value that represents an undefined or unrepresentable value.</span></span> 

![Container nodes performance view](./media/monitoring-container-health/container-health-node-metric-dropdown.png)

<span data-ttu-id="bb0fa-255">By default, Performance data is based on the last six hours, but you can change the window by using the **Time Range** drop-down list at the upper right.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-255">By default, Performance data is based on the last six hours, but you can change the window by using the **Time Range** drop-down list at the upper right.</span></span> <span data-ttu-id="bb0fa-256">At this time, the page does not auto-refresh, so you need to manually refresh it.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-256">At this time, the page does not auto-refresh, so you need to manually refresh it.</span></span> <span data-ttu-id="bb0fa-257">You can also filter the results within the time range by selecting **Avg**, **Min**, **Max**, **50th**, **90th**, and **95th** in the percentile selector.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-257">You can also filter the results within the time range by selecting **Avg**, **Min**, **Max**, **50th**, **90th**, and **95th** in the percentile selector.</span></span> 

![Percentile selection for data filtering](./media/monitoring-container-health/container-health-metric-percentile-filter.png)

<span data-ttu-id="bb0fa-259">In the following example, note for node *aks-nodepool-3977305*, the value for **Containers** is 5, which is a roll-up of the total number of containers deployed.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-259">In the following example, note for node *aks-nodepool-3977305*, the value for **Containers** is 5, which is a roll-up of the total number of containers deployed.</span></span>

![Roll-up of containers per node example](./media/monitoring-container-health/container-health-nodes-containerstotal.png)

<span data-ttu-id="bb0fa-261">It can help you quickly identify whether you have a proper balance of containers between nodes in your cluster.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-261">It can help you quickly identify whether you have a proper balance of containers between nodes in your cluster.</span></span> 

<span data-ttu-id="bb0fa-262">The information that's presented when you view Nodes is described in the following table:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-262">The information that's presented when you view Nodes is described in the following table:</span></span>

| <span data-ttu-id="bb0fa-263">Column</span><span class="sxs-lookup"><span data-stu-id="bb0fa-263">Column</span></span> | <span data-ttu-id="bb0fa-264">Description</span><span class="sxs-lookup"><span data-stu-id="bb0fa-264">Description</span></span> | 
|--------|-------------|
| <span data-ttu-id="bb0fa-265">Name</span><span class="sxs-lookup"><span data-stu-id="bb0fa-265">Name</span></span> | <span data-ttu-id="bb0fa-266">The name of the host.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-266">The name of the host.</span></span> |
| <span data-ttu-id="bb0fa-267">Status</span><span class="sxs-lookup"><span data-stu-id="bb0fa-267">Status</span></span> | <span data-ttu-id="bb0fa-268">Kubernetes view of the node status.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-268">Kubernetes view of the node status.</span></span> |
| <span data-ttu-id="bb0fa-269">Avg&nbsp;%, Min&nbsp;%, Max&nbsp;%, 50th&nbsp;%, 90th&nbsp;%</span><span class="sxs-lookup"><span data-stu-id="bb0fa-269">Avg&nbsp;%, Min&nbsp;%, Max&nbsp;%, 50th&nbsp;%, 90th&nbsp;%</span></span> | <span data-ttu-id="bb0fa-270">Average node percentage based on percentile during the selected duration.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-270">Average node percentage based on percentile during the selected duration.</span></span> |
| <span data-ttu-id="bb0fa-271">Avg, Min, Max, 50th, 90th</span><span class="sxs-lookup"><span data-stu-id="bb0fa-271">Avg, Min, Max, 50th, 90th</span></span> | <span data-ttu-id="bb0fa-272">Average nodes actual value based on percentile during that time duration selected.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-272">Average nodes actual value based on percentile during that time duration selected.</span></span> <span data-ttu-id="bb0fa-273">The average value is measured from the CPU/Memory limit set for a node; for pods and containers it is the avg value reported by the host.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-273">The average value is measured from the CPU/Memory limit set for a node; for pods and containers it is the avg value reported by the host.</span></span> |
| <span data-ttu-id="bb0fa-274">Containers</span><span class="sxs-lookup"><span data-stu-id="bb0fa-274">Containers</span></span> | <span data-ttu-id="bb0fa-275">Number of containers.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-275">Number of containers.</span></span> |
| <span data-ttu-id="bb0fa-276">Uptime</span><span class="sxs-lookup"><span data-stu-id="bb0fa-276">Uptime</span></span> | <span data-ttu-id="bb0fa-277">Represents the time since a node started or was rebooted.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-277">Represents the time since a node started or was rebooted.</span></span> |
| <span data-ttu-id="bb0fa-278">Controllers</span><span class="sxs-lookup"><span data-stu-id="bb0fa-278">Controllers</span></span> | <span data-ttu-id="bb0fa-279">Only for containers and pods.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-279">Only for containers and pods.</span></span> <span data-ttu-id="bb0fa-280">It shows which controller it is residing in.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-280">It shows which controller it is residing in.</span></span> <span data-ttu-id="bb0fa-281">Not all pods are in a controller, so some might display **N/A**.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-281">Not all pods are in a controller, so some might display **N/A**.</span></span> | 
| <span data-ttu-id="bb0fa-282">Trend Avg&nbsp;%, Min&nbsp;%, Max&nbsp;%, 50th&nbsp;%, 90th&nbsp;%</span><span class="sxs-lookup"><span data-stu-id="bb0fa-282">Trend Avg&nbsp;%, Min&nbsp;%, Max&nbsp;%, 50th&nbsp;%, 90th&nbsp;%</span></span> | <span data-ttu-id="bb0fa-283">Bar graph trend presenting the percentile metric percentage of the controller.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-283">Bar graph trend presenting the percentile metric percentage of the controller.</span></span> |


<span data-ttu-id="bb0fa-284">In the selector, select **Controllers**.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-284">In the selector, select **Controllers**.</span></span>

![Select controllers view](./media/monitoring-container-health/container-health-controllers-tab.png)

<span data-ttu-id="bb0fa-286">Here you can view the performance health of your controllers.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-286">Here you can view the performance health of your controllers.</span></span>

![<Name> controllers performance view](./media/monitoring-container-health/container-health-controllers-view.png)

<span data-ttu-id="bb0fa-288">The row hierarchy starts with a controller and expands the controller.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-288">The row hierarchy starts with a controller and expands the controller.</span></span> <span data-ttu-id="bb0fa-289">You view one or more containers.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-289">You view one or more containers.</span></span> <span data-ttu-id="bb0fa-290">Expand a pod, and the last row displays the container grouped to the pod.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-290">Expand a pod, and the last row displays the container grouped to the pod.</span></span> 

<span data-ttu-id="bb0fa-291">The information that's displayed when you view controllers is described in the following table:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-291">The information that's displayed when you view controllers is described in the following table:</span></span>

| <span data-ttu-id="bb0fa-292">Column</span><span class="sxs-lookup"><span data-stu-id="bb0fa-292">Column</span></span> | <span data-ttu-id="bb0fa-293">Description</span><span class="sxs-lookup"><span data-stu-id="bb0fa-293">Description</span></span> | 
|--------|-------------|
| <span data-ttu-id="bb0fa-294">Name</span><span class="sxs-lookup"><span data-stu-id="bb0fa-294">Name</span></span> | <span data-ttu-id="bb0fa-295">The name of the controller.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-295">The name of the controller.</span></span>|
| <span data-ttu-id="bb0fa-296">Status</span><span class="sxs-lookup"><span data-stu-id="bb0fa-296">Status</span></span> | <span data-ttu-id="bb0fa-297">The roll-up status of the containers when it has completed running with status, such as *OK*, *Terminated*, *Failed* *Stopped*, or *Paused*.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-297">The roll-up status of the containers when it has completed running with status, such as *OK*, *Terminated*, *Failed* *Stopped*, or *Paused*.</span></span> <span data-ttu-id="bb0fa-298">If the container is running, but the status was either not properly displayed or was not picked up by the agent and has not responded more than 30 minutes, the status is *Unknown*.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-298">If the container is running, but the status was either not properly displayed or was not picked up by the agent and has not responded more than 30 minutes, the status is *Unknown*.</span></span> <span data-ttu-id="bb0fa-299">Additional details of the status icon are provided in the table below.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-299">Additional details of the status icon are provided in the table below.</span></span>|
| <span data-ttu-id="bb0fa-300">Avg&nbsp;%, Min&nbsp;%, Max&nbsp;%, 50th&nbsp;%, 90th&nbsp;%</span><span class="sxs-lookup"><span data-stu-id="bb0fa-300">Avg&nbsp;%, Min&nbsp;%, Max&nbsp;%, 50th&nbsp;%, 90th&nbsp;%</span></span> | <span data-ttu-id="bb0fa-301">Roll-up average of the average percentage of each entity for the selected metric and percentile.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-301">Roll-up average of the average percentage of each entity for the selected metric and percentile.</span></span> |
| <span data-ttu-id="bb0fa-302">Avg, Min, Max, 50th, 90th</span><span class="sxs-lookup"><span data-stu-id="bb0fa-302">Avg, Min, Max, 50th, 90th</span></span>  | <span data-ttu-id="bb0fa-303">Roll-up of the average CPU millicore or memory performance of the container for the selected percentile.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-303">Roll-up of the average CPU millicore or memory performance of the container for the selected percentile.</span></span> <span data-ttu-id="bb0fa-304">The average value is measured from the CPU/Memory limit set for a pod.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-304">The average value is measured from the CPU/Memory limit set for a pod.</span></span> |
| <span data-ttu-id="bb0fa-305">Containers</span><span class="sxs-lookup"><span data-stu-id="bb0fa-305">Containers</span></span> | <span data-ttu-id="bb0fa-306">Total number of containers for the controller or pod.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-306">Total number of containers for the controller or pod.</span></span> |
| <span data-ttu-id="bb0fa-307">Restarts</span><span class="sxs-lookup"><span data-stu-id="bb0fa-307">Restarts</span></span> | <span data-ttu-id="bb0fa-308">Roll-up of the restart count from containers.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-308">Roll-up of the restart count from containers.</span></span> |
| <span data-ttu-id="bb0fa-309">Uptime</span><span class="sxs-lookup"><span data-stu-id="bb0fa-309">Uptime</span></span> | <span data-ttu-id="bb0fa-310">Represents the time since a container started.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-310">Represents the time since a container started.</span></span> |
| <span data-ttu-id="bb0fa-311">Node</span><span class="sxs-lookup"><span data-stu-id="bb0fa-311">Node</span></span> | <span data-ttu-id="bb0fa-312">Only for containers and pods.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-312">Only for containers and pods.</span></span> <span data-ttu-id="bb0fa-313">It shows which controller it is residing.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-313">It shows which controller it is residing.</span></span> | 
| <span data-ttu-id="bb0fa-314">Trend Avg&nbsp;%, Min&nbsp;%, Max&nbsp;%, 50th&nbsp;%, 90th&nbsp;%</span><span class="sxs-lookup"><span data-stu-id="bb0fa-314">Trend Avg&nbsp;%, Min&nbsp;%, Max&nbsp;%, 50th&nbsp;%, 90th&nbsp;%</span></span>| <span data-ttu-id="bb0fa-315">Bar graph trend representing percentile metric of the controller.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-315">Bar graph trend representing percentile metric of the controller.</span></span> |

<span data-ttu-id="bb0fa-316">The icons in the status field indicate the online status of the containers:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-316">The icons in the status field indicate the online status of the containers:</span></span>
 
| <span data-ttu-id="bb0fa-317">Icon</span><span class="sxs-lookup"><span data-stu-id="bb0fa-317">Icon</span></span> | <span data-ttu-id="bb0fa-318">Status</span><span class="sxs-lookup"><span data-stu-id="bb0fa-318">Status</span></span> | 
|--------|-------------|
| ![Ready running status icon](./media/monitoring-container-health/container-health-ready-icon.png) | <span data-ttu-id="bb0fa-320">Running (Ready)</span><span class="sxs-lookup"><span data-stu-id="bb0fa-320">Running (Ready)</span></span>|
| ![Waiting or paused status icon](./media/monitoring-container-health/container-health-waiting-icon.png) | <span data-ttu-id="bb0fa-322">Waiting or Paused</span><span class="sxs-lookup"><span data-stu-id="bb0fa-322">Waiting or Paused</span></span>|
| ![Last reported running status icon](./media/monitoring-container-health/container-health-grey-icon.png) | <span data-ttu-id="bb0fa-324">Last reported running but hasn't responded more than 30 minutes</span><span class="sxs-lookup"><span data-stu-id="bb0fa-324">Last reported running but hasn't responded more than 30 minutes</span></span>|
| ![Successful status icon](./media/monitoring-container-health/container-health-green-icon.png) | <span data-ttu-id="bb0fa-326">Successfully stopped or failed to stop</span><span class="sxs-lookup"><span data-stu-id="bb0fa-326">Successfully stopped or failed to stop</span></span>|

<span data-ttu-id="bb0fa-327">The status icon displays a count based on what the pod provides.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-327">The status icon displays a count based on what the pod provides.</span></span> <span data-ttu-id="bb0fa-328">It shows the worst two states, and when you hover over the status, it displays a roll-up status from all pods in the container.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-328">It shows the worst two states, and when you hover over the status, it displays a roll-up status from all pods in the container.</span></span> <span data-ttu-id="bb0fa-329">If there isn't a ready state, the status value displays **(0)**.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-329">If there isn't a ready state, the status value displays **(0)**.</span></span> 

<span data-ttu-id="bb0fa-330">In the selector, select **Containers**.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-330">In the selector, select **Containers**.</span></span>

![Select containers view](./media/monitoring-container-health/container-health-containers-tab.png)

<span data-ttu-id="bb0fa-332">Here you can view the performance health of your containers.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-332">Here you can view the performance health of your containers.</span></span>

![<Name> controllers performance view](./media/monitoring-container-health/container-health-containers-view.png)

<span data-ttu-id="bb0fa-334">The information that's displayed when you view containers is described in the following table:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-334">The information that's displayed when you view containers is described in the following table:</span></span>

| <span data-ttu-id="bb0fa-335">Column</span><span class="sxs-lookup"><span data-stu-id="bb0fa-335">Column</span></span> | <span data-ttu-id="bb0fa-336">Description</span><span class="sxs-lookup"><span data-stu-id="bb0fa-336">Description</span></span> | 
|--------|-------------|
| <span data-ttu-id="bb0fa-337">Name</span><span class="sxs-lookup"><span data-stu-id="bb0fa-337">Name</span></span> | <span data-ttu-id="bb0fa-338">The name of the controller.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-338">The name of the controller.</span></span>|
| <span data-ttu-id="bb0fa-339">Status</span><span class="sxs-lookup"><span data-stu-id="bb0fa-339">Status</span></span> | <span data-ttu-id="bb0fa-340">Status of the containers, if any.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-340">Status of the containers, if any.</span></span> <span data-ttu-id="bb0fa-341">Additional details of the status icon are provided in the next table.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-341">Additional details of the status icon are provided in the next table.</span></span>|
| <span data-ttu-id="bb0fa-342">Avg&nbsp;%, Min&nbsp;%, Max&nbsp;%, 50th&nbsp;%, 90th&nbsp;%</span><span class="sxs-lookup"><span data-stu-id="bb0fa-342">Avg&nbsp;%, Min&nbsp;%, Max&nbsp;%, 50th&nbsp;%, 90th&nbsp;%</span></span> | <span data-ttu-id="bb0fa-343">The roll-up of the average percentage of each entity for the selected metric and percentile.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-343">The roll-up of the average percentage of each entity for the selected metric and percentile.</span></span> |
| <span data-ttu-id="bb0fa-344">Avg, Min, Max, 50th, 90th</span><span class="sxs-lookup"><span data-stu-id="bb0fa-344">Avg, Min, Max, 50th, 90th</span></span>  | <span data-ttu-id="bb0fa-345">The roll-up of the average CPU millicore or memory performance of the container for the selected percentile.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-345">The roll-up of the average CPU millicore or memory performance of the container for the selected percentile.</span></span> <span data-ttu-id="bb0fa-346">The average value is measured from the CPU/Memory limit set for a pod.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-346">The average value is measured from the CPU/Memory limit set for a pod.</span></span> |
| <span data-ttu-id="bb0fa-347">Pod</span><span class="sxs-lookup"><span data-stu-id="bb0fa-347">Pod</span></span> | <span data-ttu-id="bb0fa-348">Container where the pod resides.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-348">Container where the pod resides.</span></span>| 
| <span data-ttu-id="bb0fa-349">Node</span><span class="sxs-lookup"><span data-stu-id="bb0fa-349">Node</span></span> |  <span data-ttu-id="bb0fa-350">Node where the container resides.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-350">Node where the container resides.</span></span> | 
| <span data-ttu-id="bb0fa-351">Restarts</span><span class="sxs-lookup"><span data-stu-id="bb0fa-351">Restarts</span></span> | <span data-ttu-id="bb0fa-352">Represents the time since a container started.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-352">Represents the time since a container started.</span></span> |
| <span data-ttu-id="bb0fa-353">Uptime</span><span class="sxs-lookup"><span data-stu-id="bb0fa-353">Uptime</span></span> | <span data-ttu-id="bb0fa-354">Represents the time since a container was started or rebooted.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-354">Represents the time since a container was started or rebooted.</span></span> |
| <span data-ttu-id="bb0fa-355">Trend Avg&nbsp;%, Min&nbsp;%, Max&nbsp;%, 50th&nbsp;%, 90th&nbsp;%</span><span class="sxs-lookup"><span data-stu-id="bb0fa-355">Trend Avg&nbsp;%, Min&nbsp;%, Max&nbsp;%, 50th&nbsp;%, 90th&nbsp;%</span></span> | <span data-ttu-id="bb0fa-356">A bar graph trend that represents the average metric percentage of the container.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-356">A bar graph trend that represents the average metric percentage of the container.</span></span> |

<span data-ttu-id="bb0fa-357">The icons in the status field indicate the online statuses of pods, as described in the following table:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-357">The icons in the status field indicate the online statuses of pods, as described in the following table:</span></span>
 
| <span data-ttu-id="bb0fa-358">Icon</span><span class="sxs-lookup"><span data-stu-id="bb0fa-358">Icon</span></span> | <span data-ttu-id="bb0fa-359">Status</span><span class="sxs-lookup"><span data-stu-id="bb0fa-359">Status</span></span> | 
|--------|-------------|
| ![Ready running status icon](./media/monitoring-container-health/container-health-ready-icon.png) | <span data-ttu-id="bb0fa-361">Running (Ready)</span><span class="sxs-lookup"><span data-stu-id="bb0fa-361">Running (Ready)</span></span>|
| ![Waiting or paused status icon](./media/monitoring-container-health/container-health-waiting-icon.png) | <span data-ttu-id="bb0fa-363">Waiting or Paused</span><span class="sxs-lookup"><span data-stu-id="bb0fa-363">Waiting or Paused</span></span>|
| ![Last reported running status icon](./media/monitoring-container-health/container-health-grey-icon.png) | <span data-ttu-id="bb0fa-365">Last reported running but hasn't responded in more than 30 minutes</span><span class="sxs-lookup"><span data-stu-id="bb0fa-365">Last reported running but hasn't responded in more than 30 minutes</span></span>|
| ![Terminated status icon](./media/monitoring-container-health/container-health-terminated-icon.png) | <span data-ttu-id="bb0fa-367">Successfully stopped or failed to stop</span><span class="sxs-lookup"><span data-stu-id="bb0fa-367">Successfully stopped or failed to stop</span></span>|
| ![Failed status icon](./media/monitoring-container-health/container-health-failed-icon.png) | <span data-ttu-id="bb0fa-369">Failed state</span><span class="sxs-lookup"><span data-stu-id="bb0fa-369">Failed state</span></span> |

## <a name="container-data-collection-details"></a><span data-ttu-id="bb0fa-370">Container data-collection details</span><span class="sxs-lookup"><span data-stu-id="bb0fa-370">Container data-collection details</span></span>
<span data-ttu-id="bb0fa-371">Container health collects various performance metrics and log data from container hosts and containers.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-371">Container health collects various performance metrics and log data from container hosts and containers.</span></span> <span data-ttu-id="bb0fa-372">Data is collected every three minutes.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-372">Data is collected every three minutes.</span></span>

### <a name="container-records"></a><span data-ttu-id="bb0fa-373">Container records</span><span class="sxs-lookup"><span data-stu-id="bb0fa-373">Container records</span></span>

<span data-ttu-id="bb0fa-374">Examples of records that are collected by container health and the data types that appear in log search results are displayed in the following table:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-374">Examples of records that are collected by container health and the data types that appear in log search results are displayed in the following table:</span></span>

| <span data-ttu-id="bb0fa-375">Data type</span><span class="sxs-lookup"><span data-stu-id="bb0fa-375">Data type</span></span> | <span data-ttu-id="bb0fa-376">Data type in Log Search</span><span class="sxs-lookup"><span data-stu-id="bb0fa-376">Data type in Log Search</span></span> | <span data-ttu-id="bb0fa-377">Fields</span><span class="sxs-lookup"><span data-stu-id="bb0fa-377">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb0fa-378">Performance for hosts and containers</span><span class="sxs-lookup"><span data-stu-id="bb0fa-378">Performance for hosts and containers</span></span> | `Perf` | <span data-ttu-id="bb0fa-379">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue, TimeGenerated, CounterPath, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="bb0fa-379">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue, TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="bb0fa-380">Container inventory</span><span class="sxs-lookup"><span data-stu-id="bb0fa-380">Container inventory</span></span> | `ContainerInventory` | <span data-ttu-id="bb0fa-381">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span><span class="sxs-lookup"><span data-stu-id="bb0fa-381">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="bb0fa-382">Container image inventory</span><span class="sxs-lookup"><span data-stu-id="bb0fa-382">Container image inventory</span></span> | `ContainerImageInventory` | <span data-ttu-id="bb0fa-383">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="bb0fa-383">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="bb0fa-384">Container log</span><span class="sxs-lookup"><span data-stu-id="bb0fa-384">Container log</span></span> | `ContainerLog` | <span data-ttu-id="bb0fa-385">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="bb0fa-385">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="bb0fa-386">Container service log</span><span class="sxs-lookup"><span data-stu-id="bb0fa-386">Container service log</span></span> | `ContainerServiceLog`  | <span data-ttu-id="bb0fa-387">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="bb0fa-387">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="bb0fa-388">Container node inventory</span><span class="sxs-lookup"><span data-stu-id="bb0fa-388">Container node inventory</span></span> | `ContainerNodeInventory_CL`| <span data-ttu-id="bb0fa-389">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="bb0fa-389">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="bb0fa-390">Container process</span><span class="sxs-lookup"><span data-stu-id="bb0fa-390">Container process</span></span> | `ContainerProcess_CL` | <span data-ttu-id="bb0fa-391">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="bb0fa-391">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="bb0fa-392">Inventory of pods in a Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="bb0fa-392">Inventory of pods in a Kubernetes cluster</span></span> | `KubePodInventory` | <span data-ttu-id="bb0fa-393">TimeGenerated, Computer, ClusterId, ContainerCreationTimeStamp, PodUid, PodCreationTimeStamp, ContainerRestartCount, PodRestartCount, PodStartTime, ContainerStartTime, ServiceName, ControllerKind, ControllerName, ContainerStatus, ContainerID, ContainerName, Name, PodLabel, Namespace, PodStatus, ClusterName, PodIp, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="bb0fa-393">TimeGenerated, Computer, ClusterId, ContainerCreationTimeStamp, PodUid, PodCreationTimeStamp, ContainerRestartCount, PodRestartCount, PodStartTime, ContainerStartTime, ServiceName, ControllerKind, ControllerName, ContainerStatus, ContainerID, ContainerName, Name, PodLabel, Namespace, PodStatus, ClusterName, PodIp, SourceSystem</span></span> |
| <span data-ttu-id="bb0fa-394">Inventory of nodes part of a Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="bb0fa-394">Inventory of nodes part of a Kubernetes cluster</span></span> | `KubeNodeInventory` | <span data-ttu-id="bb0fa-395">TimeGenerated, Computer, ClusterName, ClusterId, LastTransitionTimeReady, Labels, Status, KubeletVersion, KubeProxyVersion, CreationTimeStamp, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="bb0fa-395">TimeGenerated, Computer, ClusterName, ClusterId, LastTransitionTimeReady, Labels, Status, KubeletVersion, KubeProxyVersion, CreationTimeStamp, SourceSystem</span></span> | 
| <span data-ttu-id="bb0fa-396">Kubernetes Events</span><span class="sxs-lookup"><span data-stu-id="bb0fa-396">Kubernetes Events</span></span> | `KubeEvents_CL` | <span data-ttu-id="bb0fa-397">TimeGenerated, Computer, ClusterId_s, FirstSeen_t, LastSeen_t, Count_d, ObjectKind_s, Namespace_s, Name_s, Reason_s, Type_s, TimeGenerated_s, SourceComponent_s, ClusterName_s, Message,  SourceSystem</span><span class="sxs-lookup"><span data-stu-id="bb0fa-397">TimeGenerated, Computer, ClusterId_s, FirstSeen_t, LastSeen_t, Count_d, ObjectKind_s, Namespace_s, Name_s, Reason_s, Type_s, TimeGenerated_s, SourceComponent_s, ClusterName_s, Message,  SourceSystem</span></span> | 
| <span data-ttu-id="bb0fa-398">Services in the Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="bb0fa-398">Services in the Kubernetes cluster</span></span> | `KubeServices_CL` | <span data-ttu-id="bb0fa-399">TimeGenerated, ServiceName_s, Namespace_s, SelectorLabels_s, ClusterId_s, ClusterName_s, ClusterIP_s, ServiceType_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="bb0fa-399">TimeGenerated, ServiceName_s, Namespace_s, SelectorLabels_s, ClusterId_s, ClusterName_s, ClusterIP_s, ServiceType_s, SourceSystem</span></span> | 
| <span data-ttu-id="bb0fa-400">Performance metrics for nodes part of the Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="bb0fa-400">Performance metrics for nodes part of the Kubernetes cluster</span></span> | <span data-ttu-id="bb0fa-401">Perf &#124; where ObjectName == “K8SNode”</span><span class="sxs-lookup"><span data-stu-id="bb0fa-401">Perf &#124; where ObjectName == “K8SNode”</span></span> | <span data-ttu-id="bb0fa-402">Computer, ObjectName, CounterName &#40;cpuUsageNanoCores, , memoryWorkingSetBytes, memoryRssBytes, networkRxBytes, networkTxBytes, restartTimeEpoch, networkRxBytesPerSec, networkTxBytesPerSec, cpuAllocatableNanoCores, memoryAllocatableBytes, cpuCapacityNanoCores, memoryCapacityBytes&#41;,CounterValue, TimeGenerated, CounterPath, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="bb0fa-402">Computer, ObjectName, CounterName &#40;cpuUsageNanoCores, , memoryWorkingSetBytes, memoryRssBytes, networkRxBytes, networkTxBytes, restartTimeEpoch, networkRxBytesPerSec, networkTxBytesPerSec, cpuAllocatableNanoCores, memoryAllocatableBytes, cpuCapacityNanoCores, memoryCapacityBytes&#41;,CounterValue, TimeGenerated, CounterPath, SourceSystem</span></span> | 
| <span data-ttu-id="bb0fa-403">Performance metrics for containers part of the Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="bb0fa-403">Performance metrics for containers part of the Kubernetes cluster</span></span> | <span data-ttu-id="bb0fa-404">Perf &#124; where ObjectName == “K8SContainer”</span><span class="sxs-lookup"><span data-stu-id="bb0fa-404">Perf &#124; where ObjectName == “K8SContainer”</span></span> | <span data-ttu-id="bb0fa-405">CounterName &#40;cpuUsageNanoCores, memoryWorkingSetBytes, memoryRssBytes, restartTimeEpoch, cpuRequestNanoCores, memoryRequestBytes, cpuLimitNanoCores, memoryLimitBytes&#41;,CounterValue, TimeGenerated, CounterPath, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="bb0fa-405">CounterName &#40;cpuUsageNanoCores, memoryWorkingSetBytes, memoryRssBytes, restartTimeEpoch, cpuRequestNanoCores, memoryRequestBytes, cpuLimitNanoCores, memoryLimitBytes&#41;,CounterValue, TimeGenerated, CounterPath, SourceSystem</span></span> | 

## <a name="search-logs-to-analyze-data"></a><span data-ttu-id="bb0fa-406">Search logs to analyze data</span><span class="sxs-lookup"><span data-stu-id="bb0fa-406">Search logs to analyze data</span></span>
<span data-ttu-id="bb0fa-407">Log Analytics can help you look for trends, diagnose bottlenecks, forecast, or correlate data that can help you determine whether the current cluster configuration is performing optimally.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-407">Log Analytics can help you look for trends, diagnose bottlenecks, forecast, or correlate data that can help you determine whether the current cluster configuration is performing optimally.</span></span> <span data-ttu-id="bb0fa-408">Pre-defined log searches are provided for you to immediately start using or to customize to return the information the way you want.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-408">Pre-defined log searches are provided for you to immediately start using or to customize to return the information the way you want.</span></span> 

<span data-ttu-id="bb0fa-409">You can perform interactive analysis of data in the workspace by selecting the **View Kubernetes event logs** or **View container logs** option in the preview pane.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-409">You can perform interactive analysis of data in the workspace by selecting the **View Kubernetes event logs** or **View container logs** option in the preview pane.</span></span> <span data-ttu-id="bb0fa-410">The **Log Search** page appears to the right of the Azure portal page that you were on.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-410">The **Log Search** page appears to the right of the Azure portal page that you were on.</span></span>

![Analyze data in Log Analytics](./media/monitoring-container-health/container-health-log-search-example.png)   

<span data-ttu-id="bb0fa-412">The container logs output that's forwarded to Log Analytics are STDOUT and STDERR.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-412">The container logs output that's forwarded to Log Analytics are STDOUT and STDERR.</span></span> <span data-ttu-id="bb0fa-413">Because container health is monitoring Azure-managed Kubernetes (AKS), Kube-system is not collected today because of the large volume of generated data.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-413">Because container health is monitoring Azure-managed Kubernetes (AKS), Kube-system is not collected today because of the large volume of generated data.</span></span> 

### <a name="example-log-search-queries"></a><span data-ttu-id="bb0fa-414">Example log search queries</span><span class="sxs-lookup"><span data-stu-id="bb0fa-414">Example log search queries</span></span>
<span data-ttu-id="bb0fa-415">It's often useful to build queries that start with an example or two and then modify them to fit your requirements.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-415">It's often useful to build queries that start with an example or two and then modify them to fit your requirements.</span></span> <span data-ttu-id="bb0fa-416">To help build more advanced queries, you can experiment with the following sample queries:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-416">To help build more advanced queries, you can experiment with the following sample queries:</span></span>

| <span data-ttu-id="bb0fa-417">Query</span><span class="sxs-lookup"><span data-stu-id="bb0fa-417">Query</span></span> | <span data-ttu-id="bb0fa-418">Description</span><span class="sxs-lookup"><span data-stu-id="bb0fa-418">Description</span></span> | 
|-------|-------------|
| <span data-ttu-id="bb0fa-419">ContainerInventory</span><span class="sxs-lookup"><span data-stu-id="bb0fa-419">ContainerInventory</span></span><br> <span data-ttu-id="bb0fa-420">&#124; project Computer, Name, Image, ImageTag, ContainerState, CreatedTime, StartedTime, FinishedTime</span><span class="sxs-lookup"><span data-stu-id="bb0fa-420">&#124; project Computer, Name, Image, ImageTag, ContainerState, CreatedTime, StartedTime, FinishedTime</span></span><br> <span data-ttu-id="bb0fa-421">&#124; render table</span><span class="sxs-lookup"><span data-stu-id="bb0fa-421">&#124; render table</span></span> | <span data-ttu-id="bb0fa-422">List all of a container's lifecycle information</span><span class="sxs-lookup"><span data-stu-id="bb0fa-422">List all of a container's lifecycle information</span></span>| 
| <span data-ttu-id="bb0fa-423">KubeEvents_CL</span><span class="sxs-lookup"><span data-stu-id="bb0fa-423">KubeEvents_CL</span></span><br> <span data-ttu-id="bb0fa-424">&#124; where not(isempty(Namespace_s))</span><span class="sxs-lookup"><span data-stu-id="bb0fa-424">&#124; where not(isempty(Namespace_s))</span></span><br> <span data-ttu-id="bb0fa-425">&#124; sort by TimeGenerated desc</span><span class="sxs-lookup"><span data-stu-id="bb0fa-425">&#124; sort by TimeGenerated desc</span></span><br> <span data-ttu-id="bb0fa-426">&#124; render table</span><span class="sxs-lookup"><span data-stu-id="bb0fa-426">&#124; render table</span></span> | <span data-ttu-id="bb0fa-427">Kubernetes events</span><span class="sxs-lookup"><span data-stu-id="bb0fa-427">Kubernetes events</span></span>|
| <span data-ttu-id="bb0fa-428">ContainerImageInventory</span><span class="sxs-lookup"><span data-stu-id="bb0fa-428">ContainerImageInventory</span></span><br> <span data-ttu-id="bb0fa-429">&#124; summarize AggregatedValue = count() by Image, ImageTag, Running</span><span class="sxs-lookup"><span data-stu-id="bb0fa-429">&#124; summarize AggregatedValue = count() by Image, ImageTag, Running</span></span> | <span data-ttu-id="bb0fa-430">Image inventory</span><span class="sxs-lookup"><span data-stu-id="bb0fa-430">Image inventory</span></span> | 
| <span data-ttu-id="bb0fa-431">**In Advanced Analytics, select line charts**:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-431">**In Advanced Analytics, select line charts**:</span></span><br> <span data-ttu-id="bb0fa-432">Perf</span><span class="sxs-lookup"><span data-stu-id="bb0fa-432">Perf</span></span><br> <span data-ttu-id="bb0fa-433">&#124; where ObjectName == "Container" and CounterName == "% Processor Time"</span><span class="sxs-lookup"><span data-stu-id="bb0fa-433">&#124; where ObjectName == "Container" and CounterName == "% Processor Time"</span></span><br> <span data-ttu-id="bb0fa-434">&#124; summarize AvgCPUPercent = avg(CounterValue) by bin(TimeGenerated, 30m), InstanceName</span><span class="sxs-lookup"><span data-stu-id="bb0fa-434">&#124; summarize AvgCPUPercent = avg(CounterValue) by bin(TimeGenerated, 30m), InstanceName</span></span> | <span data-ttu-id="bb0fa-435">Container CPU</span><span class="sxs-lookup"><span data-stu-id="bb0fa-435">Container CPU</span></span> | 
| <span data-ttu-id="bb0fa-436">**In Advanced Analytics, select line charts**:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-436">**In Advanced Analytics, select line charts**:</span></span><br> <span data-ttu-id="bb0fa-437">Perf &#124; where ObjectName == "Container" and CounterName == "Memory Usage MB"</span><span class="sxs-lookup"><span data-stu-id="bb0fa-437">Perf &#124; where ObjectName == "Container" and CounterName == "Memory Usage MB"</span></span><br> <span data-ttu-id="bb0fa-438">&#124; summarize AvgUsedMemory = avg(CounterValue) by bin(TimeGenerated, 30m), InstanceName</span><span class="sxs-lookup"><span data-stu-id="bb0fa-438">&#124; summarize AvgUsedMemory = avg(CounterValue) by bin(TimeGenerated, 30m), InstanceName</span></span> | <span data-ttu-id="bb0fa-439">Container memory</span><span class="sxs-lookup"><span data-stu-id="bb0fa-439">Container memory</span></span> |

## <a name="how-to-stop-monitoring-with-container-health"></a><span data-ttu-id="bb0fa-440">How to stop monitoring with container health</span><span class="sxs-lookup"><span data-stu-id="bb0fa-440">How to stop monitoring with container health</span></span>
<span data-ttu-id="bb0fa-441">If, after you enable monitoring of your AKS container, you decide you no longer want to monitor it, you can *opt out* by using either the provided Azure Resource Manager templates with the PowerShell cmdlet **New-AzureRmResourceGroupDeployment** or the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-441">If, after you enable monitoring of your AKS container, you decide you no longer want to monitor it, you can *opt out* by using either the provided Azure Resource Manager templates with the PowerShell cmdlet **New-AzureRmResourceGroupDeployment** or the Azure CLI.</span></span> <span data-ttu-id="bb0fa-442">One JSON template specifies the configuration to *opt out*. The other contains parameter values that you configure to specify the AKS cluster resource ID and resource group that the cluster is deployed in.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-442">One JSON template specifies the configuration to *opt out*. The other contains parameter values that you configure to specify the AKS cluster resource ID and resource group that the cluster is deployed in.</span></span> 

<span data-ttu-id="bb0fa-443">If you're unfamiliar with the concept of deploying resources by using a template, see:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-443">If you're unfamiliar with the concept of deploying resources by using a template, see:</span></span>
* [<span data-ttu-id="bb0fa-444">Deploy resources with Resource Manager templates and Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb0fa-444">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="bb0fa-445">Deploy resources with Resource Manager templates and the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bb0fa-445">Deploy resources with Resource Manager templates and the Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)

<span data-ttu-id="bb0fa-446">If you choose to use the Azure CLI, you first need to install and use the CLI locally.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-446">If you choose to use the Azure CLI, you first need to install and use the CLI locally.</span></span> <span data-ttu-id="bb0fa-447">You must be running the Azure CLI version 2.0.27 or later.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-447">You must be running the Azure CLI version 2.0.27 or later.</span></span> <span data-ttu-id="bb0fa-448">To identify your version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-448">To identify your version, run `az --version`.</span></span> <span data-ttu-id="bb0fa-449">If you need to install or upgrade the Azure CLI, see [Install the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bb0fa-449">If you need to install or upgrade the Azure CLI, see [Install the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

### <a name="create-and-execute-template"></a><span data-ttu-id="bb0fa-450">Create and execute template</span><span class="sxs-lookup"><span data-stu-id="bb0fa-450">Create and execute template</span></span>

1. <span data-ttu-id="bb0fa-451">Copy and paste the following JSON syntax into your file:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-451">Copy and paste the following JSON syntax into your file:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "aksResourceId": {
           "type": "string",
           "metadata": {
             "description": "AKS Cluster Resource ID"
           }
       },
      "aksResourceLocation": {
        "type": "string",
        "metadata": {
           "description": "Location of the AKS resource e.g. \"East US\""
         }
       }
    },
    "resources": [
      {
        "name": "[split(parameters('aksResourceId'),'/')[8]]",
        "type": "Microsoft.ContainerService/managedClusters",
        "location": "[parameters('aksResourceLocation')]",
        "apiVersion": "2018-03-31",
        "properties": {
          "mode": "Incremental",
          "id": "[parameters('aksResourceId')]",
          "addonProfiles": {
            "omsagent": {
              "enabled": false,
              "config": null
            }
           }
         }
       }
      ]
    }
    ```

2. <span data-ttu-id="bb0fa-452">Save this file as **OptOutTemplate.json** to a local folder.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-452">Save this file as **OptOutTemplate.json** to a local folder.</span></span>
3. <span data-ttu-id="bb0fa-453">Paste the following JSON syntax into your file:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-453">Paste the following JSON syntax into your file:</span></span>

    ```json
    {
     "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
       "aksResourceId": {
         "value": "/subscriptions/<SubscriptionID>/resourcegroups/<ResourceGroup>/providers/Microsoft.ContainerService/managedClusters/<ResourceName>"
      },
      "aksResourceLocation": {
        "value": "<aksClusterRegion>"
        }
      }
    }
    ```

4. <span data-ttu-id="bb0fa-454">Edit the values for **aksResourceId** and **aksResourceLocation** by using the values of the AKS cluster, which you can find on the **Properties** page for the selected cluster.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-454">Edit the values for **aksResourceId** and **aksResourceLocation** by using the values of the AKS cluster, which you can find on the **Properties** page for the selected cluster.</span></span>

    ![Container properties page](./media/monitoring-container-health/container-properties-page.png)

    <span data-ttu-id="bb0fa-456">While you are on the **Properties** page, also copy the **Workspace Resource ID**.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-456">While you are on the **Properties** page, also copy the **Workspace Resource ID**.</span></span> <span data-ttu-id="bb0fa-457">This value is required if you decide you want to delete the Log Analytics workspace later.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-457">This value is required if you decide you want to delete the Log Analytics workspace later.</span></span> <span data-ttu-id="bb0fa-458">Deleting the Log Analytics workspace is not performed as part of this process.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-458">Deleting the Log Analytics workspace is not performed as part of this process.</span></span> 

5. <span data-ttu-id="bb0fa-459">Save this file as **OptOutParam.json** to a local folder.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-459">Save this file as **OptOutParam.json** to a local folder.</span></span>
6. <span data-ttu-id="bb0fa-460">You are ready to deploy this template.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-460">You are ready to deploy this template.</span></span> 

    * <span data-ttu-id="bb0fa-461">To use the following PowerShell commands in the folder containing the template:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-461">To use the following PowerShell commands in the folder containing the template:</span></span>

        ```powershell
        Connect-AzureRmAccount
        Select-AzureRmSubscription -SubscriptionName <yourSubscriptionName>
        New-AzureRmResourceGroupDeployment -Name opt-out -ResourceGroupName <ResourceGroupName> -TemplateFile .\OptOutTemplate.json -TemplateParameterFile .\OptOutParam.json
        ```

        <span data-ttu-id="bb0fa-462">The configuration change can take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-462">The configuration change can take a few minutes to complete.</span></span> <span data-ttu-id="bb0fa-463">When it's completed, a message similar to the following that includes the result is returned:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-463">When it's completed, a message similar to the following that includes the result is returned:</span></span>

        ```powershell
        ProvisioningState       : Succeeded
        ```

    * <span data-ttu-id="bb0fa-464">To run following command with Azure CLI on Linux:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-464">To run following command with Azure CLI on Linux:</span></span>

        ```azurecli
        az login   
        az account set --subscription "Subscription Name" 
        az group deployment create --resource-group <ResourceGroupName> --template-file ./OptOutTemplate.json --parameters @./OptOutParam.json  
        ```

        <span data-ttu-id="bb0fa-465">The configuration change can take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-465">The configuration change can take a few minutes to complete.</span></span> <span data-ttu-id="bb0fa-466">When it's completed, a message similar to the following that includes the result is returned:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-466">When it's completed, a message similar to the following that includes the result is returned:</span></span>

        ```azurecli
        ProvisioningState       : Succeeded
        ```

<span data-ttu-id="bb0fa-467">If the workspace was created only to support monitoring the cluster and it's no longer needed, you have to manually delete it.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-467">If the workspace was created only to support monitoring the cluster and it's no longer needed, you have to manually delete it.</span></span> <span data-ttu-id="bb0fa-468">If you are not familiar with how to delete a workspace, see [Delete an Azure Log Analytics workspace with the Azure portal](../log-analytics/log-analytics-manage-del-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="bb0fa-468">If you are not familiar with how to delete a workspace, see [Delete an Azure Log Analytics workspace with the Azure portal](../log-analytics/log-analytics-manage-del-workspace.md).</span></span> <span data-ttu-id="bb0fa-469">Don't forget about the **Workspace Resource ID** we copied earlier in step 4, you're going to need that.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-469">Don't forget about the **Workspace Resource ID** we copied earlier in step 4, you're going to need that.</span></span> 

## <a name="troubleshooting"></a><span data-ttu-id="bb0fa-470">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="bb0fa-470">Troubleshooting</span></span>
<span data-ttu-id="bb0fa-471">This section provides information to help troubleshoot issues with container health.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-471">This section provides information to help troubleshoot issues with container health.</span></span>

<span data-ttu-id="bb0fa-472">If container health was successfully enabled and configured but you cannot view status information or results in Log Analytics when you perform a log search, you can help diagnose the problem by doing the following:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-472">If container health was successfully enabled and configured but you cannot view status information or results in Log Analytics when you perform a log search, you can help diagnose the problem by doing the following:</span></span> 

1. <span data-ttu-id="bb0fa-473">Check the status of the agent by running the following command:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-473">Check the status of the agent by running the following command:</span></span> 

    `kubectl get ds omsagent --namespace=kube-system`

    <span data-ttu-id="bb0fa-474">The output should resemble the following, which indicates that it was deployed properly:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-474">The output should resemble the following, which indicates that it was deployed properly:</span></span>

    ```
    User@aksuser:~$ kubectl get ds omsagent --namespace=kube-system 
    NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE SELECTOR                 AGE
    omsagent   2         2         2         2            2           beta.kubernetes.io/os=linux   1d
    ```  
2. <span data-ttu-id="bb0fa-475">Check the solution deployment status with agent version *06072018* or later by running the following command:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-475">Check the solution deployment status with agent version *06072018* or later by running the following command:</span></span>

    `kubectl get deployment omsagent-rs -n=kube-system`

    <span data-ttu-id="bb0fa-476">The output should resemble the following, which indicates that it was deployed properly:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-476">The output should resemble the following, which indicates that it was deployed properly:</span></span>

    ```
    User@aksuser:~$ kubectl get deployment omsagent-rs -n=kube-system 
    NAME       DESIRED   CURRENT   UP-TO-DATE   AVAILABLE    AGE
    omsagent   1         1         1            1            3h
    ```

3. <span data-ttu-id="bb0fa-477">Check the status of the pod to verify that it is running by running the following command: `kubectl get pods --namespace=kube-system`</span><span class="sxs-lookup"><span data-stu-id="bb0fa-477">Check the status of the pod to verify that it is running by running the following command: `kubectl get pods --namespace=kube-system`</span></span>

    <span data-ttu-id="bb0fa-478">The output should resemble the following with a status of *Running* for the omsagent:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-478">The output should resemble the following with a status of *Running* for the omsagent:</span></span>

    ```
    User@aksuser:~$ kubectl get pods --namespace=kube-system 
    NAME                                READY     STATUS    RESTARTS   AGE 
    aks-ssh-139866255-5n7k5             1/1       Running   0          8d 
    azure-vote-back-4149398501-7skz0    1/1       Running   0          22d 
    azure-vote-front-3826909965-30n62   1/1       Running   0          22d 
    omsagent-484hw                      1/1       Running   0          1d 
    omsagent-fkq7g                      1/1       Running   0          1d 
    ```

4. <span data-ttu-id="bb0fa-479">Check the agent logs.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-479">Check the agent logs.</span></span> <span data-ttu-id="bb0fa-480">When the containerized agent gets deployed, it runs a quick check by running OMI commands and displays the version of the agent and provider.</span><span class="sxs-lookup"><span data-stu-id="bb0fa-480">When the containerized agent gets deployed, it runs a quick check by running OMI commands and displays the version of the agent and provider.</span></span> 

5. <span data-ttu-id="bb0fa-481">To verify that the agent has been onboarded successfully, run the following command: `kubectl logs omsagent-484hw --namespace=kube-system`</span><span class="sxs-lookup"><span data-stu-id="bb0fa-481">To verify that the agent has been onboarded successfully, run the following command: `kubectl logs omsagent-484hw --namespace=kube-system`</span></span>

    <span data-ttu-id="bb0fa-482">The status should resemble the following:</span><span class="sxs-lookup"><span data-stu-id="bb0fa-482">The status should resemble the following:</span></span>

    ```
    User@aksuser:~$ kubectl logs omsagent-484hw --namespace=kube-system
    :
    :
    instance of Container_HostInventory
    {
        [Key] InstanceID=3a4407a5-d840-4c59-b2f0-8d42e07298c2
        Computer=aks-nodepool1-39773055-0
        DockerVersion=1.13.1
        OperatingSystem=Ubuntu 16.04.3 LTS
        Volume=local
        Network=bridge host macvlan null overlay
        NodeRole=Not Orchestrated
        OrchestratorType=Kubernetes
    }
    Primary Workspace: b438b4f6-912a-46d5-9cb1-b44069212abc    Status: Onboarded(OMSAgent Running)
    omi 1.4.2.2
    omsagent 1.6.0.23
    docker-cimprov 1.0.0.31
    ```

## <a name="next-steps"></a><span data-ttu-id="bb0fa-483">Next steps</span><span class="sxs-lookup"><span data-stu-id="bb0fa-483">Next steps</span></span>

<span data-ttu-id="bb0fa-484">To view detailed container health and application performance information, see [Search logs](../log-analytics/log-analytics-log-search.md).</span><span class="sxs-lookup"><span data-stu-id="bb0fa-484">To view detailed container health and application performance information, see [Search logs](../log-analytics/log-analytics-log-search.md).</span></span> 
