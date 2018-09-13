---
title: Container instance logging with Azure Log Analytics
description: Learn how to send container output (STDOUT and STDERR) to Azure Log Analytics.
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: overview
ms.date: 07/17/2018
ms.author: marsma
ms.openlocfilehash: e4c1efbf4c2c844bae971fa1136e0fe3bed18bcc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870563"
---
# <a name="container-instance-logging-with-azure-log-analytics"></a><span data-ttu-id="475fc-103">Container instance logging with Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="475fc-103">Container instance logging with Azure Log Analytics</span></span>

<span data-ttu-id="475fc-104">Log Analytics workspaces provide a centralized location for storing and querying log data from not only Azure resources, but also on premises resources and resources in other clouds.</span><span class="sxs-lookup"><span data-stu-id="475fc-104">Log Analytics workspaces provide a centralized location for storing and querying log data from not only Azure resources, but also on premises resources and resources in other clouds.</span></span> <span data-ttu-id="475fc-105">Azure Container Instances includes built-in support for sending data to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="475fc-105">Azure Container Instances includes built-in support for sending data to Log Analytics.</span></span>

<span data-ttu-id="475fc-106">To send container instance data to Log Analytics, you must create a container group by using the Azure CLI (or Cloud Shell) and a YAML file.</span><span class="sxs-lookup"><span data-stu-id="475fc-106">To send container instance data to Log Analytics, you must create a container group by using the Azure CLI (or Cloud Shell) and a YAML file.</span></span> <span data-ttu-id="475fc-107">The following sections describe creating a logging-enabled container group and querying logs.</span><span class="sxs-lookup"><span data-stu-id="475fc-107">The following sections describe creating a logging-enabled container group and querying logs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="475fc-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="475fc-108">Prerequisites</span></span>

<span data-ttu-id="475fc-109">To enable logging in your container instances, you need the following:</span><span class="sxs-lookup"><span data-stu-id="475fc-109">To enable logging in your container instances, you need the following:</span></span>

* [<span data-ttu-id="475fc-110">Log Analytics workspace</span><span class="sxs-lookup"><span data-stu-id="475fc-110">Log Analytics workspace</span></span>](../log-analytics/log-analytics-quick-create-workspace.md)
* <span data-ttu-id="475fc-111">[Azure CLI](/cli/azure/install-azure-cli) (or [Cloud Shell](/azure/cloud-shell/overview))</span><span class="sxs-lookup"><span data-stu-id="475fc-111">[Azure CLI](/cli/azure/install-azure-cli) (or [Cloud Shell](/azure/cloud-shell/overview))</span></span>

## <a name="get-log-analytics-credentials"></a><span data-ttu-id="475fc-112">Get Log Analytics credentials</span><span class="sxs-lookup"><span data-stu-id="475fc-112">Get Log Analytics credentials</span></span>

<span data-ttu-id="475fc-113">Azure Container Instances needs permission to send data to your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="475fc-113">Azure Container Instances needs permission to send data to your Log Analytics workspace.</span></span> <span data-ttu-id="475fc-114">To grant this permission and enable logging, you must provide the Log Analytics workspace ID and one of its keys (either primary or secondary) when you create the container group.</span><span class="sxs-lookup"><span data-stu-id="475fc-114">To grant this permission and enable logging, you must provide the Log Analytics workspace ID and one of its keys (either primary or secondary) when you create the container group.</span></span>

<span data-ttu-id="475fc-115">To obtain the Log Analytics workspace ID and primary key:</span><span class="sxs-lookup"><span data-stu-id="475fc-115">To obtain the Log Analytics workspace ID and primary key:</span></span>

1. <span data-ttu-id="475fc-116">Navigate to your Log Analytics workspace in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="475fc-116">Navigate to your Log Analytics workspace in the Azure portal</span></span>
1. <span data-ttu-id="475fc-117">Under **SETTINGS**, select **Advanced settings**</span><span class="sxs-lookup"><span data-stu-id="475fc-117">Under **SETTINGS**, select **Advanced settings**</span></span>
1. <span data-ttu-id="475fc-118">Select **Connected Sources** > **Windows Servers** (or **Linux Servers**--the ID and keys are the same for both)</span><span class="sxs-lookup"><span data-stu-id="475fc-118">Select **Connected Sources** > **Windows Servers** (or **Linux Servers**--the ID and keys are the same for both)</span></span>
1. <span data-ttu-id="475fc-119">Take note of:</span><span class="sxs-lookup"><span data-stu-id="475fc-119">Take note of:</span></span>
   * <span data-ttu-id="475fc-120">**WORKSPACE ID**</span><span class="sxs-lookup"><span data-stu-id="475fc-120">**WORKSPACE ID**</span></span>
   * <span data-ttu-id="475fc-121">**PRIMARY KEY**</span><span class="sxs-lookup"><span data-stu-id="475fc-121">**PRIMARY KEY**</span></span>

