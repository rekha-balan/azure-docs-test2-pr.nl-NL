---
title: Quickstart - Azure Kubernetes cluster for Linux
description: Quickly learn to create a Kubernetes cluster for Linux containers in AKS with the Azure CLI.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: quickstart
ms.date: 07/31/2018
ms.author: iainfou
ms.custom: H1Hack27Feb2017, mvc, devcenter
ms.openlocfilehash: f52551e9d57ccfc44502992b59412878c4092c0d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868908"
---
# <a name="quickstart-deploy-an-azure-kubernetes-service-aks-cluster"></a><span data-ttu-id="eec85-103">Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster</span><span class="sxs-lookup"><span data-stu-id="eec85-103">Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster</span></span>

<span data-ttu-id="eec85-104">In this quickstart, an AKS cluster is deployed using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="eec85-104">In this quickstart, an AKS cluster is deployed using the Azure CLI.</span></span> <span data-ttu-id="eec85-105">A multi-container application consisting of web front end and a Redis instance is then run on the cluster.</span><span class="sxs-lookup"><span data-stu-id="eec85-105">A multi-container application consisting of web front end and a Redis instance is then run on the cluster.</span></span> <span data-ttu-id="eec85-106">Once completed, the application is accessible over the internet.</span><span class="sxs-lookup"><span data-stu-id="eec85-106">Once completed, the application is accessible over the internet.</span></span>

![Image of browsing to Azure Vote](media/container-service-kubernetes-walkthrough/azure-vote.png)

<span data-ttu-id="eec85-108">This quickstart assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation][kubernetes-documentation].</span><span class="sxs-lookup"><span data-stu-id="eec85-108">This quickstart assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation][kubernetes-documentation].</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="eec85-109">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.43 or later.</span><span class="sxs-lookup"><span data-stu-id="eec85-109">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.43 or later.</span></span> <span data-ttu-id="eec85-110">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="eec85-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="eec85-111">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span><span class="sxs-lookup"><span data-stu-id="eec85-111">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="eec85-112">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="eec85-112">Create a resource group</span></span>

<span data-ttu-id="eec85-113">Create a resource group with the [az group create][az-group-create] command.</span><span class="sxs-lookup"><span data-stu-id="eec85-113">Create a resource group with the [az group create][az-group-create] command.</span></span> <span data-ttu-id="eec85-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="eec85-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> <span data-ttu-id="eec85-115">When you create a resource group, you are asked to specify a location.</span><span class="sxs-lookup"><span data-stu-id="eec85-115">When you create a resource group, you are asked to specify a location.</span></span> <span data-ttu-id="eec85-116">This location is where your resources run in Azure.</span><span class="sxs-lookup"><span data-stu-id="eec85-116">This location is where your resources run in Azure.</span></span>

<span data-ttu-id="eec85-117">The following example creates a resource group named *myAKSCluster* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="eec85-117">The following example creates a resource group named *myAKSCluster* in the *eastus* location.</span></span>

```azurecli-interactive
az group create --name myAKSCluster --location eastus
```

<span data-ttu-id="eec85-118">Output:</span><span class="sxs-lookup"><span data-stu-id="eec85-118">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myAKSCluster",
  "location": "eastus",
  "managedBy": null,
  "name": "myAKSCluster",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-aks-cluster"></a><span data-ttu-id="eec85-119">Create AKS cluster</span><span class="sxs-lookup"><span data-stu-id="eec85-119">Create AKS cluster</span></span>

<span data-ttu-id="eec85-120">Use the [az aks create][az-aks-create] command to create an AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="eec85-120">Use the [az aks create][az-aks-create] command to create an AKS cluster.</span></span> <span data-ttu-id="eec85-121">The following example creates a cluster named *myAKSCluster* with one node.</span><span class="sxs-lookup"><span data-stu-id="eec85-121">The following example creates a cluster named *myAKSCluster* with one node.</span></span> <span data-ttu-id="eec85-122">Container health monitoring is also enabled using the *--enable-addons monitoring* parameter.</span><span class="sxs-lookup"><span data-stu-id="eec85-122">Container health monitoring is also enabled using the *--enable-addons monitoring* parameter.</span></span> <span data-ttu-id="eec85-123">For more information on enabling the container health monitoring solution, see [Monitor Azure Kubernetes Service health][aks-monitor].</span><span class="sxs-lookup"><span data-stu-id="eec85-123">For more information on enabling the container health monitoring solution, see [Monitor Azure Kubernetes Service health][aks-monitor].</span></span>

```azurecli-interactive
az aks create --resource-group myAKSCluster --name myAKSCluster --node-count 1 --enable-addons monitoring --generate-ssh-keys
```

