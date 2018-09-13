---
title: Kubernetes on Azure tutorial  - Scale Application
description: In this Azure Kubernetes Service (AKS) tutorial, you learn how to scale nodes and pods in Kubernetes, and implement horizontal pod autoscaling.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 08/14/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 5ffe7b4c7830500e5eeeeb61c57730d9a0d9df47
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856205"
---
# <a name="tutorial-scale-applications-in-azure-kubernetes-service-aks"></a><span data-ttu-id="96e15-103">Tutorial: Scale applications in Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="96e15-103">Tutorial: Scale applications in Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="96e15-104">If you've been following the tutorials, you have a working Kubernetes cluster in AKS and you deployed the Azure Voting app.</span><span class="sxs-lookup"><span data-stu-id="96e15-104">If you've been following the tutorials, you have a working Kubernetes cluster in AKS and you deployed the Azure Voting app.</span></span> <span data-ttu-id="96e15-105">In this tutorial, part five of seven, you scale out the pods in the app and try pod autoscaling.</span><span class="sxs-lookup"><span data-stu-id="96e15-105">In this tutorial, part five of seven, you scale out the pods in the app and try pod autoscaling.</span></span> <span data-ttu-id="96e15-106">You also learn how to scale the number of Azure VM nodes to change the cluster's capacity for hosting workloads.</span><span class="sxs-lookup"><span data-stu-id="96e15-106">You also learn how to scale the number of Azure VM nodes to change the cluster's capacity for hosting workloads.</span></span> <span data-ttu-id="96e15-107">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="96e15-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="96e15-108">Scale the Kubernetes nodes</span><span class="sxs-lookup"><span data-stu-id="96e15-108">Scale the Kubernetes nodes</span></span>
> * <span data-ttu-id="96e15-109">Manually scale Kubernetes pods that run your application</span><span class="sxs-lookup"><span data-stu-id="96e15-109">Manually scale Kubernetes pods that run your application</span></span>
> * <span data-ttu-id="96e15-110">Configure autoscaling pods that run the app front-end</span><span class="sxs-lookup"><span data-stu-id="96e15-110">Configure autoscaling pods that run the app front-end</span></span>

<span data-ttu-id="96e15-111">In subsequent tutorials, the Azure Vote application is updated to a new version.</span><span class="sxs-lookup"><span data-stu-id="96e15-111">In subsequent tutorials, the Azure Vote application is updated to a new version.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="96e15-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="96e15-112">Before you begin</span></span>

<span data-ttu-id="96e15-113">In previous tutorials, an application was packaged into a container image, this image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span><span class="sxs-lookup"><span data-stu-id="96e15-113">In previous tutorials, an application was packaged into a container image, this image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="96e15-114">The application was then run on the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="96e15-114">The application was then run on the Kubernetes cluster.</span></span> <span data-ttu-id="96e15-115">If you have not done these steps, and would like to follow along, return to the [Tutorial 1 – Create container images][aks-tutorial-prepare-app].</span><span class="sxs-lookup"><span data-stu-id="96e15-115">If you have not done these steps, and would like to follow along, return to the [Tutorial 1 – Create container images][aks-tutorial-prepare-app].</span></span>

<span data-ttu-id="96e15-116">This tutorial requires that you are running the Azure CLI version 2.0.38 or later.</span><span class="sxs-lookup"><span data-stu-id="96e15-116">This tutorial requires that you are running the Azure CLI version 2.0.38 or later.</span></span> <span data-ttu-id="96e15-117">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="96e15-117">Run `az --version` to find the version.</span></span> <span data-ttu-id="96e15-118">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span><span class="sxs-lookup"><span data-stu-id="96e15-118">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span></span>

## <a name="manually-scale-pods"></a><span data-ttu-id="96e15-119">Manually scale pods</span><span class="sxs-lookup"><span data-stu-id="96e15-119">Manually scale pods</span></span>

<span data-ttu-id="96e15-120">When the Azure Vote front-end and Redis instance were deployed in previous tutorials, a single replica was created.</span><span class="sxs-lookup"><span data-stu-id="96e15-120">When the Azure Vote front-end and Redis instance were deployed in previous tutorials, a single replica was created.</span></span> <span data-ttu-id="96e15-121">To see the number and state of pods in your cluster, use the [kubectl get][kubectl-get] command as follows:</span><span class="sxs-lookup"><span data-stu-id="96e15-121">To see the number and state of pods in your cluster, use the [kubectl get][kubectl-get] command as follows:</span></span>

```console
kubectl get pods
```

