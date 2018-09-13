---
title: Kubernetes on Azure - Cluster Autoscaler
description: Learn how to use the cluster autoscaler with Azure Kubernetes Service (AKS) to automatically scale your cluster to meet demand.
services: container-service
author: sakthivetrivel
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 07/19/18
ms.author: sakthivetrivel
ms.custom: mvc
ms.openlocfilehash: 06b93273ea096f2d24df4411a64ce99d054892cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864857"
---
# <a name="cluster-autoscaler-on-azure-kubernetes-service-aks---preview"></a><span data-ttu-id="b83bb-103">Cluster Autoscaler on Azure Kubernetes Service (AKS) - Preview</span><span class="sxs-lookup"><span data-stu-id="b83bb-103">Cluster Autoscaler on Azure Kubernetes Service (AKS) - Preview</span></span>

<span data-ttu-id="b83bb-104">Azure Kubernetes Service (AKS) provides a flexible solution to deploy a managed Kubernetes cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="b83bb-104">Azure Kubernetes Service (AKS) provides a flexible solution to deploy a managed Kubernetes cluster in Azure.</span></span> <span data-ttu-id="b83bb-105">As resource demands increase, the cluster autoscaler allows your cluster to grow to meet that demand based on constraints you set.</span><span class="sxs-lookup"><span data-stu-id="b83bb-105">As resource demands increase, the cluster autoscaler allows your cluster to grow to meet that demand based on constraints you set.</span></span> <span data-ttu-id="b83bb-106">The cluster autoscaler (CA) does this by scaling your agent nodes based on pending pods.</span><span class="sxs-lookup"><span data-stu-id="b83bb-106">The cluster autoscaler (CA) does this by scaling your agent nodes based on pending pods.</span></span> <span data-ttu-id="b83bb-107">It scans the cluster periodically to check for pending pods or empty nodes and increases the size if possible.</span><span class="sxs-lookup"><span data-stu-id="b83bb-107">It scans the cluster periodically to check for pending pods or empty nodes and increases the size if possible.</span></span> <span data-ttu-id="b83bb-108">By default, the CA scans for pending pods every 10 seconds and removes a node if it's unneeded for more than 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="b83bb-108">By default, the CA scans for pending pods every 10 seconds and removes a node if it's unneeded for more than 10 minutes.</span></span> <span data-ttu-id="b83bb-109">When used with the [horizontal pod autoscaler](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) (HPA), the HPA will update pod replicas and resources as per demand.</span><span class="sxs-lookup"><span data-stu-id="b83bb-109">When used with the [horizontal pod autoscaler](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) (HPA), the HPA will update pod replicas and resources as per demand.</span></span> <span data-ttu-id="b83bb-110">If there aren't enough nodes or unneeded nodes following this pod scaling, the CA will respond and schedule the pods on the new set of nodes.</span><span class="sxs-lookup"><span data-stu-id="b83bb-110">If there aren't enough nodes or unneeded nodes following this pod scaling, the CA will respond and schedule the pods on the new set of nodes.</span></span>

<span data-ttu-id="b83bb-111">This article describes how to deploy the cluster autoscaler on the agent nodes.</span><span class="sxs-lookup"><span data-stu-id="b83bb-111">This article describes how to deploy the cluster autoscaler on the agent nodes.</span></span> <span data-ttu-id="b83bb-112">However, since the cluster autoscaler is deployed in the kube-system namespace, the autoscaler will not scale down the node running that pod.</span><span class="sxs-lookup"><span data-stu-id="b83bb-112">However, since the cluster autoscaler is deployed in the kube-system namespace, the autoscaler will not scale down the node running that pod.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b83bb-113">Azure Kubernetes Service (AKS) cluster autoscaler integration is currently in **preview**.</span><span class="sxs-lookup"><span data-stu-id="b83bb-113">Azure Kubernetes Service (AKS) cluster autoscaler integration is currently in **preview**.</span></span> <span data-ttu-id="b83bb-114">Previews are made available to you on the condition that you agree to the [supplemental terms of use](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="b83bb-114">Previews are made available to you on the condition that you agree to the [supplemental terms of use](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span> <span data-ttu-id="b83bb-115">Some aspects of this feature may change prior to general availability (GA).</span><span class="sxs-lookup"><span data-stu-id="b83bb-115">Some aspects of this feature may change prior to general availability (GA).</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="b83bb-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b83bb-116">Prerequisites</span></span>

