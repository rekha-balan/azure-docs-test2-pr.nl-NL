---
title: Azure Container Service - FAQ | Microsoft Docs
description: Answers frequently asked questions about Azure Container Service, a service that simplifies the creation, configuration, and management of a cluster of virtual machines to run Docker container apps.
services: container-service
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure, Kubernetes
ms.assetid: ''
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a70b82770a13231ee59ac768deb45b232f95687d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669378"
---
# <a name="container-service-frequently-asked-questions"></a><span data-ttu-id="5a288-104">Container Service frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="5a288-104">Container Service frequently asked questions</span></span>


## <a name="orchestrators"></a><span data-ttu-id="5a288-105">Orchestrators</span><span class="sxs-lookup"><span data-stu-id="5a288-105">Orchestrators</span></span>

### <a name="which-container-orchestrators-do-you-support-on-azure-container-service"></a><span data-ttu-id="5a288-106">Which container orchestrators do you support on Azure Container Service?</span><span class="sxs-lookup"><span data-stu-id="5a288-106">Which container orchestrators do you support on Azure Container Service?</span></span> 

<span data-ttu-id="5a288-107">There is support for open-source DC/OS, Docker Swarm, and Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="5a288-107">There is support for open-source DC/OS, Docker Swarm, and Kubernetes.</span></span> <span data-ttu-id="5a288-108">For more information, see the [Overview](container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="5a288-108">For more information, see the [Overview](container-service-intro.md).</span></span>
 
### <a name="do-you-support-docker-swarm-mode"></a><span data-ttu-id="5a288-109">Do you support Docker Swarm mode?</span><span class="sxs-lookup"><span data-stu-id="5a288-109">Do you support Docker Swarm mode?</span></span> 

<span data-ttu-id="5a288-110">Currently Swarm mode is not supported, but it is on the service roadmap.</span><span class="sxs-lookup"><span data-stu-id="5a288-110">Currently Swarm mode is not supported, but it is on the service roadmap.</span></span> 

### <a name="does-azure-container-service-support-windows-containers"></a><span data-ttu-id="5a288-111">Does Azure Container Service support Windows containers?</span><span class="sxs-lookup"><span data-stu-id="5a288-111">Does Azure Container Service support Windows containers?</span></span>  

<span data-ttu-id="5a288-112">Currently Linux containers are supported with all orchestrators.</span><span class="sxs-lookup"><span data-stu-id="5a288-112">Currently Linux containers are supported with all orchestrators.</span></span> <span data-ttu-id="5a288-113">Support for Windows containers with Kubernetes is in preview.</span><span class="sxs-lookup"><span data-stu-id="5a288-113">Support for Windows containers with Kubernetes is in preview.</span></span>

### <a name="do-you-recommend-a-specific-orchestrator-in-azure-container-service"></a><span data-ttu-id="5a288-114">Do you recommend a specific orchestrator in Azure Container Service?</span><span class="sxs-lookup"><span data-stu-id="5a288-114">Do you recommend a specific orchestrator in Azure Container Service?</span></span> 
<span data-ttu-id="5a288-115">Generally we do not recommend a specific orchestrator.</span><span class="sxs-lookup"><span data-stu-id="5a288-115">Generally we do not recommend a specific orchestrator.</span></span> <span data-ttu-id="5a288-116">If you have experience with one of the supported orchestrators, you can apply that experience in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="5a288-116">If you have experience with one of the supported orchestrators, you can apply that experience in Azure Container Service.</span></span> <span data-ttu-id="5a288-117">Data trends suggest, however, that DC/OS is production proven for Big Data and IoT workloads, Kubernetes is suited for cloud-native workloads, and Docker Swarm is known for its integration with Docker tools and easy learning curve.</span><span class="sxs-lookup"><span data-stu-id="5a288-117">Data trends suggest, however, that DC/OS is production proven for Big Data and IoT workloads, Kubernetes is suited for cloud-native workloads, and Docker Swarm is known for its integration with Docker tools and easy learning curve.</span></span>

<span data-ttu-id="5a288-118">Depending on your scenario, you can also build and manage custom container solutions with other Azure services.</span><span class="sxs-lookup"><span data-stu-id="5a288-118">Depending on your scenario, you can also build and manage custom container solutions with other Azure services.</span></span> <span data-ttu-id="5a288-119">These services include [Virtual Machines](../virtual-machines/linux/overview.md), [Service Fabric](../service-fabric/service-fabric-overview.md), [Web Apps](../app-service-web/app-service-web-overview.md), and [Batch](../batch/batch-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a288-119">These services include [Virtual Machines](../virtual-machines/linux/overview.md), [Service Fabric](../service-fabric/service-fabric-overview.md), [Web Apps](../app-service-web/app-service-web-overview.md), and [Batch](../batch/batch-technical-overview.md).</span></span>  

### <a name="what-is-the-difference-between-azure-container-service-and-acs-engine"></a><span data-ttu-id="5a288-120">What is the difference between Azure Container Service and ACS Engine?</span><span class="sxs-lookup"><span data-stu-id="5a288-120">What is the difference between Azure Container Service and ACS Engine?</span></span> 
<span data-ttu-id="5a288-121">Azure Container Service is an SLA-backed Azure service with features in the Azure portal, Azure command-line tools, and Azure APIs.</span><span class="sxs-lookup"><span data-stu-id="5a288-121">Azure Container Service is an SLA-backed Azure service with features in the Azure portal, Azure command-line tools, and Azure APIs.</span></span> <span data-ttu-id="5a288-122">The service enables you to quickly implement and manage clusters running standard container orchestration tools with a relatively small number of configuration choices.</span><span class="sxs-lookup"><span data-stu-id="5a288-122">The service enables you to quickly implement and manage clusters running standard container orchestration tools with a relatively small number of configuration choices.</span></span> 

<span data-ttu-id="5a288-123">[ACS Engine](http://github.com/Azure/acs-engine) is an open-source project that enables power users to customize the cluster configuration at every level.</span><span class="sxs-lookup"><span data-stu-id="5a288-123">[ACS Engine](http://github.com/Azure/acs-engine) is an open-source project that enables power users to customize the cluster configuration at every level.</span></span> <span data-ttu-id="5a288-124">This ability to alter the configuration of both infrastructure and software means that we offer no SLA for ACS Engine.</span><span class="sxs-lookup"><span data-stu-id="5a288-124">This ability to alter the configuration of both infrastructure and software means that we offer no SLA for ACS Engine.</span></span> <span data-ttu-id="5a288-125">Support is handled through the open-source project on GitHub rather than through official Microsoft channels.</span><span class="sxs-lookup"><span data-stu-id="5a288-125">Support is handled through the open-source project on GitHub rather than through official Microsoft channels.</span></span> 

## <a name="cluster-management"></a><span data-ttu-id="5a288-126">Cluster management</span><span class="sxs-lookup"><span data-stu-id="5a288-126">Cluster management</span></span>

### <a name="how-do-i-create-ssh-keys-for-my-cluster"></a><span data-ttu-id="5a288-127">How do I create SSH keys for my cluster?</span><span class="sxs-lookup"><span data-stu-id="5a288-127">How do I create SSH keys for my cluster?</span></span>

<span data-ttu-id="5a288-128">You can use standard tools on your operating system to create an SSH RSA public and private key pair for authentication against the Linux virtual machines for your cluster.</span><span class="sxs-lookup"><span data-stu-id="5a288-128">You can use standard tools on your operating system to create an SSH RSA public and private key pair for authentication against the Linux virtual machines for your cluster.</span></span> <span data-ttu-id="5a288-129">For steps, see the [OS X and Linux](../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../virtual-machines/linux/ssh-from-windows.md) guidance.</span><span class="sxs-lookup"><span data-stu-id="5a288-129">For steps, see the [OS X and Linux](../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../virtual-machines/linux/ssh-from-windows.md) guidance.</span></span> 

<span data-ttu-id="5a288-130">If you use [Azure CLI 2.0 commands](container-service-create-acs-cluster-cli.md) to deploy a container service cluster, SSH keys can be automatically generated for your cluster.</span><span class="sxs-lookup"><span data-stu-id="5a288-130">If you use [Azure CLI 2.0 commands](container-service-create-acs-cluster-cli.md) to deploy a container service cluster, SSH keys can be automatically generated for your cluster.</span></span>

### <a name="how-do-i-create-a-service-principal-for-my-kubernetes-cluster"></a><span data-ttu-id="5a288-131">How do I create a service principal for my Kubernetes cluster?</span><span class="sxs-lookup"><span data-stu-id="5a288-131">How do I create a service principal for my Kubernetes cluster?</span></span>

<span data-ttu-id="5a288-132">An Azure Active Directory service principal ID and password are also needed to create a Kubernetes cluster in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="5a288-132">An Azure Active Directory service principal ID and password are also needed to create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="5a288-133">For more information, see [About the service principal for a Kubernetes cluster](container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="5a288-133">For more information, see [About the service principal for a Kubernetes cluster](container-service-kubernetes-service-principal.md).</span></span>


<span data-ttu-id="5a288-134">If you use [Azure CLI 2.0 commands](container-service-create-acs-cluster-cli.md) to deploy a Kubernetes cluster, service principal credentials can be automatically generated for your cluster.</span><span class="sxs-lookup"><span data-stu-id="5a288-134">If you use [Azure CLI 2.0 commands](container-service-create-acs-cluster-cli.md) to deploy a Kubernetes cluster, service principal credentials can be automatically generated for your cluster.</span></span>

### <a name="how-large-a-cluster-can-i-create"></a><span data-ttu-id="5a288-135">How large a cluster can I create?</span><span class="sxs-lookup"><span data-stu-id="5a288-135">How large a cluster can I create?</span></span>
<span data-ttu-id="5a288-136">You can create a cluster with 1, 3, or 5 master nodes.</span><span class="sxs-lookup"><span data-stu-id="5a288-136">You can create a cluster with 1, 3, or 5 master nodes.</span></span> <span data-ttu-id="5a288-137">You can choose up to 100 agent nodes.</span><span class="sxs-lookup"><span data-stu-id="5a288-137">You can choose up to 100 agent nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a288-138">For larger clusters and depending on the VM size you choose for your nodes, you might need to increase the cores quota in your subscription.</span><span class="sxs-lookup"><span data-stu-id="5a288-138">For larger clusters and depending on the VM size you choose for your nodes, you might need to increase the cores quota in your subscription.</span></span> <span data-ttu-id="5a288-139">To request a quota increase, open an [online customer support request](../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span><span class="sxs-lookup"><span data-stu-id="5a288-139">To request a quota increase, open an [online customer support request](../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span> <span data-ttu-id="5a288-140">If you're using an [Azure free account](https://azure.microsoft.com/free/), you can use only a limited number of Azure compute cores.</span><span class="sxs-lookup"><span data-stu-id="5a288-140">If you're using an [Azure free account](https://azure.microsoft.com/free/), you can use only a limited number of Azure compute cores.</span></span>
> 

### <a name="how-do-i-increase-the-number-of-masters-after-a-cluster-is-created"></a><span data-ttu-id="5a288-141">How do I increase the number of masters after a cluster is created?</span><span class="sxs-lookup"><span data-stu-id="5a288-141">How do I increase the number of masters after a cluster is created?</span></span> 
<span data-ttu-id="5a288-142">Once the cluster is created, the number of masters is fixed and cannot be changed.</span><span class="sxs-lookup"><span data-stu-id="5a288-142">Once the cluster is created, the number of masters is fixed and cannot be changed.</span></span> <span data-ttu-id="5a288-143">During the creation of the cluster, you should ideally select multiple masters for high availability.</span><span class="sxs-lookup"><span data-stu-id="5a288-143">During the creation of the cluster, you should ideally select multiple masters for high availability.</span></span>


### <a name="how-do-i-increase-the-number-of-agents-after-a-cluster-is-created"></a><span data-ttu-id="5a288-144">How do I increase the number of agents after a cluster is created?</span><span class="sxs-lookup"><span data-stu-id="5a288-144">How do I increase the number of agents after a cluster is created?</span></span> 
<span data-ttu-id="5a288-145">You can scale the number of agents in the cluster by using the Azure portal or command-line tools.</span><span class="sxs-lookup"><span data-stu-id="5a288-145">You can scale the number of agents in the cluster by using the Azure portal or command-line tools.</span></span> <span data-ttu-id="5a288-146">See [Scale an Azure Container Service cluster](container-service-scale.md).</span><span class="sxs-lookup"><span data-stu-id="5a288-146">See [Scale an Azure Container Service cluster](container-service-scale.md).</span></span>


### <a name="what-are-the-urls-of-my-masters-and-agents"></a><span data-ttu-id="5a288-147">What are the URLs of my masters and agents?</span><span class="sxs-lookup"><span data-stu-id="5a288-147">What are the URLs of my masters and agents?</span></span> 
<span data-ttu-id="5a288-148">The URLs of cluster resources in Azure Container Service are based on the DNS name prefix you supply and the name of the Azure region you chose for deployment.</span><span class="sxs-lookup"><span data-stu-id="5a288-148">The URLs of cluster resources in Azure Container Service are based on the DNS name prefix you supply and the name of the Azure region you chose for deployment.</span></span> <span data-ttu-id="5a288-149">For example, the fully qualified domain name (FQDN) of the master node is of this form:</span><span class="sxs-lookup"><span data-stu-id="5a288-149">For example, the fully qualified domain name (FQDN) of the master node is of this form:</span></span>

``` 
DNSnamePrefix.AzureRegion.cloudapp.azure.net
```

<span data-ttu-id="5a288-150">You can find commonly used URLs for your cluster in the Azure portal, the Azure Resource Explorer, or other Azure tools.</span><span class="sxs-lookup"><span data-stu-id="5a288-150">You can find commonly used URLs for your cluster in the Azure portal, the Azure Resource Explorer, or other Azure tools.</span></span>

### <a name="how-do-i-tell-which-orchestrator-version-is-running-in-my-cluster"></a><span data-ttu-id="5a288-151">How do I tell which orchestrator version is running in my cluster?</span><span class="sxs-lookup"><span data-stu-id="5a288-151">How do I tell which orchestrator version is running in my cluster?</span></span>

* <span data-ttu-id="5a288-152">DC/OS: See the [Mesosphere documentation](https://support.mesosphere.com/hc/en-us/articles/207719793-How-to-get-the-DCOS-version-from-the-command-line-)</span><span class="sxs-lookup"><span data-stu-id="5a288-152">DC/OS: See the [Mesosphere documentation](https://support.mesosphere.com/hc/en-us/articles/207719793-How-to-get-the-DCOS-version-from-the-command-line-)</span></span>
* <span data-ttu-id="5a288-153">Docker Swarm: Run `docker version`</span><span class="sxs-lookup"><span data-stu-id="5a288-153">Docker Swarm: Run `docker version`</span></span>
* <span data-ttu-id="5a288-154">Kubernetes: Run `kubectl version`</span><span class="sxs-lookup"><span data-stu-id="5a288-154">Kubernetes: Run `kubectl version`</span></span>


### <a name="how-do-i-upgrade-the-orchestrator-after-deployment"></a><span data-ttu-id="5a288-155">How do I upgrade the orchestrator after deployment?</span><span class="sxs-lookup"><span data-stu-id="5a288-155">How do I upgrade the orchestrator after deployment?</span></span>

<span data-ttu-id="5a288-156">Currently, Azure Container Service doesn't provide tools to upgrade the version of the orchestrator you deployed on your cluster.</span><span class="sxs-lookup"><span data-stu-id="5a288-156">Currently, Azure Container Service doesn't provide tools to upgrade the version of the orchestrator you deployed on your cluster.</span></span> <span data-ttu-id="5a288-157">If Container Service supports a later version, you can deploy a new cluster.</span><span class="sxs-lookup"><span data-stu-id="5a288-157">If Container Service supports a later version, you can deploy a new cluster.</span></span> <span data-ttu-id="5a288-158">Another option is to use orchestrator-specific tools if they are available to upgrade a cluster in-place.</span><span class="sxs-lookup"><span data-stu-id="5a288-158">Another option is to use orchestrator-specific tools if they are available to upgrade a cluster in-place.</span></span> <span data-ttu-id="5a288-159">For example, see [DC/OS Upgrading](https://dcos.io/docs/1.8/administration/upgrading/).</span><span class="sxs-lookup"><span data-stu-id="5a288-159">For example, see [DC/OS Upgrading](https://dcos.io/docs/1.8/administration/upgrading/).</span></span>
 
### <a name="where-do-i-find-the-ssh-connection-string-to-my-cluster"></a><span data-ttu-id="5a288-160">Where do I find the SSH connection string to my cluster?</span><span class="sxs-lookup"><span data-stu-id="5a288-160">Where do I find the SSH connection string to my cluster?</span></span>

<span data-ttu-id="5a288-161">You can find the connection string in the Azure portal, or by using Azure command-line tools.</span><span class="sxs-lookup"><span data-stu-id="5a288-161">You can find the connection string in the Azure portal, or by using Azure command-line tools.</span></span> 

1. <span data-ttu-id="5a288-162">In the portal, navigate to the resource group for the cluster deployment.</span><span class="sxs-lookup"><span data-stu-id="5a288-162">In the portal, navigate to the resource group for the cluster deployment.</span></span>  

2. <span data-ttu-id="5a288-163">Click **Overview** and click the link for **Deployments** under **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="5a288-163">Click **Overview** and click the link for **Deployments** under **Essentials**.</span></span> 

3. <span data-ttu-id="5a288-164">In the **Deployment history** blade, click the deployment that has a name beginning with **microsoft-acs** followed by a deployment date.</span><span class="sxs-lookup"><span data-stu-id="5a288-164">In the **Deployment history** blade, click the deployment that has a name beginning with **microsoft-acs** followed by a deployment date.</span></span> <span data-ttu-id="5a288-165">Example: microsoft-acs-201701310000.</span><span class="sxs-lookup"><span data-stu-id="5a288-165">Example: microsoft-acs-201701310000.</span></span>  

4. <span data-ttu-id="5a288-166">On the **Summary** page, under **Outputs**, several cluster links are provided.</span><span class="sxs-lookup"><span data-stu-id="5a288-166">On the **Summary** page, under **Outputs**, several cluster links are provided.</span></span> <span data-ttu-id="5a288-167">**SSHMaster0** provides an SSH connection string to the first master in your container service cluster.</span><span class="sxs-lookup"><span data-stu-id="5a288-167">**SSHMaster0** provides an SSH connection string to the first master in your container service cluster.</span></span> 

<span data-ttu-id="5a288-168">As previously noted, you can also use Azure tools to find the FQDN of the master.</span><span class="sxs-lookup"><span data-stu-id="5a288-168">As previously noted, you can also use Azure tools to find the FQDN of the master.</span></span> <span data-ttu-id="5a288-169">Make an SSH connection to the master using the FQDN of the master and the user name you specified when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a288-169">Make an SSH connection to the master using the FQDN of the master and the user name you specified when creating the cluster.</span></span> <span data-ttu-id="5a288-170">For example:</span><span class="sxs-lookup"><span data-stu-id="5a288-170">For example:</span></span>

```bash
ssh userName@masterFQDN –A –p 22 
```

<span data-ttu-id="5a288-171">For more information, see [Connect to an Azure Container Service cluster](container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="5a288-171">For more information, see [Connect to an Azure Container Service cluster](container-service-connect.md).</span></span>




## <a name="next-steps"></a><span data-ttu-id="5a288-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="5a288-172">Next steps</span></span>

* <span data-ttu-id="5a288-173">[Learn more](container-service-intro.md) about Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="5a288-173">[Learn more](container-service-intro.md) about Azure Container Service.</span></span>
* <span data-ttu-id="5a288-174">Deploy a container service cluster using the [portal](container-service-deployment.md) or [Azure CLI 2.0](container-service-create-acs-cluster-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5a288-174">Deploy a container service cluster using the [portal](container-service-deployment.md) or [Azure CLI 2.0](container-service-create-acs-cluster-cli.md).</span></span>
