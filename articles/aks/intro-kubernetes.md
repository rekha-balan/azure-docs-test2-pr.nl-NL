---
title: Introduction to Azure Kubernetes Service
description: Azure Kubernetes Service makes it simple to deploy and manage container-based applications on Azure.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: overview
ms.date: 06/13/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 93c6a894b6914ac6e9764fafc27495aa506a56d0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869597"
---
# <a name="azure-kubernetes-service-aks"></a><span data-ttu-id="3e720-103">Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="3e720-103">Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="3e720-104">Azure Kubernetes Service (AKS) makes it simple to deploy a managed Kubernetes cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="3e720-104">Azure Kubernetes Service (AKS) makes it simple to deploy a managed Kubernetes cluster in Azure.</span></span> <span data-ttu-id="3e720-105">AKS reduces the complexity and operational overhead of managing Kubernetes by offloading much of that responsibility to Azure.</span><span class="sxs-lookup"><span data-stu-id="3e720-105">AKS reduces the complexity and operational overhead of managing Kubernetes by offloading much of that responsibility to Azure.</span></span> <span data-ttu-id="3e720-106">As a hosted Kubernetes service, Azure handles critical tasks like health monitoring and maintenance for you.</span><span class="sxs-lookup"><span data-stu-id="3e720-106">As a hosted Kubernetes service, Azure handles critical tasks like health monitoring and maintenance for you.</span></span> <span data-ttu-id="3e720-107">In addition, the service is free, you only pay for the agent nodes within your clusters, not for the masters.</span><span class="sxs-lookup"><span data-stu-id="3e720-107">In addition, the service is free, you only pay for the agent nodes within your clusters, not for the masters.</span></span>

<span data-ttu-id="3e720-108">This document provides an overview on the features of Azure Kubernetes Service (AKS).</span><span class="sxs-lookup"><span data-stu-id="3e720-108">This document provides an overview on the features of Azure Kubernetes Service (AKS).</span></span>

## <a name="flexible-deployment-options"></a><span data-ttu-id="3e720-109">Flexible deployment options</span><span class="sxs-lookup"><span data-stu-id="3e720-109">Flexible deployment options</span></span>

<span data-ttu-id="3e720-110">Azure Kubernetes Service offers portal, command line, and template driven deployment options (Resource Manager templates and Terraform).</span><span class="sxs-lookup"><span data-stu-id="3e720-110">Azure Kubernetes Service offers portal, command line, and template driven deployment options (Resource Manager templates and Terraform).</span></span> <span data-ttu-id="3e720-111">When deploying an AKS cluster, the Kubernetes master and all nodes are deployed and configured for you.</span><span class="sxs-lookup"><span data-stu-id="3e720-111">When deploying an AKS cluster, the Kubernetes master and all nodes are deployed and configured for you.</span></span> <span data-ttu-id="3e720-112">Additional features such as advanced networking, Azure Active Directory integration, and monitoring can also be configured during the deployment process.</span><span class="sxs-lookup"><span data-stu-id="3e720-112">Additional features such as advanced networking, Azure Active Directory integration, and monitoring can also be configured during the deployment process.</span></span>

<span data-ttu-id="3e720-113">For more information, see both the [AKS portal quickstart][aks-portal] or the [AKS CLI quickstart][aks-cli].</span><span class="sxs-lookup"><span data-stu-id="3e720-113">For more information, see both the [AKS portal quickstart][aks-portal] or the [AKS CLI quickstart][aks-cli].</span></span>

## <a name="identity-and-security-management"></a><span data-ttu-id="3e720-114">Identity and security management</span><span class="sxs-lookup"><span data-stu-id="3e720-114">Identity and security management</span></span>