<span data-ttu-id="b83bb-117">This document assumes that you have an RBAC-enabled AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="b83bb-117">This document assumes that you have an RBAC-enabled AKS cluster.</span></span> <span data-ttu-id="b83bb-118">If you need an AKS cluster, see the [Azure Kubernetes Service (AKS) quickstart][aks-quick-start].</span><span class="sxs-lookup"><span data-stu-id="b83bb-118">If you need an AKS cluster, see the [Azure Kubernetes Service (AKS) quickstart][aks-quick-start].</span></span>

 <span data-ttu-id="b83bb-119">To use the cluster autoscaler, your cluster must be using Kubernetes v1.10.X or higher and must be RBAC-enabled.</span><span class="sxs-lookup"><span data-stu-id="b83bb-119">To use the cluster autoscaler, your cluster must be using Kubernetes v1.10.X or higher and must be RBAC-enabled.</span></span> <span data-ttu-id="b83bb-120">To upgrade your cluster, see the article on [upgrading an AKS cluster][aks-upgrade].</span><span class="sxs-lookup"><span data-stu-id="b83bb-120">To upgrade your cluster, see the article on [upgrading an AKS cluster][aks-upgrade].</span></span>

## <a name="gather-information"></a><span data-ttu-id="b83bb-121">Gather information</span><span class="sxs-lookup"><span data-stu-id="b83bb-121">Gather information</span></span>

<span data-ttu-id="b83bb-122">To generate the permissions for your cluster autoscaler to run in your cluster, run this bash script:</span><span class="sxs-lookup"><span data-stu-id="b83bb-122">To generate the permissions for your cluster autoscaler to run in your cluster, run this bash script:</span></span>

```sh
#! /bin/bash
ID=`az account show --query id -o json`
SUBSCRIPTION_ID=`echo $ID | tr -d '"' `

TENANT=`az account show --query tenantId -o json`
TENANT_ID=`echo $TENANT | tr -d '"' | base64`

read -p "What's your cluster name? " cluster_name
read -p "Resource group name? " resource_group

CLUSTER_NAME=`echo $cluster_name | base64`
RESOURCE_GROUP=`echo $resource_group | base64`

PERMISSIONS=`az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/$SUBSCRIPTION_ID" -o json`
CLIENT_ID=`echo $PERMISSIONS | sed -e 's/^.*"appId"[ ]*:[ ]*"//' -e 's/".*//' | base64`
CLIENT_SECRET=`echo $PERMISSIONS | sed -e 's/^.*"password"[ ]*:[ ]*"//' -e 's/".*//' | base64`

SUBSCRIPTION_ID=`echo $ID | tr -d '"' | base64 `

NODE_RESOURCE_GROUP=`az aks show --name $cluster_name  --resource-group $resource_group -o tsv --query 'nodeResourceGroup' | base64`

echo "---
apiVersion: v1
kind: Secret
metadata:
    name: cluster-autoscaler-azure
    namespace: kube-system
data:
    ClientID: $CLIENT_ID
    ClientSecret: $CLIENT_SECRET
    ResourceGroup: $RESOURCE_GROUP
    SubscriptionID: $SUBSCRIPTION_ID
    TenantID: $TENANT_ID
    VMType: QUtTCg==
    ClusterName: $CLUSTER_NAME
    NodeResourceGroup: $NODE_RESOURCE_GROUP
---"
```

<span data-ttu-id="b83bb-123">After following the steps in the script, the script will output your details in the form of a secret, like so:</span><span class="sxs-lookup"><span data-stu-id="b83bb-123">After following the steps in the script, the script will output your details in the form of a secret, like so:</span></span>

```yaml
---
apiVersion: v1
kind: Secret
metadata:
  name: cluster-autoscaler-azure
  namespace: kube-system
