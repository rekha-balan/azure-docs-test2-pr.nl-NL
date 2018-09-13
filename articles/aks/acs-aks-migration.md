---
title: Migrating from Azure Container Service (ACS) to Azure Kubernetes Service (AKS)
description: Migrating from Azure Container Service (ACS) to Azure Kubernetes Service (AKS)
services: container-service
author: noelbundick
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 06/13/2018
ms.author: nobun
ms.custom: mvc
ms.openlocfilehash: cb143998ac46f7f86b2dbf47b69cee7843418f5d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865586"
---
# <a name="migrating-from-azure-container-service-acs-to-azure-kubernetes-service-aks"></a><span data-ttu-id="1c95b-103">Migrating from Azure Container Service (ACS) to Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="1c95b-103">Migrating from Azure Container Service (ACS) to Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="1c95b-104">The goal of this document is to help you plan and execute a successful migration between Azure Container Service with Kubernetes (ACS) and Azure Kubernetes Service (AKS).</span><span class="sxs-lookup"><span data-stu-id="1c95b-104">The goal of this document is to help you plan and execute a successful migration between Azure Container Service with Kubernetes (ACS) and Azure Kubernetes Service (AKS).</span></span> <span data-ttu-id="1c95b-105">This guide details the differences between ACS and AKS, provides an overview of the migration process, and should help you make key decisions.</span><span class="sxs-lookup"><span data-stu-id="1c95b-105">This guide details the differences between ACS and AKS, provides an overview of the migration process, and should help you make key decisions.</span></span>

## <a name="differences-between-acs-and-aks"></a><span data-ttu-id="1c95b-106">Differences between ACS and AKS</span><span class="sxs-lookup"><span data-stu-id="1c95b-106">Differences between ACS and AKS</span></span>

<span data-ttu-id="1c95b-107">ACS and AKS differ in some key areas that impact migration.</span><span class="sxs-lookup"><span data-stu-id="1c95b-107">ACS and AKS differ in some key areas that impact migration.</span></span> <span data-ttu-id="1c95b-108">You should review and plan to address the following differences before any migration.</span><span class="sxs-lookup"><span data-stu-id="1c95b-108">You should review and plan to address the following differences before any migration.</span></span>

