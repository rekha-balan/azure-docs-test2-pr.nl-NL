---
title: Azure Container Registry authentication with service principals
description: Learn how to provide access to images in your private container registry by using an Azure Active Directory service principal.
services: container-registry
author: mmacy
manager: jeconnoc
ms.service: container-registry
ms.topic: article
ms.date: 04/23/2018
ms.author: marsma
ms.openlocfilehash: ffdf8af805ce7e5068ceef9a4b265ea00d36fc79
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856865"
---
# <a name="azure-container-registry-authentication-with-service-principals"></a><span data-ttu-id="c9ffb-103">Azure Container Registry authentication with service principals</span><span class="sxs-lookup"><span data-stu-id="c9ffb-103">Azure Container Registry authentication with service principals</span></span>

<span data-ttu-id="c9ffb-104">You can use an Azure Active Directory (Azure AD) service principal to provide container image `docker push` and `pull` access to your container registry.</span><span class="sxs-lookup"><span data-stu-id="c9ffb-104">You can use an Azure Active Directory (Azure AD) service principal to provide container image `docker push` and `pull` access to your container registry.</span></span> <span data-ttu-id="c9ffb-105">By using a service principal, you can provide access to "headless" services and applications.</span><span class="sxs-lookup"><span data-stu-id="c9ffb-105">By using a service principal, you can provide access to "headless" services and applications.</span></span>

## <a name="what-is-a-service-principal"></a><span data-ttu-id="c9ffb-106">What is a service principal?</span><span class="sxs-lookup"><span data-stu-id="c9ffb-106">What is a service principal?</span></span>

<span data-ttu-id="c9ffb-107">Azure AD *service principals* provide access to Azure resources within your subscription.</span><span class="sxs-lookup"><span data-stu-id="c9ffb-107">Azure AD *service principals* provide access to Azure resources within your subscription.</span></span> <span data-ttu-id="c9ffb-108">You can think of a service principal as a user identity for a service, where "service" is any application, service, or platform that needs access to the resources.</span><span class="sxs-lookup"><span data-stu-id="c9ffb-108">You can think of a service principal as a user identity for a service, where "service" is any application, service, or platform that needs access to the resources.</span></span> <span data-ttu-id="c9ffb-109">You can configure a service principal with access rights scoped only to those resources you specify.</span><span class="sxs-lookup"><span data-stu-id="c9ffb-109">You can configure a service principal with access rights scoped only to those resources you specify.</span></span> <span data-ttu-id="c9ffb-110">Then, you can configure your application or service to use the service principal's credentials to access those resources.</span><span class="sxs-lookup"><span data-stu-id="c9ffb-110">Then, you can configure your application or service to use the service principal's credentials to access those resources.</span></span>

<span data-ttu-id="c9ffb-111">In the context of Azure Container Registry, you can create an Azure AD service principal with pull, push and pull, or owner permissions to your private Docker registry in Azure.</span><span class="sxs-lookup"><span data-stu-id="c9ffb-111">In the context of Azure Container Registry, you can create an Azure AD service principal with pull, push and pull, or owner permissions to your private Docker registry in Azure.</span></span>

## <a name="why-use-a-service-principal"></a><span data-ttu-id="c9ffb-112">Why use a service principal?</span><span class="sxs-lookup"><span data-stu-id="c9ffb-112">Why use a service principal?</span></span>

<span data-ttu-id="c9ffb-113">By using an Azure AD service principal, you can provide scoped access to your private container registry.</span><span class="sxs-lookup"><span data-stu-id="c9ffb-113">By using an Azure AD service principal, you can provide scoped access to your private container registry.</span></span> <span data-ttu-id="c9ffb-114">You can create different service principals for each of your applications or services, each with tailored access rights to your registry.</span><span class="sxs-lookup"><span data-stu-id="c9ffb-114">You can create different service principals for each of your applications or services, each with tailored access rights to your registry.</span></span> <span data-ttu-id="c9ffb-115">And, because you can avoid sharing credentials between services and applications, you can rotate credentials or revoke access for only the service principal (and thus the application) you choose.</span><span class="sxs-lookup"><span data-stu-id="c9ffb-115">And, because you can avoid sharing credentials between services and applications, you can rotate credentials or revoke access for only the service principal (and thus the application) you choose.</span></span>

