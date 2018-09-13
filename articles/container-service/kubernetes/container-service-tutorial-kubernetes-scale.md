---
title: Azure Container Service tutorial - Scale Application
description: Azure Container Service tutorial - Scale Application
services: container-service
author: dlepow
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 09/14/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 792d9b1409b9571474f47da4940724df7a764d82
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871516"
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a><span data-ttu-id="6a38e-103">Scale Kubernetes pods and Kubernetes infrastructure</span><span class="sxs-lookup"><span data-stu-id="6a38e-103">Scale Kubernetes pods and Kubernetes infrastructure</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

<span data-ttu-id="6a38e-104">If you've been following the tutorials, you have a working Kubernetes cluster in Azure Container Service and you deployed the Azure Voting app.</span><span class="sxs-lookup"><span data-stu-id="6a38e-104">If you've been following the tutorials, you have a working Kubernetes cluster in Azure Container Service and you deployed the Azure Voting app.</span></span> 

<span data-ttu-id="6a38e-105">In this tutorial, part five of seven, you scale out the pods in the app and try pod autoscaling.</span><span class="sxs-lookup"><span data-stu-id="6a38e-105">In this tutorial, part five of seven, you scale out the pods in the app and try pod autoscaling.</span></span> <span data-ttu-id="6a38e-106">You also learn how to scale the number of Azure VM agent nodes to change the cluster's capacity for hosting workloads.</span><span class="sxs-lookup"><span data-stu-id="6a38e-106">You also learn how to scale the number of Azure VM agent nodes to change the cluster's capacity for hosting workloads.</span></span> <span data-ttu-id="6a38e-107">Tasks completed include:</span><span class="sxs-lookup"><span data-stu-id="6a38e-107">Tasks completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6a38e-108">Manually scaling Kubernetes pods</span><span class="sxs-lookup"><span data-stu-id="6a38e-108">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="6a38e-109">Configuring Autoscale pods running the app front end</span><span class="sxs-lookup"><span data-stu-id="6a38e-109">Configuring Autoscale pods running the app front end</span></span>
> * <span data-ttu-id="6a38e-110">Scale the Kubernetes Azure agent nodes</span><span class="sxs-lookup"><span data-stu-id="6a38e-110">Scale the Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="6a38e-111">In subsequent tutorials, the Azure Vote application is updated, and Log Analytics is configured to monitor the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="6a38e-111">In subsequent tutorials, the Azure Vote application is updated, and Log Analytics is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6a38e-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="6a38e-112">Before you begin</span></span>

<span data-ttu-id="6a38e-113">In previous tutorials, an application was packaged into a container image, this image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span><span class="sxs-lookup"><span data-stu-id="6a38e-113">In previous tutorials, an application was packaged into a container image, this image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="6a38e-114">The application was then run on the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="6a38e-114">The application was then run on the Kubernetes cluster.</span></span> 