## <a name="create-container-group"></a><span data-ttu-id="475fc-122">Create container group</span><span class="sxs-lookup"><span data-stu-id="475fc-122">Create container group</span></span>

<span data-ttu-id="475fc-123">Now that you have the Log Analytics workspace ID and primary key, you're ready to create a logging-enabled container group.</span><span class="sxs-lookup"><span data-stu-id="475fc-123">Now that you have the Log Analytics workspace ID and primary key, you're ready to create a logging-enabled container group.</span></span>

<span data-ttu-id="475fc-124">The following examples demonstrate two ways to create a container group with a single [fluentd][fluentd] container: Azure CLI, and Azure CLI with a YAML template.</span><span class="sxs-lookup"><span data-stu-id="475fc-124">The following examples demonstrate two ways to create a container group with a single [fluentd][fluentd] container: Azure CLI, and Azure CLI with a YAML template.</span></span> <span data-ttu-id="475fc-125">The Fluentd container produces several lines of output in its default configuration.</span><span class="sxs-lookup"><span data-stu-id="475fc-125">The Fluentd container produces several lines of output in its default configuration.</span></span> <span data-ttu-id="475fc-126">Because this output is sent to your Log Analytics workspace, it works well for demonstrating the viewing and querying of logs.</span><span class="sxs-lookup"><span data-stu-id="475fc-126">Because this output is sent to your Log Analytics workspace, it works well for demonstrating the viewing and querying of logs.</span></span>

### <a name="deploy-with-azure-cli"></a><span data-ttu-id="475fc-127">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="475fc-127">Deploy with Azure CLI</span></span>

<span data-ttu-id="475fc-128">To deploy with the Azure CLI, specify the `--log-analytics-workspace` and `--log-analytics-workspace-key` parameters in the [az container create][az-container-create] command.</span><span class="sxs-lookup"><span data-stu-id="475fc-128">To deploy with the Azure CLI, specify the `--log-analytics-workspace` and `--log-analytics-workspace-key` parameters in the [az container create][az-container-create] command.</span></span> <span data-ttu-id="475fc-129">Replace the two workspace values with the values you obtained in the previous step (and update the resource group name) before running the following command.</span><span class="sxs-lookup"><span data-stu-id="475fc-129">Replace the two workspace values with the values you obtained in the previous step (and update the resource group name) before running the following command.</span></span>

```azurecli-interactive
az container create \
    --resource-group myResourceGroup \
    --name mycontainergroup001 \
    --image fluent/fluentd \
    --log-analytics-workspace <WORKSPACE_ID> \
    --log-analytics-workspace-key <WORKSPACE_KEY>
```

### <a name="deploy-with-yaml"></a><span data-ttu-id="475fc-130">Deploy with YAML</span><span class="sxs-lookup"><span data-stu-id="475fc-130">Deploy with YAML</span></span>

<span data-ttu-id="475fc-131">Use this method if you prefer to deploy container groups with YAML.</span><span class="sxs-lookup"><span data-stu-id="475fc-131">Use this method if you prefer to deploy container groups with YAML.</span></span> <span data-ttu-id="475fc-132">The following YAML defines a container group with a single container.</span><span class="sxs-lookup"><span data-stu-id="475fc-132">The following YAML defines a container group with a single container.</span></span> <span data-ttu-id="475fc-133">Copy the YAML into a new file, then replace `LOG_ANALYTICS_WORKSPACE_ID` and `LOG_ANALYTICS_WORKSPACE_KEY` with the values you obtained in the previous step.</span><span class="sxs-lookup"><span data-stu-id="475fc-133">Copy the YAML into a new file, then replace `LOG_ANALYTICS_WORKSPACE_ID` and `LOG_ANALYTICS_WORKSPACE_KEY` with the values you obtained in the previous step.</span></span> <span data-ttu-id="475fc-134">Save the file as **deploy-aci.yaml**.</span><span class="sxs-lookup"><span data-stu-id="475fc-134">Save the file as **deploy-aci.yaml**.</span></span>