<span data-ttu-id="c9ffb-116">For example, your web application can use a service principal that provides it with image `pull` access only, while your build system can use a service principal that provides it with both `push` and `pull` access.</span><span class="sxs-lookup"><span data-stu-id="c9ffb-116">For example, your web application can use a service principal that provides it with image `pull` access only, while your build system can use a service principal that provides it with both `push` and `pull` access.</span></span> <span data-ttu-id="c9ffb-117">If development of your application changes hands, you can rotate its service principle credentials without affecting the build system.</span><span class="sxs-lookup"><span data-stu-id="c9ffb-117">If development of your application changes hands, you can rotate its service principle credentials without affecting the build system.</span></span>

## <a name="when-to-use-a-service-principal"></a><span data-ttu-id="c9ffb-118">When to use a service principal</span><span class="sxs-lookup"><span data-stu-id="c9ffb-118">When to use a service principal</span></span>

<span data-ttu-id="c9ffb-119">You should use a service principal to provide registry access in **headless scenarios**.</span><span class="sxs-lookup"><span data-stu-id="c9ffb-119">You should use a service principal to provide registry access in **headless scenarios**.</span></span> <span data-ttu-id="c9ffb-120">That is, any application, service, or script that must push or pull container images in an automated or otherwise unattended manner.</span><span class="sxs-lookup"><span data-stu-id="c9ffb-120">That is, any application, service, or script that must push or pull container images in an automated or otherwise unattended manner.</span></span>

<span data-ttu-id="c9ffb-121">For individual access to a registry, such as when you manually pull a container image to your development workstation, you should instead use your own [Azure AD identity](container-registry-authentication.md#individual-login-with-azure-ad) for registry access (for example, with [az acr login][az-acr-login]).</span><span class="sxs-lookup"><span data-stu-id="c9ffb-121">For individual access to a registry, such as when you manually pull a container image to your development workstation, you should instead use your own [Azure AD identity](container-registry-authentication.md#individual-login-with-azure-ad) for registry access (for example, with [az acr login][az-acr-login]).</span></span>

[!INCLUDE [container-registry-service-principal](../../includes/container-registry-service-principal.md)]

## <a name="sample-scripts"></a><span data-ttu-id="c9ffb-122">Sample scripts</span><span class="sxs-lookup"><span data-stu-id="c9ffb-122">Sample scripts</span></span>

<span data-ttu-id="c9ffb-123">You can find the preceding sample scripts for Azure CLI on GitHub, as well versions for Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c9ffb-123">You can find the preceding sample scripts for Azure CLI on GitHub, as well versions for Azure PowerShell:</span></span>

* <span data-ttu-id="c9ffb-124">[Azure CLI][acr-scripts-cli]</span><span class="sxs-lookup"><span data-stu-id="c9ffb-124">[Azure CLI][acr-scripts-cli]</span></span>
* <span data-ttu-id="c9ffb-125">[Azure PowerShell][acr-scripts-psh]</span><span class="sxs-lookup"><span data-stu-id="c9ffb-125">[Azure PowerShell][acr-scripts-psh]</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9ffb-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="c9ffb-126">Next steps</span></span>

<span data-ttu-id="c9ffb-127">Once you have a service principal that you've granted access to your container registry, you can use its credentials in your applications and services for registry interaction.</span><span class="sxs-lookup"><span data-stu-id="c9ffb-127">Once you have a service principal that you've granted access to your container registry, you can use its credentials in your applications and services for registry interaction.</span></span>

<span data-ttu-id="c9ffb-128">While configuring individual applications to use service principal credentials is outside the scope of this article, you can find instructions for some specific services and platforms here:</span><span class="sxs-lookup"><span data-stu-id="c9ffb-128">While configuring individual applications to use service principal credentials is outside the scope of this article, you can find instructions for some specific services and platforms here:</span></span>

* [<span data-ttu-id="c9ffb-129">Authenticate with Azure Container Registry from Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="c9ffb-129">Authenticate with Azure Container Registry from Azure Kubernetes Service (AKS)</span></span>](container-registry-auth-aks.md)
* [<span data-ttu-id="c9ffb-130">Authenticate with Azure Container Registry from Azure Container Instances (ACI)</span><span class="sxs-lookup"><span data-stu-id="c9ffb-130">Authenticate with Azure Container Registry from Azure Container Instances (ACI)</span></span>](container-registry-auth-aci.md)

<!-- LINKS - External -->
[acr-scripts-cli]: https://github.com/Azure/azure-docs-cli-python-samples/tree/master/container-registry
[acr-scripts-psh]: https://github.com/Azure/azure-docs-powershell-samples/tree/master/container-registry

<!-- LINKS - Internal -->
[az-acr-login]: /cli/azure/acr#az-acr-login