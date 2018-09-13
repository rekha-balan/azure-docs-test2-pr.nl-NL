---
title: Azure Resource Manager template samples - Azure Container Instances
description: Azure Resource Manager template samples for Azure Container Instances
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 05/17/2018
ms.author: marsma
ms.openlocfilehash: fcc2e6c52e773d95bcdfe43d881fce036fae6513
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856233"
---
# <a name="azure-resource-manager-templates-for-azure-container-instances"></a><span data-ttu-id="0298c-103">Azure Resource Manager templates for Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="0298c-103">Azure Resource Manager templates for Azure Container Instances</span></span>

<span data-ttu-id="0298c-104">The following sample templates deploy container instances in various configurations.</span><span class="sxs-lookup"><span data-stu-id="0298c-104">The following sample templates deploy container instances in various configurations.</span></span>

<span data-ttu-id="0298c-105">For deployment options, see the [Deployment](#deployment) section.</span><span class="sxs-lookup"><span data-stu-id="0298c-105">For deployment options, see the [Deployment](#deployment) section.</span></span> <span data-ttu-id="0298c-106">If you'd like to create your own templates, the Azure Container Instances [Resource Manager template reference][ref] details template format and available properties.</span><span class="sxs-lookup"><span data-stu-id="0298c-106">If you'd like to create your own templates, the Azure Container Instances [Resource Manager template reference][ref] details template format and available properties.</span></span>

## <a name="sample-templates"></a><span data-ttu-id="0298c-107">Sample templates</span><span class="sxs-lookup"><span data-stu-id="0298c-107">Sample templates</span></span>

| | |
|-|-|
| <span data-ttu-id="0298c-108">**Applications**</span><span class="sxs-lookup"><span data-stu-id="0298c-108">**Applications**</span></span> ||
| <span data-ttu-id="0298c-109">[Wordpress][app-wp]</span><span class="sxs-lookup"><span data-stu-id="0298c-109">[Wordpress][app-wp]</span></span> | <span data-ttu-id="0298c-110">Creates a WordPress website and its MySQL database in a container instance.</span><span class="sxs-lookup"><span data-stu-id="0298c-110">Creates a WordPress website and its MySQL database in a container instance.</span></span> <span data-ttu-id="0298c-111">The WordPress site content and MySQL database are persisted to an Azure Files share.</span><span class="sxs-lookup"><span data-stu-id="0298c-111">The WordPress site content and MySQL database are persisted to an Azure Files share.</span></span> |
| <span data-ttu-id="0298c-112">[MS NAV with SQL Server and IIS][app-nav]</span><span class="sxs-lookup"><span data-stu-id="0298c-112">[MS NAV with SQL Server and IIS][app-nav]</span></span> | <span data-ttu-id="0298c-113">Deploys a single Windows container with a fully featured self-contained Dynamics NAV / Dynamics 365 Business Central environment.</span><span class="sxs-lookup"><span data-stu-id="0298c-113">Deploys a single Windows container with a fully featured self-contained Dynamics NAV / Dynamics 365 Business Central environment.</span></span> |
| <span data-ttu-id="0298c-114">**Volumes**</span><span class="sxs-lookup"><span data-stu-id="0298c-114">**Volumes**</span></span> ||
| <span data-ttu-id="0298c-115">[emptyDir][vol-emptydir]</span><span class="sxs-lookup"><span data-stu-id="0298c-115">[emptyDir][vol-emptydir]</span></span> | <span data-ttu-id="0298c-116">Deploys two Linux containers that share an emptyDir volume.</span><span class="sxs-lookup"><span data-stu-id="0298c-116">Deploys two Linux containers that share an emptyDir volume.</span></span> |
| <span data-ttu-id="0298c-117">[gitRepo][vol-gitrepo]</span><span class="sxs-lookup"><span data-stu-id="0298c-117">[gitRepo][vol-gitrepo]</span></span> | <span data-ttu-id="0298c-118">Deploys a Linux container that clones a GitHub repo and mounts it as a volume.</span><span class="sxs-lookup"><span data-stu-id="0298c-118">Deploys a Linux container that clones a GitHub repo and mounts it as a volume.</span></span> |
| <span data-ttu-id="0298c-119">[secret][vol-secret]</span><span class="sxs-lookup"><span data-stu-id="0298c-119">[secret][vol-secret]</span></span> | <span data-ttu-id="0298c-120">Deploys a Linux container with a PFX cert mounted as a secret volume.</span><span class="sxs-lookup"><span data-stu-id="0298c-120">Deploys a Linux container with a PFX cert mounted as a secret volume.</span></span> |
| <span data-ttu-id="0298c-121">**Networking**</span><span class="sxs-lookup"><span data-stu-id="0298c-121">**Networking**</span></span> ||
| <span data-ttu-id="0298c-122">[UDP-exposed container][net-udp]</span><span class="sxs-lookup"><span data-stu-id="0298c-122">[UDP-exposed container][net-udp]</span></span> | <span data-ttu-id="0298c-123">Deploys a Windows or Linux container that exposes a UDP port.</span><span class="sxs-lookup"><span data-stu-id="0298c-123">Deploys a Windows or Linux container that exposes a UDP port.</span></span> |
| <span data-ttu-id="0298c-124">[Linux container with public IP][net-publicip]</span><span class="sxs-lookup"><span data-stu-id="0298c-124">[Linux container with public IP][net-publicip]</span></span> | <span data-ttu-id="0298c-125">Deploys a single Linux container accessible via a public IP.</span><span class="sxs-lookup"><span data-stu-id="0298c-125">Deploys a single Linux container accessible via a public IP.</span></span> |
| <span data-ttu-id="0298c-126">**Azure resources**</span><span class="sxs-lookup"><span data-stu-id="0298c-126">**Azure resources**</span></span> ||
| <span data-ttu-id="0298c-127">[Create Azure Storage account and Files share][az-files]</span><span class="sxs-lookup"><span data-stu-id="0298c-127">[Create Azure Storage account and Files share][az-files]</span></span> | <span data-ttu-id="0298c-128">Uses the Azure CLI in a container instance to create a storage account and an Azure Files share.</span><span class="sxs-lookup"><span data-stu-id="0298c-128">Uses the Azure CLI in a container instance to create a storage account and an Azure Files share.</span></span>

## <a name="deployment"></a><span data-ttu-id="0298c-129">Deployment</span><span class="sxs-lookup"><span data-stu-id="0298c-129">Deployment</span></span>

<span data-ttu-id="0298c-130">You have several options for deploying resources with Resource Manager templates:</span><span class="sxs-lookup"><span data-stu-id="0298c-130">You have several options for deploying resources with Resource Manager templates:</span></span>

<span data-ttu-id="0298c-131">[Azure CLI][deploy-cli]</span><span class="sxs-lookup"><span data-stu-id="0298c-131">[Azure CLI][deploy-cli]</span></span>

<span data-ttu-id="0298c-132">[Azure PowerShell][deploy-powershell]</span><span class="sxs-lookup"><span data-stu-id="0298c-132">[Azure PowerShell][deploy-powershell]</span></span>

<span data-ttu-id="0298c-133">[Azure portal][deploy-portal]</span><span class="sxs-lookup"><span data-stu-id="0298c-133">[Azure portal][deploy-portal]</span></span>

<span data-ttu-id="0298c-134">[REST API][deploy-rest]</span><span class="sxs-lookup"><span data-stu-id="0298c-134">[REST API][deploy-rest]</span></span>

<!-- LINKS - External -->
[app-nav]: https://github.com/Azure/azure-quickstart-templates/tree/master/101-aci-dynamicsnav
[app-wp]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-aci-wordpress
[az-files]: https://github.com/Azure/azure-quickstart-templates/tree/master/101-aci-storage-file-share
[net-publicip]: https://github.com/Azure/azure-quickstart-templates/tree/master/101-aci-linuxcontainer-public-ip
[net-udp]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-aci-udp
[repo]: https://github.com/Azure/azure-quickstart-templates
[vol-emptydir]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-aci-linuxcontainer-volume-emptydir
[vol-gitrepo]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-aci-linuxcontainer-volume-gitrepo
[vol-secret]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-aci-linuxcontainer-volume-secret

<!-- LINKS - Internal -->
[deploy-cli]: ../azure-resource-manager/resource-group-template-deploy-cli.md
[deploy-portal]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[deploy-powershell]: ../azure-resource-manager/resource-group-template-deploy.md
[deploy-rest]: ../azure-resource-manager/resource-group-template-deploy-rest.md
[ref]: /azure/templates/microsoft.containerinstance/containergroups