```yaml
apiVersion: 2018-06-01
location: eastus
name: mycontainergroup001
properties:
  containers:
  - name: mycontainer001
    properties:
      environmentVariables: []
      image: fluent/fluentd
      ports: []
      resources:
        requests:
          cpu: 1.0
          memoryInGB: 1.5
  osType: Linux
  restartPolicy: Always
  diagnostics:
    logAnalytics:
      workspaceId: LOG_ANALYTICS_WORKSPACE_ID
      workspaceKey: LOG_ANALYTICS_WORKSPACE_KEY
tags: null
type: Microsoft.ContainerInstance/containerGroups
```

<span data-ttu-id="475fc-135">Next, execute the following command to deploy the container group; replace `myResourceGroup` with a resource group in your subscription (or first create a resource group named "myResourceGroup"):</span><span class="sxs-lookup"><span data-stu-id="475fc-135">Next, execute the following command to deploy the container group; replace `myResourceGroup` with a resource group in your subscription (or first create a resource group named "myResourceGroup"):</span></span>

```azurecli-interactive
az container create --resource-group myResourceGroup --name mycontainergroup001 --file deploy-aci.yaml
```

<span data-ttu-id="475fc-136">You should receive a response from Azure containing deployment details shortly after issuing the command.</span><span class="sxs-lookup"><span data-stu-id="475fc-136">You should receive a response from Azure containing deployment details shortly after issuing the command.</span></span>

## <a name="view-logs-in-log-analytics"></a><span data-ttu-id="475fc-137">View logs in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="475fc-137">View logs in Log Analytics</span></span>

<span data-ttu-id="475fc-138">After you've deployed the container group, it can take several minutes (up to 10) for the first log entries to appear in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="475fc-138">After you've deployed the container group, it can take several minutes (up to 10) for the first log entries to appear in the Azure portal.</span></span> <span data-ttu-id="475fc-139">To view the container group's logs, open your Log Analytics workspace, then:</span><span class="sxs-lookup"><span data-stu-id="475fc-139">To view the container group's logs, open your Log Analytics workspace, then:</span></span>

1. <span data-ttu-id="475fc-140">In the **OMS Workspace** overview, select **Log Search**</span><span class="sxs-lookup"><span data-stu-id="475fc-140">In the **OMS Workspace** overview, select **Log Search**</span></span>
1. <span data-ttu-id="475fc-141">Under **A few more queries to try**, select the **All collected data** link</span><span class="sxs-lookup"><span data-stu-id="475fc-141">Under **A few more queries to try**, select the **All collected data** link</span></span>

<span data-ttu-id="475fc-142">You should see several results displayed by the `search *` query.</span><span class="sxs-lookup"><span data-stu-id="475fc-142">You should see several results displayed by the `search *` query.</span></span> <span data-ttu-id="475fc-143">If at first you don't see any results, wait a few minutes, then select the **RUN** button to execute the query again.</span><span class="sxs-lookup"><span data-stu-id="475fc-143">If at first you don't see any results, wait a few minutes, then select the **RUN** button to execute the query again.</span></span> <span data-ttu-id="475fc-144">By default, log entries are displayed in "List" view--select **Table** to see the log entries in a more condensed format.</span><span class="sxs-lookup"><span data-stu-id="475fc-144">By default, log entries are displayed in "List" view--select **Table** to see the log entries in a more condensed format.</span></span> <span data-ttu-id="475fc-145">You can then expand a row to see the contents of an individual log entry.</span><span class="sxs-lookup"><span data-stu-id="475fc-145">You can then expand a row to see the contents of an individual log entry.</span></span>

![Log Search results in the Azure portal][log-search-01]

## <a name="query-container-logs"></a><span data-ttu-id="475fc-147">Query container logs</span><span class="sxs-lookup"><span data-stu-id="475fc-147">Query container logs</span></span>