<span data-ttu-id="96e15-122">The following example output shows one front-end pod and one back-end pod:</span><span class="sxs-lookup"><span data-stu-id="96e15-122">The following example output shows one front-end pod and one back-end pod:</span></span>

```
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

<span data-ttu-id="96e15-123">To manually change the number of pods in the *azure-vote-front* deployment, use the [kubectl scale][kubectl-scale] command.</span><span class="sxs-lookup"><span data-stu-id="96e15-123">To manually change the number of pods in the *azure-vote-front* deployment, use the [kubectl scale][kubectl-scale] command.</span></span> <span data-ttu-id="96e15-124">The following example increases the number of front-end pods to *5*:</span><span class="sxs-lookup"><span data-stu-id="96e15-124">The following example increases the number of front-end pods to *5*:</span></span>

```console
kubectl scale --replicas=5 deployment/azure-vote-front
```

<span data-ttu-id="96e15-125">Run [kubectl get pods][kubectl-get] again to verify that Kubernetes creates the additional pods.</span><span class="sxs-lookup"><span data-stu-id="96e15-125">Run [kubectl get pods][kubectl-get] again to verify that Kubernetes creates the additional pods.</span></span> <span data-ttu-id="96e15-126">After a minute or so, the additional pods are available in your cluster:</span><span class="sxs-lookup"><span data-stu-id="96e15-126">After a minute or so, the additional pods are available in your cluster:</span></span>

```console
$ kubectl get pods

                                    READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a><span data-ttu-id="96e15-127">Autoscale pods</span><span class="sxs-lookup"><span data-stu-id="96e15-127">Autoscale pods</span></span>

<span data-ttu-id="96e15-128">Kubernetes supports [horizontal pod autoscaling][kubernetes-hpa] to adjust the number of pods in a deployment depending on CPU utilization or other select metrics.</span><span class="sxs-lookup"><span data-stu-id="96e15-128">Kubernetes supports [horizontal pod autoscaling][kubernetes-hpa] to adjust the number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> <span data-ttu-id="96e15-129">The [Metrics Server][metrics-server] is used to provide resource utilization to Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="96e15-129">The [Metrics Server][metrics-server] is used to provide resource utilization to Kubernetes.</span></span> <span data-ttu-id="96e15-130">To install the Metrics Server, clone the `metrics-server` GitHub repo and install the example resource definitions.</span><span class="sxs-lookup"><span data-stu-id="96e15-130">To install the Metrics Server, clone the `metrics-server` GitHub repo and install the example resource definitions.</span></span> <span data-ttu-id="96e15-131">To view the contents of these YAML definitions, see [Metrics Server for Kuberenetes 1.8+][metrics-server-github].</span><span class="sxs-lookup"><span data-stu-id="96e15-131">To view the contents of these YAML definitions, see [Metrics Server for Kuberenetes 1.8+][metrics-server-github].</span></span>

```console
git clone https://github.com/kubernetes-incubator/metrics-server.git
kubectl create -f metrics-server/deploy/1.8+/
```

<span data-ttu-id="96e15-132">To use the autoscaler, your pods must have CPU requests and limits defined.</span><span class="sxs-lookup"><span data-stu-id="96e15-132">To use the autoscaler, your pods must have CPU requests and limits defined.</span></span> <span data-ttu-id="96e15-133">In the `azure-vote-front` deployment, the front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span><span class="sxs-lookup"><span data-stu-id="96e15-133">In the `azure-vote-front` deployment, the front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span></span> <span data-ttu-id="96e15-134">The settings look like:</span><span class="sxs-lookup"><span data-stu-id="96e15-134">The settings look like:</span></span>

```yaml
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

<span data-ttu-id="96e15-135">The following example uses the [kubectl autoscale][kubectl-autoscale] command to autoscale the number of pods in the *azure-vote-front* deployment.</span><span class="sxs-lookup"><span data-stu-id="96e15-135">The following example uses the [kubectl autoscale][kubectl-autoscale] command to autoscale the number of pods in the *azure-vote-front* deployment.</span></span> <span data-ttu-id="96e15-136">If CPU utilization exceeds 50%, the autoscaler increases the pods up to a maximum of 10 instances:</span><span class="sxs-lookup"><span data-stu-id="96e15-136">If CPU utilization exceeds 50%, the autoscaler increases the pods up to a maximum of 10 instances:</span></span>

```console
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

<span data-ttu-id="96e15-137">To see the status of the autoscaler, use the `kubectl get hpa` command as follows:</span><span class="sxs-lookup"><span data-stu-id="96e15-137">To see the status of the autoscaler, use the `kubectl get hpa` command as follows:</span></span>