<span data-ttu-id="3e720-115">AKS clusters support [Role-Based Access Control (RBAC)][kubernetes-rbac].</span><span class="sxs-lookup"><span data-stu-id="3e720-115">AKS clusters support [Role-Based Access Control (RBAC)][kubernetes-rbac].</span></span> <span data-ttu-id="3e720-116">An AKS cluster can also be configured to integrate with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3e720-116">An AKS cluster can also be configured to integrate with Azure Active Directory.</span></span> <span data-ttu-id="3e720-117">In this configuration, Kubernetes access can be configured based on Azure Active Directory identity and group membership.</span><span class="sxs-lookup"><span data-stu-id="3e720-117">In this configuration, Kubernetes access can be configured based on Azure Active Directory identity and group membership.</span></span>

<span data-ttu-id="3e720-118">For more information, see, [Integrate Azure Active Directory with AKS][aks-aad].</span><span class="sxs-lookup"><span data-stu-id="3e720-118">For more information, see, [Integrate Azure Active Directory with AKS][aks-aad].</span></span>

## <a name="integrated-logging-and-monitoring"></a><span data-ttu-id="3e720-119">Integrated logging and monitoring</span><span class="sxs-lookup"><span data-stu-id="3e720-119">Integrated logging and monitoring</span></span>

<span data-ttu-id="3e720-120">Container health gives you performance visibility by collecting memory and processor metrics from containers, nodes, and controllers.</span><span class="sxs-lookup"><span data-stu-id="3e720-120">Container health gives you performance visibility by collecting memory and processor metrics from containers, nodes, and controllers.</span></span> <span data-ttu-id="3e720-121">Container logs are also collected.</span><span class="sxs-lookup"><span data-stu-id="3e720-121">Container logs are also collected.</span></span> <span data-ttu-id="3e720-122">This data is stored in your Log Analytics workspace, and is available through the Azure portal, Azure CLI, or a REST endpoint.</span><span class="sxs-lookup"><span data-stu-id="3e720-122">This data is stored in your Log Analytics workspace, and is available through the Azure portal, Azure CLI, or a REST endpoint.</span></span>

<span data-ttu-id="3e720-123">For more information, see [Monitor Azure Kubernetes Service container health][container-health].</span><span class="sxs-lookup"><span data-stu-id="3e720-123">For more information, see [Monitor Azure Kubernetes Service container health][container-health].</span></span>

## <a name="cluster-node-scaling"></a><span data-ttu-id="3e720-124">Cluster node scaling</span><span class="sxs-lookup"><span data-stu-id="3e720-124">Cluster node scaling</span></span>

<span data-ttu-id="3e720-125">As demand for resources increases, the nodes of an AKS cluster can be scaled out to match.</span><span class="sxs-lookup"><span data-stu-id="3e720-125">As demand for resources increases, the nodes of an AKS cluster can be scaled out to match.</span></span> <span data-ttu-id="3e720-126">If resource demand drops, nodes can be removed by scaling in the cluster.</span><span class="sxs-lookup"><span data-stu-id="3e720-126">If resource demand drops, nodes can be removed by scaling in the cluster.</span></span> <span data-ttu-id="3e720-127">AKS scale operations can be completed using the Azure portal or the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="3e720-127">AKS scale operations can be completed using the Azure portal or the Azure CLI.</span></span>

<span data-ttu-id="3e720-128">For more information, see [Scale an Azure Kubernetes Service (AKS) cluster][aks-scale].</span><span class="sxs-lookup"><span data-stu-id="3e720-128">For more information, see [Scale an Azure Kubernetes Service (AKS) cluster][aks-scale].</span></span>

## <a name="cluster-node-upgrades"></a><span data-ttu-id="3e720-129">Cluster node upgrades</span><span class="sxs-lookup"><span data-stu-id="3e720-129">Cluster node upgrades</span></span>

<span data-ttu-id="3e720-130">Azure Kubernetes Service offers multiple Kubernetes versions.</span><span class="sxs-lookup"><span data-stu-id="3e720-130">Azure Kubernetes Service offers multiple Kubernetes versions.</span></span> <span data-ttu-id="3e720-131">As new versions become available in AKS, your cluster can be upgraded using the Azure portal or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="3e720-131">As new versions become available in AKS, your cluster can be upgraded using the Azure portal or Azure CLI.</span></span> <span data-ttu-id="3e720-132">During the upgrade process, nodes are carefully cordoned and drained to minimize disruption to running applications.</span><span class="sxs-lookup"><span data-stu-id="3e720-132">During the upgrade process, nodes are carefully cordoned and drained to minimize disruption to running applications.</span></span>