<span data-ttu-id="475fc-148">Log Analytics includes an extensive [query language][query_lang] for pulling information from potentially thousands of lines of log output.</span><span class="sxs-lookup"><span data-stu-id="475fc-148">Log Analytics includes an extensive [query language][query_lang] for pulling information from potentially thousands of lines of log output.</span></span>

<span data-ttu-id="475fc-149">The Azure Container Instances logging agent sends entries to the `ContainerInstanceLog_CL` table in your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="475fc-149">The Azure Container Instances logging agent sends entries to the `ContainerInstanceLog_CL` table in your Log Analytics workspace.</span></span> <span data-ttu-id="475fc-150">The basic structure of a query is the source table (`ContainerInstanceLog_CL`) followed by a series of operators separated by the pipe character (`|`).</span><span class="sxs-lookup"><span data-stu-id="475fc-150">The basic structure of a query is the source table (`ContainerInstanceLog_CL`) followed by a series of operators separated by the pipe character (`|`).</span></span> <span data-ttu-id="475fc-151">You can chain several operators to refine the results and perform advanced functions.</span><span class="sxs-lookup"><span data-stu-id="475fc-151">You can chain several operators to refine the results and perform advanced functions.</span></span>

<span data-ttu-id="475fc-152">To see example query results, paste the following query into the query text box (under "Show legacy language converter"), and select the **RUN** button to execute the query.</span><span class="sxs-lookup"><span data-stu-id="475fc-152">To see example query results, paste the following query into the query text box (under "Show legacy language converter"), and select the **RUN** button to execute the query.</span></span> <span data-ttu-id="475fc-153">This query displays all log entries whose "Message" field contains the word "warn":</span><span class="sxs-lookup"><span data-stu-id="475fc-153">This query displays all log entries whose "Message" field contains the word "warn":</span></span>

```query
ContainerInstanceLog_CL
| where Message contains("warn")
```

<span data-ttu-id="475fc-154">More complex queries are also supported.</span><span class="sxs-lookup"><span data-stu-id="475fc-154">More complex queries are also supported.</span></span> <span data-ttu-id="475fc-155">For example, this query displays only those log entries for the "mycontainergroup001" container group generated within the last hour:</span><span class="sxs-lookup"><span data-stu-id="475fc-155">For example, this query displays only those log entries for the "mycontainergroup001" container group generated within the last hour:</span></span>

```query
ContainerInstanceLog_CL
| where (ContainerGroup_s == "mycontainergroup001")
| where (TimeGenerated > ago(1h))
```

## <a name="next-steps"></a><span data-ttu-id="475fc-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="475fc-156">Next steps</span></span>

### <a name="log-analytics"></a><span data-ttu-id="475fc-157">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="475fc-157">Log Analytics</span></span>

<span data-ttu-id="475fc-158">For more information about querying logs and configuring alerts in Azure Log Analytics, see:</span><span class="sxs-lookup"><span data-stu-id="475fc-158">For more information about querying logs and configuring alerts in Azure Log Analytics, see:</span></span>

* [<span data-ttu-id="475fc-159">Understanding log searches in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="475fc-159">Understanding log searches in Log Analytics</span></span>](../log-analytics/log-analytics-log-search.md)
* [<span data-ttu-id="475fc-160">Unified alerts in Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="475fc-160">Unified alerts in Azure Monitor</span></span>](../monitoring-and-diagnostics/monitoring-overview-unified-alerts.md)

### <a name="monitor-container-cpu-and-memory"></a><span data-ttu-id="475fc-161">Monitor container CPU and memory</span><span class="sxs-lookup"><span data-stu-id="475fc-161">Monitor container CPU and memory</span></span>

<span data-ttu-id="475fc-162">For information about monitoring container instance CPU and memory resources, see:</span><span class="sxs-lookup"><span data-stu-id="475fc-162">For information about monitoring container instance CPU and memory resources, see:</span></span>

* <span data-ttu-id="475fc-163">[Monitor container resources in Azure Container Instances](container-instances-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="475fc-163">[Monitor container resources in Azure Container Instances](container-instances-monitor.md).</span></span>

<!-- IMAGES -->
[log-search-01]: ./media/container-instances-log-analytics/portal-query-01.png

<!-- LINKS - External -->
[fluentd]: https://hub.docker.com/r/fluent/fluentd/
[query_lang]: https://docs.loganalytics.io/

<!-- LINKS - Internal -->
[az-container-create]: /cli/azure/container#az-container-create