<span data-ttu-id="eec85-124">After several minutes, the command completes and returns JSON-formatted information about the cluster.</span><span class="sxs-lookup"><span data-stu-id="eec85-124">After several minutes, the command completes and returns JSON-formatted information about the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="eec85-125">Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="eec85-125">Connect to the cluster</span></span>

<span data-ttu-id="eec85-126">To manage a Kubernetes cluster, use [kubectl][kubectl], the Kubernetes command-line client.</span><span class="sxs-lookup"><span data-stu-id="eec85-126">To manage a Kubernetes cluster, use [kubectl][kubectl], the Kubernetes command-line client.</span></span>

<span data-ttu-id="eec85-127">If you're using Azure Cloud Shell, `kubectl` is already installed.</span><span class="sxs-lookup"><span data-stu-id="eec85-127">If you're using Azure Cloud Shell, `kubectl` is already installed.</span></span> <span data-ttu-id="eec85-128">If you want to install it locally, use the [az aks install-cli][az-aks-install-cli] command.</span><span class="sxs-lookup"><span data-stu-id="eec85-128">If you want to install it locally, use the [az aks install-cli][az-aks-install-cli] command.</span></span>


```azurecli
az aks install-cli
```

<span data-ttu-id="eec85-129">To configure `kubectl` to connect to your Kubernetes cluster, use the [az aks get-credentials][az-aks-get-credentials] command.</span><span class="sxs-lookup"><span data-stu-id="eec85-129">To configure `kubectl` to connect to your Kubernetes cluster, use the [az aks get-credentials][az-aks-get-credentials] command.</span></span> <span data-ttu-id="eec85-130">This step downloads credentials and configures the Kubernetes CLI to use them.</span><span class="sxs-lookup"><span data-stu-id="eec85-130">This step downloads credentials and configures the Kubernetes CLI to use them.</span></span>

```azurecli-interactive
az aks get-credentials --resource-group myAKSCluster --name myAKSCluster
```

<span data-ttu-id="eec85-131">To verify the connection to your cluster, use the [kubectl get][kubectl-get] command to return a list of the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="eec85-131">To verify the connection to your cluster, use the [kubectl get][kubectl-get] command to return a list of the cluster nodes.</span></span> <span data-ttu-id="eec85-132">It can take a few minutes for the nodes to appear.</span><span class="sxs-lookup"><span data-stu-id="eec85-132">It can take a few minutes for the nodes to appear.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="eec85-133">Output:</span><span class="sxs-lookup"><span data-stu-id="eec85-133">Output:</span></span>

```
NAME                          STATUS    ROLES     AGE       VERSION
k8s-myAKSCluster-36346190-0   Ready     agent     2m        v1.7.7
```

## <a name="run-the-application"></a><span data-ttu-id="eec85-134">Run the application</span><span class="sxs-lookup"><span data-stu-id="eec85-134">Run the application</span></span>

<span data-ttu-id="eec85-135">A Kubernetes manifest file defines a desired state for the cluster, including what container images should be running.</span><span class="sxs-lookup"><span data-stu-id="eec85-135">A Kubernetes manifest file defines a desired state for the cluster, including what container images should be running.</span></span> <span data-ttu-id="eec85-136">For this example, a manifest is used to create all objects needed to run the Azure Vote application.</span><span class="sxs-lookup"><span data-stu-id="eec85-136">For this example, a manifest is used to create all objects needed to run the Azure Vote application.</span></span> <span data-ttu-id="eec85-137">This manifest includes two [Kubernetes deployments][kubernetes-deployment], one for the Azure Vote Python applications, and the other for a Redis instance.</span><span class="sxs-lookup"><span data-stu-id="eec85-137">This manifest includes two [Kubernetes deployments][kubernetes-deployment], one for the Azure Vote Python applications, and the other for a Redis instance.</span></span> <span data-ttu-id="eec85-138">Also, two [Kubernetes Services][kubernetes-service] are created, an internal service for the Redis instance, and an external service for accessing the Azure Vote application from the internet.</span><span class="sxs-lookup"><span data-stu-id="eec85-138">Also, two [Kubernetes Services][kubernetes-service] are created, an internal service for the Redis instance, and an external service for accessing the Azure Vote application from the internet.</span></span>

<span data-ttu-id="eec85-139">Create a file named `azure-vote.yaml` and copy into it the following YAML code.</span><span class="sxs-lookup"><span data-stu-id="eec85-139">Create a file named `azure-vote.yaml` and copy into it the following YAML code.</span></span> <span data-ttu-id="eec85-140">If you are working in Azure Cloud Shell, this file can be created using vi or Nano as if working on a virtual or physical system.</span><span class="sxs-lookup"><span data-stu-id="eec85-140">If you are working in Azure Cloud Shell, this file can be created using vi or Nano as if working on a virtual or physical system.</span></span>

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      containers:
      - name: azure-vote-back
        image: redis
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      containers:
      - name: azure-vote-front
        image: microsoft/azure-vote-front:v1
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

