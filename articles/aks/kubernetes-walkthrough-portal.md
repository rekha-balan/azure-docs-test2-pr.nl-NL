---
title: Quickstart - Azure Kubernetes cluster portal quickstart
description: Quickly learn to create a Kubernetes cluster for Linux containers in AKS with the Azure portal.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: quickstart
ms.date: 07/27/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: aceddc2594065c9c36f8dbf63fce2ad03577a383
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870895"
---
# <a name="quickstart-deploy-an-azure-kubernetes-service-aks-cluster"></a><span data-ttu-id="824cb-103">Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster</span><span class="sxs-lookup"><span data-stu-id="824cb-103">Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster</span></span>

<span data-ttu-id="824cb-104">In this quickstart, you deploy an AKS cluster using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="824cb-104">In this quickstart, you deploy an AKS cluster using the Azure portal.</span></span> <span data-ttu-id="824cb-105">A multi-container application consisting of web front end and a Redis instance is then run on the cluster.</span><span class="sxs-lookup"><span data-stu-id="824cb-105">A multi-container application consisting of web front end and a Redis instance is then run on the cluster.</span></span> <span data-ttu-id="824cb-106">Once completed, the application is accessible over the internet.</span><span class="sxs-lookup"><span data-stu-id="824cb-106">Once completed, the application is accessible over the internet.</span></span>

![Image of browsing to Azure Vote sample application](media/container-service-kubernetes-walkthrough/azure-vote.png)

<span data-ttu-id="824cb-108">This quickstart assumes a basic understanding of Kubernetes concepts.</span><span class="sxs-lookup"><span data-stu-id="824cb-108">This quickstart assumes a basic understanding of Kubernetes concepts.</span></span> <span data-ttu-id="824cb-109">For detailed information on Kubernetes, see the [Kubernetes documentation][kubernetes-documentation].</span><span class="sxs-lookup"><span data-stu-id="824cb-109">For detailed information on Kubernetes, see the [Kubernetes documentation][kubernetes-documentation].</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="824cb-110">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="824cb-110">Sign in to Azure</span></span>

<span data-ttu-id="824cb-111">Sign in to the Azure portal at http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="824cb-111">Sign in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-an-aks-cluster"></a><span data-ttu-id="824cb-112">Create an AKS cluster</span><span class="sxs-lookup"><span data-stu-id="824cb-112">Create an AKS cluster</span></span>

<span data-ttu-id="824cb-113">In the top left-hand corner of the Azure portal, select **Create a resource** > **Kubernetes Service**.</span><span class="sxs-lookup"><span data-stu-id="824cb-113">In the top left-hand corner of the Azure portal, select **Create a resource** > **Kubernetes Service**.</span></span>

<span data-ttu-id="824cb-114">To create an AKS cluster, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="824cb-114">To create an AKS cluster, complete the following steps:</span></span>