<span data-ttu-id="3e720-133">For more information, see [Upgrade an Azure Kubernetes Service (AKS) cluster][aks-upgrade].</span><span class="sxs-lookup"><span data-stu-id="3e720-133">For more information, see [Upgrade an Azure Kubernetes Service (AKS) cluster][aks-upgrade].</span></span>

## <a name="http-application-routing"></a><span data-ttu-id="3e720-134">HTTP application routing</span><span class="sxs-lookup"><span data-stu-id="3e720-134">HTTP application routing</span></span>

<span data-ttu-id="3e720-135">The HTTP Application Routing solution makes it easy to access applications deployed to your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="3e720-135">The HTTP Application Routing solution makes it easy to access applications deployed to your AKS cluster.</span></span> <span data-ttu-id="3e720-136">When enabled, the HTTP application routing solution configures an ingress controller in your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="3e720-136">When enabled, the HTTP application routing solution configures an ingress controller in your AKS cluster.</span></span> <span data-ttu-id="3e720-137">As applications are deployed, publicly accessible DNS names are auto configured.</span><span class="sxs-lookup"><span data-stu-id="3e720-137">As applications are deployed, publicly accessible DNS names are auto configured.</span></span>

<span data-ttu-id="3e720-138">For more information, see [HTTP application routing][aks-http-routing].</span><span class="sxs-lookup"><span data-stu-id="3e720-138">For more information, see [HTTP application routing][aks-http-routing].</span></span>

## <a name="gpu-enabled-nodes"></a><span data-ttu-id="3e720-139">GPU enabled nodes</span><span class="sxs-lookup"><span data-stu-id="3e720-139">GPU enabled nodes</span></span>

<span data-ttu-id="3e720-140">AKS supports the creation of GPU enabled node pools.</span><span class="sxs-lookup"><span data-stu-id="3e720-140">AKS supports the creation of GPU enabled node pools.</span></span> <span data-ttu-id="3e720-141">Azure currently provides single or multiple GPU enabled VMs.</span><span class="sxs-lookup"><span data-stu-id="3e720-141">Azure currently provides single or multiple GPU enabled VMs.</span></span> <span data-ttu-id="3e720-142">GPU enabled VMs are designed for compute-intensive, graphics-intensive, and visualization workloads.</span><span class="sxs-lookup"><span data-stu-id="3e720-142">GPU enabled VMs are designed for compute-intensive, graphics-intensive, and visualization workloads.</span></span>

<span data-ttu-id="3e720-143">For more information, see [Using GPUs on AKS][aks-gpu].</span><span class="sxs-lookup"><span data-stu-id="3e720-143">For more information, see [Using GPUs on AKS][aks-gpu].</span></span>

## <a name="development-tooling-integration"></a><span data-ttu-id="3e720-144">Development tooling integration</span><span class="sxs-lookup"><span data-stu-id="3e720-144">Development tooling integration</span></span>

<span data-ttu-id="3e720-145">Kubernetes has a rich ecosystem of development and management tools such as Helm, Draft, and the Kubernetes extension for Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="3e720-145">Kubernetes has a rich ecosystem of development and management tools such as Helm, Draft, and the Kubernetes extension for Visual Studio Code.</span></span> <span data-ttu-id="3e720-146">These tools work seamlessly with Azure Kubernetes Service.</span><span class="sxs-lookup"><span data-stu-id="3e720-146">These tools work seamlessly with Azure Kubernetes Service.</span></span>

