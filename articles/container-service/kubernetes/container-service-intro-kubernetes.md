---
title: Introduction to Azure Container Service for Kubernetes
description: Azure Container Service for Kubernetes makes it simple to deploy and manage container-based applications on Azure.
services: container-service
author: gabrtv
manager: jeconnoc
ms.service: container-service
ms.topic: overview
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: f12fc0baa055e62d4f15c0e42eb7add3661ea6fc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865861"
---
# <a name="introduction-to-azure-container-service-for-kubernetes"></a><span data-ttu-id="178e1-103">Introduction to Azure Container Service for Kubernetes</span><span class="sxs-lookup"><span data-stu-id="178e1-103">Introduction to Azure Container Service for Kubernetes</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

<span data-ttu-id="178e1-104">Azure Container Service for Kubernetes makes it simple to create, configure, and manage a cluster of virtual machines that are preconfigured to run containerized applications.</span><span class="sxs-lookup"><span data-stu-id="178e1-104">Azure Container Service for Kubernetes makes it simple to create, configure, and manage a cluster of virtual machines that are preconfigured to run containerized applications.</span></span> <span data-ttu-id="178e1-105">This enables you to use your existing skills, or draw upon a large and growing body of community expertise, to deploy and manage container-based applications on Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="178e1-105">This enables you to use your existing skills, or draw upon a large and growing body of community expertise, to deploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="178e1-106">By using Azure Container Service, you can take advantage of the enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and the Docker image format.</span><span class="sxs-lookup"><span data-stu-id="178e1-106">By using Azure Container Service, you can take advantage of the enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and the Docker image format.</span></span>

## <a name="using-azure-container-service-for-kubernetes"></a><span data-ttu-id="178e1-107">Using Azure Container Service for Kubernetes</span><span class="sxs-lookup"><span data-stu-id="178e1-107">Using Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="178e1-108">Our goal with Azure Container Service is to provide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span><span class="sxs-lookup"><span data-stu-id="178e1-108">Our goal with Azure Container Service is to provide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="178e1-109">To this end, we expose the standard Kubernetes API endpoints.</span><span class="sxs-lookup"><span data-stu-id="178e1-109">To this end, we expose the standard Kubernetes API endpoints.</span></span> <span data-ttu-id="178e1-110">By using these standard endpoints, you can leverage any software that is capable of talking to a Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="178e1-110">By using these standard endpoints, you can leverage any software that is capable of talking to a Kubernetes cluster.</span></span> <span data-ttu-id="178e1-111">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span><span class="sxs-lookup"><span data-stu-id="178e1-111">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span></span>

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a><span data-ttu-id="178e1-112">Creating a Kubernetes cluster using Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="178e1-112">Creating a Kubernetes cluster using Azure Container Service</span></span>
<span data-ttu-id="178e1-113">To begin using Azure Container Service, deploy an Azure Container Service cluster with the [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via the portal (search the Marketplace for **Azure Container Service**).</span><span class="sxs-lookup"><span data-stu-id="178e1-113">To begin using Azure Container Service, deploy an Azure Container Service cluster with the [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via the portal (search the Marketplace for **Azure Container Service**).</span></span> <span data-ttu-id="178e1-114">If you are an advanced user who needs more control over the Azure Resource Manager templates, you can use the open source [acs-engine](https://github.com/Azure/acs-engine) project to build your own custom Kubernetes cluster and deploy it via the `az` CLI.</span><span class="sxs-lookup"><span data-stu-id="178e1-114">If you are an advanced user who needs more control over the Azure Resource Manager templates, you can use the open source [acs-engine](https://github.com/Azure/acs-engine) project to build your own custom Kubernetes cluster and deploy it via the `az` CLI.</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="178e1-115">Using Kubernetes</span><span class="sxs-lookup"><span data-stu-id="178e1-115">Using Kubernetes</span></span>
<span data-ttu-id="178e1-116">Kubernetes automates deployment, scaling, and management of containerized applications.</span><span class="sxs-lookup"><span data-stu-id="178e1-116">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="178e1-117">It has a rich set of features including:</span><span class="sxs-lookup"><span data-stu-id="178e1-117">It has a rich set of features including:</span></span>
* <span data-ttu-id="178e1-118">Automatic binpacking</span><span class="sxs-lookup"><span data-stu-id="178e1-118">Automatic binpacking</span></span>
* <span data-ttu-id="178e1-119">Self-healing</span><span class="sxs-lookup"><span data-stu-id="178e1-119">Self-healing</span></span>
* <span data-ttu-id="178e1-120">Horizontal scaling</span><span class="sxs-lookup"><span data-stu-id="178e1-120">Horizontal scaling</span></span>
* <span data-ttu-id="178e1-121">Service discovery and load balancing</span><span class="sxs-lookup"><span data-stu-id="178e1-121">Service discovery and load balancing</span></span>
* <span data-ttu-id="178e1-122">Automated rollouts and rollbacks</span><span class="sxs-lookup"><span data-stu-id="178e1-122">Automated rollouts and rollbacks</span></span>
* <span data-ttu-id="178e1-123">Secret and configuration management</span><span class="sxs-lookup"><span data-stu-id="178e1-123">Secret and configuration management</span></span>
* <span data-ttu-id="178e1-124">Storage orchestration</span><span class="sxs-lookup"><span data-stu-id="178e1-124">Storage orchestration</span></span>
* <span data-ttu-id="178e1-125">Batch execution</span><span class="sxs-lookup"><span data-stu-id="178e1-125">Batch execution</span></span>

<span data-ttu-id="178e1-126">Architectural diagram of Kubernetes deployed via Azure Container Service:</span><span class="sxs-lookup"><span data-stu-id="178e1-126">Architectural diagram of Kubernetes deployed via Azure Container Service:</span></span>

![Azure Container Service configured to use Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a><span data-ttu-id="178e1-128">Videos</span><span class="sxs-lookup"><span data-stu-id="178e1-128">Videos</span></span>

<span data-ttu-id="178e1-129">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span><span class="sxs-lookup"><span data-stu-id="178e1-129">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

<span data-ttu-id="178e1-130">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span><span class="sxs-lookup"><span data-stu-id="178e1-130">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="178e1-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="178e1-131">Next steps</span></span>

<span data-ttu-id="178e1-132">Explore the [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) to begin exploring Azure Container Service today.</span><span class="sxs-lookup"><span data-stu-id="178e1-132">Explore the [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) to begin exploring Azure Container Service today.</span></span>