1. <span data-ttu-id="824cb-115">**Basics** - Configure the following options:</span><span class="sxs-lookup"><span data-stu-id="824cb-115">**Basics** - Configure the following options:</span></span>
    - <span data-ttu-id="824cb-116">*PROJECT DETAILS*: Select an Azure subscription, then select or create an Azure resource group, such as *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="824cb-116">*PROJECT DETAILS*: Select an Azure subscription, then select or create an Azure resource group, such as *myResourceGroup*.</span></span> <span data-ttu-id="824cb-117">Enter a **Kubernetes cluster name**, such as *myAKSCluster*.</span><span class="sxs-lookup"><span data-stu-id="824cb-117">Enter a **Kubernetes cluster name**, such as *myAKSCluster*.</span></span>
    - <span data-ttu-id="824cb-118">*CLUSTER DETAILS*: Select a region, Kubernetes version, and DNS name prefix for the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="824cb-118">*CLUSTER DETAILS*: Select a region, Kubernetes version, and DNS name prefix for the AKS cluster.</span></span>
    - <span data-ttu-id="824cb-119">*SCALE*: Select a VM size for the AKS nodes.</span><span class="sxs-lookup"><span data-stu-id="824cb-119">*SCALE*: Select a VM size for the AKS nodes.</span></span> <span data-ttu-id="824cb-120">The VM size **cannot** be changed once an AKS cluster has been deployed.</span><span class="sxs-lookup"><span data-stu-id="824cb-120">The VM size **cannot** be changed once an AKS cluster has been deployed.</span></span>
        - <span data-ttu-id="824cb-121">Select the number of nodes to deploy into the cluster.</span><span class="sxs-lookup"><span data-stu-id="824cb-121">Select the number of nodes to deploy into the cluster.</span></span> <span data-ttu-id="824cb-122">For this quickstart, set **Node count** to *1*.</span><span class="sxs-lookup"><span data-stu-id="824cb-122">For this quickstart, set **Node count** to *1*.</span></span> <span data-ttu-id="824cb-123">Node count **can** be adjusted after the cluster has been deployed.</span><span class="sxs-lookup"><span data-stu-id="824cb-123">Node count **can** be adjusted after the cluster has been deployed.</span></span>
    
    ![Create AKS cluster - provide basic information](media/kubernetes-walkthrough-portal/create-cluster-1.png)

    <span data-ttu-id="824cb-125">Select **Next: Authentication** when complete.</span><span class="sxs-lookup"><span data-stu-id="824cb-125">Select **Next: Authentication** when complete.</span></span>

1. <span data-ttu-id="824cb-126">**Authentication**: Configure the following options:</span><span class="sxs-lookup"><span data-stu-id="824cb-126">**Authentication**: Configure the following options:</span></span>
    - <span data-ttu-id="824cb-127">Create a new service principal or *Configure* to use an existing one.</span><span class="sxs-lookup"><span data-stu-id="824cb-127">Create a new service principal or *Configure* to use an existing one.</span></span> <span data-ttu-id="824cb-128">When using an existing SPN, you need to provide the SPN client ID and secret.</span><span class="sxs-lookup"><span data-stu-id="824cb-128">When using an existing SPN, you need to provide the SPN client ID and secret.</span></span>
    - <span data-ttu-id="824cb-129">Enable the option for Kubernetes role-based access controls (RBAC).</span><span class="sxs-lookup"><span data-stu-id="824cb-129">Enable the option for Kubernetes role-based access controls (RBAC).</span></span> <span data-ttu-id="824cb-130">These controls provide more fine-grained control over access to the Kubernetes resources deployed in your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="824cb-130">These controls provide more fine-grained control over access to the Kubernetes resources deployed in your AKS cluster.</span></span>

    ![Create AKS cluster - configure authentication](media/kubernetes-walkthrough-portal/create-cluster-2.png)

    <span data-ttu-id="824cb-132">Select **Next: Networking** when complete.</span><span class="sxs-lookup"><span data-stu-id="824cb-132">Select **Next: Networking** when complete.</span></span>

1. <span data-ttu-id="824cb-133">**Networking**: Configure the following networking options, which should be set as default:</span><span class="sxs-lookup"><span data-stu-id="824cb-133">**Networking**: Configure the following networking options, which should be set as default:</span></span>
    
    - <span data-ttu-id="824cb-134">**Http application routing** - Select **Yes** to configure an integrated ingress controller with automatic public DNS name creation.</span><span class="sxs-lookup"><span data-stu-id="824cb-134">**Http application routing** - Select **Yes** to configure an integrated ingress controller with automatic public DNS name creation.</span></span> <span data-ttu-id="824cb-135">For more information on Http routing, see, [AKS HTTP routing and DNS][http-routing].</span><span class="sxs-lookup"><span data-stu-id="824cb-135">For more information on Http routing, see, [AKS HTTP routing and DNS][http-routing].</span></span>
    - <span data-ttu-id="824cb-136">**Network configuration** - Select the **Basic** network configuration using the [kubenet][kubenet] Kubernetes plugin, rather than advanced networking configuration using [Azure CNI][azure-cni].</span><span class="sxs-lookup"><span data-stu-id="824cb-136">**Network configuration** - Select the **Basic** network configuration using the [kubenet][kubenet] Kubernetes plugin, rather than advanced networking configuration using [Azure CNI][azure-cni].</span></span> <span data-ttu-id="824cb-137">For more information on networking options, see [AKS networking overview][aks-network].</span><span class="sxs-lookup"><span data-stu-id="824cb-137">For more information on networking options, see [AKS networking overview][aks-network].</span></span>
    
    <span data-ttu-id="824cb-138">Select **Next: Monitoring** when complete.</span><span class="sxs-lookup"><span data-stu-id="824cb-138">Select **Next: Monitoring** when complete.</span></span>