<span data-ttu-id="3e720-147">Additionally, Azure Dev Spaces provides a rapid, iterative Kubernetes development experience for teams.</span><span class="sxs-lookup"><span data-stu-id="3e720-147">Additionally, Azure Dev Spaces provides a rapid, iterative Kubernetes development experience for teams.</span></span> <span data-ttu-id="3e720-148">With minimal configuration, you can run and debug containers directly in Azure Kubernetes Service (AKS).</span><span class="sxs-lookup"><span data-stu-id="3e720-148">With minimal configuration, you can run and debug containers directly in Azure Kubernetes Service (AKS).</span></span>

<span data-ttu-id="3e720-149">For more information, see [Azure Dev Spaces][azure-dev-spaces].</span><span class="sxs-lookup"><span data-stu-id="3e720-149">For more information, see [Azure Dev Spaces][azure-dev-spaces].</span></span>

<span data-ttu-id="3e720-150">Azure DevOps project provides a simple solution for bringing existing code and Git repository into Azure.</span><span class="sxs-lookup"><span data-stu-id="3e720-150">Azure DevOps project provides a simple solution for bringing existing code and Git repository into Azure.</span></span> <span data-ttu-id="3e720-151">The DevOps project automatically creates Azure resources such as AKS, a release pipeline in Azure DevOps Services that includes a build pipeline for CI, sets up a release pipeline for CD, and then creates an Azure Application Insights resource for monitoring.</span><span class="sxs-lookup"><span data-stu-id="3e720-151">The DevOps project automatically creates Azure resources such as AKS, a release pipeline in Azure DevOps Services that includes a build pipeline for CI, sets up a release pipeline for CD, and then creates an Azure Application Insights resource for monitoring.</span></span>

<span data-ttu-id="3e720-152">For more information, see [Azure DevOps project][azure-devops].</span><span class="sxs-lookup"><span data-stu-id="3e720-152">For more information, see [Azure DevOps project][azure-devops].</span></span>

## <a name="virtual-network-integration"></a><span data-ttu-id="3e720-153">Virtual network integration</span><span class="sxs-lookup"><span data-stu-id="3e720-153">Virtual network integration</span></span>

<span data-ttu-id="3e720-154">An AKS cluster can be deployed into an existing VNet.</span><span class="sxs-lookup"><span data-stu-id="3e720-154">An AKS cluster can be deployed into an existing VNet.</span></span> <span data-ttu-id="3e720-155">In this configuration, every pod in the cluster is assigned an IP address in the VNet, and can directly communicate with other pods in the cluster, and other nodes in the VNet.</span><span class="sxs-lookup"><span data-stu-id="3e720-155">In this configuration, every pod in the cluster is assigned an IP address in the VNet, and can directly communicate with other pods in the cluster, and other nodes in the VNet.</span></span> <span data-ttu-id="3e720-156">Pods can connect also to other services in a peered VNet, and to on-premises networks over ExpressRoute and site-to-site (S2S) VPN connections.</span><span class="sxs-lookup"><span data-stu-id="3e720-156">Pods can connect also to other services in a peered VNet, and to on-premises networks over ExpressRoute and site-to-site (S2S) VPN connections.</span></span>

<span data-ttu-id="3e720-157">For more information, see the [AKS networking overview][aks-networking].</span><span class="sxs-lookup"><span data-stu-id="3e720-157">For more information, see the [AKS networking overview][aks-networking].</span></span>

## <a name="private-container-registry"></a><span data-ttu-id="3e720-158">Private container registry</span><span class="sxs-lookup"><span data-stu-id="3e720-158">Private container registry</span></span>

<span data-ttu-id="3e720-159">Integrate with Azure Container Registry (ACR) for private storage of your Docker images.</span><span class="sxs-lookup"><span data-stu-id="3e720-159">Integrate with Azure Container Registry (ACR) for private storage of your Docker images.</span></span>

<span data-ttu-id="3e720-160">For more information, see [Azure Container Registry (ACR)][acr-docs].</span><span class="sxs-lookup"><span data-stu-id="3e720-160">For more information, see [Azure Container Registry (ACR)][acr-docs].</span></span>

## <a name="storage-volume-support"></a><span data-ttu-id="3e720-161">Storage volume support</span><span class="sxs-lookup"><span data-stu-id="3e720-161">Storage volume support</span></span>

