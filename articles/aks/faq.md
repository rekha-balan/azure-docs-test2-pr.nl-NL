---
title: Frequently asked questions for Azure Kubernetes Service (AKS)
description: Provides answers to some of the common questions about Azure Kubernetes Service (AKS).
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 08/17/2018
ms.author: iainfou
ms.openlocfilehash: f4bc7724c0bc288ab269d1b3ec054bd1a6ba26e3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856555"
---
# <a name="frequently-asked-questions-about-azure-kubernetes-service-aks"></a><span data-ttu-id="35a8c-103">Frequently asked questions about Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="35a8c-103">Frequently asked questions about Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="35a8c-104">This article addresses frequent questions about Azure Kubernetes Service (AKS).</span><span class="sxs-lookup"><span data-stu-id="35a8c-104">This article addresses frequent questions about Azure Kubernetes Service (AKS).</span></span>

## <a name="which-azure-regions-provide-the-azure-kubernetes-service-aks-today"></a><span data-ttu-id="35a8c-105">Which Azure regions provide the Azure Kubernetes Service (AKS) today?</span><span class="sxs-lookup"><span data-stu-id="35a8c-105">Which Azure regions provide the Azure Kubernetes Service (AKS) today?</span></span>

<span data-ttu-id="35a8c-106">For a complete list of available regions, see [AKS Regions and availability][aks-regions].</span><span class="sxs-lookup"><span data-stu-id="35a8c-106">For a complete list of available regions, see [AKS Regions and availability][aks-regions].</span></span>

## <a name="does-aks-support-node-autoscaling"></a><span data-ttu-id="35a8c-107">Does AKS support node autoscaling?</span><span class="sxs-lookup"><span data-stu-id="35a8c-107">Does AKS support node autoscaling?</span></span>

<span data-ttu-id="35a8c-108">Yes, autoscaling is available via the [Kubernetes autoscaler][auto-scaler] as of Kubernetes 1.10.</span><span class="sxs-lookup"><span data-stu-id="35a8c-108">Yes, autoscaling is available via the [Kubernetes autoscaler][auto-scaler] as of Kubernetes 1.10.</span></span> <span data-ttu-id="35a8c-109">For more information on how to configure and use the cluster autoscaler, see [Cluster autoscale on AKS][aks-cluster-autoscale].</span><span class="sxs-lookup"><span data-stu-id="35a8c-109">For more information on how to configure and use the cluster autoscaler, see [Cluster autoscale on AKS][aks-cluster-autoscale].</span></span>

## <a name="does-aks-support-kubernetes-role-based-access-control-rbac"></a><span data-ttu-id="35a8c-110">Does AKS support Kubernetes role-based access control (RBAC)?</span><span class="sxs-lookup"><span data-stu-id="35a8c-110">Does AKS support Kubernetes role-based access control (RBAC)?</span></span>

<span data-ttu-id="35a8c-111">Yes, Kubernetes RBAC is enabled by default when clusters are created with the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="35a8c-111">Yes, Kubernetes RBAC is enabled by default when clusters are created with the Azure CLI.</span></span> <span data-ttu-id="35a8c-112">RBAC can be enabled for clusters created using the Azure portal or templates.</span><span class="sxs-lookup"><span data-stu-id="35a8c-112">RBAC can be enabled for clusters created using the Azure portal or templates.</span></span>

## <a name="can-i-deploy-aks-into-my-existing-virtual-network"></a><span data-ttu-id="35a8c-113">Can I deploy AKS into my existing virtual network?</span><span class="sxs-lookup"><span data-stu-id="35a8c-113">Can I deploy AKS into my existing virtual network?</span></span>

<span data-ttu-id="35a8c-114">Yes, you can deploy an AKS cluster into an existing virtual network using the [advanced networking feature][aks-advanced-networking].</span><span class="sxs-lookup"><span data-stu-id="35a8c-114">Yes, you can deploy an AKS cluster into an existing virtual network using the [advanced networking feature][aks-advanced-networking].</span></span>

## <a name="can-i-restrict-the-kubernetes-api-server-to-only-be-accessible-within-my-virtual-network"></a><span data-ttu-id="35a8c-115">Can I restrict the Kubernetes API server to only be accessible within my virtual network?</span><span class="sxs-lookup"><span data-stu-id="35a8c-115">Can I restrict the Kubernetes API server to only be accessible within my virtual network?</span></span>

