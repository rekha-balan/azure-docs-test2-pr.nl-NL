---
title: Monitor Azure Kubernetes cluster - Operations Management
description: Monitoring Kubernetes cluster in Azure Container Service using Log Analytics
services: container-service
author: bburns
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 3b014ce4c91d1dc9fae744ef4b528c98f9f787b3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867940"
---
# <a name="monitor-an-azure-container-service-cluster-with-log-analytics"></a><span data-ttu-id="64b9a-103">Monitor an Azure Container Service cluster with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="64b9a-103">Monitor an Azure Container Service cluster with Log Analytics</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

## <a name="prerequisites"></a><span data-ttu-id="64b9a-104">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="64b9a-104">Prerequisites</span></span>
<span data-ttu-id="64b9a-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="64b9a-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="64b9a-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span><span class="sxs-lookup"><span data-stu-id="64b9a-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="64b9a-107">You can test if you have the `az` tool installed by running:</span><span class="sxs-lookup"><span data-stu-id="64b9a-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="64b9a-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="64b9a-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>
<span data-ttu-id="64b9a-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview), which has the `az` Azure cli and `kubectl` tools already installed for you.</span><span class="sxs-lookup"><span data-stu-id="64b9a-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview), which has the `az` Azure cli and `kubectl` tools already installed for you.</span></span>

<span data-ttu-id="64b9a-110">You can test if you have the `kubectl` tool installed by running:</span><span class="sxs-lookup"><span data-stu-id="64b9a-110">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="64b9a-111">If you don't have `kubectl` installed, you can run:</span><span class="sxs-lookup"><span data-stu-id="64b9a-111">If you don't have `kubectl` installed, you can run:</span></span>
```console
$ az acs kubernetes install-cli
```

<span data-ttu-id="64b9a-112">To test if you have kubernetes keys installed in your kubectl tool you can run:</span><span class="sxs-lookup"><span data-stu-id="64b9a-112">To test if you have kubernetes keys installed in your kubectl tool you can run:</span></span>
```console
$ kubectl get nodes
```

<span data-ttu-id="64b9a-113">If the above command errors out, you need to install kubernetes cluster keys into your kubectl tool.</span><span class="sxs-lookup"><span data-stu-id="64b9a-113">If the above command errors out, you need to install kubernetes cluster keys into your kubectl tool.</span></span> <span data-ttu-id="64b9a-114">You can do that with the following command:</span><span class="sxs-lookup"><span data-stu-id="64b9a-114">You can do that with the following command:</span></span>
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-log-analytics"></a><span data-ttu-id="64b9a-115">Monitoring Containers with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="64b9a-115">Monitoring Containers with Log Analytics</span></span>

<span data-ttu-id="64b9a-116">Log Analytics is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span><span class="sxs-lookup"><span data-stu-id="64b9a-116">Log Analytics is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="64b9a-117">Container Solution is a solution in Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span><span class="sxs-lookup"><span data-stu-id="64b9a-117">Container Solution is a solution in Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="64b9a-118">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span><span class="sxs-lookup"><span data-stu-id="64b9a-118">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="64b9a-119">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="64b9a-119">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-log-analytics-on-kubernetes"></a><span data-ttu-id="64b9a-120">Installing Log Analytics on Kubernetes</span><span class="sxs-lookup"><span data-stu-id="64b9a-120">Installing Log Analytics on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="64b9a-121">Obtain your workspace ID and key</span><span class="sxs-lookup"><span data-stu-id="64b9a-121">Obtain your workspace ID and key</span></span>
<span data-ttu-id="64b9a-122">For the Log Analytics agent to talk to the service it needs to be configured with a workspace ID and a workspace key.</span><span class="sxs-lookup"><span data-stu-id="64b9a-122">For the Log Analytics agent to talk to the service it needs to be configured with a workspace ID and a workspace key.</span></span> <span data-ttu-id="64b9a-123">To get the workspace ID and key you need to create an account at <https://mms.microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="64b9a-123">To get the workspace ID and key you need to create an account at <https://mms.microsoft.com>.</span></span>
<span data-ttu-id="64b9a-124">Please follow the steps to create an account.</span><span class="sxs-lookup"><span data-stu-id="64b9a-124">Please follow the steps to create an account.</span></span> <span data-ttu-id="64b9a-125">Once you are done creating the account, you need to obtain your ID and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span><span class="sxs-lookup"><span data-stu-id="64b9a-125">Once you are done creating the account, you need to obtain your ID and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-the-log-analytics-agent-using-a-daemonset"></a><span data-ttu-id="64b9a-126">Install the Log Analytics agent using a DaemonSet</span><span class="sxs-lookup"><span data-stu-id="64b9a-126">Install the Log Analytics agent using a DaemonSet</span></span>
<span data-ttu-id="64b9a-127">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span><span class="sxs-lookup"><span data-stu-id="64b9a-127">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="64b9a-128">They're perfect for running monitoring agents.</span><span class="sxs-lookup"><span data-stu-id="64b9a-128">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="64b9a-129">Here is the [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span><span class="sxs-lookup"><span data-stu-id="64b9a-129">Here is the [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="64b9a-130">Save it to a file named `oms-daemonset.yaml` and replace the place-holder values for `WSID` and `KEY` with your workspace ID and key in the file.</span><span class="sxs-lookup"><span data-stu-id="64b9a-130">Save it to a file named `oms-daemonset.yaml` and replace the place-holder values for `WSID` and `KEY` with your workspace ID and key in the file.</span></span>