1. <span data-ttu-id="824cb-139">When deploying an AKS cluster, Azure Container Insights can be configured to monitor health of the AKS cluster and pods running on the cluster.</span><span class="sxs-lookup"><span data-stu-id="824cb-139">When deploying an AKS cluster, Azure Container Insights can be configured to monitor health of the AKS cluster and pods running on the cluster.</span></span> <span data-ttu-id="824cb-140">For more information on container health monitoring, see [Monitor Azure Kubernetes Service health][aks-monitor].</span><span class="sxs-lookup"><span data-stu-id="824cb-140">For more information on container health monitoring, see [Monitor Azure Kubernetes Service health][aks-monitor].</span></span>

    <span data-ttu-id="824cb-141">Select **Yes** to enable container monitoring and select an existing Log Analytics workspace, or create a new one.</span><span class="sxs-lookup"><span data-stu-id="824cb-141">Select **Yes** to enable container monitoring and select an existing Log Analytics workspace, or create a new one.</span></span>
    
    <span data-ttu-id="824cb-142">Select **Review + create** and then **Create** when ready.</span><span class="sxs-lookup"><span data-stu-id="824cb-142">Select **Review + create** and then **Create** when ready.</span></span>

<span data-ttu-id="824cb-143">It takes a few minutes to create the AKS cluster and to be ready for use.</span><span class="sxs-lookup"><span data-stu-id="824cb-143">It takes a few minutes to create the AKS cluster and to be ready for use.</span></span> <span data-ttu-id="824cb-144">Browse to the AKS cluster resource group, such as *myResourceGroup*, and select the AKS resource, such as *myAKSCluster*.</span><span class="sxs-lookup"><span data-stu-id="824cb-144">Browse to the AKS cluster resource group, such as *myResourceGroup*, and select the AKS resource, such as *myAKSCluster*.</span></span> <span data-ttu-id="824cb-145">The AKS cluster dashboard is shown, as in the following example screenshot:</span><span class="sxs-lookup"><span data-stu-id="824cb-145">The AKS cluster dashboard is shown, as in the following example screenshot:</span></span>

![Example AKS dashboard in the Azure portal](media/kubernetes-walkthrough-portal/aks-portal-dashboard.png)

## <a name="connect-to-the-cluster"></a><span data-ttu-id="824cb-147">Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="824cb-147">Connect to the cluster</span></span>

<span data-ttu-id="824cb-148">To manage a Kubernetes cluster, use [kubectl][kubectl], the Kubernetes command-line client.</span><span class="sxs-lookup"><span data-stu-id="824cb-148">To manage a Kubernetes cluster, use [kubectl][kubectl], the Kubernetes command-line client.</span></span> <span data-ttu-id="824cb-149">The `kubectl` client is pre-installed in the Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="824cb-149">The `kubectl` client is pre-installed in the Azure Cloud Shell.</span></span>

<span data-ttu-id="824cb-150">Open Cloud Shell using the button on the top right-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="824cb-150">Open Cloud Shell using the button on the top right-hand corner of the Azure portal.</span></span>

![Open the Azure Cloud Shell in the portal](media/kubernetes-walkthrough-portal/aks-cloud-shell.png)

<span data-ttu-id="824cb-152">Use the [az aks get-credentials][az-aks-get-credentials] command to configure `kubectl` to connect to your Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="824cb-152">Use the [az aks get-credentials][az-aks-get-credentials] command to configure `kubectl` to connect to your Kubernetes cluster.</span></span> <span data-ttu-id="824cb-153">The following example gets credentials for the cluster name *myAKSCluster* in the resource group named *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="824cb-153">The following example gets credentials for the cluster name *myAKSCluster* in the resource group named *myResourceGroup*:</span></span>