<span data-ttu-id="35a8c-116">Not at this time.</span><span class="sxs-lookup"><span data-stu-id="35a8c-116">Not at this time.</span></span> <span data-ttu-id="35a8c-117">The Kubernetes API server is exposed as a public fully qualified domain name (FQDN).</span><span class="sxs-lookup"><span data-stu-id="35a8c-117">The Kubernetes API server is exposed as a public fully qualified domain name (FQDN).</span></span> <span data-ttu-id="35a8c-118">You can control access to your cluster using [Kubernetes role-based access control (RBAC) and Azure Active Directory (AAD)][aks-rbac-aad]</span><span class="sxs-lookup"><span data-stu-id="35a8c-118">You can control access to your cluster using [Kubernetes role-based access control (RBAC) and Azure Active Directory (AAD)][aks-rbac-aad]</span></span>

## <a name="are-security-updates-applied-to-aks-agent-nodes"></a><span data-ttu-id="35a8c-119">Are security updates applied to AKS agent nodes?</span><span class="sxs-lookup"><span data-stu-id="35a8c-119">Are security updates applied to AKS agent nodes?</span></span>

<span data-ttu-id="35a8c-120">Yes, Azure automatically applies security patches to the nodes in your cluster on a nightly schedule.</span><span class="sxs-lookup"><span data-stu-id="35a8c-120">Yes, Azure automatically applies security patches to the nodes in your cluster on a nightly schedule.</span></span> <span data-ttu-id="35a8c-121">However, you are responsible for ensuring that nodes are rebooted as required.</span><span class="sxs-lookup"><span data-stu-id="35a8c-121">However, you are responsible for ensuring that nodes are rebooted as required.</span></span> <span data-ttu-id="35a8c-122">You have several options for performing node reboots:</span><span class="sxs-lookup"><span data-stu-id="35a8c-122">You have several options for performing node reboots:</span></span>