* <span data-ttu-id="1c95b-109">AKS nodes use [Managed Disks](../virtual-machines/windows/managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1c95b-109">AKS nodes use [Managed Disks](../virtual-machines/windows/managed-disks-overview.md)</span></span>
    * <span data-ttu-id="1c95b-110">Unmanaged disks will need to be converted before they can be attached to AKS nodes</span><span class="sxs-lookup"><span data-stu-id="1c95b-110">Unmanaged disks will need to be converted before they can be attached to AKS nodes</span></span>
    * <span data-ttu-id="1c95b-111">Custom `StorageClass` objects for Azure disks will need to be changed from `unmanaged` to `managed`</span><span class="sxs-lookup"><span data-stu-id="1c95b-111">Custom `StorageClass` objects for Azure disks will need to be changed from `unmanaged` to `managed`</span></span>
    * <span data-ttu-id="1c95b-112">Any `PersistentVolumes` will need to use `kind: Managed`</span><span class="sxs-lookup"><span data-stu-id="1c95b-112">Any `PersistentVolumes` will need to use `kind: Managed`</span></span>
* <span data-ttu-id="1c95b-113">AKS currently supports only one agent pool</span><span class="sxs-lookup"><span data-stu-id="1c95b-113">AKS currently supports only one agent pool</span></span>
* <span data-ttu-id="1c95b-114">Windows Server-based nodes are currently in [private preview](https://azure.microsoft.com/en-us/blog/kubernetes-on-azure/)</span><span class="sxs-lookup"><span data-stu-id="1c95b-114">Windows Server-based nodes are currently in [private preview](https://azure.microsoft.com/en-us/blog/kubernetes-on-azure/)</span></span>
* <span data-ttu-id="1c95b-115">Check the list of AKS [supported regions](https://docs.microsoft.com/azure/aks/container-service-quotas)</span><span class="sxs-lookup"><span data-stu-id="1c95b-115">Check the list of AKS [supported regions](https://docs.microsoft.com/azure/aks/container-service-quotas)</span></span>
* <span data-ttu-id="1c95b-116">AKS is a managed service with a hosted Kubernetes control plane.</span><span class="sxs-lookup"><span data-stu-id="1c95b-116">AKS is a managed service with a hosted Kubernetes control plane.</span></span> <span data-ttu-id="1c95b-117">You may need to modify your applications if you've previously modified the configuration of your ACS masters</span><span class="sxs-lookup"><span data-stu-id="1c95b-117">You may need to modify your applications if you've previously modified the configuration of your ACS masters</span></span>

### <a name="differences-between-kubernetes-versions"></a><span data-ttu-id="1c95b-118">Differences between Kubernetes versions</span><span class="sxs-lookup"><span data-stu-id="1c95b-118">Differences between Kubernetes versions</span></span>

<span data-ttu-id="1c95b-119">If you're migrating to a newer version of Kubernetes (ex: 1.7.x to 1.9.x), there are a few changes to the k8s API that will require your attention.</span><span class="sxs-lookup"><span data-stu-id="1c95b-119">If you're migrating to a newer version of Kubernetes (ex: 1.7.x to 1.9.x), there are a few changes to the k8s API that will require your attention.</span></span>

* [<span data-ttu-id="1c95b-120">Migrate a ThirdPartyResource to CustomResourceDefinition</span><span class="sxs-lookup"><span data-stu-id="1c95b-120">Migrate a ThirdPartyResource to CustomResourceDefinition</span></span>](https://kubernetes.io/docs/tasks/access-kubernetes-api/migrate-third-party-resource/)
* <span data-ttu-id="1c95b-121">[Workloads API changes in versions 1.8 and 1.9](https://kubernetes.io/docs/reference/workloads-18-19/).</span><span class="sxs-lookup"><span data-stu-id="1c95b-121">[Workloads API changes in versions 1.8 and 1.9](https://kubernetes.io/docs/reference/workloads-18-19/).</span></span>

## <a name="migration-considerations"></a><span data-ttu-id="1c95b-122">Migration considerations</span><span class="sxs-lookup"><span data-stu-id="1c95b-122">Migration considerations</span></span>

### <a name="agent-pools"></a><span data-ttu-id="1c95b-123">Agent Pools</span><span class="sxs-lookup"><span data-stu-id="1c95b-123">Agent Pools</span></span>

<span data-ttu-id="1c95b-124">While AKS manages the Kubernetes control plane, you still define the size and number of nodes you want to include in your new cluster.</span><span class="sxs-lookup"><span data-stu-id="1c95b-124">While AKS manages the Kubernetes control plane, you still define the size and number of nodes you want to include in your new cluster.</span></span> <span data-ttu-id="1c95b-125">Assuming you want a 1:1 mapping from ACS to AKS, you'll want to capture your existing ACS node information.</span><span class="sxs-lookup"><span data-stu-id="1c95b-125">Assuming you want a 1:1 mapping from ACS to AKS, you'll want to capture your existing ACS node information.</span></span> <span data-ttu-id="1c95b-126">You'll use this data when creating your new AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="1c95b-126">You'll use this data when creating your new AKS cluster.</span></span>

<span data-ttu-id="1c95b-127">Example:</span><span class="sxs-lookup"><span data-stu-id="1c95b-127">Example:</span></span>

| <span data-ttu-id="1c95b-128">Name</span><span class="sxs-lookup"><span data-stu-id="1c95b-128">Name</span></span> | <span data-ttu-id="1c95b-129">Count</span><span class="sxs-lookup"><span data-stu-id="1c95b-129">Count</span></span> | <span data-ttu-id="1c95b-130">VM Size</span><span class="sxs-lookup"><span data-stu-id="1c95b-130">VM Size</span></span> | <span data-ttu-id="1c95b-131">Operating System</span><span class="sxs-lookup"><span data-stu-id="1c95b-131">Operating System</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1c95b-132">agentpool0</span><span class="sxs-lookup"><span data-stu-id="1c95b-132">agentpool0</span></span> | <span data-ttu-id="1c95b-133">3</span><span class="sxs-lookup"><span data-stu-id="1c95b-133">3</span></span> | <span data-ttu-id="1c95b-134">Standard_D8_v2</span><span class="sxs-lookup"><span data-stu-id="1c95b-134">Standard_D8_v2</span></span> | <span data-ttu-id="1c95b-135">Linux</span><span class="sxs-lookup"><span data-stu-id="1c95b-135">Linux</span></span> |
| <span data-ttu-id="1c95b-136">agentpool1</span><span class="sxs-lookup"><span data-stu-id="1c95b-136">agentpool1</span></span> | <span data-ttu-id="1c95b-137">1</span><span class="sxs-lookup"><span data-stu-id="1c95b-137">1</span></span> | <span data-ttu-id="1c95b-138">Standard_D2_v2</span><span class="sxs-lookup"><span data-stu-id="1c95b-138">Standard_D2_v2</span></span> | <span data-ttu-id="1c95b-139">Windows</span><span class="sxs-lookup"><span data-stu-id="1c95b-139">Windows</span></span> |

<span data-ttu-id="1c95b-140">Because additional virtual machines will be deployed into your subscription during migration, you should verify that your quotas and limits are sufficient for these resources.</span><span class="sxs-lookup"><span data-stu-id="1c95b-140">Because additional virtual machines will be deployed into your subscription during migration, you should verify that your quotas and limits are sufficient for these resources.</span></span> <span data-ttu-id="1c95b-141">You can learn more by reviewing [Azure subscription and service limits](https://docs.microsoft.com/en-us/azure/azure-subscription-service-limits).</span><span class="sxs-lookup"><span data-stu-id="1c95b-141">You can learn more by reviewing [Azure subscription and service limits](https://docs.microsoft.com/en-us/azure/azure-subscription-service-limits).</span></span> <span data-ttu-id="1c95b-142">To check your current quotas, go to the [subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in the Azure portal, select your subscription, then select `Usage + quotas`.</span><span class="sxs-lookup"><span data-stu-id="1c95b-142">To check your current quotas, go to the [subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in the Azure portal, select your subscription, then select `Usage + quotas`.</span></span>

### <a name="networking"></a><span data-ttu-id="1c95b-143">Networking</span><span class="sxs-lookup"><span data-stu-id="1c95b-143">Networking</span></span>

<span data-ttu-id="1c95b-144">For complex applications, you'll typically migrate over time rather than all at once.</span><span class="sxs-lookup"><span data-stu-id="1c95b-144">For complex applications, you'll typically migrate over time rather than all at once.</span></span> <span data-ttu-id="1c95b-145">That means that the old and new environments may need to communicate over the network.</span><span class="sxs-lookup"><span data-stu-id="1c95b-145">That means that the old and new environments may need to communicate over the network.</span></span> <span data-ttu-id="1c95b-146">Applications that were previously able to use `ClusterIP` services to communicate may need to be exposed as type `LoadBalancer` and secured appropriately.</span><span class="sxs-lookup"><span data-stu-id="1c95b-146">Applications that were previously able to use `ClusterIP` services to communicate may need to be exposed as type `LoadBalancer` and secured appropriately.</span></span>

<span data-ttu-id="1c95b-147">To complete the migration, you'll want to point clients to the new services running on AKS.</span><span class="sxs-lookup"><span data-stu-id="1c95b-147">To complete the migration, you'll want to point clients to the new services running on AKS.</span></span> <span data-ttu-id="1c95b-148">The recommended way to redirect traffic is by updating DNS to point to the Load Balancer that sits in front of your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="1c95b-148">The recommended way to redirect traffic is by updating DNS to point to the Load Balancer that sits in front of your AKS cluster.</span></span>

### <a name="stateless-applications"></a><span data-ttu-id="1c95b-149">Stateless Applications</span><span class="sxs-lookup"><span data-stu-id="1c95b-149">Stateless Applications</span></span>

<span data-ttu-id="1c95b-150">Stateless application migration is the most straightforward case.</span><span class="sxs-lookup"><span data-stu-id="1c95b-150">Stateless application migration is the most straightforward case.</span></span> <span data-ttu-id="1c95b-151">You'll apply your YAML definitions to the new cluster, validate that everything is working as expected, and redirect traffic to make your new cluster active.</span><span class="sxs-lookup"><span data-stu-id="1c95b-151">You'll apply your YAML definitions to the new cluster, validate that everything is working as expected, and redirect traffic to make your new cluster active.</span></span>

### <a name="stateful-applications"></a><span data-ttu-id="1c95b-152">Stateful Applications</span><span class="sxs-lookup"><span data-stu-id="1c95b-152">Stateful Applications</span></span>

<span data-ttu-id="1c95b-153">Migrating stateful applications requires careful planning to avoid data loss or unexpected downtime.</span><span class="sxs-lookup"><span data-stu-id="1c95b-153">Migrating stateful applications requires careful planning to avoid data loss or unexpected downtime.</span></span>

#### <a name="highly-available-applications"></a><span data-ttu-id="1c95b-154">Highly Available Applications</span><span class="sxs-lookup"><span data-stu-id="1c95b-154">Highly Available Applications</span></span>

<span data-ttu-id="1c95b-155">Some stateful applications can be deployed in a high availability configuration and can copy data across replicas.</span><span class="sxs-lookup"><span data-stu-id="1c95b-155">Some stateful applications can be deployed in a high availability configuration and can copy data across replicas.</span></span> <span data-ttu-id="1c95b-156">If this describes your current deployment, it may be possible to create a new member on the new AKS cluster, and migrate with minimal impact to downstream callers.</span><span class="sxs-lookup"><span data-stu-id="1c95b-156">If this describes your current deployment, it may be possible to create a new member on the new AKS cluster, and migrate with minimal impact to downstream callers.</span></span> <span data-ttu-id="1c95b-157">The migration steps for this scenario generally are:</span><span class="sxs-lookup"><span data-stu-id="1c95b-157">The migration steps for this scenario generally are:</span></span>

1. <span data-ttu-id="1c95b-158">Create a new secondary replica on AKS</span><span class="sxs-lookup"><span data-stu-id="1c95b-158">Create a new secondary replica on AKS</span></span>
2. <span data-ttu-id="1c95b-159">Wait for data to replicate</span><span class="sxs-lookup"><span data-stu-id="1c95b-159">Wait for data to replicate</span></span>
3. <span data-ttu-id="1c95b-160">Fail over to make secondary replica the new primary</span><span class="sxs-lookup"><span data-stu-id="1c95b-160">Fail over to make secondary replica the new primary</span></span>
4. <span data-ttu-id="1c95b-161">Point traffic to the AKS cluster</span><span class="sxs-lookup"><span data-stu-id="1c95b-161">Point traffic to the AKS cluster</span></span>

#### <a name="migrating-persistent-volumes"></a><span data-ttu-id="1c95b-162">Migrating Persistent Volumes</span><span class="sxs-lookup"><span data-stu-id="1c95b-162">Migrating Persistent Volumes</span></span>

<span data-ttu-id="1c95b-163">There are several factors to consider if you're migrating existing Persistent Volumes to AKS.</span><span class="sxs-lookup"><span data-stu-id="1c95b-163">There are several factors to consider if you're migrating existing Persistent Volumes to AKS.</span></span> <span data-ttu-id="1c95b-164">Generally, the steps involved are:</span><span class="sxs-lookup"><span data-stu-id="1c95b-164">Generally, the steps involved are:</span></span>

1. <span data-ttu-id="1c95b-165">(Optional) Quiesce writes to the application (requires downtime)</span><span class="sxs-lookup"><span data-stu-id="1c95b-165">(Optional) Quiesce writes to the application (requires downtime)</span></span>
2. <span data-ttu-id="1c95b-166">Snapshot disks</span><span class="sxs-lookup"><span data-stu-id="1c95b-166">Snapshot disks</span></span>
3. <span data-ttu-id="1c95b-167">Create new Managed Disks from snapshots</span><span class="sxs-lookup"><span data-stu-id="1c95b-167">Create new Managed Disks from snapshots</span></span>
4. <span data-ttu-id="1c95b-168">Create Persistent Volumes in AKS</span><span class="sxs-lookup"><span data-stu-id="1c95b-168">Create Persistent Volumes in AKS</span></span>
5. <span data-ttu-id="1c95b-169">Update Pod specifications to [use existing volumes](https://docs.microsoft.com/en-us/azure/aks/azure-disk-volume) rather than PersistentVolumeClaims (static provisioning)</span><span class="sxs-lookup"><span data-stu-id="1c95b-169">Update Pod specifications to [use existing volumes](https://docs.microsoft.com/en-us/azure/aks/azure-disk-volume) rather than PersistentVolumeClaims (static provisioning)</span></span>
6. <span data-ttu-id="1c95b-170">Deploy application to AKS</span><span class="sxs-lookup"><span data-stu-id="1c95b-170">Deploy application to AKS</span></span>
7. <span data-ttu-id="1c95b-171">Validate</span><span class="sxs-lookup"><span data-stu-id="1c95b-171">Validate</span></span>
8. <span data-ttu-id="1c95b-172">Point traffic to the AKS cluster</span><span class="sxs-lookup"><span data-stu-id="1c95b-172">Point traffic to the AKS cluster</span></span>

> <span data-ttu-id="1c95b-173">**Important**: If you choose not to quiesce writes, you'll need to replicate data to the new deployment, as you'll be missing data that was written since the disk snapshot</span><span class="sxs-lookup"><span data-stu-id="1c95b-173">**Important**: If you choose not to quiesce writes, you'll need to replicate data to the new deployment, as you'll be missing data that was written since the disk snapshot</span></span>

<span data-ttu-id="1c95b-174">Open-source tools exist that can help you create Managed Disks and migrate volumes between Kubernetes clusters.</span><span class="sxs-lookup"><span data-stu-id="1c95b-174">Open-source tools exist that can help you create Managed Disks and migrate volumes between Kubernetes clusters.</span></span>

* <span data-ttu-id="1c95b-175">[noelbundick/azure-cli-disk-extension](https://github.com/noelbundick/azure-cli-disk-copy-extension) - copy and convert disks across Resource Groups and Azure regions</span><span class="sxs-lookup"><span data-stu-id="1c95b-175">[noelbundick/azure-cli-disk-extension](https://github.com/noelbundick/azure-cli-disk-copy-extension) - copy and convert disks across Resource Groups and Azure regions</span></span>
* <span data-ttu-id="1c95b-176">[yaron2/azure-kube-cli](https://github.com/yaron2/azure-kube-cli) - enumerate ACS Kubernetes volumes and migrate them to an AKS cluster</span><span class="sxs-lookup"><span data-stu-id="1c95b-176">[yaron2/azure-kube-cli](https://github.com/yaron2/azure-kube-cli) - enumerate ACS Kubernetes volumes and migrate them to an AKS cluster</span></span>

#### <a name="azure-files"></a><span data-ttu-id="1c95b-177">Azure Files</span><span class="sxs-lookup"><span data-stu-id="1c95b-177">Azure Files</span></span>

<span data-ttu-id="1c95b-178">Unlike disks, Azure Files can be mounted to multiple hosts concurrently.</span><span class="sxs-lookup"><span data-stu-id="1c95b-178">Unlike disks, Azure Files can be mounted to multiple hosts concurrently.</span></span> <span data-ttu-id="1c95b-179">Neither Azure nor Kubernetes prevents you from creating a Pod in your AKS cluster that is still being used by your ACS cluster.</span><span class="sxs-lookup"><span data-stu-id="1c95b-179">Neither Azure nor Kubernetes prevents you from creating a Pod in your AKS cluster that is still being used by your ACS cluster.</span></span> <span data-ttu-id="1c95b-180">To prevent data loss and unexpected behavior, you should ensure that both clusters aren't writing to the same files at the same time.</span><span class="sxs-lookup"><span data-stu-id="1c95b-180">To prevent data loss and unexpected behavior, you should ensure that both clusters aren't writing to the same files at the same time.</span></span>

<span data-ttu-id="1c95b-181">If your application can host multiple replicas pointing to the same file share, you can follow the stateless migration steps and deploy your YAML definitions to your new cluster.</span><span class="sxs-lookup"><span data-stu-id="1c95b-181">If your application can host multiple replicas pointing to the same file share, you can follow the stateless migration steps and deploy your YAML definitions to your new cluster.</span></span>

<span data-ttu-id="1c95b-182">If not, one possible migration approach involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="1c95b-182">If not, one possible migration approach involves the following steps:</span></span>

1. <span data-ttu-id="1c95b-183">Deploy your application to AKS with a replica count of 0</span><span class="sxs-lookup"><span data-stu-id="1c95b-183">Deploy your application to AKS with a replica count of 0</span></span>
2. <span data-ttu-id="1c95b-184">Scale the application on ACS to 0 (requires downtime)</span><span class="sxs-lookup"><span data-stu-id="1c95b-184">Scale the application on ACS to 0 (requires downtime)</span></span>
3. <span data-ttu-id="1c95b-185">Scale the application on AKS up to 1</span><span class="sxs-lookup"><span data-stu-id="1c95b-185">Scale the application on AKS up to 1</span></span>
4. <span data-ttu-id="1c95b-186">Validate</span><span class="sxs-lookup"><span data-stu-id="1c95b-186">Validate</span></span>
5. <span data-ttu-id="1c95b-187">Point traffic to the AKS cluster</span><span class="sxs-lookup"><span data-stu-id="1c95b-187">Point traffic to the AKS cluster</span></span>

<span data-ttu-id="1c95b-188">In cases where you'd like to start with an empty share, then make a copy of the source data, you can use the [`az storage file copy`](https://docs.microsoft.com/en-us/cli/azure/storage/file/copy?view=azure-cli-latest) commands to migrate your data.</span><span class="sxs-lookup"><span data-stu-id="1c95b-188">In cases where you'd like to start with an empty share, then make a copy of the source data, you can use the [`az storage file copy`](https://docs.microsoft.com/en-us/cli/azure/storage/file/copy?view=azure-cli-latest) commands to migrate your data.</span></span>

### <a name="deployment-strategy"></a><span data-ttu-id="1c95b-189">Deployment Strategy</span><span class="sxs-lookup"><span data-stu-id="1c95b-189">Deployment Strategy</span></span>

<span data-ttu-id="1c95b-190">The recommended method is to use your existing CI/CD pipeline to deploy a known-good configuration to AKS.</span><span class="sxs-lookup"><span data-stu-id="1c95b-190">The recommended method is to use your existing CI/CD pipeline to deploy a known-good configuration to AKS.</span></span> <span data-ttu-id="1c95b-191">You'll clone your existing deploy tasks, and ensure that your `kubeconfig` points to the new AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="1c95b-191">You'll clone your existing deploy tasks, and ensure that your `kubeconfig` points to the new AKS cluster.</span></span>

<span data-ttu-id="1c95b-192">In cases where that's not possible, you'll need to export resource definition from ACS, and then apply them to AKS.</span><span class="sxs-lookup"><span data-stu-id="1c95b-192">In cases where that's not possible, you'll need to export resource definition from ACS, and then apply them to AKS.</span></span> <span data-ttu-id="1c95b-193">You can use `kubectl` to export objects.</span><span class="sxs-lookup"><span data-stu-id="1c95b-193">You can use `kubectl` to export objects.</span></span>

```console
kubectl get deployment -o=yaml --export > deployments.yaml
```

<span data-ttu-id="1c95b-194">There are also several open-source tools that can help, depending on your needs:</span><span class="sxs-lookup"><span data-stu-id="1c95b-194">There are also several open-source tools that can help, depending on your needs:</span></span>

* <span data-ttu-id="1c95b-195">[heptio/ark](https://github.com/heptio/ark) - requires k8s 1.7</span><span class="sxs-lookup"><span data-stu-id="1c95b-195">[heptio/ark](https://github.com/heptio/ark) - requires k8s 1.7</span></span>
* [<span data-ttu-id="1c95b-196">yaron2/azure-kube-cli</span><span class="sxs-lookup"><span data-stu-id="1c95b-196">yaron2/azure-kube-cli</span></span>](https://github.com/yaron2/azure-kube-cli)
* [<span data-ttu-id="1c95b-197">mhausenblas/reshifter</span><span class="sxs-lookup"><span data-stu-id="1c95b-197">mhausenblas/reshifter</span></span>](https://github.com/mhausenblas/reshifter)

## <a name="migration-steps"></a><span data-ttu-id="1c95b-198">Migration steps</span><span class="sxs-lookup"><span data-stu-id="1c95b-198">Migration steps</span></span>

### <a name="1-create-an-aks-cluster"></a><span data-ttu-id="1c95b-199">1. Create an AKS cluster</span><span class="sxs-lookup"><span data-stu-id="1c95b-199">1. Create an AKS cluster</span></span>

<span data-ttu-id="1c95b-200">You can follow the docs to [create an AKS cluster](https://docs.microsoft.com/en-us/azure/aks/create-cluster) via the Azure portal, Azure CLI, or Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="1c95b-200">You can follow the docs to [create an AKS cluster](https://docs.microsoft.com/en-us/azure/aks/create-cluster) via the Azure portal, Azure CLI, or Resource Manager template.</span></span>

> <span data-ttu-id="1c95b-201">You can find sample Azure Resource Manager templates for AKS at the [Azure/AKS](https://github.com/Azure/AKS/tree/master/examples/vnet) repository on GitHub</span><span class="sxs-lookup"><span data-stu-id="1c95b-201">You can find sample Azure Resource Manager templates for AKS at the [Azure/AKS](https://github.com/Azure/AKS/tree/master/examples/vnet) repository on GitHub</span></span>

### <a name="2-modify-applications"></a><span data-ttu-id="1c95b-202">2. Modify applications</span><span class="sxs-lookup"><span data-stu-id="1c95b-202">2. Modify applications</span></span>

<span data-ttu-id="1c95b-203">Make any necessary modifications to your YAML definitions.</span><span class="sxs-lookup"><span data-stu-id="1c95b-203">Make any necessary modifications to your YAML definitions.</span></span> <span data-ttu-id="1c95b-204">Ex: replacing `apps/v1beta1` with `apps/v1` for `Deployments`</span><span class="sxs-lookup"><span data-stu-id="1c95b-204">Ex: replacing `apps/v1beta1` with `apps/v1` for `Deployments`</span></span>

### <a name="3-optional-migrate-volumes"></a><span data-ttu-id="1c95b-205">3. (Optional) Migrate volumes</span><span class="sxs-lookup"><span data-stu-id="1c95b-205">3. (Optional) Migrate volumes</span></span>

<span data-ttu-id="1c95b-206">Migrate volumes from your ACS cluster to your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="1c95b-206">Migrate volumes from your ACS cluster to your AKS cluster.</span></span> <span data-ttu-id="1c95b-207">More details can be found in the [Migrating Persistent Volumes](#Migrating-Persistent-Volumes) section.</span><span class="sxs-lookup"><span data-stu-id="1c95b-207">More details can be found in the [Migrating Persistent Volumes](#Migrating-Persistent-Volumes) section.</span></span>

### <a name="4-deploy-applications"></a><span data-ttu-id="1c95b-208">4. Deploy applications</span><span class="sxs-lookup"><span data-stu-id="1c95b-208">4. Deploy applications</span></span>

<span data-ttu-id="1c95b-209">Use your CI/CD system to deploy applications to AKS or use kubectl to apply the YAML definitions.</span><span class="sxs-lookup"><span data-stu-id="1c95b-209">Use your CI/CD system to deploy applications to AKS or use kubectl to apply the YAML definitions.</span></span>

### <a name="5-validate"></a><span data-ttu-id="1c95b-210">5. Validate</span><span class="sxs-lookup"><span data-stu-id="1c95b-210">5. Validate</span></span>

<span data-ttu-id="1c95b-211">Validate that your applications are working as expected and that any migrated data has been copied over.</span><span class="sxs-lookup"><span data-stu-id="1c95b-211">Validate that your applications are working as expected and that any migrated data has been copied over.</span></span>

### <a name="6-redirect-traffic"></a><span data-ttu-id="1c95b-212">6. Redirect traffic</span><span class="sxs-lookup"><span data-stu-id="1c95b-212">6. Redirect traffic</span></span>

<span data-ttu-id="1c95b-213">Update DNS to point clients to your AKS deployment.</span><span class="sxs-lookup"><span data-stu-id="1c95b-213">Update DNS to point clients to your AKS deployment.</span></span>

### <a name="7-post-migration-tasks"></a><span data-ttu-id="1c95b-214">7. Post-migration tasks</span><span class="sxs-lookup"><span data-stu-id="1c95b-214">7. Post-migration tasks</span></span>

<span data-ttu-id="1c95b-215">If you migrated volumes and chose not to quiesce writes, you'll need to copy that data to the new cluster.</span><span class="sxs-lookup"><span data-stu-id="1c95b-215">If you migrated volumes and chose not to quiesce writes, you'll need to copy that data to the new cluster.</span></span>
