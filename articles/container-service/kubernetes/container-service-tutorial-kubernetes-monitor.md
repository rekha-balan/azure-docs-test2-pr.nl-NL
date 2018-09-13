---
title: Azure Container Service tutorial - Monitor Kubernetes
description: Azure Container Service tutorial - Monitor Kubernetes with Log Analytics
services: container-service
author: neilpeterson
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 04/05/2018
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 17398a9f74e40a7d513912d654fa609d9837d805
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864684"
---
# <a name="monitor-a-kubernetes-cluster-with-log-analytics"></a><span data-ttu-id="2ce06-103">Monitor a Kubernetes cluster with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2ce06-103">Monitor a Kubernetes cluster with Log Analytics</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

<span data-ttu-id="2ce06-104">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span><span class="sxs-lookup"><span data-stu-id="2ce06-104">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span></span>

<span data-ttu-id="2ce06-105">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span><span class="sxs-lookup"><span data-stu-id="2ce06-105">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span></span> <span data-ttu-id="2ce06-106">In this tutorial, you monitor your Kubernetes cluster by using the Containers solution in [Log Analytics](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span><span class="sxs-lookup"><span data-stu-id="2ce06-106">In this tutorial, you monitor your Kubernetes cluster by using the Containers solution in [Log Analytics](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span></span> <span data-ttu-id="2ce06-107">(The Containers solution is in preview.)</span><span class="sxs-lookup"><span data-stu-id="2ce06-107">(The Containers solution is in preview.)</span></span>

<span data-ttu-id="2ce06-108">This tutorial, part seven of seven, covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="2ce06-108">This tutorial, part seven of seven, covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2ce06-109">Get Log Analytics Workspace settings</span><span class="sxs-lookup"><span data-stu-id="2ce06-109">Get Log Analytics Workspace settings</span></span>
> * <span data-ttu-id="2ce06-110">Set up Log Analytics agents on the Kubernetes nodes</span><span class="sxs-lookup"><span data-stu-id="2ce06-110">Set up Log Analytics agents on the Kubernetes nodes</span></span>
> * <span data-ttu-id="2ce06-111">Access monitoring information in the Log Analytics portal or Azure portal</span><span class="sxs-lookup"><span data-stu-id="2ce06-111">Access monitoring information in the Log Analytics portal or Azure portal</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2ce06-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="2ce06-112">Before you begin</span></span>

<span data-ttu-id="2ce06-113">In previous tutorials, an application was packaged into container images, these images uploaded to Azure Container Registry, and a Kubernetes cluster created.</span><span class="sxs-lookup"><span data-stu-id="2ce06-113">In previous tutorials, an application was packaged into container images, these images uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span>

<span data-ttu-id="2ce06-114">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="2ce06-114">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

## <a name="get-workspace-settings"></a><span data-ttu-id="2ce06-115">Get Workspace settings</span><span class="sxs-lookup"><span data-stu-id="2ce06-115">Get Workspace settings</span></span>

<span data-ttu-id="2ce06-116">When you can access the [Log Analytics portal](https://mms.microsoft.com), go to **Settings** > **Connected Sources** > **Linux Servers**.</span><span class="sxs-lookup"><span data-stu-id="2ce06-116">When you can access the [Log Analytics portal](https://mms.microsoft.com), go to **Settings** > **Connected Sources** > **Linux Servers**.</span></span> <span data-ttu-id="2ce06-117">There, you can find the *Workspace ID* and a primary or secondary *Workspace Key*.</span><span class="sxs-lookup"><span data-stu-id="2ce06-117">There, you can find the *Workspace ID* and a primary or secondary *Workspace Key*.</span></span> <span data-ttu-id="2ce06-118">Take note of these values, which you need to set up Log Analytics agents on the cluster.</span><span class="sxs-lookup"><span data-stu-id="2ce06-118">Take note of these values, which you need to set up Log Analytics agents on the cluster.</span></span>

## <a name="create-kubernetes-secret"></a><span data-ttu-id="2ce06-119">Create Kubernetes secret</span><span class="sxs-lookup"><span data-stu-id="2ce06-119">Create Kubernetes secret</span></span>

<span data-ttu-id="2ce06-120">Store the Log Analytics workspace settings in a Kubernetes secret named `omsagent-secret` using the [kubectl create secret][kubectl-create-secret] command.</span><span class="sxs-lookup"><span data-stu-id="2ce06-120">Store the Log Analytics workspace settings in a Kubernetes secret named `omsagent-secret` using the [kubectl create secret][kubectl-create-secret] command.</span></span> <span data-ttu-id="2ce06-121">Update `WORKSPACE_ID` with your Log Analytics workspace ID and `WORKSPACE_KEY` with the workspace key.</span><span class="sxs-lookup"><span data-stu-id="2ce06-121">Update `WORKSPACE_ID` with your Log Analytics workspace ID and `WORKSPACE_KEY` with the workspace key.</span></span>

```console
kubectl create secret generic omsagent-secret --from-literal=WSID=WORKSPACE_ID --from-literal=KEY=WORKSPACE_KEY
```

## <a name="set-up-log-analytics-agents"></a><span data-ttu-id="2ce06-122">Set up Log Analytics agents</span><span class="sxs-lookup"><span data-stu-id="2ce06-122">Set up Log Analytics agents</span></span>

<span data-ttu-id="2ce06-123">The following Kubernetes manifest file can be used to configure the container monitoring agents on a Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="2ce06-123">The following Kubernetes manifest file can be used to configure the container monitoring agents on a Kubernetes cluster.</span></span> <span data-ttu-id="2ce06-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span><span class="sxs-lookup"><span data-stu-id="2ce06-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span></span>

<span data-ttu-id="2ce06-125">Save the following text to a file named `oms-daemonset.yaml`.</span><span class="sxs-lookup"><span data-stu-id="2ce06-125">Save the following text to a file named `oms-daemonset.yaml`.</span></span>

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: 1.4.3-174
    dockerProviderVersion: 1.0.0-30
  spec:
   containers:
     - name: omsagent
       image: "microsoft/oms"
       imagePullPolicy: Always
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log
          name: host-log
        - mountPath: /etc/omsagent-secret
          name: omsagent-secret
          readOnly: true
        - mountPath: /var/lib/docker/containers
          name: containerlog-path
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   nodeSelector:
    beta.kubernetes.io/os: linux
   # Tolerate a NoSchedule taint on master that ACS Engine sets.
   tolerations:
    - key: "node-role.kubernetes.io/master"
      operator: "Equal"
      value: "true"
      effect: "NoSchedule"
   volumes:
    - name: docker-sock
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
    - name: omsagent-secret
      secret:
       secretName: omsagent-secret
    - name: containerlog-path
      hostPath:
       path: /var/lib/docker/containers
```

<span data-ttu-id="2ce06-126">Create the DaemonSet with the following command:</span><span class="sxs-lookup"><span data-stu-id="2ce06-126">Create the DaemonSet with the following command:</span></span>

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

<span data-ttu-id="2ce06-127">To see that the DaemonSet is created, run:</span><span class="sxs-lookup"><span data-stu-id="2ce06-127">To see that the DaemonSet is created, run:</span></span>

```azurecli-interactive
kubectl get daemonset
```

<span data-ttu-id="2ce06-128">Output is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="2ce06-128">Output is similar to the following:</span></span>

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

<span data-ttu-id="2ce06-129">After the agents are running, it takes several minutes for Log Analytics to ingest and process the data.</span><span class="sxs-lookup"><span data-stu-id="2ce06-129">After the agents are running, it takes several minutes for Log Analytics to ingest and process the data.</span></span>

## <a name="access-monitoring-data"></a><span data-ttu-id="2ce06-130">Access monitoring data</span><span class="sxs-lookup"><span data-stu-id="2ce06-130">Access monitoring data</span></span>

<span data-ttu-id="2ce06-131">View and analyze the container monitoring data with the [Container solution](../../log-analytics/log-analytics-containers.md) in either the Log Analytics portal or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2ce06-131">View and analyze the container monitoring data with the [Container solution](../../log-analytics/log-analytics-containers.md) in either the Log Analytics portal or the Azure portal.</span></span>

<span data-ttu-id="2ce06-132">To install the Container solution using the [Log Analytics portal](https://mms.microsoft.com), go to **Solutions Gallery**.</span><span class="sxs-lookup"><span data-stu-id="2ce06-132">To install the Container solution using the [Log Analytics portal](https://mms.microsoft.com), go to **Solutions Gallery**.</span></span> <span data-ttu-id="2ce06-133">Then add **Container Solution**.</span><span class="sxs-lookup"><span data-stu-id="2ce06-133">Then add **Container Solution**.</span></span> <span data-ttu-id="2ce06-134">Alternatively, add the Containers solution from the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span><span class="sxs-lookup"><span data-stu-id="2ce06-134">Alternatively, add the Containers solution from the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span></span>

<span data-ttu-id="2ce06-135">In the Log Analytics portal, look for a **Containers** summary tile on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="2ce06-135">In the Log Analytics portal, look for a **Containers** summary tile on the dashboard.</span></span> <span data-ttu-id="2ce06-136">Click the tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span><span class="sxs-lookup"><span data-stu-id="2ce06-136">Click the tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span></span> <span data-ttu-id="2ce06-137">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="2ce06-137">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span></span>

![Containers dashboard in OMS portal](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

<span data-ttu-id="2ce06-139">Similarly, in the Azure portal, go to **Log Analytics** and select your workspace name.</span><span class="sxs-lookup"><span data-stu-id="2ce06-139">Similarly, in the Azure portal, go to **Log Analytics** and select your workspace name.</span></span> <span data-ttu-id="2ce06-140">To see the **Containers** summary tile, click **Solutions** > **Containers**.</span><span class="sxs-lookup"><span data-stu-id="2ce06-140">To see the **Containers** summary tile, click **Solutions** > **Containers**.</span></span> <span data-ttu-id="2ce06-141">To see details, click the tile.</span><span class="sxs-lookup"><span data-stu-id="2ce06-141">To see details, click the tile.</span></span>

<span data-ttu-id="2ce06-142">See the [Azure Log Analytics documentation](../../log-analytics/index.yml) for detailed guidance on querying and analyzing monitoring data.</span><span class="sxs-lookup"><span data-stu-id="2ce06-142">See the [Azure Log Analytics documentation](../../log-analytics/index.yml) for detailed guidance on querying and analyzing monitoring data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ce06-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="2ce06-143">Next steps</span></span>

<span data-ttu-id="2ce06-144">In this tutorial, you monitored your Kubernetes cluster with Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2ce06-144">In this tutorial, you monitored your Kubernetes cluster with Log Analytics.</span></span> <span data-ttu-id="2ce06-145">Tasks covered included:</span><span class="sxs-lookup"><span data-stu-id="2ce06-145">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2ce06-146">Get Log Analytics Workspace settings</span><span class="sxs-lookup"><span data-stu-id="2ce06-146">Get Log Analytics Workspace settings</span></span>
> * <span data-ttu-id="2ce06-147">Set up Log Analytics agents on the Kubernetes nodes</span><span class="sxs-lookup"><span data-stu-id="2ce06-147">Set up Log Analytics agents on the Kubernetes nodes</span></span>
> * <span data-ttu-id="2ce06-148">Access monitoring information in the Log Analytics portal or Azure portal</span><span class="sxs-lookup"><span data-stu-id="2ce06-148">Access monitoring information in the Log Analytics portal or Azure portal</span></span>


<span data-ttu-id="2ce06-149">Follow this link to see pre-built script samples for Container Service.</span><span class="sxs-lookup"><span data-stu-id="2ce06-149">Follow this link to see pre-built script samples for Container Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2ce06-150">Azure Container Service script samples</span><span class="sxs-lookup"><span data-stu-id="2ce06-150">Azure Container Service script samples</span></span>](cli-samples.md)
