---
title: Run Virtual Kubelet in an Azure Kubernetes Service (AKS) cluster
description: Learn how to use Virtual Kubelet with Azure Kubernetes Service (AKS) to run Linux and Windows containers on Azure Container Instances.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 08/14/2018
ms.author: iainfou
ms.openlocfilehash: e7208cb4c2cdef6fc4e639b32fdb2fac242bd3a2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869069"
---
# <a name="use-virtual-kubelet-with-azure-kubernetes-service-aks"></a><span data-ttu-id="eb269-103">Use Virtual Kubelet with Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="eb269-103">Use Virtual Kubelet with Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="eb269-104">Azure Container Instances (ACI) provide a hosted environment for running containers in Azure.</span><span class="sxs-lookup"><span data-stu-id="eb269-104">Azure Container Instances (ACI) provide a hosted environment for running containers in Azure.</span></span> <span data-ttu-id="eb269-105">When using ACI, there is no need to manage the underlying compute infrastructure, Azure handles this management for you.</span><span class="sxs-lookup"><span data-stu-id="eb269-105">When using ACI, there is no need to manage the underlying compute infrastructure, Azure handles this management for you.</span></span> <span data-ttu-id="eb269-106">When running containers in ACI, you are charged by the second for each running container.</span><span class="sxs-lookup"><span data-stu-id="eb269-106">When running containers in ACI, you are charged by the second for each running container.</span></span>

<span data-ttu-id="eb269-107">When using the Virtual Kubelet provider for Azure Container Instances, both Linux and Windows containers can be scheduled on a container instance as if it is a standard Kubernetes node.</span><span class="sxs-lookup"><span data-stu-id="eb269-107">When using the Virtual Kubelet provider for Azure Container Instances, both Linux and Windows containers can be scheduled on a container instance as if it is a standard Kubernetes node.</span></span> <span data-ttu-id="eb269-108">This configuration allows you to take advantage of both the capabilities of Kubernetes and the management value and cost benefit of container instances.</span><span class="sxs-lookup"><span data-stu-id="eb269-108">This configuration allows you to take advantage of both the capabilities of Kubernetes and the management value and cost benefit of container instances.</span></span>

> [!NOTE]
> <span data-ttu-id="eb269-109">Virtual Kubelet is an experimental open source project and should be used as such.</span><span class="sxs-lookup"><span data-stu-id="eb269-109">Virtual Kubelet is an experimental open source project and should be used as such.</span></span> <span data-ttu-id="eb269-110">To contribute, file issues, and read more about virtual kubelet, see the [Virtual Kubelet GitHub project][vk-github].</span><span class="sxs-lookup"><span data-stu-id="eb269-110">To contribute, file issues, and read more about virtual kubelet, see the [Virtual Kubelet GitHub project][vk-github].</span></span>

<span data-ttu-id="eb269-111">This document details configuring the Virtual Kubelet for container instances on an AKS.</span><span class="sxs-lookup"><span data-stu-id="eb269-111">This document details configuring the Virtual Kubelet for container instances on an AKS.</span></span>

## <a name="prerequisite"></a><span data-ttu-id="eb269-112">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="eb269-112">Prerequisite</span></span>

<span data-ttu-id="eb269-113">This document assumes that you have an AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="eb269-113">This document assumes that you have an AKS cluster.</span></span> <span data-ttu-id="eb269-114">If you need an AKS cluster, see the [Azure Kubernetes Service (AKS) quickstart][aks-quick-start].</span><span class="sxs-lookup"><span data-stu-id="eb269-114">If you need an AKS cluster, see the [Azure Kubernetes Service (AKS) quickstart][aks-quick-start].</span></span>