<span data-ttu-id="eec85-141">Use the [kubectl apply][kubectl-apply] command to run the application.</span><span class="sxs-lookup"><span data-stu-id="eec85-141">Use the [kubectl apply][kubectl-apply] command to run the application.</span></span>

```azurecli-interactive
kubectl apply -f azure-vote.yaml
```

<span data-ttu-id="eec85-142">Output:</span><span class="sxs-lookup"><span data-stu-id="eec85-142">Output:</span></span>

```
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-the-application"></a><span data-ttu-id="eec85-143">Test the application</span><span class="sxs-lookup"><span data-stu-id="eec85-143">Test the application</span></span>

<span data-ttu-id="eec85-144">As the application is run, a [Kubernetes service][kubernetes-service] is created that exposes the application front end to the internet.</span><span class="sxs-lookup"><span data-stu-id="eec85-144">As the application is run, a [Kubernetes service][kubernetes-service] is created that exposes the application front end to the internet.</span></span> <span data-ttu-id="eec85-145">This process can take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="eec85-145">This process can take a few minutes to complete.</span></span>

<span data-ttu-id="eec85-146">To monitor progress, use the [kubectl get service][kubectl-get] command with the `--watch` argument.</span><span class="sxs-lookup"><span data-stu-id="eec85-146">To monitor progress, use the [kubectl get service][kubectl-get] command with the `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="eec85-147">Initially the *EXTERNAL-IP* for the *azure-vote-front* service appears as *pending*.</span><span class="sxs-lookup"><span data-stu-id="eec85-147">Initially the *EXTERNAL-IP* for the *azure-vote-front* service appears as *pending*.</span></span>

```
NAME               TYPE           CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   LoadBalancer   10.0.37.27   <pending>     80:30572/TCP   6s
```

<span data-ttu-id="eec85-148">Once the *EXTERNAL-IP* address has changed from *pending* to an *IP address*, use `CTRL-C` to stop the kubectl watch process.</span><span class="sxs-lookup"><span data-stu-id="eec85-148">Once the *EXTERNAL-IP* address has changed from *pending* to an *IP address*, use `CTRL-C` to stop the kubectl watch process.</span></span>

```
azure-vote-front   LoadBalancer   10.0.37.27   52.179.23.131   80:30572/TCP   2m
```

<span data-ttu-id="eec85-149">Now browse to the external IP address to see the Azure Vote App.</span><span class="sxs-lookup"><span data-stu-id="eec85-149">Now browse to the external IP address to see the Azure Vote App.</span></span>

![Image of browsing to Azure Vote](media/container-service-kubernetes-walkthrough/azure-vote.png)

## <a name="monitor-health-and-logs"></a><span data-ttu-id="eec85-151">Monitor health and logs</span><span class="sxs-lookup"><span data-stu-id="eec85-151">Monitor health and logs</span></span>

<span data-ttu-id="eec85-152">When the AKS cluster was created, monitoring was enabled to capture health metrics for both the cluster nodes and pods.</span><span class="sxs-lookup"><span data-stu-id="eec85-152">When the AKS cluster was created, monitoring was enabled to capture health metrics for both the cluster nodes and pods.</span></span> <span data-ttu-id="eec85-153">These health metrics are available in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="eec85-153">These health metrics are available in the Azure portal.</span></span> <span data-ttu-id="eec85-154">For more information on container health monitoring, see [Monitor Azure Kubernetes Service health][aks-monitor].</span><span class="sxs-lookup"><span data-stu-id="eec85-154">For more information on container health monitoring, see [Monitor Azure Kubernetes Service health][aks-monitor].</span></span>

<span data-ttu-id="eec85-155">To see current status, uptime, and resource usage for the Azure Vote pods, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="eec85-155">To see current status, uptime, and resource usage for the Azure Vote pods, complete the following steps:</span></span>