data:
  ClientID: <base64-encoded-client-id>
  ClientSecret: <base64-encoded-client-secret>$
  ResourceGroup: <base64-encoded-resource-group>  SubscriptionID: <base64-encode-subscription-id>
  TenantID: <base64-encoded-tenant-id>
  VMType: QUtTCg==
  ClusterName: <base64-encoded-clustername>
  NodeResourceGroup: <base64-encoded-node-resource-group>
---
```

<span data-ttu-id="b83bb-124">Next, get the name of your node pool by running the following command.</span><span class="sxs-lookup"><span data-stu-id="b83bb-124">Next, get the name of your node pool by running the following command.</span></span> 

```console
$ kubectl get nodes --show-labels
```

<span data-ttu-id="b83bb-125">Output:</span><span class="sxs-lookup"><span data-stu-id="b83bb-125">Output:</span></span>

```console
NAME                       STATUS    ROLES     AGE       VERSION   LABELS
aks-nodepool1-37756013-0   Ready     agent     1h        v1.10.3   agentpool=nodepool1,beta.kubernetes.io/arch=amd64,beta.kubernetes.io/instance-type=Standard_DS1_v2,beta.kubernetes.io/os=linux,failure-domain.beta.kubernetes.io/region=eastus,failure-domain.beta.kubernetes.io/zone=0,kubernetes.azure.com/cluster=MC_[resource-group]\_[cluster-name]_[location],kubernetes.io/hostname=aks-nodepool1-37756013-0,kubernetes.io/role=agent,storageprofile=managed,storagetier=Premium_LRS
 ```

<span data-ttu-id="b83bb-126">Then, extract the value of the label **agentpool**.</span><span class="sxs-lookup"><span data-stu-id="b83bb-126">Then, extract the value of the label **agentpool**.</span></span> <span data-ttu-id="b83bb-127">The default name for the node pool of a cluster is "nodepool1".</span><span class="sxs-lookup"><span data-stu-id="b83bb-127">The default name for the node pool of a cluster is "nodepool1".</span></span>

<span data-ttu-id="b83bb-128">Now using your secret and node pool, you can create a deployment chart.</span><span class="sxs-lookup"><span data-stu-id="b83bb-128">Now using your secret and node pool, you can create a deployment chart.</span></span>

## <a name="create-a-deployment-chart"></a><span data-ttu-id="b83bb-129">Create a deployment chart</span><span class="sxs-lookup"><span data-stu-id="b83bb-129">Create a deployment chart</span></span>

<span data-ttu-id="b83bb-130">Create a file named `aks-cluster-autoscaler.yaml`, and copy into it the following YAML code.</span><span class="sxs-lookup"><span data-stu-id="b83bb-130">Create a file named `aks-cluster-autoscaler.yaml`, and copy into it the following YAML code.</span></span>

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  labels:
    k8s-addon: cluster-autoscaler.addons.k8s.io
    k8s-app: cluster-autoscaler
  name: cluster-autoscaler
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRole
metadata:
  name: cluster-autoscaler
  labels:
    k8s-addon: cluster-autoscaler.addons.k8s.io
    k8s-app: cluster-autoscaler
rules:
- apiGroups: [""]
  resources: ["events","endpoints"]
  verbs: ["create", "patch"]
- apiGroups: [""]
  resources: ["pods/eviction"]
  verbs: ["create"]
- apiGroups: [""]
  resources: ["pods/status"]
  verbs: ["update"]
- apiGroups: [""]
  resources: ["endpoints"]
  resourceNames: ["cluster-autoscaler"]
  verbs: ["get","update"]
- apiGroups: [""]
  resources: ["nodes"]
  verbs: ["watch","list","get","update"]
- apiGroups: [""]
  resources: ["pods","services","replicationcontrollers","persistentvolumeclaims","persistentvolumes"]
  verbs: ["watch","list","get"]
- apiGroups: ["extensions"]
  resources: ["replicasets","daemonsets"]
  verbs: ["watch","list","get"]
- apiGroups: ["policy"]
  resources: ["poddisruptionbudgets"]
  verbs: ["watch","list"]
- apiGroups: ["apps"]
  resources: ["statefulsets"]
  verbs: ["watch","list","get"]
- apiGroups: ["storage.k8s.io"]
  resources: ["storageclasses"]
  verbs: ["get", "list", "watch"]

---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: Role
metadata:
  name: cluster-autoscaler
  namespace: kube-system
  labels:
    k8s-addon: cluster-autoscaler.addons.k8s.io
    k8s-app: cluster-autoscaler
rules:
- apiGroups: [""]
  resources: ["configmaps"]
  verbs: ["create"]
- apiGroups: [""]
  resources: ["configmaps"]
  resourceNames: ["cluster-autoscaler-status"]
  verbs: ["delete","get","update"]

---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: cluster-autoscaler
  labels:
    k8s-addon: cluster-autoscaler.addons.k8s.io
    k8s-app: cluster-autoscaler
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-autoscaler
subjects:
  - kind: ServiceAccount
    name: cluster-autoscaler
    namespace: kube-system

---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: RoleBinding
metadata:
  name: cluster-autoscaler
  namespace: kube-system
  labels:
    k8s-addon: cluster-autoscaler.addons.k8s.io
    k8s-app: cluster-autoscaler
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: cluster-autoscaler
subjects:
  - kind: ServiceAccount
    name: cluster-autoscaler
    namespace: kube-system

---
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  labels:
    app: cluster-autoscaler
  name: cluster-autoscaler
  namespace: kube-system
spec:
  replicas: 1
  selector:
    matchLabels:
      app: cluster-autoscaler
  template:
    metadata:
      labels:
        app: cluster-autoscaler
    spec:
      serviceAccountName: cluster-autoscaler
      containers:
      - image: k8s.gcr.io/cluster-autoscaler:{{ ca_version }}
        imagePullPolicy: Always
        name: cluster-autoscaler
        resources:
          limits:
            cpu: 100m
            memory: 300Mi
          requests:
            cpu: 100m
            memory: 300Mi
        command:
        - ./cluster-autoscaler
        - --v=3
        - --logtostderr=true
        - --cloud-provider=azure
        - --skip-nodes-with-local-storage=false
        - --nodes=1:10:nodepool1
        env:
        - name: ARM_SUBSCRIPTION_ID
          valueFrom:
            secretKeyRef:
              key: SubscriptionID
              name: cluster-autoscaler-azure
        - name: ARM_RESOURCE_GROUP
          valueFrom:
            secretKeyRef:
              key: ResourceGroup
              name: cluster-autoscaler-azure
        - name: ARM_TENANT_ID
          valueFrom:
            secretKeyRef:
              key: TenantID
              name: cluster-autoscaler-azure
        - name: ARM_CLIENT_ID
          valueFrom:
            secretKeyRef:
              key: ClientID
              name: cluster-autoscaler-azure
        - name: ARM_CLIENT_SECRET
          valueFrom:
            secretKeyRef:
              key: ClientSecret
              name: cluster-autoscaler-azure
        - name: ARM_VM_TYPE
          valueFrom:
            secretKeyRef:
              key: VMType
              name: cluster-autoscaler-azure
        - name: AZURE_CLUSTER_NAME
          valueFrom:
            secretKeyRef:
              key: ClusterName
              name: cluster-autoscaler-azure
        - name: AZURE_NODE_RESOURCE_GROUP
          valueFrom:
            secretKeyRef:
              key: NodeResourceGroup
              name: cluster-autoscaler-azure
      restartPolicy: Always
```