<span data-ttu-id="3e720-162">Azure Kubernetes Service (AKS) support mounting storage volumes for persistent data.</span><span class="sxs-lookup"><span data-stu-id="3e720-162">Azure Kubernetes Service (AKS) support mounting storage volumes for persistent data.</span></span> <span data-ttu-id="3e720-163">AKS clusters are created with support for Azure Files and Azure Disks.</span><span class="sxs-lookup"><span data-stu-id="3e720-163">AKS clusters are created with support for Azure Files and Azure Disks.</span></span>

<span data-ttu-id="3e720-164">For more information, see [Azure Files][azure-files] and [Azure Disks][azure-disk].</span><span class="sxs-lookup"><span data-stu-id="3e720-164">For more information, see [Azure Files][azure-files] and [Azure Disks][azure-disk].</span></span>

## <a name="docker-image-support"></a><span data-ttu-id="3e720-165">Docker image support</span><span class="sxs-lookup"><span data-stu-id="3e720-165">Docker image support</span></span>

<span data-ttu-id="3e720-166">Azure Kubernetes Service (AKS) supports the Docker image format.</span><span class="sxs-lookup"><span data-stu-id="3e720-166">Azure Kubernetes Service (AKS) supports the Docker image format.</span></span>

## <a name="kubernetes-certification"></a><span data-ttu-id="3e720-167">Kubernetes certification</span><span class="sxs-lookup"><span data-stu-id="3e720-167">Kubernetes certification</span></span>

<span data-ttu-id="3e720-168">Azure Kubernetes Service (AKS) has been CNCF certified as Kubernetes conformant.</span><span class="sxs-lookup"><span data-stu-id="3e720-168">Azure Kubernetes Service (AKS) has been CNCF certified as Kubernetes conformant.</span></span>

## <a name="regulatory-compliance"></a><span data-ttu-id="3e720-169">Regulatory compliance</span><span class="sxs-lookup"><span data-stu-id="3e720-169">Regulatory compliance</span></span>

<span data-ttu-id="3e720-170">Azure Kubernetes Service (AKS) is compliant with SOC, ISO, and PCI DSS.</span><span class="sxs-lookup"><span data-stu-id="3e720-170">Azure Kubernetes Service (AKS) is compliant with SOC, ISO, and PCI DSS.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e720-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="3e720-171">Next steps</span></span>

<span data-ttu-id="3e720-172">Learn more about deploying and managing AKS with the AKS quickstart.</span><span class="sxs-lookup"><span data-stu-id="3e720-172">Learn more about deploying and managing AKS with the AKS quickstart.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="3e720-173">[AKS quickstart][aks-cli]</span><span class="sxs-lookup"><span data-stu-id="3e720-173">[AKS quickstart][aks-cli]</span></span>

<!-- LINKS - external -->
[acs-engine]: https://github.com/Azure/acs-engine
[draft]: https://github.com/Azure/draft
[helm]: https://helm.sh/
[kubectl-overview]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[kubernetes-rbac]: https://kubernetes.io/docs/reference/access-authn-authz/rbac/

<!-- LINKS - internal -->
[acr-docs]: ../container-registry/container-registry-intro.md
[aks-aad]: ./aad-integration.md
[aks-cli]: ./kubernetes-walkthrough.md
[aks-gpu]: ./gpu-cluster.md
[aks-http-routing]: ./http-application-routing.md
[aks-networking]: ./networking-overview.md
[aks-portal]: ./kubernetes-walkthrough-portal.md
[aks-scale]: ./scale-cluster.md
[aks-upgrade]: ./upgrade-cluster.md
[azure-dev-spaces]: https://docs.microsoft.com/en-us/azure/dev-spaces/azure-dev-spaces
[azure-devops]: https://docs.microsoft.com/en-us/azure/devops-project/overview
[azure-disk]: ./azure-disks-dynamic-pv.md
[azure-files]: ./azure-files-dynamic-pv.md
[container-health]: ../monitoring/monitoring-container-health.md