<span data-ttu-id="6a38e-115">If you have not done these steps, and would like to follow along, return to the [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="6a38e-115">If you have not done these steps, and would like to follow along, return to the [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="manually-scale-pods"></a><span data-ttu-id="6a38e-116">Manually scale pods</span><span class="sxs-lookup"><span data-stu-id="6a38e-116">Manually scale pods</span></span>

<span data-ttu-id="6a38e-117">Thus far, the Azure Vote front-end and Redis instance have been deployed, each with a single replica.</span><span class="sxs-lookup"><span data-stu-id="6a38e-117">Thus far, the Azure Vote front-end and Redis instance have been deployed, each with a single replica.</span></span> <span data-ttu-id="6a38e-118">To verify, run the [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command.</span><span class="sxs-lookup"><span data-stu-id="6a38e-118">To verify, run the [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command.</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="6a38e-119">Output:</span><span class="sxs-lookup"><span data-stu-id="6a38e-119">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

<span data-ttu-id="6a38e-120">Manually change the number of pods in the `azure-vote-front` deployment using the [kubectl scale](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#scale) command.</span><span class="sxs-lookup"><span data-stu-id="6a38e-120">Manually change the number of pods in the `azure-vote-front` deployment using the [kubectl scale](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#scale) command.</span></span> <span data-ttu-id="6a38e-121">This example increases the number to 5.</span><span class="sxs-lookup"><span data-stu-id="6a38e-121">This example increases the number to 5.</span></span>

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

<span data-ttu-id="6a38e-122">Run [kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) to verify that Kubernetes is creating the pods.</span><span class="sxs-lookup"><span data-stu-id="6a38e-122">Run [kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) to verify that Kubernetes is creating the pods.</span></span> <span data-ttu-id="6a38e-123">After a minute or so, the additional pods are running:</span><span class="sxs-lookup"><span data-stu-id="6a38e-123">After a minute or so, the additional pods are running:</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="6a38e-124">Output:</span><span class="sxs-lookup"><span data-stu-id="6a38e-124">Output:</span></span>

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a><span data-ttu-id="6a38e-125">Autoscale pods</span><span class="sxs-lookup"><span data-stu-id="6a38e-125">Autoscale pods</span></span>

<span data-ttu-id="6a38e-126">Kubernetes supports [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) to adjust the number of pods in a deployment depending on CPU utilization or other select metrics.</span><span class="sxs-lookup"><span data-stu-id="6a38e-126">Kubernetes supports [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) to adjust the number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> 

<span data-ttu-id="6a38e-127">To use the autoscaler, your pods must have CPU requests and limits defined.</span><span class="sxs-lookup"><span data-stu-id="6a38e-127">To use the autoscaler, your pods must have CPU requests and limits defined.</span></span> <span data-ttu-id="6a38e-128">In the `azure-vote-front` deployment, the front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span><span class="sxs-lookup"><span data-stu-id="6a38e-128">In the `azure-vote-front` deployment, the front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span></span> <span data-ttu-id="6a38e-129">The settings look like:</span><span class="sxs-lookup"><span data-stu-id="6a38e-129">The settings look like:</span></span>

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

<span data-ttu-id="6a38e-130">The following example uses the [kubectl autoscale](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#autoscale) command to autoscale the number of pods in the `azure-vote-front` deployment.</span><span class="sxs-lookup"><span data-stu-id="6a38e-130">The following example uses the [kubectl autoscale](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#autoscale) command to autoscale the number of pods in the `azure-vote-front` deployment.</span></span> <span data-ttu-id="6a38e-131">Here, if CPU utilization exceeds 50%, the autoscaler increases the pods to a maximum of 10.</span><span class="sxs-lookup"><span data-stu-id="6a38e-131">Here, if CPU utilization exceeds 50%, the autoscaler increases the pods to a maximum of 10.</span></span>


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

<span data-ttu-id="6a38e-132">To see the status of the autoscaler, run the following command:</span><span class="sxs-lookup"><span data-stu-id="6a38e-132">To see the status of the autoscaler, run the following command:</span></span>

```azurecli-interactive
kubectl get hpa
```

<span data-ttu-id="6a38e-133">Output:</span><span class="sxs-lookup"><span data-stu-id="6a38e-133">Output:</span></span>

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

<span data-ttu-id="6a38e-134">After a few minutes, with minimal load on the Azure Vote app, the number of pod replicas decreases automatically to 3.</span><span class="sxs-lookup"><span data-stu-id="6a38e-134">After a few minutes, with minimal load on the Azure Vote app, the number of pod replicas decreases automatically to 3.</span></span>

## <a name="scale-the-agents"></a><span data-ttu-id="6a38e-135">Scale the agents</span><span class="sxs-lookup"><span data-stu-id="6a38e-135">Scale the agents</span></span>

<span data-ttu-id="6a38e-136">If you created your Kubernetes cluster using default commands in the previous tutorial, it has three agent nodes.</span><span class="sxs-lookup"><span data-stu-id="6a38e-136">If you created your Kubernetes cluster using default commands in the previous tutorial, it has three agent nodes.</span></span> <span data-ttu-id="6a38e-137">You can adjust the number of agents manually if you plan more or fewer container workloads on your cluster.</span><span class="sxs-lookup"><span data-stu-id="6a38e-137">You can adjust the number of agents manually if you plan more or fewer container workloads on your cluster.</span></span> <span data-ttu-id="6a38e-138">Use the [az acs scale](/cli/azure/acs#az-acs-scale) command, and specify the number of agents with the `--new-agent-count` parameter.</span><span class="sxs-lookup"><span data-stu-id="6a38e-138">Use the [az acs scale](/cli/azure/acs#az-acs-scale) command, and specify the number of agents with the `--new-agent-count` parameter.</span></span>

<span data-ttu-id="6a38e-139">The following example increases the number of agent nodes to 4 in the Kubernetes cluster named *myK8sCluster*.</span><span class="sxs-lookup"><span data-stu-id="6a38e-139">The following example increases the number of agent nodes to 4 in the Kubernetes cluster named *myK8sCluster*.</span></span> <span data-ttu-id="6a38e-140">The command takes a couple of minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="6a38e-140">The command takes a couple of minutes to complete.</span></span>

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

<span data-ttu-id="6a38e-141">The command output shows the number of agent nodes in the value of `agentPoolProfiles:count`:</span><span class="sxs-lookup"><span data-stu-id="6a38e-141">The command output shows the number of agent nodes in the value of `agentPoolProfiles:count`:</span></span>

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a><span data-ttu-id="6a38e-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a38e-142">Next steps</span></span>

<span data-ttu-id="6a38e-143">In this tutorial, you used different scaling features in your Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="6a38e-143">In this tutorial, you used different scaling features in your Kubernetes cluster.</span></span> <span data-ttu-id="6a38e-144">Tasks covered included:</span><span class="sxs-lookup"><span data-stu-id="6a38e-144">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6a38e-145">Manually scaling Kubernetes pods</span><span class="sxs-lookup"><span data-stu-id="6a38e-145">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="6a38e-146">Configuring Autoscale pods running the app front end</span><span class="sxs-lookup"><span data-stu-id="6a38e-146">Configuring Autoscale pods running the app front end</span></span>
> * <span data-ttu-id="6a38e-147">Scale the Kubernetes Azure agent nodes</span><span class="sxs-lookup"><span data-stu-id="6a38e-147">Scale the Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="6a38e-148">Advance to the next tutorial to learn about updating application in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6a38e-148">Advance to the next tutorial to learn about updating application in Kubernetes.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6a38e-149">Update an application in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6a38e-149">Update an application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-app-update.md)