<span data-ttu-id="b83bb-131">Copy and paste the secret created in the previous step, and insert it at the start of the file.</span><span class="sxs-lookup"><span data-stu-id="b83bb-131">Copy and paste the secret created in the previous step, and insert it at the start of the file.</span></span>

<span data-ttu-id="b83bb-132">Next, to set the range of nodes, fill in the argument for `--nodes` under `command` in the form MIN:MAX:NODE_POOL_NAME.</span><span class="sxs-lookup"><span data-stu-id="b83bb-132">Next, to set the range of nodes, fill in the argument for `--nodes` under `command` in the form MIN:MAX:NODE_POOL_NAME.</span></span> <span data-ttu-id="b83bb-133">For example: `--nodes=3:10:nodepool1` sets the minimum number of nodes to 3, the maximum number of nodes to 10, and the node pool name to nodepool1.</span><span class="sxs-lookup"><span data-stu-id="b83bb-133">For example: `--nodes=3:10:nodepool1` sets the minimum number of nodes to 3, the maximum number of nodes to 10, and the node pool name to nodepool1.</span></span>

<span data-ttu-id="b83bb-134">Then, fill in the image field under **containers** with the version of the cluster autoscaler you want to use.</span><span class="sxs-lookup"><span data-stu-id="b83bb-134">Then, fill in the image field under **containers** with the version of the cluster autoscaler you want to use.</span></span> <span data-ttu-id="b83bb-135">AKS requires v1.2.2 or newer.</span><span class="sxs-lookup"><span data-stu-id="b83bb-135">AKS requires v1.2.2 or newer.</span></span> <span data-ttu-id="b83bb-136">The example here uses v1.2.2.</span><span class="sxs-lookup"><span data-stu-id="b83bb-136">The example here uses v1.2.2.</span></span>