```azurecli-interactive
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```

<span data-ttu-id="824cb-154">To verify the connection to your cluster, use the [kubectl get][kubectl-get] command to return a list of the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="824cb-154">To verify the connection to your cluster, use the [kubectl get][kubectl-get] command to return a list of the cluster nodes.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="824cb-155">The following example output shows the single node created in the previous steps.</span><span class="sxs-lookup"><span data-stu-id="824cb-155">The following example output shows the single node created in the previous steps.</span></span>

```
NAME                       STATUS    ROLES     AGE       VERSION
aks-agentpool-14693408-0   Ready     agent     10m       v1.10.5
```

## <a name="run-the-application"></a><span data-ttu-id="824cb-156">Run the application</span><span class="sxs-lookup"><span data-stu-id="824cb-156">Run the application</span></span>

<span data-ttu-id="824cb-157">Kubernetes manifest files define a desired state for a cluster, including what container images should be running.</span><span class="sxs-lookup"><span data-stu-id="824cb-157">Kubernetes manifest files define a desired state for a cluster, including what container images should be running.</span></span> <span data-ttu-id="824cb-158">In this quickstart, a manifest is used to create all the objects needed to run a sample Azure Vote application.</span><span class="sxs-lookup"><span data-stu-id="824cb-158">In this quickstart, a manifest is used to create all the objects needed to run a sample Azure Vote application.</span></span> <span data-ttu-id="824cb-159">These objects include two [Kubernetes deployments][kubernetes-deployment] - one for the Azure Vote front end, and the other for a Redis instance.</span><span class="sxs-lookup"><span data-stu-id="824cb-159">These objects include two [Kubernetes deployments][kubernetes-deployment] - one for the Azure Vote front end, and the other for a Redis instance.</span></span> <span data-ttu-id="824cb-160">Also, two [Kubernetes Services][kubernetes-service] are created - an internal service for the Redis instance, and an external service for accessing the Azure Vote application from the internet.</span><span class="sxs-lookup"><span data-stu-id="824cb-160">Also, two [Kubernetes Services][kubernetes-service] are created - an internal service for the Redis instance, and an external service for accessing the Azure Vote application from the internet.</span></span>

<span data-ttu-id="824cb-161">Create a file named `azure-vote.yaml` and copy into it the following YAML code.</span><span class="sxs-lookup"><span data-stu-id="824cb-161">Create a file named `azure-vote.yaml` and copy into it the following YAML code.</span></span> <span data-ttu-id="824cb-162">If you are working in Azure Cloud Shell, create the file using `vi` or `Nano`, as if working on a virtual or physical system.</span><span class="sxs-lookup"><span data-stu-id="824cb-162">If you are working in Azure Cloud Shell, create the file using `vi` or `Nano`, as if working on a virtual or physical system.</span></span>

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

<span data-ttu-id="824cb-163">Use the [kubectl apply][kubectl-apply] command to run the application.</span><span class="sxs-lookup"><span data-stu-id="824cb-163">Use the [kubectl apply][kubectl-apply] command to run the application.</span></span>

```azurecli-interactive
kubectl create -f azure-vote.yaml
```

<span data-ttu-id="824cb-164">The following example output shows the Kubernetes resources created on your AKS cluster:</span><span class="sxs-lookup"><span data-stu-id="824cb-164">The following example output shows the Kubernetes resources created on your AKS cluster:</span></span>

