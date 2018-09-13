---
title: Monitor Azure Kubernetes cluster - Operations Management | Microsoft Docs
description: Monitoring Kubernetes cluster in Azure Container Service using Microsoft Operations Management Suite
services: container-service
documentationcenter: ''
author: bburns
manager: timlt
editor: ''
tags: acs, azure-container-service, kubernetes
keywords: ''
ms.assetid: ''
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.openlocfilehash: a3ebc9b429a5d11191e37aa7d8b5706e3c44b36c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562816"
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a><span data-ttu-id="5d394-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="5d394-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d394-104">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5d394-104">Prerequisites</span></span>
<span data-ttu-id="5d394-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="5d394-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="5d394-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span><span class="sxs-lookup"><span data-stu-id="5d394-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="5d394-107">You can test if you have the `az` tool installed by running:</span><span class="sxs-lookup"><span data-stu-id="5d394-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="5d394-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="5d394-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="5d394-109">You can test if you have the `kubectl` tool installed by running:</span><span class="sxs-lookup"><span data-stu-id="5d394-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="5d394-110">If you don't have `kubectl` installed, you can run:</span><span class="sxs-lookup"><span data-stu-id="5d394-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a><span data-ttu-id="5d394-111">Monitoring Containers with Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="5d394-111">Monitoring Containers with Operations Management Suite (OMS)</span></span>

<span data-ttu-id="5d394-112">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span><span class="sxs-lookup"><span data-stu-id="5d394-112">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="5d394-113">Container Solution is a solution in OMS Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span><span class="sxs-lookup"><span data-stu-id="5d394-113">Container Solution is a solution in OMS Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="5d394-114">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span><span class="sxs-lookup"><span data-stu-id="5d394-114">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="5d394-115">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="5d394-115">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-oms-on-kubernetes"></a><span data-ttu-id="5d394-116">Installing OMS on Kubernetes</span><span class="sxs-lookup"><span data-stu-id="5d394-116">Installing OMS on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="5d394-117">Obtain your workspace ID and key</span><span class="sxs-lookup"><span data-stu-id="5d394-117">Obtain your workspace ID and key</span></span>
<span data-ttu-id="5d394-118">For the OMS agent to talk to the service it needs to be configured with a workspace id and a workspace key.</span><span class="sxs-lookup"><span data-stu-id="5d394-118">For the OMS agent to talk to the service it needs to be configured with a workspace id and a workspace key.</span></span> <span data-ttu-id="5d394-119">To get the workspace id and key you need to create an OMS account at <https://mms.microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="5d394-119">To get the workspace id and key you need to create an OMS account at <https://mms.microsoft.com>.</span></span>
<span data-ttu-id="5d394-120">Please follow the steps to create an account.</span><span class="sxs-lookup"><span data-stu-id="5d394-120">Please follow the steps to create an account.</span></span> <span data-ttu-id="5d394-121">Once you are done creating the account, you need to obtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span><span class="sxs-lookup"><span data-stu-id="5d394-121">Once you are done creating the account, you need to obtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-oms/image5.png)

### <a name="install-the-oms-agent-using-a-daemonset"></a><span data-ttu-id="5d394-122">Install the OMS agent using a DaemonSet</span><span class="sxs-lookup"><span data-stu-id="5d394-122">Install the OMS agent using a DaemonSet</span></span>
<span data-ttu-id="5d394-123">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span><span class="sxs-lookup"><span data-stu-id="5d394-123">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="5d394-124">They're perfect for running monitoring agents.</span><span class="sxs-lookup"><span data-stu-id="5d394-124">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="5d394-125">Here is the [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span><span class="sxs-lookup"><span data-stu-id="5d394-125">Here is the [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="5d394-126">Save it to a file named `oms-daemonset.yaml` and replace the place-holder values for `WSID` and `KEY` with your workspace id and key in the file.</span><span class="sxs-lookup"><span data-stu-id="5d394-126">Save it to a file named `oms-daemonset.yaml` and replace the place-holder values for `WSID` and `KEY` with your workspace id and key in the file.</span></span>

<span data-ttu-id="5d394-127">Once you have added your workspace ID and key to the DaemonSet configuration, you can install the OMS agent on your cluster with the `kubectl` command line tool:</span><span class="sxs-lookup"><span data-stu-id="5d394-127">Once you have added your workspace ID and key to the DaemonSet configuration, you can install the OMS agent on your cluster with the `kubectl` command line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="conclusion"></a><span data-ttu-id="5d394-128">Conclusion</span><span class="sxs-lookup"><span data-stu-id="5d394-128">Conclusion</span></span>
<span data-ttu-id="5d394-129">That's it!</span><span class="sxs-lookup"><span data-stu-id="5d394-129">That's it!</span></span> <span data-ttu-id="5d394-130">After a few minutes, you should be able to see data flowing to your OMS dashboard.</span><span class="sxs-lookup"><span data-stu-id="5d394-130">After a few minutes, you should be able to see data flowing to your OMS dashboard.</span></span>