## <a name="deployment"></a><span data-ttu-id="b83bb-137">Deployment</span><span class="sxs-lookup"><span data-stu-id="b83bb-137">Deployment</span></span>

<span data-ttu-id="b83bb-138">Deploy cluster-autoscaler by running</span><span class="sxs-lookup"><span data-stu-id="b83bb-138">Deploy cluster-autoscaler by running</span></span>

```console
kubectl create -f aks-cluster-autoscaler.yaml
```

<span data-ttu-id="b83bb-139">To check if the cluster autoscaler is running, use the following command and check the list of pods.</span><span class="sxs-lookup"><span data-stu-id="b83bb-139">To check if the cluster autoscaler is running, use the following command and check the list of pods.</span></span> <span data-ttu-id="b83bb-140">There should be a pod prefixed with "cluster-autoscaler" running.</span><span class="sxs-lookup"><span data-stu-id="b83bb-140">There should be a pod prefixed with "cluster-autoscaler" running.</span></span> <span data-ttu-id="b83bb-141">If you see this, your cluster autoscaler has been deployed.</span><span class="sxs-lookup"><span data-stu-id="b83bb-141">If you see this, your cluster autoscaler has been deployed.</span></span>

```console
kubectl -n kube-system get pods
```

<span data-ttu-id="b83bb-142">To view the status of the cluster autoscaler, run</span><span class="sxs-lookup"><span data-stu-id="b83bb-142">To view the status of the cluster autoscaler, run</span></span>

```console
kubectl -n kube-system describe configmap cluster-autoscaler-status
```

## <a name="interpreting-the-cluster-autoscaler-status"></a><span data-ttu-id="b83bb-143">Interpreting the cluster autoscaler status</span><span class="sxs-lookup"><span data-stu-id="b83bb-143">Interpreting the cluster autoscaler status</span></span>