```
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-the-application"></a><span data-ttu-id="824cb-165">Test the application</span><span class="sxs-lookup"><span data-stu-id="824cb-165">Test the application</span></span>

<span data-ttu-id="824cb-166">As the application is run, a [Kubernetes service][kubernetes-service] is created to expose the application to the internet.</span><span class="sxs-lookup"><span data-stu-id="824cb-166">As the application is run, a [Kubernetes service][kubernetes-service] is created to expose the application to the internet.</span></span> <span data-ttu-id="824cb-167">This process can take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="824cb-167">This process can take a few minutes to complete.</span></span>

<span data-ttu-id="824cb-168">To monitor progress, use the [kubectl get service][kubectl-get] command with the `--watch` argument.</span><span class="sxs-lookup"><span data-stu-id="824cb-168">To monitor progress, use the [kubectl get service][kubectl-get] command with the `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="824cb-169">Initially, the *EXTERNAL-IP* for the *azure-vote-front* service appears as *pending*.</span><span class="sxs-lookup"><span data-stu-id="824cb-169">Initially, the *EXTERNAL-IP* for the *azure-vote-front* service appears as *pending*.</span></span>

```
NAME               TYPE           CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   LoadBalancer   10.0.37.27   <pending>     80:30572/TCP   6s
```

<span data-ttu-id="824cb-170">Once the *EXTERNAL-IP* address has changed from *pending* to an *IP address*, use `CTRL-C` to stop the kubectl watch process.</span><span class="sxs-lookup"><span data-stu-id="824cb-170">Once the *EXTERNAL-IP* address has changed from *pending* to an *IP address*, use `CTRL-C` to stop the kubectl watch process.</span></span>

```
azure-vote-front   LoadBalancer   10.0.37.27   52.179.23.131   80:30572/TCP   2m
```

<span data-ttu-id="824cb-171">Open a web browser to the external IP address of your service to see the Azure Vote App, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="824cb-171">Open a web browser to the external IP address of your service to see the Azure Vote App, as shown in the following example:</span></span>

![Image of browsing to Azure Vote sample application](media/container-service-kubernetes-walkthrough/azure-vote.png)

## <a name="monitor-health-and-logs"></a><span data-ttu-id="824cb-173">Monitor health and logs</span><span class="sxs-lookup"><span data-stu-id="824cb-173">Monitor health and logs</span></span>

<span data-ttu-id="824cb-174">When you created the cluster, container insights monitoring was enabled.</span><span class="sxs-lookup"><span data-stu-id="824cb-174">When you created the cluster, container insights monitoring was enabled.</span></span> <span data-ttu-id="824cb-175">This monitoring feature provides health metrics for both the AKS cluster and pods running on the cluster.</span><span class="sxs-lookup"><span data-stu-id="824cb-175">This monitoring feature provides health metrics for both the AKS cluster and pods running on the cluster.</span></span> <span data-ttu-id="824cb-176">For more information on container health monitoring, see [Monitor Azure Kubernetes Service health][aks-monitor].</span><span class="sxs-lookup"><span data-stu-id="824cb-176">For more information on container health monitoring, see [Monitor Azure Kubernetes Service health][aks-monitor].</span></span>

<span data-ttu-id="824cb-177">It may take a few minutes for this data to populate in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="824cb-177">It may take a few minutes for this data to populate in the Azure portal.</span></span> <span data-ttu-id="824cb-178">To see current status, uptime, and resource usage for the Azure Vote pods, browse back to the AKS resource in the Azure portal, such as *myAKSCluster*.</span><span class="sxs-lookup"><span data-stu-id="824cb-178">To see current status, uptime, and resource usage for the Azure Vote pods, browse back to the AKS resource in the Azure portal, such as *myAKSCluster*.</span></span> <span data-ttu-id="824cb-179">Choose **Monitor Container Health** > select the **default** namespace > then select **Containers**.</span><span class="sxs-lookup"><span data-stu-id="824cb-179">Choose **Monitor Container Health** > select the **default** namespace > then select **Containers**.</span></span>  <span data-ttu-id="824cb-180">The *azure-vote-back* and *azure-vote-front* containers are shown:</span><span class="sxs-lookup"><span data-stu-id="824cb-180">The *azure-vote-back* and *azure-vote-front* containers are shown:</span></span>

![View the health of running containers in AKS](media/kubernetes-walkthrough-portal/monitor-containers.png)