```
$ kubectl get hpa

NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

<span data-ttu-id="96e15-138">After a few minutes, with minimal load on the Azure Vote app, the number of pod replicas decreases automatically to three.</span><span class="sxs-lookup"><span data-stu-id="96e15-138">After a few minutes, with minimal load on the Azure Vote app, the number of pod replicas decreases automatically to three.</span></span> <span data-ttu-id="96e15-139">You can use `kubectl get pods` again to see the unneeded pods being removed.</span><span class="sxs-lookup"><span data-stu-id="96e15-139">You can use `kubectl get pods` again to see the unneeded pods being removed.</span></span>

## <a name="manually-scale-aks-nodes"></a><span data-ttu-id="96e15-140">Manually scale AKS nodes</span><span class="sxs-lookup"><span data-stu-id="96e15-140">Manually scale AKS nodes</span></span>

<span data-ttu-id="96e15-141">If you created your Kubernetes cluster using the commands in the previous tutorial, it has one node.</span><span class="sxs-lookup"><span data-stu-id="96e15-141">If you created your Kubernetes cluster using the commands in the previous tutorial, it has one node.</span></span> <span data-ttu-id="96e15-142">You can adjust the number of nodes manually if you plan more or fewer container workloads on your cluster.</span><span class="sxs-lookup"><span data-stu-id="96e15-142">You can adjust the number of nodes manually if you plan more or fewer container workloads on your cluster.</span></span>

<span data-ttu-id="96e15-143">The following example increases the number of nodes to three in the Kubernetes cluster named *myAKSCluster*.</span><span class="sxs-lookup"><span data-stu-id="96e15-143">The following example increases the number of nodes to three in the Kubernetes cluster named *myAKSCluster*.</span></span> <span data-ttu-id="96e15-144">The command takes a couple of minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="96e15-144">The command takes a couple of minutes to complete.</span></span>

```azurecli
az aks scale --resource-group=myResourceGroup --name=myAKSCluster --node-count 3
```

<span data-ttu-id="96e15-145">The output is similar to:</span><span class="sxs-lookup"><span data-stu-id="96e15-145">The output is similar to:</span></span>

```
"agentPoolProfiles": [
  {
    "count": 3,
    "dnsPrefix": null,
    "fqdn": null,
    "name": "myAKSCluster",
    "osDiskSizeGb": null,
    "osType": "Linux",
    "ports": null,
    "storageProfile": "ManagedDisks",
    "vmSize": "Standard_D2_v2",
    "vnetSubnetId": null
  }
```

## <a name="next-steps"></a><span data-ttu-id="96e15-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="96e15-146">Next steps</span></span>

<span data-ttu-id="96e15-147">In this tutorial, you used different scaling features in your Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="96e15-147">In this tutorial, you used different scaling features in your Kubernetes cluster.</span></span> <span data-ttu-id="96e15-148">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="96e15-148">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="96e15-149">Scale the Kubernetes nodes</span><span class="sxs-lookup"><span data-stu-id="96e15-149">Scale the Kubernetes nodes</span></span>
> * <span data-ttu-id="96e15-150">Manually scale Kubernetes pods that run your application</span><span class="sxs-lookup"><span data-stu-id="96e15-150">Manually scale Kubernetes pods that run your application</span></span>
> * <span data-ttu-id="96e15-151">Configure autoscaling pods that run the app front-end</span><span class="sxs-lookup"><span data-stu-id="96e15-151">Configure autoscaling pods that run the app front-end</span></span>

<span data-ttu-id="96e15-152">Advance to the next tutorial to learn how to update application in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="96e15-152">Advance to the next tutorial to learn how to update application in Kubernetes.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="96e15-153">[Update an application in Kubernetes][aks-tutorial-update-app]</span><span class="sxs-lookup"><span data-stu-id="96e15-153">[Update an application in Kubernetes][aks-tutorial-update-app]</span></span>

<!-- LINKS - external -->
[kubectl-autoscale]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#autoscale
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubectl-scale]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#scale
[kubernetes-hpa]: https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/
[metrics-server-github]: https://github.com/kubernetes-incubator/metrics-server/tree/master/deploy/1.8%2B
[metrics-server]: https://kubernetes.io/docs/tasks/debug-application-cluster/core-metrics-pipeline/

<!-- LINKS - internal -->
[aks-tutorial-prepare-app]: ./tutorial-kubernetes-prepare-app.md
[aks-tutorial-update-app]: ./tutorial-kubernetes-app-update.md
[az-aks-scale]: /cli/azure/aks#az-aks-scale
[azure-cli-install]: /cli/azure/install-azure-cli