<span data-ttu-id="64b9a-131">Once you have added your workspace ID and key to the DaemonSet configuration, you can install the Log Analytics agent on your cluster with the `kubectl` command-line tool:</span><span class="sxs-lookup"><span data-stu-id="64b9a-131">Once you have added your workspace ID and key to the DaemonSet configuration, you can install the Log Analytics agent on your cluster with the `kubectl` command-line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-the-log-analytics-agent-using-a-kubernetes-secret"></a><span data-ttu-id="64b9a-132">Installing the Log Analytics agent using a Kubernetes Secret</span><span class="sxs-lookup"><span data-stu-id="64b9a-132">Installing the Log Analytics agent using a Kubernetes Secret</span></span>
<span data-ttu-id="64b9a-133">To protect your Log Analytics workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span><span class="sxs-lookup"><span data-stu-id="64b9a-133">To protect your Log Analytics workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span></span>

 - <span data-ttu-id="64b9a-134">Copy the script, secret template file, and the DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on the same directory.</span><span class="sxs-lookup"><span data-stu-id="64b9a-134">Copy the script, secret template file, and the DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on the same directory.</span></span>
      - <span data-ttu-id="64b9a-135">secret generating script - secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="64b9a-135">secret generating script - secret-gen.sh</span></span>
      - <span data-ttu-id="64b9a-136">secret template - secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="64b9a-136">secret template - secret-template.yaml</span></span>
   - <span data-ttu-id="64b9a-137">DaemonSet YAML file - omsagent-ds-secrets.yaml</span><span class="sxs-lookup"><span data-stu-id="64b9a-137">DaemonSet YAML file - omsagent-ds-secrets.yaml</span></span>
 - <span data-ttu-id="64b9a-138">Run the script.</span><span class="sxs-lookup"><span data-stu-id="64b9a-138">Run the script.</span></span> <span data-ttu-id="64b9a-139">The script will ask for the Log Analytics Workspace ID and Primary Key.</span><span class="sxs-lookup"><span data-stu-id="64b9a-139">The script will ask for the Log Analytics Workspace ID and Primary Key.</span></span> <span data-ttu-id="64b9a-140">Insert that and the script will create a secret yaml file so you can run it.</span><span class="sxs-lookup"><span data-stu-id="64b9a-140">Insert that and the script will create a secret yaml file so you can run it.</span></span>
   ```
   #> sudo bash ./secret-gen.sh
   ```

   - <span data-ttu-id="64b9a-141">Create the secrets pod by running the following: ``` kubectl create -f omsagentsecret.yaml ```</span><span class="sxs-lookup"><span data-stu-id="64b9a-141">Create the secrets pod by running the following: ``` kubectl create -f omsagentsecret.yaml ```</span></span>

   - <span data-ttu-id="64b9a-142">To check, run the following:</span><span class="sxs-lookup"><span data-stu-id="64b9a-142">To check, run the following:</span></span>

   ```
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes
   ```

  - <span data-ttu-id="64b9a-143">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="64b9a-143">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

### <a name="conclusion"></a><span data-ttu-id="64b9a-144">Conclusion</span><span class="sxs-lookup"><span data-stu-id="64b9a-144">Conclusion</span></span>
<span data-ttu-id="64b9a-145">That's it!</span><span class="sxs-lookup"><span data-stu-id="64b9a-145">That's it!</span></span> <span data-ttu-id="64b9a-146">After a few minutes, you should be able to see data flowing to your Log Analytics dashboard.</span><span class="sxs-lookup"><span data-stu-id="64b9a-146">After a few minutes, you should be able to see data flowing to your Log Analytics dashboard.</span></span>