<span data-ttu-id="824cb-182">To see logs for the `azure-vote-front` pod, select the **View Logs** link on the right-hand side of the containers list.</span><span class="sxs-lookup"><span data-stu-id="824cb-182">To see logs for the `azure-vote-front` pod, select the **View Logs** link on the right-hand side of the containers list.</span></span> <span data-ttu-id="824cb-183">These logs include the *stdout* and *stderr* streams from the container.</span><span class="sxs-lookup"><span data-stu-id="824cb-183">These logs include the *stdout* and *stderr* streams from the container.</span></span>

![View the containers logs in AKS](media/kubernetes-walkthrough-portal/monitor-containers-logs.png)

## <a name="delete-cluster"></a><span data-ttu-id="824cb-185">Delete cluster</span><span class="sxs-lookup"><span data-stu-id="824cb-185">Delete cluster</span></span>

<span data-ttu-id="824cb-186">When the cluster is no longer needed, delete the cluster resource, which deletes all associated resources.</span><span class="sxs-lookup"><span data-stu-id="824cb-186">When the cluster is no longer needed, delete the cluster resource, which deletes all associated resources.</span></span> <span data-ttu-id="824cb-187">This operation can be completed in the Azure portal by selecting the **Delete** button on the AKS cluster dashboard.</span><span class="sxs-lookup"><span data-stu-id="824cb-187">This operation can be completed in the Azure portal by selecting the **Delete** button on the AKS cluster dashboard.</span></span> <span data-ttu-id="824cb-188">Alternatively, the [az aks delete][az-aks-delete] command can be used in the Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="824cb-188">Alternatively, the [az aks delete][az-aks-delete] command can be used in the Cloud Shell:</span></span>

```azurecli-interactive
az aks delete --resource-group myResourceGroup --name myAKSCluster --no-wait
```

## <a name="get-the-code"></a><span data-ttu-id="824cb-189">Get the code</span><span class="sxs-lookup"><span data-stu-id="824cb-189">Get the code</span></span>

<span data-ttu-id="824cb-190">In this quickstart, pre-created container images have been used to create a Kubernetes deployment.</span><span class="sxs-lookup"><span data-stu-id="824cb-190">In this quickstart, pre-created container images have been used to create a Kubernetes deployment.</span></span> <span data-ttu-id="824cb-191">The related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="824cb-191">The related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span></span>

[https://github.com/Azure-Samples/azure-voting-app-redis][azure-vote-app]

## <a name="next-steps"></a><span data-ttu-id="824cb-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="824cb-192">Next steps</span></span>

<span data-ttu-id="824cb-193">In this quickstart, you deployed a Kubernetes cluster and deployed a multi-container application to it.</span><span class="sxs-lookup"><span data-stu-id="824cb-193">In this quickstart, you deployed a Kubernetes cluster and deployed a multi-container application to it.</span></span>

<span data-ttu-id="824cb-194">To learn more about AKS, and walk through a complete code to deployment example, continue to the Kubernetes cluster tutorial.</span><span class="sxs-lookup"><span data-stu-id="824cb-194">To learn more about AKS, and walk through a complete code to deployment example, continue to the Kubernetes cluster tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="824cb-195">[AKS tutorial][aks-tutorial]</span><span class="sxs-lookup"><span data-stu-id="824cb-195">[AKS tutorial][aks-tutorial]</span></span>

<!-- LINKS - external -->
[azure-vote-app]: https://github.com/Azure-Samples/azure-voting-app-redis.git
[azure-cni]: https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md
[kubectl]: https://kubernetes.io/docs/user-guide/kubectl/
[kubectl-apply]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubenet]: https://kubernetes.io/docs/concepts/cluster-administration/network-plugins/#kubenet
[kubernetes-deployment]: https://kubernetes.io/docs/concepts/workloads/controllers/deployment/
[kubernetes-documentation]: https://kubernetes.io/docs/home/
[kubernetes-service]: https://kubernetes.io/docs/concepts/services-networking/service/

<!-- LINKS - internal -->
[az-aks-get-credentials]: /cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials
[az-aks-delete]: /cli/azure/aks#az-aks-delete
[aks-monitor]: ../monitoring/monitoring-container-health.md
[aks-network]: ./networking-overview.md
[aks-tutorial]: ./tutorial-kubernetes-prepare-app.md
[http-routing]: ./http-application-routing.md