1. <span data-ttu-id="eec85-156">Open a web browser to the Azure portal [https://portal.azure.com][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="eec85-156">Open a web browser to the Azure portal [https://portal.azure.com][azure-portal].</span></span>
1. <span data-ttu-id="eec85-157">Select your resource group, such as *myResourceGroup*, then select your AKS cluster, such as *myAKSCluster*.</span><span class="sxs-lookup"><span data-stu-id="eec85-157">Select your resource group, such as *myResourceGroup*, then select your AKS cluster, such as *myAKSCluster*.</span></span> 
1. <span data-ttu-id="eec85-158">Choose **Monitor container health** > select the **default** namespace > then select **Containers**.</span><span class="sxs-lookup"><span data-stu-id="eec85-158">Choose **Monitor container health** > select the **default** namespace > then select **Containers**.</span></span>

<span data-ttu-id="eec85-159">It may take a few minutes for this data to populate in the Azure portal, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="eec85-159">It may take a few minutes for this data to populate in the Azure portal, as shown in the following example:</span></span>

![Create AKS cluster one](media/kubernetes-walkthrough/view-container-health.png)

<span data-ttu-id="eec85-161">To see logs for the `azure-vote-front` pod, select the **View Logs** link on the right-hand side of the list of containers.</span><span class="sxs-lookup"><span data-stu-id="eec85-161">To see logs for the `azure-vote-front` pod, select the **View Logs** link on the right-hand side of the list of containers.</span></span> <span data-ttu-id="eec85-162">These logs include the *stdout* and *stderr* streams from the container.</span><span class="sxs-lookup"><span data-stu-id="eec85-162">These logs include the *stdout* and *stderr* streams from the container.</span></span>

![Create AKS cluster one](media/kubernetes-walkthrough/view-container-logs.png)

## <a name="delete-cluster"></a><span data-ttu-id="eec85-164">Delete cluster</span><span class="sxs-lookup"><span data-stu-id="eec85-164">Delete cluster</span></span>

<span data-ttu-id="eec85-165">When the cluster is no longer needed, use the [az group delete][az-group-delete] command to remove the resource group, container service, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="eec85-165">When the cluster is no longer needed, use the [az group delete][az-group-delete] command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myAKSCluster --yes --no-wait
```

> [!NOTE]
> <span data-ttu-id="eec85-166">When you delete the cluster, the Azure Active Directory service principal used by the AKS cluster is not removed.</span><span class="sxs-lookup"><span data-stu-id="eec85-166">When you delete the cluster, the Azure Active Directory service principal used by the AKS cluster is not removed.</span></span> <span data-ttu-id="eec85-167">For steps on how to remove the service principal, see [AKS service principal considerations and deletion][sp-delete].</span><span class="sxs-lookup"><span data-stu-id="eec85-167">For steps on how to remove the service principal, see [AKS service principal considerations and deletion][sp-delete].</span></span>

## <a name="get-the-code"></a><span data-ttu-id="eec85-168">Get the code</span><span class="sxs-lookup"><span data-stu-id="eec85-168">Get the code</span></span>

<span data-ttu-id="eec85-169">In this quickstart, pre-created container images have been used to create a Kubernetes deployment.</span><span class="sxs-lookup"><span data-stu-id="eec85-169">In this quickstart, pre-created container images have been used to create a Kubernetes deployment.</span></span> <span data-ttu-id="eec85-170">The related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="eec85-170">The related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span></span>

[https://github.com/Azure-Samples/azure-voting-app-redis][azure-vote-app]

## <a name="next-steps"></a><span data-ttu-id="eec85-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="eec85-171">Next steps</span></span>

<span data-ttu-id="eec85-172">In this quickstart, you deployed a Kubernetes cluster and deployed a multi-container application to it.</span><span class="sxs-lookup"><span data-stu-id="eec85-172">In this quickstart, you deployed a Kubernetes cluster and deployed a multi-container application to it.</span></span>

<span data-ttu-id="eec85-173">To learn more about AKS, and walk through a complete code to deployment example, continue to the Kubernetes cluster tutorial.</span><span class="sxs-lookup"><span data-stu-id="eec85-173">To learn more about AKS, and walk through a complete code to deployment example, continue to the Kubernetes cluster tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="eec85-174">[AKS tutorial][aks-tutorial]</span><span class="sxs-lookup"><span data-stu-id="eec85-174">[AKS tutorial][aks-tutorial]</span></span>

<!-- LINKS - external -->
[azure-vote-app]: https://github.com/Azure-Samples/azure-voting-app-redis.git
[kubectl]: https://kubernetes.io/docs/user-guide/kubectl/
[kubectl-apply]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply
[kubernetes-deployment]: https://kubernetes.io/docs/concepts/workloads/controllers/deployment/
[kubernetes-documentation]: https://kubernetes.io/docs/home/
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubernetes-service]: https://kubernetes.io/docs/concepts/services-networking/service/

<!-- LINKS - internal -->
[aks-monitor]: https://aka.ms/coingfonboarding
[aks-tutorial]: ./tutorial-kubernetes-prepare-app.md
[az-aks-browse]: /cli/azure/aks?view=azure-cli-latest#az-aks-browse
[az-aks-create]: /cli/azure/aks?view=azure-cli-latest#az-aks-create
[az-aks-get-credentials]: /cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials
[az-aks-install-cli]: /cli/azure/aks?view=azure-cli-latest#az-aks-install-cli
[az-group-create]: /cli/azure/group#az-group-create
[az-group-delete]: /cli/azure/group#az-group-delete
[azure-cli-install]: /cli/azure/install-azure-cli
[sp-delete]: kubernetes-service-principal.md#additional-considerations
[azure-portal]: https://portal.azure.com
