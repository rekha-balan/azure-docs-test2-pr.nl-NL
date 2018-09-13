---
title: View kubelet logs in Azure Kubernetes Service (AKS)
description: How to view troubleshooting information in the kubelet logs from Azure Kubernetes Service (AKS) nodes
services: container-service
author: iainfoulds
ms.service: container-service
ms.topic: article
ms.date: 08/21/2018
ms.author: iainfou
ms.openlocfilehash: aeab24685f3663ba2c50205344d33db3d34676c2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868676"
---
# <a name="get-kubelet-logs-from-azure-kubernetes-service-aks-cluster-nodes"></a><span data-ttu-id="cc6c8-103">Get kubelet logs from Azure Kubernetes Service (AKS) cluster nodes</span><span class="sxs-lookup"><span data-stu-id="cc6c8-103">Get kubelet logs from Azure Kubernetes Service (AKS) cluster nodes</span></span>

<span data-ttu-id="cc6c8-104">Occasionally, you may need to get *kubelet* logs from an Azure Kubernetes Service (AKS) node for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="cc6c8-104">Occasionally, you may need to get *kubelet* logs from an Azure Kubernetes Service (AKS) node for troubleshooting purposes.</span></span> <span data-ttu-id="cc6c8-105">This article shows you how you can use `journalctl` to view the *kubelet* logs.</span><span class="sxs-lookup"><span data-stu-id="cc6c8-105">This article shows you how you can use `journalctl` to view the *kubelet* logs.</span></span>

## <a name="create-an-ssh-connection"></a><span data-ttu-id="cc6c8-106">Create an SSH connection</span><span class="sxs-lookup"><span data-stu-id="cc6c8-106">Create an SSH connection</span></span>

<span data-ttu-id="cc6c8-107">First, create an SSH connection with the node on which you need to view *kubelet* logs.</span><span class="sxs-lookup"><span data-stu-id="cc6c8-107">First, create an SSH connection with the node on which you need to view *kubelet* logs.</span></span> <span data-ttu-id="cc6c8-108">This operation is detailed in the [SSH into Azure Kubernetes Service (AKS) cluster nodes][aks-ssh] document.</span><span class="sxs-lookup"><span data-stu-id="cc6c8-108">This operation is detailed in the [SSH into Azure Kubernetes Service (AKS) cluster nodes][aks-ssh] document.</span></span>

## <a name="get-kubelet-logs"></a><span data-ttu-id="cc6c8-109">Get kubelet logs</span><span class="sxs-lookup"><span data-stu-id="cc6c8-109">Get kubelet logs</span></span>

<span data-ttu-id="cc6c8-110">Once you have connected to the node, run the following command to pull the *kubelet* logs:</span><span class="sxs-lookup"><span data-stu-id="cc6c8-110">Once you have connected to the node, run the following command to pull the *kubelet* logs:</span></span>

```console
sudo journalctl -u kubelet -o cat
```

<span data-ttu-id="cc6c8-111">The following sample output shows the *kubelet* log data:</span><span class="sxs-lookup"><span data-stu-id="cc6c8-111">The following sample output shows the *kubelet* log data:</span></span>

```
I0508 12:26:17.905042    8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-11482510-0"
I0508 12:26:27.943494    8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-11482510-0"
I0508 12:26:28.920125    8672 server.go:796] GET /stats/summary: (10.370874ms) 200 [[Ruby] 10.244.0.2:52292]
I0508 12:26:37.964650    8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-11482510-0"
I0508 12:26:47.996449    8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-11482510-0"
I0508 12:26:58.019746    8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-11482510-0"
I0508 12:27:05.107680    8672 server.go:796] GET /stats/summary/: (24.853838ms) 200 [[Go-http-client/1.1] 10.244.0.3:44660]
I0508 12:27:08.041736    8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-11482510-0"
I0508 12:27:18.068505    8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-11482510-0"
I0508 12:27:28.094889    8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-11482510-0"
I0508 12:27:38.121346    8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-11482510-0"
I0508 12:27:44.015205    8672 server.go:796] GET /stats/summary: (30.236824ms) 200 [[Ruby] 10.244.0.2:52588]
I0508 12:27:48.145640    8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-11482510-0"
I0508 12:27:58.178534    8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-11482510-0"
I0508 12:28:05.040375    8672 server.go:796] GET /stats/summary/: (27.78503ms) 200 [[Go-http-client/1.1] 10.244.0.3:44660]
I0508 12:28:08.214158    8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-11482510-0"
I0508 12:28:18.242160    8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-11482510-0"
I0508 12:28:28.274408    8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-11482510-0"
I0508 12:28:38.296074    8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-11482510-0"
I0508 12:28:48.321952    8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-11482510-0"
I0508 12:28:58.344656    8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-11482510-0"
```

## <a name="next-steps"></a><span data-ttu-id="cc6c8-112">Next steps</span><span class="sxs-lookup"><span data-stu-id="cc6c8-112">Next steps</span></span>

<span data-ttu-id="cc6c8-113">If you need additional troubleshooting information from the Kubernetes master, see [view Kubernetes master node logs in AKS][aks-master-logs].</span><span class="sxs-lookup"><span data-stu-id="cc6c8-113">If you need additional troubleshooting information from the Kubernetes master, see [view Kubernetes master node logs in AKS][aks-master-logs].</span></span>

<!-- LINKS - internal -->
[aks-ssh]: ssh.md
[aks-master-logs]: view-master-logs.md