```console
$ kubectl -n kube-system describe configmap cluster-autoscaler-status
Name:         cluster-autoscaler-status
Namespace:    kube-system
Labels:       <none>
Annotations:  cluster-autoscaler.kubernetes.io/last-updated=2018-07-25 22:59:22.661669494 +0000 UTC

Data
====
status:
----
Cluster-autoscaler status at 2018-07-25 22:59:22.661669494 +0000 UTC:
Cluster-wide:
  Health:      Healthy (ready=1 unready=0 notStarted=0 longNotStarted=0 registered=1 longUnregistered=0)
               LastProbeTime:      2018-07-25 22:59:22.067828801 +0000 UTC
               LastTransitionTime: 2018-07-25 00:38:36.41372897 +0000 UTC
  ScaleUp:     NoActivity (ready=1 registered=1)
               LastProbeTime:      2018-07-25 22:59:22.067828801 +0000 UTC
               LastTransitionTime: 2018-07-25 00:38:36.41372897 +0000 UTC
  ScaleDown:   NoCandidates (candidates=0)
               LastProbeTime:      2018-07-25 22:59:22.067828801 +0000 UTC
               LastTransitionTime: 2018-07-25 00:38:36.41372897 +0000 UTC

NodeGroups:
  Name:        nodepool1
  Health:      Healthy (ready=1 unready=0 notStarted=0 longNotStarted=0 registered=1 longUnregistered=0 cloudProviderTarget=1 (minSize=1, maxSize=5))
               LastProbeTime:      2018-07-25 22:59:22.067828801 +0000 UTC
               LastTransitionTime: 2018-07-25 00:38:36.41372897 +0000 UTC
  ScaleUp:     NoActivity (ready=1 cloudProviderTarget=1)
               LastProbeTime:      2018-07-25 22:59:22.067828801 +0000 UTC
               LastTransitionTime: 2018-07-25 00:38:36.41372897 +0000 UTC
  ScaleDown:   NoCandidates (candidates=0)
               LastProbeTime:      2018-07-25 22:59:22.067828801 +0000 UTC
               LastTransitionTime: 2018-07-25 00:38:36.41372897 +0000 UTC


Events:  <none>
```

<span data-ttu-id="b83bb-144">The cluster autoscaler status allows you to see the state of the cluster autoscaler on two different levels: cluster-wide and within each node group.</span><span class="sxs-lookup"><span data-stu-id="b83bb-144">The cluster autoscaler status allows you to see the state of the cluster autoscaler on two different levels: cluster-wide and within each node group.</span></span> <span data-ttu-id="b83bb-145">Since AKS currently only supports one node pool, these metrics are the same.</span><span class="sxs-lookup"><span data-stu-id="b83bb-145">Since AKS currently only supports one node pool, these metrics are the same.</span></span>

* <span data-ttu-id="b83bb-146">Health indicates the overall health of the nodes.</span><span class="sxs-lookup"><span data-stu-id="b83bb-146">Health indicates the overall health of the nodes.</span></span> <span data-ttu-id="b83bb-147">If the cluster autoscaler struggles to create or removes nodes in the cluster, this status will change to "Unhealthy".</span><span class="sxs-lookup"><span data-stu-id="b83bb-147">If the cluster autoscaler struggles to create or removes nodes in the cluster, this status will change to "Unhealthy".</span></span> <span data-ttu-id="b83bb-148">There's also a breakdown of the status of different nodes:</span><span class="sxs-lookup"><span data-stu-id="b83bb-148">There's also a breakdown of the status of different nodes:</span></span>
    * <span data-ttu-id="b83bb-149">"Ready" means a node is a ready to have pods scheduled on it.</span><span class="sxs-lookup"><span data-stu-id="b83bb-149">"Ready" means a node is a ready to have pods scheduled on it.</span></span>
    * <span data-ttu-id="b83bb-150">"Unready" means a node that broke down after it started.</span><span class="sxs-lookup"><span data-stu-id="b83bb-150">"Unready" means a node that broke down after it started.</span></span>
    * <span data-ttu-id="b83bb-151">"NotStarted" means a node isn't fully started yet.</span><span class="sxs-lookup"><span data-stu-id="b83bb-151">"NotStarted" means a node isn't fully started yet.</span></span>
    * <span data-ttu-id="b83bb-152">"LongNotStarted" means a node failed to start within a reasonable limit.</span><span class="sxs-lookup"><span data-stu-id="b83bb-152">"LongNotStarted" means a node failed to start within a reasonable limit.</span></span>
    * <span data-ttu-id="b83bb-153">"Registered means a node is registered in the group</span><span class="sxs-lookup"><span data-stu-id="b83bb-153">"Registered means a node is registered in the group</span></span>
    * <span data-ttu-id="b83bb-154">"Unregistered" means a node is present on the cluster provider side but failed to register in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="b83bb-154">"Unregistered" means a node is present on the cluster provider side but failed to register in Kubernetes.</span></span>
  