- <span data-ttu-id="35a8c-123">Manually, through the Azure portal or the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="35a8c-123">Manually, through the Azure portal or the Azure CLI.</span></span>
- <span data-ttu-id="35a8c-124">By upgrading your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="35a8c-124">By upgrading your AKS cluster.</span></span> <span data-ttu-id="35a8c-125">Cluster upgrades automatically [cordon and drain nodes][cordon-drain], then bring each node back up with the latest Ubuntu image and a new patch version or a minor Kubernetes version.</span><span class="sxs-lookup"><span data-stu-id="35a8c-125">Cluster upgrades automatically [cordon and drain nodes][cordon-drain], then bring each node back up with the latest Ubuntu image and a new patch version or a minor Kubernetes version.</span></span> <span data-ttu-id="35a8c-126">For more information, see [Upgrade an AKS cluster][aks-upgrade].</span><span class="sxs-lookup"><span data-stu-id="35a8c-126">For more information, see [Upgrade an AKS cluster][aks-upgrade].</span></span>
- <span data-ttu-id="35a8c-127">Using [Kured](https://github.com/weaveworks/kured), an open-source reboot daemon for Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="35a8c-127">Using [Kured](https://github.com/weaveworks/kured), an open-source reboot daemon for Kubernetes.</span></span> <span data-ttu-id="35a8c-128">Kured runs as a [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) and monitors each node for the presence of a file indicating that a reboot is required.</span><span class="sxs-lookup"><span data-stu-id="35a8c-128">Kured runs as a [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) and monitors each node for the presence of a file indicating that a reboot is required.</span></span> <span data-ttu-id="35a8c-129">OS reboots are managed across the cluster using the same [cordon and drain process][cordon-drain] as a cluster upgrade.</span><span class="sxs-lookup"><span data-stu-id="35a8c-129">OS reboots are managed across the cluster using the same [cordon and drain process][cordon-drain] as a cluster upgrade.</span></span>

## <a name="why-are-two-resource-groups-created-with-aks"></a><span data-ttu-id="35a8c-130">Why are two resource groups created with AKS?</span><span class="sxs-lookup"><span data-stu-id="35a8c-130">Why are two resource groups created with AKS?</span></span>

<span data-ttu-id="35a8c-131">Each AKS deployment spans two resource groups:</span><span class="sxs-lookup"><span data-stu-id="35a8c-131">Each AKS deployment spans two resource groups:</span></span>

- <span data-ttu-id="35a8c-132">The first resource group is created by you and contains only the Kubernetes service resource.</span><span class="sxs-lookup"><span data-stu-id="35a8c-132">The first resource group is created by you and contains only the Kubernetes service resource.</span></span> <span data-ttu-id="35a8c-133">The AKS resource provider automatically creates the second one during deployment, such as *MC_myResourceGroup_myAKSCluster_eastus*.</span><span class="sxs-lookup"><span data-stu-id="35a8c-133">The AKS resource provider automatically creates the second one during deployment, such as *MC_myResourceGroup_myAKSCluster_eastus*.</span></span>
- <span data-ttu-id="35a8c-134">This second resource group, such as *MC_myResourceGroup_myAKSCluster_eastus*, contains all of the infrastructure resources associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="35a8c-134">This second resource group, such as *MC_myResourceGroup_myAKSCluster_eastus*, contains all of the infrastructure resources associated with the cluster.</span></span> <span data-ttu-id="35a8c-135">These resources include the Kubernetes node VMs, virtual networking, and storage.</span><span class="sxs-lookup"><span data-stu-id="35a8c-135">These resources include the Kubernetes node VMs, virtual networking, and storage.</span></span> <span data-ttu-id="35a8c-136">This separate resource group is created to simplify resource cleanup.</span><span class="sxs-lookup"><span data-stu-id="35a8c-136">This separate resource group is created to simplify resource cleanup.</span></span>

<span data-ttu-id="35a8c-137">If you create resources for use with your AKS cluster, such as storage accounts or reserved public IP addresses, place them in the automatically generated resource group.</span><span class="sxs-lookup"><span data-stu-id="35a8c-137">If you create resources for use with your AKS cluster, such as storage accounts or reserved public IP addresses, place them in the automatically generated resource group.</span></span>

## <a name="can-i-modify-tags-and-other-properties-of-the-aks-resources-in-the-mc-resource-group"></a><span data-ttu-id="35a8c-138">Can I modify tags and other properties of the AKS resources in the MC_\* resource group?</span><span class="sxs-lookup"><span data-stu-id="35a8c-138">Can I modify tags and other properties of the AKS resources in the MC_\* resource group?</span></span>

<span data-ttu-id="35a8c-139">Modifying and deleting the Azure-created tags and other properties of resources in the *MC_*\* resource group can lead to unexpected results such as scaling and upgrading errors.</span><span class="sxs-lookup"><span data-stu-id="35a8c-139">Modifying and deleting the Azure-created tags and other properties of resources in the *MC_*\* resource group can lead to unexpected results such as scaling and upgrading errors.</span></span> <span data-ttu-id="35a8c-140">It is supported to create and modify additional custom tags, such as to assign a business unit or cost center.</span><span class="sxs-lookup"><span data-stu-id="35a8c-140">It is supported to create and modify additional custom tags, such as to assign a business unit or cost center.</span></span> <span data-ttu-id="35a8c-141">Modifying the resources under the *MC_*\* in the AKS cluster breaks the SLO.</span><span class="sxs-lookup"><span data-stu-id="35a8c-141">Modifying the resources under the *MC_*\* in the AKS cluster breaks the SLO.</span></span>

## <a name="what-kubernetes-admission-controllers-does-aks-support-can-admission-controllers-be-added-or-removed"></a><span data-ttu-id="35a8c-142">What Kubernetes admission controllers does AKS support?</span><span class="sxs-lookup"><span data-stu-id="35a8c-142">What Kubernetes admission controllers does AKS support?</span></span> <span data-ttu-id="35a8c-143">Can admission controllers be added or removed?</span><span class="sxs-lookup"><span data-stu-id="35a8c-143">Can admission controllers be added or removed?</span></span>

<span data-ttu-id="35a8c-144">AKS supports the following [admission controllers][admission-controllers]:</span><span class="sxs-lookup"><span data-stu-id="35a8c-144">AKS supports the following [admission controllers][admission-controllers]:</span></span>

- <span data-ttu-id="35a8c-145">*NamespaceLifecycle*</span><span class="sxs-lookup"><span data-stu-id="35a8c-145">*NamespaceLifecycle*</span></span>
- <span data-ttu-id="35a8c-146">*LimitRanger*</span><span class="sxs-lookup"><span data-stu-id="35a8c-146">*LimitRanger*</span></span>
- <span data-ttu-id="35a8c-147">*ServiceAccount*</span><span class="sxs-lookup"><span data-stu-id="35a8c-147">*ServiceAccount*</span></span>
- <span data-ttu-id="35a8c-148">*DefaultStorageClass*</span><span class="sxs-lookup"><span data-stu-id="35a8c-148">*DefaultStorageClass*</span></span>
- <span data-ttu-id="35a8c-149">*DefaultTolerationSeconds*</span><span class="sxs-lookup"><span data-stu-id="35a8c-149">*DefaultTolerationSeconds*</span></span>
- <span data-ttu-id="35a8c-150">*MutatingAdmissionWebhook*</span><span class="sxs-lookup"><span data-stu-id="35a8c-150">*MutatingAdmissionWebhook*</span></span>
- <span data-ttu-id="35a8c-151">*ValidatingAdmissionWebhook*</span><span class="sxs-lookup"><span data-stu-id="35a8c-151">*ValidatingAdmissionWebhook*</span></span>
- <span data-ttu-id="35a8c-152">*ResourceQuota*</span><span class="sxs-lookup"><span data-stu-id="35a8c-152">*ResourceQuota*</span></span>
- <span data-ttu-id="35a8c-153">*DenyEscalatingExec*</span><span class="sxs-lookup"><span data-stu-id="35a8c-153">*DenyEscalatingExec*</span></span>
- <span data-ttu-id="35a8c-154">*AlwaysPullImages*</span><span class="sxs-lookup"><span data-stu-id="35a8c-154">*AlwaysPullImages*</span></span>

<span data-ttu-id="35a8c-155">It is not currently possible to modify the list of admission controllers in AKS.</span><span class="sxs-lookup"><span data-stu-id="35a8c-155">It is not currently possible to modify the list of admission controllers in AKS.</span></span>

## <a name="is-azure-key-vault-integrated-with-aks"></a><span data-ttu-id="35a8c-156">Is Azure Key Vault integrated with AKS?</span><span class="sxs-lookup"><span data-stu-id="35a8c-156">Is Azure Key Vault integrated with AKS?</span></span>

<span data-ttu-id="35a8c-157">AKS is not currently natively integrated with Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="35a8c-157">AKS is not currently natively integrated with Azure Key Vault.</span></span> <span data-ttu-id="35a8c-158">However, the [Azure Key Vault FlexVolume for Kubernetes project][keyvault-flexvolume] enables direct integration from Kubernetes pods to KeyVault secrets.</span><span class="sxs-lookup"><span data-stu-id="35a8c-158">However, the [Azure Key Vault FlexVolume for Kubernetes project][keyvault-flexvolume] enables direct integration from Kubernetes pods to KeyVault secrets.</span></span>

## <a name="can-i-run-windows-server-containers-on-aks"></a><span data-ttu-id="35a8c-159">Can I run Windows Server containers on AKS?</span><span class="sxs-lookup"><span data-stu-id="35a8c-159">Can I run Windows Server containers on AKS?</span></span>

<span data-ttu-id="35a8c-160">To run Windows Server containers, you need to run Windows Server-based nodes.</span><span class="sxs-lookup"><span data-stu-id="35a8c-160">To run Windows Server containers, you need to run Windows Server-based nodes.</span></span> <span data-ttu-id="35a8c-161">Windows Server-based nodes are not available in AKS at this time.</span><span class="sxs-lookup"><span data-stu-id="35a8c-161">Windows Server-based nodes are not available in AKS at this time.</span></span> <span data-ttu-id="35a8c-162">You can, however, use Virtual Kubelet to schedule Windows containers on Azure Container Instances and manage them as part of your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="35a8c-162">You can, however, use Virtual Kubelet to schedule Windows containers on Azure Container Instances and manage them as part of your AKS cluster.</span></span> <span data-ttu-id="35a8c-163">For more information, see [Use Virtual Kubelet with AKS][virtual-kubelet].</span><span class="sxs-lookup"><span data-stu-id="35a8c-163">For more information, see [Use Virtual Kubelet with AKS][virtual-kubelet].</span></span>

## <a name="does-aks-offer-a-service-level-agreement"></a><span data-ttu-id="35a8c-164">Does AKS offer a service level agreement?</span><span class="sxs-lookup"><span data-stu-id="35a8c-164">Does AKS offer a service level agreement?</span></span>

<span data-ttu-id="35a8c-165">In a service level agreement (SLA), the provider agrees to reimburse the customer for the cost of the service if the published service level isn't met.</span><span class="sxs-lookup"><span data-stu-id="35a8c-165">In a service level agreement (SLA), the provider agrees to reimburse the customer for the cost of the service if the published service level isn't met.</span></span> <span data-ttu-id="35a8c-166">Since AKS itself is free, there is no cost available to reimburse and thus no formal SLA.</span><span class="sxs-lookup"><span data-stu-id="35a8c-166">Since AKS itself is free, there is no cost available to reimburse and thus no formal SLA.</span></span> <span data-ttu-id="35a8c-167">However, AKS seeks to maintain availability of at least 99.5% for the Kubernetes API server.</span><span class="sxs-lookup"><span data-stu-id="35a8c-167">However, AKS seeks to maintain availability of at least 99.5% for the Kubernetes API server.</span></span>

<!-- LINKS - internal -->

[aks-regions]: ./container-service-quotas.md#region-availability
[aks-upgrade]: ./upgrade-cluster.md
[aks-cluster-autoscale]: ./autoscaler.md
[virtual-kubelet]: virtual-kubelet.md
[aks-advanced-networking]: ./networking-overview.md#advanced-networking
[aks-rbac-aad]: ./aad-integration.md

<!-- LINKS - external -->

[auto-scaler]: https://github.com/kubernetes/autoscaler
[cordon-drain]: https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/
[hexadite]: https://github.com/Hexadite/acs-keyvault-agent
[admission-controllers]: https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/
[keyvault-flexvolume]: https://github.com/Azure/kubernetes-keyvault-flexvol
