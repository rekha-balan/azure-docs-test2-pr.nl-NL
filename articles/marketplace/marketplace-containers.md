---
title: Containers Offer Publishing Guide for Azure Marketplace
description: This article describes the requirements to publish Containers in the Marketplace
services: Azure, Marketplace, Compute, Storage, Networking, Blockchain, Security
documentationcenter: ''
author: ellacroi
manager: nunoc
editor: ''
ms.assetid: ''
ms.service: marketplace
ms.workload: ''
ms.tgt_pltfrm: ''
ms.devlang: ''
ms.topic: article
ms.date: 07/09/2018
ms.author: ellacroi
ms.openlocfilehash: 5eb30c65032332825d05097f86d0275b015a8929
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867844"
---
# <a name="containers-offer-publishing-guide"></a><span data-ttu-id="0d180-103">Containers Offer Publishing Guide</span><span class="sxs-lookup"><span data-stu-id="0d180-103">Containers Offer Publishing Guide</span></span>

<span data-ttu-id="0d180-104">Container offers help you publish your container image to the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0d180-104">Container offers help you publish your container image to the Azure Marketplace.</span></span> <span data-ttu-id="0d180-105">Use this guide to understand the requirements for this offer.</span><span class="sxs-lookup"><span data-stu-id="0d180-105">Use this guide to understand the requirements for this offer.</span></span> 

<span data-ttu-id="0d180-106">These are transaction offers which are deployed and billed through the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0d180-106">These are transaction offers which are deployed and billed through the Marketplace.</span></span> <span data-ttu-id="0d180-107">The call to action that a user sees is "Get It Now."</span><span class="sxs-lookup"><span data-stu-id="0d180-107">The call to action that a user sees is "Get It Now."</span></span>

<span data-ttu-id="0d180-108">Use the Container offer type when your solution is a Docker container image provisioned as a Kubernetes-based Azure container service.</span><span class="sxs-lookup"><span data-stu-id="0d180-108">Use the Container offer type when your solution is a Docker container image provisioned as a Kubernetes-based Azure container service.</span></span>

>[!NOTE]
><span data-ttu-id="0d180-109">For example, a Kubernetes-based Azure container service like Azure Kubernetes Service or Azure Container Instances, the choice of Azure customers for a Kubernetes-based container runtime.</span><span class="sxs-lookup"><span data-stu-id="0d180-109">For example, a Kubernetes-based Azure container service like Azure Kubernetes Service or Azure Container Instances, the choice of Azure customers for a Kubernetes-based container runtime.</span></span>  

<span data-ttu-id="0d180-110">Microsoft currently supports free and bring-your-own-license (BYOL) licensing models.</span><span class="sxs-lookup"><span data-stu-id="0d180-110">Microsoft currently supports free and bring-your-own-license (BYOL) licensing models.</span></span>

## <a name="containers-offer"></a><span data-ttu-id="0d180-111">Containers Offer</span><span class="sxs-lookup"><span data-stu-id="0d180-111">Containers Offer</span></span>

| <span data-ttu-id="0d180-112">Requirement</span><span class="sxs-lookup"><span data-stu-id="0d180-112">Requirement</span></span> | <span data-ttu-id="0d180-113">Details</span><span class="sxs-lookup"><span data-stu-id="0d180-113">Details</span></span> |  
|:--- |:--- |  
| <span data-ttu-id="0d180-114">Billing and metering</span><span class="sxs-lookup"><span data-stu-id="0d180-114">Billing and metering</span></span> | <span data-ttu-id="0d180-115">Support either the free or BYOL billing model.</span><span class="sxs-lookup"><span data-stu-id="0d180-115">Support either the free or BYOL billing model.</span></span> |  
| <span data-ttu-id="0d180-116">Image built from Dockerfile</span><span class="sxs-lookup"><span data-stu-id="0d180-116">Image built from Dockerfile</span></span> | <span data-ttu-id="0d180-117">Container images must be based on the Docker image specification and must be built from a Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="0d180-117">Container images must be based on the Docker image specification and must be built from a Dockerfile.</span></span><ul> <li><span data-ttu-id="0d180-118">For more information about building docker images, visit the Usage section located at [docs.docker.com/engine/reference/builder/#usage](https://docs.docker.com/engine/reference/builder/#usage).</span><span class="sxs-lookup"><span data-stu-id="0d180-118">For more information about building docker images, visit the Usage section located at [docs.docker.com/engine/reference/builder/#usage](https://docs.docker.com/engine/reference/builder/#usage).</span></span></li> </ul> |  
| <span data-ttu-id="0d180-119">Hosting in ACR</span><span class="sxs-lookup"><span data-stu-id="0d180-119">Hosting in ACR</span></span> | <span data-ttu-id="0d180-120">Container images must be hosted in an Azure Container Registry (ACR) repository.</span><span class="sxs-lookup"><span data-stu-id="0d180-120">Container images must be hosted in an Azure Container Registry (ACR) repository.</span></span><ul> <li><span data-ttu-id="0d180-121">For more information about working with ACR, visit the Quickstart: Create a container registry using the Azure portal page located at [docs.microsoft.com/azure/container-registry/container-registry-get-started-portal](https://docs.microsoft.com/azure/container-registry/container-registry-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="0d180-121">For more information about working with ACR, visit the Quickstart: Create a container registry using the Azure portal page located at [docs.microsoft.com/azure/container-registry/container-registry-get-started-portal](https://docs.microsoft.com/azure/container-registry/container-registry-get-started-portal).</span></span></li> </ul> |  
| <span data-ttu-id="0d180-122">Image tagging</span><span class="sxs-lookup"><span data-stu-id="0d180-122">Image tagging</span></span> | <span data-ttu-id="0d180-123">Container images must contain at least 1 tag (maximum tags: 16).</span><span class="sxs-lookup"><span data-stu-id="0d180-123">Container images must contain at least 1 tag (maximum tags: 16).</span></span><ul> <li><span data-ttu-id="0d180-124">For more information about tagging an image, visit the docker tag page located at [docs.docker.com/engine/reference/commandline/tag](https://docs.docker.com/engine/reference/commandline/tag).</span><span class="sxs-lookup"><span data-stu-id="0d180-124">For more information about tagging an image, visit the docker tag page located at [docs.docker.com/engine/reference/commandline/tag](https://docs.docker.com/engine/reference/commandline/tag).</span></span></li> </ul> |  


## <a name="next-steps"></a><span data-ttu-id="0d180-125">Next Steps</span><span class="sxs-lookup"><span data-stu-id="0d180-125">Next Steps</span></span>

<span data-ttu-id="0d180-126">If you haven't already done so,</span><span class="sxs-lookup"><span data-stu-id="0d180-126">If you haven't already done so,</span></span> 

- <span data-ttu-id="0d180-127">[Register](https://azuremarketplace.microsoft.com/sell) in the marketplace</span><span class="sxs-lookup"><span data-stu-id="0d180-127">[Register](https://azuremarketplace.microsoft.com/sell) in the marketplace</span></span>

<span data-ttu-id="0d180-128">If you're registered and are creating a new offer or working on an existing one,</span><span class="sxs-lookup"><span data-stu-id="0d180-128">If you're registered and are creating a new offer or working on an existing one,</span></span>

- <span data-ttu-id="0d180-129">[Log in to Cloud Partner Portal](https://cloudpartner.azure.com) to create or complete your offer</span><span class="sxs-lookup"><span data-stu-id="0d180-129">[Log in to Cloud Partner Portal](https://cloudpartner.azure.com) to create or complete your offer</span></span>