* <span data-ttu-id="b83bb-155">ScaleUp allows you to check when the cluster determines a scale up should occur in your cluster.</span><span class="sxs-lookup"><span data-stu-id="b83bb-155">ScaleUp allows you to check when the cluster determines a scale up should occur in your cluster.</span></span>
    * <span data-ttu-id="b83bb-156">A transition is when the number of nodes in the cluster changes or the status of a node changes.</span><span class="sxs-lookup"><span data-stu-id="b83bb-156">A transition is when the number of nodes in the cluster changes or the status of a node changes.</span></span>
    * <span data-ttu-id="b83bb-157">The number of ready nodes is the number of nodes available and ready in the cluster.</span><span class="sxs-lookup"><span data-stu-id="b83bb-157">The number of ready nodes is the number of nodes available and ready in the cluster.</span></span> 
    * <span data-ttu-id="b83bb-158">The cloudProviderTarget is the number of nodes the cluster autoscaler has determined the cluster needs to handle its workload.</span><span class="sxs-lookup"><span data-stu-id="b83bb-158">The cloudProviderTarget is the number of nodes the cluster autoscaler has determined the cluster needs to handle its workload.</span></span>

* <span data-ttu-id="b83bb-159">ScaleDown allows you to check if there are candidates for scale down.</span><span class="sxs-lookup"><span data-stu-id="b83bb-159">ScaleDown allows you to check if there are candidates for scale down.</span></span> 
    * <span data-ttu-id="b83bb-160">A candidate for scale down is a node the cluster autoscaler has determined can be removed without affecting the cluster's ability to handle its workload.</span><span class="sxs-lookup"><span data-stu-id="b83bb-160">A candidate for scale down is a node the cluster autoscaler has determined can be removed without affecting the cluster's ability to handle its workload.</span></span> 
    * <span data-ttu-id="b83bb-161">The times provided show the last time the cluster was checked for scale down candidates and its last transition time.</span><span class="sxs-lookup"><span data-stu-id="b83bb-161">The times provided show the last time the cluster was checked for scale down candidates and its last transition time.</span></span>

<span data-ttu-id="b83bb-162">Finally, under Events, you can see up any scale or scale down events, failed or successful, and their times, that the cluster autoscaler has carried out.</span><span class="sxs-lookup"><span data-stu-id="b83bb-162">Finally, under Events, you can see up any scale or scale down events, failed or successful, and their times, that the cluster autoscaler has carried out.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b83bb-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="b83bb-163">Next steps</span></span>

<span data-ttu-id="b83bb-164">To use the cluster autoscaler with the horizontal pod autoscaler, check out [scaling Kubernetes application and infrastructure][aks-tutorial-scale].</span><span class="sxs-lookup"><span data-stu-id="b83bb-164">To use the cluster autoscaler with the horizontal pod autoscaler, check out [scaling Kubernetes application and infrastructure][aks-tutorial-scale].</span></span>

<span data-ttu-id="b83bb-165">Learn more about deploying and managing AKS with the AKS tutorials.</span><span class="sxs-lookup"><span data-stu-id="b83bb-165">Learn more about deploying and managing AKS with the AKS tutorials.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="b83bb-166">[AKS Tutorial][aks-tutorial-prepare-app]</span><span class="sxs-lookup"><span data-stu-id="b83bb-166">[AKS Tutorial][aks-tutorial-prepare-app]</span></span>

<!-- LINKS - internal -->
[aks-quick-start]: ./kubernetes-walkthrough.md
[aks-tutorial-prepare-app]: ./tutorial-kubernetes-prepare-app.md
[aks-tutorial-scale]: ./tutorial-kubernetes-scale.md
[aks-upgrade]: ./upgrade-cluster.md

<!-- LINKS - external -->
[cluster-autoscale]: https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md