<span data-ttu-id="eb269-115">You also need the Azure CLI version **2.0.33** or later.</span><span class="sxs-lookup"><span data-stu-id="eb269-115">You also need the Azure CLI version **2.0.33** or later.</span></span> <span data-ttu-id="eb269-116">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="eb269-116">Run `az --version` to find the version.</span></span> <span data-ttu-id="eb269-117">If you need to install or upgrade, see [Install Azure CLI](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eb269-117">If you need to install or upgrade, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="eb269-118">To install the Virtual Kubelet, [Helm](https://docs.helm.sh/using_helm/#installing-helm) is also required.</span><span class="sxs-lookup"><span data-stu-id="eb269-118">To install the Virtual Kubelet, [Helm](https://docs.helm.sh/using_helm/#installing-helm) is also required.</span></span>

### <a name="for-rbac-enabled-clusters"></a><span data-ttu-id="eb269-119">For RBAC-enabled clusters</span><span class="sxs-lookup"><span data-stu-id="eb269-119">For RBAC-enabled clusters</span></span>

<span data-ttu-id="eb269-120">If your AKS cluster is RBAC-enabled, you must create a service account and role binding for use with Tiller.</span><span class="sxs-lookup"><span data-stu-id="eb269-120">If your AKS cluster is RBAC-enabled, you must create a service account and role binding for use with Tiller.</span></span> <span data-ttu-id="eb269-121">For more information, see [Helm Role-based access control][helm-rbac].</span><span class="sxs-lookup"><span data-stu-id="eb269-121">For more information, see [Helm Role-based access control][helm-rbac].</span></span> <span data-ttu-id="eb269-122">To create a service account and role binding, create a file named *rbac-virtualkubelet.yaml* and paste the following definition:</span><span class="sxs-lookup"><span data-stu-id="eb269-122">To create a service account and role binding, create a file named *rbac-virtualkubelet.yaml* and paste the following definition:</span></span>

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: tiller
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: tiller
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
  - kind: ServiceAccount
    name: tiller
    namespace: kube-system
```

<span data-ttu-id="eb269-123">Apply the service account and binding with [kubectl apply][kubectl-apply] and specify your *rbac-virtualkubelet.yaml* file, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="eb269-123">Apply the service account and binding with [kubectl apply][kubectl-apply] and specify your *rbac-virtualkubelet.yaml* file, as shown in the following example:</span></span>

```
$ kubectl apply -f rbac-virtual-kubelet.yaml

clusterrolebinding.rbac.authorization.k8s.io/tiller created
```

<span data-ttu-id="eb269-124">Configure Helm to use the tiller service account:</span><span class="sxs-lookup"><span data-stu-id="eb269-124">Configure Helm to use the tiller service account:</span></span>

```console
helm init --service-account tiller
```

<span data-ttu-id="eb269-125">You can now continue to installing the Virtual Kubelet into your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="eb269-125">You can now continue to installing the Virtual Kubelet into your AKS cluster.</span></span>

## <a name="installation"></a><span data-ttu-id="eb269-126">Installation</span><span class="sxs-lookup"><span data-stu-id="eb269-126">Installation</span></span>

<span data-ttu-id="eb269-127">Use the [az aks install-connector][aks-install-connector] command to install Virtual Kubelet.</span><span class="sxs-lookup"><span data-stu-id="eb269-127">Use the [az aks install-connector][aks-install-connector] command to install Virtual Kubelet.</span></span> <span data-ttu-id="eb269-128">The following example deploys both the Linux and Windows connector.</span><span class="sxs-lookup"><span data-stu-id="eb269-128">The following example deploys both the Linux and Windows connector.</span></span>

```azurecli-interactive
az aks install-connector --resource-group myAKSCluster --name myAKSCluster --connector-name virtual-kubelet --os-type Both
```

<span data-ttu-id="eb269-129">These arguments are available for the `aks install-connector` command.</span><span class="sxs-lookup"><span data-stu-id="eb269-129">These arguments are available for the `aks install-connector` command.</span></span>

| <span data-ttu-id="eb269-130">Argument:</span><span class="sxs-lookup"><span data-stu-id="eb269-130">Argument:</span></span> | <span data-ttu-id="eb269-131">Description</span><span class="sxs-lookup"><span data-stu-id="eb269-131">Description</span></span> | <span data-ttu-id="eb269-132">Required</span><span class="sxs-lookup"><span data-stu-id="eb269-132">Required</span></span> |
|---|---|:---:|
| `--connector-name` | <span data-ttu-id="eb269-133">Name of the ACI Connector.</span><span class="sxs-lookup"><span data-stu-id="eb269-133">Name of the ACI Connector.</span></span>| <span data-ttu-id="eb269-134">Yes</span><span class="sxs-lookup"><span data-stu-id="eb269-134">Yes</span></span> |
| <span data-ttu-id="eb269-135">`--name` `-n`</span><span class="sxs-lookup"><span data-stu-id="eb269-135">`--name` `-n`</span></span> | <span data-ttu-id="eb269-136">Name of the managed cluster.</span><span class="sxs-lookup"><span data-stu-id="eb269-136">Name of the managed cluster.</span></span> | <span data-ttu-id="eb269-137">Yes</span><span class="sxs-lookup"><span data-stu-id="eb269-137">Yes</span></span> |
| <span data-ttu-id="eb269-138">`--resource-group` `-g`</span><span class="sxs-lookup"><span data-stu-id="eb269-138">`--resource-group` `-g`</span></span> | <span data-ttu-id="eb269-139">Name of resource group.</span><span class="sxs-lookup"><span data-stu-id="eb269-139">Name of resource group.</span></span> | <span data-ttu-id="eb269-140">Yes</span><span class="sxs-lookup"><span data-stu-id="eb269-140">Yes</span></span> |
| `--os-type` | <span data-ttu-id="eb269-141">Container instances operating system type.</span><span class="sxs-lookup"><span data-stu-id="eb269-141">Container instances operating system type.</span></span> <span data-ttu-id="eb269-142">Allowed values: Both, Linux, Windows.</span><span class="sxs-lookup"><span data-stu-id="eb269-142">Allowed values: Both, Linux, Windows.</span></span> <span data-ttu-id="eb269-143">Default: Linux.</span><span class="sxs-lookup"><span data-stu-id="eb269-143">Default: Linux.</span></span> | <span data-ttu-id="eb269-144">No</span><span class="sxs-lookup"><span data-stu-id="eb269-144">No</span></span> |
| `--aci-resource-group` | <span data-ttu-id="eb269-145">The resource group in which to create the ACI container groups.</span><span class="sxs-lookup"><span data-stu-id="eb269-145">The resource group in which to create the ACI container groups.</span></span> | <span data-ttu-id="eb269-146">No</span><span class="sxs-lookup"><span data-stu-id="eb269-146">No</span></span> |
| <span data-ttu-id="eb269-147">`--location` `-l`</span><span class="sxs-lookup"><span data-stu-id="eb269-147">`--location` `-l`</span></span> | <span data-ttu-id="eb269-148">The location to create the ACI container groups.</span><span class="sxs-lookup"><span data-stu-id="eb269-148">The location to create the ACI container groups.</span></span> | <span data-ttu-id="eb269-149">No</span><span class="sxs-lookup"><span data-stu-id="eb269-149">No</span></span> |
| `--service-principal` | <span data-ttu-id="eb269-150">Service principal used for authentication to Azure APIs.</span><span class="sxs-lookup"><span data-stu-id="eb269-150">Service principal used for authentication to Azure APIs.</span></span> | <span data-ttu-id="eb269-151">No</span><span class="sxs-lookup"><span data-stu-id="eb269-151">No</span></span> |
| `--client-secret` | <span data-ttu-id="eb269-152">Secret associated with the service principal.</span><span class="sxs-lookup"><span data-stu-id="eb269-152">Secret associated with the service principal.</span></span> | <span data-ttu-id="eb269-153">No</span><span class="sxs-lookup"><span data-stu-id="eb269-153">No</span></span> |
| `--chart-url` | <span data-ttu-id="eb269-154">URL of a Helm chart that installs ACI Connector.</span><span class="sxs-lookup"><span data-stu-id="eb269-154">URL of a Helm chart that installs ACI Connector.</span></span> | <span data-ttu-id="eb269-155">No</span><span class="sxs-lookup"><span data-stu-id="eb269-155">No</span></span> |
| `--image-tag` | <span data-ttu-id="eb269-156">The image tag of the virtual kubelet container image.</span><span class="sxs-lookup"><span data-stu-id="eb269-156">The image tag of the virtual kubelet container image.</span></span> | <span data-ttu-id="eb269-157">No</span><span class="sxs-lookup"><span data-stu-id="eb269-157">No</span></span> |

## <a name="validate-virtual-kubelet"></a><span data-ttu-id="eb269-158">Validate Virtual Kubelet</span><span class="sxs-lookup"><span data-stu-id="eb269-158">Validate Virtual Kubelet</span></span>

<span data-ttu-id="eb269-159">To validate that Virtual Kubelet has been installed, return a list of Kubernetes nodes using the [kubectl get nodes][kubectl-get] command.</span><span class="sxs-lookup"><span data-stu-id="eb269-159">To validate that Virtual Kubelet has been installed, return a list of Kubernetes nodes using the [kubectl get nodes][kubectl-get] command.</span></span>

```
$ kubectl get nodes

NAME                                    STATUS    ROLES     AGE       VERSION
aks-nodepool1-23443254-0                Ready     agent     16d       v1.9.6
aks-nodepool1-23443254-1                Ready     agent     16d       v1.9.6
aks-nodepool1-23443254-2                Ready     agent     16d       v1.9.6
virtual-kubelet-virtual-kubelet-linux   Ready     agent     4m        v1.8.3
virtual-kubelet-virtual-kubelet-win     Ready     agent     4m        v1.8.3
```

## <a name="run-linux-container"></a><span data-ttu-id="eb269-160">Run Linux container</span><span class="sxs-lookup"><span data-stu-id="eb269-160">Run Linux container</span></span>

<span data-ttu-id="eb269-161">Create a file named `virtual-kubelet-linux.yaml` and copy in the following YAML.</span><span class="sxs-lookup"><span data-stu-id="eb269-161">Create a file named `virtual-kubelet-linux.yaml` and copy in the following YAML.</span></span> <span data-ttu-id="eb269-162">Replace the `kubernetes.io/hostname` value with the name of the Linux Virtual Kubelet node.</span><span class="sxs-lookup"><span data-stu-id="eb269-162">Replace the `kubernetes.io/hostname` value with the name of the Linux Virtual Kubelet node.</span></span> <span data-ttu-id="eb269-163">Take note that a [nodeSelector][node-selector] and [toleration][toleration] are being used to schedule the container on the node.</span><span class="sxs-lookup"><span data-stu-id="eb269-163">Take note that a [nodeSelector][node-selector] and [toleration][toleration] are being used to schedule the container on the node.</span></span>

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: aci-helloworld
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: aci-helloworld
    spec:
      containers:
      - name: aci-helloworld
        image: microsoft/aci-helloworld
        ports:
        - containerPort: 80
      nodeSelector:
        kubernetes.io/hostname: virtual-kubelet-virtual-kubelet-linux
      tolerations:
      - key: azure.com/aci
        effect: NoSchedule
```

<span data-ttu-id="eb269-164">Run the application with the [kubectl create][kubectl-create] command.</span><span class="sxs-lookup"><span data-stu-id="eb269-164">Run the application with the [kubectl create][kubectl-create] command.</span></span>

```console
kubectl create -f virtual-kubelet-linux.yaml
```

<span data-ttu-id="eb269-165">Use the [kubectl get pods][kubectl-get] command with the `-o wide` argument to output a list of pods with the scheduled node.</span><span class="sxs-lookup"><span data-stu-id="eb269-165">Use the [kubectl get pods][kubectl-get] command with the `-o wide` argument to output a list of pods with the scheduled node.</span></span> <span data-ttu-id="eb269-166">Notice that the `aci-helloworld` pod has been scheduled on the `virtual-kubelet-virtual-kubelet-linux` node.</span><span class="sxs-lookup"><span data-stu-id="eb269-166">Notice that the `aci-helloworld` pod has been scheduled on the `virtual-kubelet-virtual-kubelet-linux` node.</span></span>

```
$ kubectl get pods -o wide

NAME                                READY     STATUS    RESTARTS   AGE       IP             NODE
aci-helloworld-2559879000-8vmjw     1/1       Running   0          39s       52.179.3.180   virtual-kubelet-virtual-kubelet-linux
```

## <a name="run-windows-container"></a><span data-ttu-id="eb269-167">Run Windows container</span><span class="sxs-lookup"><span data-stu-id="eb269-167">Run Windows container</span></span>

<span data-ttu-id="eb269-168">Create a file named `virtual-kubelet-windows.yaml` and copy in the following YAML.</span><span class="sxs-lookup"><span data-stu-id="eb269-168">Create a file named `virtual-kubelet-windows.yaml` and copy in the following YAML.</span></span> <span data-ttu-id="eb269-169">Replace the `kubernetes.io/hostname` value with the name of the Windows Virtual Kubelet node.</span><span class="sxs-lookup"><span data-stu-id="eb269-169">Replace the `kubernetes.io/hostname` value with the name of the Windows Virtual Kubelet node.</span></span> <span data-ttu-id="eb269-170">Take note that a [nodeSelector][node-selector] and [toleration][toleration] are being used to schedule the container on the node.</span><span class="sxs-lookup"><span data-stu-id="eb269-170">Take note that a [nodeSelector][node-selector] and [toleration][toleration] are being used to schedule the container on the node.</span></span>

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: nanoserver-iis
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: nanoserver-iis
    spec:
      containers:
      - name: nanoserver-iis
        image: microsoft/iis:nanoserver
        ports:
        - containerPort: 80
      nodeSelector:
        kubernetes.io/hostname: virtual-kubelet-virtual-kubelet-win
      tolerations:
      - key: azure.com/aci
        effect: NoSchedule
```

<span data-ttu-id="eb269-171">Run the application with the [kubectl create][kubectl-create] command.</span><span class="sxs-lookup"><span data-stu-id="eb269-171">Run the application with the [kubectl create][kubectl-create] command.</span></span>

```console
kubectl create -f virtual-kubelet-windows.yaml
```

<span data-ttu-id="eb269-172">Use the [kubectl get pods][kubectl-get] command with the `-o wide` argument to output a list of pods with the scheduled node.</span><span class="sxs-lookup"><span data-stu-id="eb269-172">Use the [kubectl get pods][kubectl-get] command with the `-o wide` argument to output a list of pods with the scheduled node.</span></span> <span data-ttu-id="eb269-173">Notice that the `nanoserver-iis` pod has been scheduled on the `virtual-kubelet-virtual-kubelet-win` node.</span><span class="sxs-lookup"><span data-stu-id="eb269-173">Notice that the `nanoserver-iis` pod has been scheduled on the `virtual-kubelet-virtual-kubelet-win` node.</span></span>

```
$ kubectl get pods -o wide

NAME                                READY     STATUS    RESTARTS   AGE       IP             NODE
nanoserver-iis-868bc8d489-tq4st     1/1       Running   8         21m       138.91.121.91   virtual-kubelet-virtual-kubelet-win
```

## <a name="remove-virtual-kubelet"></a><span data-ttu-id="eb269-174">Remove Virtual Kubelet</span><span class="sxs-lookup"><span data-stu-id="eb269-174">Remove Virtual Kubelet</span></span>

<span data-ttu-id="eb269-175">Use the [az aks remove-connector][aks-remove-connector] command to remove Virtual Kubelet.</span><span class="sxs-lookup"><span data-stu-id="eb269-175">Use the [az aks remove-connector][aks-remove-connector] command to remove Virtual Kubelet.</span></span> <span data-ttu-id="eb269-176">Replace the argument values with the name of the connector, AKS cluster, and the AKS cluster resource group.</span><span class="sxs-lookup"><span data-stu-id="eb269-176">Replace the argument values with the name of the connector, AKS cluster, and the AKS cluster resource group.</span></span>

```azurecli-interactive
az aks remove-connector --resource-group myAKSCluster --name myAKSCluster --connector-name virtual-kubelet
```

> [!NOTE]
> <span data-ttu-id="eb269-177">If you encounter errors removing both OS connectors, or want to remove just the Windows or Linux OS connector, you can manually specify the OS type.</span><span class="sxs-lookup"><span data-stu-id="eb269-177">If you encounter errors removing both OS connectors, or want to remove just the Windows or Linux OS connector, you can manually specify the OS type.</span></span> <span data-ttu-id="eb269-178">Add the `--os-type` parameter to the previous `az aks remove-connector` command, and specify `Windows` or `Linux`.</span><span class="sxs-lookup"><span data-stu-id="eb269-178">Add the `--os-type` parameter to the previous `az aks remove-connector` command, and specify `Windows` or `Linux`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb269-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="eb269-179">Next steps</span></span>

<span data-ttu-id="eb269-180">For possible issues with the Virtual Kubelet, see the [Known quirks and workarounds][vk-troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="eb269-180">For possible issues with the Virtual Kubelet, see the [Known quirks and workarounds][vk-troubleshooting].</span></span> <span data-ttu-id="eb269-181">To report problems with the Virtual Kubelet, [open a GitHub issue][vk-issues].</span><span class="sxs-lookup"><span data-stu-id="eb269-181">To report problems with the Virtual Kubelet, [open a GitHub issue][vk-issues].</span></span>

<span data-ttu-id="eb269-182">Read more about Virtual Kubelet at the [Virtual Kubelet Github project][vk-github].</span><span class="sxs-lookup"><span data-stu-id="eb269-182">Read more about Virtual Kubelet at the [Virtual Kubelet Github project][vk-github].</span></span>

<!-- LINKS - internal -->
[aks-quick-start]: ./kubernetes-walkthrough.md
[aks-remove-connector]: /cli/azure/aks#az-aks-remove-connector
[az-container-list]: /cli/azure/aks#az-aks-list
[aks-install-connector]: /cli/azure/aks#az-aks-install-connector

<!-- LINKS - external -->
[kubectl-create]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create
[kubectl-get]: https://kubernetes.io/docs/user-guide/kubectl/v1.8/#get
[node-selector]:https://kubernetes.io/docs/concepts/configuration/assign-pod-node/
[toleration]: https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/
[vk-github]: https://github.com/virtual-kubelet/virtual-kubelet
[helm-rbac]: https://docs.helm.sh/using_helm/#role-based-access-control
[kubectl-apply]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply
[vk-troubleshooting]: https://github.com/virtual-kubelet/virtual-kubelet#known-quirks-and-workarounds
[vk-issues]: https://github.com/virtual-kubelet/virtual-kubelet/issues
